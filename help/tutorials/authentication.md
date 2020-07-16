---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Autenticazione e accesso  API Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 1%

---


# Autenticazione e accesso [!DNL Experience Platform] alle API

Questo documento fornisce un&#39;esercitazione passo-passo per ottenere l&#39;accesso a un account sviluppatore  Adobe Experience Platform per effettuare chiamate alle [!DNL Experience Platform] API.

## Autenticazione per effettuare chiamate API

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste alle API di I/O Adobe devono essere autenticate e autorizzate utilizzando standard quali OAuth e JSON Web Token (JWT). Il JWT viene quindi utilizzato insieme alle informazioni specifiche per il cliente per generare il token di accesso personale.

Questa esercitazione descrive i passaggi dell&#39;autenticazione mediante la creazione di un token di accesso delineato nel seguente diagramma di flusso:
![](images/authentication/authentication-flowchart.png)

## Prerequisiti

Per effettuare correttamente le chiamate alle [!DNL Experience Platform] API, è necessario quanto segue:

* Un&#39;organizzazione IMS con accesso al Adobe Experience Platform 
* Un account  Adobe ID registrato
* Un amministratore  Admin Console per aggiungere voi come **sviluppatore** e un **utente** a un prodotto.

Le sezioni seguenti descrivono i passaggi necessari per creare un Adobe ID  e diventare sviluppatore e utente per un&#39;organizzazione.

### Creare un Adobe ID 

Se non disponete di un Adobe ID , potete crearne uno seguendo la procedura seguente:

1. Vai ad [Adobe Developer Console](https://console.adobe.io)
2. Fai clic su **[!UICONTROL create a new account]**.
3. Completare il processo di registrazione

## Diventare sviluppatore e utente per [!DNL Experience Platform] un&#39;organizzazione

Prima di creare integrazioni sull&#39;I/O Adobe, il vostro account deve disporre delle autorizzazioni per lo sviluppatore per un prodotto in un&#39;organizzazione IMS. Informazioni dettagliate sugli account sviluppatore nell&#39;Admin Console  sono disponibili nel documento [di](https://helpx.adobe.com/enterprise/using/manage-developers.html) supporto per la gestione degli sviluppatori.

**Accesso sviluppatore**

Contatta un [!DNL Admin Console] amministratore dell’organizzazione per aggiungere l’utente come sviluppatore per uno dei prodotti dell’organizzazione che utilizza l’ [!DNL Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

L&#39;amministratore deve assegnare l&#39;utente come sviluppatore ad almeno un profilo di prodotto per continuare.

![](images/authentication/add-developer.png)

Una volta assegnati come sviluppatore, potrete disporre dei privilegi di accesso per creare integrazioni su [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Queste integrazioni sono una pipeline dalle app e dai servizi esterni all&#39;API Adobe.

**Accesso utente**

L’ [!DNL Admin Console] amministratore deve anche aggiungere l’utente al prodotto come utente.

![](images/authentication/assign-users.png)

Come per la procedura di aggiunta di uno sviluppatore, l’amministratore deve assegnarvi almeno un profilo di prodotto per poter procedere.

![](images/authentication/assign-user-details.png)

## Generazione di credenziali di accesso in Adobe Developer Console

>[!NOTE]
>
>Se state seguendo questo documento dalla guida [per gli sviluppatori di](../privacy-service/api/getting-started.md)Privacy Service, ora potete tornare a tale guida per generare le credenziali di accesso univoche per [!DNL Privacy Service].

Con Adobe Developer Console, dovete generare le seguenti tre credenziali di accesso:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

È necessario generare `{IMS_ORG}` e `{API_KEY}` solo una volta e riutilizzarli in chiamate [!DNL Platform] API future. Tuttavia, `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi sono descritti in dettaglio di seguito.

### Configurazione una tantum

Andate ad [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ed effettuate l&#39;accesso con il vostro Adobe ID . Attenetevi quindi ai passaggi descritti nell&#39;esercitazione sulla [creazione di un progetto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vuoto nella documentazione di Adobe Developer Console.

Dopo aver creato un nuovo progetto, fate clic **[!UICONTROL Add API]** sulla schermata Panoramica __ progetto.

![](images/authentication/add-api-button.png)

Viene visualizzata la schermata _Aggiungi un&#39;API_ . Fate clic sull&#39;icona del prodotto per  Adobe Experience Platform, quindi selezionate **[!UICONTROL Experience Platform API]** prima di fare clic su **[!UICONTROL Next]**.

![](images/authentication/add-platform-api.png)

Dopo aver selezionato [!DNL Experience Platform] come API da aggiungere al progetto, segui i passaggi descritti nell&#39;esercitazione sull&#39; [aggiunta di un&#39;API a un progetto utilizzando un account di servizio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partire dal passaggio &quot;Configura API&quot;) per completare il processo.

Una volta aggiunta l&#39;API al progetto, la pagina di panoramica _del_ progetto visualizza le seguenti credenziali che sono richieste in tutte le chiamate alle [!DNL Experience Platform] API:

* `{API_KEY}` (ID client)
* `{IMS_ORG}` (ID organizzazione)

![](./images/authentication/api-key-ims-org.png)

### Autenticazione per ogni sessione

L&#39;ultima credenziale richiesta da raccogliere è la tua `{ACCESS_TOKEN}`. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare [!DNL Platform] le API.

Per generare un nuovo `{ACCESS_TOKEN}`, seguite i passaggi per [generare un token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) JWT nella guida alle credenziali della console per sviluppatori.

## Verifica credenziali di accesso

Dopo aver raccolto tutte e tre le credenziali necessarie, puoi provare a effettuare la seguente chiamata API. Questa chiamata elenca tutte le classi [!DNL Experience Data Model] (XDM) all&#39;interno del `global` contenitore del Registro di sistema dello schema:

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

## Utilizzare Postman per l&#39;autenticazione JWT e le chiamate API

[Postman](https://www.getpostman.com/) è uno strumento popolare per lavorare con le API RESTful. Questo post [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Medium descrive come impostare postman per eseguire automaticamente l&#39;autenticazione JWT e usarlo per utilizzare  API Adobe Experience Platform.

## Passaggi successivi

Leggendo questo documento, hai raccolto e verificato con successo le credenziali di accesso per [!DNL Platform] le API. Ora puoi seguire le chiamate API di esempio fornite nell&#39;intera [documentazione](../landing/documentation/overview.md).

Oltre ai valori di autenticazione raccolti in questa esercitazione, molte [!DNL Platform] API richiedono anche che come intestazione sia `{SANDBOX_NAME}` disponibile una valida. Per ulteriori informazioni, consultate la panoramica [delle](../sandboxes/home.md) sandbox.