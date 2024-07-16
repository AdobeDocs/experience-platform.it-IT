---
keywords: Experience Platform;home;argomenti popolari;Pinterest Ads;
title: Panoramica di pinterest Ads Source
description: Scopri come collegare Pinterest Ads a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 8edbcb26-0a18-47f1-8012-ca209d99d7a6
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 1%

---

# [!DNL Pinterest Ads]

>[!NOTE]
>
>L&#39;origine [!DNL Pinterest Ads] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, leggere la [Panoramica origini](../../home.md#terms-and-conditions).

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema pubblicitario di terze parti. Il supporto per i provider pubblicitari include [!DNL Pinterest Ads].

[[!DNL Pinterest]](https://www.pinterest.com) è un motore di ricerca visiva che consente di trovare ricette, decorazioni domestiche, ispirazioni allo stile e altre idee nel Web. Questi vengono presentati su piccola scala utilizzando immagini, GIF animati e video in formato bacheca. [[!DNL Pinterest Ads]](https://ads.pinterest.com/) ti consente di espandere la tua attività e di raggiungere 400 milioni di persone utilizzando [!DNL Pinterest].

Con [!DNL Pinterest Ads], puoi raggiungere gli utenti tramite annunci mirati per scoprire e acquistare i tuoi prodotti. I pin di [!DNL Pinterest Ads] sono sponsorizzati per ricevere un&#39;esposizione aggiuntiva nei risultati di ricerca pertinenti. Gli utenti abbonati a [!DNL Pinterest Business] possono scegliere di promuovere i pin con le prestazioni migliori esistenti, creare una nuova immagine o un nuovo video o persino promuovere un&#39;immagine bloccata da un sito Web. [!DNL Pinterest Ads] offre diversi formati di annunci per aiutarti a raggiungere gli obiettivi specifici della tua campagna.

## [!DNL Pinterest] API {#pinterest-apis}

L&#39;origine [!DNL Pinterest Ads] sfrutta le API [!DNL Pinterest] per recuperare i dati [!DNL Pinterest Ads], insieme a tutte le prestazioni e le metriche. Gli endpoint API supportati sono:

* [Analisi delle campagne](https://developers.pinterest.com/docs/api/v5/#operation/campaigns/analytics)
* [Analisi del gruppo di annunci](https://developers.pinterest.com/docs/api/v5/#operation/ad_groups/analytics)
* [Analisi annunci](https://developers.pinterest.com/docs/api/v5/#operation/ads/analytics)

Utilizza l&#39;origine [!DNL Pinterest Ads] per portare i tuoi dati da [!DNL Pinterest] all&#39;Experience Platform, dove puoi quindi eseguire analisi dei dati. I dati vengono restituiti a partire dalla data di acquisizione per un intervallo retrodatato di 90 giorni. [!DNL Pinterest Ads] utilizza token Bearer come meccanismo di autenticazione per comunicare con le API [!DNL Pinterest].

## Prerequisiti {#prerequisites}

Il primo passaggio nella creazione di una connessione di origine [!DNL Pinterest Ads] consiste nel verificare di disporre di un account sviluppatore Pinterest. Se non ne hai già uno, visita la pagina [iscriviti](https://www.pinterest.com/business/create/?next=https://developers.pinterest.com/account-setup/) per registrarti e creare il tuo account.

### Imposta l&#39;app [!DNL Pinterest] e genera il token di accesso {#create-app-and-generate-token}

>[!IMPORTANT]
>
>Si consiglia di utilizzare le API [!DNL Pinterest] per generare il token di accesso, in quanto la generazione del token di accesso nell&#39;interfaccia utente offre un accesso limitato. Tramite l&#39;interfaccia utente, potrai accedere solo ai seguenti ambiti: `pins:read`, `boards:read` e `user_accounts:read`. Questa limitazione non è adeguata per l&#39;utilizzo con gli endpoint di analisi dell&#39;API [!DNL Pinterest].

Per generare il token di accesso, leggere le guide di [!DNL Pinterest] in [configurazione dell&#39;app](https://developers.pinterest.com/docs/getting-started/set-up-app/) e [autenticazione tramite OAuth 2.0](https://developers.pinterest.com/docs/getting-started/authentication/).

### Raccogli le credenziali richieste {#gather-required-credentials}

Per connettere [!DNL Pinterest Ads] a Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| Token di accesso | Il token di accesso [!DNL Pinterest Ads] per l&#39;account utente. L&#39;account utente del token deve essere il proprietario dell&#39;account [!DNL Pinterest Ad] specificato o disporre di uno dei ruoli necessari concessi tramite Business Access: Admin, Analyst o Campaign Manager. Per ulteriori informazioni sul token di accesso, consulta la [[!DNL Pinterest] guida sulla generazione del token di accesso](https://developers.pinterest.com/docs/getting-started/set-up-app/). |
| ID account annuncio | L&#39;ID dell&#39;account dell&#39;annuncio [!DNL Pinterest Ads] correlato per la tua business unit. Per informazioni sul recupero dell&#39;ID account dell&#39;annuncio. Visita la [[!DNL Pinterest] guida alla ricerca degli ID in Ads Manager](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager). |
| ID campagna, gruppo di annunci o annuncio | Gli ID `campaign`, `ad group` o `ad` corrispondenti all&#39;ID dell&#39;account dell&#39;annuncio. Per ottenere gli ID richiesti, passa alla pagina [!DNL Pinterest] per **Pinterest Business Hub** > **Riepilogo account annuncio** > **Campagne** / **Gruppi annunci** / **Annunci** e copia gli ID richiesti indicati sotto ciascuno dei loro nomi. |

>[!NOTE]
>
>L&#39;API [!DNL Pinterest] fornisce singole API per recuperare i dati associati a ciascun ID. Di conseguenza, devi passare solo gli ID corrispondenti per il tipo di ID che ti interessa.

## Guardrail {#guardrails}

Nelle sezioni seguenti vengono fornite informazioni sui guardrail dei dati per [!DNL Pinterest].

### Intervallo date [!DNL Pinterest] {#pinterest-date-range}

L&#39;API [!DNL Pinterest] supporta sia un parametro `start_date` che un parametro `end_date` per recuperare i dati di analisi tra un determinato intervallo di date.

* `start_date` non può precedere di oltre 90 giorni la data corrente.
* `end_date` non può essere più di 90 giorni dopo `start_date`.

Quando pianifichi il flusso di dati, devi configurare una delle seguenti impostazioni di frequenza e intervallo:

| Frequenza | Intervallo |
| --- | --- |
| `Day` | 1 |
| `Hour` | 24 |

Ad esempio, se l’acquisizione è impostata il 15 marzo 2023 con un’impostazione di frequenza e intervallo configurata su `Day=1` o `Hour=24`, l’API [!DNL Pinterest] recupererà i dati solo a partire dal 15 dicembre 2022 perché il calcolo è retrodatato di 90 giorni.

### Intervallo di tempo [!DNL Pinterest] {#pinterest-time-range}

L&#39;API [!DNL Pinterest] supporta diversi tipi di granularità temporale per il recupero dei dati:

| Granularità temporale | Descrizione |
| --- | --- |
| **TOTALE** | Le metriche dei dati sono aggregate in un intervallo di date specificato. |
| **GIORNO** | Le metriche dei dati sono suddivise su base giornaliera. |
| **ORA** | Le metriche dei dati sono suddivise su base oraria. |
| **SETTIMANALE** | Le metriche dei dati sono suddivise su base settimanale. |
| **MENSILE** | Le metriche dei dati sono disaggregate su base mensile. |

Per Platform, l&#39;origine [!DNL Pinterest Ads] è configurata internamente per `Day`, il che significa che i dati verranno aggregati su base giornaliera. Ad esempio, utilizzando `impressions recorded` come metrica, poiché la granularità è configurata come `DAY`, si otterrebbero `xx` impression su `day 1`, `yy` impression su `day 2` e così via.

>[!IMPORTANT]
>
>Pinterest impone un limite di 1000 chiamate API al giorno sulla propria API per leggere informazioni da annunci, gruppi di annunci o campagne pubblicitarie. Per informazioni sui limiti di tariffa applicabili alle chiamate API sottostanti, consulta la [[!DNL Pinterest] documentazione sui limiti di tariffa](https://developers.pinterest.com/docs/reference/ratelimits/).

## Connetti [!DNL Pinterest Ads] a Platform {#connect-to-platform}

La documentazione seguente fornisce informazioni su come connettere [!DNL Pinterest Ads] a Platform tramite API o tramite l&#39;interfaccia utente:

### Connetti [!DNL Pinterest Ads] a Platform tramite API {#connect-to-platform-using-api}

* [Creare una connessione di base Pinterest utilizzando l’API del servizio Flusso](../../tutorials/api/create/advertising/pinterest-ads.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine pubblicitaria utilizzando l’API del servizio Flow](../../tutorials/api/collect/advertising.md)

### Connetti [!DNL Pinterest Ads] a Platform tramite l&#39;interfaccia utente {#connect-to-platform-using-ui}

* [Creare una connessione sorgente Pinterest nell’interfaccia utente](../../tutorials/ui/create/advertising/pinterest-ads.md)
* [Creare un flusso di dati per una connessione sorgente per annunci pubblicitari nell’interfaccia utente](../../tutorials/ui/dataflow/advertising.md)
