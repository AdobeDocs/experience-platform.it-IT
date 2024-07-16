---
title: Vista Editor di convalida
description: Questa guida contiene informazioni dettagliate sulla vista Editor di convalida in Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 100%

---

# Vista Editor di convalida

L’Editor di convalida consente di gestire in modo rapido e semplice le funzioni JavaScript per convalidare gli eventi in una sessione di Adobe Experience Platform Assurance. Ogni funzione riceve gli eventi in una sessione di Assurance. Puoi scrivere funzioni per convalidare la configurazione del client, le condizioni degli eventi, i test e i casi d’uso.

## Introduzione all’Editor di convalida

Dopo aver [configurato Assurance](../tutorials/implement-assurance.md), sulla vista **[!UICONTROL Home]**, seleziona l’**[!UICONTROL Editor di convalida]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Scrivere una funzione di convalida

Questa funzione consente di creare, modificare o eliminare funzioni di convalida per le sessioni di Adobe Experience Platform Assurance.

1. Seleziona **[!UICONTROL Crea una nuova convalida]**.
2. Immetti un **nome** per identificare la convalida, quindi specifica una **categoria** e una **descrizione**.
3. Modifica il codice nell’editor per convalidare gli eventi per la sessione di Assurance.

Una volta completati i test di funzione, seleziona **[!UICONTROL Pubblica]** per salvare la convalida.

### Definizione dell’evento

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `uuid` | Stringa | Identificatore univoco universale dell’evento. |
| `timestamp` | Numero | Timestamp ricevuta dal client quando l’evento è stato inviato ad Assurance. |
| `eventNumber` | Numero | Utilizzato per mettere in ordine quando l’evento è stato inviato. Questa chiave è utile quando gli eventi hanno lo stesso timestamp. |
| `vendor` | Stringa | Stringa di identificazione del fornitore secondo il formato del nome di dominio inverso (ad esempio, com.adobe.assurance). |
| `type` | Stringa | Utilizzata per indicare il tipo di evento. |
| `payload` | Oggetto | Definisce i dati per l’evento e contiene proprietà univoche e comuni. Alcune proprietà comuni includono `ACPExtensionEventSource` e `ACPExtensionEventType`. |
| `annotations` | Array | Un array di oggetti di annotazione. |

### Definizione dell’annotazione

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `uuid` | Stringa | Identificatore univoco universale dell’annotazione. |
| `type` | Stringa | Utilizzata per indicare il tipo di annotazione e in genere è il nome del plug-in (ad esempio, Analytics). |
| `payload` | Oggetto | Definisce i dati che devono integrare l’evento. Per Adobe Analytics, è qui che sono contenuti i dati hit in fase di post-elaborazione. |

### Risultati della convalida

La funzione di convalida deve restituire un oggetto contenente quanto segue:

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `message` | Stringa | Il messaggio di convalida da visualizzare nei risultati di riepilogo. |
| `events` | Array | Array di eventi UUID da segnalare come corrispondente o non corrispondente. |
| `links` | Array | Un array di oggetti `ValidationResultLink` per fare riferimento alla documentazione e ad altre risorse `{( type: 'doc'|'product', url: String )}` |
| `result` | Stringa | Questo è il risultato della convalida e deve essere una delle stringhe enumerate: “corrispondente”, “non corrispondente”, “sconosciuto” |

## Visualizzare i risultati della convalida

I risultati della funzione vengono visualizzati nella sezione dei risultati sotto l’editor di codice. Se il risultato della convalida è `unknown` o `not matched` e l’array `events` dispone di uno o più `uuids`, gli eventi vengono evidenziati nella timeline con i seguenti colori:

* Verde - corrispondente
* Arancione - sconosciuto
* Rosso - non corrispondente

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Risoluzione dei problemi

Puoi aggiungere `console.log()` nella tua funzione per stampare gli elementi in Developer Console. In alternativa, è possibile utilizzare la proprietà messaggio del risultato oggetto per eseguire il debug dei messaggi nel pannello dei risultati.

Se si verifica un errore nell’editor di codice JavaScript, viene visualizzato uno stato di errore e il motivo.

Per ulteriori informazioni sulle convalide, visita il GitHub [Convalide di Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins). Qui troverai alcuni esempi di convalide di proprietà di Adobe. Per una descrizione più dettagliata sulle convalide, consulta la [wiki](https://github.com/adobe/griffon-validation-plugins/wiki).
