---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creazione di un segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---


# Creazione di un segmento

Questo documento fornisce un’esercitazione per lo sviluppo, il test, l’anteprima e il salvataggio di una definizione di segmento mediante l’API [](../api/getting-started.md)DNL  Adobe Experience Platform Segmentation Service.

Per informazioni su come creare segmenti utilizzando l’interfaccia utente, consulta la guida [di](../ui/overview.md)Segment Builder (Generatore di segmenti).

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari [!DNL Adobe Experience Platform] servizi coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [!DNL Adobe Experience Platform Segmentation Service](../home.md): Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate alle [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è prima necessario completare l&#39;esercitazione [sull&#39;](../../tutorials/authentication.md)autenticazione. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate [!DNL Experience Platform] API, come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui avrà luogo l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Sviluppo di una definizione di segmento

Il primo passo nella segmentazione consiste nel definire un segmento, rappresentato in un costrutto chiamato definizione **di** segmento. Una definizione di segmento è un oggetto che racchiude una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato **PQL**. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o dati delle serie temporali forniti da [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla scrittura di query PQL, consultate la guida [](../pql/overview.md) PQL.

Puoi creare una nuova definizione di segmento effettuando una richiesta POST all’ `/segment/definitions` endpoint nell’ [!DNL Segmentation] API. L&#39;esempio seguente illustra come formattare una richiesta di definizione, incluse le informazioni necessarie per definire correttamente un segmento.

Per una spiegazione dettagliata su come definire un segmento, consulta la guida [per gli sviluppatori per la definizione del](../api/segment-definitions.md#create)segmento.

## Stima e anteprima di un&#39;audience {#estimate-and-preview-an-audience}

Mentre sviluppate la definizione del segmento, potete utilizzare gli strumenti di stima e anteprima all’interno [!DNL Real-time Customer Profile] per visualizzare le informazioni a livello di riepilogo per garantire che l’audience attesa sia isolata. Le stime forniscono informazioni statistiche sulla definizione di un segmento, come la dimensione dell&#39;audience e l&#39;intervallo di confidenza proiettati. Le anteprime forniscono elenchi impaginati di profili di qualifica per una definizione di segmento, consentendo di confrontare i risultati con quanto previsto.

Stimando e visualizzando in anteprima il pubblico, potete sottoporre a test e ottimizzare i predicati PQL fino a ottenere un risultato desiderato, da cui poi utilizzarli in una definizione aggiornata del segmento.

Sono necessari due passaggi per visualizzare l’anteprima o ottenere una stima del segmento:

1. [Creare un processo di anteprima](#create-a-preview-job)
2. [Visualizzare la stima o l’anteprima](#view-an-estimate-or-preview) utilizzando l’ID del processo di anteprima

### Modalità di generazione delle stime

Gli esempi di dati vengono utilizzati per valutare i segmenti e stimare il numero di profili di qualifica. I nuovi dati vengono caricati in memoria ogni mattina (tra le 12AM-2AM PT, che è 7-9AM UTC), e tutte le query di segmentazione sono stimate utilizzando i dati di esempio di quel giorno. Di conseguenza, eventuali nuovi campi aggiunti o dati aggiuntivi raccolti saranno riportati nelle stime il giorno successivo.

La dimensione del campione dipende dal numero complessivo di entità nell&#39;archivio profili. Queste dimensioni di campione sono rappresentate nella seguente tabella:

| Entità nell&#39;archivio profili | Dimensione del campione |
| ------------------------- | ----------- |
| Meno di 1 milione | Set di dati completo |
| Da 1 a 20 milioni | 1 milione |
| Oltre 20 milioni | 5% del totale |

Le stime generalmente vengono eseguite su un periodo di 10-15 secondi, a partire da una stima approssimativa e con un perfezionamento man mano che vengono letti più record.

### Creare un processo di anteprima

Potete creare un nuovo processo di anteprima effettuando una richiesta POST all’ `/preview` endpoint.

Per istruzioni dettagliate sulla creazione di un processo di anteprima, consultate la guida [alle](../api/previews-and-estimates.md#create-preview)anteprime e agli endpoint delle stime.

### Visualizzare una stima o un&#39;anteprima

I processi di stima e anteprima vengono eseguiti in modo asincrono, in quanto le diverse query possono richiedere diversi tempi di completamento. Una volta avviata la query, potete utilizzare le chiamate API per recuperare (GET) lo stato corrente della stima o dell&#39;anteprima mentre progredisce.

Utilizzando l&#39; [!DNL Segmentation Service] API, potete cercare lo stato corrente di un processo di anteprima con il relativo ID. Se lo stato è &quot;RESULT_READY&quot;, è possibile visualizzare i risultati. Per visualizzare lo stato corrente di un processo di anteprima, consultate la sezione sul [recupero di una sezione](../api/previews-and-estimates.md#get-preview) del processo di anteprima nella guida alle anteprime e alle stime degli endpoint. Per verificare lo stato corrente di un processo di stima, consultare la sezione sul [recupero di un processo](../api/previews-and-estimates.md#get-estimate) di stima nella guida alle anteprime e agli endpoint delle stime.


## Passaggi successivi

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi creare un processo di segmento per creare un pubblico utilizzando l&#39; [!DNL Segmentation Service] API. Per informazioni dettagliate su come [valutare e accedere ai risultati](./evaluate-a-segment.md) del segmento, consulta l’esercitazione.