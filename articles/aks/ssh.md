---
title: SSH do węzłów klastra Azure Kubernetes Service (AKS)
description: Dowiedz się, jak utworzyć połączenie SSH z węzłów klastra Azure Kubernetes Service (AKS) dla zadania rozwiązywania problemów i konserwacji.
services: container-service
author: iainfoulds
ms.service: container-service
ms.topic: article
ms.date: 08/21/2018
ms.author: iainfou
ms.openlocfilehash: d687467e6bd64363c78f60064c6a17adbc5e0d1f
ms.sourcegitcommit: 11d8ce8cd720a1ec6ca130e118489c6459e04114
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52846135"
---
# <a name="connect-with-ssh-to-azure-kubernetes-service-aks-cluster-nodes-for-maintenance-or-troubleshooting"></a>Połącz przy użyciu protokołu SSH do usługi Azure Kubernetes Service (AKS) węzłów klastra z powodu konserwacji lub rozwiązywania problemów

W całym cyklu życia klastra Azure Kubernetes Service (AKS) może być konieczne do uzyskania dostępu do węzła usługi AKS. Dostęp może być konserwacji, zbieranie danych dziennika lub inne operacje dotyczące rozwiązywania problemów. Węzłów AKS są maszyny wirtualne systemu Linux, dzięki czemu można z nich korzystać przy użyciu protokołu SSH. Ze względów bezpieczeństwa węzłów AKS nie są połączone z Internetem.

W tym artykule pokazano, jak utworzyć połączenie SSH z węzłem AKS za pomocą prywatnych adresów IP.

## <a name="add-your-public-ssh-key"></a>Dodaj klucz publiczny SSH

Domyślnie zostaną wygenerowane klucze SSH, podczas tworzenia klastra usługi AKS. Jeśli nie podano klucze SSH podczas tworzenia klastra usługi AKS, należy dodać publicznych kluczy SSH do węzłów AKS. 

Aby dodać klucz SSH do węzłów AKS, wykonaj następujące czynności:

1. Pobierz nazwę grupy zasobów dla zasobów klastra usługi AKS przy użyciu [az aks show][az-aks-show]. Podaj własne podstawowej grupy zasobów i nazwę klastra AKS:

    ```azurecli
    az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv
    ```

1. Listy maszyn wirtualnych za pomocą grupy zasobów klastra usługi AKS [az vm list] [ az-vm-list] polecenia. Te maszyny wirtualne są węzłów AKS:

    ```azurecli
    az vm list --resource-group MC_myResourceGroup_myAKSCluster_eastus -o table
    ```

    Następujące przykładowe dane wyjściowe pokazuje węzłów AKS:

    ```
    Name                      ResourceGroup                                  Location
    ------------------------  ---------------------------------------------  ----------
    aks-nodepool1-79590246-0  MC_myResourceGroupAKS_myAKSClusterRBAC_eastus  eastus
    ```

1. Aby dodać kluczy SSH z węzłem, użyj [az vm użytkownik aktualizację] [ az-vm-user-update] polecenia. Podaj nazwę grupy zasobów, a następnie jeden z węzłów AKS uzyskanego w poprzednim kroku. Domyślnie, nazwa użytkownika dla węzłów AKS jest *azureuser*. Podaj lokalizację własne SSH ogólnodostępnej lokalizacji kluczy, takie jak *~/.ssh/id_rsa.pub*, lub Wklej zawartość klucza publicznego SSH:

    ```azurecli
    az vm user update \
      --resource-group MC_myResourceGroup_myAKSCluster_eastus \
      --name aks-nodepool1-79590246-0 \
      --username azureuser \
      --ssh-key-value ~/.ssh/id_rsa.pub
    ```

## <a name="get-the-aks-node-address"></a>Uzyskaj adres węzła usługi AKS

Węzłów AKS nie są widoczne publicznie w Internecie. Aby SSH do węzłów AKS należy użyć prywatnego adresu IP.

Wyświetl prywatny adres IP w usłudze AKS klastra węzła przy użyciu [az vm-— adresy ip] [ az-vm-list-ip-addresses] polecenia. Podaj własny AKS klastra Nazwa grupy zasobów uzyskane w ramach poprzedniego [az-aks-show] [ az-aks-show] krok:

```azurecli
az vm list-ip-addresses --resource-group MC_myAKSCluster_myAKSCluster_eastus -o table
```

Następujące przykładowe dane wyjściowe pokazuje prywatnych adresów IP węzłów AKS:

```
VirtualMachine            PrivateIPAddresses
------------------------  --------------------
aks-nodepool1-79590246-0  10.240.0.4
```

## <a name="create-the-ssh-connection"></a>Utwórz połączenie SSH

Aby utworzyć połączenie SSH z węzłem AKS, uruchamiasz zasobnik pomocnika w klastrze AKS. Pod tym pomocnika zapewnia dostęp protokołu SSH w klastrze i następnie dodatkowy dostęp do węzła SSH. Aby utworzyć i korzystać z tego zasobnika pomocnika, wykonaj następujące czynności:

1. Uruchom `debian` kontenera obrazów i do niej dołączyć sesji terminalowej. Ten kontener można utworzyć sesję SSH z dowolnego węzła w klastrze AKS:

    ```console
    kubectl run -it --rm aks-ssh --image=debian
    ```

1. Podstawowego obrazu systemu Debian nie zawiera składników protokołu SSH. Po sesji terminalowej jest podłączony do kontenera, należy zainstalować klienta SSH za pomocą `apt-get` w następujący sposób:

    ```console
    apt-get update && apt-get install openssh-client -y
    ```

1. W nowym oknie terminala nie jest podłączony do kontenera, listy zasobników przy użyciu klastra usługi AKS [kubectl get pods-] [ kubectl-get] polecenia. Zasobnik utworzony w poprzednim kroku, który zaczyna się od nazwy *aks — ssh*, jak pokazano w poniższym przykładzie:

    ```
    $ kubectl get pods
    
    NAME                       READY     STATUS    RESTARTS   AGE
    aks-ssh-554b746bcf-kbwvf   1/1       Running   0          1m
    ```

1. W pierwszym kroku w tym artykule dodano publiczny klucz SSH węzłów AKS. Teraz skopiuj klucz prywatny SSH do zasobników. Ten klucz prywatny jest używany do tworzenia protokołu SSH do węzłów AKS.

    Podaj własny *aks — ssh* nazwy zasobnika uzyskanego w poprzednim kroku. W razie potrzeby zmień *~/.ssh/id_rsa* lokalizacji klucz prywatny SSH:

    ```console
    kubectl cp ~/.ssh/id_rsa aks-ssh-554b746bcf-kbwvf:/id_rsa
    ```

1. W sesji terminalowej do kontenera, należy zaktualizować uprawnienia na skopiowany `id_rsa` klucza prywatnego SSH, tak, aby użytkownik tylko do odczytu:

    ```console
    chmod 0600 id_rsa
    ```

1. Teraz Utwórz połączenie SSH z węzłem usługi AKS. Ponownie jest domyślna nazwa użytkownika dla węzłów AKS *azureuser*. Zaakceptuj monit z połączeniem jest kontynuowane zgodnie z klucza SSH jest pierwszy zaufanych. Następnie otrzymują wierszu polecenia powłoki bash węzła usługi AKS:

    ```console
    $ ssh -i id_rsa azureuser@10.240.0.4
    
    ECDSA key fingerprint is SHA256:A6rnRkfpG21TaZ8XmQCCgdi9G/MYIMc+gFAuY9RUY70.
    Are you sure you want to continue connecting (yes/no)? yes
    Warning: Permanently added '10.240.0.4' (ECDSA) to the list of known hosts.
    
    Welcome to Ubuntu 16.04.5 LTS (GNU/Linux 4.15.0-1018-azure x86_64)
    
     * Documentation:  https://help.ubuntu.com
     * Management:     https://landscape.canonical.com
     * Support:        https://ubuntu.com/advantage
    
      Get cloud support with Ubuntu Advantage Cloud Guest:
        https://www.ubuntu.com/business/services/cloud
    
    [...]
    
    azureuser@aks-nodepool1-79590246-0:~$
    ```

## <a name="remove-ssh-access"></a>Usuń dostęp SSH

Po zakończeniu `exit` sesji SSH i następnie `exit` sesji interaktywnych kontenera. Po zamknięciu sesji to kontener, zasobnika używane dla dostępu SSH z klastrem AKS został usunięty.

## <a name="next-steps"></a>Kolejne kroki

Jeśli potrzebne są dodatkowe dane dotyczące rozwiązywania problemów, możesz to zrobić [wyświetlanie dzienników agenta kubelet] [ view-kubelet-logs] lub [wyświetlanie dzienników węzła głównego Kubernetes][view-master-logs].

<!-- EXTERNAL LINKS -->
[kubectl-get]: https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get

<!-- INTERNAL LINKS -->
[az-aks-show]: /cli/azure/aks#az-aks-show
[az-vm-list]: /cli/azure/vm#az-vm-list
[az-vm-user-update]: /cli/azure/vm/user#az-vm-user-update
[az-vm-list-ip-addresses]: /cli/azure/vm#az-vm-list-ip-addresses
[view-kubelet-logs]: kubelet-logs.md
[view-master-logs]: view-master-logs.md
