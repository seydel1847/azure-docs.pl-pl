---
title: Wskazówki dotyczące ograniczania usługi Azure Key Vault
description: Ograniczania usługi Key Vault ogranicza liczbę równoczesnych wywołań, aby zapobiec nadmiernemu zużyciu zasobów.
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: ''
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.topic: conceptual
ms.date: 05/10/2018
ms.author: bryanla
ms.openlocfilehash: f119e4a5b5c5f97848c588636a3a707428abbd5b
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53082530"
---
# <a name="azure-key-vault-throttling-guidance"></a>Wskazówki dotyczące ograniczania usługi Azure Key Vault

Ograniczenie to proces zainicjowanych przez, który ogranicza liczbę równoczesnych wywołań do usługi Azure zapobiega nadmiernemu zużyciu zasobów. Usługa Azure Key Vault (AKV) została zaprojektowana do obsługi dużej liczby żądań. W przypadku zbyt dużej liczby żądań ograniczanie żądań klienta pomaga utrzymać optymalną wydajność i niezawodność usługi AKV.

Limity ograniczania różnią się zależnie od scenariusza. Na przykład jeśli przeprowadzasz dużej liczby zapisów możliwości ograniczania jest wyższa niż jeśli są wykonywane tylko operacje odczytu.

## <a name="how-does-key-vault-handle-its-limits"></a>Jak usługa Key Vault obsługuje zmuszenia?

Limity usługi w usłudze Key Vault, istnieją zapobiegania niewłaściwemu użyciu zasobów i zapewnienia dobrej jakości usługi dla wszystkich klientów usługi Key Vault. Po przekroczeniu progu usługi Key Vault ogranicza wszystkie dalsze żądania z tego klienta w okresie czasu. W takiej sytuacji usługa Key Vault zwraca kod stanu HTTP 429 (zbyt wiele żądań), i Niepowodzenie żądania. Ponadto żądań zakończonych niepowodzeniem, które zwracają 429 liczba kierunku limitów ograniczania przepływności śledzone przez usługę Key Vault. 

Jeśli masz biznesowe przypadku wyższych limitów ograniczania przepływności, skontaktuj się z nami.


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a>Jak ograniczyć aplikację w odpowiedzi na limity usługi

Poniżej przedstawiono **najlepsze praktyki** ograniczania aplikacji:
- Zmniejsz liczbę operacji na żądanie.
- Zmniejsz częstotliwość żądań.
- Należy unikać bezpośredniego ponownych prób. 
    - Wszystkie żądania są naliczane względem limitów użycia.

Podczas implementowania obsługi błędów aplikacji, należy użyć kod błędu HTTP 429 można wykrywać ograniczania po stronie klienta. Jeśli żądanie nie powiedzie się ponownie z kodem błędu HTTP 429, nadal występują ograniczenia usług platformy Azure. Nadal używać zalecanych klienta ograniczania metody, ponowieniem próby żądania, aż do skutku.

Poniżej przedstawiono kod, który implementuje wykładniczego wycofywania. 
```
     public async Task OnGetAsync()
     {
         Message = "Your application description page.";
         int retries = 0;
         bool retry = false;
         try
         {
             AzureServiceTokenProvider azureServiceTokenProvider = new AzureServiceTokenProvider();
             KeyVaultClient keyVaultClient = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(azureServiceTokenProvider.KeyVaultTokenCallback));
             var secret = await keyVaultClient.GetSecretAsync("https://<YourKeyVaultName>.vault.azure.net/secrets/AppSecret")
                     .ConfigureAwait(false);
             Message = secret.Value;

             /* The below do while logic is to handle throttling errors thrown by Azure Key Vault. It shows how to do exponential backoff which is the recommended client side throttling*/
             do
             {
                 long waitTime = Math.Min(getWaitTime(retries), 2000000);
                 secret = await keyVaultClient.GetSecretAsync("https://<YourKeyVaultName>.vault.azure.net/secrets/AppSecret")
                     .ConfigureAwait(false);
                 retry = false;
             } 
             while(retry && (retries++ < 10));
         }
         /// <exception cref="KeyVaultErrorException">
         /// Thrown when the operation returned an invalid status code
         /// </exception>
         catch (KeyVaultErrorException keyVaultException)
         {
             Message = keyVaultException.Message;
             if((int)keyVaultException.Response.StatusCode == 429)
                 retry = true;
         }
     }

     // This method implements exponential backoff incase of 429 errors from Azure Key Vault
     private static long getWaitTime(int retryCount)
     {
         long waitTime = ((long)Math.Pow(2, retryCount) * 100L);
         return waitTime;
     }
```

### <a name="recommended-client-side-throttling-method"></a>Zalecana metoda ograniczania przepływności po stronie klienta

Na kod błędu HTTP 429 Rozpocznij ograniczanie klienta przy użyciu podejścia wykładniczego wycofywania:

1. Poczekaj 1 sekundę, ponów próbę żądania
2. Jeśli nadal ograniczona poczekaj 2 sekundy, ponów próbę wykonania żądania
3. Jeśli nadal ograniczona oczekiwania 4 sekundy, ponów próbę wykonania żądania
4. Jeśli nadal ograniczona oczekiwania 8 sekund, ponów próbę wykonania żądania
5. Jeśli nadal ograniczona oczekiwania 16 sekund, ponów próbę wykonania żądania

W tym momencie użytkownik powinien nie uzyskać kody odpowiedzi HTTP 429.

## <a name="see-also"></a>Zobacz także

Dla bardziej orientację ograniczania przepustowości na Microsoft Cloud, zobacz [wzorzec ograniczania](https://docs.microsoft.com/azure/architecture/patterns/throttling).

