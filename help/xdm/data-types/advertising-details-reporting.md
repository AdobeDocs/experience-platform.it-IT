---
title: Tipo di dati di reporting di Advertising Details
description: Scopri il tipo di dati Advertising Details Reporting Experience Data Model (XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 11%

---

# [!UICONTROL Dettagli pubblicitari] Tipo di dati di reporting

[!UICONTROL Dettagli pubblicitari] Il reporting è un tipo di dati Experience Data Model (XDM) standard che acquisisce gli attributi chiave relativi agli annunci pubblicitari. Include informazioni quali ID dell’annuncio, ID dell’inserzionista e della campagna, lunghezza, posizione all’interno di una sequenza, dettagli sul rendering dell’annuncio da parte del lettore e così via. Puoi utilizzare questo tipo di dati per monitorare e analizzare vari aspetti delle prestazioni e del coinvolgimento degli annunci, e fornire informazioni su come i tipi di pubblico interagiscono con e rispondono a diversi annunci pubblicitari.

+++Selezionare questa opzione per visualizzare un diagramma del tipo di dati Segnalazione dettagli pubblicità.
![Diagramma del tipo di dati Reporting di Advertising Details.](../images/data-types/advertising-details-information.png)
+++

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Nome annuncio] | `friendlyName` | string | Nome leggibile dell’annuncio. Nella generazione rapporti, “Nome annuncio” è la classificazione e “Nome annuncio (variabile)” è l’eVar. |
| [!UICONTROL ID annuncio] | `name` | string | ID dell’annuncio. Qualsiasi combinazione di numeri interi e/o lettere. |
| [!UICONTROL Lunghezza O Durata Dell’Annuncio] | `length` | numero intero | La lunghezza dell’annuncio video in secondi. |
| [!UICONTROL Posizione annuncio nel pod (avvio annuncio)] | `podPosition` | numero intero | L’indice dell’annuncio all’interno dell’inizio dell’annuncio principale, ad esempio, il primo annuncio ha indice 0 e il secondo annuncio ha indice 1. |
| [!UICONTROL Nome del lettore dell’annuncio] | `playerName` | string | Nome del lettore responsabile del rendering dell’annuncio. |
| [!UICONTROL Inserzionista] | `advertiser` | string | Azienda o marchio il cui prodotto è presentato nell’annuncio. |
| [!UICONTROL Campagna pubblicitaria] | `campaignID` | string | ID della campagna pubblicitaria. |
| [!UICONTROL ID creatività annuncio] | `creativeID` | string | ID della creatività dell’annuncio. |
| [!UICONTROL ID sito annuncio] | `siteID` | string | ID del sito dell’annuncio. |
| [!UICONTROL URL creatività annuncio] | `creativeURL` | string | URL della creatività dell’annuncio. |
| [!UICONTROL ID posizionamento annuncio] | `placementID` | string | ID di posizionamento dell’annuncio. |
| [!UICONTROL Annuncio completato] | `isCompleted` | booleano | Tiene traccia del completamento dell’annuncio. |
| [!UICONTROL Annuncio avviato] | `isStarted` | booleano | Tiene traccia dell’avvio dell’annuncio. |
| [!UICONTROL Tempo di riproduzione dell’annuncio] | `timePlayed` | numero intero | La quantità totale di tempo, in secondi, trascorsa a guardare l’annuncio (ovvero, il numero di secondi riprodotti). |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
