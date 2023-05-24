---
title: Visualizzazione editor convalida
description: Questa guida contiene informazioni dettagliate sulla visualizzazione Editor di convalida in Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---

# Vista Editor di convalida

L’editor di convalida consente di gestire in modo rapido e semplice le funzioni JavaScript per convalidare gli eventi in una sessione di Adobe Experience Platform Assurance. Ogni funzione riceve gli eventi in una sessione Assurance. Puoi scrivere funzioni per convalidare la configurazione del client, le condizioni degli eventi, i test e i casi d’uso.

## Introduzione all’editor di convalida

Dopo [impostazione di Assurance](../tutorials/implement-assurance.md), sulla **[!UICONTROL Home]** visualizza, seleziona **[!UICONTROL Editor di convalida]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Scrivere una funzione di convalida

Questa funzione consente di creare, modificare o eliminare funzioni di convalida per le sessioni di Adobe Experience Platform Assurance.

1. Seleziona **[!UICONTROL Crea una nuova convalida]**.
2. Immetti un **nome** per identificare la convalida, fornisci una **categoria** e un **descrizione**.
3. Modifica il codice nell’editor per convalidare gli eventi per la sessione Assurance.

Una volta completati i test di funzione, seleziona **[!UICONTROL Pubblica]** per salvare la convalida.

### Definizione evento

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `uuid` | Stringa | Identificatore universale univoco dell’evento. |
| `timestamp` | Numero | Timestamp dal client quando l’evento è stato inviato ad Assurance. |
| `eventNumber` | Numero | Utilizzato per ordinare quando l’evento è stato inviato. Questa chiave è utile quando gli eventi hanno la stessa marca temporale. |
| `vendor` | Stringa | Stringa di identificazione del fornitore nel formato del nome di dominio inverso (ad esempio, com.adobe.assurance). |
| `type` | Stringa | Utilizzato per indicare il tipo di evento. |
| `payload` | Oggetto | Definisce i dati per l’evento e contiene proprietà univoche e comuni. Alcune proprietà comuni includono `ACPExtensionEventSource` e `ACPExtensionEventType`. |
| `annotations` | Array | Matrice di oggetti di annotazione. |

### Definizione dell’annotazione

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `uuid` | Stringa | Identificatore universale univoco dell’annotazione. |
| `type` | Stringa | Utilizzato per indicare il tipo di annotazione; in genere è il nome del plug-in (ad esempio, analytics). |
| `payload` | Oggetto | Definisce i dati che devono integrare l’evento. Per Adobe Analytics, è qui che sono contenuti i dati hit post-elaborati. |

### Risultati convalida

La funzione di convalida deve restituire un oggetto contenente quanto segue:

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `message` | Stringa | Messaggio di convalida da visualizzare nei risultati di riepilogo. |
| `events` | Array | Array di UUID evento da segnalare come corrispondente o non corrispondente. |
| `links` | Array | Un array di `ValidationResultLink` oggetti per fare riferimento alla documentazione e ad altre risorse `{( type: 'doc'|'product', url: String )}` |
| `result` | Stringa | Questo è il risultato della convalida e deve essere una delle stringhe enumerate: &quot;matched&quot;, &quot;not matched&quot;, &quot;unknown&quot; |

## Visualizzare i risultati della convalida

I risultati della funzione vengono visualizzati nella sezione dei risultati sotto l’editor di codice. Se il risultato della convalida è `unknown` o `not matched` e `events` l&#39;array ha uno o più `uuids`, gli eventi vengono evidenziati nella timeline con i seguenti colori:

* Verde - corrisponde
* Arancione - sconosciuto
* Rosso - non corrispondente

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Risoluzione dei problemi

Puoi aggiungere `console.log()` nella tua funzione di stampare gli elementi in developer console. In alternativa, è possibile utilizzare la proprietà message dell&#39;oggetto result per eseguire il debug dei messaggi nel pannello dei risultati.

Se si verifica un errore nell’editor di codice JavaScript, viene visualizzato uno stato di errore e il motivo.

Per ulteriori informazioni sulle convalide, visita il [Convalide Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins) GitHub. Qui troverai alcuni esempi di convalide di proprietà di Adobe. Consulta la [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) per una descrizione più dettagliata delle convalide.
