---
keywords: Experience Platform;home;argomenti popolari;connettore Audience Manager;Audience manager;audience manager
solution: Experience Platform
title: Panoramica di Audience Manager Source
description: L’origine Adobe Audience Manager trasmette i dati di prime parti raccolti in Audience Manager a Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 8ef9fedcc77f39707ef5191988a5b7360e1118cc
workflow-type: tm+mt
source-wordcount: '1127'
ht-degree: 1%

---

# Sorgente Audience Manager

>[!IMPORTANT]
>
>Al momento della configurazione iniziale, l&#39;origine di Adobe Audience Manager restituisce un messaggio di errore che indica che non esiste uno spazio dei nomi di identità con un determinato `namespaceCode={VALUE}`. **Nota**: nel back-end, `namespaceCode` viene utilizzato per fare riferimento al simbolo di identità. Per completare l’integrazione, devi:
>
>- [Creare uno spazio dei nomi personalizzato in Identity Service](../../../identity-service/features/namespaces.md#create-custom-namespaces) con il simbolo di identità specificato (`VALUE`).
>- Acquisisci di nuovo i dati.

L’origine Adobe Audience Manager trasmette i dati di prime parti raccolti in Adobe Audience Manager per l’attivazione in Adobe Experience Platform. L’origine di Audience Manager acquisisce due tipi di dati in Platform:

- **Dati in tempo reale:** Dati acquisiti in tempo reale sul server di raccolta dati di Audience Manager. Questi dati vengono utilizzati in Audience Manager per popolare le caratteristiche basate su regole e compariranno in Platform nel minor tempo di latenza.
- **Dati profilo:** L&#39;Audience Manager utilizza dati in tempo reale e onboarded per derivare i profili dei clienti. Questi profili vengono utilizzati per compilare grafici di identità e caratteristiche sulle realizzazioni dei segmenti.

L’origine di Audience Manager mappa questi tipi di dati su uno schema Experience Data Model (XDM) e quindi li invia a Platform. I dati in tempo reale vengono inviati come dati ExperienceEvent XDM, mentre i dati profilo vengono inviati come dati profilo individuale XDM.

Per ulteriori informazioni, leggere la guida in [creazione di una connessione sorgente Audience Manager nell&#39;interfaccia utente](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Cos’è Experience Data Model (XDM)?

XDM è una specifica documentata pubblicamente che fornisce un framework standardizzato tramite il quale Platform organizza i dati sull’esperienza del cliente.

Il rispetto degli standard XDM consente di incorporare in modo uniforme i dati sull’esperienza del cliente, semplificando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni sull&#39;utilizzo di XDM in Experience Platform, leggere la [Panoramica del sistema XDM](../../../xdm/home.md). Per ulteriori informazioni sulla struttura degli schemi XDM tra profili ed eventi, leggi le [nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md).

## Esempi di schemi XDM

Di seguito sono riportati alcuni Audienci Manager della struttura mappata su ExperienceEvent XDM e Profilo individuale XDM in Platform.

### ExperienceEvent: per dati in tempo reale e dati onboarded

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Profilo individuale XDM - per dati profilo

![](images/aam-profile-xdm-for-profile-data.png)

Per informazioni sul modo in cui i campi vengono mappati da Audience Manager a XDM, consulta la documentazione su [Audience Manager di campi di mappatura](./mapping/audience-manager.md).

## Gestione dei dati sulla piattaforma

### Set di dati

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e campi (righe) e viene reso disponibile da una connessione dati. I dati di Audience Manager sono costituiti da dati in tempo reale, dati in entrata e dati di profilo. Per individuare i set di dati di Audience Manager, utilizza la funzione di ricerca nell’interfaccia utente con le convenzioni di denominazione fornite per ciascun tipo di dati.

I set di dati di Audience Manager sono disabilitati per il profilo per impostazione predefinita e gli utenti possono abilitare o disabilitare i set di dati in base ai loro casi d’uso. Si sconsiglia di disabilitare i set di dati che verranno utilizzati per l’iscrizione al segmento nel profilo.

>[!NOTE]
>
>AAM Il tempo reale è l’unico set di dati che va al data lake. Tutti gli altri set di dati di Audience Manager vanno a [!DNL Profile], se sono abilitati per [!DNL Profile]. Se non sono abilitati per [!DNL Profile], non ricevono dati e verranno visualizzati come vuoti.

| Nome set di dati | Descrizione | Classe |
| --- | --- | --- |
| AAM in tempo reale | Questo set di dati contiene dati raccolti da hit diretti sugli endpoint DCS Audience Manager e mappe di identità per i profili Audience Manager. Mantieni questo set di dati abilitato per l’acquisizione del profilo. | Evento esperienza |
| Aggiornamenti del profilo in tempo reale dell’AAM | Questo set di dati consente il targeting in tempo reale di caratteristiche e segmenti Audience Manager. Include informazioni sull’instradamento regionale di Edge, sulle caratteristiche e sull’iscrizione ai segmenti. Mantieni questo set di dati abilitato per l’acquisizione del profilo. I dati non sono visibili come batch nel set di dati. È possibile abilitare l&#39;interruttore **[!UICONTROL Profilo]** per acquisire direttamente i dati nel profilo. | Record |
| Dati dispositivi AAM | Dati del dispositivo con ECID e realizzazioni del segmento corrispondenti, aggregati in Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare l&#39;interruttore **[!UICONTROL Profilo]** per acquisire direttamente i dati nel profilo. | Record |
| Dati profilo dispositivo AAM | Utilizzato per la diagnostica del connettore di Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare l&#39;interruttore **[!UICONTROL Profilo]** per acquisire direttamente i dati nel profilo. | Record |
| Profili autenticati AAM | Questo set di dati contiene Audienci Manager di profili autenticati. I dati non sono visibili come batch nel set di dati. È possibile abilitare l&#39;interruttore **[!UICONTROL Profilo]** per acquisire direttamente i dati nel profilo. | Record |
| Metadati profili autenticati AAM | Utilizzato per la diagnostica del connettore di Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare l&#39;interruttore **[!UICONTROL Profilo]** per acquisire direttamente i dati nel profilo. | Record |
| Recupero dati dispositivi AAM | Set di dati da importare dati di dispositivi passati. Contiene gli ECID e le realizzazioni dei segmenti corrispondenti aggregati in Audience Manager. I dati non sono visibili come batch nel set di dati. È possibile abilitare l&#39;interruttore **[!UICONTROL Profilo]** per acquisire direttamente i dati nel profilo. | Record |
| Recupero profili autenticati AAM | Set di dati dall’inserimento di dati autenticati precedenti. Audience Manager di profili autenticati. I dati non sono visibili come batch nel set di dati. È possibile abilitare l&#39;interruttore **[!UICONTROL Profilo]** per acquisire direttamente i dati nel profilo. | Record |

### Connessioni

Adobe Audience Manager crea una connessione nel catalogo: Connessione Audience Manager. Catalogo è il sistema dei record per la posizione e la derivazione dei dati in Adobe Experience Platform. Una connessione è un oggetto Catalog che è un&#39;istanza dei connettori specifica del cliente. Per ulteriori informazioni su catalogo, connessioni e connettori, leggere la [panoramica di Catalog Service](../../../catalog/home.md).

### Impatto da popolazione del segmento a profilo

Le dimensioni della popolazione del segmento hanno un impatto diretto sui numeri di profilo quando invii un segmento di Audience Manager a Platform per la prima volta. Ciò significa che la selezione di tutti i segmenti può potenzialmente causare interruzioni del profilo che superano il limite di utilizzo della licenza. Platform distingue anche i nuovi dati dai dati storici per l’acquisizione del profilo. Un segmento con 100 identità basate su prime parti creerà 100 profili. Tuttavia, se la popolazione dello stesso segmento è stata aumentata a 150 ed è stata acquisita in Platform, il numero di profili aumenterà solo di 50, in quanto sono presenti solo 50 nuovi profili.

Puoi anche controllare l&#39;utilizzo del profilo disponibile per il tuo account tramite la [Dashboard utilizzo licenze](../../../dashboards/guides/license-usage.md).

## Qual è la latenza prevista per i dati di Audience Manager su Platform?

| Dati Audience Manager | Tipo | Latenza | Note |
| --- | --- | --- | --- |
| Dati in tempo reale | Eventi | &lt;25 minuti | Tempo dall’acquisizione nel nodo Edge di Audience Manager alla visualizzazione nel data lake. |
| Dati in tempo reale | Aggiornamenti del profilo | &lt;10 minuti | Tempo di atterraggio nel profilo cliente in tempo reale. |
| Dati in tempo reale e onboarded | Aggiornamenti del profilo | Da 24 a 36 ore | Tempo dall&#39;acquisizione tramite dati Edge DCS/PCS e dati onboarded, dall&#39;elaborazione a un profilo utente, alla visualizzazione nel Profilo cliente in tempo reale. Attualmente, questi dati non vengono inseriti direttamente nel data lake. L’attivazione del profilo può essere abilitata, ad Audience Manager per i set di dati Profilo, per acquisire questi dati direttamente in Real-Time Customer Profile. |
