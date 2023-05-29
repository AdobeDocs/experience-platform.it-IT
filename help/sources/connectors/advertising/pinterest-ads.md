---
keywords: Experience Platform;home;argomenti popolari;Pinterest Ads;
title: Panoramica sull’origine di pinterest Ads
description: Scopri come collegare Pinterest Ads a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>Il [!DNL Pinterest Ads] sorgente in versione beta. Leggi le [Panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di connettori con etichetta beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema pubblicitario di terze parti. Il supporto per i provider pubblicitari include [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) è un motore di scoperta visiva per trovare ricette, arredamento della casa, ispirazione di stile e altre idee attraverso il web. Questi vengono presentati su piccola scala utilizzando immagini, GIF animati e video in formato bacheca. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) consente di crescere e raggiungere i 400 milioni di persone utilizzando [!DNL Pinterest].

Con [!DNL Pinterest Ads], puoi raggiungere gli utenti tramite annunci mirati per scoprire e acquistare i tuoi prodotti. Pin da [!DNL Pinterest Ads] sono sponsorizzati per ricevere un’esposizione aggiuntiva nei risultati di ricerca pertinenti. Utenti abbonati a [!DNL Pinterest Business] può scegliere di promuovere i pin con le prestazioni migliori esistenti, creare una nuova immagine o un nuovo video o persino promuovere un&#39;immagine bloccata da un sito Web. [!DNL Pinterest Ads] offre diversi formati di annunci per aiutarti a raggiungere gli obiettivi specifici della campagna.

## [!DNL Pinterest] API {#pinterest-apis}

Il [!DNL Pinterest Ads] l&#39;origine utilizza [!DNL Pinterest] API per recuperare [!DNL Pinterest Ads] insieme a tutte le prestazioni e le metriche. Gli endpoint API supportati sono:

* [Analisi di Campaign](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Analisi del gruppo di annunci](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Analisi degli annunci](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilizza il [!DNL Pinterest Ads] origine da cui estrarre i dati [!DNL Pinterest] ad Experience Platform, dove puoi eseguire data analytics. I dati vengono restituiti a partire dalla data di acquisizione per un intervallo retrodatato di 90 giorni. [!DNL Pinterest Ads] utilizza token Bearer come meccanismo di autenticazione per comunicare con [!DNL Pinterest] API.

## Prerequisiti {#prerequisites}

Il primo passaggio nella creazione di un’ [!DNL Pinterest Ads] la connessione di origine consente di assicurarsi di disporre di un account sviluppatore Pinterest. Se non ne hai già uno, visita il [iscriviti](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) per registrarti e creare il tuo account.

### Configurazione [!DNL Pinterest] app e genera token di accesso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Si consiglia di utilizzare il [!DNL Pinterest] API per generare il token di accesso, in quanto la generazione del token di accesso nell’interfaccia utente offre un accesso limitato. Tramite l’interfaccia utente, potrai accedere solo ai seguenti ambiti: `pins:read`, `boards:read` e `user_accounts:read`. Questa limitazione non è adeguata per l’utilizzo con gli endpoint di analisi del [!DNL Pinterest] API.

Per generare il token di accesso, leggi [!DNL Pinterest] guide su [configurazione dell’app](https://developers.pinterest.com/docs/getting-started/set-up-app/) e [autenticazione tramite OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Raccogli le credenziali richieste {#gather-required-credentials}

Per connettersi [!DNL Pinterest Ads] In Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| Token di accesso | Il [!DNL Pinterest Ads] token di accesso per l’account utente. L&#39;account utente del token deve essere il proprietario del [!DNL Pinterest Ad] o dispongono di uno dei ruoli necessari concessi loro tramite Business Access: Amministratore, Analista o Responsabile di Campaign. Per ulteriori informazioni sul token di accesso, consulta [[!DNL Pinterest] guida alla generazione del token di accesso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID account annuncio | I relativi [!DNL Pinterest Ads] ID dell’account per la tua business unit. Per informazioni sul recupero dell&#39;ID account dell&#39;annuncio. Visita il [[!DNL Pinterest] guida alla ricerca di ID in Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| ID campagna, gruppo di annunci o annuncio | Il `campaign`, `ad group`, o `ad` ID corrispondenti all&#39;ID dell&#39;account dell&#39;annuncio. Per ottenere gli ID richiesti, vai alla [!DNL Pinterest] pagina per **Pinterest Business Hub** > **Riepilogo account annuncio** > **Campagne** / **Gruppi di annunci** / **Annunci** e copia gli ID richiesti indicati sotto ciascuno dei loro nomi. |

>[!NOTE]
>
>Il [!DNL Pinterest] API fornisce singole API per recuperare i dati associati a ciascun ID. Di conseguenza, devi passare solo gli ID corrispondenti per il tipo di ID che ti interessa.

## Guardrail {#guardrails}

Le sezioni seguenti forniscono informazioni sui guardrail dei dati per [!DNL Pinterest].

### [!DNL Pinterest] intervallo date {#pinterest-date-range}

Il [!DNL Pinterest] L’API supporta sia `start_date` e un `end_date` per recuperare i dati di analisi tra un determinato intervallo di date.

* Il `start_date` non può precedere di più di 90 giorni la data corrente.
* Il `end_date` non può essere posteriore di oltre 90 giorni alla `start_date`.

Quando pianifichi il flusso di dati, devi configurare una delle seguenti impostazioni di frequenza e intervallo:

| Frequenza | Interval |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Ad esempio, se l’acquisizione è impostata per il 15 marzo 2023 con un’impostazione di frequenza e intervallo configurata su `Day=1` o `Hour=24`, quindi [!DNL Pinterest] L’API recupererebbe i dati solo a partire dal 15 dicembre 2022, perché il calcolo è retrodatato per 90 giorni.

### [!DNL Pinterest] intervallo di tempo {#pinterest-time-range}

Il [!DNL Pinterest] L’API supporta diversi tipi di granularità temporale per il recupero dei dati:

| Granularità temporale | Descrizione |
| --- | --- |
| **TOTALE** | Le metriche dei dati sono aggregate in un intervallo di date specificato. |
| **GIORNO** | Le metriche dei dati sono suddivise su base giornaliera. |
| **ORA** | Le metriche dei dati sono suddivise su base oraria. |
| **OGNI SETTIMANA** | Le metriche dei dati sono suddivise su base settimanale. |
| **MENSILE** | Le metriche dei dati sono disaggregate su base mensile. |

Per Platform, il [!DNL Pinterest Ads] l&#39;origine è configurata internamente per `Day`: i dati saranno aggregati su base giornaliera. Ad esempio, utilizzando `impressions recorded` come metrica, poiché la granularità è configurata come `DAY`, otterrai `xx` impression su `day 1`, `yy` impression su `day 2` e così via.

>[!IMPORTANT]
>
>Pinterest impone un limite di 1000 chiamate API al giorno sulla propria API per leggere informazioni da annunci, gruppi di annunci o campagne pubblicitarie. Per informazioni sui limiti di tariffa applicabili alle chiamate API sottostanti, consulta [[!DNL Pinterest] documentazione sui limiti di tariffa](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connetti [!DNL Pinterest Ads] alla piattaforma {#connect-to-platform}

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Pinterest Ads] in Platform tramite API o l’interfaccia utente:

### Connetti [!DNL Pinterest Ads] alla piattaforma utilizzando le API {#connect-to-platform-using-api}

* [Creare una connessione di base Pinterest utilizzando l’API del servizio Flusso](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine pubblicitaria utilizzando l’API del servizio Flow](../../tutorials/api/collect/advertising.md)

### Connetti [!DNL Pinterest Ads] a Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Creare una connessione sorgente Pinterest nell’interfaccia utente](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Creare un flusso di dati per una connessione sorgente per annunci pubblicitari nell’interfaccia utente](../../tutorials/ui/dataflow/advertising.md)
