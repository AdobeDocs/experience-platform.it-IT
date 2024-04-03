---
title: Tipo di dati della raccolta dei dettagli sulla pubblicità
description: Scopri il tipo di dati Experience Data Model (XDM) della raccolta dei dettagli di Advertising.
source-git-commit: fe239bee3c853d43c04200092f59537dfeb00c87
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 11%

---

# [!UICONTROL Dettagli pubblicitari] Tipo di dati della raccolta

[!UICONTROL Dettagli pubblicitari] La raccolta è un tipo di dati Experience Data Model (XDM) standard che acquisisce gli attributi chiave relativi agli annunci pubblicitari. Include informazioni quali ID dell’annuncio, ID dell’inserzionista e della campagna, lunghezza, posizione all’interno di una sequenza, dettagli sul rendering dell’annuncio da parte del lettore e così via. Puoi utilizzare questo tipo di dati per monitorare e analizzare vari aspetti delle prestazioni e del coinvolgimento degli annunci, e fornire informazioni su come i tipi di pubblico interagiscono con e rispondono a diversi annunci pubblicitari. Queste informazioni vengono utilizzate per tenere traccia dei dati di streaming.

+++Selezionare questa opzione per visualizzare un diagramma del tipo di dati Raccolta dettagli annunci.
![Diagramma del tipo di dati Raccolta dettagli pubblicitari.](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>Ogni nome visualizzato contiene un collegamento per ulteriori informazioni sui parametri audio e video. Le pagine collegate contengono dettagli sui dati degli annunci video raccolti da Adobe, i valori di implementazione, i parametri di rete, il reporting e considerazioni importanti.

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL Inserzionista]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | string | No | Azienda o marchio il cui prodotto è presentato nell’annuncio. |
| [[!UICONTROL Campagna pubblicitaria]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | string | No | ID della campagna pubblicitaria. |
| [[!UICONTROL ID creatività annuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | string | No | ID della creatività dell’annuncio. |
| [[!UICONTROL URL creatività annuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | string | No | URL della creatività dell’annuncio. |
| [[!UICONTROL Posizione annuncio nel pod (avvio annuncio)]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | numero intero | Sì | L’indice dell’annuncio all’interno dell’inizio dell’annuncio principale, ad esempio, il primo annuncio ha indice 0 e il secondo annuncio ha indice 1. |
| [[!UICONTROL Lunghezza O Durata Dell’Annuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | numero intero | Sì | La lunghezza dell’annuncio video in secondi. |
| [[!UICONTROL Nome annuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | string | Sì | Nome leggibile dell’annuncio. Nella generazione rapporti, “Nome annuncio” è la classificazione e “Nome annuncio (variabile)” è l’eVar. |
| [[!UICONTROL ID posizionamento annuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | string | No | ID di posizionamento dell’annuncio. |
| [[!UICONTROL Nome del lettore dell’annuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | string | Sì | Nome del lettore responsabile del rendering dell’annuncio. |
| [[!UICONTROL ID sito annuncio]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | string | No | ID del sito dell’annuncio. |
