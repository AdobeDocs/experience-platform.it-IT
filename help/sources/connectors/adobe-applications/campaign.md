---
keywords: Experience Platform;home;argomenti popolari;Adobe Campaign Managed Cloud Services;campagna;campaign managed services
title: Adobe Campaign Managed Cloud Services
description: Scopri come collegare Cloud Service gestiti di Campaign a Platform utilizzando l’interfaccia utente
exl-id: 8f18bf73-ebf1-4b4e-a12b-964faa0e24cc
source-git-commit: 39a503b14c731aeed279bbbfa8c814c2ec26ed92
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 1%

---

# Adobe Campaign Managed Cloud Services

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Adobe Campaign Managed Cloud Services fornisce una piattaforma Managed Services per la progettazione di customer experience cross-channel e un ambiente per l’orchestrazione visiva delle campagne, la gestione delle interazioni in tempo reale e l’esecuzione cross-channel. Visita il [Documentazione di Adobe Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaign-home.html?lang=en) per ulteriori informazioni.

Il codice sorgente di Adobe Campaign Managed Cloud Services consente di portare i registri di consegna e i dati dei registri di tracciamento di Adobe Campaign v8 a Adobe Experience Platform.

## Prerequisiti

Prima di poter creare una connessione sorgente per l’Experience Platform di Campaign v8, è necessario soddisfare i seguenti prerequisiti:

* [Configurare l’importazione del registro eventi utilizzando la console client di Adobe Campaign](#view-delivery-and-tracking-log-data)
* [Creare uno schema XDM ExperienceEvent](#create-a-schema)
* [Creare un set di dati](#create-a-dataset)

### Visualizzare i dati di registro di consegna e tracciamento {#view-delivery-and-tracking-log-data}

>[!IMPORTANT]
>
>Per visualizzare i dati di registro in Campaign, devi avere accesso alla console client di Adobe Campaign v8. Visita il [Documentazione di Campaign v8](https://experienceleague.adobe.com/docs/campaign/campaign-v8/deploy/connect.html?lang=en) per informazioni su come scaricare e installare la console client.

Accedi all’istanza di Campaign v8 tramite la console client. Sotto [!DNL Explorer] , seleziona [!DNL Administration] e quindi seleziona [!DNL Configuration]. Quindi, seleziona [!DNL Data schemas] e quindi applica il `broadLog` filtro per nome o etichetta. Nell’elenco visualizzato, seleziona lo schema di origine dei registri di consegna del destinatario con il nome `broadLogRcp`.

![La console client di Adobe Campaign v8 con la scheda Explorer selezionata, i nodi Administration, Configuration e Data schemas espansi e il filtro impostato su &quot;broad&quot; (Ampia).](./images/campaign/explorer.png)

Quindi, seleziona la **Dati** scheda.

![La console client di Adobe Campaign v8 con la scheda dati selezionata.](./images/campaign/data.png)

Fate clic con il pulsante destro del mouse o premete un tasto nel pannello dati per aprire il menu contestuale. Da qui, seleziona **Configura elenco...**

![Viene aperta la console client di Adobe Campaign v8 con il menu contestuale e l’opzione Configura elenco selezionata.](./images/campaign/configure.png)

Viene visualizzata la finestra di configurazione dell’elenco, che fornisce un’interfaccia in cui è possibile aggiungere eventuali campi desiderati all’elenco preesistente per visualizzare i dati nel pannello dati.

![Un elenco di configurazioni per i registri di consegna dei destinatari che possono essere aggiunte per la visualizzazione.](./images/campaign/list-configuration.png)

Ora puoi visualizzare i registri di consegna dei destinatari, inclusi i campi di configurazione aggiunti nel passaggio precedente.

>[!TIP]
>
>Puoi ripetere gli stessi passaggi, ma filtrare per `tracking` per visualizzare i dati del registro di tracciamento.

![Vengono visualizzati i registri di consegna del destinatario con le informazioni relative all’ultima modifica del nome, del canale di consegna, del nome di consegna interno e dell’etichetta.](./images/campaign/recipient-delivery-logs.png)

### Crea uno schema {#create-a-schema}

Quindi, crea uno schema XDM ExperienceEvent per i registri di consegna e di tracciamento. Devi applicare il gruppo di campi Registri di consegna campagna allo schema dei registri di consegna e il gruppo di campi Registri di tracciamento campagna allo schema dei registri di tracciamento. È inoltre necessario definire `externalID` come identità primaria dello schema.

>[!NOTE]
>
>Per acquisire i dati di Campaign in, lo schema XDM ExperienceEvent deve essere abilitato per il profilo [!DNL Real-Time Customer Profile].

Per istruzioni dettagliate su come creare uno schema, consulta la guida su [creazione di uno schema XDM nell’interfaccia utente](../../../xdm/tutorials/create-schema-ui.md).

### Creare un set di dati {#create-a-dataset}

Infine, devi creare un set di dati per gli schemi. Per istruzioni dettagliate su come creare un set di dati, consulta la guida su [creazione di un set di dati nell’interfaccia utente](../../../catalog/datasets/user-guide.md).

## Creare una connessione sorgente Adobe Campaign Managed Cloud Services utilizzando l’interfaccia utente di Platform

Dopo aver effettuato l’accesso ai registri dati nella console client di Campaign, creato uno schema e un set di dati, ora puoi procedere con la creazione di una connessione di origine per portare i dati di Campaign Managed Services su Platform.

Per istruzioni dettagliate su come trasferire i dati dei registri di consegna e di tracciamento di Campaign v8 in Experience Platform, consulta la guida su [creazione di una connessione sorgente di Campaign Managed Services nell’interfaccia utente](../../tutorials/ui/create/adobe-applications/campaign.md).

>[!IMPORTANT]
>
>Esiste un caso limite in cui l’interazione di un destinatario e-mail rimosso di recente con un’e-mail potrebbe riacquisire informazioni personali in Experienci Platform. In alcuni casi, questo potrebbe riabilitare il marketing per tale utente.
>
>* Questo scenario è attivo solo tra il momento in cui una richiesta di accesso a dati personali viene eseguita in Experienci Platform e il momento in cui viene eseguita in Adobe Campaign Classic. Dopo aver eseguito la richiesta in Campaign, viene eseguito un controllo per verificare che il record non venga esportato in Campaign. Per risolvere il problema, invia nuovamente una richiesta RGPD dopo 72 ore dall’esecuzione.