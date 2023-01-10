---
keywords: Experience Platform;home;argomenti popolari;segmento;segmento;creare segmenti;segmentazione;creare un segmento;servizio di segmentazione;
solution: Experience Platform
title: Creare un segmento utilizzando l’API del servizio di segmentazione
type: Tutorial
description: Segui questa esercitazione per scoprire come sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Creare un segmento utilizzando l’API del servizio di segmentazione

Questo documento fornisce un’esercitazione per sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Per informazioni su come creare i segmenti utilizzando l’interfaccia utente, consulta [Guida al Generatore di segmenti](../ui/overview.md).

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei vari [!DNL Adobe Experience Platform] servizi coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Consente di creare segmenti di pubblico dai dati Profilo cliente in tempo reale.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience. Per utilizzare al meglio la segmentazione, assicurati che i tuoi dati vengano acquisiti come profili ed eventi in base alla [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate al [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] guida alla risoluzione dei problemi.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate a [!DNL Platform] API, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione sull’autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le [!DNL Experience Platform] Chiamate API, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste a [!DNL Platform] Le API richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], vedi [documentazione panoramica su sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Tipo di contenuto: application/json

## Sviluppare una definizione di segmento

Il primo passaggio nella segmentazione consiste nel definire un segmento, rappresentato in un costrutto chiamato definizione di segmento. Una definizione di segmento è un oggetto che incapsula una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o ai dati delle serie temporali forniti [!DNL Real-Time Customer Profile]. Consulta la sezione [Guida PQL](../pql/overview.md) per ulteriori informazioni sulla scrittura di query PQL.

Puoi creare una nuova definizione di segmento effettuando una richiesta di POST al `/segment/definitions` punto finale [!DNL Segmentation] API. L’esempio seguente illustra come formattare una richiesta di definizione, incluse le informazioni necessarie affinché un segmento possa essere definito correttamente.

Per una spiegazione dettagliata su come definire un segmento, leggere il [guida per gli sviluppatori di definizioni di segmenti](../api/segment-definitions.md#create).

## Stimare e visualizzare in anteprima un pubblico {#estimate-and-preview-an-audience}

Man mano che sviluppi la definizione del segmento, puoi utilizzare gli strumenti di stima e anteprima in [!DNL Real-Time Customer Profile] per visualizzare informazioni a livello di riepilogo per assicurarti di isolare il pubblico previsto. Le stime forniscono informazioni statistiche su una definizione di segmento, ad esempio la dimensione del pubblico e l’intervallo di affidabilità proiettati. Le anteprime forniscono elenchi impaginati di profili qualificati per una definizione di segmento, che consentono di confrontare i risultati rispetto alle aspettative.

Stimando e visualizzando in anteprima il pubblico, puoi testare e ottimizzare i predicati PQL fino a quando non producono un risultato desiderato, dove possono quindi essere utilizzati in una definizione di segmento aggiornata.

Esistono due passaggi necessari per visualizzare in anteprima o ottenere una stima del segmento:

1. [Creare un processo di anteprima](#create-a-preview-job)
2. [Visualizza stima o anteprima](#view-an-estimate-or-preview) utilizzo dell’ID del processo di anteprima

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

Puoi creare un nuovo processo di anteprima effettuando una richiesta di POST al `/preview` punto finale.

Le istruzioni dettagliate sulla creazione di un processo di anteprima sono disponibili nella sezione [guida alle anteprime e alle stime degli endpoint](../api/previews-and-estimates.md#create-preview).

### Visualizzare una stima o un&#39;anteprima

La stima e l’anteprima dei processi vengono eseguite in modo asincrono, in quanto il completamento di query diverse può richiedere tempi diversi. Una volta avviata una query, puoi utilizzare le chiamate API per recuperare (GET) lo stato corrente della stima o dell’anteprima mentre progredisce.

Utilizzo della [!DNL Segmentation Service] API, puoi cercare lo stato corrente di un processo di anteprima in base al relativo ID. Se lo stato è &quot;RESULT_READY&quot;, è possibile visualizzare i risultati. Per cercare lo stato corrente di un processo di anteprima, leggi la sezione su [recupero di una sezione del processo di anteprima](../api/previews-and-estimates.md#get-preview) nella guida anteprime e stime endpoint . Per cercare lo stato corrente di un processo di stima, leggere la sezione su [recupero di un processo di stima](../api/previews-and-estimates.md#get-estimate) nella guida anteprime e stime endpoint .


## Passaggi successivi

Una volta sviluppata, testata e salvata la definizione del segmento, puoi creare un processo di segmento per creare un pubblico utilizzando [!DNL Segmentation Service] API. Guarda l’esercitazione su [valutazione e accesso ai risultati dei segmenti](./evaluate-a-segment.md) per passaggi dettagliati su come eseguire questa operazione.
