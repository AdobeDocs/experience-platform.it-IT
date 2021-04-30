---
keywords: Experience Platform;home;argomenti popolari;autenticare;accedere
solution: Experience Platform
title: API di Experience Platform di autenticazione e accesso
topic-legacy: tutorial
type: Tutorial
description: Questo documento spiega passo-passo come accedere a un account sviluppatore di Adobe Experience Platform per effettuare chiamate alle API di Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 6%

---


# Autenticazione e accesso alle API di Experience Platform

Questo documento spiega passo-passo come accedere a un account sviluppatore di Adobe Experience Platform per effettuare chiamate alle API di Experience Platform. Al termine dell’esercitazione, avrai generato le seguenti credenziali richieste per tutte le chiamate API di Platform:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste alle API di Adobe I/O devono essere autenticate e autorizzate utilizzando standard come OAuth e JSON Web Token (JWT). Per generare il token di accesso personale, viene utilizzato un JWT con informazioni specifiche per il cliente.

Questa esercitazione illustra come raccogliere le credenziali richieste per autenticare le chiamate API di Platform, come descritto nel seguente diagramma di flusso:

![](./images/api-authentication/authentication-flowchart.png)

## Prerequisiti

Per effettuare correttamente le chiamate alle API di Experience Platform, devi disporre dei seguenti elementi:

* Organizzazione IMS con accesso a Adobe Experience Platform.
* Un amministratore di Admin Console in grado di aggiungerti come sviluppatore e come utente per un profilo di prodotto.

Devi anche disporre di un Adobe ID per completare questa esercitazione. Se non disponi di un Adobe ID, puoi crearne uno seguendo questi passaggi:

1. Vai a [Adobe Developer Console](https://console.adobe.io).
2. Seleziona **[!UICONTROL Create a new account]**.
3. Completa il processo di registrazione.

## Acquisisci ad Experience Platform l’accesso degli sviluppatori e degli utenti

Prima di creare integrazioni su Adobe Developer Console, il tuo account deve disporre delle autorizzazioni per sviluppatori e utenti per un profilo di prodotto di Experience Platform in Adobe Admin Console.

### Accesso per sviluppatori

Contatta un amministratore [!DNL Admin Console] della tua organizzazione per aggiungerti come sviluppatore a un profilo di prodotto di Experience Platform utilizzando [[!DNL Admin Console]](https://adminconsole.adobe.com/). Per istruzioni specifiche su come [gestire l&#39;accesso degli sviluppatori per i profili di prodotto](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html), consulta la documentazione [!DNL Admin Console] .

Una volta assegnato come sviluppatore, puoi iniziare a creare integrazioni in [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Queste integrazioni sono una pipeline da applicazioni e servizi esterni alle API di Adobe.

### Accesso utente

L’amministratore di [!DNL Admin Console] deve anche aggiungerti come utente allo stesso profilo di prodotto. Per ulteriori informazioni, consulta la guida sulla [gestione dei gruppi di utenti in [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) .

## Generare una chiave API, un ID organizzazione IMS e un segreto client {#api-ims-secret}

>[!NOTE]
>
>Se segui questo documento dalla [guida per sviluppatori di Privacy Service](../privacy-service/api/getting-started.md), ora puoi tornare a tale guida per generare le credenziali di accesso univoche per [!DNL Privacy Service].

Dopo aver ricevuto dallo sviluppatore e dall’utente l’accesso a Platform tramite [!DNL Admin Console], il passaggio successivo consiste nel generare le credenziali `{IMS_ORG}` e `{API_KEY}` in Adobe Developer Console. Queste credenziali devono essere generate una sola volta e possono essere riutilizzate nelle chiamate API future di Platform.

### Aggiungere un Experience Platform a un progetto

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nell’esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione di Adobe Developer Console.

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Add API]** nella schermata **[!UICONTROL Project Overview]** .

![](./images/api-authentication/add-api.png)

Viene visualizzata la schermata **[!UICONTROL Add an API]**. Seleziona l’icona del prodotto per Adobe Experience Platform, quindi scegli **[!UICONTROL Experience Platform API]** prima di selezionare **[!UICONTROL Next]**.

![](./images/api-authentication/platform-api.png)

Da qui, segui i passaggi descritti nell’esercitazione sull’ [aggiunta di un’API a un progetto utilizzando un account di servizio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partire dal passaggio &quot;Configura API&quot;) per completare il processo.

>[!IMPORTANT]
>
>A un certo punto del processo collegato qui sopra, il browser scarica automaticamente una chiave privata e un certificato pubblico associato. Nota dove questa chiave privata è memorizzata nel computer, in quanto è necessaria in un passaggio successivo in questa esercitazione.

### Raccogli credenziali

Una volta aggiunta l’API al progetto, la pagina **[!UICONTROL Experience Platform API]** del progetto visualizza le seguenti credenziali richieste in tutte le chiamate alle API di Experience Platform:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{IMS_ORG}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

Oltre alle credenziali di cui sopra, è necessario anche il **[!UICONTROL Client Secret]** generato per un passaggio futuro. Selezionare **[!UICONTROL Retrieve client secret]** per visualizzare il valore, quindi copiarlo per un uso successivo.

![](././images/api-authentication/client-secret.png)

## Generare un token web JSON (JWT) {#jwt}

Il passaggio successivo consiste nel generare un JSON Web Token (JWT) basato sulle credenziali del tuo account. Questo valore viene utilizzato per generare le credenziali `{ACCESS_TOKEN}` da utilizzare nelle chiamate API di Platform, che devono essere rigenerate ogni 24 ore.

Seleziona **[!UICONTROL Service Account (JWT)]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Generate JWT]**.

![](././images/api-authentication/generate-jwt.png)

Nella casella di testo fornita in **[!UICONTROL Generate custom JWT]**, incolla il contenuto della chiave privata che hai generato in precedenza quando aggiungi l’API Platform al tuo account di servizio. Quindi, seleziona **[!UICONTROL Generate Token]**.

![](././images/api-authentication/paste-key.png)

La pagina viene aggiornata per mostrare il JWT generato, insieme a un comando cURL di esempio che consente di generare un token di accesso. Ai fini di questa esercitazione, seleziona **[!UICONTROL Copy]** accanto a **[!UICONTROL Generated JWT]** per copiare il token negli Appunti.

![](././images/api-authentication/copy-jwt.png)

## Generare un token di accesso

Dopo aver generato un JWT, puoi utilizzarlo in una chiamata API per generare il tuo `{ACCESS_TOKEN}`. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, per continuare a utilizzare le API di Platform è necessario generare un nuovo token ogni 24 ore.

**Richiesta**

La seguente richiesta genera un nuovo `{ACCESS_TOKEN}` in base alle credenziali fornite nel payload. Questo endpoint accetta solo i dati del modulo come payload, pertanto deve essere fornito un&#39;intestazione `Content-Type` di `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Proprietà | Descrizione |
| --- | --- |
| `{API_KEY}` | Il `{API_KEY}` ([!UICONTROL Client ID]) recuperato in un [passaggio precedente](#api-ims-secret). |
| `{SECRET}` | Il segreto client recuperato in un [passaggio precedente](#api-ims-secret). |
| `{JWT}` | JWT generato in un [passaggio precedente](#jwt). |

>[!NOTE]
>
>Puoi utilizzare la stessa chiave API, lo stesso segreto client e JWT per generare un nuovo token di accesso per ogni sessione. Questo consente di automatizzare la generazione di token di accesso nelle applicazioni.

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
| `token_type` | Tipo di token restituito. Per i token di accesso, questo valore è sempre `bearer`. |
| `access_token` | Il `{ACCESS_TOKEN}` generato. Questo valore, con il prefisso `Bearer`, è obbligatorio come intestazione `Authentication` per tutte le chiamate API di Platform. |
| `expires_in` | Il numero di millisecondi che rimangono fino alla scadenza del token di accesso. Una volta che questo valore raggiunge 0, è necessario generare un nuovo token di accesso per continuare a utilizzare le API di Platform. |

## Verificare le credenziali di accesso

Dopo aver raccolto tutte e tre le credenziali richieste, puoi provare a effettuare la seguente chiamata API. Questa chiamata elenca tutte le classi [!DNL Experience Data Model] standard (XDM) disponibili per la tua organizzazione.

**Richiesta**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Risposta**

Se la risposta è simile a quella mostrata di seguito, le credenziali sono valide e funzionanti. Questa risposta è stata troncata per lo spazio.

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

## Utilizzare Postman per autenticare e testare le chiamate API

[](https://www.postman.com/) Postmanis uno strumento popolare che consente agli sviluppatori di esplorare e testare le API RESTful. Questo [post medio](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descrive come impostare Postman per eseguire automaticamente l&#39;autenticazione JWT e utilizzarlo per utilizzare le API di Platform.

## Passaggi successivi

Leggendo questo documento, hai raccolto e verificato con successo le credenziali di accesso per le API di Platform. Ora puoi seguire l&#39;esempio di chiamate API fornite nella [documentazione](../landing/documentation/overview.md).

Oltre ai valori di autenticazione raccolti in questa esercitazione, molte API di Platform richiedono anche un `{SANDBOX_NAME}` valido da fornire come intestazione. Per ulteriori informazioni, consulta la [panoramica sulle sandbox](../sandboxes/home.md) .