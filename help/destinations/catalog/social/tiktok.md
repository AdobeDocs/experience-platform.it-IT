---
title: Connessione TikTok
description: Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le campagne pubblicitarie. Questi tipi di pubblico possono essere costituiti da persone che hanno visitato il tuo sito web o interagito con il tuo contenuto. Invia in modo rapido e sicuro il pubblico desiderato da Adobe Experience Platform a TikTok utilizzando l’integrazione in tempo reale di Adobe con TikTok Ads Manager.
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 6%

---

# Connessione TikTok

## Panoramica {#overview}

Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le campagne pubblicitarie. Questi tipi di pubblico possono essere costituiti da persone che hanno visitato il tuo sito web o interagito con il tuo contenuto. Invia in modo rapido e sicuro il pubblico desiderato da Adobe Experience Platform a TikTok utilizzando l’integrazione in tempo reale di Adobe con TikTok Ads Manager. Visita [Centro di assistenza aziendale di TikTok](https://ads.tiktok.com/help/article/audiences) per ulteriori informazioni.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team TikTok. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/).

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione TikTok, ecco un caso d’uso di esempio per i clienti Adobe Experience Platform.

### Caso d’uso {#use-case-1}

Un marchio di abbigliamento sportivo vuole raggiungere i clienti esistenti attraverso i loro account di social media. Il marchio di abbigliamento può acquisire indirizzi e-mail dal proprio CRM per Adobe Experience Platform, creare tipi di pubblico dai propri dati offline e inviare tali tipi di pubblico a TikTok per visualizzare annunci nei feed di social media dei propri clienti.

## Prerequisiti {#prerequisites}

Devi avere [!DNL Admin] o [!DNL Operator] accedere all’account TikTok Ads Manager a cui desideri inviare i tipi di pubblico. Ulteriori istruzioni sono disponibili sul sito [Centro assistenza TikTok](https://ads.tiktok.com/help/article/add-users-tiktok-business-center).

Prima di inviare i dati all’account TikTok Ads Manager, devi concedere l’autorizzazione Adobe Experience Platform per accedere all’account annuncio per `Audience Management`. Questa autorizzazione può essere fornita da [immissione dell&#39;ID gestore annunci](#authenticate) nell’interfaccia utente di Experienci Platform e concessione dell’autorizzazione dopo essere stato reindirizzato all’account TikTok Ads Manager.

## Identità supportate {#supported-identities}

TikTok supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| Numero di telefono | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform e devono essere in formato E.164. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| E-mail | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione TikTok. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, verrai reindirizzato per accedere al tuo [!DNL TikTok Ads Manager] e autorizzare Adobe a gestire i tipi di pubblico per tuo conto.

![Selezione delle autorizzazioni TikTok](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "Immagine dell’interfaccia utente di TikTok per la selezione delle autorizzazioni")

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Dettagli di connessione della destinazione](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "Immagine dell’interfaccia utente di Platform che mostra i dettagli della connessione di destinazione da compilare")

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID TikTok Ads Manager]**: il tuo [!DNL TikTok Ads Manager ID]. Puoi trovarlo nel tuo [!DNL TikTok Ads manager] account.

![ID TikTok Ads Manager](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "Immagine dell&#39;interfaccia utente di TikTok Ads Manager, che mostra come ottenere l&#39;ID di TikTok Ads Manager")

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Mappare le identità {#map}

Di seguito è riportato un esempio di corretta mappatura identità durante l’esportazione di tipi di pubblico in TikTok Ads Manager.

Selezione dei campi di origine:

* Seleziona un identificatore (ad esempio:` Email_LC_SHA256`) come identità di origine che identifica in modo univoco un profilo in Adobe Experience Platform e [!DNL TikTok Ads Manager].

Selezione dei campi di destinazione:

* Seleziona lo spazio dei nomi e-mail come identità di destinazione.

![Mappatura identità](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "Immagine dell’interfaccia utente di Platform, mappatura delle identità")

## Dati esportati {#exported-data}

Controlla il tuo [!DNL TikTok Ads Manager] account (sotto **Assets > Audiences**) per verificare se il pubblico Experience Platform è stato esportato correttamente. Il pubblico verrà popolato come un tipo di pubblico: `Partner Audience`.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Consulta la sezione [Pagina del Centro assistenza TikTok](https://ads.tiktok.com/help/article/audiences) per ulteriori informazioni.
