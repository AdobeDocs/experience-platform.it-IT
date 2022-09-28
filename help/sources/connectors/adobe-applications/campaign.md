---
keywords: Experience Platform;home;argomenti popolari;Adobe Campaign Managed Cloud Services;campagna;servizi gestiti per campagne
title: Adobe Campaign Managed Cloud Services
description: Scopri come collegare Cloud Services gestiti di Campaign a Platform utilizzando l’interfaccia utente di
source-git-commit: 99f65889aecf8c045dbb72053ebaca9429c3ebe1
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Adobe Campaign Managed Cloud Services fornisce una piattaforma Managed Services per la progettazione di esperienze cliente cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel. Visita il [Documentazione di Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) per ulteriori informazioni.

La sorgente Adobe Campaign Managed Cloud Services ti consente di portare i registri di consegna Adobe Campaign v8 e i dati dei registri di tracciamento in Adobe Experience Platform.

## Prerequisiti

Prima di poter creare una connessione sorgente per dare Experience Platform alla tua Campaign v8, devi prima completare i seguenti prerequisiti:

* [Imposta l’importazione del registro eventi utilizzando la console client di Adobe Campaign](#view-delivery-and-tracking-log-data)
* [Creare uno schema ExperienceEvent XDM](#create-a-schema)
* [Creare un set di dati](#create-a-dataset)

### Visualizzare i dati del registro di consegna e di tracciamento {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Per visualizzare i dati di registro in Campaign, devi disporre dell’accesso alla console client Adobe Campaign v8 . Visita il [Documentazione di Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) per informazioni su come scaricare e installare la console client.

Accedi all’istanza Campaign v8 tramite la console client. Sotto la [!DNL Explorer] scheda , seleziona [!DNL Administration] quindi seleziona [!DNL Configuration]. Quindi, seleziona [!DNL Data schemas] e quindi applicare il `broadLog` filtro per nome o etichetta. Nell’elenco visualizzato, seleziona lo schema di origine dei registri di consegna destinatari con il nome `broadLogRcp`.

![La console client Adobe Campaign v8 con la scheda Explorer selezionata, i nodi Amministrazione, Configurazione e Schema dati si sono espansi e filtrano impostati su &quot;ampio&quot;.](./images/campaign/explorer.png)

Quindi, seleziona la **Dati** scheda .

![Console client Adobe Campaign v8 con la scheda dati selezionata.](./images/campaign/data.png)

Fai clic con il pulsante destro del mouse o premi il tasto nel pannello dati per aprire il menu contestuale. Da qui, seleziona **Configura elenco...**

![Console client Adobe Campaign v8 con menu contestuale aperto e opzione Configura elenco selezionata.](./images/campaign/configure.png)

Viene visualizzata la finestra di configurazione dell’elenco, che fornisce un’interfaccia in cui è possibile aggiungere all’elenco preesistente tutti i campi desiderati per visualizzare i dati nel pannello dati.

![Elenco di configurazioni per i registri di consegna dei destinatari che possono essere aggiunte per la visualizzazione.](./images/campaign/list-configuration.png)

Ora puoi visualizzare i registri di consegna dei destinatari, inclusi i campi di configurazione aggiunti nel passaggio precedente.

>[!TIP]
>
>È possibile ripetere gli stessi passaggi, ma filtrare per `tracking` per visualizzare i dati del registro di tracciamento.

![I registri di consegna dei destinatari visualizzati con informazioni sul nome modificato, il canale di consegna, il nome di consegna interno e l’etichetta.](./images/campaign/recipient-delivery-logs.png)

### Creare uno schema {#create-a-schema}

Quindi, crea uno schema ExperienceEvent XDM per i registri di consegna e di tracciamento. Devi applicare il gruppo di campi Registri di consegna Campaign allo schema dei registri di consegna e il gruppo di campi Registri di tracciamento campagna allo schema dei registri di tracciamento. È inoltre necessario definire le `externalID` come identità principale dello schema.

>[!NOTE]
>
>Lo schema ExperienceEvent XDM deve essere abilitato per il profilo per acquisire i dati Campaign in [!DNL Real-time Customer Profile].

Per istruzioni dettagliate su come creare uno schema, consulta la guida in [creazione di uno schema XDM nell’interfaccia utente](../../../xdm/tutorials/create-schema-ui.md).

### Creare un set di dati {#create-a-dataset}

Infine, devi creare un set di dati per i tuoi schemi. Per istruzioni dettagliate su come creare un set di dati, consulta la guida su [creazione di un set di dati nell’interfaccia utente](../../../catalog/datasets/user-guide.md).

## Creare una connessione sorgente Adobe Campaign Managed Cloud Services tramite l’interfaccia utente di Platform

Ora che hai effettuato l’accesso ai registri dati nella console del client Campaign, hai creato uno schema e un set di dati, puoi procedere alla creazione di una connessione sorgente per trasferire i dati di Campaign Managed Services a Platform.

Per istruzioni dettagliate su come portare i registri di consegna v8 di Campaign e i dati dei registri di tracciamento in Experience Platform, consulta la guida su [creazione di una connessione sorgente Managed Services Campaign nell’interfaccia utente](../../tutorials/ui/create/adobe-applications/campaign.md).