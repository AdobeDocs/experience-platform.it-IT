---
title: Destinazione Marketo Engage
description: Marketi Engage è l’unica soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il marketing, la pubblicità, l’analisi e il commercio. Ti consente di automatizzare e gestire le attività dalla gestione dei lead CRM e il coinvolgimento dei clienti fino all’attribuzione di marketing e ricavi basata sull’account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 3%

---

# destinazione Marketo Engage {#beta-marketo-engage-destination}

## Panoramica {#overview}

Marketi Engage è l’unica soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il marketing, la pubblicità, l’analisi e il commercio. Ti consente di automatizzare e gestire le attività dalla gestione dei lead CRM e il coinvolgimento dei clienti fino all’attribuzione di marketing e ricavi basata sull’account.

La destinazione consente agli esperti di marketing di inviare in push i segmenti creati in Adobe Experience Platform a Marketo dove verranno visualizzati come elenchi statici.

## Identità supportate {#supported-identities}

| Identità di destinazione | Descrizione |
|---|---|
| ECID | Spazio dei nomi che rappresenta ECID. Questo namespace può essere indicato anche dai seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| E-mail | Spazio dei nomi che rappresenta un indirizzo e-mail. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>In [fase di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di destinazione di attivazione, è *obbligatorio* mappare le identità e *facoltativo* per mappare gli attributi. La mappatura di E-mail e/o ECID dalla scheda Namespace Identity è la cosa più importante da fare per garantire che la persona corrisponda in Marketo. La mappatura di e-mail garantisce la percentuale di corrispondenza più elevata.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (e-mail, ECID) utilizzati nella destinazione del Marketo Engage. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Impostare la destinazione e attivare i segmenti {#set-up}

>[!IMPORTANT]
> 
>* Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions).
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.


Per istruzioni dettagliate su come impostare la destinazione e attivare i segmenti, leggi [Inviare un segmento Adobe Experience Platform a un elenco statico di Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) nella documentazione di Marketo.

Il video seguente illustra anche i passaggi per configurare una destinazione Marketo e attivare i segmenti.

>[!NOTE]
>
>L&#39;interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione di questo video. Per le informazioni più aggiornate, consulta la guida riportata sopra.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
