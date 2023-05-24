---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;editor query;editor query;editor query;
solution: Experience Platform
title: Guida alle credenziali di Query Service
description: Adobe Experience Platform Query Service fornisce un’interfaccia utente che può essere utilizzata per scrivere ed eseguire query, visualizzare le query eseguite in precedenza e accedere a quelle salvate dagli utenti della tua organizzazione.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 2%

---

# Guida alle credenziali

Adobe Experience Platform Query Service consente di connettersi con client esterni. È possibile connettersi a questi client esterni utilizzando credenziali in scadenza o credenziali senza scadenza.

## Credenziali in scadenza {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Modalità SSL del client"
>abstract="La modalità SSL deve essere abilitata nei client connessi a Query Service. Assicurati che la modalità SSL sia impostata su “Richiesta”."

È possibile utilizzare le credenziali in scadenza per impostare rapidamente una connessione a un client esterno.

![La scheda Credenziali del dashboard Query con la sezione Credenziali in scadenza evidenziata.](../images/ui/credentials/expiring-credentials.png)

Il **[!UICONTROL Credenziali in scadenza]** La sezione fornisce le seguenti informazioni:

- **[!UICONTROL Host]**: nome dell’host a cui connettere il client. Incorpora il nome dell’organizzazione, come visualizzato nella barra multifunzione superiore dell’interfaccia utente di Platform.
- **[!UICONTROL Porta]**: numero di porta dell’host a cui connettersi.
- **[!UICONTROL Database]**: nome del database a cui connettere un client.
- **[!UICONTROL Nome utente]**: nome utente utilizzato per connettersi a Query Service.
- **[!UICONTROL Password]**: password utilizzata per la connessione a Query Service. Le password nell’interfaccia utente sono state sottoposte a hashing per motivi di sicurezza. Seleziona l’icona Copia (![Icona Copia.](../images/ui/credentials/copy-icon.png)) per copiare negli Appunti le credenziali complete senza hash.
- **[!UICONTROL comando PSQL]**: comando che ha inserito automaticamente tutte le informazioni rilevanti per la connessione a Query Service tramite PSQL nella riga di comando.
- **[!UICONTROL Scade]**: data e ora di scadenza delle credenziali. La durata di validità predefinita del token è di 24 ore, ma può essere modificata nelle impostazioni avanzate dell’Admin Console.

>[!TIP]
>
>Per modificare la durata della sessione per la connessione delle credenziali in scadenza a Query Service, passa a [Admin Console](https://adminconsole.adobe.com/) e selezionare le seguenti opzioni sullo schermo: **Impostazioni** > **Privacy e sicurezza** > **Impostazioni di autenticazione** > **Impostazioni avanzate** > **Durata massima della sessione**.
>
>![La scheda delle impostazioni di Admin Console con Privacy e sicurezza, Impostazioni autenticazione e Durata massima sessione evidenziate.](../images/ui/credentials/max-session-life.png)
>
>Consulta la documentazione di Adobe per ulteriori informazioni sulla [Impostazioni avanzate](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) offerte da Admin Console.

## Credenziali senza scadenza {#non-expiring-credentials}

È possibile utilizzare credenziali senza scadenza per impostare una connessione più permanente a un client esterno.

### Prerequisiti

Prima di poter generare credenziali senza scadenza, è necessario completare i seguenti passaggi in Adobe Admin Console:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com/) e seleziona l’organizzazione appropriata dalla barra di navigazione superiore.
2. [Seleziona un profilo di prodotto.](../../access-control/ui/browse.md)
3. [Configura entrambi **Sandbox** e **Gestire l’integrazione di Query Service** autorizzazioni](../../access-control/ui/permissions.md) per il profilo di prodotto.
4. [Aggiungere un nuovo utente a un profilo di prodotto](../../access-control/ui/users.md) in modo che possano disporre delle autorizzazioni configurate.
5. [Aggiungere l’utente come amministratore del profilo di prodotto](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) per consentire la creazione di un account per qualsiasi profilo di prodotto attivo.
6. [Aggiungere l’utente come sviluppatore del profilo di prodotto](https://helpx.adobe.com/it/enterprise/using/manage-developers.html) per creare un’integrazione.

Per ulteriori informazioni su come assegnare le autorizzazioni, consulta la documentazione su [controllo degli accessi](../../access-control/home.md).

Tutte le autorizzazioni necessarie sono ora configurate nella console di Adobe Developer affinché l’utente possa utilizzare la funzione delle credenziali in scadenza.

### Genera credenziali

Per creare un set di credenziali senza scadenza, torna all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Query] Workspace. Quindi, seleziona la **[!UICONTROL Credenziali]** scheda seguita da **[!UICONTROL Genera credenziali]**.

![Il dashboard Query con la scheda Credenziali ed Evidenzia Genera credenziali.](../images/ui/credentials/generate-credentials.png)

Viene visualizzata una finestra di dialogo che consente di generare le credenziali. Per creare credenziali senza scadenza, è necessario fornire i dettagli seguenti:

- **[!UICONTROL Nome]**: nome delle credenziali che si stanno generando.
- **[!UICONTROL Descrizione]**: (facoltativo) descrizione delle credenziali che si stanno generando.
- **[!UICONTROL Assegnato a]**: utente a cui verranno assegnate le credenziali. Questo valore deve essere l’indirizzo e-mail dell’utente che sta creando le credenziali.
- **[!UICONTROL Password]** (Facoltativo) Password facoltativa per le credenziali. Se la password non è impostata, Adobe genererà automaticamente una password.

Dopo aver fornito tutti i dettagli richiesti, seleziona **[!UICONTROL Genera credenziali]** per generare le credenziali.

![Viene evidenziata la finestra di dialogo Genera credenziali.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Quando **[!UICONTROL Genera credenziali]** viene selezionato, nel computer locale viene scaricato un file JSON di configurazione. Poiché l’Adobe **non** registrare le credenziali generate, è necessario memorizzare in modo sicuro il file scaricato e tenere un record delle credenziali.
>
>Inoltre, se le credenziali non vengono utilizzate per 90 giorni, verranno eliminate.

Il file JSON di configurazione contiene informazioni come il nome dell’account tecnico, l’ID dell’account tecnico e le credenziali. Viene fornito nel seguente formato.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Dopo aver salvato le credenziali generate, seleziona **[!UICONTROL Chiudi]**. È ora disponibile un elenco di tutte le credenziali senza scadenza.

![La scheda Credenziali del dashboard delle query con la sezione Credenziali senza scadenza evidenziata.](../images/ui/credentials/list-credentials.png)

È possibile modificare o eliminare le credenziali senza scadenza. Per modificare una credenziale senza scadenza, seleziona l’icona a forma di matita (![Un’icona a forma di matita.](../images/ui/credentials/edit-icon.png)). Per eliminare una credenziale senza scadenza, selezionare l&#39;icona Elimina (![Icona cestino.](../images/ui/credentials/delete-icon.png)).

Quando si modifica una credenziale senza scadenza, viene visualizzata una finestra modale. Puoi fornire i seguenti dettagli da aggiornare:

- **[!UICONTROL Nome]**: nome delle credenziali che si stanno generando.
- **[!UICONTROL Descrizione]**: (facoltativo) descrizione delle credenziali che si stanno generando.
- **[!UICONTROL Assegnato a]**: utente a cui verranno assegnate le credenziali. Questo valore deve essere l’indirizzo e-mail dell’utente che sta creando le credenziali.

![Finestra di dialogo Aggiorna account.](../images/ui/credentials/update-credentials.png)

Dopo aver fornito tutti i dettagli richiesti, seleziona **[!UICONTROL Aggiorna account]** per completare l&#39;aggiornamento delle credenziali.

## Utilizzare le credenziali per connettersi ai client esterni {#use-credential-to-connect}

Puoi utilizzare le credenziali in scadenza o non in scadenza per connetterti con client esterni, ad esempio Aqua Data Studio, Looker o Power BI. Il metodo di input per queste credenziali varia a seconda del client esterno. Per istruzioni specifiche sull’utilizzo di queste credenziali, consulta la documentazione del client esterno.

L’immagine indica la posizione di ciascun parametro trovato nell’interfaccia utente, ad eccezione della password delle credenziali senza scadenza. Le credenziali senza scadenza vengono fornite dai relativi file di configurazione JSON, ma puoi visualizzare le credenziali in scadenza sotto **Credenziali** nell&#39;interfaccia utente.

![La scheda Credenziali dell’area di lavoro Query con la sezione Credenziali in scadenza evidenziata.](../images/ui/credentials/expiring-credentials.png)

La tabella seguente illustra i parametri normalmente necessari per la connessione ai client esterni.

>[!NOTE]
>
>Quando ci si connette a un host utilizzando credenziali senza scadenza, è comunque necessario utilizzare tutti i parametri elencati nella [!UICONTROL CREDENZIALI IN SCADENZA] ad eccezione della password e del nome utente.
>Il formato per l’immissione del nome utente e della password utilizza valori separati da due punti, come illustrato in questo esempio `username:{your_username}` e `password:{password_string}`.

| Parametro | Descrizione | Esempio |
|---|---|---|
| **Server/Host** | Il nome del server/host a cui ti stai connettendo. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza e assume la forma di `server.adobe.io`. Il valore si trova in **[!UICONTROL Host]** nel [!UICONTROL CREDENZIALI IN SCADENZA] sezione.</ul></li> | `acme.platform.adobe.io` |
| **Porta** | Porta del server/host a cui ci si sta connettendo. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza e si trova in **[!UICONTROL Porta]** nel [!UICONTROL CREDENZIALI IN SCADENZA] sezione.</ul></li> | `80` |
| **Database** | Il database a cui ci si connette. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza e si trova in **[!UICONTROL Database]** nel [!UICONTROL CREDENZIALI IN SCADENZA] sezione. </ul></li> | `prod:all` |
| **Nome utente** | Nome utente dell&#39;utente che si connette al client esterno. <ul><li>Questo valore viene utilizzato sia per le credenziali in scadenza che per quelle senza scadenza. Si presenta sotto forma di stringa alfanumerica prima del `@AdobeOrg`. Questo valore si trova in **[!UICONTROL Nome utente]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Password** | Password dell&#39;utente che si connette al client esterno. <ul><li>Se utilizzi le credenziali in scadenza, puoi trovarle in **[!UICONTROL Password]** all&#39;interno del [!UICONTROL CREDENZIALI IN SCADENZA] sezione.</li><li>Se utilizzi credenziali senza scadenza, questo valore corrisponde agli argomenti concatenati di technicalAccountID e alle credenziali prese dal file JSON di configurazione. Il valore della password è il seguente: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Una password delle credenziali in scadenza supera un migliaio di caratteri alfanumerici. Non verrà fornito alcun esempio.</li><li>La password delle credenziali senza scadenza è la seguente:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Passaggi successivi

Ora che hai compreso il funzionamento sia delle credenziali in scadenza che di quelle non in scadenza, puoi utilizzare queste credenziali per connettersi ai client esterni. Per ulteriori informazioni dettagliate sui client esterni, leggere [collegare i client alla guida di Query Service](../clients/overview.md).
