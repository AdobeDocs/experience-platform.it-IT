---
title: Destinazione Marketo Engage
description: Marketo Engage è l'unica soluzione CXM (Customer Experience Management) end-to-end per il marketing, la pubblicità, l'analisi e il commerce. Consente di automatizzare e gestire le attività, dalla gestione dei lead CRM al coinvolgimento dei clienti, fino all’attribuzione dei ricavi e al marketing basato sull’account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 1%

---

# (Legacy) (V2) destinazione Marketo Engage {#beta-marketo-engage-destination}

## Registro modifiche destinazione {#changelog}

<!--
>[!IMPORTANT]
>
>The **[!UICONTROL (Legacy) (V2) Marketo Engage]** will be deprecated in **March 2026**.
>
>To ensure a smooth transition to the new **[[!UICONTROL Marketo Engage]](marketo-engage-connection.md)** destination, review the following key points and required actions:
>
>* All users of the existing **[!UICONTROL (Legacy) (V2) Marketo Engage]** must migrate to the new **[!UICONTROL Marketo Engage]** destination by March 2026.
>* **Existing dataflows will not be migrated automatically.** You must [set up a new connection](../../ui/connect-destination.md) to the new **[!UICONTROL Marketo Engage]** destination and activate your audiences there.

-->

![Immagine delle due schede di destinazione di Marketo in una visualizzazione affiancata.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

I miglioramenti nella destinazione di Marketo V2 includono:

* Nel passaggio **[!UICONTROL Schedule segment]** del flusso di lavoro di attivazione, in Marketo V1, era necessario aggiungere manualmente un **ID mappatura** per esportare correttamente i dati in Marketo. Questo passaggio manuale non è più richiesto in Marketo V2.
* Nel passaggio **[!UICONTROL Mapping]** del flusso di lavoro di attivazione, in Marketo V1, è stato possibile mappare i campi XDM solo su tre campi di destinazione in Marketo: `firstName`, `lastName` e `companyName`. Con la versione di Marketo V2, ora è possibile mappare i campi XDM su molti più campi in Marketo. Per ulteriori informazioni, consulta la sezione [attributi supportati](#supported-attributes) più avanti.

## Panoramica {#overview}

[!DNL Marketo Engage] è l&#39;unica soluzione CXM (Customer Experience Management) end-to-end per il marketing, la pubblicità, l&#39;analisi e il commerce. Consente di automatizzare e gestire le attività, dalla gestione dei lead CRM al coinvolgimento dei clienti, fino all’attribuzione dei ricavi e al marketing basato sull’account.

La destinazione consente agli addetti al marketing di inviare i tipi di pubblico creati in Adobe Experience Platform a Marketo, dove verranno visualizzati come elenchi statici.

## Identità e attributi supportati {#supported-identities-attributes}

>[!NOTE]
>
>Nel [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro attiva destinazione, è *obbligatorio* mappare le identità e *facoltativo* mappare gli attributi. La mappatura di e-mail e/o ECID dalla scheda Identity Namespace (Spazio dei nomi delle identità) è la cosa più importante da fare per garantire che la persona corrisponda in Marketo. La mappatura dell’e-mail assicura la percentuale di corrispondenza più elevata.

### Identità supportate {#supported-identities}

| Identità di destinazione | Descrizione |
|---|---|
| ECID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, consulta il seguente documento su [ECID](/help/identity-service/features/ecid.md). |
| E-mail | Uno spazio dei nomi che rappresenta un indirizzo e-mail. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |

{style="table-layout:auto"}

### Attributi supportati {#supported-attributes}

È possibile mappare gli attributi da Experience Platform a qualsiasi attributo a cui la tua organizzazione ha accesso in Marketo. In Marketo è possibile utilizzare la [richiesta Descrivi API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) per recuperare i campi attributo a cui la tua organizzazione ha accesso.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail, ECID) utilizzati nella destinazione [!DNL Marketo Engage]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Impostare la destinazione e attivare i tipi di pubblico {#set-up}

>[!IMPORTANT]
> 
>* Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions).
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni dettagliate su come impostare la destinazione e attivare i tipi di pubblico, leggi [Pubblicare un pubblico Adobe Experience Platform in un elenco statico di Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=it) nella documentazione di Marketo.

Il video seguente illustra anche i passaggi per configurare una destinazione Marketo e attivare i tipi di pubblico.

>[!IMPORTANT]
>
>Il video non riflette completamente la funzionalità corrente. Per le informazioni più aggiornate, consulta la guida collegata in precedenza. Le seguenti parti del video sono obsolete:
> 
>* La scheda di destinazione da utilizzare nell&#39;interfaccia utente di Experience Platform è **[!UICONTROL Marketo V2]**.
>* Il video non mostra il nuovo campo del selettore **[!UICONTROL Person creation]** nel flusso di lavoro di connessione alla destinazione. Per utilizzare questo campo, è necessario mappare sia il nome che il cognome durante il passaggio di mappatura degli attributi.
>* Le due limitazioni indicate nel video non sono più applicabili. Ora puoi mappare molti altri campi dell’attributo del profilo, oltre alle informazioni sull’iscrizione al pubblico supportate al momento della registrazione del video. Puoi anche esportare i membri del pubblico in Marketo che non esistono ancora negli elenchi statici di Marketo e verranno aggiunti agli elenchi.
>* In Marketo V1, nel **[!UICONTROL Schedule audience step]** del flusso di lavoro di attivazione era necessario aggiungere manualmente **[!UICONTROL Mapping ID]** per esportare correttamente i dati in Marketo. Questo passaggio manuale non è più richiesto in Marketo V2.

>[!VIDEO](https://video.tv.adobe.com/v/3440166?captions=ita&quality=12)

## Monitorare la destinazione {#monitor-destination}

Dopo la connessione alla destinazione e la definizione di un flusso di dati di destinazione, puoi utilizzare la [funzionalità di monitoraggio](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP per ottenere informazioni dettagliate sui record del profilo attivati nella destinazione in ogni esecuzione del flusso di dati.

Le informazioni di monitoraggio per la connessione [!DNL Marketo Engage] includono informazioni a livello di pubblico relative a identità attivate, escluse e non riuscite in ogni flusso di dati e flusso di dati eseguito. [Ulteriori informazioni](/help/dataflows/ui/monitor-destinations.md#segment-level-view) sulla nuova funzionalità.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la [panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).
