---
description: Scopri come Experience Platform gestisce i diversi tipi di errori restituiti dalle destinazioni di streaming e come tenta di inviare dati alla piattaforma di destinazione.
title: Limitazione della frequenza e criteri per nuovi tentativi per le destinazioni di streaming create con Destination SDK
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Limitazione della frequenza e criteri per nuovi tentativi per le destinazioni di streaming create con Destination SDK

Le destinazioni create dai partner possono restituire vari errori e disporre di criteri di limitazione della frequenza diversi. Questa pagina spiega come Experience Platform gestisce diversi tipi di errori restituiti dalle destinazioni di streaming.

Durante la configurazione di una destinazione tramite Destination SDK, è possibile selezionare tra due tipi di aggregazione: [aggregazione ottimizzata](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) e [aggregazione configurabile](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). A seconda del tipo di aggregazione selezionato, leggi di seguito come Experience Platform gestisce gli errori e le limitazioni della frequenza.

## Aggregazione ottimale {#best-effort-aggregation}

Experience Platform ritenta le chiamate che restituiscono i seguenti codici di risposta HTTP: **403, 408, 409, 429, 500, 502, 503, 504**. Vengono eseguiti due nuovi tentativi agli intervalli seguenti:

* Primo tentativo: dopo 15 secondi
* Secondo tentativo: dopo 30 secondi

Experience Platform *non* ritenta le chiamate che restituiscono altri codici di risposta HTTP, ad esempio 400 (richiesta non valida). Se la chiamata continua a non riuscire dopo entrambi i tentativi, Experience Platform interrompe l’attivazione e non ritenta.

Per richiedere un criterio diverso per i nuovi tentativi per flussi di dati specifici, contatta l’Assistenza clienti.

## Aggregazione configurato {#configurable-aggregation}

Nel caso delle piattaforme di destinazione impostate con aggregazione configurabile, Experience Platform distingue tra il tipo di errore restituito dalla piattaforma:

* Errori in cui Experience Platform tenta di inviare i dati alla piattaforma:
   * Codici di risposta HTTP 420 e 429
   * Codici di risposta HTTP superiori a 500
* Errori in cui Experience Platform *non* tenta di inviare nuovamente i dati alla piattaforma: tutti gli altri sono restituiti dalla piattaforma

### Descrizione dell’approccio Riprova {#retry-approach}

L’approccio di Experience Platform per l’aggregazione configurabile è descritto di seguito. Questo esempio presuppone che Experience Platform invii dati a una piattaforma di destinazione che inizia a restituire codici di errore 429 se riceve più di 50.000 richieste al minuto:

* Minuto 1: Experience Platform aggrega batch da 40.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua 40.000 richieste HTTP e tutte hanno esito positivo.
* Minuto 2: Experience Platform aggrega batch da 70.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua 70.000 richieste HTTP e 50.000 sono riuscite. Gli altri 20.000 ricevono un errore di limitazione della frequenza dall’endpoint e verranno tentati di nuovo tra 30 minuti.
* Minuto 3: Experience Platform aggrega batch da 30.000 con profili da inviare alla piattaforma di destinazione. Experience Platform effettua 30.000 richieste HTTP e tutte hanno esito positivo.
* ...
* ...
* Minuto 32: Experience Platform tenta nuovamente di inviare i batch da 20.000 che non sono riusciti al minuto 2. Tutte le chiamate sono riuscite.

## Passaggi successivi {#next-steps}

Ora sai come Experience Platform gestisce gli errori e la limitazione della frequenza dalle piattaforme di destinazione, a seconda dei criteri di aggregazione selezionati al momento della configurazione della destinazione di streaming. A questo punto, consulta la seguente documentazione:

* [Verifica la configurazione di destinazione](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Invia per la revisione di una destinazione creata in Destination SDK](../guides/submit-destination.md)
