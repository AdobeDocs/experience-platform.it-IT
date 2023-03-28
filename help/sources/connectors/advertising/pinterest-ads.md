---
keywords: Experience Platform;home;argomenti popolari;Pinterest Ads;
title: Panoramica dell’origine di pinterest Ads
description: Scopri come collegare Pinterest Ads a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badge: "Beta"
hide: true
hidefromtoc: true
source-git-commit: a16264da68d9e5e9aeac86b1a3083c701407febb
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>La [!DNL Pinterest Ads] la sorgente è in versione beta. Leggi la sezione [Panoramica delle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo dei connettori con etichetta beta.

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema pubblicitario di terze parti. Il supporto ai fornitori di pubblicità include: [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) è un motore di scoperta visiva per trovare ricette, arredamento domestico, ispirazione di stile e altre idee in tutto il web. Questi vengono presentati su piccola scala utilizzando immagini, GIF animati e video in formato a bacheca. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) consente di crescere il tuo business e raggiungere 400 milioni di persone utilizzando [!DNL Pinterest].

Con [!DNL Pinterest Ads], puoi raggiungere gli utenti tramite annunci pubblicitari mirati per scoprire e acquistare i tuoi prodotti. Pins da [!DNL Pinterest Ads] sono sponsorizzati per ricevere un&#39;esposizione supplementare nei risultati di ricerca pertinenti. Utenti abbonati a [!DNL Pinterest Business] può scegliere di promuovere i pin con le prestazioni migliori esistenti, creare una nuova immagine o un nuovo video o persino promuovere un&#39;immagine che è stata bloccata da un sito web. [!DNL Pinterest Ads] offre diversi formati di annunci per aiutarti a raggiungere gli obiettivi specifici della campagna.

## [!DNL Pinterest] API {#pinterest-apis}

La [!DNL Pinterest Ads] la sorgente sfrutta [!DNL Pinterest] API per recuperare le [!DNL Pinterest Ads] insieme a tutte le prestazioni e le metriche. Gli endpoint API supportati sono:

* [Analisi di Campaign](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Analisi di Ad Group](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Analisi degli annunci](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilizza la [!DNL Pinterest Ads] origine da cui estrarre i dati [!DNL Pinterest] ad Experience Platform, dove puoi eseguire l’analisi dei dati. I dati vengono restituiti a partire dalla data di acquisizione per un intervallo retrodatato di 90 giorni. [!DNL Pinterest Ads] utilizza i token portatori come meccanismo di autenticazione per comunicare con [!DNL Pinterest] API.

## Prerequisiti {#prerequisites}

Il primo passaggio nella creazione di un [!DNL Pinterest Ads] la connessione di origine deve garantire di disporre di un account sviluppatore Pinterest. Se non ne hai già uno, visita il [iscriviti](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) per registrare e creare il tuo account.

### Configurazione [!DNL Pinterest] app e genera token di accesso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Si consiglia di utilizzare il [!DNL Pinterest] API per generare il token di accesso perché la generazione del token di accesso nell’interfaccia utente fornisce un accesso limitato. Tramite l’interfaccia utente, potrai accedere solo ai seguenti ambiti: `pins:read`, `boards:read` e `user_accounts:read`. Questa limitazione non è adeguata per l’utilizzo con gli endpoint di analisi del [!DNL Pinterest] API.

Per generare il token di accesso, leggi il [!DNL Pinterest] guide su [configurazione dell’app](https://developers.pinterest.com/docs/getting-started/set-up-app/) e [autenticazione tramite OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Raccogli credenziali richieste {#gather-required-credentials}

Per connettersi [!DNL Pinterest Ads] in Platform, devi fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| Token di accesso | La [!DNL Pinterest Ads] token di accesso per il tuo account utente. L’account utente del token deve essere il proprietario del [!DNL Pinterest Ad] o hanno uno dei ruoli necessari assegnati tramite Business Access: Amministratore, analista o Campaign Manager. Per ulteriori informazioni sul token di accesso, consulta la [[!DNL Pinterest] guida alla generazione del token di accesso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID account annuncio | I relativi [!DNL Pinterest Ads] ID account dell&#39;annuncio per la tua unità aziendale. Per informazioni su come recuperare l’ID del tuo account annuncio. Visita il [[!DNL Pinterest] guida alla ricerca degli ID in Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| Campagna, gruppo di annunci o ID annuncio | La `campaign`, `ad group`oppure `ad` ID corrispondenti al tuo ID account annuncio. Per ottenere gli ID richiesti, passa alla [!DNL Pinterest] pagina per **Pinterest Business Hub** > **Riepilogo account annuncio** > **Campagne** / **Gruppi di annunci** / **Annunci** e copia l&#39;ID richiesto appena sotto ciascuno dei loro nomi. |

>[!NOTE]
>
>La [!DNL Pinterest] API fornisce singole API per recuperare i dati associati a ciascun ID. Di conseguenza, devi trasmettere solo gli ID corrispondenti per il tipo di ID a cui sei interessato.

## Guardrail {#guardrails}

Le sezioni seguenti forniscono informazioni sulle protezioni dei dati per [!DNL Pinterest].

### [!DNL Pinterest] intervallo date {#pinterest-date-range}

La [!DNL Pinterest] L’API supporta entrambi `start_date` e `end_date` per recuperare i dati analitici tra un determinato intervallo di date.

* La `start_date` non può essere più di 90 giorni prima della data corrente.
* La `end_date` non può essere superiore a 90 giorni dopo il `start_date`.

Quando pianifichi il flusso di dati, devi configurare una delle seguenti impostazioni di frequenza e intervallo:

| Frequenza | Intervallo |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Ad esempio, se l’acquisizione è impostata il 15 marzo 2023 con un’impostazione di frequenza e intervallo configurata per `Day=1` o `Hour=24`, quindi [!DNL Pinterest] L’API recupera i dati solo dal 15 dicembre 2022 perché il calcolo è retrodatato per 90 giorni.

### [!DNL Pinterest] intervallo di tempo {#pinterest-time-range}

La [!DNL Pinterest] L’API supporta diversi tipi di granularità temporale per il recupero dei dati:

| Granularità temporale | Descrizione |
| --- | --- |
| **TOTALE** | Le metriche dei dati vengono aggregate in un intervallo di date specificato. |
| **GIORNO** | Le metriche dei dati sono suddivise su base giornaliera. |
| **ORA** | Le metriche dati sono suddivise su base oraria. |
| **SETTIMANALE** | Le metriche dei dati sono suddivise settimanalmente. |
| **MENSILE** | Le metriche dei dati sono suddivise su base mensile. |

Per Platform, la [!DNL Pinterest Ads] origine configurata internamente a `Day`, il che significa che i dati saranno aggregati su base giornaliera. Ad esempio, utilizzando `impressions recorded` come metrica, poiché la granularità è configurata come `DAY`... `xx` impression su `day 1`, `yy` impression su `day 2` e così via.

>[!IMPORTANT]
>
>Pinterest impone un limite di frequenza di 1000 chiamate API ogni giorno sulla sua API per leggere informazioni da annunci, gruppi di annunci o campagne pubblicitarie. Per informazioni sui limiti di tasso applicabili alle chiamate API sottostanti, consulta [[!DNL Pinterest] documentazione sui limiti delle aliquote](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connetti [!DNL Pinterest Ads] su Platform {#connect-to-platform}

La documentazione seguente fornisce informazioni su come connettersi [!DNL Pinterest Ads] su Platform utilizzando le API o l’interfaccia utente:

### Connetti [!DNL Pinterest Ads] su Platform tramite API {#connect-to-platform-using-api}

* [Creare una connessione di base Pinterest utilizzando l’API del servizio di flusso](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio di flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine pubblicitaria utilizzando l’API del servizio di flusso](../../tutorials/api/collect/advertising.md)

### Connetti [!DNL Pinterest Ads] su Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Creare una connessione sorgente Pinterest nell’interfaccia utente](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Creare un flusso di dati per una connessione a un’origine pubblicitaria nell’interfaccia utente](../../tutorials/ui/dataflow/advertising.md)
