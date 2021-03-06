---
title: Rozwiązywanie typowych problemów w usłudze Azure Kubernetes Service
description: Dowiedz się, jak do rozwiązywania oraz usuwania typowych problemów w przypadku korzystania z usługi Azure Kubernetes Service (AKS)
services: container-service
author: sauryadas
ms.service: container-service
ms.topic: troubleshooting
ms.date: 08/13/2018
ms.author: saudas
ms.openlocfilehash: fd3d1c464c6f2d4cbecd715db0689581ca141769
ms.sourcegitcommit: e68df5b9c04b11c8f24d616f4e687fe4e773253c
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/20/2018
ms.locfileid: "53654074"
---
# <a name="aks-troubleshooting"></a>Rozwiązywanie problemów z usługi AKS

Podczas tworzenia lub zarządzanie klastrami usługi Azure Kubernetes Service (AKS) może czasami wystąpić problemy. Ten artykuł szczegółowo opisuje niektóre typowe problemy i kroki rozwiązywania problemów.

## <a name="in-general-where-do-i-find-information-about-debugging-kubernetes-problems"></a>Ogólnie rzecz biorąc, gdzie można znaleźć informacje o debugowaniu problemów Kubernetes?

Spróbuj [oficjalny przewodnik rozwiązywania problemów z klastrów Kubernetes](https://kubernetes.io/docs/tasks/debug-application-cluster/troubleshooting/).
Istnieje również [przewodnik rozwiązywania problemów z](https://github.com/feiskyer/kubernetes-handbook/blob/master/en/troubleshooting/index.md)opublikowanymi przez inżynier z firmy Microsoft do rozwiązywania problemów zasobników, węzły, klastrów i innych funkcji.

## <a name="im-getting-a-quota-exceeded-error-during-creation-or-upgrade-what-should-i-do"></a>Otrzymuję błąd "Przekroczono limit przydziału" podczas tworzenia lub uaktualniania. Co mam zrobić? 

Musisz [żądania rdzeni](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request).

## <a name="what-is-the-maximum-pods-per-node-setting-for-aks"></a>Co to jest ustawienie maksymalne zasobników na węzeł dla usługi AKS?

Ustawienie maksymalne zasobników każdego węzła jest domyślnie 30, jeśli musisz wdrożyć klaster usługi AKS w witrynie Azure portal.
Ustawienie maksymalne zasobników każdego węzła jest 110 domyślnie, jeśli musisz wdrożyć klaster usługi AKS w interfejsie wiersza polecenia platformy Azure. (Upewnij się, że używasz najnowszej wersji interfejsu wiersza polecenia platformy Azure). To ustawienie domyślne można zmienić za pomocą `–-max-pods` znacznik w `az aks create` polecenia.

## <a name="im-getting-an-insufficientsubnetsize-error-while-deploying-an-aks-cluster-with-advanced-networking-what-should-i-do"></a>Otrzymuję błąd insufficientSubnetSize podczas wdrażania klastra usługi AKS z zaawansowany siecią. Co mam zrobić?

W przypadku niestandardowych usługi Azure Virtual Network opcji dla sieci podczas tworzenia usługi AKS wtyczki Azure Container sieci interfejsu (CNI) jest używany dla zarządzania adresami IP (IPAM). Liczba węzłów w klastrze AKS może być dowolnym miejscu od 1 do 100. Oparte na poprzedniej sekcji, rozmiar podsieci powinien być większy niż iloczyn liczby węzłów i maksymalna zasobników w każdym węźle. Relacje mogą być wyrażone w ten sposób: rozmiar podsieci > Liczba węzłów w klastrze * maksymalna zasobników w każdym węźle.

## <a name="my-pod-is-stuck-in-crashloopbackoff-mode-what-should-i-do"></a>Moje zasobnika została zablokowana w trybie CrashLoopBackOff. Co mam zrobić?

Może to być różne przyczyny zasobnika ustawiany jest zablokowana w trybie. Użytkownik może wyglądać na:

* Zasobnik, za pomocą `kubectl describe pod <pod-name>`.
* Dzienniki, korzystając z `kubectl log <pod-name>`.

Aby uzyskać więcej informacji na temat rozwiązywania problemów pod zobacz [debugowania aplikacji](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/#debugging-pods).

## <a name="im-trying-to-enable-rbac-on-an-existing-cluster-how-can-i-do-that"></a>Próbuję włączyć RBAC w istniejącym klastrze. Jak można zrobić?

Niestety włączania kontroli dostępu opartej na rolach (RBAC) na istniejących klastrów nie jest obsługiwana w tej chwili. Należy jawnie utworzyć nowych klastrów. Jeśli używasz interfejsu wiersza polecenia, RBAC jest domyślnie włączona. Jeśli używasz portalu usługi AKS, przycisk przełączania, aby umożliwić RBAC jest dostępna w przepływ pracy tworzenia.

## <a name="i-created-a-cluster-with-rbac-enabled-by-using-either-the-azure-cli-with-defaults-or-the-azure-portal-and-now-i-see-many-warnings-on-the-kubernetes-dashboard-the-dashboard-used-to-work-without-any-warnings-what-should-i-do"></a>Po utworzeniu klastra przy użyciu RBAC włączana przy użyciu dowolnego wiersza polecenia platformy Azure przy użyciu wartości domyślnych lub witryny Azure portal, a teraz zobaczyć wiele ostrzeżenia na pulpicie nawigacyjnym platformy Kubernetes. Pulpit nawigacyjny pozwala działać bez ostrzeżenia. Co mam zrobić?

Przyczyna ostrzeżenia na pulpicie nawigacyjnym jest klastra jest teraz włączone wraz z RBAC i do niego dostęp ma domyślnie wyłączone. Ogólnie rzecz biorąc to podejście jest dobrym rozwiązaniem, ponieważ narażenia domyślnego pulpitu nawigacyjnego dla wszystkich użytkowników klastra może prowadzić do zagrożenia bezpieczeństwa. Jeśli nadal chcesz włączyć Pulpit nawigacyjny, wykonaj kroki opisane w [ten wpis w blogu](https://pascalnaber.wordpress.com/2018/06/17/access-dashboard-on-aks-with-rbac-enabled/).

## <a name="i-cant-connect-to-the-dashboard-what-should-i-do"></a>Nie można nawiązać pulpitu nawigacyjnego. Co mam zrobić?

Najprostszym sposobem uzyskania dostępu do usługi spoza klastra jest uruchomienie `kubectl proxy`, które serwery proxy żądania wysyłane do localhost port 8001 do serwera interfejsu API rozwiązania Kubernetes. W efekcie serwera interfejsu API można serwera proxy do usługi: `http://localhost:8001/api/v1/namespaces/kube-system/services/kubernetes-dashboard/proxy/#!/node?namespace=default`.

Jeśli nie widzisz pulpit nawigacyjny platformy Kubernetes, sprawdź, czy `kube-proxy` zasobnik jest uruchomiony w `kube-system` przestrzeni nazw. Jeśli nie jest w stanie uruchomienia, usunąć zasobnik i zostanie uruchomiona ponownie.

## <a name="i-cant-get-logs-by-using-kubectl-logs-or-i-cant-connect-to-the-api-server-im-getting-error-from-server-error-dialing-backend-dial-tcp-what-should-i-do"></a>Nie mogę uzyskać dzienniki przy użyciu narzędzia kubectl dzienników lub nie można nawiązać połączenia serwera interfejsu API. Otrzymuję "błąd z serwera: błąd podczas wybierania zaplecza: wybierania tcp..." Co mam zrobić?

Upewnij się, że domyślną sieciową grupę zabezpieczeń (NSG) nie jest modyfikowana i że port 22 jest otwarty dla połączenia do serwera interfejsu API. Sprawdź, czy `tunnelfront` zasobnik jest uruchomiony w `kube-system` przestrzeni nazw. Jeśli nie, Wymuś usunięcie zasobnik i zostanie uruchomiony ponownie.

## <a name="im-trying-to-upgrade-or-scale-and-am-getting-a-message-changing-property-imagereference-is-not-allowed-error--how-do-i-fix-this-problem"></a>I próbuję uaktualnienia lub skalowania i są zwracane "komunikat: Nie można zmienić właściwości "imageReference" "Wystąpił błąd.  Jak rozwiązać ten problem?

Użytkownik może się pojawiać ten błąd ponieważ znaczniki węzły agenta w ramach klastra usługi AKS został zmodyfikowany. Modyfikowanie i usuwanie tagów i innych właściwości zasobów w grupie zasobów MC_ * może prowadzić do nieoczekiwanych wyników. Modyfikowanie zasobów w grupie MC_ * w usłudze AKS klastra przerywa cel poziomu usług (SLO).

## <a name="how-do-i-renew-the-service-principal-secret-on-my-aks-cluster"></a>Jak odnowić klucz tajny jednostki usługi na mój klaster AKS?

Domyślnie klastry usługi AKS są tworzone przy użyciu nazwy głównej usługi czasu wygaśnięcia jeden rok. Jak blisko datę wygaśnięcia można zresetować poświadczenia, które mają rozszerzenie nazwy głównej usługi dla dodatkowy okres czasu.

Poniższy przykład wykonuje następujące czynności:

1. Pobiera identyfikator jednostki usługi z klastrem przy użyciu [az aks show](/cli/azure/aks#az-aks-show) polecenia.
1. Wyświetla klucz tajny klienta jednostki usługi przy użyciu [az ad sp poświadczeń listy](/cli/azure/ad/sp/credential#az-ad-sp-credential-list).
1. Rozszerza nazwy głównej usługi przy użyciu innego rok [az ad sp reset poświadczeń](/cli/azure/ad/sp/credential#az-ad-sp-credential-reset) polecenia. Klucz tajny klienta jednostki usługi musi pozostać taka sama dla klastra AKS, by działała poprawnie.

```azurecli
# Get the service principal ID of your AKS cluster.
sp_id=$(az aks show -g myResourceGroup -n myAKSCluster \
    --query servicePrincipalProfile.clientId -o tsv)

# Get the existing service principal client secret.
key_secret=$(az ad sp credential list --id $sp_id --query [].keyId -o tsv)

# Reset the credentials for your AKS service principal and extend for one year.
az ad sp credential reset \
    --name $sp_id \
    --password $key_secret \
    --years 1
```
