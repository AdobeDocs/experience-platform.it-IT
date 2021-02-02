---
keywords: ' Experience Platform;home;argomenti popolari;segmento;segmento;creare segmento;segmentazione;creare un segmento;segmentazione;creare un segmento;Servizio segmentazione;'
solution: Experience Platform
title: Creazione di un segmento
topic: tutorial
type: Tutorial
description: Questo documento fornisce un'esercitazione per lo sviluppo, il test, la visualizzazione in anteprima e il salvataggio di una definizione di segmento mediante l'API di Adobe Experience Platform Segmentation Service.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---


# Creazione di un segmento

Questo documento fornisce un&#39;esercitazione per sviluppare, testare, visualizzare in anteprima e salvare una definizione di segmento utilizzando [[!DNL Adobe Experience Platform Segmentation Service API]](../api/getting-started.md).

Per informazioni su come creare segmenti utilizzando l&#39;interfaccia utente, consultare la [Guida per la generazione di segmenti](../ui/overview.md).

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella creazione di segmenti di pubblico. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate alle [!DNL Platform] API.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md#how-do-i-format-an-api-request) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

### Raccogli valori per le intestazioni richieste

Per effettuare chiamate alle [!DNL Platform] API, è innanzitutto necessario completare l&#39;esercitazione sull&#39;autenticazione [a2/>. ](https://www.adobe.com/go/platform-api-authentication-en) Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API [!DNL Experience Platform], come illustrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in [!DNL Experience Platform] sono isolate in sandbox virtuali specifiche. Tutte le richieste alle [!DNL Platform] API richiedono un&#39;intestazione che specifica il nome della sandbox in cui verrà eseguita l&#39;operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in [!DNL Platform], consultate la documentazione di [panoramica sulla sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un&#39;intestazione aggiuntiva:

- Content-Type: application/json

## Sviluppo di una definizione di segmento

Il primo passo nella segmentazione consiste nel definire un segmento, rappresentato in un costrutto chiamato definizione di segmento. Una definizione di segmento è un oggetto che racchiude una query scritta in [!DNL Profile Query Language] (PQL). Questo oggetto è anche denominato predicato PQL. I predicati PQL definiscono le regole per il segmento in base alle condizioni relative a qualsiasi record o dati delle serie temporali forniti a [!DNL Real-time Customer Profile]. Per ulteriori informazioni sulla scrittura di query PQL, vedere la [Guida PQL](../pql/overview.md).

Puoi creare una nuova definizione di segmento effettuando una richiesta di POST all&#39;endpoint `/segment/definitions` nell&#39;API [!DNL Segmentation]. L&#39;esempio seguente illustra come formattare una richiesta di definizione, incluse le informazioni necessarie per definire correttamente un segmento.

Per una spiegazione dettagliata su come definire un segmento, leggere la [guida per gli sviluppatori di definizione del segmento](../api/segment-definitions.md#create).

## Stima e anteprima di un&#39;audience {#estimate-and-preview-an-audience}

Mentre sviluppate la definizione del segmento, potete utilizzare gli strumenti di stima e anteprima all&#39;interno di [!DNL Real-time Customer Profile] per visualizzare le informazioni a livello di riepilogo per garantire che l&#39;audience attesa sia isolata. Le stime forniscono informazioni statistiche sulla definizione di un segmento, come la dimensione dell&#39;audience e l&#39;intervallo di confidenza proiettati. Le anteprime forniscono elenchi impaginati di profili di qualifica per una definizione di segmento, consentendo di confrontare i risultati con quanto previsto.

Stimando e visualizzando in anteprima il pubblico, potete sottoporre a test e ottimizzare i predicati PQL fino a ottenere un risultato desiderato, da cui poi utilizzarli in una definizione aggiornata del segmento.

Sono necessari due passaggi per visualizzare l’anteprima o ottenere una stima del segmento:

1. [Creare un processo di anteprima](#create-a-preview-job)
2. [Visualizzare la stima o l’](#view-an-estimate-or-preview) anteprima utilizzando l’ID del processo di anteprima

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

Potete creare un nuovo processo di anteprima effettuando una richiesta di POST all&#39;endpoint `/preview`.

Per istruzioni dettagliate sulla creazione di un processo di anteprima, consultate la [guida alle anteprime e agli endpoint delle stime](../api/previews-and-estimates.md#create-preview).

### Visualizzare una stima o un&#39;anteprima

I processi di stima e anteprima vengono eseguiti in modo asincrono, in quanto le diverse query possono richiedere diversi tempi di completamento. Una volta avviata la query, potete utilizzare le chiamate API per recuperare (GET) lo stato corrente della stima o dell&#39;anteprima mentre progredisce.

Utilizzando l&#39;API [!DNL Segmentation Service], potete cercare lo stato corrente di un processo di anteprima in base al relativo ID. Se lo stato è &quot;RESULT_READY&quot;, è possibile visualizzare i risultati. Per verificare lo stato corrente di un processo di anteprima, consultare la sezione relativa al recupero di una sezione del processo di anteprima](../api/previews-and-estimates.md#get-preview) nella guida anteprime e stime degli endpoint. [ Per verificare lo stato corrente di un processo stimato, consultare la sezione relativa al recupero di un processo stimato](../api/previews-and-estimates.md#get-estimate) nella guida alle anteprime e alle stime degli endpoint.[


## Passaggi successivi

Dopo aver sviluppato, testato e salvato la definizione del segmento, puoi creare un processo di segmento per creare un pubblico utilizzando l&#39;API [!DNL Segmentation Service]. Per informazioni dettagliate su come eseguire questa operazione, vedere l&#39;esercitazione su [valutazione e accesso ai risultati del segmento](./evaluate-a-segment.md).