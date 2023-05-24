---
description: Scopri come Experience Platform gestisce diversi tipi di errori restituiti dalle destinazioni di streaming e come tenta di inviare dati alla piattaforma di destinazione.
title: Limitazione della frequenza e criteri per nuovi tentativi per le destinazioni di streaming create con Destination SDK
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Limitazione della frequenza e criteri per nuovi tentativi per le destinazioni di streaming create con Destination SDK

Le destinazioni create dai partner possono restituire vari errori e disporre di criteri di limitazione della frequenza diversi. Questa pagina spiega come Experience Platform gestisce diversi tipi di errori restituiti dalle destinazioni di streaming.

Quando configuri una destinazione utilizzando Destination SDK, puoi scegliere tra due tipi di aggregazione: [aggregazione della migliore fatica](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) e [aggregazione configurabile](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). A seconda del tipo di aggregazione selezionato, leggi di seguito come Experience Platform gestisce gli errori e le limitazioni della frequenza.

## Aggregazione ottimale {#best-effort-aggregation}

Per eventuali chiamate HTTP effettuate sulla destinazione che hanno esito negativo, Experience Platform tenta di effettuare di nuovo la chiamata una volta in più, immediatamente dopo la prima chiamata. Se al secondo tentativo la chiamata non riesce, Experience Platform la abbandona e non la ritenta una terza volta.

## Aggregazione configurato {#configurable-aggregation}

Nel caso delle piattaforme di destinazione impostate con aggregazione configurabile, l’Experience Platform distingue tra il tipo di errore restituito dalla piattaforma:

* Errori in cui Experience Platform tenta di inviare i dati alla piattaforma:
   * Codici di risposta HTTP 420 e 429
   * Codici di risposta HTTP superiori a 500
* Errori in cui Experience Platform *non* riprova a inviare i dati alla piattaforma: tutti gli altri restituiti dalla piattaforma

### Descrizione dell’approccio Riprova {#retry-approach}

L’approccio di Experience Platform per l’aggregazione configurabile è descritto di seguito. L’esempio presuppone che Experience Platform invii dati a una piattaforma di destinazione che inizia a restituire codici di errore 429 se riceve più di 50.000 richieste al minuto:

* Minuto 1: Experience Platform aggrega batch da 40.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua 40.000 richieste HTTP e tutte hanno esito positivo.
* Minuto 2: Experience Platform aggrega batch da 70.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua 70.000 richieste HTTP e 50.000 hanno esito positivo. Gli altri 20.000 ricevono un errore di limitazione della frequenza dall’endpoint e verranno tentati di nuovo tra 30 minuti.
* Minuto 3: Experience Platform aggrega batch da 30.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua 30.000 richieste HTTP e tutte hanno esito positivo.
* ...
* ...
* Minuto 32: Experience Platform tenta nuovamente di inviare i batch da 20.000 che non sono riusciti al minuto 2. Tutte le chiamate sono riuscite.

## Passaggi successivi {#next-steps}

Ora sai come Experience Platform gestisce gli errori e la limitazione della frequenza dalle piattaforme di destinazione, a seconda dei criteri di aggregazione selezionati al momento della configurazione della destinazione di streaming. A questo punto, consulta la seguente documentazione:

* [Verifica la configurazione di destinazione](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Invia per la revisione una destinazione creata in Destination SDK](../guides/submit-destination.md)
