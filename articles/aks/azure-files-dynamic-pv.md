---
title: Dynamiczne tworzenie woluminu plików dla wielu zasobnikach w usłudze Azure Kubernetes Service (AKS)
description: Dowiedz się, jak dynamicznie utworzyć trwały wolumin za pomocą usługi Azure Files do użytku z wielu jednoczesnych zasobników w usłudze Azure Kubernetes Service (AKS)
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 10/08/2018
ms.author: iainfou
ms.openlocfilehash: 841c65fd8420fdfe681cb99ee7054cb4edd5fcd3
ms.sourcegitcommit: 803e66de6de4a094c6ae9cde7b76f5f4b622a7bb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/02/2019
ms.locfileid: "53968996"
---
# <a name="dynamically-create-and-use-a-persistent-volume-with-azure-files-in-azure-kubernetes-service-aks"></a>Dynamiczne tworzenie i trwały wolumin za pomocą usługi Azure Files w usłudze Azure Kubernetes Service (AKS)

Trwały wolumin reprezentuje fragment magazynu, który został aprowizowany do użytku z zasobników. Trwały wolumin może być używany przez jeden lub wiele zasobników i mogą być dynamicznie lub statycznie udostępniane. Jeśli wielu zasobnikach równoczesny dostęp do tego samego woluminu magazynu, można użyć usługi Azure Files, połączyć się przy użyciu [protokołu bloku komunikatów serwera (SMB)][smb-overview]. W tym artykule pokazano, jak dynamiczne tworzenie udziału plików platformy Azure do użycia przez wielu zasobnikach w klastrze usługi Azure Kubernetes Service (AKS).

Aby uzyskać więcej informacji na woluminach trwałego rozwiązania Kubernetes, zobacz [woluminy trwałe Kubernetes][kubernetes-volumes].

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym artykule założono, że masz istniejący klaster usługi AKS. Jeśli potrzebujesz klastra AKS, zobacz Przewodnik Szybki Start usługi AKS [przy użyciu wiersza polecenia platformy Azure] [ aks-quickstart-cli] lub [przy użyciu witryny Azure portal][aks-quickstart-portal].

Musisz również mieć zainstalowany i skonfigurowany interfejs wiersza polecenia platformy Azure w wersji 2.0.46 lub nowszej. Uruchom polecenie  `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczne będzie przeprowadzenie instalacji lub uaktualnienia, zobacz  [Instalowanie interfejsu wiersza polecenia platformy Azure][install-azure-cli].

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Gdy dynamiczne tworzenie udziału plików platformy Azure jako wolumin Kubernetes, wszystkich kont magazynu można tak długo, jak znajduje się w usłudze AKS **węzła** grupy zasobów. Ta grupa jest jednym z *MC_* prefiks, który został utworzony przez Inicjowanie obsługi administracyjnej zasobów klastra usługi AKS. Pobierz nazwę grupy zasobów przy użyciu [az aks show] [ az-aks-show] polecenia.

```azurecli
$ az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv

MC_myResourceGroup_myAKSCluster_eastus
```

Użyj [Tworzenie konta magazynu az] [ az-storage-account-create] polecenie, aby utworzyć konto magazynu.

Aktualizacja `--resource-group` nazwą grupy zasobów zebranych w ostatnim kroku i `--name` nazwę ulubionego. Podaj własny unikatowej nazwy konta magazynu:

```azurecli
az storage account create --resource-group MC_myResourceGroup_myAKSCluster_eastus --name mystorageaccount --sku Standard_LRS
```

> [!NOTE]
> W usłudze pliki Azure obecnie tylko pracę z magazynu w warstwie standardowa. Jeśli używasz usługi Premium storage, woluminu nie powiodło się aprowizacji.

## <a name="create-a-storage-class"></a>Utwórz klasę magazynu

Klasa magazynu jest używane do definiowania sposobu tworzenia udziału plików platformy Azure. Konto magazynu można określić w klasie. Jeśli nie określono konta magazynu, *skuName* i *lokalizacji* muszą być określone, i wszystkich kont magazynu w skojarzonej grupy zasobów są oceniane pod kątem dopasowania. Aby uzyskać więcej informacji na temat klasy magazynu w usłudze Kubernetes dla usługi Azure Files, zobacz [klasy magazynu w usłudze Kubernetes][kubernetes-storage-classes].

Utwórz plik o nazwie `azure-file-sc.yaml` i skopiuj następujące manifest przykładu. Aktualizacja *storageAccount* wartość z nazwą konta magazynu utworzonego w poprzednim kroku. Aby uzyskać więcej informacji na temat *mountOptions*, zobacz [opcje instalacji] [ mount-options] sekcji.

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
parameters:
  skuName: Standard_LRS
  storageAccount: mystorageaccount
```

Utwórz klasę magazynu za pomocą [zastosować kubectl] [ kubectl-apply] polecenia:

```console
kubectl apply -f azure-file-sc.yaml
```

## <a name="create-a-cluster-role-and-binding"></a>Tworzenie roli klastra i powiązania

Klastry usługi AKS używają Kubernetes kontroli dostępu opartej na rolach (RBAC) do limitu akcji, które mogą być wykonywane. *Role* zdefiniować uprawnienia, aby przyznać użytkownikom, i *powiązania* zastosować je do odpowiednich użytkowników. Te przypisania można zastosować do danej przestrzeni nazw lub dla całego klastra. Aby uzyskać więcej informacji, zobacz [autoryzacji RBAC przy użyciu][kubernetes-rbac].

Aby zezwolić na platformie Azure do utworzenia zasobów wymaganych magazynu, należy utworzyć *ClusterRole* i *ClusterRoleBinding*. Utwórz plik o nazwie `azure-pvc-roles.yaml` i skopiuj do poniższego kodu YAML:

```yaml
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: system:azure-cloud-provider
rules:
- apiGroups: ['']
  resources: ['secrets']
  verbs:     ['get','create']
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: system:azure-cloud-provider
roleRef:
  kind: ClusterRole
  apiGroup: rbac.authorization.k8s.io
  name: system:azure-cloud-provider
subjects:
- kind: ServiceAccount
  name: persistent-volume-binder
  namespace: kube-system
```

Przypisywanie uprawnień za pomocą [zastosować kubectl] [ kubectl-apply] polecenia:

```console
kubectl apply -f azure-pvc-roles.yaml
```

## <a name="create-a-persistent-volume-claim"></a>Tworzenie oświadczenia trwały wolumin

Oświadczenie trwały wolumin (PVC) używa obiektu klasy magazynu, aby dynamicznie aprowizuj udziału plików platformy Azure. Poniższego kodu YAML może służyć do tworzenia oświadczeń trwały wolumin *5GB* w rozmiarze *ReadWriteMany* dostępu. Aby uzyskać więcej informacji na temat trybów dostępu, zobacz [trwały wolumin Kubernetes] [ access-modes] dokumentacji.

Teraz Utwórz plik o nazwie `azure-file-pvc.yaml` i skopiuj do poniższego kodu YAML. Upewnij się, że *storageClassName* odpowiada klasę magazynu utworzone w poprzednim kroku:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azurefile
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: azurefile
  resources:
    requests:
      storage: 5Gi
```

Tworzenie oświadczenia trwały wolumin z [zastosować kubectl] [ kubectl-apply] polecenia:

```console
kubectl apply -f azure-file-pvc.yaml
```

Po zakończeniu zostanie utworzony udział plików. Wpisie tajnym rozwiązania Kubernetes jest tworzona zawierający informacje o połączeniu oraz poświadczenia. Możesz użyć [kubectl get-] [ kubectl-get] polecenie, aby wyświetlić stan PVC:

```
$ kubectl get pvc azurefile

NAME        STATUS    VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
azurefile   Bound     pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477   5Gi        RWX            azurefile      5m
```

## <a name="use-the-persistent-volume"></a>Użyj trwały wolumin

Poniższego kodu YAML tworzy zasobnik, który używa oświadczeń trwały wolumin *azurefile* zainstalować udział plików platformy Azure w */mnt/azure* ścieżki.

Utwórz plik o nazwie `azure-pvc-files.yaml`, a następnie skopiuj do poniższego kodu YAML. Upewnij się, że *claimName* odpowiada PVC utworzony w poprzednim kroku.

```yaml
kind: Pod
apiVersion: v1
metadata:
  name: mypod
spec:
  containers:
  - name: mypod
    image: nginx:1.15.5
    resources:
      requests:
        cpu: 100m
        memory: 128Mi
      limits:
        cpu: 250m
        memory: 256Mi
    volumeMounts:
    - mountPath: "/mnt/azure"
      name: volume
  volumes:
    - name: volume
      persistentVolumeClaim:
        claimName: azurefile
```

Utwórz zasobnik za pomocą [zastosować kubectl] [ kubectl-apply] polecenia.

```console
kubectl apply -f azure-pvc-files.yaml
```

Masz teraz uruchomiony zasobnik z udziałem plików platformy Azure zainstalowany w */mnt/azure* katalogu. Ta konfiguracja może być moment zapoznanie się tym zasobniku za pośrednictwem `kubectl describe pod mypod`. Następujące dane wyjściowe skróconego przykładu przedstawia wolumin zainstalowany w kontenerze:

```
Containers:
  mypod:
    Container ID:   docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e
    Image:          nginx:1.15.5
    Image ID:       docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424
    State:          Running
      Started:      Wed, 15 Aug 2018 22:22:27 +0000
    Ready:          True
    Mounts:
      /mnt/azure from volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro)
[...]
Volumes:
  volume:
    Type:       PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
    ClaimName:  azurefile
    ReadOnly:   false
[...]
```

## <a name="mount-options"></a>Opcje instalacji

Domyślne *fileMode* i *dirMode* wartości różnią się między wersjami usługi Kubernetes, zgodnie z opisem w poniższej tabeli.

| version | wartość |
| ---- | ---- |
| v1.6.x, v1.7.x | 0777 |
| v1.8.0-v1.8.5 | 0700 |
| V1.8.6 lub nowszy | 0755 |
| v1.9.0 | 0700 |
| V1.9.1 lub nowszy | 0755 |

Jeśli przy użyciu klastra wersji 1.8.5 lub nowszej i dynamiczne utworzenie trwały wolumin z klasą magazynu, opcje instalacji może być określony dla obiektu klasy magazynowania. Poniższy przykład ustawia *0777*:

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
parameters:
  skuName: Standard_LRS
```

Jeśli przy użyciu klastra wersji 1.8.5 lub nowszej i statycznie tworzenia obiektu trwały wolumin, opcje instalacji muszą być określone w *PersistentVolume* obiektu. Aby uzyskać więcej informacji na temat tworzenia statycznie trwały wolumin, zobacz [statyczne woluminy trwałe][pv-static].

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: azurefile
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteMany
  azureFile:
    secretName: azure-secret
    shareName: azurefile
    readOnly: false
  mountOptions:
  - dir_mode=0777
  - file_mode=0777
  - uid=1000
  - gid=1000
```

Jeśli przy użyciu klastra wersji 1.8.0 - 1.8.4, kontekstu zabezpieczeń można określić za pomocą *nazwa_użytkownika* wartość *0*. Aby uzyskać więcej informacji w kontekście zabezpieczeń zasobników, zobacz [skonfigurować kontekstu zabezpieczeń][kubernetes-security-context].

## <a name="next-steps"></a>Kolejne kroki

Dowiedz się więcej o woluminy trwałe Kubernetes za pomocą usługi Azure Files.

> [!div class="nextstepaction"]
> [Wtyczka usługi Kubernetes dla usługi Azure Files][kubernetes-files]

<!-- LINKS - external -->
[access-modes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes
[kubectl-apply]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply
[kubectl-describe]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get
[kubernetes-files]: https://github.com/kubernetes/examples/blob/master/staging/volumes/azure_file/README.md
[kubernetes-secret]: https://kubernetes.io/docs/concepts/configuration/secret/
[kubernetes-security-context]: https://kubernetes.io/docs/tasks/configure-pod-container/security-context/
[kubernetes-storage-classes]: https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file
[kubernetes-volumes]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/
[pv-static]: https://kubernetes.io/docs/concepts/storage/persistent-volumes/#static
[kubernetes-rbac]: https://kubernetes.io/docs/reference/access-authn-authz/rbac/
[smb-overview]: /windows/desktop/FileIO/microsoft-smb-protocol-and-cifs-protocol-overview

<!-- LINKS - internal -->
[az-group-create]: /cli/azure/group#az-group-create
[az-group-list]: /cli/azure/group#az-group-list
[az-resource-show]: /cli/azure/aks#az-aks-show
[az-storage-account-create]: /cli/azure/storage/account#az-storage-account-create
[az-storage-create]: /cli/azure/storage/account#az-storage-account-create
[az-storage-key-list]: /cli/azure/storage/account/keys#az-storage-account-keys-list
[az-storage-share-create]: /cli/azure/storage/share#az-storage-share-create
[mount-options]: #mount-options
[aks-quickstart-cli]: kubernetes-walkthrough.md
[aks-quickstart-portal]: kubernetes-walkthrough-portal.md
[install-azure-cli]: /cli/azure/install-azure-cli
[az-aks-show]: /cli/azure/aks#az-aks-show
