---
title: Destinazione Marketo Engage
description: Marketi Engage è l'unica soluzione end-to-end di gestione della customer experience (CXM) per il marketing, la pubblicità, l'analisi e il commerce. Consente di automatizzare e gestire le attività, dalla gestione dei lead CRM al coinvolgimento dei clienti, fino all’attribuzione dei ricavi e al marketing basato sull’account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 0507fd3596246bc2ead5c212c228822bf25f94e5
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 1%

---

# Marketo Engage di destinazione {#beta-marketo-engage-destination}

## Registro modifiche destinazione {#changelog}

>[!IMPORTANT]
>
>Con il rilascio del [connettore di destinazione Marketo V2 avanzato](/help/release-notes/2022/july-2022.md#destinations), nel catalogo delle destinazioni sono ora presenti due schede Marketo.
>* Se stai già attivando i dati in **[!UICONTROL Marketo V1]** destinazione: crea nuovi flussi di dati per **[!UICONTROL Marketo V2]** destinazione ed eliminare i flussi di dati esistenti nella **[!UICONTROL Marketo V1]** destinazione entro febbraio 2023. A partire da tale data, la **[!UICONTROL Marketo V1]** la scheda di destinazione verrà rimossa.
>* Se non hai ancora creato flussi di dati per **[!UICONTROL Marketo V1]** destinazione, utilizza il nuovo **[!UICONTROL Marketo V2]** per la connessione e l&#39;esportazione di dati in Marketo.

![Immagine delle due schede di destinazione Marketo affiancata.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

I miglioramenti nella destinazione di Marketo V2 includono:

* In **[!UICONTROL Pianifica segmento]** passaggio del flusso di lavoro di attivazione, in Marketo V1, era necessario aggiungere manualmente un **ID mappatura** per esportare correttamente i dati in Marketo. Questo passaggio manuale non è più richiesto in Marketo V2.
* In **[!UICONTROL Mappatura]** passaggio del flusso di lavoro di attivazione, in Marketo V1, è stato possibile mappare i campi XDM solo su tre campi di destinazione in Marketo: `firstName`, `lastName`, e `companyName`. Con la versione di Marketo V2, ora è possibile mappare i campi XDM su molti più campi in Marketo. Per ulteriori informazioni, leggere [attributi supportati](#supported-attributes) più avanti.

## Panoramica {#overview}

[!DNL Marketo Engage] è l&#39;unica soluzione CXM (Customer Experience Management) end-to-end per il marketing, la pubblicità, le analisi e il commerce. Consente di automatizzare e gestire le attività, dalla gestione dei lead CRM al coinvolgimento dei clienti, fino all’attribuzione dei ricavi e al marketing basato sull’account.

La destinazione consente agli addetti al marketing di inviare i tipi di pubblico creati in Adobe Experience Platform a Marketo, dove verranno visualizzati come elenchi statici.

## Identità e attributi supportati {#supported-identities-attributes}

>[!NOTE]
>
>In [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro attiva destinazione, è *obbligatorio* mappare le identità e *facoltativo* per mappare gli attributi. La mappatura di e-mail e/o ECID dalla scheda Identity Namespace (Spazio dei nomi delle identità) è la cosa più importante da fare per garantire che la persona corrisponda in Marketo. La mappatura dell’e-mail assicura la percentuale di corrispondenza più elevata.

### Identità supportate {#supported-identities}

| Identità di destinazione | Descrizione |
|---|---|
| ECID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| E-mail | Uno spazio dei nomi che rappresenta un indirizzo e-mail. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |

{style="table-layout:auto"}

### Attributi supportati {#supported-attributes}

È possibile mappare gli attributi da Experienci Platform a qualsiasi attributo a cui la tua organizzazione ha accesso in Marketo. In Marketo, puoi utilizzare [Descrizione della richiesta API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) per recuperare i campi attributo a cui la tua organizzazione ha accesso.

## Tipi di pubblico supportati {#supported-audiences}

Questa destinazione supporta l’attivazione di tutti i tipi di pubblico generati tramite l’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md).

Inoltre, questa destinazione supporta anche l’attivazione dei tipi di pubblico descritti nella tabella seguente.

| Tipo di pubblico esterno | Descrizione |
---------|----------|
| Caricamenti personalizzati | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail, ECID) utilizzati in [!DNL Marketo Engage] destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Impostare la destinazione e attivare i tipi di pubblico {#set-up}

>[!IMPORTANT]
> 
>* Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions).
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni dettagliate su come impostare la destinazione e attivare i tipi di pubblico, leggi [Pubblicare un pubblico Adobe Experience Platform in un elenco statico di Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) nella documentazione di Marketo.

Il video seguente illustra anche i passaggi per configurare una destinazione Marketo e attivare i tipi di pubblico.

>[!IMPORTANT]
>
>Il video non riflette completamente la funzionalità corrente. Per le informazioni più aggiornate, consulta la guida collegata in precedenza. Le seguenti parti del video sono obsolete:
> 
>* La scheda di destinazione da utilizzare nell’interfaccia utente di Experienci Platform è **[!UICONTROL Marketo V2]**.
>* Il video non mostra il nuovo **[!UICONTROL Creazione di persona]** campo del selettore nel flusso di lavoro connetti a destinazione.
>* Le due limitazioni indicate nel video non sono più applicabili. Ora puoi mappare molti altri campi dell’attributo del profilo, oltre alle informazioni sull’iscrizione al pubblico supportate al momento della registrazione del video. Puoi anche esportare i membri del pubblico in Marketo che non esistono ancora negli elenchi statici di Marketo e verranno aggiunti agli elenchi.
>* In **[!UICONTROL Passaggio Pianificazione pubblico]** del flusso di lavoro di attivazione, in Marketo V1, era necessario aggiungere manualmente una **[!UICONTROL ID mappatura]** per esportare correttamente i dati in Marketo. Questo passaggio manuale non è più richiesto in Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
