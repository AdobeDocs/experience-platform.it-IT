---
keywords: Experience Platform;home;argomenti popolari;tableau;Tableau;servizio query;servizio query;connettersi al servizio query;
solution: Experience Platform
title: Connettere Tableau a Query Service
description: Questo documento illustra i passaggi necessari per collegare Tableau a Adobe Experience Platform Query Service.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# Connetti [!DNL Tableau] a Query Service

Questo documento fornisce informazioni sulla connessione [!DNL Tableau] con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL Tableau] e hanno familiarità con le modalità di navigazione nell’interfaccia. Ulteriori informazioni su [!DNL Tableau] si trova nella sezione [ufficiale [!DNL Tableau] documentazione](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Istruzioni su come [connettersi a un server PostgreSQL con Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) sono disponibili dal sito ufficiale di Tableau. Una volta visualizzata la finestra di dialogo per le impostazioni di connessione, inserisci le credenziali di Platform nei campi dei parametri per la connessione a Adobe Experience Platform. Di seguito è riportato un elenco dei parametri di connessione richiesti.

| Parametro di connessione | Descrizione |
|---|---|
| **[!DNL Server]** | L’indirizzo del percorso di archiviazione SFTP. Utilizza il valore del tuo Experience Platform **[!UICONTROL Host]** credenziali. |
| **[!DNL Port]:** | La porta per [!DNL Query Service]. È necessario utilizzare la porta **80** o **5432** per connettersi con [!DNL Query Service]. |
| **[!DNL Database]** | Database a cui si desidera accedere. Utilizza il valore del tuo Experience Platform **[!UICONTROL Database]** credenziali: `prod:all`. |
| **[!DNL Authentication]:** | Il metodo scelto per dimostrare l’identità dell’utente. È consigliabile selezionare [!DNL Username and Password] dalle opzioni disponibili del menu a discesa. |
| **[!DNL Username]** | Questo è l’ID organizzazione della tua piattaforma. Utilizza il valore del tuo Experience Platform **[!UICONTROL Nome utente]** credenziali. L’ID sarà nel formato di `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Questa stringa alfanumerica è il tuo Experience Platform **[!UICONTROL Password]** credenziali. Se si desidera utilizzare credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati del `technicalAccountID` e `credential` scaricato nel file JSON di configurazione. Il valore della password è il seguente: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali senza scadenza è un download una tantum durante l’inizializzazione di, Adobe di cui non conserva una copia. |

Per ulteriori informazioni su come trovare nome utente, password e credenziali di accesso, leggere [guida alle credenziali](../ui/credentials.md). Per trovare le credenziali, accedi a [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

Verifica di aver selezionato **[!UICONTROL Richiedi SSL]** prima di tentare la connessione. Consulta la [Documentazione sulle modalità SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Le strutture di dati nidificate negli strumenti di BI di terze parti possono essere appiattite per migliorarne l’usabilità e ridurre il carico di lavoro necessario per recuperare, analizzare, trasformare e generare rapporti sui dati. Consulta la documentazione su[`FLATTEN` funzionalità](../essential-concepts/flatten-nested-data.md) per istruzioni su come attivare questa impostazione durante la connessione a un database.

Dopo aver compilato tutte le credenziali, conferma le impostazioni per continuare. Hai effettuato la connessione a Adobe Experience Platform.

## Passaggi successivi

Ora che hai stabilito una connessione con [!DNL Query Service], è possibile utilizzare [!DNL Tableau] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, consulta la guida su [esecuzione di query](../best-practices/writing-queries.md).
