---
title: Tipo di dati raccolta dettagli sessione
description: Scopri il tipo di dati Experience Data Model (XDM) della raccolta dei dettagli della sessione.
exl-id: ffe6bcf7-61e1-4f7a-ba95-7fcb78683cc9
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 9%

---

# Tipo di dati della raccolta [!UICONTROL Session Details]

La raccolta [!UICONTROL Session Details] è un tipo di dati Experience Data Model (XDM) standard che tiene traccia dei dati relativi alle sessioni di riproduzione multimediale. I campi di raccolta multimediale vengono utilizzati per acquisire i dati inviati ad altri servizi Adobe per l’ulteriore elaborazione. Questo schema include un’ampia gamma di proprietà che possono essere utilizzate per fornire informazioni sul comportamento degli utenti e sui modelli di consumo dei contenuti. Utilizzare il tipo di dati della raccolta [!UICONTROL Session Details] per acquisire il coinvolgimento dell&#39;utente registrando eventi di riproduzione, interazioni pubblicitarie, indicatori di avanzamento, pause e altre metriche.

+++Selezionare questa opzione per visualizzare un diagramma del tipo di dati Raccolta dettagli sessione.
![Diagramma del tipo di dati Raccolta dettagli sessione.](../images/data-types/session-details-collection.png)
+++

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|-----------|----------|---------------------------------------------------------------------------------------|
| [!UICONTROL Ad Load Type] | `adLoad` | Stringa | No | Il tipo di annuncio caricato come definito dalla rappresentazione interna di ciascun cliente. |
| [[!UICONTROL Album]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#album) | `album` | Stringa | No | Il nome dell&#39;album a cui appartiene la registrazione musicale o il video. |
| [[!UICONTROL Artist]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#artist) | `artist` | Stringa | No | Nome dell&#39;artista o del gruppo dell&#39;album che esegue la registrazione musicale o il video. |
| [[!UICONTROL Asset ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#asset-id) | `assetID` | Stringa | No | [!UICONTROL Asset ID] è l&#39;identificatore univoco del contenuto della risorsa multimediale, ad esempio l&#39;identificatore di un episodio di una serie TV, di una risorsa di un film o di un evento in diretta. In genere questi ID derivano da autorità metadati come EIDR, TMS/Gracenote o Rovi. Questi identificatori possono provenire anche da altri sistemi proprietari o interni. |
| [[!UICONTROL Author]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#author) | `author` | Stringa | No | Nome dell’autore del contenuto multimediale. |
| [[!UICONTROL Broadcast Content Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-type) | `contentType` | Stringa | Sì | [!UICONTROL Broadcast Content Type] della consegna del flusso. I valori disponibili per [!UICONTROL Stream Type] includono:<br>Audio: &quot;canzone&quot;, &quot;podcast&quot;, &quot;audiobook&quot; e &quot;radio&quot;;<br>Video: &quot;VoD&quot;, &quot;Live&quot;, &quot;Linear&quot;, &quot;UGC&quot; e &quot;DVoD&quot;.<br>I clienti possono fornire valori personalizzati per questo parametro. |
| [[!UICONTROL Broadcast Network]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#network) | `network` | Stringa | No | Nome della rete o del canale. |
| [[!UICONTROL Content Channel]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-channel) | `channel` | Stringa | Sì | [!UICONTROL Content Channel] è il canale di distribuzione da cui è stato riprodotto il contenuto. |
| [!UICONTROL Content Delivery Network] | `cdn` | Stringa | No | [!UICONTROL Content Delivery Network] del contenuto riprodotto. |
| [[!UICONTROL Content ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-id) | `name` | stringa | Sì | [!UICONTROL Content ID] è un identificatore univoco del contenuto. Può essere utilizzato per effettuare il collegamento ad altri ID di settore o CMS. |
| [[!UICONTROL Content Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-name-(variable)) | `friendlyName` | Stringa | No | [!UICONTROL Content Name] è il nome &quot;descrittivo&quot; (leggibile dall&#39;utente) del contenuto. |
| [[!UICONTROL Content Player Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-player-name) | `playerName` | Stringa | Sì | Nome del lettore di contenuti. |
| [[!UICONTROL Creator Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#originator) | `originator` | Stringa | No | Nome del creatore del contenuto. |
| [[!UICONTROL Day Part]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#day-part) | `dayPart` | Stringa | No | Proprietà che definisce l’ora del giorno in cui il contenuto è stato trasmesso o riprodotto. Questo potrebbe avere qualsiasi valore impostato dai clienti secondo necessità |
| [[!UICONTROL Episode Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#episode) | `episode` | Stringa | No | Numero dell’episodio. |
| [[!UICONTROL Feed Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#media-feed-type) | `feed` | Stringa | No | Il tipo di feed, che può rappresentare dati effettivi relativi al feed come EAST HD o SD, o la sorgente del feed come un URL. |
| [[!UICONTROL First Air Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-air-date) | `firstAirDate` | Stringa | No | La data in cui il contenuto è andato in onda per la prima volta in televisione. Qualsiasi formato di data è accettabile, ma Adobe consiglia: AAAA-MM-GG. |
| [[!UICONTROL First Digital Date]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#first-digital-date) | `firstDigitalDate` | Stringa | No | La data in cui il contenuto è andato in onda per la prima volta su qualsiasi canale o piattaforma digitale. Qualsiasi formato di data è accettabile, ma Adobe consiglia: AAAA-MM-GG. |
| [[!UICONTROL Genre]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#genre) | `genre` | Stringa | No | Tipo o raggruppamento di contenuti definiti dal produttore del contenuto. I valori devono essere delimitati da virgole nell’implementazione delle variabili. |
| [[!UICONTROL Media Authorized]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#authorized) | `authorized` | Stringa | No | Conferma se l’utente è stato autorizzato tramite Adobe Authentication. |
| [[!UICONTROL Media Content Length]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-length-(variable)) | `length` | Intero | Sì | [!UICONTROL Media Content Length] contiene la lunghezza/runtime della clip, ovvero la lunghezza massima (o durata) del contenuto utilizzato, in secondi. |
| [[!UICONTROL MVPD Identifier]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#mvpd) | `mvpd` | Stringa | No | L’identificatore Multi-channel Video Programming Distributor (MVPD) fornito tramite l’autenticazione di Adobe. |
| [[!UICONTROL Publisher]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#publisher) | `publisher` | Stringa | No | Nome dell&#39;autore del contenuto audio. |
| [[!UICONTROL Radio Station]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#station) | `station` | Stringa | No | Il nome della stazione radio su cui viene riprodotto l’audio. |
| [[!UICONTROL Rating Value]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-rating) | `rating` | Stringa | No | La classificazione definita dalle linee guida TV per genitori. |
| [[!UICONTROL Record Label]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#label) | `label` | Stringa | No | Nome dell&#39;etichetta discografica. |
| [[!UICONTROL Resume]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#content-resumes) | `hasResume` | Booleano | No | Contrassegna ogni riproduzione ripresa dopo più di 30 minuti di buffer, pausa o interruzione. |
| [[!UICONTROL Season Number]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#season) | `season` | Stringa | No | [!UICONTROL Season Number] a cui appartiene il programma. La stagione della serie è necessaria solo se lo spettacolo fa parte di una serie. |
| [[!UICONTROL Series Name]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show) | `show` | Stringa | No | Il Nome Del Programma/Serie. Il nome del programma è necessario solo se lo spettacolo fa parte di una serie. |
| [[!UICONTROL Show Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#show-type) | `showType` | Stringa | No | Il tipo di contenuto. Ad esempio, un trailer o un episodio completo. Il tipo di contenuto è espresso come numero intero compreso tra 0 e 3. Ad esempio, &quot;0&quot; = episodio completo; &quot;1&quot; = anteprima/trailer; &quot;2&quot; = clip; &quot;3&quot; = altro. |
| [[!UICONTROL Stream Format]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-format) | `streamFormat` | Stringa | No | Il formato del flusso (HD, SD). |
| [[!UICONTROL Stream Type]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#stream-type) | `streamType` | Stringa | No | Tipo di flusso multimediale. |
| [[!UICONTROL Version]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/audio-video-parameters.html#sdk-version) | `appVersion` | Stringa | No | Versione SDK utilizzata dal lettore. Questo potrebbe avere qualsiasi valore personalizzato che abbia senso per il lettore. |

{style="table-layout:auto"}
