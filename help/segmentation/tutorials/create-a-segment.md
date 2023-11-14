---
solution: Experience Platform
title: Creare una definizione di segmento utilizzando l’API del servizio di segmentazione
type: Tutorial
description: Segui questa esercitazione per scoprire come sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 12%

---

# Creare una definizione del segmento utilizzando l’API del servizio di segmentazione

Questo documento fornisce un’esercitazione per sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Per informazioni su come creare definizioni dei segmenti utilizzando l’interfaccia utente, consulta la sezione [Guida al Generatore di segmenti](../ui/overview.md).

## Introduzione

Questo tutorial richiede una buona conoscenza delle varie [!DNL Adobe Experience Platform] servizi coinvolti nella creazione di definizioni di segmenti. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): consente di creare tipi di pubblico utilizzando definizioni di segmenti o altre origini esterne dai dati del profilo cliente in tempo reale.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato per l’organizzazione dei dati sull’esperienza del cliente in [!DNL Platform]. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate al [!DNL Platform] API.

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere gli esempi di chiamate API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi.di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API di [!DNL Platform], devi prima completare il [tutorial sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolati in specifiche sandbox virtuali. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedere [documentazione di panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Sviluppare una definizione di segmento

Il primo passaggio nella segmentazione consiste nel definire una definizione di segmento. Una definizione di segmento è un oggetto che incapsula una query scritta in [!DNL Profile Query Language] (PQL) Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per la definizione del segmento in base alle condizioni relative a qualsiasi record o serie temporale fornito [!DNL Real-Time Customer Profile]. Consulta la [Guida di PQL](../pql/overview.md) per ulteriori informazioni sulla scrittura di query PQL.

Per creare una nuova definizione di segmento, devi effettuare una richiesta POST al `/segment/definitions` endpoint nella [!DNL Segmentation] API. L’esempio seguente illustra come formattare una richiesta di definizione, incluse le informazioni necessarie per la corretta definizione di una definizione di segmento.

Per una spiegazione dettagliata su come definire una definizione di segmento, leggi [guida per gli sviluppatori sulla definizione dei segmenti](../api/segment-definitions.md#create).

## Stimare e visualizzare in anteprima un pubblico {#estimate-and-preview-an-audience}

Quando sviluppi la definizione del segmento, puoi utilizzare gli strumenti di stima e anteprima in [!DNL Real-Time Customer Profile] per visualizzare informazioni di riepilogo utili per isolare il pubblico previsto. Le stime forniscono informazioni statistiche su una definizione di segmento, ad esempio la dimensione del pubblico prevista e l’intervallo di affidabilità. Le anteprime forniscono elenchi impaginati di profili idonei per la definizione di un segmento, consentendo di confrontare i risultati rispetto a quelli previsti.

Stimando e visualizzando in anteprima il pubblico, puoi testare e ottimizzare i predicati PQL fino a quando non producono un risultato desiderato, che può quindi essere utilizzato in una definizione di segmento aggiornata.

Per visualizzare in anteprima o stimare la definizione del segmento sono necessari due passaggi:

1. [Creare un processo di anteprima](#create-a-preview-job)
2. [Visualizza stima o anteprima](#view-an-estimate-or-preview) utilizzo dell’ID del processo di anteprima

### Come vengono generate le stime

Gli esempi di dati vengono utilizzati per valutare le definizioni dei segmenti e stimare il numero di profili idonei. I nuovi dati vengono caricati in memoria ogni mattina (tra le 12 e le 2 del mattino PT, che è tra le 7 e le 9 del mattino UTC) e tutte le query di segmentazione vengono stimate utilizzando i dati di esempio di quel giorno. Di conseguenza, eventuali nuovi campi aggiunti o dati aggiuntivi raccolti saranno riflessi nelle stime il giorno successivo.

La dimensione del campione dipende dal numero complessivo di entità nell’archivio profili. Queste dimensioni di esempio sono rappresentate nella tabella seguente:

| Entità nell’archivio profili | Dimensione campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Le stime generalmente durano 10-15 secondi, a partire da una stima approssimativa e con la lettura di più record.

### Creare un processo di anteprima

Per creare un nuovo processo di anteprima, devi effettuare una richiesta POST al `/preview` endpoint.

Le istruzioni dettagliate sulla creazione di un processo di anteprima sono disponibili nella sezione [guida alle anteprime e alle stime degli endpoint](../api/previews-and-estimates.md#create-preview).

### Visualizzare una stima o un’anteprima

I processi di stima e anteprima vengono eseguiti in modo asincrono in quanto il completamento di query diverse può richiedere tempi diversi. Una volta avviata una query, puoi utilizzare le chiamate API per recuperare (GET) lo stato corrente della stima o dell’anteprima durante l’avanzamento.

Utilizzo di [!DNL Segmentation Service] API, puoi cercare lo stato corrente di un processo di anteprima in base al suo ID. Se lo stato è &quot;RESULT_READY&quot;, è possibile visualizzare i risultati. Per cercare lo stato corrente di un processo di anteprima, leggi la sezione su [recupero di una sezione del processo di anteprima](../api/previews-and-estimates.md#get-preview) nella guida anteprime ed endpoint stime. Per cercare lo stato corrente di un processo di stima, leggere la sezione su [recupero di un processo di stima](../api/previews-and-estimates.md#get-estimate) nella guida anteprime ed endpoint stime.


## Passaggi successivi

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi creare un processo per creare un pubblico utilizzando [!DNL Segmentation Service] API. Guarda il tutorial su [valutazione e accesso ai risultati dei segmenti](./evaluate-a-segment.md) per i passaggi dettagliati su come eseguire questa operazione.
