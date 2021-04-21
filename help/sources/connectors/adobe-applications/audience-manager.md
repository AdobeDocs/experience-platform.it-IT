---
keywords: Experience Platform;home;argomenti comuni;connettore Audience Manager;Audience Manager;audience manager
solution: Experience Platform
title: Panoramica del connettore di origine di Audience Manager
topic-legacy: overview
description: Il connettore di origine Adobe Audience Manager invia in Adobe Experience Platform i dati di prime parti raccolti in Audience Manager.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 0%

---

# Connettore Audience Manager

Il connettore dati Adobe Audience Manager invia in Adobe Experience Platform i dati di prime parti raccolti in Adobe Audience Manager. Il connettore di Audience Manager acquisisce due categorie di dati in Platform:

- **Dati in tempo reale:** dati acquisiti in tempo reale sul server di raccolta dati di Audience Manager. Questi dati vengono utilizzati in Audience Manager per popolare caratteristiche basate su regole e verranno visualizzati in Platform nel minor tempo di latenza possibile.
- **Dati profilo:** Audience Manager utilizza dati in tempo reale e onboarded per derivare i profili dei clienti. Questi profili vengono utilizzati per popolare grafici di identità e caratteristiche sulle realizzazioni dei segmenti.

Il connettore di Audience Manager mappa queste categorie di dati sullo schema Experience Data Model (XDM) e le invia a Platform. I dati in tempo reale vengono inviati come dati XDM ExperienceEvent, mentre i dati di profilo vengono inviati come profili individuali XDM.

Per istruzioni su come creare una connessione con Adobe Audience Manager utilizzando l’interfaccia utente di Platform, consulta l’ [tutorial sul connettore di Audience Manager](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Cos’è Experience Data Model (XDM)?

XDM è una specifica documentata pubblicamente che fornisce un framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.

Il rispetto degli standard XDM consente di incorporare in modo uniforme i dati sulla customer experience, facilitando la trasmissione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni sull&#39;utilizzo di XDM in Experience Platform, consulta la [Panoramica del sistema XDM](../../../xdm/home.md). Per ulteriori informazioni sulla struttura degli schemi XDM come Profilo ed ExperienceEvent, consulta le [nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md).

## Esempi di schemi XDM

Di seguito sono riportati alcuni esempi della struttura di Audience Manager mappata a XDM ExperienceEvent e al profilo individuale XDM in Platform.

### ExperienceEvent - per dati in tempo reale e dati onboarded

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Profilo individuale XDM - per i dati di profilo

![](images/aam-profile-xdm-for-profile-data.png)

## Come vengono mappati i campi da Adobe Audience Manager a XDM?

Per ulteriori informazioni, consulta la documentazione relativa a [campi di mappatura Audienci Manager](./mapping/audience-manager.md) .

## Gestione dei dati su Platform

### Set di dati

I set di dati sono un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene schema (colonne) e campi (righe) ed è resa disponibile da una connessione dati. I dati di Audience Manager sono costituiti da dati in tempo reale, dati in entrata e dati di profilo. Per individuare i set di dati di Audience Manager, utilizza la funzione di ricerca nell’interfaccia utente con le convenzioni di denominazione fornite per ciascun tipo di dati.

I set di dati di Audience Manager sono disabilitati per il profilo per impostazione predefinita e gli utenti possono abilitare o disabilitare i set di dati in base ai relativi casi d’uso. Si sconsiglia di disabilitare i set di dati che verranno utilizzati per l’appartenenza al segmento in Profilo.

| Nome set di dati | Descrizione |
| ------------ | ----------- |
| AAM in tempo reale | Questo set di dati contiene dati raccolti da hit diretti negli endpoint DCS di Audience Manager e mappe di identità per i profili di Audience Manager. Tieni abilitato questo set di dati per l’acquisizione di profili. |
| Aggiornamenti AAM profilo in tempo reale | Questo set di dati consente il targeting in tempo reale di caratteristiche e segmenti di Audience Manager. Include informazioni sull’indirizzamento regionale Edge, sulle caratteristiche e sull’appartenenza ai segmenti. Tieni abilitato questo set di dati per l’acquisizione di profili. I dati non sono visibili come batch nel set di dati. Puoi abilitare l’opzione **[!UICONTROL Profile]** per acquisire direttamente i dati in Profilo. |
| Dati dei dispositivi AAM | Dati del dispositivo con ECID e realizzazioni di segmenti corrispondenti aggregate in Audience Manager. I dati non sono visibili come batch nel set di dati. Puoi abilitare l’opzione **[!UICONTROL Profile]** per acquisire direttamente i dati in Profilo. |
| Dati profilo dispositivo AAM | Utilizzato per la diagnostica del connettore di Audience Manager. I dati non sono visibili come batch nel set di dati. Puoi abilitare l’opzione **[!UICONTROL Profile]** per acquisire direttamente i dati in Profilo. |
| AAM profili autenticati | Questo set di dati contiene Audienci Manager di profili autenticati. I dati non sono visibili come batch nel set di dati. Puoi abilitare l’opzione **[!UICONTROL Profile]** per acquisire direttamente i dati in Profilo. |
| Metadati dei profili autenticati AAM | Utilizzato per la diagnostica del connettore di Audience Manager. I dati non sono visibili come batch nel set di dati. Puoi abilitare l’opzione **[!UICONTROL Profile]** per acquisire direttamente i dati in Profilo. |
| Backfill dei dati dei dispositivi AAM | Set di dati per l&#39;inserimento di dati di dispositivi precedenti. Contiene ECID e realizzazioni di segmenti corrispondenti aggregate in Audience Manager. I dati non sono visibili come batch nel set di dati. Puoi abilitare l’opzione **[!UICONTROL Profile]** per acquisire direttamente i dati in Profilo. |
| Recupero di profili autenticati AAM | Set di dati per l&#39;inserimento di dati autenticati precedenti. Questo contiene Audienci Manager di profili autenticati. I dati non sono visibili come batch nel set di dati. Puoi abilitare l’opzione **[!UICONTROL Profile]** per acquisire direttamente i dati in Profilo. |

### Connessioni

Adobe Audience Manager crea una connessione nel Catalogo: Audience Manager di connessione. Catalogo è il sistema dei record per la posizione e la derivazione dei dati all&#39;interno di Adobe Experience Platform. Una connessione è un oggetto Catalog che è un’istanza specifica del cliente dei connettori. Per ulteriori informazioni su Catalogo, connessioni e connettori, consulta la [Panoramica del servizio catalogo](../../../catalog/home.md) .

## Qual è la latenza prevista per i dati di Audience Manager su Platform?

| Dati Audience Manager | Latenza | Note |
| --- | --- | --- |
| Dati in tempo reale | &lt; 35 minuti. | Tempo dall’acquisizione sul nodo Audience Manager Edge alla visualizzazione su Platform Data Lake. |
| Dati profilo | &lt; 2 giorni | Tempo dall’acquisizione tramite dati DCS/PCS Edge e dati onboarded, dall’elaborazione a un profilo utente, fino alla visualizzazione in Profilo. Questi dati non arrivano direttamente su Platform Data Lake oggi. L’opzione di attivazione del profilo può essere abilitata, ad Audience Manager, per i set di dati Profilo per l’acquisizione diretta di tali dati in Profilo. |
