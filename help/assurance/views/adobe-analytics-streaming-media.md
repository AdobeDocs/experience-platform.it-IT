---
title: Visualizzare Adobe Analytics per contenuti in streaming in Assurance
description: Questa guida spiega come utilizzare Adobe Analytics per contenuti in streaming con Adobe Experience Platform Assurance.
exl-id: 9a9c2c64-e9ed-4d58-b936-d802f1c3b7d3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '412'
ht-degree: 100%

---

# Visualizzare Adobe Analytics per contenuti in streaming in Assurance

Con l’integrazione di Adobe Analytics per contenuti in streaming e Adobe Experience Platform Assurance, ora puoi convalidare l’implementazione di Media Analytics nella tua app mobile. Le viste di Media Analytics mostrano ciò che viene tracciato nella sessione multimediale, ad esempio:

- L’evento di inizio della sessione che contiene tutte le proprietà principali del contenuto, dei metadati standard e dei metadati personalizzati, nonché gli eventi di fine e di completamento della sessione.
- Eventi di inizio interruzione pubblicitaria e inizio annuncio, completi di tutte le proprietà, nonché eventi Ignora e Completato per entrambi.
- Inizio capitolo con tutte le proprietà associate, nonché gli eventi Salta capitolo e Completa capitolo.
- Tutti gli eventi di modifica della riproduzione (riproduzione, pausa, buffer, errori, modifica del bitrate).
- Tutti gli eventi di tracciamento delle modifiche dello stato del lettore (inizio, fine).

Una volta che i dati sono elaborati in Analytics, nella vista dei dettagli dell’evento sono disponibili anche i dati e lo stato relativi alla fase di post-elaborazione, ad esempio il tempo impiegato dal contenuto multimediale e la durata totale della pausa.

## Introduzione

Prima di continuare, assicurati di disporre dei seguenti servizi:

- L’[Interfaccia utente della Raccolta dati di Adobe Experience Platform](https://experience.adobe.com/it#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/it/assurance)

Per informazioni su come installare Assurance nell’applicazione, consulta la [guida all’implementazione di Assurance](../tutorials/implement-assurance.md).

## Utilizzare Assurance con Adobe Analytics per contenuti in streaming

Dopo aver effettuato la connessione e configurato l’app per Adobe Analytics, puoi configurarla per l’analisi dei contenuti multimediali in streaming. Nella parte inferiore del pannello a sinistra, seleziona **[!UICONTROL Configura]** per aggiungere la vista Eventi di Media Analytics e **Salva**.

![Configura](./images/adobe-analytics-streaming-media/configure.png)

Una volta aggiunto, seleziona la vista **[!UICONTROL Eventi di Media Analytics]** nella sezione **[!UICONTROL Adobe Analytics]** per convalidare il tracciamento della sessione.

![Seleziona](./images/adobe-analytics-streaming-media/select.png)

Nella vista **[!UICONTROL Eventi di Media Analytics]**, è possibile cercare e filtrare per ID sessione (VSID) per visualizzare una sessione multimediale specifica. Per visualizzare ulteriori dettagli sull’evento, seleziona un evento specifico.

![Eventi multimediali](./images/adobe-analytics-streaming-media/media-events.png)

Per una visualizzazione più sintetica delle chiamate API, puoi anche nascondere gli eventi di aggiornamento della testina di riproduzione selezionando il filtro **[!UICONTROL Nascondi eventi di aggiornamento della testina di riproduzione]**.

![Nascondi testina di riproduzione](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>La visualizzazione dei dati di analisi dei contenuti multimediali in fase di post-elaborazione richiede l’utilizzo delle versioni SDK Android Media 2.1.2 e iOS AEPMedia 3.0.1 (o versioni successive)

Per visualizzare i dati in fase di post-elaborazione, individua l’evento di inizio sessione e verifica nella colonna dello stato che la sessione sia stata completata. Se è stata completata, fai clic sull’evento per visualizzare il riepilogo di una sessione multimediale nella vista dei dettagli dell’evento. Per ulteriori dettagli, scorri verso il basso per trovare i dettagli della post-elaborazione.

![Vista Post-elaborazione](./images/adobe-analytics-streaming-media/post-processed-view.png)
