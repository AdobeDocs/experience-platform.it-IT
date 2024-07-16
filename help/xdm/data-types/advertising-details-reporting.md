---
title: Tipo di dati per generazione rapporti dettagli Advertising
description: Scopri il tipo di dati Advertising Details Reporting Experience Data Model (XDM).
exl-id: fbca5b2a-a9bd-4f76-a494-d682cb2cbfbc
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 12%

---

# [!UICONTROL Dettagli Advertising] Tipo di dati di reporting

[!UICONTROL Dettagli di Advertising] Il reporting è un tipo di dati Experience Data Model (XDM) standard che acquisisce gli attributi chiave relativi agli annunci pubblicitari. Include informazioni quali ID dell’annuncio, ID dell’inserzionista e della campagna, lunghezza, posizione all’interno di una sequenza, dettagli sul rendering dell’annuncio da parte del lettore e così via. Puoi utilizzare questo tipo di dati per monitorare e analizzare vari aspetti delle prestazioni e del coinvolgimento degli annunci, e fornire informazioni su come i tipi di pubblico interagiscono con e rispondono a diversi annunci pubblicitari.

+++Selezionare questa opzione per visualizzare un diagramma del tipo di dati di Advertising Details Reporting.
![Diagramma del tipo di dati di Advertising Details Reporting.](../images/data-types/advertising-details-information.png)
+++

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|----------------------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Nome annuncio] | `friendlyName` | stringa | Nome leggibile dell’annuncio. Nella generazione rapporti, &quot;Nome annuncio&quot; è la classificazione e &quot;Nome annuncio (variabile)&quot; è l’eVar. |
| [!UICONTROL ID annuncio] | `name` | stringa | ID dell’annuncio. Qualsiasi combinazione di numeri interi e/o lettere. |
| [!UICONTROL Lunghezza O Durata Dell&#39;Annuncio] | `length` | intero | La lunghezza dell’annuncio video in secondi. |
| [!UICONTROL Annuncio In Posizione Pod (Avvio Annuncio)] | `podPosition` | intero | L’indice dell’annuncio all’interno dell’inizio dell’annuncio principale, ad esempio, il primo annuncio ha indice 0 e il secondo annuncio ha indice 1. |
| [!UICONTROL Nome Lettore Annuncio] | `playerName` | stringa | Il nome del lettore responsabile del rendering dell’annuncio. |
| [!UICONTROL Inserzionista] | `advertiser` | stringa | Azienda o marchio il cui prodotto è presentato nell’annuncio. |
| [!UICONTROL Campagna pubblicitaria] | `campaignID` | stringa | ID della campagna pubblicitaria. |
| [!UICONTROL ID creatività annuncio] | `creativeID` | stringa | L’ID della creatività dell’annuncio. |
| [!UICONTROL ID sito annuncio] | `siteID` | stringa | ID del sito dell’annuncio. |
| [!UICONTROL URL creativo annuncio] | `creativeURL` | stringa | L’URL della creatività dell’annuncio. |
| [!UICONTROL ID posizionamento annuncio] | `placementID` | stringa | ID di posizionamento dell’annuncio. |
| [!UICONTROL Annuncio completato] | `isCompleted` | booleano | Tiene traccia del completamento dell’annuncio. |
| [!UICONTROL Annuncio avviato] | `isStarted` | booleano | Tiene traccia dell’avvio dell’annuncio. |
| [!UICONTROL Tempo di riproduzione annuncio] | `timePlayed` | intero | La quantità totale di tempo, in secondi, trascorsa a guardare l’annuncio (ovvero, il numero di secondi riprodotti). |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
