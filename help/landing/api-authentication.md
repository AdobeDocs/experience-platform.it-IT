---
solution: Experience Platform
title: Autenticazione e accesso alle API di Experience Platform
type: Tutorial
description: Questo documento spiega passo-passo come accedere a un account sviluppatore di Adobe Experience Platform per effettuare chiamate alle API di Experience Platform.
role: Developer
feature: API
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2508'
ht-degree: 3%

---


# Autenticazione e accesso alle API di Experience Platform

Questo documento fornisce un tutorial dettagliato per accedere a un account sviluppatore Adobe Experience Platform per effettuare chiamate alle API di Experience Platform. Al termine di questa esercitazione, avrai generato o raccolto le seguenti credenziali, necessarie come intestazioni in tutte le chiamate API di Experience Platform:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>Oltre alle tre credenziali di cui sopra, molte API di Experience Platform richiedono anche un `{SANDBOX_NAME}` valido da fornire come intestazione. Per ulteriori informazioni sulle sandbox e sulla documentazione dell&#39;[endpoint di gestione sandbox](/help/sandboxes/api/sandboxes.md#list), consulta la [panoramica sulle sandbox](../sandboxes/home.md).

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste alle API di Experience Platform devono essere autenticate e autorizzate utilizzando standard come OAuth.

Questo tutorial illustra come raccogliere le credenziali necessarie per autenticare le chiamate API di Experience Platform, come descritto nel diagramma di flusso seguente. È possibile raccogliere la maggior parte delle credenziali richieste nella configurazione iniziale una tantum. Il token di accesso, tuttavia, deve essere aggiornato ogni 24 ore.

![Requisiti del flusso di autenticazione per l&#39;installazione iniziale una tantum e per ogni sessione successiva.](./images/api-authentication/authentication-flowchart.png)

## Prerequisiti {#prerequisites}

Per effettuare correttamente le chiamate alle API di Experience Platform, è necessario disporre dei seguenti elementi:

* Organizzazione con accesso a Adobe Experience Platform.
* Un amministratore di Admin Console che può aggiungerti come sviluppatore e utente per un profilo di prodotto.
* Un amministratore di sistema Experience Platform che può concederti i controlli di accesso basati su attributi necessari per eseguire operazioni di lettura o scrittura su parti diverse di Experience Platform tramite API.

Per completare questa esercitazione è necessario disporre anche di un Adobe ID. Se non disponi di un’Adobe ID, puoi crearne una seguendo questi passaggi:

1. Vai a [Adobe Developer Console](https://console.adobe.io).
2. Selezionare **[!UICONTROL Crea un nuovo account]**.
3. Completa il processo di registrazione.

## Accesso utente e sviluppatore per Experience Platform {#gain-developer-user-access}

Prima di creare integrazioni su Adobe Developer Console, il tuo account deve disporre delle autorizzazioni per sviluppatori e utenti per un profilo di prodotto Experience Platform in Adobe Admin Console.

### Accesso per sviluppatori {#gain-developer-access}

Contatta un amministratore Admin Console della tua organizzazione per aggiungerti come sviluppatore a un profilo di prodotto Experience Platform. Per istruzioni specifiche su come [gestire l&#39;accesso degli sviluppatori per i profili di prodotto](https://helpx.adobe.com/it/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html), consulta la documentazione di Admin Console.

Una volta assegnati come sviluppatori, puoi iniziare a creare integrazioni in [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Queste integrazioni sono una pipeline da app e servizi esterni alle API di Adobe.

### Ottenere l’accesso utente {#gain-user-access}

L’amministratore di Admin Console deve anche aggiungere te come utente allo stesso profilo di prodotto. Con l’accesso utente, puoi visualizzare nell’interfaccia utente il risultato delle operazioni API eseguite.

Per ulteriori informazioni, consulta la guida sulla gestione dei gruppi di utenti in Admin Console[&#128279;](https://helpx.adobe.com/it/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html).

## Generare una chiave API (ID client) e un ID organizzazione {#generate-credentials}

>[!NOTE]
>
>Se stai seguendo questo documento dalla [guida API di Privacy Service](../privacy-service/api/getting-started.md), ora puoi tornare a tale guida per generare le credenziali di accesso univoche per [!DNL Privacy Service].

Dopo aver ottenuto l&#39;accesso utente e sviluppatore ad Experience Platform tramite Admin Console, il passaggio successivo consiste nel generare le credenziali di `{ORG_ID}` e `{API_KEY}` in Adobe Developer Console. Queste credenziali devono essere generate solo una volta e possono essere riutilizzate nelle chiamate API future di Experience Platform.

>[!TIP]
>
>Invece di passare a Developer Console, puoi ottenere tutte le credenziali di autenticazione necessarie per utilizzare le API di Experience Platform direttamente dalle pagine della documentazione di riferimento API. [Ulteriori informazioni](#get-credentials-functionality) sulla nuova funzionalità.

### Aggiungere Experience Platform a un progetto {#add-platform-to-project}

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nel tutorial su [creazione di un progetto vuoto](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) nella documentazione di Adobe Developer Console.

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Aggiungi API]** nella schermata **[!UICONTROL Panoramica progetto]**.

>[!TIP]
>
>Se disponi del provisioning per più organizzazioni, utilizza il selettore organizzazione nell’angolo superiore destro dell’interfaccia per assicurarti di essere nell’organizzazione necessaria.

![Schermata Developer Console con l&#39;opzione Aggiungi API evidenziata.](./images/api-authentication/add-api.png)

Viene visualizzata la schermata **[!UICONTROL Add an API]** (Aggiungi un’API). Seleziona l&#39;icona del prodotto per **[!UICONTROL Adobe Experience Platform]**, quindi scegli **[!UICONTROL Experience Platform API]** prima di selezionare **[!UICONTROL Next]**.

![Selezionare l&#39;API Experience Platform nella schermata Aggiungi un&#39;API.](./images/api-authentication/platform-api.png)

>[!TIP]
>
>Seleziona l&#39;opzione **[!UICONTROL Visualizza documenti]** per passare in una finestra del browser separata alla [documentazione di riferimento API di Experience Platform](https://developer.adobe.com/experience-platform-apis/) completa.

### Seleziona il tipo di autenticazione da server a server [!UICONTROL OAuth] {#select-oauth-server-to-server}

Quindi, seleziona il tipo di autenticazione **[!UICONTROL OAuth Server-to-Server]** per generare i token di accesso e accedere all&#39;API di Experience Platform. Assegna alle credenziali un nome significativo nel campo di testo **[!UICONTROL Nome credenziali]** prima di selezionare **[!UICONTROL Successivo]**.

>[!IMPORTANT]
>
>Il metodo **[!UICONTROL OAuth Server-to-Server]** è l&#39;unico metodo di generazione di token supportato per gli spostamenti in avanti. Il metodo **[!UICONTROL Service Account (JWT)]** precedentemente supportato è obsoleto e non può essere selezionato per nuove integrazioni. Anche se le integrazioni esistenti che utilizzano il metodo di autenticazione JWT continueranno a funzionare fino al 30 giugno 2025, Adobe consiglia vivamente di migrare le integrazioni esistenti al nuovo metodo [!UICONTROL OAuth Server-to-Server] prima di tale data. Ulteriori informazioni nella sezione [!BADGE Obsoleto]{type=negative}[Genera un token Web JSON (JWT)](#jwt).

![Selezionare il metodo di autenticazione server-to-server OAuth per l&#39;API Experience Platform.](./images/api-authentication/oauth-authentication-method.png)

### Selezionare i profili di prodotto per l’integrazione {#select-product-profiles}

Nella schermata **[!UICONTROL Configura API]**, seleziona **[!UICONTROL AEP-Default-All-Users]** insieme agli eventuali profili di prodotto aggiuntivi a cui desideri accedere.

>[!IMPORTANT]
>
>Per accedere a determinate funzioni di Experience Platform, è necessario disporre anche di un amministratore di sistema che conceda le autorizzazioni di controllo dell’accesso basate su attributi necessarie. Ulteriori informazioni nella sezione [Ottenere le autorizzazioni di controllo dell&#39;accesso basate su attributi necessarie](#get-abac-permissions).

![Seleziona i profili di prodotto per la tua integrazione.](./images/api-authentication/select-product-profiles.png)

Seleziona **[!UICONTROL Salva API configurata]** quando sei pronto.

Una descrizione dettagliata dei passaggi descritti in precedenza per impostare un’integrazione con l’API di Experience Platform è disponibile anche nel tutorial video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

### Raccogli le credenziali {#gather-credentials}

Una volta aggiunta l&#39;API al progetto, nella pagina **[!UICONTROL OAuth Server-to-Server]** per il progetto vengono visualizzate le credenziali seguenti, necessarie in tutte le chiamate alle API di Experience Platform:

![Informazioni sull&#39;integrazione dopo l&#39;aggiunta di un&#39;API in Developer Console.](./images/api-authentication/api-integration-information.png)

* `{API_KEY}` ([!UICONTROL ID client])
* `{ORG_ID}` ([!UICONTROL ID organizzazione])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## Generare un token di accesso {#generate-access-token}

Il passaggio successivo consiste nel generare una credenziale `{ACCESS_TOKEN}` da utilizzare nelle chiamate API di Experience Platform. A differenza dei valori per `{API_KEY}` e `{ORG_ID}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare le API di Experience Platform. Seleziona **[!UICONTROL Genera token di accesso]** che genera il token di accesso, come illustrato di seguito.

![Mostra come generare il token di accesso](././images/api-authentication/generate-access-token.png)

>[!TIP]
>
>Puoi inoltre utilizzare un ambiente e una raccolta Postman per generare i token di accesso. Per ulteriori informazioni, leggere la sezione relativa all&#39;utilizzo di [Postman per l&#39;autenticazione e il test delle chiamate API](#use-postman).

## Crea e recupera le credenziali di autenticazione direttamente nella documentazione di riferimento dell’API {#get-credentials-functionality}

A partire dalla versione di novembre 2024 di Experience Platform, è possibile ottenere le credenziali per utilizzare le API di Experience Platform direttamente dalle pagine di riferimento API, senza dover passare a [!UICONTROL Developer Console]. Visualizza l&#39;esempio seguente dalla [pagina Destinazioni dell&#39;API del servizio di flusso](https://developer.adobe.com/experience-platform-apis/references/destinations/).

![La funzionalità di recupero delle credenziali è evidenziata nella parte superiore di una pagina di riferimento API.](././images/api-authentication/get-credentials-highlighted.png)

Per ottenere le credenziali per chiamare le API Experience Platform, passa a una pagina di riferimento API Experience Platform e seleziona **[!UICONTROL Accedi]** nella parte superiore della pagina. Accedi con il tuo **[!UICONTROL account personale]** o **[!UICONTROL account aziendale o scolastico]**.

Dopo l&#39;accesso, selezionare **[!UICONTROL Crea nuova credenziale]** per creare un nuovo set di credenziali per accedere alle API di Experience Platform.

![Crea nuove credenziali per accedere alle API di Experience Platform.](././images/api-authentication/create-credentials.gif)

Quindi, utilizza il selettore a discesa per aprire la finestra delle credenziali, generare un token di accesso e ottenere la chiave API e l’ID organizzazione. Copia le credenziali nei blocchi [**[!UICONTROL Prova]**](/help/release-notes/2024/may-2024.md#interactive-api-documentation) nelle pagine di riferimento API per iniziare a lavorare con le API di Experience Platform.

![Utilizzare il selettore a discesa per visualizzare le credenziali e generare un token di accesso.](././images/api-authentication/view-copy-credentials.gif)

>[!TIP]
>
>Il blocco delle credenziali nella parte superiore della pagina rimane visualizzato quando navighi tra diverse pagine di endpoint nella documentazione di riferimento API di Experience Platform.

## [!BADGE Deprecato]{type=negativo} genera un token web JSON (JWT) {#jwt}

>[!WARNING]
>
>Il metodo JWT per generare i token di accesso è stato dichiarato obsoleto. Tutte le nuove integrazioni devono essere create utilizzando il metodo di autenticazione server-to-server [OAuth](#select-oauth-server-to-server). Per continuare a funzionare, Adobe richiede anche la migrazione delle integrazioni esistenti al metodo OAuth entro il 30 giugno 2025. Leggi la seguente documentazione importante:
> 
>* [Guida alla migrazione per le applicazioni da JWT a OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
>* [Guida all&#39;implementazione per applicazioni nuove e vecchie con OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
>* [Vantaggi dell&#39;utilizzo del metodo delle credenziali server-to-server OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ Visualizza informazioni obsolete

Il passaggio successivo consiste nel generare un token web JSON (JWT) in base alle credenziali del tuo account. Questo valore viene utilizzato per generare le credenziali `{ACCESS_TOKEN}` da utilizzare nelle chiamate API di Experience Platform, che devono essere rigenerate ogni 24 ore.

>[!IMPORTANT]
>
>Ai fini di questa esercitazione, i passaggi seguenti descrivono come generare un JWT in Developer Console. Tuttavia, questo metodo di generazione dovrebbe essere utilizzato solo a fini di prova e valutazione.
>
>Per un uso regolare, il JWT deve essere generato automaticamente. Per ulteriori informazioni su come generare JWT a livello di programmazione, consulta la [guida all&#39;autenticazione dell&#39;account di servizio](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) su Adobe Developer.

Seleziona **[!UICONTROL Account di servizio (JWT)]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Genera JWT]**.

![](././images/api-authentication/generate-jwt.png)

Nella casella di testo fornita in **[!UICONTROL Genera JWT personalizzato]**, incolla il contenuto della chiave privata generata in precedenza durante l&#39;aggiunta dell&#39;API Experience Platform all&#39;account del servizio. Quindi, seleziona **[!UICONTROL Genera token]**.

![](././images/api-authentication/paste-key.png)

La pagina viene aggiornata per mostrare il JWT generato, insieme a un comando cURL di esempio che consente di generare un token di accesso. Ai fini di questa esercitazione, seleziona **[!UICONTROL Copia]** accanto a **[!UICONTROL JWT generato]** per copiare il token negli Appunti.

![](././images/api-authentication/copy-jwt.png)

**Generare un token di accesso**

Dopo aver generato un JWT, puoi utilizzarlo in una chiamata API per generare il tuo `{ACCESS_TOKEN}`. A differenza dei valori per `{API_KEY}` e `{ORG_ID}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare le API di Experience Platform.

**Richiesta**

La richiesta seguente genera un nuovo `{ACCESS_TOKEN}` in base alle credenziali fornite nel payload. Questo endpoint accetta solo i dati del modulo come payload, pertanto deve ricevere un&#39;intestazione `Content-Type` di `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Proprietà | Descrizione |
| --- | --- |
| `{API_KEY}` | `{API_KEY}` ([!UICONTROL ID client]) recuperato in un [passaggio precedente](#api-ims-secret). |
| `{SECRET}` | Il segreto client recuperato in un [passaggio precedente](#api-ims-secret). |
| `{JWT}` | Il JWT generato in un [passaggio precedente](#jwt). |

>[!NOTE]
>
>Puoi utilizzare la stessa chiave API, lo stesso segreto client e lo stesso JWT per generare un nuovo token di accesso per ogni sessione. Questo consente di automatizzare la generazione dei token di accesso nelle applicazioni.

**Risposta**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Proprietà | Descrizione |
| --- | --- |
| `token_type` | Il tipo of token restituito. Per i token di accesso, questo valore è sempre `bearer`. |
| `access_token` | `{ACCESS_TOKEN}` generato. Questo valore, con prefisso `Bearer`, è obbligatorio come intestazione `Authentication` per tutte le chiamate API di Experience Platform. |
| `expires_in` | Il numero di millisecondi rimanenti fino alla scadenza del token di accesso. Quando questo valore raggiunge 0, è necessario generare un nuovo token di accesso per continuare a utilizzare le API di Experience Platform. |

+++

## Verifica credenziali di accesso {#test-credentials}

Dopo aver raccolto tutte e tre le credenziali richieste (token di accesso, chiave API e ID organizzazione), puoi provare ad effettuare la seguente chiamata API. Questa chiamata elenca tutte le classi standard [!DNL Experience Data Model] (XDM) disponibili per la tua organizzazione. Importa ed esegui la chiamata in [Postman](#use-postman).

>[!BEGINSHADEBOX]

**Richiesta**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
```

**Risposta**

Se la risposta è simile a quella mostrata di seguito, le credenziali sono valide e funzionanti. (La risposta è stata troncata per motivi di spazio).

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
>Anche se la chiamata precedente è sufficiente per testare le credenziali di accesso, non sarà possibile accedere a o modificare diverse risorse senza disporre delle autorizzazioni di controllo dell’accesso basate su attributi corretti. Ulteriori informazioni sono disponibili nella sezione **Ottenere le autorizzazioni di controllo dell&#39;accesso basate su attributi necessarie**.

## Ottenere le autorizzazioni di controllo dell&#39;accesso basate su attributi necessarie {#get-abac-permissions}

Per accedere a o modificare diverse risorse all’interno di Experience Platform, devi disporre delle autorizzazioni di controllo di accesso appropriate. Gli amministratori di sistema possono concederti le [autorizzazioni necessarie](/help/access-control/ui/permissions.md). Ulteriori informazioni nella sezione sulla gestione delle credenziali API [per un ruolo](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role).

Informazioni dettagliate su come un amministratore di sistema può concedere le autorizzazioni necessarie per accedere alle risorse di Experience Platform tramite l’API sono disponibili anche nel tutorial video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=159)

## Utilizzare Postman per autenticare e testare le chiamate API {#use-postman}

[Postman](https://www.postman.com/) è uno strumento popolare che consente agli sviluppatori di esplorare e testare le API RESTful. Puoi utilizzare le raccolte e gli ambienti Experience Platform Postman per velocizzare il tuo lavoro con le API Experience Platform. Ulteriori informazioni sull&#39;utilizzo di [Postman in Experience Platform](/help/landing/postman.md) e sulla guida introduttiva alle raccolte e agli ambienti.

Informazioni dettagliate sull’utilizzo di Postman con raccolte e ambienti Experience Platform sono disponibili anche nei tutorial video seguenti:

**Scarica e importa un ambiente Postman da utilizzare con le API di Experience Platform**

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=106)

**Utilizzare una raccolta Postman per generare token di accesso**

Scarica la [raccolta Postman di Identity Management Service](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) e guarda il video seguente per scoprire come generare i token di accesso.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)

**Scarica raccolte Postman API di Experience Platform e interagisce con le API**

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Experience Platform APIs.
-->

## Amministratori di sistema: concedere agli sviluppatori e al controllo dell’accesso API autorizzazioni Experience Platform {#grant-developer-and-api-access-control}

Prima di poter creare integrazioni su Adobe Developer Console, il tuo account deve disporre di autorizzazioni per sviluppatori e utenti per un profilo di prodotto Experience Platform.

>[!NOTE]
>
>Solo gli amministratori di sistema possono visualizzare e gestire le credenziali API in Autorizzazioni.

### Aggiungere sviluppatori al profilo di prodotto {#add-developers-to-product-profile}

Passa a [Admin Console](https://adminconsole.adobe.com/) e accedi con il tuo Adobe ID.

Seleziona **[!UICONTROL Prodotti]** dalla barra di navigazione, quindi seleziona **[!UICONTROL Adobe Experience Platform]** dall&#39;elenco dei prodotti.

![Pagina prodotti in Adobe Admin Console con il prodotto Adobe Experience Platform evidenziato.](././images/api-authentication/products.png)

Dalla scheda **[!UICONTROL Profili di prodotto]**, seleziona **[!UICONTROL AEP-Default-All-Users]**. In alternativa, utilizza la barra di ricerca per cercare il profilo di prodotto inserendo il nome.

![La pagina dei profili di prodotto con la barra di ricerca e il prodotto AEP-Default-All-Users evidenziato.](././images/api-authentication/select-product-profile.png)

Seleziona la scheda **[!UICONTROL Sviluppatori]**, quindi seleziona **[!UICONTROL Aggiungi sviluppatore]**.

![Viene visualizzata la scheda Sviluppatori con l&#39;opzione Aggiungi sviluppatori evidenziata,](././images/api-authentication/add-developer1.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Aggiungi sviluppatori]**. Immetti **[!UICONTROL Email o nome utente]** dello sviluppatore. [!UICONTROL Indirizzo e-mail o nome utente] valido visualizza i dettagli dello sviluppatore. Seleziona **[!UICONTROL Salva]**.

![La finestra di dialogo Aggiungi sviluppatori con le informazioni per gli sviluppatori è stata compilata ed è stata evidenziata l&#39;opzione Salva.](././images/api-authentication/add-developer-email.png)

Lo sviluppatore è stato aggiunto correttamente e viene visualizzato nella scheda **[!UICONTROL Sviluppatori]**.

![Nella scheda Sviluppatori viene visualizzato l&#39;elenco di tutti gli sviluppatori aggiunti con lo sviluppatore appena aggiunto evidenziato.](././images/api-authentication/developer-added.png)

### Assegnare le credenziali API a un ruolo

>[!NOTE]
>
>Solo un amministratore di sistema può assegnare le API ai ruoli nell’interfaccia utente di Experience Platform.

Per utilizzare ed eseguire operazioni sulle API di Experience Platform, un amministratore di sistema deve aggiungere le credenziali API oltre al set di autorizzazioni assegnato a un ruolo. Ulteriori informazioni nella sezione sulla gestione delle credenziali API [per un ruolo](../access-control/abac/ui/permissions.md#manage-api-credentials-for-a-role).

Una descrizione dettagliata dei passaggi descritti in precedenza per aggiungere sviluppatori ai profili di prodotto e assegnare API ai ruoli è disponibile anche nel tutorial video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3426407/?learn=on)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni sulle API di Experience Platform, consulta le risorse aggiuntive elencate di seguito

* [Autentica e accedi alla pagina dei video tutorial sulle API di Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=it)
* [Raccolta Postman del servizio Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) per la generazione dei token di accesso
* [Raccolte Postman API Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## Passaggi successivi {#next-steps}

Una volta letto questo documento, hai raccolto e verificato correttamente le credenziali di accesso per le API di Experience Platform. Ora puoi seguire insieme alle chiamate API di esempio fornite nella [documentazione](../landing/documentation/overview.md).

Oltre ai valori di autenticazione raccolti in questa esercitazione, molte API di Experience Platform richiedono anche un `{SANDBOX_NAME}` valido da fornire come intestazione. Per ulteriori informazioni, consulta la [panoramica delle sandbox](../sandboxes/home.md).
