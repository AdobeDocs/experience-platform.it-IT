---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;generare set di dati;generare set di dati;creare set di dati;
solution: Experience Platform
title: Genera set di dati di output dai risultati della query
type: Tutorial
description: Adobe Experience Platform Query Service consente di creare set di dati dall’interfaccia utente. Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati nel Data Lake e utilizzarlo per diversi casi d’uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Genera set di dati di output dai risultati della query

[!DNL Query Service] consente di utilizzare le query per generare set di dati in [!DNL Data Lake]. Questi set di dati possono quindi essere utilizzati come input per più query o in altri servizi come [!DNL Data Science Workspace], Real-Time Customer Profile o [!DNL Analysis Workspace].

## Generare set di dati dall’interfaccia utente di Adobe Experience Platform

Per creare set di dati dall’interfaccia utente di Adobe Experience Platform, effettua le seguenti operazioni:

1. Crea una query utilizzando un client connesso e convalida l’output. Per scoprire come scrivere query utilizzando [!DNL Query Editor], leggi [!DNL Query Editor] Guida all’interfaccia utente [sulla scrittura di query](./user-guide.md#writing-queries).

2. Nell’interfaccia utente di Platform, passa a **[!UICONTROL Query]** seguito da **[!UICONTROL Modelli]** e selezionare la query creata. Per ulteriori dettagli su come visualizzare le query create e salvate per la tua organizzazione nell’interfaccia utente di Platform, leggi [[!DNL Query Service] panoramica](./overview.md#browse).

3. Nel pannello Dettagli query, seleziona **[!UICONTROL Set di dati di output]**.

   ![La scheda Modelli dell’area di lavoro Query con Seleziona set di dati di output evidenziato.](../images/ui/create-datasets/output-dataset.png)

4. Nella finestra di dialogo visualizzata, inserisci il nome di un set di dati aggiunto all’ID LDAP. Il nome del set di dati non deve essere univoco o sicuro per SQL. Tieni presente che il nome della tabella per il set di dati verrà generato in base al nome del set di dati creato qui.

5. Quindi, immetti una descrizione per il set di dati in [!UICONTROL Descrizione] e seleziona **[!UICONTROL Esegui query]**.

   ![Finestra di dialogo Set di dati di output con i dettagli del set di dati ed esegui query evidenziata](../images/ui/create-datasets/run-query.png)

6. Una volta completata l’esecuzione della query, passa a **[!UICONTROL Set di dati]** per visualizzare il set di dati creato. Per ulteriori informazioni su come eseguire azioni comuni quando si utilizzano i set di dati nell’interfaccia utente di Platform, consulta [Guida all’interfaccia utente dei set di dati](../../catalog/datasets/user-guide.md).

Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati in [!DNL Data Lake] e utilizzati per una varietà di casi d’uso.

>[!NOTE]
>
>In un’implementazione live, devi applicare le etichette di governance dei dati dopo la creazione del set di dati. Per ulteriori informazioni su come applicare le etichette di utilizzo dei dati ai set di dati, consulta [Panoramica delle etichette di utilizzo dei dati](../../data-governance/labels/overview.md).

## Genera set di dati con un predefinito [!DNL Experience Data Model] schema

Utilizzare la sintassi SQL per generare un set di dati con un [!DNL Experience Data Model] (XDM). Per ulteriori informazioni sulla sintassi supportata da [!DNL Query Service], leggi le [Guida alla sintassi SQL](../sql/syntax.md#create-table-as-select).

## Set di dati di output

I set di dati creati tramite questa funzionalità vengono generati con uno schema ad hoc che corrisponde alla struttura dei dati di output definita nell’istruzione SQL. Alcuni servizi a valle richiedono set di dati con schemi XDM specifici. Verifica i requisiti di formattazione dei dati per i servizi a valle prima di scrivere le query.

## Passaggi successivi

Dopo aver letto questo documento, dovresti sapere come utilizzare [!DNL Query Service] per generare set di dati dall’interfaccia utente di Platform. Per ulteriori informazioni su come accedere, scrivere ed eseguire query nell’interfaccia utente di Platform, consulta [[!DNL Query Service] Panoramica dell’interfaccia utente](./overview.md).
