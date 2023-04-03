---
title: Visualizzazione dell’editor di convalida
description: Questa guida descrive informazioni sulla vista Editor di convalida in Adobe Experience Platform Assurance.
source-git-commit: 5778d4db27d0f57281821dc8e042a31b69745514
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 3%

---


# Vista Editor di convalida

L’Editor di convalida consente di gestire in modo rapido e semplice le funzioni JavaScript per convalidare gli eventi in una sessione di Adobe Experience Platform Assurance. Ogni funzione riceve gli eventi in una sessione di Assurance. Puoi scrivere funzioni per convalidare la configurazione client, le condizioni dell’evento, i test e i casi d’uso.

## Guida introduttiva all’Editor di convalida

Dopo [configurazione di Assurance](../tutorials/implement-assurance.md), sul **[!UICONTROL Pagina principale]** visualizza, seleziona **[!UICONTROL Editor di convalida]**.

![Convalida-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Scrivere una funzione di convalida

Questa funzione consente di creare, modificare o eliminare funzioni di convalida per le sessioni di Adobe Experience Platform Assurance.

1. Seleziona **[!UICONTROL Crea nuova convalida]**.
2. Inserisci un **name** per identificare la convalida, fornisci un **categoria** e **descrizione**.
3. Modifica il codice nell’editor per convalidare gli eventi per la sessione di Assurance.

Una volta completati i test della funzione, seleziona **[!UICONTROL Pubblica]** per salvare la convalida.

### Definizione evento

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `uuid` | Stringa | Identificatore univoco universale per l&#39;evento. |
| `timestamp` | Numero | Timestamp dal client quando l’evento è stato inviato ad Assurance. |
| `eventNumber` | Numero | Utilizzato per ordinare quando l’evento è stato inviato. Questa chiave è utile quando gli eventi hanno la stessa marca temporale. |
| `vendor` | Stringa | Stringa di identificazione del fornitore nel formato del nome di dominio inverso (ad esempio, com.adobe.Assurance). |
| `type` | Stringa | Utilizzato per indicare il tipo di evento. |
| `payload` | Oggetto | Definisce i dati per l&#39;evento e contiene proprietà univoche e comuni. Alcune proprietà comuni includono `ACPExtensionEventSource` e `ACPExtensionEventType`. |
| `annotations` | Array | Matrice di oggetti annotazione. |

### Definizione dell&#39;annotazione

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `uuid` | Stringa | Identificatore univoco universale per l&#39;annotazione. |
| `type` | Stringa | Utilizzato per indicare il tipo di annotazione ed è in genere il nome del plug-in (ad esempio, analytics). |
| `payload` | Oggetto | Definisce i dati che devono integrare l’evento. Per Adobe Analytics, è qui che sono contenuti i dati degli hit post-elaborati. |

### Risultati della convalida

La funzione di convalida deve restituire un oggetto contenente quanto segue:

| Chiave | Tipo | Descrizione |
| :--- | :--- | :--- |
| `message` | Stringa | Messaggio di convalida da visualizzare nei risultati di riepilogo. |
| `events` | Array | Matrice di uuuid evento da segnalare come corrispondente o non corrispondente. |
| `links` | Array | Matrice di `ValidationResultLink` oggetti che fanno riferimento alla documentazione e ad altre risorse `{( type: 'doc'|'product', url: String )}` |
| `result` | Stringa | Questo è il risultato della convalida ed è previsto che sia una delle stringhe enumerate: &quot;corrisponde&quot;, &quot;non corrisponde&quot;, &quot;sconosciuto&quot; |

## Visualizzazione dei risultati della convalida

I risultati della funzione vengono visualizzati nella sezione dei risultati sotto l&#39;editor di codice. Se il risultato della convalida è `unknown` o `not matched` e `events` array con uno o più `uuids`, gli eventi vengono evidenziati nella timeline con i seguenti colori:

* Verde - abbinato
* Arancione - sconosciuto
* Rosso - non corrispondente

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Risoluzione dei problemi

Puoi aggiungere `console.log()` nella funzione per stampare gli elementi nella console dello sviluppatore. In alternativa, è possibile utilizzare la proprietà message dell&#39;oggetto result per eseguire il debug dei messaggi nel pannello dei risultati.

Se si verifica un errore nell&#39;editor di codice JavaScript, viene visualizzato uno stato di errore insieme al motivo.

Per ulteriori informazioni sulle convalide, visita [Convalida Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins) GitHub. Di seguito sono riportati alcuni esempi di convalide di proprietà di Adobe. Consulta la sezione [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) per descrizioni più dettagliate delle convalide.
