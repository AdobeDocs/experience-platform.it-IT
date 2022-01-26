---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: 9cd9307d54d0950d4f67d5d8cee9c6412a558275
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 7%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 gennaio 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi {#alerts}](#alerts-alerts)
- [[!DNL Data Prep] {#data-prep}](#dnl-data-prep-data-prep)
- [[!DNL Dashboards] {#dashboards}](#dnl-dashboards-dashboards)
- [Servizio query {#query-service}](#query-service-query-service)
- [Sandbox {#sandboxes}](#sandboxes-sandboxes)
- [Servizio di segmentazione {#segmentation}](#segmentation-service-segmentation)

## Avvisi {#alerts}

L’Experience Platform ti consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite [!UICONTROL Avvisi] nell’interfaccia utente di Platform e può scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove regole di avviso | Sono ora disponibili diverse nuove regole di avviso per i flussi di lavoro relativi all’acquisizione dei dati, alle identità, ai profili, alla segmentazione e all’attivazione. Vedi la panoramica su [regole di avviso](../../observability/alerts/rules.md) per l’elenco aggiornato dei tipi di avviso. |

Per ulteriori informazioni sugli avvisi in Platform, consulta [panoramica degli avvisi](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esperienza di mappatura consolidata | La nuova interfaccia di mappatura nell’interfaccia utente di Platform offre un’esperienza di mappatura coerente per sfruttare le raccomandazioni di mappatura intelligente, configurare manualmente le regole di mappatura ed eseguire il debug degli errori che si verificano nei set di mappatura. Per ulteriori informazioni, consulta la sezione [[!DNL Data Prep] Guida all’interfaccia utente](../../data-prep/home.md). |

Per ulteriori informazioni su [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## [!DNL Dashboards] {#dashboards}

[!DNL Dashboards] fa cose carine.

| Funzione | Descrizione |
|---------|-------------|
| Sottotitoli intelligenti | Un algoritmo di apprendimento automatico fornisce automaticamente informazioni sul profilo e sui dati del pubblico e illustra pattern e tendenze in un periodo di 30-90 giorni o 12 mesi. Le didascalie includono informazioni su <ul><li>Forma generale e statistiche</li><li>Tendenze e modifiche brusche</li><li>Modelli stagionali</li><li>Anomalie impreviste</li></ul> Per ulteriori informazioni, consulta [dashboard dei profili](../../dashboards/guides/profiles.md#profiles-count-trend) e [dashboard segmenti](../../dashboards/guides/segments.md#audience-size-trend) documentazione. |
| Inventario delle dashboard | Accedi ai rapporti preconfigurati di profili, segmenti e dashboard di destinazioni, comprese eventuali integrazioni installate come PowerBI, in una posizione centralizzata. Per ulteriori informazioni, consulta la sezione [[!DNL Dashboards] panoramica](../../dashboards/home.md). |
| Modelli di rapporto PowerBI | Crea, personalizza o estende le metriche dai modelli di dati di report di profilo, segmenti e destinazioni utilizzando nuovi grafici PowerBI. Il flusso di lavoro di installazione automatizzata ti consente di condividere le informazioni di marketing all’interno dell’organizzazione dall’ambiente PowerBI. Per ulteriori informazioni, consulta la sezione [[!DNL Dashboards] panoramica](../../dashboards/home.md). |

Per ulteriori informazioni su [!DNL Dashboards], vedi [[!DNL Dashboards] panoramica](../../dashboards/home.md).

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

| Funzione | Descrizione |
|----------------------|-----------------------|
| Blocco anonimo | Il costrutto SQL a blocchi anonimi consente di suddividere i processi di preparazione dei dati su larga scala in Query Service in attività più piccole, quindi riutilizzarli ed eseguirli in sequenza per il caricamento incrementale dei dati. Per ulteriori informazioni, consulta la sezione [Panoramica del servizio query](../../query-service/home.md). |
| Organizzazione del set di dati | Fornisce una struttura dati coerente e logica per organizzare le risorse dati da utilizzare con Query Service man mano che la quantità di risorse dati all’interno della sandbox cresce. Per ulteriori informazioni, consulta la sezione [Panoramica del servizio query](../../query-service/home.md). |

Per ulteriori informazioni su [!DNL Query Service], vedi [[!DNL Query Service] panoramica](../../query-service/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experience Platform fornisce sandbox che suddividono una singola istanza di Platform in ambienti virtuali separati per contribuire a sviluppare e sviluppare applicazioni di esperienza digitale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti dell’interfaccia utente delle sandbox | L’indicatore sandbox è ora integrato nell’intestazione di tutte le applicazioni dell’interfaccia utente di Platform. L’indicatore della sandbox visualizza il nome della sandbox, la regione e il tipo e consente inoltre di accedere a un menu a discesa per passare da una sandbox all’altra. Per ulteriori informazioni, consulta la sezione [guida all’interfaccia utente di sandbox](../../sandboxes/ui/user-guide.md). |

Per ulteriori informazioni sulle sandbox, consulta la sezione [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Corrispondenza segmento | Segment Match è un servizio di collaborazione dati che consente a due o più utenti Platform di scambiare dati, basati su identificatori comuni, in modo sicuro, gestito e rispettoso della privacy. Per ulteriori informazioni, consulta la sezione [Panoramica sulla corrispondenza dei segmenti](../../segmentation/ui/segment-match/overview.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).
