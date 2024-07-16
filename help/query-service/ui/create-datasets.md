---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;generare set di dati;generare set di dati;creare set di dati;
solution: Experience Platform
title: Genera set di dati di output dai risultati della query
type: Tutorial
description: Adobe Experience Platform Query Service consente di creare set di dati dall’interfaccia utente. Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati nel Data Lake e utilizzarlo per diversi casi d’uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 59d2d74b2d77f3bbaca381af908de5295af24e5b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Genera set di dati di output dai risultati della query

[!DNL Query Service] consente di utilizzare le query per generare set di dati in [!DNL Data Lake]. Questi set di dati possono quindi essere utilizzati come input per ulteriori query o in altri servizi come [!DNL Data Science Workspace], Real-Time Customer Profile o [!DNL Analysis Workspace].

## Generare set di dati dall’interfaccia utente di Adobe Experience Platform

Per creare set di dati dall’interfaccia utente di Adobe Experience Platform, effettua le seguenti operazioni:

1. Crea una query utilizzando un client connesso e convalida l’output. Per informazioni su come scrivere query utilizzando [!DNL Query Editor], leggere la guida dell&#39;interfaccia utente [!DNL Query Editor] [per la scrittura di query](./user-guide.md#writing-queries).

2. Nell&#39;interfaccia utente di Platform, passa a **[!UICONTROL Query]** seguito dalla scheda **[!UICONTROL Modelli]** e seleziona la query creata. Per ulteriori dettagli su come visualizzare le query create e salvate per la tua organizzazione nell&#39;interfaccia utente di Platform, consulta la [[!DNL Query Service] panoramica](./overview.md#browse).

3. Nel pannello Dettagli query, selezionare **[!UICONTROL Esegui come CTAS]**.

   ![Scheda [!UICONTROL Modelli] dell&#39;area di lavoro Query con l&#39;opzione Seleziona [!UICONTROL Esegui come CTAS] evidenziata.](../images/ui/create-datasets/run-as-ctas.png)

4. Nella finestra di dialogo visualizzata, inserisci il nome di un set di dati aggiunto all’ID LDAP. Il nome del set di dati non deve essere univoco o sicuro per SQL. Tieni presente che il nome della tabella per il set di dati verrà generato in base al nome del set di dati creato qui.

5. Immettere quindi una descrizione per il set di dati nel campo [!UICONTROL Descrizione] e selezionare **[!UICONTROL Esegui come CTAS]**.

   ![La finestra di dialogo del set di dati di output con i dettagli del set di dati e [!UICONTROL Esegui come CTAS] è evidenziata](../images/ui/create-datasets/run-query.png)

6. Una volta completata l&#39;esecuzione della query, passa a **[!UICONTROL Set di dati]** per visualizzare il set di dati creato. Per ulteriori informazioni su come eseguire azioni comuni quando si utilizzano i set di dati nell&#39;interfaccia utente di Platform, consulta la [guida all&#39;interfaccia utente dei set di dati](../../catalog/datasets/user-guide.md).

Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati in [!DNL Data Lake] e utilizzarlo per diversi casi d&#39;uso.

>[!NOTE]
>
>In un’implementazione live, devi applicare le etichette di governance dei dati dopo la creazione del set di dati. Per ulteriori informazioni su come applicare etichette di utilizzo dati ai set di dati, consulta la [Panoramica delle etichette di utilizzo dati](../../data-governance/labels/overview.md).

## Genera set di dati con uno schema [!DNL Experience Data Model] predefinito

Utilizzare la sintassi SQL per generare un set di dati con uno schema predefinito [!DNL Experience Data Model] (XDM). Per ulteriori informazioni sulla sintassi supportata da [!DNL Query Service], leggere la [Guida alla sintassi SQL](../sql/syntax.md#create-table-as-select).

## Set di dati di output

I set di dati creati tramite questa funzionalità vengono generati con uno schema ad hoc che corrisponde alla struttura dei dati di output definita nell’istruzione SQL. Alcuni servizi a valle richiedono set di dati con schemi XDM specifici. Verifica i requisiti di formattazione dei dati per i servizi a valle prima di scrivere le query.

## Passaggi successivi

Dopo aver letto questo documento, sarai in grado di utilizzare [!DNL Query Service] per generare set di dati dall&#39;interfaccia utente di Platform. Per ulteriori informazioni su come accedere, scrivere ed eseguire query nell&#39;interfaccia utente di Platform, vedere la [[!DNL Query Service] panoramica dell&#39;interfaccia utente](./overview.md).
