---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: API Authenticate e Access Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: e1ba476fffc164b78decd7168192714993c791bc
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 1%

---


# Autenticazione e accesso alle API della piattaforma Experience

Questo documento fornisce un&#39;esercitazione passo-passo per ottenere l&#39;accesso a un account sviluppatore Adobe Experience Platform per effettuare chiamate alle API della piattaforma Experience.

## Autenticazione per effettuare chiamate API

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste alle API di I/O Adobe devono essere autenticate e autorizzate utilizzando standard quali OAuth e JSON Web Token (JWT). Il JWT viene quindi utilizzato insieme alle informazioni specifiche per il cliente per generare il token di accesso personale.

Questa esercitazione descrive i passaggi dell&#39;autenticazione mediante la creazione di un token di accesso delineato nel seguente diagramma di flusso:
![](images/authentication/authentication-flowchart.png)

## Prerequisiti

Per effettuare correttamente le chiamate alle API della piattaforma Experience, è necessario quanto segue:

* Un&#39;organizzazione IMS con accesso ad Adobe Experience Platform
* Un account Adobe ID registrato
* Un amministratore di Admin Console per aggiungere te come **sviluppatore** e un **utente** per un prodotto.

Le sezioni seguenti descrivono i passaggi necessari per creare un Adobe ID e diventare sviluppatore e utente per un&#39;organizzazione.

### Creare un Adobe ID

Se non disponete di un ID Adobe, potete crearne uno seguendo la procedura seguente:

1. Vai ad [Adobe Developer Console](https://console.adobe.io)
2. Fate clic su **Crea un nuovo account**
3. Completare il processo di registrazione

## Diventa sviluppatore e utente per la piattaforma Experience per un&#39;organizzazione

Prima di creare integrazioni sull&#39;I/O Adobe, il vostro account deve disporre delle autorizzazioni per lo sviluppatore per un prodotto in un&#39;organizzazione IMS. Informazioni dettagliate sugli account di sviluppatori nell&#39;Admin Console sono disponibili nel documento [di](https://helpx.adobe.com/enterprise/using/manage-developers.html) supporto per la gestione degli sviluppatori.

**Accesso sviluppatore**

Contatta un amministratore di Admin Console nella tua organizzazione per aggiungere te come sviluppatore per uno dei prodotti della tua organizzazione tramite [Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

L&#39;amministratore deve assegnare l&#39;utente come sviluppatore ad almeno un profilo di prodotto per continuare.

![](images/authentication/add-developer.png)

Una volta assegnati come sviluppatore, potrete disporre dei privilegi di accesso per creare integrazioni su [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Queste integrazioni sono una pipeline dalle app e dai servizi esterni all&#39;API Adobe.

**Accesso utente**

L’amministratore di Admin Console deve anche aggiungere l’utente al prodotto come utente.

![](images/authentication/assign-users.png)

Come per la procedura di aggiunta di uno sviluppatore, l’amministratore deve assegnarvi almeno un profilo di prodotto per poter procedere.

![](images/authentication/assign-user-details.png)


## Generazione di credenziali di accesso in Adobe Developer Console

Con Adobe Developer Console, dovete generare le seguenti tre credenziali di accesso:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

È necessario generare `{IMS_ORG}` e `{API_KEY}` solo una volta e riutilizzarli in chiamate API della piattaforma future. Tuttavia, `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi sono descritti in dettaglio di seguito.

### Configurazione una tantum

Andate ad [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ed effettuate l&#39;accesso con il vostro Adobe ID. Attenetevi quindi ai passaggi descritti nell&#39;esercitazione sulla [creazione di un progetto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vuoto nella documentazione di Adobe Developer Console.

Dopo aver creato un nuovo progetto, fate clic **[!UICONTROL Add API]** sulla schermata Panoramica __ progetto.

![](images/authentication/add-api-button.png)

Viene visualizzata la schermata _Aggiungi un&#39;API_ . Fai clic sull&#39;icona del prodotto per Adobe Experience Platform, quindi seleziona **[!UICONTROL Experience Platform API]** prima di fare clic su **[!UICONTROL Next]**.

![](images/authentication/add-platform-api.png)

Dopo aver selezionato Experience Platform come API da aggiungere al progetto, segui i passaggi descritti nell&#39;esercitazione sull&#39; [aggiunta di un&#39;API a un progetto utilizzando un account di servizio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partire dal passaggio &quot;Configura API&quot;) per completare il processo.

Dopo che l&#39;API è stata aggiunta al progetto, nella pagina di panoramica _del_ progetto vengono visualizzate le seguenti credenziali, richieste in tutte le chiamate alle API della piattaforma Experience:

* `{API_KEY}` (ID client)
* `{IMS_ORG}` (ID organizzazione)

![](./images/authentication/api-key-ims-org.png)

### Autenticazione per ogni sessione

L&#39;ultima credenziale richiesta da raccogliere è la tua `{ACCESS_TOKEN}`. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare le API della piattaforma.

Per generare un nuovo `{ACCESS_TOKEN}`, seguite i passaggi per [generare un token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) JWT nella guida alle credenziali della console per sviluppatori.

## Verifica credenziali di accesso

Dopo aver raccolto tutte e tre le credenziali necessarie, puoi provare a effettuare la seguente chiamata API. Questa chiamata elenca tutte le classi Experience Data Model (XDM) all&#39;interno del `global` contenitore del Registro di sistema dello schema:

**Formato API**

```http
GET /global/classes
```

**Richiesta**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

Se la risposta è simile a quella mostrata di seguito, le credenziali sono valide e funzionanti. Questa risposta è stata troncata per lo spazio.

**Risposta**

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

## Utilizzare Postman per l&#39;autenticazione JWT e le chiamate API

[Postman](https://www.getpostman.com/) è uno strumento popolare per lavorare con le API RESTful. Questo post [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Medium descrive come impostare postman per eseguire automaticamente l&#39;autenticazione JWT e utilizzarlo per utilizzare le API Adobe Experience Platform.

## Passaggi successivi

Leggendo questo documento, hai raccolto e verificato con successo le credenziali di accesso per le API della piattaforma. Ora puoi seguire le chiamate API di esempio fornite nell&#39;intera [documentazione](../landing/documentation/overview.md).

Oltre ai valori di autenticazione raccolti in questa esercitazione, molte API della piattaforma richiedono anche che venga fornito un header valido `{SANDBOX_NAME}` . Per ulteriori informazioni, consultate la panoramica [delle](../sandboxes/home.md) sandbox.