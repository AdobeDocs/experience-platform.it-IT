---
title: Destinazione Marketo Engage
description: Marketi Engage è l’unica soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il marketing, la pubblicità, l’analisi e il commercio. Ti consente di automatizzare e gestire le attività dalla gestione dei lead CRM e il coinvolgimento dei clienti fino all’attribuzione di marketing e ricavi basata sull’account.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 9f305ee7824bd8790dec57ccbd2d9462ccfa8b49
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 2%

---

# destinazione Marketo Engage {#beta-marketo-engage-destination}

## Passaggio alla destinazione {#changelog}

>[!IMPORTANT]
>
>Con il rilascio della [connettore di destinazione Marketo V2 migliorato](/help/release-notes/2022/july-2022.md#destinations), vedrai due schede Marketo nel catalogo delle destinazioni.
>* Se hai già attivato i dati per la **[!UICONTROL Marketo V1]** destinazione: Crea nuovi flussi di dati per **[!UICONTROL Marketo V2]** destinazione ed eliminazione dei flussi di dati esistenti **[!UICONTROL Marketo V1]** destinazione entro febbraio 2023. A decorrere da tale data, il **[!UICONTROL Marketo V1]** la scheda di destinazione verrà rimossa.
>* Se non hai ancora creato alcun flusso di dati per il **[!UICONTROL Marketo V1]** destinazione, utilizzare il nuovo **[!UICONTROL Marketo V2]** scheda per la connessione e l’esportazione di dati a Marketo.


![Immagine delle due schede di destinazione Marketo affiancate.](/help/destinations/assets/catalog/adobe/marketo-side-by-side-view.png)

I miglioramenti nella destinazione Marketo V2 includono:

* In **[!UICONTROL Segmento di programmazione]** passaggio del flusso di lavoro di attivazione, in Marketo V1, era necessario aggiungere manualmente un **ID mappatura** per esportare correttamente i dati in Marketo. Questo passaggio manuale non è più necessario in Marketo V2.
* In **[!UICONTROL Mappatura]** passaggio del flusso di lavoro di attivazione, in Marketo V1, è stato possibile mappare i campi XDM su soli tre campi target in Marketo: `firstName`, `lastName`e `companyName`. Con la versione Marketo V2, ora puoi mappare i campi XDM su molti altri campi in Marketo. Per ulteriori informazioni, consulta la sezione [attributi supportati](#supported-attributes) più avanti.

## Panoramica {#overview}

[!DNL Marketo Engage] è l’unica soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il marketing, la pubblicità, l’analisi e l’e-commerce. Ti consente di automatizzare e gestire le attività dalla gestione dei lead CRM e il coinvolgimento dei clienti fino all’attribuzione di marketing e ricavi basata sull’account.

La destinazione consente agli esperti di marketing di inviare in push i segmenti creati in Adobe Experience Platform a Marketo dove verranno visualizzati come elenchi statici.

## Identità e attributi supportati {#supported-identities-attributes}

>[!NOTE]
>
>In [fase di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di destinazione di attivazione, è *obbligatorio* mappare le identità e *facoltativo* per mappare gli attributi. La mappatura di E-mail e/o ECID dalla scheda Namespace Identity è la cosa più importante da fare per garantire che la persona corrisponda in Marketo. La mappatura di e-mail garantisce la percentuale di corrispondenza più elevata.

### Identità supportate {#supported-identities}

| Identità di destinazione | Descrizione |
|---|---|
| ECID | Spazio dei nomi che rappresenta ECID. Questo namespace può essere indicato anche dai seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/ecid.md) per ulteriori informazioni. |
| E-mail | Spazio dei nomi che rappresenta un indirizzo e-mail. Questo tipo di spazio dei nomi è spesso associato a una singola persona e può quindi essere utilizzato per identificarla tra canali diversi. |

{style=&quot;table-layout:auto&quot;}

### Attributi supportati {#supported-attributes}

Puoi mappare gli attributi da Experience Platform a uno qualsiasi degli attributi a cui la tua organizzazione ha accesso in Marketo. In Marketo puoi utilizzare la funzione [Descrizione della richiesta API](https://developers.marketo.com/rest-api/lead-database/leads/#describe) per recuperare i campi attributo a cui la tua organizzazione ha accesso.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (e-mail, ECID) utilizzati nel [!DNL Marketo Engage] destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Impostare la destinazione e attivare i segmenti {#set-up}

>[!IMPORTANT]
> 
>* Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions).
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.


Per istruzioni dettagliate su come impostare la destinazione e attivare i segmenti, leggi [Inviare un segmento Adobe Experience Platform a un elenco statico di Marketo](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) nella documentazione di Marketo.

Il video seguente illustra anche i passaggi per configurare una destinazione Marketo e attivare i segmenti.

>[!IMPORTANT]
>
>Il video non riflette completamente la capacità corrente. Per le informazioni più aggiornate, consulta la guida riportata sopra. Le seguenti parti del video sono obsolete:
> 
>* La scheda di destinazione da utilizzare nell’interfaccia utente di Experience Platform è **[!UICONTROL Marketo V2]**.
>* Il video non mostra il nuovo **[!UICONTROL Creazione di persone]** campo selettore nel flusso di lavoro di connessione alla destinazione.
>* Le due limitazioni indicate nel video non sono più applicabili. Ora puoi mappare molti altri campi dell’attributo del profilo oltre alle informazioni sull’appartenenza al segmento supportate al momento della registrazione del video. Puoi anche esportare i membri dei segmenti in Marketo che non esistono ancora negli elenchi statici di Marketo e questi verranno aggiunti agli elenchi.
>* In **[!UICONTROL Fase di pianificazione del segmento]** del flusso di lavoro di attivazione, in Marketo V1, era necessario aggiungere manualmente un **[!UICONTROL ID mappatura]** per esportare correttamente i dati in Marketo. Questo passaggio manuale non è più necessario in Marketo V2.


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
