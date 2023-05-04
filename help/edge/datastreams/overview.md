---
title: Panoramica dei Datastreams
description: Connetti l’integrazione lato client di Experience Platform SDK con i prodotti Adobe e le destinazioni di terze parti.
keywords: configurazione;datastreams;datastreamId;edge;datastream id;Impostazioni ambiente;edgeConfigId;identità;sincronizzazione id abilitata;ID contenitore di sincronizzazione ID;Sandbox;ingresso streaming;set di dati evento;target;codice client;token di proprietà;ID ambiente di Target;destinazioni cookie;destinazioni url;destinazioni Analytics Settings Blockreport suite id;Data Prep for Data Collection;Data Prep;Mapper;Mapper DM;Mapper sul bordo;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# Panoramica dei Datastreams

Un flusso di dati rappresenta la configurazione lato server quando si implementano gli SDK per Web e dispositivi mobili di Adobe Experience Platform. Mentre il [configura, comando](../fundamentals/configuring-the-sdk.md) nell&#39;SDK controlla gli elementi che devono essere gestiti sul client (come il `edgeDomain`), i datastreams gestiscono tutte le altre configurazioni per l&#39;SDK. Quando viene inviata una richiesta a Adobe Experience Platform Edge Network, la `edgeConfigId` viene utilizzato per fare riferimento al datastream. Questo consente di aggiornare la configurazione lato server senza dover apportare modifiche al codice sul sito web.

Puoi creare e gestire i datastreams selezionando **[!UICONTROL Datastreams]** nella navigazione a sinistra nell’interfaccia utente di Adobe Experience Platform o di Raccolta dati.

![Scheda Datastreams nell’interfaccia utente](../assets/datastreams/overview/datastreams-tab.png)

Per ulteriori informazioni su come configurare un datastream nell’interfaccia utente, consulta [guida alla configurazione](./configure.md).

## Gestione dei dati sensibili nei datastreams {#sensitive}

>[!IMPORTANT]
>
>Il contenuto di questo documento non rappresenta e non intende sostituirsi a una consulenza legale. Consulta l’ufficio legale della tua azienda per ricevere consigli sul trattamento dei dati sensibili.

Le politiche aziendali di gestione dei dati e i requisiti normativi stanno aumentando le restrizioni sul modo in cui i dati sensibili dei clienti possono essere raccolti, elaborati e utilizzati. Ciò include la raccolta, il trattamento e l&#39;utilizzo di dati sanitari protetti (PHI) soggetti a normative come l&#39;Health Insurance Portability and Accountability Act (HIPAA).

Datastreams fornisce tre metodi per aiutarti a gestire in modo sicuro i tuoi dati sensibili:

* [Crittografia avanzata](#encryption)
* [Governance dei dati](#governance)
* [Registri di controllo](#audit-logs)

### Crittografia avanzata {#encryption}

Tutti i dati in transito attraverso la rete Edge vengono eseguiti su connessioni protette e crittografate utilizzando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Se il datastream sta inserendo dati in Experience Platform, i dati vengono poi crittografati a riposo nel data lake Experience Platform. Visualizza il documento in [crittografia dei dati in Experience Platform](../../landing/governance-privacy-security/encryption.md) per ulteriori informazioni.

### Governance dei dati {#governance}

I Datastreams sfruttano le funzionalità integrate di governance dei dati di Experience Platform per impedire l’invio di dati sensibili a servizi non predisposti per l’HIPAA. Etichettando campi specifici che contengono dati sensibili negli schemi del datastream, puoi prendere un controllo granulare su quali campi di dati possono essere utilizzati per scopi specifici.

Il video seguente fornisce una breve panoramica della configurazione e dell’applicazione delle restrizioni di utilizzo dei dati per i datastreams nell’interfaccia utente:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

Ad Experience Platform, puoi applicare [etichette di utilizzo dati sensibili](../../data-governance/labels/reference.md#sensitive) a schemi e campi contenenti dati ritenuti sensibili dalla tua organizzazione. Ad esempio, il `RHD` l&#39;etichetta è utilizzata per indicare le informazioni sulla salute protetta (PHI) e `S1` L’etichetta rappresenta i dati di geolocalizzazione.

>[!NOTE]
>
>Per informazioni dettagliate su come applicare le etichette di utilizzo dei dati all’interno di [!UICONTROL Schemi] nell’interfaccia utente Experience Platform o nell’interfaccia utente di raccolta dati, consulta la [esercitazione sull&#39;etichettatura dello schema](../../xdm/tutorials/labels.md).

Quando crei un nuovo datastream, se lo schema selezionato contiene etichette di utilizzo dati sensibili, il datastream può essere configurato solo per inviare tali dati a destinazioni pronte per l’HIPAA. Attualmente, l’unica destinazione predisposta per HIPAA supportata dai datastreams è Adobe Experience Platform. Altri servizi di destinazione, tra cui Adobe Target, Adobe Analytics, Adobe Audience Manager, inoltro eventi e destinazioni edge, sono disabilitati per i datastreams contenenti etichette di utilizzo dati sensibili.

Se uno schema viene utilizzato in un datastream esistente con servizi non predisposti per HIPAA, il tentativo di aggiungere un&#39;etichetta di utilizzo dei dati sensibili allo schema comporta un messaggio di violazione dei criteri e l&#39;azione viene impedita. Il messaggio specifica quale datastream ha attivato la violazione e suggerisce di rimuovere eventuali servizi non predisposti per HIPAA dal datastream per risolvere il problema.

### Registri di controllo

Ad Experience Platform, le attività del datastream possono essere monitorate sotto forma di registri di controllo. Un registro di controllo comunica **chi** eseguito **cosa** e **quando**, insieme ad altri dati contestuali che possono aiutarti a risolvere i problemi relativi ai datastreams per aiutarti a rispettare le politiche aziendali sulla gestione dei dati e i requisiti normativi.

Ogni volta che un utente crea, aggiorna o elimina un datastream, viene creato un registro di controllo per registrare l’azione. Lo stesso si verifica ogni volta che un utente crea, aggiorna o elimina una mappatura attraverso [Preparazione per la raccolta dei dati](./data-prep.md). Indipendentemente dal fatto che si trattasse di un datastream o di una mappatura aggiornata, il registro di controllo risultante viene classificato in [!UICONTROL Datastreams] tipo di risorsa.

Consulta la documentazione su [registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md) per ulteriori informazioni su come interpretare i registri da datastreams e altri servizi supportati.

## Passaggi successivi

Questa guida fornisce una panoramica di alto livello dei datastreams e del loro utilizzo nella raccolta dati e nell’elaborazione dei dati sensibili. Per i passaggi su come impostare un nuovo datastream, vedi [guida alla configurazione di datastream](./configure.md).
