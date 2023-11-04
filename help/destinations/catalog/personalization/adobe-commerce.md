---
title: Connettore di destinazione Adobe Commerce
description: Scopri come i commercianti di Adobe Commerce e Real-Time CDP possono personalizzare l’esperienza di acquisto distribuendo contenuti e promozioni del sito altamente pertinenti, personalizzati per il pubblico dei clienti e creati e gestiti in Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: ba5a539603da656117c95d19c9e989ef0e252f82
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 4%

---

# Connessione Adobe Commerce {#adobe-commerce}

## Panoramica {#overview}

Il [!DNL Adobe Commerce] il connettore di destinazione consente di selezionare uno o più tipi di pubblico di Real-Time CDP da attivare nel [!DNL Adobe Commerce] per offrire agli acquirenti un&#39;esperienza dinamica e personalizzata. Entro [!DNL Adobe Commerce], puoi quindi selezionare i tipi di pubblico di Real-Time CDP per personalizzare offerte univoche nel carrello, ad esempio &quot;acquista 2 ottieni 1 gratis&quot;. Puoi anche visualizzare hero banner e modificare il prezzo dei prodotti attraverso offerte promozionali, tutte personalizzate per il pubblico di Adobe Real-Time CDP.

## Prerequisiti {#prerequisites}

Questo connettore è disponibile nel catalogo delle destinazioni per i clienti che hanno acquistato Real-Time CDP Prime o Ultimate e Adobe Commerce.

Per utilizzare questa connessione di destinazione, assicurati di avere accesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Con l’accesso alla console per sviluppatori, puoi visualizzare le informazioni sull’account del servizio e sulle credenziali necessarie per [completare la configurazione](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) dell’estensione in Adobe Commerce.
- [Adobe Commerce Cloud versione 2.4.4 o successiva](https://business.adobe.com/products/magento/magento-commerce.html)

Ad Experience Platform, crea quanto segue:

- [Schema](../../../xdm/schema/composition.md). Lo schema creato rappresenta i dati che intendi acquisire da Adobe Commerce. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html) informazioni su come creare uno schema contenente gruppi di campi specifici di Commerce.
- [Set di dati](../../../catalog/datasets/user-guide.md#create). Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati. Crea questo set di dati dallo schema creato in precedenza.
- [Datastream](../../../datastreams/overview.md#create). ID che consente il flusso di dati da Adobe Experience Platform ad altri prodotti Adobe DX. Questo ID deve essere associato a un sito web specifico all’interno della tua istanza Adobe Commerce specifica. Quando crei questo flusso di dati, specifica lo schema XDM creato in precedenza.

Dopo aver completato i prerequisiti, connettiti a [!DNL Commerce] destinazione.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi al [!DNL Adobe Commerce] destinazione:

1. In [Interfaccia della piattaforma](https://experience.adobe.com/platform/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.
1. Seleziona **[!UICONTROL Personalizzazione]**.
1. Seleziona la destinazione Adobe Commerce per evidenziarla, quindi seleziona **[!UICONTROL Configurazione]**.
1. Segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

- **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
- **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione. Questo campo è facoltativo.
- **[!UICONTROL Alias di integrazione]**: questo valore viene inviato all’SDK web per Experienci Platform come nome di oggetto JSON.
- **[!UICONTROL ID flusso di dati]**: questo determina quale flusso di dati di Raccolta dati contiene i tipi di pubblico inclusi nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Consulta [Configurazione di uno stream di dati](../../../datastreams/overview.md) per ulteriori dettagli.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i tipi di pubblico in [!DNL Commerce] destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e tipi di pubblico nelle destinazioni delle richieste di profilo](../../ui/activate-edge-personalization-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico [!DNL Commerce] destinazione.

## Passaggi successivi in [!DNL Adobe Commerce]

Ora che hai configurato [!DNL Commerce] all&#39;interno di Experienci Platform, è necessario installare [!DNL Audience Activation] estensione in [!DNL Commerce] e configurare [!DNL Commerce Admin] per importare i tipi di pubblico di Real-Time CDP creati. Consulta la [[!DNL Commerce] documentazione](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html) per ulteriori informazioni.

## Convalidare l’attivazione del pubblico in Commerce {#exported-data}

Dopo aver attivato i tipi di pubblico di Real-Time CDP sul tuo [!DNL Adobe Commerce] dell&#39;account, tali tipi di pubblico saranno disponibili quando si passa al _Amministratore_ barra laterale, quindi vai a **[!UICONTROL Clienti]** > **[!UICONTROL Pubblico Real-Time CDP]**.

![Dashboard di Real-Time CDP Audiences](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
