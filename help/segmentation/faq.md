---
title: Domande frequenti sui tipi di pubblico
description: Trova le risposte alle domande più frequenti sui tipi di pubblico.
source-git-commit: 4dbd20dd3ac596052a3390eb6d3731fac7095c0d
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---


# Domande frequenti

Adobe Experience Platform [!DNL Segmentation Service] fornisce un’interfaccia utente e un’API RESTful che consente di creare tipi di pubblico tramite le definizioni dei segmenti o altre origini dal tuo [!DNL Real-Time Customer Profile] dati. Questi tipi di pubblico sono configurati e gestiti centralmente su Platform e sono facilmente accessibili da qualsiasi soluzione Adobe. Di seguito è riportato un elenco di domande frequenti relative a tipi di pubblico e segmentazione.

## Posso accedere a Audience Portal e alla Composizione del pubblico?

Audience Portal e Audience Composition sono disponibili per tutti i clienti Real-Time CDP Prime e Ultimate (edizioni B2C, B2B e B2P) e per i clienti Journey Optimizer Select, Prime, Ultimate Starter e Ultimate.

Al momento, sono supportati solo i tipi di pubblico basati sul profilo. Il supporto per i tipi di pubblico basati sull’account verrà aggiunto in una versione successiva.

## Audience Portal supporta tipi di pubblico predefiniti generati esternamente?

Sì, i tipi di pubblico predefiniti generati esternamente sono supportati con Audience Portal. A questo punto puoi importare un pubblico generato esternamente tramite un file CSV. In futuro, potrai aggiungere tipi di pubblico tramite connettori di origine in batch o basati su streaming.

## È possibile riconciliare i dati sul pubblico generato esternamente con un profilo esistente in Platform?

Sì, se gli identificatori primari corrispondono, il pubblico generato esternamente verrà unito al profilo esistente in Platform. La riconciliazione di questi dati può richiedere fino a 24 ore. Se i dati del profilo non esistono già, verrà creato un nuovo profilo durante l’acquisizione dei dati.

## Posso utilizzare un pubblico generato esternamente per creare altri tipi di pubblico?

Sì, qualsiasi pubblico generato esternamente verrà visualizzato nell’inventario del pubblico e può essere utilizzato per creare tipi di pubblico all’interno di [Generatore di segmenti](./ui/segment-builder.md).

## Posso utilizzare attributi caricati esternamente come parte della segmentazione?

No, non puoi. Gli attributi del profilo devono essere attributi di lunga durata, mentre i dati del pubblico generati esternamente e caricati contengono solo dati contestuali associati a quel pubblico generato esternamente.

I dati contestuali o attributi di arricchimento del pubblico generato esternamente sono **non** duraturo, in quanto il loro ciclo di vita è legato al pubblico caricato. Di conseguenza, data la sua natura transitoria, questi attributi di arricchimento sono **non** disponibile per l’utilizzo nella segmentazione.

Tuttavia, quando mappi i tipi di pubblico a destinazioni in batch o basate su file, puoi utilizzare questi attributi di arricchimento generati esternamente per migliorare i tipi di pubblico e ulteriori attivazioni a valle.

Per ulteriori informazioni su questa funzionalità, consulta la guida su [attivazione dei dati sul pubblico nelle destinazioni di esportazione del profilo batch](../destinations/ui/activate-batch-profile-destinations.md#mapping).

## Posso attivare pubblici generati esternamente in Adobe Journey Optimizer?

A questo punto, no. Tuttavia, questa funzionalità sarà disponibile a breve.

## Posso eliminare un pubblico generato esternamente?

A questo punto, no. Al suo posto, puoi disattivare o archiviare questo pubblico. In questo stato, i profili **will** rimane attivo per l’utilizzo in applicazioni a valle. Il supporto per l’eliminazione dei tipi di pubblico generati esternamente verrà aggiunto in una versione successiva.

## In che modo Audience Portal e Audience Composition interagiranno con il rilascio di Real-Time CDP Partner Data?

Audience Portal e Audience Composition interagiranno con i dati dei partner in due modi:

1. Se acquisisci un elenco di potenziali clienti fornito dal partner utilizzando la classe e il flusso di lavoro Prospect Profile, i potenziali clienti verranno mantenuti **separatamente** da unire i profili cliente in Profile Service. Di conseguenza, gli elenchi di potenziali clienti **non** sono disponibili in Audience Portal o in Audience Composition.
2. Se utilizzi gli attributi forniti dal partner per arricchire **esistente** profili di prime parti, tipi di pubblico arricchiti di dati dei partner **will** sono disponibili sia in Audience Portal che in Audience Composition.

## Posso utilizzare tipi di pubblico generati esternamente in Composizione pubblico?

A questo punto, no. Tuttavia, questa funzionalità dovrebbe essere disponibile a breve.

## Posso inviare tipi di pubblico da Audience Composition a tutte le destinazioni e i canali a valle?

A questo punto, no. Attualmente, puoi utilizzare i tipi di pubblico da Composizione pubblico in Campagne Adobe Journey Optimizer e destinazioni di Real-time CDP. I Percorsi Adobe Journey Optimizer saranno supportati in una versione futura.

## Ci sono dei guardrail sul numero di composizioni?

In questo momento, è possibile avere solo **10** composizioni pubblicate per sandbox. Questo guardrail verrà incrementato in una versione futura.

## Quali sono i guardrail del flusso di lavoro per Audience Composition?

Il posizionamento del componente di composizione segue una struttura rigida come segue:

1. Tu **sempre** inizia con [!UICONTROL Pubblico] blocca per selezionare l’attività iniziale. Puoi avere un massimo di **uno** [!UICONTROL Pubblico] blocco.
2. Facoltativamente, puoi aggiungere una [!UICONTROL Escludi] blocco che segue il [!UICONTROL Pubblico] blocco.
3. Facoltativamente, puoi aggiungere una [!UICONTROL Arricchire] blocco che segue il [!UICONTROL Escludi] blocco.
4. Facoltativamente, puoi aggiungere una [!UICONTROL Classifica] o [!UICONTROL Dividi] blocco. È possibile **solo** avere uno di questi blocchi per composizione.
5. Tu **sempre** termina con [!UICONTROL Salva] blocca per salvare il pubblico.

Per ulteriori dettagli sull’utilizzo di Audience Composition, consulta la sezione [Guida dell’interfaccia utente di Audience Composition](./ui/audience-composition.md).

## Posso utilizzare una composizione di pubblico in un&#39;altra composizione?

No, i tipi di pubblico sono stati creati utilizzando la composizione del pubblico **non può** essere utilizzato come input in un’altra composizione di pubblico.

## Come funziona la suddivisione in Audience Composition?

La suddivisione del pubblico consente di suddividere ulteriormente il pubblico in gruppi più piccoli. Questa divisione forza l&#39;esclusività reciproca tra i gruppi. Ciò significa che se un record soddisfa i criteri di più percorsi di suddivisione, gli verrà assegnato il **primo** percorso da sinistra e **non** assegnati a uno qualsiasi degli altri percorsi.

Per ulteriori informazioni sul blocco Split, leggi [Guida dell’interfaccia utente di Audience Composition](./ui/audience-composition.md#split).

## Posso utilizzare tutti i tipi di segmentazione nel flusso di lavoro Composizione pubblico?

Sì, tutti i tipi di segmentazione ([segmentazione batch, segmentazione in streaming e segmentazione Edge](./home.md#evaluate-segments)) sono supportate nel flusso di lavoro Composizione pubblico. Tuttavia, poiché le composizioni vengono attualmente eseguite solo una volta al giorno, anche se sono inclusi i tipi di pubblico valutati in streaming o edge, il risultato sarà basato sull’iscrizione al pubblico al momento dell’esecuzione della composizione.

## Come posso confermare l’appartenenza di un profilo a un pubblico?

Per confermare l’iscrizione al pubblico di un profilo, visita la pagina dei dettagli del profilo che desideri confermare. Seleziona **[!UICONTROL Attributi]**, seguito da **[!UICONTROL Visualizza JSON]** e confermare che il `segmentMembership` L’oggetto contiene l’ID del pubblico.
