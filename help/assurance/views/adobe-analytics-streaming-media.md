---
title: Visualizzazione Adobe Analytics per contenuti in streaming in Assurance
description: Questa guida spiega come utilizzare Adobe Analytics per contenuti in streaming con Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 1%

---


# Vista Adobe Analytics per contenuti in streaming in Assurance

Con l’integrazione tra Adobe Analytics per contenuti in streaming e Adobe Experience Platform Assurance, ora puoi convalidare l’implementazione Media Analytics nella tua app mobile. Le visualizzazioni di Media Analytics mostrano cosa viene tracciato nella sessione multimediale, ad esempio:

- Evento di avvio della sessione contenente tutte le proprietà di base del contenuto, i metadati standard e i metadati personalizzati, nonché gli eventi di fine sessione e completamento della sessione.
- Eventi Inizio interruzione annuncio e Inizio annuncio con tutte le proprietà annuncio associate, nonché eventi Salta e Completa per entrambi.
- Capitolo Inizio con tutte le proprietà allegate, nonché gli eventi Capitolo Salta e Capitolo Completa.
- Tutti gli eventi di modifica della riproduzione (riproduzione, pausa, buffer, errori, modifica del bitrate).
- Tutti gli eventi di tracciamento delle modifiche dello stato del lettore (inizio, fine).

Una volta elaborati i dati in Analytics, nella visualizzazione dei dettagli dell’evento sono disponibili anche lo stato e i dati post-elaborazione, ad esempio il tempo trascorso per i file multimediali e la durata totale della pausa.

## Introduzione

Prima di continuare, assicurati di disporre dei seguenti servizi:

- La [Interfaccia utente di raccolta dati di Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

Per informazioni su come installare Assurance nella tua applicazione, leggi la [guida all’implementazione di Assurance](../tutorials/implement-assurance.md).

## Utilizzare la garanzia con Adobe Analytics per contenuti in streaming

Dopo aver connesso e configurato l’app per Adobe Analytics, puoi configurarla per Streaming Media Analytics. Nella parte inferiore del pannello di sinistra, seleziona **[!UICONTROL Configura]** per aggiungere la visualizzazione Eventi di Media Analytics e **Salva** .

![Configurare gli](./images/adobe-analytics-streaming-media/configure.png)

Una volta aggiunto, seleziona la **[!UICONTROL Eventi Media Analytics]** visualizza in **[!UICONTROL Adobe Analytics]** per convalidare il tracciamento della sessione.

![Seleziona](./images/adobe-analytics-streaming-media/select.png)

In **[!UICONTROL Eventi Media Analytics]** puoi cercare e filtrare per ID sessione (VSID) per visualizzare una sessione multimediale specifica. Per visualizzare ulteriori dettagli sull’evento, seleziona un evento specifico.

![Eventi multimediali](./images/adobe-analytics-streaming-media/media-events.png)

Per una visualizzazione più succinta delle chiamate API, puoi anche nascondere gli eventi di aggiornamento del playhead selezionando la **[!UICONTROL Nascondi eventi di aggiornamento della sequenza di riproduzione]** filtro.

![Nascondi sequenza di riproduzione](./images/adobe-analytics-streaming-media/hide-playhead.png)

>[!INFO]
>
>La visualizzazione dei dati di analisi dei contenuti multimediali post-elaborati richiede l&#39;utilizzo di versioni SDK: Android Media 2.1.2 e iOS AEPMMedia 3.0.1 (o versioni successive)

Per visualizzare i dati post-elaborati, individua l’evento di inizio sessione e convalida nella colonna dello stato del completamento della sessione. Se completato, fai clic sull’evento per visualizzare un riepilogo della sessione multimediale nella visualizzazione dei dettagli dell’evento. Per ulteriori dettagli, scorri verso il basso per trovare i dettagli post-elaborati.

![Visualizzazione post-elaborazione](./images/adobe-analytics-streaming-media/post-processed-view.png)
