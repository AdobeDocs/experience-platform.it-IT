---
title: Connessione TikTok
description: Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le campagne pubblicitarie. Questi tipi di pubblico possono essere costituiti da persone che hanno visitato il tuo sito web o interagito con il tuo contenuto. Invia in modo rapido e sicuro il pubblico desiderato da Adobe Experience Platform a TikTok utilizzando l’integrazione in tempo reale di Adobe con TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 82ff222d22255b9c99de76111d25d4a3cf6f2d5c
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 4%

---

# Connessione TikTok

## Panoramica {#overview}

Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le campagne pubblicitarie. Questi tipi di pubblico possono essere costituiti da persone che hanno visitato il tuo sito web o interagito con il tuo contenuto. Invia in modo rapido e sicuro il pubblico desiderato da Adobe Experience Platform a TikTok utilizzando l’integrazione in tempo reale di Adobe con TikTok Ads Manager. Per ulteriori informazioni, visitare il [Centro assistenza commerciale di TikTok](https://ads.tiktok.com/help/article/audiences).

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team TikTok. Per richieste di informazioni o richieste di aggiornamento, contattale direttamente all&#39;indirizzo [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione TikTok, ecco un caso d’uso di esempio per i clienti Adobe Experience Platform.

### Caso d’uso {#use-case-1}

Un marchio di abbigliamento sportivo vuole raggiungere i clienti esistenti attraverso i loro account di social media. Il marchio di abbigliamento può acquisire indirizzi e-mail dal proprio CRM per Adobe Experience Platform, creare tipi di pubblico dai propri dati offline e inviare tali tipi di pubblico a TikTok per visualizzare annunci nei feed di social media dei propri clienti.

## Prerequisiti {#prerequisites}

È necessario disporre dell&#39;accesso [!DNL Admin] o [!DNL Operator] all&#39;account TikTok Ads Manager a cui si desidera inviare i tipi di pubblico. Ulteriori istruzioni sono disponibili nel [Centro assistenza TikTok](https://ads.tiktok.com/help/article/add-users-tiktok-business-center).

Prima di inviare i dati all&#39;account TikTok Ads Manager, devi concedere l&#39;autorizzazione Adobe Experience Platform per accedere all&#39;account annuncio per `Audience Management`. Questa autorizzazione può essere fornita da [inserendo il tuo ID Ads Manager](#authenticate) nell&#39;interfaccia utente di Experience Platform e concedendo l&#39;autorizzazione dopo essere stato reindirizzato al tuo account TikTok Ads Manager.

## Identità supportate {#supported-identities}

TikTok supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. I valori GAID con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. I valori IDFA con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| Numero di telefono | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform e devono essere in formato E.164. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| E-mail | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sì | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Tutte le altre origini del pubblico | Sì | Questa categoria include tutte le origini del pubblico al di fuori dei tipi di pubblico generati tramite [!DNL Segmentation Service]. Leggi informazioni sulle [diverse origini del pubblico](/help/segmentation/ui/audience-portal.md#customize). Alcuni esempi includono: <ul><li> i tipi di pubblico per caricamento personalizzati [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV,</li><li> pubblico simile, </li><li> pubblico federato, </li><li> tipi di pubblico generati in altre app di Experience Platform come Adobe Journey Optimizer, </li><li> e altro ancora. </li></ul> |
| [!DNL Federated Audience Composition] | Sì | Tipi di pubblico importati in Experience Platform tramite [Federated Audience Composition](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/start/audiences). |

{style="table-layout:auto"}



Tipi di pubblico supportati per tipo di dati sul pubblico:

| Tipo di dati del pubblico | Supportato | Descrizione | Casi d’uso |
|--------------------|-----------|-------------|-----------|
| [Tipi di pubblico per persone](/help/segmentation/types/people-audiences.md) | Sì | In base ai profili dei clienti, consente di eseguire il targeting di gruppi specifici di persone per campagne di marketing. | Acquirenti frequenti, abbandoni del carrello |
| [Pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti all’interno di organizzazioni specifiche per strategie di marketing basate sull’account. | Marketing B2B |
| [Pubblico potenziale](/help/segmentation/types/prospect-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti che non sono ancora clienti, ma che condividono alcune caratteristiche con il tuo pubblico di destinazione. | Ricerca di dati di terze parti |
| [Esportazioni set di dati](/help/catalog/datasets/overview.md) | No | Raccolte di dati strutturati archiviati nel Data Lake di Adobe Experience Platform. | Reporting, flussi di lavoro di data science |

{style="table-layout:auto"}


## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione TikTok. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, verrai reindirizzato per accedere al tuo account [!DNL TikTok Ads Manager] e autorizzare Adobe a gestire i tipi di pubblico per tuo conto.

![Selezione autorizzazioni TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Immagine dell&#39;interfaccia utente di TikTok per la selezione delle autorizzazioni")

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Dettagli della connessione di destinazione](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Immagine dell&#39;interfaccia utente di Experience Platform che mostra i dettagli della connessione di destinazione da compilare")

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL TikTok Ads Manager ID]**: [!DNL TikTok Ads Manager ID]. Puoi trovarlo nel tuo account [!DNL TikTok Ads manager].

![ID TikTok Ads Manager](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Immagine dell&#39;interfaccia utente di TikTok Ads Manager che mostra come ottenere l&#39;ID di TikTok Ads Manager")

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare le identità {#map}

Di seguito è riportato un esempio di corretta mappatura identità durante l’esportazione di tipi di pubblico in TikTok Ads Manager.

Selezione dei campi di origine:

* Selezionare un identificatore (ad esempio: `Email_LC_SHA256`) come identità di origine che identifica in modo univoco un profilo in Adobe Experience Platform e [!DNL TikTok Ads Manager].

Selezione dei campi di destinazione:

* Seleziona lo spazio dei nomi e-mail come identità di destinazione.

![Mappatura identità](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Immagine dell&#39;interfaccia utente di Experience Platform, mappatura identità")

## Dati esportati {#exported-data}

Controlla il tuo account [!DNL TikTok Ads Manager] (in **Assets > Tipi di pubblico**) per verificare se il pubblico Experience Platform è stato esportato correttamente. Il pubblico verrà popolato come tipo di pubblico: `Partner Audience`.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, fare riferimento alla [pagina del Centro assistenza TikTok](https://ads.tiktok.com/help/article/audiences).
