---
keywords: Experience Platform;home;argomenti comuni;connettore Audience Manager;Audience Manager;audience manager
solution: Experience Platform
title: Panoramica origine di Audience Manager
description: L’origine Adobe Audience Manager invia ad Adobe Experience Platform i dati di prime parti raccolti in Audience Manager.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# Origine Audience Manager

L’origine Adobe Audience Manager invia in streaming i dati di prime parti raccolti in Adobe Audience Manager per l’attivazione in Adobe Experience Platform. L’origine Audience Manager acquisisce due tipi di dati in Platform:

- **Dati in tempo reale:** Dati acquisiti in tempo reale sul server di raccolta dati di Audience Manager. Questi dati vengono utilizzati in Audience Manager per popolare caratteristiche basate su regole e verranno visualizzati in Platform nel minor tempo di latenza possibile.
- **Dati profilo:** Audience Manager utilizza dati in tempo reale e onboarded per derivare i profili dei clienti. Questi profili vengono utilizzati per popolare grafici di identità e caratteristiche sulle realizzazioni dei segmenti.

L’origine Audience Manager associa questi tipi di dati a uno schema Experience Data Model (XDM) e li invia a Platform. I dati in tempo reale vengono inviati come dati XDM ExperienceEvent, mentre i dati di profilo vengono inviati come dati XDM di profilo individuale.

Per ulteriori informazioni, consulta la guida su [creazione di una connessione sorgente Audience Manager nell’interfaccia utente](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Cos’è Experience Data Model (XDM)?

XDM è una specifica documentata pubblicamente che fornisce un framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.

Il rispetto degli standard XDM consente di incorporare in modo uniforme i dati sulla customer experience, facilitando la trasmissione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni sull’utilizzo di XDM in Experience Platform, consulta la sezione [Panoramica del sistema XDM](../../../xdm/home.md). Per ulteriori informazioni sulla struttura degli schemi XDM tra profili ed eventi, consulta la sezione [nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md).

## Esempi di schemi XDM

Di seguito sono riportati alcuni esempi della struttura di Audience Manager mappata a XDM ExperienceEvent e al profilo individuale XDM in Platform.

### ExperienceEvent : per dati in tempo reale e dati onboarded

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Profilo individuale XDM - per i dati di profilo

![](images/aam-profile-xdm-for-profile-data.png)

Per informazioni sulla mappatura dei campi da Audience Manager a XDM, consulta la documentazione su [Audience Manager di campi di mappatura](./mapping/audience-manager.md).

## Gestione dei dati su Platform

### Set di dati

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe) ed è reso disponibile tramite una connessione dati. I dati di Audience Manager sono costituiti da dati in tempo reale, dati in entrata e dati di profilo. Per individuare i set di dati di Audience Manager, utilizza la funzione di ricerca nell’interfaccia utente con le convenzioni di denominazione fornite per ciascun tipo di dati.

I set di dati di Audience Manager sono disabilitati per il profilo per impostazione predefinita e gli utenti possono abilitare o disabilitare i set di dati in base ai relativi casi d’uso. Si sconsiglia di disabilitare i set di dati che verranno utilizzati per l’appartenenza al segmento in Profilo.

>[!NOTE]
>
>AAM Real-time è l&#39;unico set di dati che va al data lake. Tutti gli altri set di dati di Audience Manager vengono inviati a [!DNL Profile], se sono abilitati per [!DNL Profile]. Se non sono abilitati per [!DNL Profile], quindi non ricevono dati e vengono visualizzati come vuoti.

| Nome set di dati | Descrizione | Classe |
| --- | --- | --- |
| AAM in tempo reale | Questo set di dati contiene dati raccolti da hit diretti negli endpoint DCS di Audience Manager e mappe di identità per i profili di Audience Manager. Tieni abilitato questo set di dati per l’acquisizione di profili. | Evento esperienza |
| Aggiornamenti AAM profilo in tempo reale | Questo set di dati consente il targeting in tempo reale di caratteristiche e segmenti di Audience Manager. Include informazioni sull’indirizzamento regionale Edge, sulle caratteristiche e sull’appartenenza ai segmenti. Tieni abilitato questo set di dati per l’acquisizione di profili. I dati non sono visibili come batch nel set di dati. È possibile abilitare **[!UICONTROL Profilo]** per acquisire direttamente i dati in Profile (Profilo). | Record |
| Dati dei dispositivi AAM | Dati del dispositivo con ECID e realizzazioni di segmenti corrispondenti aggregate in Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare **[!UICONTROL Profilo]** per acquisire direttamente i dati in Profile (Profilo). | Record |
| Dati profilo dispositivo AAM | Utilizzato per la diagnostica del connettore di Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare **[!UICONTROL Profilo]** per acquisire direttamente i dati in Profile (Profilo). | Record |
| AAM profili autenticati | Questo set di dati contiene Audienci Manager di profili autenticati. I dati non sono visibili come batch nel set di dati. È possibile abilitare **[!UICONTROL Profilo]** per acquisire direttamente i dati in Profile (Profilo). | Record |
| Metadati dei profili autenticati AAM | Utilizzato per la diagnostica del connettore di Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare **[!UICONTROL Profilo]** per acquisire direttamente i dati in Profile (Profilo). | Record |
| Backfill dei dati dei dispositivi AAM | Set di dati per l&#39;inserimento di dati di dispositivi precedenti. Contiene ECID e realizzazioni di segmenti corrispondenti aggregate in Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare **[!UICONTROL Profilo]** per acquisire direttamente i dati in Profilo. | Record |
| Recupero di profili autenticati AAM | Set di dati per l&#39;inserimento di dati autenticati precedenti. Questo contiene Audienci Manager di profili autenticati. I dati non sono visibili come batch nel set di dati. È possibile abilitare **[!UICONTROL Profilo]** per acquisire direttamente i dati in Profilo. | Record |

### Connessioni

Adobe Audience Manager crea una connessione nel Catalogo: Audience Manager di connessione. Catalogo è il sistema dei record per la posizione e la derivazione dei dati all&#39;interno di Adobe Experience Platform. Una connessione è un oggetto Catalog che è un’istanza di connettori specifica del cliente. Per piacere, leggi le [Panoramica del servizio catalogo](../../../catalog/home.md) per ulteriori informazioni su Catalogo, connessioni e connettori.

### Impatto della popolazione del segmento sul profilo

Le dimensioni della popolazione dei segmenti hanno un impatto diretto sui numeri di profilo quando invii un segmento di Audience Manager a Platform per la prima volta. Ciò significa che la selezione di tutti i segmenti può potenzialmente causare sovrapposizioni di profilo che superano l’adesione all’utilizzo della licenza. Platform distingue inoltre i nuovi dati dai dati storici per l’acquisizione di profili. Un segmento con 100 identità basate su prime parti creerà 100 profili. Tuttavia, se la popolazione dello stesso segmento è stata elevata a 150 ed è stata assimilata in Platform, il numero di profili aumenterà solo di 50, in quanto ci sono solo 50 nuovi profili.

Puoi anche verificare l’utilizzo del profilo disponibile per il tuo account tramite [Dashboard di utilizzo della licenza](../../../dashboards/guides/license-usage.md).

## Qual è la latenza prevista per i dati di Audience Manager su Platform?

| Dati Audience Manager | Tipo | Latenza | Note |
| --- | --- | --- | --- |
| Dati in tempo reale | Eventi | &lt;25 minuti | Tempo dall&#39;acquisizione sul nodo Audience Manager Edge per la visualizzazione nel data lake. |
| Dati in tempo reale | Aggiornamenti del profilo | &lt;10 minuti | È ora di iniziare il Profilo del cliente in tempo reale. |
| Dati in tempo reale e onboarded | Aggiornamenti del profilo | da 24 a 36 ore | Tempo dall’acquisizione tramite dati DCS/PCS Edge e dati onboarded, dall’elaborazione a un profilo utente, fino alla visualizzazione nel Profilo cliente in tempo reale. Attualmente, questi dati non arrivano direttamente nel lago dati. L’opzione di attivazione del profilo può essere abilitata, ad Audience Manager, per i set di dati Profilo per acquisire questi dati direttamente nel Profilo cliente in tempo reale. |
