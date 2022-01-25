---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 10%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 gennaio 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [Preparazione dei dati](#data-prep)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)

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
