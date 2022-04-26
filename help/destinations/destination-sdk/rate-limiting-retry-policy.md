---
description: Scopri come Experience Platform gestisce diversi tipi di errori restituiti dalle destinazioni di streaming e come tenta nuovamente di inviare dati alla piattaforma di destinazione.
title: Limitazione dei tassi e nuovi tentativi per le destinazioni di streaming create con Destination SDK
source-git-commit: ec50608f6454dd619c30b6337f454561844183ba
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Limitazione dei tassi e nuovi tentativi per le destinazioni di streaming create con Destination SDK

## Panoramica {#overview}

Le destinazioni create dai partner possono restituire vari errori e avere diverse politiche di limitazione delle tariffe. Questa pagina spiega come Experience Platform gestisce diversi tipi di errori restituiti dalle destinazioni di streaming.

Quando configuri una destinazione utilizzando Destination SDK, puoi selezionare due tipi di aggregazione: [aggregazione dello sforzo migliore](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) e [aggregazione configurabile](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). A seconda del tipo di aggregazione selezionato, leggere di seguito come Experience Platform gestisce gli errori e le limitazioni di velocità.

## Aggregazione degli sforzi migliori {#best-effort-aggregation}

Per tutte le chiamate HTTP effettuate alla destinazione con errore, Experience Platform tenta di effettuare nuovamente la chiamata immediatamente dopo la prima chiamata. Se la chiamata continua a non riuscire al secondo tentativo, Experience Platform rilascia la chiamata e non ritenta una terza volta.

## Aggregazione configurabile {#configurable-aggregation}

Nel caso di piattaforme di destinazione configurate con aggregazione configurabile, l’Experience Platform distingue tra il tipo di errore restituito dalla piattaforma:

* Errori in cui Experience Platform tenta nuovamente di inviare i dati alla piattaforma:
   * Codici di risposta HTTP 420 e 429
   * Codici di risposta HTTP superiori a 500
* Errori in cui Experience Platform *non* tenta di inviare i dati alla piattaforma: tutti gli altri restituiti dalla piattaforma

### Metodo del tentativo descritto {#retry-approach}

Di seguito è descritto l’approccio Experience Platform per l’aggregazione configurabile. Questo esempio presuppone che Experience Platform invii dati a una piattaforma di destinazione che inizia a restituire codici di errore 429 se riceve più di 50.000 richieste al minuto:

* Minuto 1: Experience Platform aggrega batch da 40.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua richieste HTTP 40k e tutte hanno esito positivo.
* Minuto 2: Experience Platform aggrega batch da 70.000 con profili da inviare alla piattaforma di destinazione. Experience Platform esegue richieste HTTP 70k e 50k ha successo. Gli altri 20.000 ricevono un errore di limitazione della velocità dall&#39;endpoint e verranno tentati di nuovo in 30 minuti.
* Minuto 3: Experience Platform aggrega batch da 30.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua richieste HTTP 30.000 e tutte hanno esito positivo.
* ...
* ...
* Minuto 32: L&#39;Experience Platform tenta nuovamente di inviare i batch da 20.000 che hanno avuto esito negativo al minuto 2. Tutte le chiamate hanno esito positivo.

## Passaggi successivi {#next-steps}

Ora sai in che modo Experience Platform gestisce gli errori e classifica le limitazioni dalle piattaforme di destinazione, a seconda del criterio di aggregazione selezionato al momento della configurazione della destinazione di streaming. Successivamente, consulta la seguente documentazione:

* [Verifica la configurazione di destinazione](/help/destinations/destination-sdk/test-destination.md)
* [Invia per la revisione di una destinazione creata in Destination SDK](/help/destinations/destination-sdk/submit-destination.md)
