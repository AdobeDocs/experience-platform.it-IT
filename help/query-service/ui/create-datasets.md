---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;generare set di dati;generare set di dati;creare set di dati;
solution: Experience Platform
title: Generare set di dati dai risultati nel servizio query
topic-legacy: queries
type: Tutorial
description: Adobe Experience Platform Query Service consente la creazione di set di dati dall’interfaccia utente. Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati nel Data Lake e utilizzarlo per diversi casi d’uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Generare set di dati dai risultati in Query Service

La vera potenza di [!DNL Query Service] viene rivelata quando le query vengono utilizzate per generare set di dati in [!DNL Data Lake] da utilizzare come input in più query o in altri servizi come [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] o [!DNL Analysis Workspace].

[!DNL Query Service] consente la creazione di set di dati dall’interfaccia utente. Segui questi passaggi:

1. Scrivi la query utilizzando un client connesso e convalida l’output.
2. Accedi all’ interfaccia utente [!DNL Platform] e vai a Query .
3. Trova la query nell’elenco e passa il cursore del mouse sulla riga.
4. Seleziona **[!UICONTROL Create Dataset]**. ![Immagine](../images/ui/create-datasets/output-dataset.png)
5. Immetti un nome di set di dati, preceduto dal tuo ID LDAP (non deve essere univoco o sicuro da SQL; il sistema genera un &quot;nome tabella&quot; in base al nome qui indicato).
6. Immetti una descrizione del set di dati e seleziona **[!UICONTROL Run Query]**.![Immagine](../images/ui/create-datasets/run-query.png)
7. Guarda la query completa, quindi vai alla pagina dell’elenco dei set di dati per vedere il set di dati appena creato.

Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati in [!DNL Data Lake] e utilizzarlo per diversi casi d’uso.

>[!NOTE]
>
>In un’implementazione live, è necessario applicare le etichette [!DNL Data Governance] dopo la creazione del set di dati.

## Generare set di dati con uno schema [!DNL Experience Data Model] predefinito

Per generare un set di dati con uno schema [!DNL Experience Data Model] (XDM) predefinito, è necessario utilizzare la sintassi SQL. Per ulteriori informazioni sulla sintassi da utilizzare, leggere la [Guida alla sintassi SQL](../sql/syntax.md#create-table-as-select).

## Set di dati di output

I set di dati creati tramite questa funzionalità vengono generati con uno schema ad hoc che corrisponde alla struttura dei dati di output definita nell&#39;istruzione SQL. Alcuni servizi a valle richiedono set di dati con particolari schemi [!DNL Experience Data Model] (XDM). Verifica i requisiti di formattazione dei dati per i servizi downstream prima di scrivere le query.
