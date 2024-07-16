---
solution: Experience Platform
title: Creare una definizione di segmento utilizzando l’API del servizio di segmentazione
type: Tutorial
description: Segui questa esercitazione per scoprire come sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando l’API del servizio di segmentazione di Adobe Experience Platform.
exl-id: 78684ae0-3721-4736-99f1-a7d1660dc849
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 6%

---

# Creare una definizione del segmento utilizzando l’API del servizio di segmentazione

Questo documento fornisce un tutorial per sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Per informazioni su come creare definizioni di segmenti utilizzando l&#39;interfaccia utente, consulta la [guida del Generatore di segmenti](../ui/segment-builder.md).

## Introduzione

Questo tutorial richiede una buona conoscenza dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella creazione delle definizioni dei segmenti. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): consente di creare tipi di pubblico utilizzando definizioni di segmenti o altre origini esterne dai dati del profilo cliente in tempo reale.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente. Per utilizzare al meglio la segmentazione, assicurati che i dati vengano acquisiti come profili ed eventi in base alle [best practice per la modellazione dei dati](../../xdm/schema/best-practices.md).

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per effettuare correttamente chiamate alle API [!DNL Platform].

### Lettura delle chiamate API di esempio

Questo tutorial fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate alle API [!DNL Platform], devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Completando il tutorial sull’autenticazione si ottengono i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di [!DNL Experience Platform], come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API [!DNL Platform] richiedono un&#39;intestazione che specifichi il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

- Content-Type: application/json

## Sviluppare una definizione di segmento

Il primo passaggio nella segmentazione consiste nel definire una definizione di segmento. Una definizione di segmento è un oggetto che incapsula una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per la definizione del segmento in base alle condizioni relative a qualsiasi record o serie temporale fornito a [!DNL Real-Time Customer Profile]. Per ulteriori informazioni sulla scrittura di query PQL, consulta la [guida di PQL](../pql/overview.md).

È possibile creare una nuova definizione di segmento effettuando una richiesta POST all&#39;endpoint `/segment/definitions` nell&#39;API [!DNL Segmentation]. L’esempio seguente illustra come formattare una richiesta di definizione, incluse le informazioni necessarie per la corretta definizione di una definizione di segmento.

Per una spiegazione dettagliata su come definire una definizione di segmento, consulta la [guida per gli sviluppatori di definizioni di segmento](../api/segment-definitions.md#create).

## Stimare e visualizzare in anteprima un pubblico {#estimate-and-preview-an-audience}

Durante lo sviluppo della definizione del segmento, è possibile utilizzare gli strumenti di stima e anteprima in [!DNL Real-Time Customer Profile] per visualizzare informazioni di riepilogo che consentono di isolare il pubblico previsto. Le stime forniscono informazioni statistiche su una definizione di segmento, ad esempio la dimensione del pubblico prevista e l’intervallo di affidabilità. Le anteprime forniscono elenchi impaginati di profili idonei per la definizione di un segmento, consentendo di confrontare i risultati rispetto a quelli previsti.

Stimando e visualizzando in anteprima il pubblico, puoi testare e ottimizzare i predicati di PQL fino a quando non producono un risultato desiderato, che può quindi essere utilizzato in una definizione di segmento aggiornata.

Per visualizzare in anteprima o stimare la definizione del segmento sono necessari due passaggi:

1. [Creare un processo di anteprima](#create-a-preview-job)
2. [Visualizza la stima o l&#39;anteprima](#view-an-estimate-or-preview) utilizzando l&#39;ID del processo di anteprima

### Come vengono generate le stime

Quando i dati abilitati per Real-Time Customer Profile vengono acquisiti in Platform, vengono memorizzati nell’archivio dati Profile. Quando l’acquisizione dei record nell’archivio profili aumenta o diminuisce il conteggio totale dei profili di oltre il 5%, viene attivato un processo di campionamento per aggiornare il conteggio. Se il conteggio dei profili non cambia di oltre il 5%, il processo di campionamento viene eseguito automaticamente su base settimanale.

Il modo in cui il campione viene attivato dipende dal tipo di acquisizione utilizzata:

- Per i flussi di lavoro di dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o riduzione del 5% è stata raggiunta. Se questa soglia è stata raggiunta, viene attivato automaticamente un processo di esempio per aggiornare il conteggio.
- Per l’acquisizione batch, entro 15 minuti dalla corretta acquisizione di un batch nell’archivio profili, se viene raggiunta la soglia di aumento o di riduzione del 5%, viene eseguito un processo per aggiornare il conteggio. Utilizzando l’API di profilo è possibile visualizzare in anteprima l’ultimo processo di esempio riuscito, nonché elencare la distribuzione del profilo per set di dati e per spazio dei nomi dell’identità.

La dimensione del campione dipende dal numero complessivo di entità nell’archivio profili. Queste dimensioni di esempio sono rappresentate nella tabella seguente:

| Entità nell&#39;archivio profili | Dimensione campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Le stime generalmente durano 10-15 secondi, a partire da una stima approssimativa e con la lettura di più record.

### Creare un processo di anteprima

È possibile creare un nuovo processo di anteprima effettuando una richiesta POST all&#39;endpoint `/preview`.

Istruzioni dettagliate sulla creazione di un processo di anteprima sono disponibili nella [guida degli endpoint per anteprime e stime](../api/previews-and-estimates.md#create-preview).

### Visualizzare una stima o un’anteprima

I processi di stima e anteprima vengono eseguiti in modo asincrono in quanto il completamento di query diverse può richiedere tempi diversi. Una volta avviata una query, puoi utilizzare le chiamate API per recuperare (GET) lo stato corrente della stima o dell’anteprima durante l’avanzamento.

Utilizzando l&#39;API [!DNL Segmentation Service], è possibile cercare lo stato corrente di un processo di anteprima in base al relativo ID. Se lo stato è &quot;RESULT_READY&quot;, è possibile visualizzare i risultati. Per cercare lo stato corrente di un processo di anteprima, leggere la sezione su [recupero di una sezione del processo di anteprima](../api/previews-and-estimates.md#get-preview) nella guida degli endpoint per anteprime e stime. Per cercare lo stato corrente di un processo di stima, leggere la sezione relativa al [recupero di un processo di stima](../api/previews-and-estimates.md#get-estimate) nella guida delle anteprime e degli endpoint di stima.


## Passaggi successivi

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi creare un processo per segmenti per creare un pubblico utilizzando l&#39;API [!DNL Segmentation Service]. Consulta il tutorial su [valutazione e accesso ai risultati dei segmenti](./evaluate-a-segment.md) per i passaggi dettagliati su come eseguire questa operazione.
