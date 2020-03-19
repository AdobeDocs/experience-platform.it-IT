---
title: Avvio rapido con Launch
seo-title: Avvio rapido dell’SDK Web per Adobe Experience Platform
description: Guida di avvio rapido per l’utilizzo dell’estensione SDK Web di Experience Platform per la raccolta dei dati
seo-description: Guida di avvio rapido per l’utilizzo dell’estensione SDK Web di Experience Platform per la raccolta dei dati
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Prerequisiti

>[!IMPORTANT]
>
>L’SDK Web per Adobe Experience Platform è attualmente in versione beta e non è disponibile per tutti gli utenti. La documentazione e la funzionalità sono soggette a modifiche.

Al momento, l’SDK Web per Adobe Experience Platform supporta solo l’invio di dati ad Adobe Experience Platform tramite XDM. Dovete soddisfare i seguenti prerequisiti.

- Accertati che sia attivato un dominio di [prime parti (CNAME)](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html) . Se hai già un CNAME per Analytics, devi usarlo.
- Accedere ad Adobe Experience Platform
- Usa la versione più recente del servizio ID visitatore

## Preparare la piattaforma

Per poter inviare dati ad Adobe Experience Platform, è necessario creare uno schema XDM e un dataset che utilizzino tale schema.

- [Create uno schema](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md) con i seguenti mixin:
   - Dettagli implementazione di ExperienceEvent
   - Dettagli ambiente ExperienceEvent
   - Dettagli Web ExperienceEvent
- Aggiungere il mixin SDK Web di Adobe Experience Platform allo schema creato
- [Creare un dataset](https://platform.adobe.com/dataset/overview) con lo schema in cui si desidera che i dati vengano inseriti

## Richiesta di un ID di configurazione

Per usare l’SDK devi disporre di un ID di configurazione. L&#39;ID di configurazione garantisce che i dati vengano indirizzati al posto giusto. Puoi ottenere un ID di configurazione dal tuo consulente o tramite Client Care. Avranno bisogno delle seguenti informazioni:

- **ID organizzazione:** Potete trovarlo utilizzando le istruzioni [qui](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- **ID set di dati:** Questa funzione è disponibile nell&#39;interfaccia utente del set di dati quando si fa clic su un set di dati
- **ID schema:** È disponibile nell’URL della schermata di creazione dello schema
- **Nome descrittivo:** Questo è il nome descrittivo che verrà utilizzato nelle interfacce future per questa configurazione

## Installa l’SDK in Launch

Accedete a Launch e installate l&#39; `AEP Web SDK` estensione. Durante l’installazione dell’SDK, ti verrà richiesto di configurare l’estensione. Immettete l’ID di configurazione richiesto in precedenza. L’estensione completa automaticamente l’ID organizzazione.

Per ulteriori dettagli sulle diverse opzioni di configurazione, consulta [Configurazione dell’SDK](../fundamentals/configuring-the-sdk.md).

## Invio di un evento

Dopo l&#39;installazione dell&#39;estensione, iniziate a inviare gli eventi aggiungendo un&#39;azione &quot;Send Beacon&quot; dall&#39;estensione AEP Web SDK. È consigliabile inviare almeno un evento ogni volta che una pagina viene caricata con l&#39;opzione &quot;si verifica all&#39;inizio di una visualizzazione&quot; selezionata.

Per ulteriori dettagli su come tenere traccia degli eventi, vedere [Tracciamento degli eventi](../fundamentals/tracking-events.md).

## Invio di dati

È possibile inviare dati che corrispondono allo schema creato in precedenza insieme agli eventi. Ad esempio, se possedete un sito commerciale e aggiungete il mixin commerce allo schema, invierete la struttura seguente quando un utente visualizza un prodotto.

```javascript
{
  "commerce": {
    "productListAdds": {
        "value":1
    }
  },
  "productListItems":{
      "name":"Floppy Green Hat",
      "SKU":"HATFLP123",
      "product":"1234567",
      "quantity":2
  }
}
```
