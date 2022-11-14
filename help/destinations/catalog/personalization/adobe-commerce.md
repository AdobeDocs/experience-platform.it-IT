---
title: (Beta) Connettore di destinazione Adobe Commerce
description: Scopri in che modo i commercianti Adobe Commerce e Real-Time CDP possono personalizzare l’esperienza di acquisto fornendo contenuti e promozioni del sito altamente pertinenti, personalizzati per i segmenti di clienti generati e gestiti all’interno di Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: 638a778d1d999ab6a1726333f9cde0a0b4fad57b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 1%

---

# (Beta) Connessione Adobe Commerce {#adobe-commerce}

## Panoramica {#overview}

>[!IMPORTANT]
> 
>La **[!UICONTROL Adobe Commerce]** Il connettore è in versione beta ed è disponibile solo per un numero selezionato di clienti.

La [!DNL Adobe Commerce] il connettore di destinazione consente di selezionare uno o più segmenti di Real-Time CDP da attivare nel [!DNL Adobe Commerce] per offrire un’esperienza personalizzata dinamica ai tuoi acquirenti. Within [!DNL Adobe Commerce], puoi quindi selezionare i segmenti Real-Time CDP per personalizzare offerte univoche nel carrello, ad esempio &quot;acquista 2 get 1 free&quot;. Puoi anche visualizzare banner eroi e modificare il prezzo del prodotto tramite offerte promozionali, tutte personalizzate per i segmenti Adobe Real-Time CDP.

<!--## Use cases {#use-cases}

To help you better understand how and when you should use the *YourDestination* destination, here are sample use cases that Adobe Experience Platform customers can solve by using this destination.

### Use case #1 {#use-case-1}

*For mobile messaging platforms:*

*A home rental and sales platform wants to push mobile notifications to customers' Android and iOS devices to let them know that there are 100 updated listings in the area where they previously searched for a rental.*

### Use case #2 {#use-case-2}

*For social network platforms:*

*An athletic apparel brand wants to reach existing customers through their social media accounts. The apparel brand can ingest email addresses from their own CRM to Adobe Experience Platform, build segments from their own offline data, and send these segments to YourDestination, to display ads in their customers' social media feeds.*-->

## Prerequisiti {#prerequisites}

Questa estensione è disponibile nel catalogo delle destinazioni per alcuni clienti beta che hanno acquistato Real-Time CDP Prime o Ultimate e Adobe Commerce.

I clienti beta devono avere accesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/)
- [Adobe Commerce Cloud versione 2.4.4 o successiva](https://business.adobe.com/products/magento/magento-commerce.html)

In Experience Platform, crea quanto segue:

- [Schema](../../../xdm/schema/composition.md). Lo schema creato rappresenta i dati che intendi acquisire da Adobe Commerce. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) informazioni su come creare uno schema contenente gruppi di campi specifici per Commerce.
- [Set di dati](../../../catalog/datasets/user-guide.md#create). Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati. Devi creare questo set di dati dallo schema creato in precedenza.
- [Datastream](../../../edge/datastreams/overview.md#create). ID che consente il flusso dei dati da Adobe Experience Platform ad altri prodotti DX di Adobe. Questo ID deve essere associato a un sito web specifico all&#39;interno della tua istanza Adobe Commerce specifica. Quando crei questo datastream, specifica lo schema XDM creato in precedenza.

Dopo aver completato i prerequisiti, collegati al [!DNL Commerce] destinazione.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi al [!DNL Adobe Commerce] destinazione:

1. In [Interfaccia di Platform](https://experience.adobe.com/platform/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.
1. Seleziona **[!UICONTROL Personalizzazione]**.
1. Seleziona la destinazione Adobe Commerce da evidenziare, quindi seleziona **[!UICONTROL Configurazione]**.
1. Segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

- **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
- **[!UICONTROL Descrizione]**: Inserisci una descrizione per la destinazione. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione. Questo campo è facoltativo.
- **[!UICONTROL Alias di integrazione]**: Questo valore viene inviato all’Experience Platform Web SDK come nome di oggetto JSON.
- **[!UICONTROL ID Datastream]**: Questo determina in quale datastream di raccolta dati i segmenti verranno inclusi nella risposta alla pagina. Il menu a discesa mostra solo i datastreams con la configurazione di destinazione abilitata. Vedi [Configurazione di un datastream](../../../edge/datastreams/overview.md) per ulteriori dettagli.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti nel [!DNL Commerce] destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di richieste di profilo](../../ui/activate-profile-request-destinations.md) per istruzioni su come attivare i segmenti di pubblico in [!DNL Commerce] destinazione.

## Passaggi successivi in [!DNL Adobe Commerce]

Ora che hai configurato il [!DNL Commerce] all’interno di Experience Platform, devi configurare il [!DNL Commerce Admin] per importare i segmenti Real-Time CDP creati. Consulta la sezione [[!DNL Commerce] documentazione](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/cart-rules/customer-segment-rtcdp.html) per saperne di più.

## Convalidare l’attivazione dell’audience in Commerce {#exported-data}

Dopo aver attivato i segmenti Real-Time CDP nel tuo [!DNL Adobe Commerce] vedrai questi segmenti disponibili nella sezione [!DNL Admin] quando crei una regola del prezzo del carrello:

![Amministratore Adobe Commerce](../../assets/catalog/personalization/adobe-commerce/rtcdp-in-admin.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
