---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Db Visualizer;DbVisualizer;db visualizzaizer;connect to query service;
solution: Experience Platform
title: Connettere DbVisualizer a Query Service
description: Questo documento illustra i passaggi necessari per la connessione di DbVisualizer con Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 106a2e4606e94f71d6359cf947e05f193c19c660
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 1%

---

# Connetti [!DNL DbVisualizer] a [!DNL Query Service] {#connect-dbvisualizer}

Questo documento illustra i passaggi necessari per collegare [!DNL DbVisualizer] strumento di database con Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede che tu abbia già accesso al [!DNL DbVisualizer] e hanno familiarità con le modalità di navigazione nell&#39;interfaccia. Per scaricare [!DNL DbVisualizer] per ulteriori informazioni, consulta la sezione [ufficiale [!DNL DbVisualizer] documentazione](https://www.dbvis.com/download/).

Per acquisire le credenziali necessarie per la connessione [!DNL  DbVisualizer] ad Experience Platform, devi avere accesso all’area di lavoro Query nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro Query, contatta l’amministratore dell’organizzazione IMS.

## Creare una connessione al database {#connect-database}

Dopo aver installato l&#39;app desktop sul computer locale, seguire le istruzioni ufficiali di BDVisualizer per [creare una nuova connessione al database](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Dopo aver selezionato **[!DNL PostgreSQL]** dal [!DNL Connections] elenco, un [!DNL Object View] scheda per il nuovo [!DNL PostgreSQL] connessione.

### Impostare le proprietà del driver per la connessione {#properties}

Dalla sezione [!DNL PostgreSQL] nella scheda della vista oggetto, selezionare **[!DNL Properties]** , seguito da **[!DNL Driver Properties]** dalla barra laterale di navigazione. Ulteriori informazioni su [proprietà driver](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) si trova nella documentazione ufficiale.

Immettere quindi le proprietà del driver descritte nella tabella seguente.

>[!IMPORTANT]
>
>Per collegare DBVisualizer a Adobe Experience Platform, è necessario abilitare l&#39;utilizzo di SSL. Consulta la [Documentazione sulle modalità SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

| Proprietà | Descrizione |
| ------ | ------ |
| `PGHOST` | Nome host per [!DNL PostgreSQL] server. Questo valore è il tuo Experience Platform **[!UICONTROL Host] credenziali**. |
| `ssl` | Definisci il valore SSL `1` per abilitare l’utilizzo di SSL. |
| `sslmode` | Questo controlla il livello di protezione SSL. Si consiglia di utilizzare il `require` Modalità SSL quando si connettono client di terze parti a Adobe Experience Platform. Il `require` La modalità garantisce che la crittografia sia necessaria in tutte le comunicazioni e che la rete sia attendibile per la connessione al server corretto. La convalida del certificato SSL del server non è richiesta. |
| `user` | Il nome utente connesso al database è l&#39;ID organizzazione. È una stringa alfanumerica che termina con `@Adobe.Org`. Questo valore è il tuo Experience Platform **[!UICONTROL Nome utente] credenziali**. |

Utilizza la barra di ricerca per trovare ogni proprietà, quindi seleziona la cella corrispondente per il valore del parametro. La cella verrà evidenziata in blu. Immetti le credenziali Platform nel campo value (Valore) e seleziona **[!DNL Apply]** per aggiungere la proprietà driver.

>[!NOTE]
>
>Per aggiungere un secondo `user` profilo, seleziona `user` dalla colonna dei parametri, seleziona l’icona blu + (più) per aggiungere le credenziali di ciascun utente. Seleziona **[!DNL Apply]** per aggiungere la proprietà driver.

Il [!DNL Edited] mostra un segno di spunta per indicare che il valore del parametro è stato aggiornato.

### Credenziali di Input Query Service {#query-service-credentials}

Per trovare le credenziali necessarie per collegare BBVisualizer a Query Service, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare **host**, **porta**, **database**, **nome utente**, e **password** , leggere le [guida alle credenziali](../ui/credentials.md).

![Pagina Credenziali dell’area di lavoro Query di Experience Platform con le credenziali ed evidenziate Credenziali in scadenza.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] offre anche credenziali senza scadenza per consentire una configurazione una tantum con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials). È necessario completare questa procedura se si desidera collegare BDVisualizer come configurazione unica. Il `credential` e `technicalAccountId` i valori acquisiti comprendono il valore per DBVisualizer `password` parametro.

## Autenticazione {#authentication}

Per richiedere un ID utente e un’autenticazione basata su password ogni volta che viene stabilita una connessione, passa alla [!DNL Properties] e seleziona **[!DNL Authentication]** dalla barra laterale di navigazione in [!DNL PostgreSQL].

Nel pannello Autenticazione della connessione, seleziona sia **[!DNL Require Userid]** e **[!DNL Require Password]** caselle di controllo, quindi seleziona **[!DNL Apply]**. Ulteriori informazioni su [impostazione delle opzioni di autenticazione](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) possono essere trovate nella documentazione ufficiale.

## Connetti a Platform

È possibile effettuare una connessione utilizzando credenziali in scadenza o non in scadenza. Per effettuare una connessione, selezionare **[!DNL Connection]** scheda da [!DNL PostgreSQL] nella scheda della vista oggetti e immettere le credenziali di Experience Platform per le impostazioni seguenti. Istruzioni complementari per [impostare una connessione manuale](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) sono disponibili sul sito web ufficiale di DBVisualizer.

>[!NOTE]
>
>Tutte le credenziali richieste da BDVisualizer nella tabella seguente sono identiche per le credenziali in scadenza e senza scadenza, a meno che non sia indicato nella descrizione del parametro.

| Parametro di connessione | Descrizione |
|---|---|
| **[!UICONTROL Nome]** | Crea un nome per la connessione. Si consiglia di fornire un nome descrittivo per riconoscere la connessione. |
| **[!UICONTROL Server di database]** | Questo è il tuo Experience Platform **[!UICONTROL Host]** credenziali. |
| **[!UICONTROL Porta database]** | La porta per [!DNL Query Service]. È necessario utilizzare la porta **80** o **5432** per connettersi con [!DNL Query Service]. |
| **[!UICONTROL Database]** | Utilizza il tuo Experience Platform **[!UICONTROL Database]** valore credenziali: `prod:all`. |
| **[!UICONTROL ID utente database]** | Questo è l’ID organizzazione della tua piattaforma. Utilizza il tuo Experience Platform **[!UICONTROL Nome utente]** valore delle credenziali. L’ID sarà nel formato di `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Password database]** | Questa stringa alfanumerica è il tuo Experience Platform **[!UICONTROL Password]** credenziali. Se si desidera utilizzare credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati del `technicalAccountID` e `credential` scaricato nel file JSON di configurazione. Il valore della password è il seguente: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali senza scadenza è un download una tantum durante l’inizializzazione di, Adobe di cui non conserva una copia. |

Dopo aver inserito tutte le credenziali pertinenti, seleziona **[!DNL Connect]**.

Il [!DNL Connect] Il dialogo appare alla prima occasione della sessione. Inserisci l’ID utente e la password e seleziona **[!DNL Connect]**. Nel registro viene visualizzato un messaggio per confermare la connessione.

## Passaggi successivi

Ora che hai effettuato la connessione [!DNL DbVisualizer] con [!DNL Query Service], è possibile utilizzare [!DNL DbVisualizer] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere [guida all’esecuzione delle query](../best-practices/writing-queries.md).
