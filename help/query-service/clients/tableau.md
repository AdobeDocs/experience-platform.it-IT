---
keywords: Experience Platform;home;argomenti popolari;tableau;Tableau;servizio query;servizio query;connettersi al servizio query;
solution: Experience Platform
title: Connettere Tableau a Query Service
description: Questo documento illustra i passaggi necessari per collegare Tableau a Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Connetti [!DNL Tableau] a Query Service

Questo documento fornisce informazioni per la connessione di [!DNL Tableau] a Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Tableau] e che tu abbia familiarità con le modalità di navigazione nella relativa interfaccia. Ulteriori informazioni su [!DNL Tableau] sono disponibili nella [documentazione [!DNL Tableau] ufficiale](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Le istruzioni su come [connettersi a un server PostgreSQL con Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) sono disponibili nel sito Web ufficiale di Tableau. Una volta visualizzata la finestra di dialogo per le impostazioni di connessione, immetti le credenziali di Platform nei campi dei parametri per la connessione a Adobe Experience Platform. Di seguito è riportato un elenco dei parametri di connessione richiesti.

| Parametro di connessione | Descrizione |
|---|---|
| **[!DNL Server]** | L’indirizzo del percorso di archiviazione SFTP. Utilizza il valore delle credenziali dell&#39;Experience Platform **[!UICONTROL Host]**. |
| **[!DNL Port]:** | Porta per [!DNL Query Service]. Per connettersi a [!DNL Query Service], è necessario utilizzare la porta **80** o **5432**. |
| **[!DNL Database]** | Database a cui si desidera accedere. Utilizza il valore delle credenziali dell&#39;Experience Platform **[!UICONTROL Database]**: `prod:all`. |
| **[!DNL Authentication]:** | Il metodo scelto per dimostrare l’identità dell’utente. Si consiglia di selezionare [!DNL Username and Password] dalle opzioni disponibili del menu a discesa. |
| **[!DNL Username]** | Questo è l’ID organizzazione della tua piattaforma. Utilizza il valore delle credenziali dell&#39;Experience Platform **[!UICONTROL Nome utente]**. L&#39;ID sarà nel formato di `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Questa stringa alfanumerica è la credenziale **[!UICONTROL Password]** di Experience Platform. Se si desidera utilizzare credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati di `technicalAccountID` e `credential` scaricati nel file JSON di configurazione. Il valore della password assume la forma: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali senza scadenza è un download una tantum durante l’inizializzazione di, Adobe di cui non conserva una copia. |

Per ulteriori informazioni su come trovare nome utente, password e credenziali di accesso, leggere la [guida delle credenziali](../ui/credentials.md). Per trovare le credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

>[!IMPORTANT]
>
>In qualità di utente Tableau o Power BI, puoi collegare il Customer Journey Analytics agli strumenti di business intelligence dalla scheda Credenziali di Query Service. Consulta la documentazione sulle credenziali per istruzioni su come [collegare gli strumenti di business intelligence al Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).

Verificare di aver selezionato la casella **[!UICONTROL Richiedi SSL]** prima di tentare la connessione. Per informazioni sul supporto SSL per connessioni di terze parti a Adobe Experience Platform Query Service, consulta la [documentazione sulle modalità SSL](./ssl-modes.md).

>[!IMPORTANT]
>
>Le strutture di dati nidificate negli strumenti di BI di terze parti possono essere appiattite per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e generare rapporti sui dati. Per istruzioni su come attivare questa impostazione durante la connessione a un database, vedere la documentazione della funzionalità [`FLATTEN`](../key-concepts/flatten-nested-data.md).

Dopo aver compilato tutte le credenziali, conferma le impostazioni per continuare. Hai effettuato la connessione a Adobe Experience Platform.

## Passaggi successivi

Dopo aver stabilito la connessione con [!DNL Query Service], è possibile utilizzare [!DNL Tableau] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere la guida in [esecuzione di query](../best-practices/writing-queries.md).
