---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;editor query;editor query;editor query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida all’interfaccia utente del servizio query
topic-legacy: guide
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare query eseguite in precedenza e accedere alle query salvate dagli utenti all’interno dell’organizzazione IMS.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 696db8081ab8225d79cd468b7435770d407d3e3d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# Guida alle credenziali

Adobe Experience Platform Query Service consente di connettersi con client esterni. È possibile connettersi a questi client esterni utilizzando credenziali in scadenza o credenziali in scadenza.

## Credenziali in scadenza

È possibile utilizzare le credenziali in scadenza per configurare rapidamente una connessione a un client esterno.

![](../images/ui/credentials/expiring-credentials.png)

La sezione **[!UICONTROL Credenziali in scadenza]** fornisce le seguenti informazioni:

- **[!UICONTROL Host]**: Nome dell&#39;host a cui ti connetterai. Per la connessione al servizio query, verrà incluso il nome dell’organizzazione IMS attualmente in uso.
- **[!UICONTROL Porta]**: Numero di porta dell&#39;host a cui ci si connette.
- **[!UICONTROL Database]**: Nome del database a cui ci si connette.
- **[!UICONTROL Nome utente]**: Nome utente che verrà utilizzato per connettersi al servizio query.
- **[!UICONTROL Password]**: Password da utilizzare per la connessione al servizio query.
- **[!UICONTROL Comando]** PSQL: Comando che ha inserito automaticamente tutte le informazioni pertinenti per la connessione a Query Service tramite PSQL nella riga di comando.
- **[!UICONTROL Scade]**: Data di scadenza delle credenziali in scadenza. Le credenziali scadono 24 ore dopo la generazione.

## Credenziali non in scadenza

È possibile utilizzare le credenziali non in scadenza per impostare una connessione più permanente a un client esterno.

### Prerequisiti

Prima di poter generare credenziali non in scadenza, è necessario completare i seguenti passaggi in Adobe Admin Console:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/) e seleziona l&#39;organizzazione pertinente dalla barra di navigazione superiore.
2. [Seleziona un profilo di prodotto.](../../access-control/ui/browse.md)
3. [Configura sia le  **** sandbox che le autorizzazioni  **Manage Query Service** ](../../access-control/ui/permissions.md) Integration per il profilo di prodotto.
4. [Aggiungi un nuovo utente a un ](../../access-control/ui/users.md) profilo di prodotto per ottenere le autorizzazioni configurate.
5. [Aggiungi l’utente come ](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) amministratore del profilo di prodotto per consentire la creazione di un account per qualsiasi profilo di prodotto attivo.
6. [Aggiungi l’utente come ](https://helpx.adobe.com/enterprise/using/manage-developers.html) sviluppatore del profilo di prodotto per creare un’integrazione.

Per ulteriori informazioni su come assegnare le autorizzazioni, consulta la documentazione sul [controllo accessi](../../access-control/home.md).

Tutte le autorizzazioni necessarie sono ora configurate in Adobe Developer Console in modo che l’utente possa utilizzare la funzione delle credenziali in scadenza.

### Genera credenziali

Per creare un set di credenziali non in scadenza, torna all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Query]. Quindi, selezionare la scheda **[!UICONTROL Credenziali]** seguita da **[!UICONTROL Genera credenziali]**.

![](../images/ui/credentials/generate-credentials.png)

Viene visualizzata una finestra di dialogo che consente di generare le credenziali. Per creare credenziali non in scadenza, è necessario fornire i seguenti dettagli:

- **[!UICONTROL Nome]**: Nome delle credenziali che si sta generando.
- **[!UICONTROL Descrizione]**: (Facoltativo) Una descrizione delle credenziali che stai generando.
- **[!UICONTROL Assegnato a]**: Utente a cui verranno assegnate le credenziali. Questo valore deve essere l&#39;indirizzo e-mail dell&#39;utente che sta creando le credenziali.
- **[!UICONTROL Password]**  (opzionale) Una password opzionale per le tue credenziali. Se la password non è impostata, Adobe genererà automaticamente una password.

Dopo aver fornito tutti i dettagli richiesti, seleziona **[!UICONTROL Genera credenziali]** per generare le credenziali.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Una volta selezionato il pulsante **[!UICONTROL Genera credenziali]**, viene scaricato un file JSON di configurazione nel computer locale. Poiché in Adobe **non** vengono registrate le credenziali generate, è necessario memorizzare in modo sicuro il file scaricato e conservare un record delle credenziali.
>
>Inoltre, se le credenziali non vengono utilizzate per 90 giorni, verranno rimosse.

Il file JSON di configurazione contiene informazioni quali il nome dell’account tecnico, l’ID account tecnico e le credenziali. Viene fornito nel seguente formato.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Dopo aver salvato le credenziali generate, seleziona **[!UICONTROL Chiudi]**. È ora possibile visualizzare un elenco di tutte le credenziali non in scadenza.

![](../images/ui/credentials/list-credentials.png)

È possibile modificare o eliminare le credenziali non in scadenza. Per modificare una credenziale non in scadenza, seleziona l’icona a forma di matita (![](../images/ui/credentials/edit-icon.png)). Per eliminare una credenziale non in scadenza, seleziona l’icona Elimina (![](../images/ui/credentials/delete-icon.png)).

Quando si modifica una credenziale non in scadenza, viene visualizzato un modale. Puoi fornire i seguenti dettagli da aggiornare:

- **[!UICONTROL Nome]**: Nome delle credenziali che si sta generando.
- **[!UICONTROL Descrizione]**: (Facoltativo) Una descrizione delle credenziali che stai generando.
- **[!UICONTROL Assegnato a]**: Utente a cui verranno assegnate le credenziali. Questo valore deve essere l&#39;indirizzo e-mail dell&#39;utente che sta creando le credenziali.

![](../images/ui/credentials/update-credentials.png)

Dopo aver fornito tutti i dettagli richiesti, seleziona **[!UICONTROL Aggiorna account]** per completare l&#39;aggiornamento delle tue credenziali.

## Utilizzo delle credenziali per la connessione a client esterni

È possibile utilizzare le credenziali in scadenza o non in scadenza per connettersi con client esterni, ad esempio Aqua Data Studio, Looker o Power BI. Il metodo di input per queste credenziali varia a seconda del client esterno. Per istruzioni specifiche sull&#39;utilizzo di queste credenziali, consulta la documentazione del client esterno .

L’immagine indica la posizione di ogni parametro trovato nell’interfaccia utente, ad eccezione della password delle credenziali in scadenza. Le credenziali in scadenza vengono fornite dai relativi file di configurazione JSON, ma puoi visualizzarle nella scheda **Credenziali** dell’interfaccia utente.

![](../images/ui/credentials/expiring-credentials.png)

La tabella seguente delinea i parametri generalmente necessari per la connessione a client esterni.

>[!NOTE]
>
>Quando ci si connette a un host utilizzando credenziali non in scadenza, è comunque necessario utilizzare tutti i parametri elencati nella sezione [!UICONTROL EXPIRING CREDENTIALS] ad eccezione della password e del nome utente.

| Parametro | Descrizione |
|---|---|
| Server/Host | Il nome del server/host a cui ti connetti. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle non in scadenza e si presenta sotto forma di `server.adobe.io`. Il valore si trova in **[!UICONTROL Host]** nella sezione [!UICONTROL CREDENZIALI DI SCADENZA].</ul></li> |
| Porta | La porta del server/host a cui ti stai connettendo. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle non in scadenza e si trova in **[!UICONTROL Porta]** nella sezione [!UICONTROL CREDENZIALI IN SCADENZA] . Un valore di esempio per la porta è `80`.</ul></li> |
| Database | Database a cui ci si connette. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle non in scadenza e si trova in **[!UICONTROL Database]** nella sezione [!UICONTROL CREDENZIALI IN SCADENZA] . Un valore di esempio per il database è `prod:all`.</ul></li> |
| Nome utente | Nome utente per l’utente che si connette al client esterno. <ul><li>Se utilizzi credenziali in scadenza, si tratta di una stringa alfanumerica precedente a `@AdobeOrg`. Questo valore si trova in **[!UICONTROL Nome utente]**.</li><li>Se utilizzi credenziali non in scadenza, questa è una stringa di tua scelta anche se **non può** essere la stessa del valore `technicalAccountID` trovato nel file JSON di configurazione.</li></ul> |
| Password | Password per l&#39;utente che si connette al client esterno. <ul><li>Se utilizzi credenziali in scadenza, puoi trovarlo in **[!UICONTROL Password]** all&#39;interno della sezione [!UICONTROL SCADENZIALI].</li><li>Se utilizzi credenziali non in scadenza, questo valore è costituito dagli argomenti concatenati di technicalAccountID e dalla credenziale prelevata dal file JSON di configurazione. Il valore della password assume la forma di: `{technicalAccountId}:{credential}`.</li></ul> |

## Passaggi successivi

Ora che si capisce come funzionano sia le credenziali in scadenza che quelle in scadenza, è possibile utilizzare queste credenziali per connettersi a client esterni. Per ulteriori informazioni dettagliate sui client esterni, leggere la [guida alla connessione dei client a Query Service](../clients/overview.md).
