---
keywords: Experience Platform;home;argomenti popolari;segmento;segmento;creare segmenti;segmentazione;creare un segmento;servizio di segmentazione;
solution: Experience Platform
title: Creare un segmento utilizzando l’API del servizio di segmentazione
topic-legacy: tutorial
type: Tutorial
description: Segui questa esercitazione per scoprire come sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# Creare un segmento utilizzando l’API del servizio di segmentazione

Questo documento fornisce un&#39;esercitazione per sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Per informazioni su come creare i segmenti utilizzando l’interfaccia utente, consulta la [guida al Generatore di segmenti](../ui/overview.md).

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Consente di creare segmenti di pubblico dai dati Profilo cliente in tempo reale.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

Le sezioni seguenti forniscono informazioni aggiuntive che dovrai conoscere per effettuare correttamente le chiamate alle API [!DNL Platform] .

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API [!DNL Platform] richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- nome x-sandbox: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la documentazione di panoramica [sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Sviluppare una definizione di segmento

Il primo passaggio nella segmentazione consiste nel definire un segmento, rappresentato in un costrutto chiamato definizione di segmento. Una definizione di segmento è un oggetto che incapsula una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o dati delle serie temporali forniti a [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla scrittura di query PQL, consulta la [Guida PQL](../pql/overview.md) .

Puoi creare una nuova definizione di segmento effettuando una richiesta POST all’endpoint `/segment/definitions` nell’ API [!DNL Segmentation] . L’esempio seguente illustra come formattare una richiesta di definizione, incluse le informazioni necessarie affinché un segmento possa essere definito correttamente.

Per una spiegazione dettagliata su come definire un segmento, consulta la [guida per gli sviluppatori della definizione del segmento](../api/segment-definitions.md#create).

## Stimare e visualizzare in anteprima un pubblico {#estimate-and-preview-an-audience}

Man mano che sviluppi la definizione del segmento, puoi utilizzare gli strumenti di stima e anteprima all’interno di [!DNL Real-time Customer Profile] per visualizzare le informazioni a livello di riepilogo per assicurarti di isolare il pubblico previsto. Le stime forniscono informazioni statistiche su una definizione di segmento, ad esempio la dimensione del pubblico e l’intervallo di affidabilità proiettati. Le anteprime forniscono elenchi impaginati di profili qualificati per una definizione di segmento, che consentono di confrontare i risultati rispetto alle aspettative.

Stimando e visualizzando in anteprima il pubblico, puoi testare e ottimizzare i predicati PQL fino a quando non producono un risultato desiderato, dove possono quindi essere utilizzati in una definizione di segmento aggiornata.

Esistono due passaggi necessari per visualizzare in anteprima o ottenere una stima del segmento:

1. [Creare un processo di anteprima](#create-a-preview-job)
2. [Visualizza la stima o l’](#view-an-estimate-or-preview) anteprima utilizzando l’ID del processo di anteprima

### Generazione delle stime

I campioni di dati vengono utilizzati per valutare i segmenti e stimare il numero di profili qualificati. I nuovi dati vengono caricati in memoria ogni mattina (tra le 12:00 e le 2:00 PT, che sono le 7-9:00 UTC), e tutte le query di segmentazione vengono stimate utilizzando i dati di esempio di quel giorno. Di conseguenza, eventuali nuovi campi aggiunti o dati aggiuntivi raccolti saranno riportati nelle stime del giorno successivo.

La dimensione del campione dipende dal numero complessivo di entità nell’archivio dei profili. Le dimensioni dei campioni sono rappresentate nella tabella seguente:

| Entità nell’archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Le stime vengono generalmente eseguite per più di 10-15 secondi, a partire da una stima approssimativa e perfezionandole quando vengono letti più record.

### Creare un processo di anteprima

È possibile creare un nuovo processo di anteprima effettuando una richiesta di POST all&#39;endpoint `/preview`.

Le istruzioni dettagliate sulla creazione di un processo di anteprima si trovano nella [guida alle anteprime e alle stime degli endpoint](../api/previews-and-estimates.md#create-preview).

### Visualizzare una stima o un&#39;anteprima

La stima e l’anteprima dei processi vengono eseguite in modo asincrono, in quanto il completamento di query diverse può richiedere tempi diversi. Una volta avviata una query, puoi utilizzare le chiamate API per recuperare (GET) lo stato corrente della stima o dell’anteprima mentre progredisce.

Utilizzando l&#39;API [!DNL Segmentation Service], puoi cercare lo stato corrente di un processo di anteprima in base al relativo ID. Se lo stato è &quot;RESULT_READY&quot;, è possibile visualizzare i risultati. Per cercare lo stato corrente di un processo di anteprima, leggi la sezione su [recupero di una sezione del processo di anteprima](../api/previews-and-estimates.md#get-preview) nella guida anteprime e stime degli endpoint. Per cercare lo stato corrente di un processo di stima, leggi la sezione su [recupero di un processo di stima](../api/previews-and-estimates.md#get-estimate) nella guida anteprime e stime endpoint.


## Passaggi successivi

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi creare un processo di segmento per creare un pubblico utilizzando l’ [!DNL Segmentation Service] API . Per informazioni dettagliate su come eseguire questa operazione, consulta l’ esercitazione su [valutazione e accesso ai risultati dei segmenti](./evaluate-a-segment.md) .
