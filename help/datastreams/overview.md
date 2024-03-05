---
title: Panoramica sugli stream di dati
description: Scopri come i flussi di dati consentono di collegare l’integrazione lato client dell’SDK Experienci Platform con prodotti Adobe e destinazioni di terze parti.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 77%

---

# Panoramica sugli stream di dati

Un flusso di dati rappresenta la configurazione lato server quando si implementano gli SDK Web e Mobile di Adobe Experience Platform. Mentre il [`configure`](/help/web-sdk/commands/configure/overview.md) nell&#39;SDK controlla gli elementi che devono essere gestiti sul client (come il `edgeDomain`), gli stream di dati gestiscono tutte le altre configurazioni dell’SDK. Quando viene inviata una richiesta ad Adobe Experience Platform Edge Network, il `edgeConfigId` viene utilizzato per fare riferimento allo stream di dati. Questo consente di aggiornare la configurazione lato server senza dover apportare modifiche al codice sul sito web.

Puoi creare e gestire gli stream di dati selezionando **[!UICONTROL Stream di dati]** nell’area di navigazione a sinistra all’interno dell’interfaccia utente di Adobe Experience Platform o di Raccolta dati.

![Scheda stream di dati nell’interfaccia utente](assets/overview/datastreams-tab.png)

Per ulteriori informazioni su come configurare uno stream di dati nell’interfaccia utente, consulta la [guida alla configurazione](./configure.md).

## Gestione dei dati sensibili negli stream di dati {#sensitive}

>[!IMPORTANT]
>
>Il contenuto di questo documento non rappresenta e non intende sostituirsi a una consulenza legale. Consulta l&#39;ufficio legale della tua azienda per ricevere consigli in merito al trattamento dei dati sensibili.

Le politiche aziendali di gestione dei dati e i requisiti normativi stanno aumentando le restrizioni su come i dati sensibili dei clienti possono essere raccolti, elaborati e utilizzati. Ciò include la raccolta, l’elaborazione e l’utilizzo di dati sanitari protetti (PHI), che sono soggetti a normative come l’Health Insurance Portability and Accountability Act (HIPAA).

Gli stream di dati forniscono tre metodi per aiutarti a gestire in modo sicuro i tuoi dati sensibili:

* [Crittografia avanzata](#encryption)
* [Governance dei dati](#governance)
* [Registri di audit](#audit-logs)

### Crittografia avanzata {#encryption}

Tutti i dati in transito attraverso la rete Edge vengono condotti tramite connessioni sicure e crittografate utilizzando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Se il flusso di dati porta i dati in Experience Platform, questi vengono quindi crittografati a riposo nel data lake di Experience Platform. Per ulteriori informazioni, consulta il documento sulla [crittografia dei dati in Experience Platform](../landing/governance-privacy-security/encryption.md).

### Governance dei dati {#governance}

Gli stream di dati utilizzano le funzionalità di governance dei dati integrate di Experience Platform per impedire l’invio di dati sensibili a servizi non conformi HIPAA. Etichettando campi specifici che contengono dati sensibili negli schemi dello stream di dati, puoi avere un controllo granulare su quali campi di dati possono essere utilizzati per scopi specifici.

Il video seguente fornisce una breve panoramica sulla configurazione e l’applicazione delle restrizioni di utilizzo dei dati per i flussi di dati nell’interfaccia utente:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

In Experience Platform, puoi applicare [etichette di utilizzo dei dati sensibili](../data-governance/labels/reference.md#sensitive) agli schemi e ai campi contenenti dati ritenuti sensibili dalla tua organizzazione. Ad esempio, l’etichetta `RHD` viene utilizzata per indicare le informazioni sanitarie protette (PHI) e l’etichetta `S1` rappresenta i dati di geolocalizzazione.

>[!NOTE]
>
>Per informazioni dettagliate su come applicare le etichette di utilizzo dei dati all’interno della scheda [!UICONTROL Schemi] nell’interfaccia utente di Experience Platform o di Raccolta dati, consulta il [tutorial sull’etichettatura degli schemi](../xdm/tutorials/labels.md).

Quando crei un datastream, se lo schema selezionato contiene etichette di utilizzo dei dati sensibili, puoi solo configurare lo stream di dati per inviare tali dati a destinazioni conformi HIPAA. Attualmente, l’unica destinazione conforme HIPAA supportata dagli stream di dati è Adobe Experience Platform. Altri servizi di destinazione, tra cui Adobe Target, Adobe Analytics, Adobe Audience Manager, l’inoltro di eventi e le destinazioni Edge, sono disabilitati per gli stream di dati contenenti etichette di utilizzo dei dati sensibili.

Se uno schema viene utilizzato in uno stream di dati esistente con servizi non conformi HIPAA, il tentativo di aggiungere un’etichetta di utilizzo dei dati sensibili allo schema genera un messaggio di violazione dei criteri e l’azione non è consentita. Il messaggio specifica quale flusso di dati ha attivato la violazione e suggerisce di rimuovere tutti i servizi non conformi HIPAA dallo stream di dati per risolvere il problema.

### Registri di audit

In Experience Platform, le attività dello stream di dati possono essere monitorate sotto forma di registri di audit. I registri di audit indicano **chi** eseguito **cosa** azione, e **quando**, insieme ad altri dati contestuali che possono aiutarti a risolvere i problemi relativi ai flussi di dati per aiutare la tua azienda a rispettare le politiche aziendali di gestione dei dati e i requisiti normativi.

Ogni volta che un utente crea, aggiorna o elimina uno stream di dati, viene creato un registro di audit per registrare l’azione. Lo stesso si verifica ogni volta che un utente crea, aggiorna o elimina una mappatura tramite la [Preparazione dei dati per la raccolta dati](./data-prep.md). Indipendentemente dal fatto che si sia trattato di uno stream di dati o di una mappatura aggiornata, il registro di audit risultante è categorizzato nel tipo di risorsa [!UICONTROL Stream di dati].

Per ulteriori informazioni su come interpretare i registri dagli stream di dati e da altri servizi supportati, consulta la documentazione sui [registri di audit](../landing/governance-privacy-security/audit-logs/overview.md).

## Passaggi successivi

Questa guida fornisce una panoramica di alto livello sugli stream di dati e del loro utilizzo nella raccolta di dati e nell’elaborazione di dati sensibili. Per informazioni su come impostare un nuovo stream di dati, consulta la [guida alla configurazione dello stream di dati](./configure.md).
