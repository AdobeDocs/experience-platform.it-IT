---
keywords: ' Experience Platform;home;argomenti popolari;servizio query;servizio query;genera dataset;genera dataset;crea dataset;'
solution: Experience Platform
title: Generazione di set di dati dai risultati della query
topic: queries
type: Tutorial
description: 'Servizio query consente la creazione di set di dati dall’interfaccia utente. Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati nel Data Lake e utilizzarlo per diversi casi di utilizzo. '
translation-type: tm+mt
source-git-commit: 0ba4e26927cdc96855f35d72a8a6de55f4a34bfa
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---


# Generazione di set di dati dai risultati della query

La vera potenza di [!DNL Query Service] viene rivelata quando le query vengono utilizzate per generare set di dati in [!DNL Data Lake] da utilizzare come input in più query o in altri servizi come [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] o [!DNL Analysis Workspace].

[!DNL Query Service] consente la creazione di set di dati dall’interfaccia utente. Effettuate le seguenti operazioni:

1. Scrivete la query utilizzando un client connesso e convalidate l&#39;output.
2. Accedete all&#39;interfaccia [!DNL Platform] e passate a Query.
3. Trovare la query nell&#39;elenco e passare il mouse sulla riga.
4. Fai clic su **[!UICONTROL Create Dataset]**. ![Immagine](../images/ui/output-dataset.png)
5. Immettete un nome per il set di dati, preceduto dall’ID LDAP (non deve essere univoco o sicuro da SQL); il sistema genera un &quot;nome tabella&quot; in base al nome qui indicato).
6. Inserite una descrizione del set di dati e fate clic su **[!UICONTROL Run Query]**.![Immagine](../images/ui/run-query.png)
7. Osservate la query completa, quindi andate alla pagina dell&#39;elenco dei dataset per vedere il set di dati appena creato.

Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati in [!DNL Data Lake] e utilizzarlo per diversi casi di utilizzo.

>[!NOTE]
>
>In un&#39;implementazione live, devi applicare etichette [!DNL Data Governance] dopo la creazione del set di dati.

## Generazione di set di dati con uno schema [!DNL Experience Data Model] predefinito

Per generare un dataset con uno schema [!DNL Experience Data Model] (XDM) predefinito, è necessario utilizzare la sintassi SQL. Per ulteriori informazioni sulla sintassi da utilizzare, consultare la [Guida alla sintassi SQL](../sql/syntax.md#create-table-as-select).

## Set di dati di output

I set di dati creati con questa funzionalità vengono generati con uno schema ad hoc che corrisponde alla struttura dei dati di output come definito nell&#39;istruzione SQL. Alcuni servizi a valle richiedono insiemi di dati con schemi [!DNL Experience Data Model] (XDM) specifici. Prima di scrivere le query, verificare i requisiti di formattazione dei dati per i servizi a valle.