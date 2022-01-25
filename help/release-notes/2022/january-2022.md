---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: 49fd8615353a4029b0e98ba90e8438f8ff512e7b
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 12%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 26 gennaio 2021**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Preparazione dei dati](#data-prep)
- [Sandbox](#sandboxes)
- [Servizio di segmentazione](#segmentation)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Esperienza di mappatura consolidata | La nuova interfaccia di mappatura nell’interfaccia utente di Platform offre un’esperienza di mappatura coerente per sfruttare le raccomandazioni di mappatura intelligente, configurare manualmente le regole di mappatura ed eseguire il debug di eventuali errori che si verificano nei set di mappatura. Per ulteriori informazioni, consulta la sezione [[!DNL Data Prep] Guida all’interfaccia utente](../../data-prep/home.md). |

Per ulteriori informazioni su [!DNL Data Prep], vedi [[!DNL Data Prep] panoramica](../../data-prep/home.md).

## Sandbox {#sandboxes}

Adobe Experience Platform è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa. Per soddisfare questa esigenza, Experience Platform fornisce sandbox che suddividono una singola istanza di Platform in ambienti virtuali separati per contribuire a sviluppare e sviluppare applicazioni di esperienza digitale.

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti dell’interfaccia utente delle sandbox | L’indicatore sandbox è ora integrato nell’intestazione di tutte le applicazioni dell’interfaccia utente di Platform. L’indicatore della sandbox visualizza il nome della sandbox, la regione e il tipo e consente inoltre di accedere a un menu a discesa per passare da una sandbox all’altra. Per ulteriori informazioni, consulta la sezione [guida all’interfaccia utente di sandbox](../../sandboxes/ui/user-guide.md). |

Per ulteriori informazioni sulle sandbox, consulta la sezione [panoramica sulle sandbox](../../sandboxes/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

| Funzione | Descrizione |
| --- | --- |
| Corrispondenza segmento | Segment Match è un servizio di collaborazione dati che consente a due o più utenti Platform di scambiare dati, basati su identificatori comuni, in modo sicuro, gestito e rispettoso della privacy. Per ulteriori informazioni, consulta la sezione [Panoramica sulla corrispondenza dei segmenti](../../segmentation/ui/segment-match/overview.md). |

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).
