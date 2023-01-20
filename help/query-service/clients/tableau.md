---
keywords: Experience Platform;home;argomenti popolari;tableau;Tableau;servizio query;servizio query;connessione al servizio query;
solution: Experience Platform
title: Connettere Tableau a Query Service
description: Questo documento descrive i passaggi necessari per la connessione di Tableau con Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connetti [!DNL Tableau] al servizio query

Questo documento fornisce informazioni sulla connessione [!DNL Tableau] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Tableau] e conoscono bene come navigare nella relativa interfaccia. Ulteriori informazioni [!DNL Tableau] si trova nella [ufficiale [!DNL Tableau] documentazione](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Istruzioni su come [connettersi a un server PostgreSQL con Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) sono disponibili sul sito ufficiale Tableau. Una volta visualizzata la finestra di dialogo per le impostazioni di connessione, immetti le credenziali Platform nei campi dei parametri per la connessione con Adobe Experience Platform. Di seguito è riportato un elenco dei parametri di connessione richiesti.

| Parametro di connessione | Descrizione |
|---|---|
| **[!DNL Server]** | L&#39;indirizzo del percorso di archiviazione SFTP. Utilizza il valore del tuo Experience Platform **[!UICONTROL Host]** credenziale. |
| **[!DNL Port]:** | La porta [!DNL Query Service]. È necessario utilizzare la porta **80** o **5432** per connettersi con [!DNL Query Service]. |
| **[!DNL Database]** | Database a cui si desidera accedere. Utilizza il valore del tuo Experience Platform **[!UICONTROL Database]** credenziale: `prod:all`. |
| **[!DNL Authentication]:** | Il metodo scelto per dimostrare l&#39;identità dell&#39;utente. È consigliabile selezionare [!DNL Username and Password] dalle opzioni disponibili del menu a discesa. |
| **[!DNL Username]** | Questo è l’ID organizzazione della piattaforma. Utilizza il valore del tuo Experience Platform **[!UICONTROL Nome utente]** credenziale. L&#39;ID sarà nel formato di `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Questa stringa alfanumerica è il tuo Experience Platform **[!UICONTROL Password]** credenziale. Se desideri utilizzare credenziali non in scadenza, questo valore è costituito dagli argomenti concatenati della variabile `technicalAccountID` e `credential` scaricato nel file JSON di configurazione. Il valore della password assume la forma di: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali non in scadenza è un download una tantum durante l&#39;inizializzazione di cui l&#39;Adobe non conserva una copia. |

Per ulteriori informazioni su come trovare il nome utente, la password e le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md). Per trovare le tue credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

Verifica di aver selezionato il **[!UICONTROL Richiedi SSL]** prima di provare a connettersi. Consulta la sezione [Documentazione sulle modalità SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti al servizio query Adobe Experience Platform.

>[!IMPORTANT]
>
>Le strutture di dati nidificate negli strumenti BI di terze parti possono essere appiattite per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e segnalare i dati. Consulta la documentazione sul[`FLATTEN` caratteristica](../essential-concepts/flatten-nested-data.md) per istruzioni su come attivare questa impostazione durante la connessione a un database.

Dopo aver compilato tutte le credenziali, conferma le impostazioni per continuare. Ora ti sei connesso a Adobe Experience Platform.

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], puoi utilizzare [!DNL Tableau] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida in [query in esecuzione](../best-practices/writing-queries.md).
