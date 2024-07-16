---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Db Visualizer;DbVisualizer;db visualizzaizer;connect to query service;
solution: Experience Platform
title: Connettere DbVisualizer a Query Service
description: Questo documento illustra i passaggi necessari per la connessione di DbVisualizer con Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 1%

---

# Connetti [!DNL DbVisualizer] a [!DNL Query Service] {#connect-dbvisualizer}

Questo documento descrive i passaggi per la connessione dello strumento di database [!DNL DbVisualizer] con Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede che tu abbia già accesso all&#39;app desktop [!DNL DbVisualizer] e che tu abbia familiarità con le modalità di navigazione nella relativa interfaccia. Per scaricare l&#39;app desktop [!DNL DbVisualizer] o per ulteriori informazioni, consulta la [documentazione ufficiale [!DNL DbVisualizer] ](https://www.dbvis.com/download/).

Per acquisire le credenziali necessarie per la connessione di [!DNL  DbVisualizer] a Experience Platform, è necessario avere accesso all&#39;area di lavoro Query nell&#39;interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro Query, contatta l’amministratore dell’organizzazione.

## Creare una connessione al database {#connect-database}

Dopo aver installato l&#39;app desktop nel computer locale, seguire le istruzioni ufficiali di BDVisualizer per [creare una nuova connessione al database](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Dopo aver selezionato **[!DNL PostgreSQL]** dall&#39;elenco [!DNL Connections], viene visualizzata una scheda [!DNL Object View] per la nuova connessione [!DNL PostgreSQL].

### Impostare le proprietà del driver per la connessione {#properties}

Dalla scheda della visualizzazione oggetti [!DNL PostgreSQL], selezionare la scheda **[!DNL Properties]**, seguita da **[!DNL Driver Properties]** nella barra laterale di navigazione. Ulteriori informazioni sulle [proprietà driver](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) sono disponibili nella documentazione ufficiale.

Immettere quindi le proprietà del driver descritte nella tabella seguente.

>[!IMPORTANT]
>
>Per collegare DBVisualizer a Adobe Experience Platform, è necessario abilitare l&#39;utilizzo di SSL. Per informazioni sul supporto SSL per connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando la modalità SSL `verify-full`, consulta la [documentazione sulle modalità SSL](./ssl-modes.md).

| Proprietà | Descrizione |
| ------ | ------ |
| `PGHOST` | Il nome host per il server [!DNL PostgreSQL]. Questo valore è la credenziale **[!UICONTROL Host] dell&#39;Experience Platform**. |
| `ssl` | Definire il valore SSL `1` per abilitare l&#39;utilizzo di SSL. |
| `sslmode` | Questo controlla il livello di protezione SSL. Si consiglia di utilizzare la modalità SSL `require` per la connessione di client di terze parti a Adobe Experience Platform. La modalità `require` garantisce che la crittografia sia necessaria in tutte le comunicazioni e che la rete sia attendibile per la connessione al server corretto. La convalida del certificato SSL del server non è richiesta. |
| `user` | Il nome utente connesso al database è l&#39;ID organizzazione. Si tratta di una stringa alfanumerica che termina con `@Adobe.Org`. Questo valore è la credenziale **[!UICONTROL Username] di Experience Platform**. |

Utilizza la barra di ricerca per trovare ogni proprietà, quindi seleziona la cella corrispondente per il valore del parametro. La cella verrà evidenziata in blu. Immettere le credenziali Platform nel campo del valore e selezionare **[!DNL Apply]** per aggiungere la proprietà del driver.

>[!NOTE]
>
>Per aggiungere un secondo profilo `user`, seleziona `user` dalla colonna dei parametri, quindi seleziona l&#39;icona blu + (più) per aggiungere le credenziali per ogni utente. Selezionare **[!DNL Apply]** per aggiungere la proprietà del driver.

La colonna [!DNL Edited] mostra un segno di spunta per indicare che il valore del parametro è stato aggiornato.

### Credenziali di Input Query Service {#query-service-credentials}

Per trovare le credenziali necessarie per connettere BBVisualizer con Query Service, accedi all&#39;interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare le credenziali di **host**, **porta**, **database**, **nome utente** e **password**, leggere la [guida delle credenziali](../ui/credentials.md).

![Pagina Credenziali dell&#39;area di lavoro Query Experience Platform con le credenziali evidenziate e le credenziali in scadenza.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] offre anche credenziali senza scadenza per consentire una configurazione una tantum con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials). È necessario completare questa procedura se si desidera collegare BDVisualizer come configurazione unica. I valori `credential` e `technicalAccountId` acquisiti comprendono il valore per il parametro DBVisualizer `password`.

## Autenticazione {#authentication}

Per richiedere un ID utente e un&#39;autenticazione basata su password ogni volta che viene stabilita una connessione, passare alla scheda [!DNL Properties] e selezionare **[!DNL Authentication]** dalla barra laterale di navigazione in [!DNL PostgreSQL].

Nel pannello Autenticazione connessione selezionare le caselle di controllo **[!DNL Require Userid]** e **[!DNL Require Password]**, quindi selezionare **[!DNL Apply]**. Ulteriori informazioni sull&#39;[impostazione delle opzioni di autenticazione](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) sono disponibili nella documentazione ufficiale.

## Connetti a Platform

È possibile effettuare una connessione utilizzando credenziali in scadenza o non in scadenza. Per stabilire una connessione, selezionare la scheda **[!DNL Connection]** dalla scheda Visualizzazione oggetti di [!DNL PostgreSQL] e immettere le credenziali di Experience Platform per le impostazioni seguenti. Le istruzioni complementari per [configurare una connessione manuale](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) sono disponibili sul sito Web ufficiale di DBVisualizer.

>[!NOTE]
>
>Tutte le credenziali richieste da BDVisualizer nella tabella seguente sono identiche per le credenziali in scadenza e senza scadenza, a meno che non sia indicato nella descrizione del parametro.

| Parametro di connessione | Descrizione |
|---|---|
| **[!UICONTROL Nome]** | Crea un nome per la connessione. Si consiglia di fornire un nome descrittivo per riconoscere la connessione. |
| **[!UICONTROL Server database]** | Credenziali dell&#39;Experience Platform **[!UICONTROL Host]**. |
| **[!UICONTROL Porta database]** | Porta per [!DNL Query Service]. Per connettersi a [!DNL Query Service], è necessario utilizzare la porta **80** o **5432**. |
| **[!UICONTROL Database]** | Utilizza il valore delle credenziali dell&#39;Experience Platform **[!UICONTROL Database]**: `prod:all`. |
| **[!UICONTROL ID utente database]** | Questo è l’ID organizzazione della tua piattaforma. Utilizza il valore delle credenziali dell&#39;Experience Platform **[!UICONTROL Nome utente]**. L&#39;ID sarà nel formato di `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Password database]** | Questa stringa alfanumerica è la credenziale **[!UICONTROL Password]** di Experience Platform. Se si desidera utilizzare credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati di `technicalAccountID` e `credential` scaricati nel file JSON di configurazione. Il valore della password assume la forma: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali senza scadenza è un download una tantum durante l’inizializzazione di, Adobe di cui non conserva una copia. |

Dopo aver immesso tutte le credenziali pertinenti, selezionare **[!DNL Connect]**.

La finestra di dialogo [!DNL Connect] viene visualizzata nella prima occasione della sessione. Immettere ID utente e password e selezionare **[!DNL Connect]**. Nel registro viene visualizzato un messaggio per confermare la connessione.

## Passaggi successivi

Ora che hai connesso [!DNL DbVisualizer] a [!DNL Query Service], puoi utilizzare [!DNL DbVisualizer] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere la [guida sull&#39;esecuzione delle query](../best-practices/writing-queries.md).
