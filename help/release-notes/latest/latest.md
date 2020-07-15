---
title: 'Note sulla versione di Adobe Experience Platform '
description: Note aggiornate sulla versione di  Experience Platform
doc-type: release notes
last-update: July 15, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 2bbd62fc53d304ff05250688733f1b18dfd18007
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 6%

---


# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 15 luglio 2020**

Aggiornamenti alle funzionalità esistenti in  Adobe Experience Platform:

<!-- - [Data Governance](#governance) -->
<!-- - [Real-time Customer Profile](#profile) -->
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

<!-- ## [!DNL Data Governance] {#governance}

Adobe Experience Platform Data Governance is a series of strategies and technologies used to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data usage. It plays a key role within [!DNL Experience Platform] at various levels, including cataloging, data lineage, data usage labeling, data access policies, and access control on data for marketing actions.

**New features**

| Feature    | Description  |
| -----------| ---------- |
| Automatic policy enforcement in [!DNL Real-time Customer Data Platform] | Data usage policies are now automatically enforced in [!DNL Real-time CDP] when violating actions occur, including activating segments to destinations. When a policy violation is triggered, users get real-time visibility into usage restrictions within the activation workflow, indicating what data they cannot use and why.<br><br>See the section on [enforcing data usage compliance](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance) within the overview on [!DNL Data Governance] in [!DNL Real-time CDP] for more information. |
| Adobe Audience Manager integration | Any segments that are shared with [!DNL Audience Manager] from [!DNL Platform] inherit any applied data usage labels as [!DNL Data Export Controls], and vice versa. See the [!DNL Audience Manager] documentation for specific [mappings between usage labels and Data Export Controls](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep). |
| Custom data usage labels | You can now create custom data usage labels using the Policy Service API or in the UI. See the [labels overview](../../data-governance/labels/overview.md) for more information. |

See the [Data Governance overview](../../data-governance/home.md) for more information on the service.

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform enables you to drive coordinated, consistent, and relevant experiences for your customers no matter where or when they interact with your brand. With [!DNL Real-time Customer Profile], you can see a holistic view of each individual customer that combines data from multiple channels, including online, offline, CRM, and third party data. [!DNL Profile] allows you to consolidate your disparate customer data into a unified view offering an actionable, timestamped account of every customer interaction.

**New features**

| Feature | Description |
| ------- | ----------- |
| Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Profile] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | 

-->

## [!DNL Segmentation Service] {#segmentation}

 Adobe Experience Platform Segmentation Service fornisce un&#39;interfaccia utente e RESTful API che consente di creare segmenti e generare audience dai [!DNL Real-time Customer Profile] dati. Questi segmenti sono configurati e mantenuti a livello centrale, [!DNL Platform]rendendoli facilmente accessibili da qualsiasi applicazione Adobe.

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all&#39;interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Segmentazione in streaming | La segmentazione in streaming può ora essere qualificata come utente in un segmento quando i dati entrano in gioco [!DNL Platform], riducendo notevolmente il tempo di qualificazione del segmento. La segmentazione in streaming riduce inoltre la necessità di eseguire manualmente i processi di segmentazione. |

<!-- | Data usage policy enforcement | In [!DNL Real-time Customer Data Platform], data usage policy violations are automatically surfaced when a violating action in the [!UICONTROL Segments] workspace is attempted. See the [release notes for Data Governance](#governance) for more information on automatic policy enforcement. | -->

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la panoramica sulla [segmentazione](../../segmentation/home.md)

## Origini {#sources}

 Adobe Experience Platform può acquisire dati da origini esterne consentendo al contempo di strutturare, etichettare e migliorare i dati utilizzando [!DNL Platform] i servizi. È possibile acquisire dati da origini diverse, come applicazioni Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

 Experience Platform fornisce un&#39;API RESTful e un&#39;interfaccia utente interattiva che consente di impostare connessioni sorgente per vari provider di dati con facilità. Queste connessioni di origine consentono di autenticare e connettersi a sistemi di storage e servizi CRM esterni, impostare i tempi per l&#39;esecuzione dell&#39;assimilazione e gestire il throughput di assimilazione dei dati.

**Nuove funzionalità**

| Funzione | Descrizione |
| ------- | ----------- |
| Supporto delle API e dell&#39;interfaccia utente per l&#39;eliminazione dei flussi di dati | I flussi di dati che venivano creati con errori o che non erano più necessari ora possono essere eliminati tramite le API o utilizzando l&#39;interfaccia utente. |
| Supporto API e interfaccia utente per l’assimilazione una tantum | L&#39;assimilazione una tantum per i flussi di dati, in cui viene fornita solo la data di inizio e non è pianificata alcuna assimilazione futura, ora può essere eseguita tramite le API o utilizzando l&#39;interfaccia utente. |

Per ulteriori informazioni sulle origini, consultate la panoramica sulle [origini](../../sources/home.md).
