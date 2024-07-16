---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida alle credenziali di Query Service
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti della tua organizzazione.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: ba4ff2715d4e3eb71377542ab2361b967cd3ac11
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 2%

---

# Guida alle credenziali

Adobe Experience Platform Query Service consente di connettersi con client esterni. È possibile connettersi a questi client esterni utilizzando credenziali in scadenza o credenziali senza scadenza.

>[!NOTE]
>
>Il pannello Credenziali non è disponibile automaticamente per tutti gli utenti. Contatta il team del tuo account di Adobe per richiedere che la scheda [!UICONTROL Credenziali] sia inclusa nell&#39;area di lavoro del servizio query se necessario. Se richiesto, questo cambiamento riguarda l’intera organizzazione ed è condotto dal team di progettazione di Adobe. Non si tratta di un’impostazione controllata dagli utenti.

## Credenziali in scadenza {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Modalità SSL del client"
>abstract="La modalità SSL deve essere abilitata nei client connessi a Query Service. Assicurati che la modalità SSL sia impostata su “Richiesta”."

È possibile utilizzare le credenziali in scadenza per impostare rapidamente una connessione a un client esterno.

![Scheda Credenziali del dashboard delle query con la sezione Credenziali in scadenza evidenziata.](../images/ui/credentials/expiring-credentials.png)

La sezione **[!UICONTROL Credenziali in scadenza]** fornisce le seguenti informazioni:

- **[!UICONTROL Host]**: nome dell&#39;host a cui connettere il client. Incorpora il nome dell’organizzazione, come visualizzato nella barra multifunzione superiore dell’interfaccia utente di Platform.
- **[!UICONTROL Porta]**: numero di porta dell&#39;host a cui connettersi.
- **[!UICONTROL Database]**: nome del database a cui connettere un client.
- **[!UICONTROL Nome utente]**: nome utente utilizzato per connettersi a Query Service.
- **[!UICONTROL Password]**: password utilizzata per la connessione a Query Service. Le password nell’interfaccia utente sono state sottoposte a hashing per motivi di sicurezza. Selezionare l&#39;icona Copia (![Icona Copia.](../images/ui/credentials/copy-icon.png)) per copiare le credenziali complete senza hash negli Appunti.
- **[!UICONTROL Comando PSQL]**: comando che ha inserito automaticamente tutte le informazioni rilevanti per la connessione a Query Service tramite PSQL nella riga di comando.
- **[!UICONTROL Scadenza]**: data e ora di scadenza delle credenziali. La durata di validità predefinita del token è di 24 ore, ma può essere modificata nelle impostazioni avanzate dell’Admin Console.

>[!TIP]
>
>Per modificare la durata della sessione per la connessione delle credenziali in scadenza a Query Service, passa all&#39;[Admin Console](https://adminconsole.adobe.com/) e seleziona le seguenti opzioni sullo schermo: **Impostazioni** > **Privacy e sicurezza** > **Impostazioni autenticazione** > **Impostazioni avanzate** > **Durata massima sessione**.
>
>![Scheda Impostazioni Admin Console con Privacy e sicurezza, Impostazioni autenticazione e Durata massima sessione evidenziate.](../images/ui/credentials/max-session-life.png)
>
>Per ulteriori informazioni sulle [impostazioni avanzate](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) offerte da Admin Console, consulta la documentazione dell&#39;Adobe.

### Connettersi ai dati di Customer Journey Analytics nelle sessioni di query {#connect-to-customer-journey-analytics}

Utilizza l&#39;estensione Customer Journey Analytics BI con Power BI o Tableau per accedere alle [visualizzazioni dati](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) del tuo Customer Journey Analytics con SQL. Integrando Query Service con l’estensione BI, puoi accedere alle visualizzazioni dati direttamente all’interno delle sessioni di Query Service. Questa integrazione semplifica le funzionalità degli strumenti BI che utilizzano Query Service come interfaccia PostgreSQL. Questa funzionalità elimina la necessità di duplicare le visualizzazioni dati negli strumenti di business intelligence, garantisce la coerenza dei rapporti tra le piattaforme e semplifica l&#39;integrazione dei dati di Customer Journey Analytics con altre origini nelle piattaforme di business intelligence.

Consulta la documentazione per scoprire come [connettere Query Service a diverse applicazioni client desktop](../clients/overview.md), ad esempio [Power BI](../clients/power-bi.md) o [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>Per utilizzare questa funzionalità sono necessari un progetto Workspace di Customer Journey Analytics e una visualizzazione dati.

Per accedere ai dati di Customer Journey Analytics in Power BI o Tableau, selezionare il menu a discesa [!UICONTROL Database], quindi selezionare `prod:cja` tra le opzioni disponibili. Copiare quindi i parametri delle credenziali [!DNL Postgres] (Host, Porta, Database, Nome utente e altri) da utilizzare nella configurazione di Power BI o Tableau.

![Scheda Credenziali di Query Service con il menu a discesa del database evidenziato.](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>Quando si collega Power BI o Tableau al Customer Journey Analytics, viene utilizzata l’adesione &quot;sessioni simultanee&quot; di Query Service. Se sono necessarie sessioni e query aggiuntive, è possibile acquistare un componente aggiuntivo per il pacchetto di utenti di query ad hoc per ottenere cinque sessioni simultanee aggiuntive e una query concorrente aggiuntiva.

Puoi anche accedere ai dati del Customer Journey Analytics direttamente da Query Editor o Postgres CLI. A tale scopo, fare riferimento al database `cja` durante la scrittura della query. Per ulteriori informazioni su come scrivere, eseguire e salvare le query, vedere la [guida all&#39;authoring delle query](./user-guide.md#query-authoring) di Query Editor.

Per istruzioni complete sull&#39;accesso alle visualizzazioni dati di Customer Journey Analytics con SQL, consulta la [BI extension guide](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/bi-extension).

## Credenziali senza scadenza {#non-expiring-credentials}

È possibile utilizzare credenziali senza scadenza per impostare una connessione più permanente a un client esterno.

>[!NOTE]
>
>Le credenziali senza scadenza hanno le seguenti limitazioni:<br><ul><li>Gli utenti devono effettuare l&#39;accesso con il proprio nome utente e password composti da `{technicalAccountId}:{credential}`. Ulteriori informazioni sono disponibili nella sezione [Genera credenziali](#generate-credentials).</li><li>Al momento della creazione delle credenziali in scadenza, viene creato un nuovo ruolo con un set di autorizzazioni di base che consente agli utenti di visualizzare schemi e set di dati. A questo ruolo viene inoltre assegnata l’autorizzazione &quot;manage queries&quot; (gestisci query), utilizzabile con Query Service.</li><li>I client di terze parti possono ottenere prestazioni diverse da quelle previste quando si elencano oggetti di query. Ad esempio, alcuni client di terze parti come [!DNL DB Visualizer] non visualizzeranno il nome della visualizzazione nel pannello sinistro. Tuttavia, il nome della visualizzazione è accessibile se chiamato all’interno di una query SELECT. Analogamente, [!DNL PowerUI] potrebbe non elencare le viste temporanee create tramite l&#39;istruzione SQL da selezionare per la creazione del dashboard.</li></ul>

### Prerequisiti

Prima di poter generare credenziali senza scadenza, è necessario completare i seguenti passaggi in Adobe Admin Console:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/) e seleziona l&#39;organizzazione pertinente dalla barra di navigazione superiore.
2. [Seleziona un profilo di prodotto.](../../access-control/ui/browse.md)
3. [Configura le autorizzazioni **Sandbox** e **Gestione integrazione servizio query**](../../access-control/ui/permissions.md) per il profilo di prodotto.
4. [Aggiungi un nuovo utente a un profilo di prodotto](../../access-control/ui/users.md) in modo che possa disporre delle autorizzazioni configurate.
5. [Aggiungi l&#39;utente come amministratore del profilo di prodotto](https://helpx.adobe.com/it/enterprise/using/manage-product-profiles.html) per consentire la creazione di un account per qualsiasi profilo di prodotto attivo.
6. [Aggiungi l&#39;utente come sviluppatore del profilo di prodotto](https://helpx.adobe.com/it/enterprise/using/manage-developers.html) per creare un&#39;integrazione.

Per ulteriori informazioni su come assegnare le autorizzazioni, leggere la documentazione sul [controllo di accesso](../../access-control/home.md).

In Adobe Developer Console sono ora configurate tutte le autorizzazioni necessarie affinché l’utente possa utilizzare la funzione delle credenziali in scadenza.

### Genera credenziali {#generate-credentials}

Per creare un set di credenziali senza scadenza, torna all&#39;interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Query]. Quindi, selezionare la scheda **[!UICONTROL Credenziali]** seguita da **[!UICONTROL Genera credenziali]**.

![Dashboard delle query con la scheda Credenziali e l&#39;opzione Genera credenziali evidenziate.](../images/ui/credentials/generate-credentials.png)

Viene visualizzata una finestra di dialogo che consente di generare le credenziali. Per creare credenziali senza scadenza, è necessario fornire i dettagli seguenti:

- **[!UICONTROL Nome]**: nome delle credenziali che si stanno generando.
- **[!UICONTROL Descrizione]**: (facoltativo) una descrizione per le credenziali che si stanno generando.
- **[!UICONTROL Assegnato a]**: l&#39;utente a cui verranno assegnate le credenziali. Questo valore deve essere l’indirizzo e-mail dell’utente che sta creando le credenziali.
- **[!UICONTROL Password]** (Facoltativo) Password facoltativa per le credenziali. Se la password non è impostata, Adobe genererà automaticamente una password.

Dopo aver fornito tutti i dettagli richiesti, selezionare **[!UICONTROL Genera credenziali]** per generare le credenziali.

![La finestra di dialogo Genera credenziali è evidenziata.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Quando è selezionata l&#39;opzione **[!UICONTROL Genera credenziali]**, nel computer locale viene scaricato un file JSON di configurazione. Poiché Adobe **non** registra le credenziali generate, è necessario archiviare in modo sicuro il file scaricato e conservare un record delle credenziali.
>
>Inoltre, se le credenziali non vengono utilizzate per 90 giorni, verranno eliminate.

Il file JSON di configurazione contiene informazioni come il nome dell’account tecnico, l’ID dell’account tecnico e le credenziali. Viene fornito nel seguente formato.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Dopo aver salvato le credenziali generate, seleziona **[!UICONTROL Chiudi]**. È ora disponibile un elenco di tutte le credenziali senza scadenza.

![Scheda Credenziali del dashboard delle query con la sezione Credenziali senza scadenza evidenziata.](../images/ui/credentials/list-credentials.png)

È possibile modificare o eliminare le credenziali senza scadenza. Per modificare una credenziale senza scadenza, selezionare l&#39;icona della matita (![Un&#39;icona della matita.](../images/ui/credentials/edit-icon.png)). Per eliminare una credenziale senza scadenza, selezionare l&#39;icona Elimina (![Icona Cestino.](../images/ui/credentials/delete-icon.png)).

Quando si modifica una credenziale senza scadenza, viene visualizzata una finestra modale. Puoi fornire i seguenti dettagli da aggiornare:

- **[!UICONTROL Nome]**: nome delle credenziali che si stanno generando.
- **[!UICONTROL Descrizione]**: (facoltativo) una descrizione per le credenziali che si stanno generando.
- **[!UICONTROL Assegnato a]**: l&#39;utente a cui verranno assegnate le credenziali. Questo valore deve essere l’indirizzo e-mail dell’utente che sta creando le credenziali.

![Finestra di dialogo Aggiorna account.](../images/ui/credentials/update-credentials.png)

Dopo aver fornito tutti i dettagli richiesti, seleziona **[!UICONTROL Aggiorna account]** per completare l&#39;aggiornamento delle credenziali.

## Utilizzare le credenziali per connettersi ai client esterni {#use-credential-to-connect}

Puoi utilizzare le credenziali in scadenza o non in scadenza per connetterti con client esterni, ad esempio Aqua Data Studio, Looker o Power BI. Il metodo di input per queste credenziali varia a seconda del client esterno. Per istruzioni specifiche sull’utilizzo di queste credenziali, consulta la documentazione del client esterno.

L’immagine indica la posizione di ciascun parametro trovato nell’interfaccia utente, ad eccezione della password delle credenziali senza scadenza. Anche se le credenziali senza scadenza vengono fornite dai relativi file di configurazione JSON, puoi visualizzare le credenziali in scadenza nella scheda **Credenziali** nell&#39;interfaccia utente.

![Scheda Credenziali dell&#39;area di lavoro query con la sezione Credenziali in scadenza evidenziata.](../images/ui/credentials/expiring-credentials.png)

La tabella seguente illustra i parametri normalmente necessari per la connessione ai client esterni.

>[!NOTE]
>
>Quando ci si connette a un host utilizzando credenziali senza scadenza, è comunque necessario utilizzare tutti i parametri elencati nella sezione [!UICONTROL EXPIRING CREDENTIALS] ad eccezione della password e del nome utente.
>Il formato per l&#39;immissione del nome utente e della password utilizza valori separati da due punti come mostrato in questo esempio `username:{your_username}` e `password:{password_string}`.

| Parametro | Descrizione | Esempio |
|---|---|---|
| **Server/Host** | Il nome del server/host a cui ti stai connettendo. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza e assume la forma di `server.adobe.io`. Il valore si trova in **[!UICONTROL Host]** nella sezione [!UICONTROL EXPIRING CREDENTIALS].</ul></li> | `acme.platform.adobe.io` |
| **Porta** | Porta del server/host a cui ci si sta connettendo. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza e si trova in **[!UICONTROL Porta]** nella sezione [!UICONTROL CREDENZIALI IN SCADENZA].</ul></li> | `80` |
| **Database** | Il database a cui ci si connette. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza e si trova in **[!UICONTROL Database]** nella sezione [!UICONTROL EXPIRING CREDENTIALS]. </ul></li> | `prod:all` |
| **Nome utente** | Nome utente dell&#39;utente che si connette al client esterno. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza. Deve essere una stringa alfanumerica prima di `@AdobeOrg`. Questo valore si trova in **[!UICONTROL Nome utente]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Password** | Password dell&#39;utente che si connette al client esterno. <ul><li>Se utilizzi credenziali in scadenza, puoi trovarle nella sezione **[!UICONTROL Password]** all&#39;interno della sezione [!UICONTROL EXPIRING CREDENTIALS].</li><li>Se utilizzi credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati di technicalAccountID e alle credenziali prese dal file JSON di configurazione. Il valore della password assume la forma: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Una password delle credenziali in scadenza supera un migliaio di caratteri alfanumerici. Non verrà fornito alcun esempio.</li><li>La password delle credenziali senza scadenza è la seguente:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi

Ora che hai compreso il funzionamento sia delle credenziali in scadenza che di quelle non in scadenza, puoi utilizzare queste credenziali per connettersi ai client esterni. Per ulteriori informazioni dettagliate sui client esterni, leggere la [guida alla connessione dei client a Query Service](../clients/overview.md).
