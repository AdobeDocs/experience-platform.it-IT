---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Generazione di set di dati dai risultati della query
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Generazione di set di dati dai risultati della query

La vera potenza di Query Service viene rivelata quando le query vengono utilizzate per generare insiemi di dati nel lago di dati da utilizzare come input per ulteriori query o in altri servizi come Data Science Workspace, Real-time Customer Profile o  Analysis Workspace.

Servizio query consente la creazione di set di dati dall’interfaccia utente. Effettuate le seguenti operazioni:

1. Scrivete la query utilizzando un client connesso e convalidate l&#39;output.
2. Accedete all’interfaccia utente di Platform e passate a Query.
3. Trovare la query nell&#39;elenco e passare il mouse sulla riga.
4. Fate clic su **Crea set di dati**. ![Immagine](../images/queries/create-datasets/click-create-dataset.png)
5. Immettete un nome per il set di dati, preceduto dall’ID LDAP (non deve essere univoco o sicuro da SQL); il sistema genera un &quot;nome tabella&quot; in base al nome qui indicato).
6. Inserite una descrizione del set di dati e fate clic su **Esegui query**.![Immagine](../images/queries/create-datasets/run-query.png)
7. Osservate la query completa, quindi andate alla pagina dell&#39;elenco dei set di dati per vedere il set di dati appena creato.

Dopo la creazione di un set di dati, è possibile accedervi come qualsiasi altro set di dati nel lago di dati e utilizzarlo per diversi casi di utilizzo.

>[!NOTE]
>
>In un&#39;implementazione live, devi applicare etichette di governance dei dati dopo la creazione del set di dati.

## Generazione di set di dati con uno schema modello dati esperienza predefinito

Per generare un dataset con uno schema XDM (Experience Data Model) predefinito, dovrete utilizzare la sintassi SQL. Per ulteriori informazioni sulla sintassi da utilizzare, consultare la guida [alla sintassi](../sql/syntax.md#create-table-as-select)SQL.

## Set di dati di output

I set di dati creati con questa funzionalità vengono generati con uno schema ad hoc che corrisponde alla struttura dei dati di output come definito nell&#39;istruzione SQL. Alcuni servizi a valle richiedono dataset con schemi XDM (Experience Data Model) specifici. Prima di scrivere le query, verificare i requisiti di formattazione dei dati per i servizi a valle.