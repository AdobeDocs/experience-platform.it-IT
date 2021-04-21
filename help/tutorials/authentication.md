---
keywords: Experience Platform;home;argomenti popolari;autenticare;accedere
solution: Experience Platform
title: API di Experience Platform di autenticazione e accesso
topic-legacy: tutorial
type: Tutorial
description: 'Questo documento spiega passo-passo come accedere a un account sviluppatore di Adobe Experience Platform per effettuare chiamate alle API di Experience Platform. '
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 4%

---


# Autenticazione e accesso alle API [!DNL Experience Platform]

Questo documento fornisce un tutorial dettagliato per ottenere l’accesso a un account sviluppatore Adobe Experience Platform per effettuare chiamate alle API [!DNL Experience Platform] .

## Effettuare chiamate API con autenticazione

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste alle API di Adobe I/O devono essere autenticate e autorizzate utilizzando standard come OAuth e JSON Web Token (JWT). Il JWT viene quindi utilizzato insieme alle informazioni specifiche per il cliente per generare il token di accesso personale.

Questa esercitazione descrive i passaggi dell’autenticazione tramite la creazione di un token di accesso descritto nel seguente diagramma di flusso:
![](images/authentication/authentication-flowchart.png)

## Prerequisiti

Per effettuare correttamente le chiamate alle API [!DNL Experience Platform] , è necessario quanto segue:

* Organizzazione IMS con accesso a Adobe Experience Platform
* Un account Adobe ID registrato
* Un amministratore di Admin Console per aggiungerti come **sviluppatore** e come **utente** per un prodotto.

Le sezioni seguenti illustrano i passaggi necessari per creare un Adobe ID e diventare uno sviluppatore e un utente per un&#39;organizzazione.

### Creare un Adobe ID

Se non disponi di un Adobe ID, puoi crearne uno seguendo questi passaggi:

1. Vai a [Adobe Developer Console](https://console.adobe.io)
2. Seleziona **[!UICONTROL create a new account]**
3. Completare il processo di registrazione

## Diventa sviluppatore e utente per [!DNL Experience Platform] per un&#39;organizzazione

Prima di creare integrazioni su Adobe I/O, il tuo account deve disporre delle autorizzazioni per gli sviluppatori per un prodotto in un’organizzazione IMS. Informazioni dettagliate sugli account sviluppatore nell&#39;Admin Console sono disponibili nel [documento di supporto](https://helpx.adobe.com/enterprise/using/manage-developers.html) per gli sviluppatori di gestione.

**Accesso per sviluppatori**

Contatta un amministratore [!DNL Admin Console] della tua organizzazione per aggiungerti come sviluppatore per uno dei prodotti della tua organizzazione utilizzando [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

L’amministratore deve assegnarti come sviluppatore ad almeno un profilo di prodotto per procedere.

![](images/authentication/add-developer.png)

Una volta assegnato come sviluppatore, avrai accesso ai privilegi di accesso per creare integrazioni su [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Queste integrazioni sono una pipeline da applicazioni e servizi esterni all’API Adobe.

**Accesso utente**

Il tuo amministratore [!DNL Admin Console] deve anche aggiungerti al prodotto come utente.

![](images/authentication/assign-users.png)

Analogamente al processo per l’aggiunta di uno sviluppatore, l’amministratore deve assegnarti almeno un profilo di prodotto per poter procedere.

![](images/authentication/assign-user-details.png)

## Generare le credenziali di accesso in Adobe Developer Console

>[!NOTE]
>
>Se segui questo documento dalla [guida per sviluppatori di Privacy Service](../privacy-service/api/getting-started.md), ora puoi tornare a tale guida per generare le credenziali di accesso univoche per [!DNL Privacy Service].

Utilizzando Adobe Developer Console, è necessario generare le tre credenziali di accesso seguenti:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Le chiamate `{IMS_ORG}` e `{API_KEY}` devono essere generate una sola volta e possono essere riutilizzate in chiamate API future [!DNL Platform]. Tuttavia, il tuo `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi sono descritti in dettaglio di seguito.

### Configurazione una tantum

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nell’esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione di Adobe Developer Console.

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Add API]** nella schermata **Panoramica progetto** .

![](images/authentication/add-api-button.png)

Viene visualizzata la schermata **Aggiungi un&#39;API** . Seleziona l’icona del prodotto per Adobe Experience Platform, quindi scegli **[!UICONTROL Experience Platform API]** prima di selezionare **[!UICONTROL Next]**.

![](images/authentication/add-platform-api.png)

Dopo aver selezionato [!DNL Experience Platform] come API da aggiungere al progetto, segui i passaggi descritti nell’esercitazione su [l’aggiunta di un’API a un progetto utilizzando un account di servizio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partire dal passaggio &quot;Configura API&quot;) per completare il processo.

Una volta aggiunta l’API al progetto, la pagina **Panoramica progetto** visualizza le seguenti credenziali richieste in tutte le chiamate alle API [!DNL Experience Platform]:

* `{API_KEY}` (ID client)
* `{IMS_ORG}` (ID organizzazione)

![](./images/authentication/api-key-ims-org.png)

### Autenticazione per ogni sessione

L&#39;ultima credenziale richiesta da raccogliere è la tua `{ACCESS_TOKEN}`. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, per continuare a utilizzare le API [!DNL Platform] è necessario generare un nuovo token ogni 24 ore.

Per generare un nuovo `{ACCESS_TOKEN}`, segui i passaggi per [generare un token JWT](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) nella guida delle credenziali della Console per sviluppatori.

## Verificare le credenziali di accesso

Dopo aver raccolto tutte e tre le credenziali richieste, puoi provare a effettuare la seguente chiamata API. Questa chiamata elencherà tutte le classi [!DNL Experience Data Model] (XDM) all&#39;interno del contenitore `global` del Registro di schema:

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

## Usa Postman per l’autenticazione JWT e le chiamate API

[](https://www.postman.com/) Postmanis uno strumento popolare per lavorare con le API RESTful. Questo [post medio](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descrive come impostare postman per eseguire automaticamente l&#39;autenticazione JWT e utilizzarlo per utilizzare le API Adobe Experience Platform.

## Passaggi successivi

Leggendo questo documento, hai raccolto e verificato con successo le credenziali di accesso per le API [!DNL Platform]. Ora puoi seguire l&#39;esempio di chiamate API fornite nella [documentazione](../landing/documentation/overview.md).

Oltre ai valori di autenticazione raccolti in questa esercitazione, molte [!DNL Platform] API richiedono anche un `{SANDBOX_NAME}` valido da fornire come intestazione. Per ulteriori informazioni, consulta la [panoramica sulle sandbox](../sandboxes/home.md) .