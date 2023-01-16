---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;Db Visualizer;DbVisualizer;db visulaizer;connettersi al servizio query;
solution: Experience Platform
title: Collegare DbVisualizer al servizio query
description: Questo documento illustra i passaggi necessari per la connessione di DbVisualizer con Adobe Experience Platform Query Service.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 106a2e4606e94f71d6359cf947e05f193c19c660
workflow-type: tm+mt
source-wordcount: '922'
ht-degree: 1%

---

# Connetti [!DNL DbVisualizer] a [!DNL Query Service] {#connect-dbvisualizer}

Il presente documento descrive i passaggi necessari per la connessione [!DNL DbVisualizer] strumento di database con Adobe Experience Platform [!DNL Query Service].

## Introduzione

Questa guida richiede l’accesso a [!DNL DbVisualizer] app desktop e scopri come navigare nella relativa interfaccia. Per scaricare i [!DNL DbVisualizer] app desktop o per ulteriori informazioni, consulta [ufficiale [!DNL DbVisualizer] documentazione](https://www.dbvis.com/download/).

Acquisizione delle credenziali necessarie per la connessione [!DNL  DbVisualizer] ad Experience Platform, devi disporre dell’accesso all’area di lavoro Query nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro Query, contatta il tuo amministratore dell’organizzazione IMS.

## Creazione di una connessione al database {#connect-database}

Dopo aver installato l’app desktop sul computer locale, segui le istruzioni ufficiali di BDVisualizer su [creare una nuova connessione al database](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Dopo aver selezionato **[!DNL PostgreSQL]** dal [!DNL Connections] elenco [!DNL Object View] scheda per il nuovo [!DNL PostgreSQL] viene visualizzata la connessione.

### Impostare le proprietà del driver per la connessione {#properties}

Da [!DNL PostgreSQL] scheda visualizzazione oggetto, selezionare **[!DNL Properties]** , seguita dalla scheda **[!DNL Driver Properties]** dalla barra laterale di navigazione. Ulteriori informazioni [proprietà del driver](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) si trova nella documentazione ufficiale.

Quindi, immettere le proprietà del driver descritte nella tabella seguente.

>[!IMPORTANT]
>
>Per collegare DBVisualizer a Adobe Experience Platform, devi abilitare l’utilizzo di SSL. Consulta la sezione [Documentazione sulle modalità SSL](./ssl-modes.md) per informazioni sul supporto SSL per le connessioni di terze parti a Adobe Experience Platform Query Service e su come connettersi utilizzando `verify-full` Modalità SSL.

| Proprietà | Descrizione |
| ------ | ------ |
| `PGHOST` | Nome host per [!DNL PostgreSQL] server. Questo valore è il tuo Experience Platform **[!UICONTROL Host] credenziale**. |
| `ssl` | Definire il valore SSL `1` per abilitare l’utilizzo di SSL. |
| `sslmode` | Questo controlla il livello di protezione SSL. Si consiglia di utilizzare il `require` Modalità SSL per la connessione di client di terze parti a Adobe Experience Platform. La `require` In questa modalità, la crittografia è necessaria su tutte le comunicazioni e la rete è affidabile per connettersi al server corretto. La convalida del certificato SSL del server non è necessaria. |
| `user` | Il nome utente connesso al database è l&#39;ID organizzazione. È una stringa alfanumerica che termina in `@Adobe.Org`. Questo valore è il tuo Experience Platform **[!UICONTROL Nome utente] credenziale**. |

Utilizza la barra di ricerca per trovare ogni proprietà, quindi seleziona la cella corrispondente al valore del parametro. La cella verrà evidenziata in blu. Immetti le credenziali della piattaforma nel campo del valore e seleziona **[!DNL Apply]** per aggiungere la proprietà driver.

>[!NOTE]
>
>Per aggiungere un secondo `user` profilo, seleziona `user` dalla colonna del parametro , seleziona l’icona blu + (più) per aggiungere le credenziali per ogni utente. Seleziona **[!DNL Apply]** per aggiungere la proprietà driver.

La [!DNL Edited] mostra un segno di spunta per indicare che il valore del parametro è stato aggiornato.

### Credenziali del servizio query di input {#query-service-credentials}

Per trovare le credenziali necessarie per la connessione di BBVisualizer con Query Service, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per ulteriori informazioni su come trovare le **host**, **porta**, **database**, **username** e **password** credenziali, leggere [guida alle credenziali](../ui/credentials.md).

![La pagina Credenziali dell&#39;area di lavoro Query Experienci Platform con credenziali e le credenziali in scadenza evidenziate.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] offre inoltre credenziali non in scadenza per consentire una configurazione unica con client di terze parti. Consulta la documentazione per [istruzioni complete su come generare e utilizzare le credenziali non in scadenza](../ui/credentials.md#non-expiring-credentials). È necessario completare questo processo se si desidera collegare BDVisualizer come configurazione una tantum. La `credential` e `technicalAccountId` i valori acquisiti comprendono il valore per il DBVisualizer `password` parametro .

## Autenticazione {#authentication}

Per richiedere un ID utente e un&#39;autenticazione basata su password ogni volta che viene stabilita una connessione, passa alla [!DNL Properties] e seleziona **[!DNL Authentication]** dalla barra laterale di navigazione sotto [!DNL PostgreSQL].

Nel pannello Autenticazione connessione, controlla entrambi i parametri **[!DNL Require Userid]** e **[!DNL Require Password]** caselle di controllo e seleziona **[!DNL Apply]**. Ulteriori informazioni [impostazione delle opzioni di autenticazione](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) può essere trovato nella documentazione ufficiale.

## Connetti a Platform

È possibile effettuare una connessione utilizzando credenziali in scadenza o non in scadenza. Per effettuare una connessione, seleziona la **[!DNL Connection]** dalla scheda [!DNL PostgreSQL] scheda visualizzazione oggetto e immetti le credenziali Experience Platform per le seguenti impostazioni. Istruzioni complementari per [impostare una connessione manuale](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) sono disponibili sul sito web ufficiale DBVisualizer.

>[!NOTE]
>
>Tutte le credenziali richieste da BDVisualizer nella tabella seguente sono uguali per le credenziali in scadenza e non in scadenza, a meno che non sia specificato nella descrizione del parametro.

| Parametro di connessione | Descrizione |
|---|---|
| **[!UICONTROL Nome]** | Crea un nome per la connessione. Si consiglia di fornire un nome descrittivo per riconoscere la connessione. |
| **[!UICONTROL Server database]** | Questo è il tuo Experience Platform **[!UICONTROL Host]** credenziale. |
| **[!UICONTROL Porta database]** | La porta [!DNL Query Service]. È necessario utilizzare la porta **80** o **5432** per connettersi con [!DNL Query Service]. |
| **[!UICONTROL Database]** | Utilizza il tuo Experience Platform **[!UICONTROL Database]** valore credenziale: `prod:all`. |
| **[!UICONTROL Userid database]** | Questo è l’ID organizzazione della piattaforma. Utilizza il tuo Experience Platform **[!UICONTROL Nome utente]** valore credenziale. L&#39;ID sarà nel formato di `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Password database]** | Questa stringa alfanumerica è il tuo Experience Platform **[!UICONTROL Password]** credenziale. Se desideri utilizzare credenziali non in scadenza, questo valore è costituito dagli argomenti concatenati della variabile `technicalAccountID` e `credential` scaricato nel file JSON di configurazione. Il valore della password assume la forma di: {technicalAccountId}:{credential}. Il file JSON di configurazione per le credenziali non in scadenza è un download una tantum durante l&#39;inizializzazione di cui l&#39;Adobe non conserva una copia. |

Dopo aver immesso tutte le credenziali rilevanti, seleziona **[!DNL Connect]**.

La [!DNL Connect] nella prima occasione della sessione viene visualizzata la finestra di dialogo. Immetti il tuo ID utente e la tua password e seleziona **[!DNL Connect]**. Nel registro viene visualizzato un messaggio per confermare la riuscita della connessione.

## Passaggi successivi

Ora che ti sei connesso [!DNL DbVisualizer] con [!DNL Query Service], puoi utilizzare [!DNL DbVisualizer] per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere il [guida all’esecuzione delle query](../best-practices/writing-queries.md).
