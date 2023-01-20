---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;generare set di dati;generare set di dati;creare set di dati;
solution: Experience Platform
title: Genera set di dati di output dai risultati della query
type: Tutorial
description: Adobe Experience Platform Query Service consente la creazione di set di dati dall’interfaccia utente. Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati nel Data Lake e utilizzarlo per diversi casi d’uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 0%

---

# Genera set di dati di output dai risultati della query

[!DNL Query Service] consente di utilizzare le query per generare i set di dati in [!DNL Data Lake]. Questi set di dati possono quindi essere utilizzati come input per più query o in altri servizi come [!DNL Data Science Workspace], Profilo cliente in tempo reale o [!DNL Analysis Workspace].

## Generare set di dati dall’interfaccia utente di Adobe Experience Platform

Per creare set di dati dall’interfaccia utente di Adobe Experience Platform, effettua le seguenti operazioni:

1. Crea una query utilizzando un client connesso e convalida l’output. Per imparare a scrivere query utilizzando [!DNL Query Editor], leggi [!DNL Query Editor] Guida all’interfaccia utente [durante la scrittura di query](./user-guide.md#writing-queries).

2. Nell’interfaccia utente di Platform, passa a **[!UICONTROL Query]** seguito da **[!UICONTROL Modelli]** e seleziona la query creata. Per ulteriori informazioni su come visualizzare le query create e salvate per la tua organizzazione nell’interfaccia utente di Platform, consulta la sezione [[!DNL Query Service] panoramica](./overview.md#browse).

3. Nel pannello Dettagli query, seleziona **[!UICONTROL Set di dati di output]**.

   ![La scheda Modelli dell&#39;area di lavoro Query con Seleziona set di dati di output evidenziato.](../images/ui/create-datasets/output-dataset.png)

4. Nella finestra di dialogo visualizzata, immetti un nome di set di dati preceduto dal tuo ID LDAP. Il nome del set di dati non deve essere univoco o sicuro da SQL. Il nome della tabella per il set di dati verrà generato in base al nome del set di dati creato qui.

5. Quindi, immetti una descrizione per il set di dati in [!UICONTROL Descrizione] campo e seleziona **[!UICONTROL Esegui query]**.

   ![Finestra di dialogo del set di dati di output con i dettagli del set di dati ed esecuzione della query evidenziata](../images/ui/create-datasets/run-query.png)

6. Al termine dell’esecuzione della query, passa a **[!UICONTROL Set di dati]** per visualizzare il set di dati creato. Per ulteriori informazioni su come eseguire azioni comuni quando si utilizzano set di dati nell’interfaccia utente di Platform, consulta la sezione [Guida all’interfaccia utente dei set di dati](../../catalog/datasets/user-guide.md).

Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati nel [!DNL Data Lake] e utilizzati per diversi casi d&#39;uso.

>[!NOTE]
>
>In un’implementazione live, devi applicare le etichette per la governance dei dati dopo la creazione del set di dati. Per ulteriori informazioni su come applicare le etichette di utilizzo dei dati ai set di dati, consulta la sezione [Panoramica delle etichette di utilizzo dei dati](../../data-governance/labels/overview.md).

## Generare set di dati con un predefinito [!DNL Experience Data Model] schema

Utilizza la sintassi SQL per generare un set di dati con un predefinito [!DNL Experience Data Model] Schema (XDM). Per ulteriori informazioni sulla sintassi supportata da [!DNL Query Service], leggi la [Guida alla sintassi SQL](../sql/syntax.md#create-table-as-select).

## Set di dati di output

I set di dati creati tramite questa funzionalità vengono generati con uno schema ad hoc che corrisponde alla struttura dei dati di output definita nell&#39;istruzione SQL. Alcuni servizi a valle richiedono set di dati con particolari schemi XDM. Verifica i requisiti di formattazione dei dati per i servizi downstream prima di scrivere le query.

## Passaggi successivi

Dopo aver letto questo documento, è ora necessario comprendere come utilizzare [!DNL Query Service] per generare set di dati dall’interfaccia utente di Platform. Per ulteriori informazioni su come accedere, scrivere ed eseguire query nell’interfaccia utente di Platform, consulta la sezione [[!DNL Query Service] Panoramica dell’interfaccia utente](./overview.md).
