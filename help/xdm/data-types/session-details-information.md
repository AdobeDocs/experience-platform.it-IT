---
title: Tipo di dati informazioni dettagli sessione
description: Scopri il tipo di dati Experience Data Model (XDM) dei dettagli della sessione.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '1375'
ht-degree: 8%

---

# [!UICONTROL Informazioni sui dettagli della sessione] tipo di dati

[!UICONTROL Informazioni sui dettagli della sessione] è un tipo di dati Experience Data Model (XDM) standard che tiene traccia dei dati relativi alle sessioni di riproduzione di contenuti multimediali. Lo schema include un’ampia gamma di proprietà che forniscono informazioni approfondite sul modo in cui viene utilizzato il contenuto multimediale. Utilizza il [!UICONTROL Informazioni sui dettagli della sessione] tipo di dati per acquisire il coinvolgimento dell’utente registrando eventi di riproduzione, interazioni pubblicitarie, indicatori di avanzamento, pause e altre metriche. Questo offre informazioni preziose sul comportamento degli utenti e sui modelli di consumo dei contenuti.

+++Selezionare questa opzione per visualizzare un diagramma del tipo di dati Dettagli sessione.
![Diagramma del tipo di dati Dettagli sessione.](../images/data-types/session-details-information.png)
+++

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL ID sessione multimediale] | `ID` | string | Il [!UICONTROL ID sessione multimediale] identifica un’istanza di un flusso di contenuto univoco per una singola riproduzione. |
| [!UICONTROL ID contenuto] | `name` | string | **Obbligatorio** Il [!UICONTROL ID contenuto] è un identificatore univoco del contenuto. Può essere utilizzato per effettuare il collegamento ad altri ID di settore o CMS. |
| [!UICONTROL Nome contenuto] | `friendlyName` | Stringa | Il [!UICONTROL Nome contenuto] è il nome &quot;descrittivo&quot; (leggibile dall’uomo) del contenuto. |
| [!UICONTROL Lunghezza contenuti multimediali] | `length` | Intero | **Obbligatorio** Il [!UICONTROL Lunghezza contenuti multimediali] contiene la lunghezza/runtime della clip: si tratta della lunghezza massima (o durata) del contenuto utilizzato (in secondi). |
| [!UICONTROL Tipo di contenuto broadcast] | `contentType` | Stringa | **Obbligatorio** Il [!UICONTROL Tipo di contenuto broadcast] della consegna del flusso. Valori disponibili per [!UICONTROL Tipo di flusso] include:<br>Audio: &quot;song&quot;, &quot;podcast&quot;, &quot;audiobook&quot; e &quot;radio&quot;;<br>Video: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; e &quot;DVoD&quot;.<br>I clienti possono fornire valori personalizzati per questo parametro. |
| [!UICONTROL Nome del lettore di contenuti] | `playerName` | Stringa | **Obbligatorio** Nome del lettore di contenuti. |
| [!UICONTROL Canale contenuto] | `channel` | Stringa | **Obbligatorio** Il [!UICONTROL Canale contenuto] è il canale di distribuzione da cui è stato riprodotto il contenuto. |
| [!UICONTROL Versione] | `appVersion` | Stringa | Versione SDK utilizzata dal lettore. Questo potrebbe avere qualsiasi valore personalizzato che abbia senso per il lettore. |
| [!UICONTROL Nome serie] | `show` | Stringa | Il Nome Del Programma/Serie. Il nome del programma è necessario solo se lo spettacolo fa parte di una serie. |
| [!UICONTROL Numero della stagione] | `season` | Stringa | Il [!UICONTROL Numero della stagione] a cui appartiene il programma. La stagione della serie è necessaria solo se lo spettacolo fa parte di una serie. |
| [!UICONTROL Numero dell’episodio] | `episode` | Stringa | Numero dell’episodio. |
| [!UICONTROL ID risorsa] | `assetID` | Stringa | Il [!UICONTROL ID risorsa] è l’identificatore univoco del contenuto della risorsa multimediale, ad esempio l’identificatore dell’episodio di una serie TV, della risorsa del film o dell’evento live. In genere questi ID hanno origine da autorità metadati come EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni. |
| [!UICONTROL Genere] | `genre` | Stringa | Tipo o raggruppamento di contenuti definiti dal produttore del contenuto. I valori devono essere delimitati da virgole nell’implementazione delle variabili. |
| [!UICONTROL Data della prima messa in onda] | `firstAirDate` | Stringa | La data in cui il contenuto è andato in onda per la prima volta in televisione. Qualsiasi formato data è accettabile, ma l’Adobe consiglia: AAAA-MM-GG. |
| [!UICONTROL Data prima versione digitale] | `firstDigitalDate` | Stringa | La data in cui il contenuto è andato in onda per la prima volta su qualsiasi canale o piattaforma digitale. Qualsiasi formato data è accettabile, ma l’Adobe consiglia: AAAA-MM-GG. |
| [!UICONTROL Valore della valutazione] | `rating` | Stringa | La classificazione definita dalle linee guida TV per genitori. |
| [!UICONTROL  Nome creatore] | `originator` | Stringa | Nome del creatore del contenuto. |
| [!UICONTROL Rete di trasmissione] | `network` | Stringa | Nome della rete o del canale. |
| [!UICONTROL Tipo di spettacolo] | `showType` | Stringa | Il tipo di contenuto, ad esempio trailer o episodio completo. |
| [!UICONTROL Tipo di caricamento dell’annuncio] | `adLoad` | Stringa | Il tipo di annuncio caricato come definito dalla rappresentazione interna di ciascun cliente. |
| [!UICONTROL Identificatore MVPD] | `mvpd` | Stringa | Il [!UICONTROL Identificatore MVPD] fornito tramite l’autenticazione Adobe. |
| [!UICONTROL Contenuti multimediali autorizzati] | `authorized` | Stringa | Conferma se l’utente è stato autorizzato tramite l’autenticazione Adobe. |
| [!UICONTROL Fascia oraria] | `dayPart` | Stringa | Proprietà che definisce l’ora del giorno in cui il contenuto è stato trasmesso o riprodotto. Questo potrebbe avere qualsiasi valore impostato dai clienti secondo necessità |
| [!UICONTROL Tipo di feed] | `feed` | Stringa | Il tipo di feed, che può rappresentare dati effettivi relativi al feed come EAST HD o SD, o la sorgente del feed come un URL. |
| [!UICONTROL Formato flusso] | `streamFormat` | Stringa | Il formato del flusso (HD, SD). |
| [!UICONTROL Riprendi] | `hasResume` | Booleano | Contrassegna ogni riproduzione ripresa dopo più di 30 minuti di buffer, pausa o interruzione. |
| [!UICONTROL Tipo di flusso] | `streamType` | Stringa | Tipo di flusso multimediale. |
| [!UICONTROL Artista] | `artist` | Stringa | Nome dell&#39;artista o del gruppo dell&#39;album che esegue la registrazione musicale o il video. |
| [!UICONTROL Album] | `album` | Stringa | Il nome dell&#39;album a cui appartiene la registrazione musicale o il video. |
| [!UICONTROL Etichetta record] | `label` | Stringa | Nome dell&#39;etichetta discografica. |
| [!UICONTROL Autore] | `author` | Stringa | Nome dell’autore del contenuto multimediale. |
| [!UICONTROL Stazione radio] | `station` | Stringa | Il nome della stazione radio su cui viene riprodotto l’audio. |
| [!UICONTROL Editore] | `publisher` | Stringa | Nome dell&#39;autore del contenuto audio. |
| [!UICONTROL Segmento video] | `segment` | Stringa | L’intervallo che descrive la parte del contenuto visualizzata in minuti. |
| [!UICONTROL Flag di contenuto multimediale scaricato] | `isDownloaded` | Booleano | Il flusso è stato riprodotto localmente sul dispositivo dopo il download. |
| [!UICONTROL Dati federati] | `isFederated` | Booleano | [!UICONTROL Dati federati] è impostato su true quando l’hit viene federato (ovvero, ricevuto dal cliente come parte di una condivisione di dati federata, anziché come implementazione propria). |
| [!UICONTROL Avvio file multimediale] | `isViewed` | Booleano | Evento di caricamento del file multimediale. Ciò si verifica quando il visualizzatore seleziona il pulsante di riproduzione. Questo conta anche se ci sono annunci pre-roll, buffering, errori e così via. |
| [!UICONTROL Inizio contenuti] | `isPlayed` | Booleano | [!UICONTROL Inizio contenuti] diventa true quando viene utilizzato il primo fotogramma del file multimediale. Se l’utente abbandona durante un annuncio, il buffering e così via, allora non ci sarebbe [!UICONTROL Inizio contenuti] evento. |
| [!UICONTROL Completamenti contenuto] | `isCompleted` | Booleano | [!UICONTROL Completamenti contenuto] indica se una risorsa multimediale a tempo è stata guardata fino al completamento. Questo evento non significa necessariamente che lo spettatore abbia guardato l&#39;intero video; potrebbe aver saltato delle parti per andare avanti. |
| [!UICONTROL Tempo trascorso dei contenuti] | `timePlayed` | Intero | [!UICONTROL Tempo trascorso dei contenuti] somma la durata dell’evento (in secondi) per tutti gli eventi di tipo PLAY sul contenuto principale. |
| [!UICONTROL Tempo trascorso contenuti multimediali] | `totalTimePlayed` | Intero | Descrive la quantità totale di tempo trascorso da un utente su una specifica risorsa multimediale a tempo, incluso il tempo trascorso a guardare gli annunci. |
| [!UICONTROL Tempo specifico di riproduzione] | `uniqueTimePlayed` | Intero | Descrive la somma degli intervalli univoci visualizzati da un utente su una risorsa multimediale a tempo, ovvero la lunghezza degli intervalli di riproduzione visualizzati più volte viene conteggiata una sola volta. |
| [!UICONTROL Pubblico medio per minuto] | `averageMinuteAudience` | Numero | Descrive il tempo medio di contenuto trascorso per un elemento multimediale specifico, ovvero il tempo totale di contenuto trascorso diviso per la durata di tutte le sessioni di riproduzione. |
| [!UICONTROL Conteggio annunci] | `adCount` | Intero | Il numero di annunci avviati durante la riproduzione. |
| [!UICONTROL Conteggio capitoli] | `chapterCount` | Intero | Il numero di capitoli avviati durante la riproduzione. |
| [!UICONTROL Indicatore di avanzamento al 10%] | `hasProgress10` | Booleano | Indica che l’indicatore di riproduzione ha superato l’indicatore del 10% del contenuto multimediale in base alla lunghezza del flusso. L’indicatore viene conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| [!UICONTROL Indicatore di avanzamento al 25%] | `hasProgress25` | Booleano | Indica che l’indicatore di riproduzione ha superato l’indicatore del 25% del contenuto multimediale in base alla lunghezza del flusso. L’indicatore è conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| [!UICONTROL Indicatore di avanzamento al 50%] | `hasProgress50` | Booleano | Indica che l’indicatore di riproduzione ha superato l’indicatore del 50% del contenuto multimediale in base alla lunghezza del flusso. L’indicatore è conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| [!UICONTROL Indicatore di avanzamento al 75%] | `hasProgress75` | Booleano | Indica che l’indicatore di riproduzione ha superato l’indicatore del 75% del contenuto multimediale in base alla lunghezza del flusso. L’indicatore è conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| [!UICONTROL Indicatore di avanzamento al 95%] | `hasProgress95` | Booleano | Indica che l’indicatore di riproduzione ha superato l’indicatore del 95% del contenuto multimediale in base alla lunghezza del flusso. L’indicatore è conteggiato una sola volta, anche se si torna indietro. Se il contenuto viene mandato avanti, gli indicatori saltati non vengono conteggiati. |
| [!UICONTROL Flussi stimati] | `estimatedStreams` | Numero | Il numero stimato di flussi video o audio per ogni singolo contenuto. |
| [!UICONTROL Flussi interessati dalla pausa] | `hasPauseImpactedStreams` | Booleano | Indica se si sono verificate una o più pause durante la riproduzione di un singolo elemento multimediale. |
| [!UICONTROL Eventi di pausa] | `pauseCount` | Intero | [!UICONTROL Eventi di pausa] conta il numero di periodi di pausa che si sono verificati durante la riproduzione. |
| [!UICONTROL Durata totale pausa] | `pauseTime` | Intero | [!UICONTROL Durata totale pausa] descrive la durata in secondi in cui la riproduzione è stata messa in pausa dall’utente. |
| [!UICONTROL Visualizzazioni segmento multimediale] | `hasSegmentView` | Booleano | [!UICONTROL Visualizzazioni segmento multimediale] indica quando è stato visualizzato almeno un fotogramma, non necessariamente il primo. |
| [!UICONTROL Timeout del server della sessione multimediale] | `secondsSinceLastCall` | Numero | Il [!UICONTROL Timeout del server della sessione multimediale] indica il tempo, in secondi, trascorso tra l’ultima interazione nota dell’utente e il momento in cui la sessione è stata chiusa. |
| [!UICONTROL Rete di distribuzione dei contenuti] | `cdn` | Stringa | Il [!UICONTROL Rete di distribuzione dei contenuti] del contenuto riprodotto. |
| [!UICONTROL Pev3] | `pev3` | Stringa | [!UICONTROL Pev3] è il tipo di flusso multimediale utilizzato per il reporting. |
| [!UICONTROL Pccr] | `pccr` | Booleano | [!UICONTROL Pccr] indica che si è verificato un reindirizzamento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json)
