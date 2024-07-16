---
title: Connettore di destinazione Adobe Commerce
description: Scopri come i commercianti di Adobe Commerce e Real-Time CDP possono personalizzare l’esperienza di acquisto distribuendo contenuti e promozioni del sito altamente pertinenti, personalizzati per il pubblico dei clienti e creati e gestiti in Real-Time CDP.
exl-id: f7aa3c6c-ba7a-440c-a4d7-5d7b50dbbc0d
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---

# Connessione Adobe Commerce {#adobe-commerce}

## Panoramica {#overview}

Il connettore di destinazione [!DNL Adobe Commerce] consente di selezionare uno o più tipi di pubblico Real-Time CDP da attivare nell&#39;account [!DNL Adobe Commerce] per fornire un&#39;esperienza dinamica personalizzata agli acquirenti. All&#39;interno di [!DNL Adobe Commerce], puoi quindi selezionare i tipi di pubblico di Real-Time CDP per personalizzare offerte univoche nel carrello, ad esempio &quot;acquista 2 ottieni 1 gratis&quot;. Puoi anche visualizzare hero banner e modificare il prezzo dei prodotti attraverso offerte promozionali, tutte personalizzate per il pubblico di Adobe Real-Time CDP.

## Prerequisiti {#prerequisites}

Questo connettore è disponibile nel catalogo delle destinazioni per i clienti che hanno acquistato Real-Time CDP Prime o Ultimate e Adobe Commerce.

Per utilizzare questa connessione di destinazione, assicurati di avere accesso a:

- [Adobe Experience Platform](https://experience.adobe.com/)
- [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started/). Con l&#39;accesso alla console per sviluppatori, puoi visualizzare le informazioni sull&#39;account del servizio e sulle credenziali necessarie per [completare la configurazione](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html#configure-the-extension) dell&#39;estensione in Adobe Commerce.
- [Adobe Commerce Cloud versione 2.4.4 o successiva](https://business.adobe.com/products/magento/magento-commerce.html)

Ad Experience Platform, crea quanto segue:

- [Schema](../../../xdm/schema/composition.md). Lo schema creato rappresenta i dati che intendi acquisire da Adobe Commerce. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html) su come creare uno schema contenente gruppi di campi specifici di Commerce.
- [Set di dati](../../../catalog/datasets/user-guide.md#create). Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati. Crea questo set di dati dallo schema creato in precedenza.
- [Stream di dati](../../../datastreams/overview.md#create). ID che consente il flusso di dati da Adobe Experience Platform ad altri prodotti Adobe DX. Questo ID deve essere associato a un sito web specifico all’interno della tua istanza Adobe Commerce specifica. Quando crei questo flusso di dati, specifica lo schema XDM creato in precedenza.

Dopo aver completato i prerequisiti, connettersi alla destinazione [!DNL Commerce].

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi alla destinazione [!DNL Adobe Commerce]:

1. Nell&#39;interfaccia [Platform](https://experience.adobe.com/platform/), vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**.
1. Seleziona **[!UICONTROL Personalization]**.
1. Seleziona la destinazione Adobe Commerce per evidenziarla, quindi seleziona **[!UICONTROL Configurazione]**.
1. Segui i passaggi descritti nell&#39;[esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

- **[!UICONTROL Nome]**: immettere il nome preferito per la destinazione.
- **[!UICONTROL Descrizione]**: immetti una descrizione per la destinazione. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione. Questo campo è facoltativo.
- **[!UICONTROL Alias di integrazione]**: questo valore viene inviato all&#39;SDK Web Experience Platform come nome di oggetto JSON.
- **[!UICONTROL ID flusso di dati]**: determina quale flusso di dati della raccolta dati contiene i tipi di pubblico inclusi nella risposta alla pagina. Il menu a discesa mostra solo gli stream di dati in cui è abilitata la configurazione della destinazione. Per ulteriori dettagli, vedere [Configurazione di uno stream di dati](../../../datastreams/overview.md).

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attiva il pubblico nella destinazione [!DNL Commerce] {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Leggi [Attivare profili e tipi di pubblico nelle destinazioni delle richieste di profilo](../../ui/activate-edge-personalization-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico nella destinazione [!DNL Commerce].

## Passaggi successivi in [!DNL Adobe Commerce]

Dopo aver configurato la destinazione [!DNL Commerce] in Experience Platform, è necessario installare l&#39;estensione [!DNL Audience Activation] in [!DNL Commerce] e configurare [!DNL Commerce Admin] per importare i tipi di pubblico Real-Time CDP creati. Per ulteriori informazioni, consulta la [[!DNL Commerce] documentazione](https://experienceleague.adobe.com/docs/commerce-admin/customers/customers-menu/audience-activation.html).

## Convalidare l’attivazione del pubblico in Commerce {#exported-data}

Dopo aver attivato i tipi di pubblico di Real-Time CDP nell&#39;account [!DNL Adobe Commerce], tali tipi di pubblico saranno disponibili quando si passa alla barra laterale _Amministratore_, quindi si passa a **[!UICONTROL Clienti]** > **[!UICONTROL Pubblico Real-Time CDP]**.

![Dashboard tipi di pubblico di Real-Time CDP](../../assets/catalog/personalization/adobe-commerce/audience-library.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
