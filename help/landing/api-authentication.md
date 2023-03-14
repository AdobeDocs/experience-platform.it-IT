---
keywords: Experience Platform;home;argomenti popolari;Autenticazione;accesso
solution: Experience Platform
title: Autenticazione e accesso alle API Experience Platform
type: Tutorial
description: Questo documento spiega passo-passo come accedere a un account sviluppatore di Adobe Experience Platform per effettuare chiamate alle API di Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 9%

---


# Autenticazione e accesso alle API di Experience Platform

Questo documento spiega passo-passo come accedere a un account sviluppatore di Adobe Experience Platform per effettuare chiamate alle API di Experience Platform. Al termine di questa esercitazione, avrai generato le seguenti credenziali necessarie per tutte le chiamate API di Platform:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste alle API Adobe I/O devono essere autenticate e autorizzate utilizzando standard come OAuth e JSON Web Tokens (JWT). Un JWT viene utilizzato insieme a informazioni specifiche per il cliente per generare il token di accesso personale.

Questo tutorial illustra come raccogliere le credenziali necessarie per autenticare le chiamate API di Platform, come descritto nel seguente diagramma di flusso:

![](./images/api-authentication/authentication-flowchart.png)

## Prerequisiti

Per effettuare correttamente le chiamate alle API Experience Platform, è necessario disporre dei seguenti elementi:

* Organizzazione IMS con accesso a Adobe Experience Platform.
* Un amministratore di Admin Console che può aggiungerti come sviluppatore e utente per un profilo di prodotto.

Per completare questa esercitazione è necessario disporre anche di un Adobe ID. Se non disponi di un’Adobe ID, puoi crearne una seguendo questi passaggi:

1. Vai a [Console Adobe Developer](https://console.adobe.io).
2. Seleziona **[!UICONTROL Crea un nuovo account]**.
3. Completa il processo di registrazione.

## Ottieni l’accesso di sviluppatori e utenti, ad Experience Platform

Prima di creare integrazioni su Adobe Developer Console, il tuo account deve disporre di autorizzazioni per sviluppatori e utenti per un profilo di prodotto di Experience Platform in Adobe Admin Console.

### Accesso per sviluppatori

Contatta un [!DNL Admin Console] per aggiungerti come sviluppatore a un profilo di prodotto di Experience Platform utilizzando [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consulta la [!DNL Admin Console] documentazione per istruzioni specifiche su come [gestire l’accesso degli sviluppatori per i profili di prodotto](https://helpx.adobe.com/it/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Una volta che ti è stato assegnato come sviluppatore, puoi iniziare a creare integrazioni in [Console Adobe Developer](https://www.adobe.com/go/devs_console_ui). Queste integrazioni sono una pipeline da app e servizi esterni alle API Adobe.

### Ottenere l’accesso utente

Il tuo [!DNL Admin Console] l’amministratore deve anche aggiungerti come utente allo stesso profilo di prodotto. Consulta la guida su [gestione dei gruppi di utenti in [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) per ulteriori informazioni.

## Generare una chiave API, un ID organizzazione IMS e un segreto client {#api-ims-secret}

>[!NOTE]
>
>Se stai seguendo questo documento da [Guida all’API di Privacy Service](../privacy-service/api/getting-started.md), è ora possibile tornare a tale guida per generare le credenziali di accesso univoche per [!DNL Privacy Service].

Dopo aver ottenuto l’accesso a Platform da parte di sviluppatori e utenti tramite [!DNL Admin Console], il passaggio successivo consiste nel generare `{ORG_ID}` e `{API_KEY}` credenziali nella console Adobe Developer. Queste credenziali devono essere generate solo una volta e possono essere riutilizzate nelle chiamate API future di Platform.

### Aggiungere un Experience Platform a un progetto

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nel tutorial su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione della console Adobe Developer.

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Aggiungi API]** il **[!UICONTROL Panoramica del progetto]** schermo.

![](./images/api-authentication/add-api.png)

Viene visualizzata la schermata **[!UICONTROL Add an API]** (Aggiungi un’API). Seleziona l’icona del prodotto per Adobe Experience Platform, quindi scegli **[!UICONTROL API EXPERIENCE PLATFORM]** prima di selezionare **[!UICONTROL Successivo]**.

![](./images/api-authentication/platform-api.png)

Da qui, segui i passaggi descritti nel tutorial su [aggiunta di un’API a un progetto utilizzando un account di servizio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partire dal passaggio &quot;Configura API&quot;) per completare il processo.

>[!IMPORTANT]
>
>Ad un certo punto durante il processo collegato in precedenza, il browser scarica automaticamente una chiave privata e un certificato pubblico associato. Tieni presente dove viene memorizzata questa chiave privata nel computer, in quanto è necessaria in un passaggio successivo di questa esercitazione.

### Raccogli le credenziali

Una volta aggiunta l’API al progetto, la **[!UICONTROL API EXPERIENCE PLATFORM]** Nella pagina del progetto vengono visualizzate le seguenti credenziali necessarie in tutte le chiamate alle API Experience Platform:

* `{API_KEY}` ([!UICONTROL ID client])
* `{ORG_ID}` ([!UICONTROL ID organizzazione])

![](././images/api-authentication/api-key-ims-org.png)

Oltre alle credenziali di cui sopra, è necessario anche il **[!UICONTROL Segreto client]** per un passaggio futuro. Seleziona **[!UICONTROL Recupera segreto client]** per visualizzare il valore e copiarlo per un uso successivo.

![](././images/api-authentication/client-secret.png)

## Generare un token web JSON (JWT) {#jwt}

Il passaggio successivo consiste nel generare un token web JSON (JWT) in base alle credenziali del tuo account. Questo valore viene utilizzato per generare il `{ACCESS_TOKEN}` credenziali da utilizzare nelle chiamate API di Platform, che devono essere rigenerate ogni 24 ore.

>[!IMPORTANT]
>
>Ai fini di questa esercitazione, i passaggi seguenti descrivono come generare un JWT in Developer Console. Tuttavia, questo metodo di generazione dovrebbe essere utilizzato solo a fini di prova e valutazione.
>
>Per un uso regolare, il JWT deve essere generato automaticamente. Per ulteriori informazioni su come generare JWT a livello di programmazione, consulta [guida all’autenticazione dell’account di servizio](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) su Adobe Developer.

Seleziona **[!UICONTROL Account di servizio (JWT)]** nel menu di navigazione a sinistra, seleziona quindi **[!UICONTROL Genera JWT]**.

![](././images/api-authentication/generate-jwt.png)

Nella casella di testo fornita in **[!UICONTROL Generare un JWT personalizzato]**, incolla il contenuto della chiave privata generata in precedenza durante l’aggiunta dell’API Platform all’account del servizio. Quindi, seleziona **[!UICONTROL Genera token]**.

![](././images/api-authentication/paste-key.png)

La pagina viene aggiornata per mostrare il JWT generato, insieme a un comando cURL di esempio che consente di generare un token di accesso. Ai fini del presente tutorial, seleziona **[!UICONTROL Copia]** accanto a **[!UICONTROL JWT generato]** per copiare il token negli Appunti.

![](././images/api-authentication/copy-jwt.png)

## Generare un token di accesso

Dopo aver generato un JWT, puoi utilizzarlo in una chiamata API per generare il tuo `{ACCESS_TOKEN}`. A differenza dei valori per `{API_KEY}` e `{ORG_ID}`, per continuare a utilizzare le API di Platform, è necessario generare un nuovo token ogni 24 ore.

**Richiesta**

La richiesta seguente genera un nuovo `{ACCESS_TOKEN}` in base alle credenziali fornite nel payload. Questo endpoint accetta solo i dati del modulo come payload, pertanto deve ricevere un `Content-Type` intestazione di `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Proprietà | Descrizione |
| --- | --- |
| `{API_KEY}` | Il `{API_KEY}` ([!UICONTROL ID client]) recuperate in un [passaggio precedente](#api-ims-secret). |
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
| `token_type` | Tipo di token restituito. Per i token di accesso questo valore è sempre `bearer`. |
| `access_token` | Il valore generato `{ACCESS_TOKEN}`. Questo valore è preceduto dalla parola `Bearer`, è richiesto in quanto `Authentication` intestazione per tutte le chiamate API di Platform. |
| `expires_in` | Il numero di millisecondi rimanenti fino alla scadenza del token di accesso. Quando questo valore raggiunge 0, è necessario generare un nuovo token di accesso per continuare a utilizzare le API di Platform. |

## Verifica credenziali di accesso

Dopo aver raccolto tutte e tre le credenziali richieste, puoi provare ad effettuare la seguente chiamata API. Questa chiamata elenca tutti gli standard [!DNL Experience Data Model] (XDM) classi disponibili per la tua organizzazione.

**Richiesta**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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

## Utilizzare Postman per autenticare e testare le chiamate API

[Postman](https://www.postman.com/) è uno strumento popolare che consente agli sviluppatori di esplorare e testare le API RESTful. Questo [Post medio](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descrive come configurare Postman per eseguire automaticamente l’autenticazione JWT e utilizzarla per utilizzare le API di Platform.

## Passaggi successivi

Una volta letto questo documento, hai raccolto e verificato correttamente le credenziali di accesso per le API di Platform. Ora puoi seguire insieme agli esempi di chiamate API fornite in [documentazione](../landing/documentation/overview.md).

Oltre ai valori di autenticazione raccolti in questa esercitazione, molte API di Platform richiedono anche un `{SANDBOX_NAME}` da fornire come intestazione. Consulta la [panoramica sulle sandbox](../sandboxes/home.md) per ulteriori informazioni.