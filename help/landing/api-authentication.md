---
keywords: ' Experience Platform;home;argomenti popolari;Authenticate;access'
solution: Experience Platform
title: Autenticazione e accesso  API Experience Platform
topic: tutorial
type: Tutorial
description: 'Questo documento spiega passo-passo come accedere a un account sviluppatore di Adobe Experience Platform per effettuare chiamate alle API di Experience Platform. '
translation-type: tm+mt
source-git-commit: 681a2554111f988ec03d40f23a3b2c8225a077ae
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 4%

---


# Autenticazione e accesso alle API [!DNL Experience Platform]

Questo documento fornisce un&#39;esercitazione passo-passo per ottenere l&#39;accesso a un account sviluppatore Adobe Experience Platform per effettuare chiamate alle [!DNL Experience Platform] API.

## Autenticazione per effettuare chiamate API

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste a  API Adobe I/O devono essere autenticate e autorizzate utilizzando standard quali OAuth e JSON Web Token (JWT). Il JWT viene quindi utilizzato insieme alle informazioni specifiche per il cliente per generare il token di accesso personale.

Questa esercitazione descrive i passaggi dell&#39;autenticazione mediante la creazione di un token di accesso delineato nel seguente diagramma di flusso:
![](images/api-authentication/authentication-flowchart.png)

## Prerequisiti

Per effettuare correttamente le chiamate alle [!DNL Experience Platform] API, è necessario disporre dei seguenti elementi:

* Un&#39;organizzazione IMS con accesso ad Adobe Experience Platform
* Un account Adobe ID  registrato
* Un amministratore di Admin Console  aggiungervi come **sviluppatore** e **utente** per un prodotto.

Le sezioni seguenti descrivono i passaggi necessari per creare un Adobe ID  e diventare sviluppatore e utente per un&#39;organizzazione.

### Creare un Adobe ID 

Se non disponete di un Adobe ID , potete crearne uno seguendo la procedura seguente:

1. Vai a [ Adobe Developer Console](https://console.adobe.io)
2. Seleziona **[!UICONTROL create a new account]**
3. Completare il processo di registrazione

## Diventare sviluppatore e utente per [!DNL Experience Platform] per un&#39;organizzazione

Prima di creare integrazioni su  Adobe I/O, il vostro account deve disporre delle autorizzazioni per lo sviluppatore per un prodotto in un&#39;organizzazione IMS. Informazioni dettagliate sugli account sviluppatore nel Admin Console  sono disponibili nel [documento di supporto](https://helpx.adobe.com/enterprise/using/manage-developers.html) per la gestione degli sviluppatori.

**Accesso sviluppatore**

Contatta un [!DNL Admin Console] amministratore nella tua organizzazione per aggiungere te come sviluppatore per uno dei prodotti della tua organizzazione utilizzando la [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/api-authentication/assign-developer.png)

L&#39;amministratore deve assegnare l&#39;utente come sviluppatore ad almeno un profilo di prodotto per continuare.

![](images/api-authentication/add-developer.png)

Una volta che ti sarà assegnato come sviluppatore, avrai i privilegi di accesso per creare integrazioni su [ Adobe I/O](https://www.adobe.com/go/devs_console_ui). Queste integrazioni sono una pipeline dalle app e dai servizi esterni all&#39;API del Adobe .

**Accesso utente**

L&#39;amministratore di [!DNL Admin Console] deve anche aggiungere l&#39;utente al prodotto come utente.

![](images/api-authentication/assign-users.png)

Come per la procedura di aggiunta di uno sviluppatore, l’amministratore deve assegnarvi almeno un profilo di prodotto per poter procedere.

![](images/api-authentication/assign-user-details.png)

## Generazione di credenziali di accesso in  Adobe Developer Console

>[!NOTE]
>
>Se si segue questo documento dalla [guida per gli sviluppatori di Privacy Service ](../privacy-service/api/getting-started.md), è ora possibile tornare a tale guida per generare le credenziali di accesso univoche per [!DNL Privacy Service].

Utilizzando  Adobe Developer Console, è necessario generare le seguenti tre credenziali di accesso:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Le `{IMS_ORG}` e `{API_KEY}` devono essere generate una sola volta e possono essere riutilizzate nelle chiamate API [!DNL Platform] future. Tuttavia, il `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi sono descritti in dettaglio di seguito.

### Configurazione una tantum

Andate a [ Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ed effettuate l&#39;accesso con il vostro Adobe ID . Seguite quindi i passaggi descritti nell&#39;esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione  Developer Console.

Dopo aver creato un nuovo progetto, selezionare **[!UICONTROL Add API]** nella schermata **Panoramica progetto**.

![](images/api-authentication/add-api-button.png)

Viene visualizzata la schermata **Aggiungi un&#39;API**. Selezionate l&#39;icona del prodotto per Adobe Experience Platform, quindi scegliete **[!UICONTROL Experience Platform API]** prima di selezionare **[!UICONTROL Next]**.

![](images/api-authentication/add-platform-api.png)

Dopo aver selezionato [!DNL Experience Platform] come API da aggiungere al progetto, segui i passaggi descritti nell&#39;esercitazione su [aggiunta di un&#39;API a un progetto utilizzando un account di servizio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partire dal passaggio &quot;Configura API&quot;) per completare il processo.

Una volta aggiunta l&#39;API al progetto, la pagina **Panoramica del progetto** visualizza le seguenti credenziali che sono richieste in tutte le chiamate alle [!DNL Experience Platform] API:

* `{API_KEY}` (ID client)
* `{IMS_ORG}` (ID organizzazione)

![](./images/api-authentication/api-key-ims-org.png)

### Autenticazione per ogni sessione

L&#39;ultima credenziale richiesta da raccogliere è la `{ACCESS_TOKEN}`. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare le API [!DNL Platform].

Per generare una nuova `{ACCESS_TOKEN}`, segui i passaggi per [generare un token JWT](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) nella guida alle credenziali della Developer Console.

## Verifica credenziali di accesso

Dopo aver raccolto tutte e tre le credenziali necessarie, puoi provare a effettuare la seguente chiamata API. Questa chiamata elenca tutte le classi [!DNL Experience Data Model] (XDM) all&#39;interno del contenitore del Registro di sistema `global`:

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

[Postmanis è uno strumento popolare per lavorare con le API RESTful. ](https://www.postman.com/) Questo [Post medio](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) descrive come impostare postman per eseguire automaticamente l&#39;autenticazione JWT e utilizzarlo per utilizzare le API Adobe Experience Platform.

## Passaggi successivi

Leggendo questo documento, hai raccolto e verificato con successo le credenziali di accesso per le [!DNL Platform] API. Ora puoi seguire le chiamate API di esempio fornite nella [documentazione](../landing/documentation/overview.md).

Oltre ai valori di autenticazione raccolti in questa esercitazione, molte [!DNL Platform] API richiedono anche un `{SANDBOX_NAME}` valido da fornire come intestazione. Per ulteriori informazioni, consultate la [panoramica sulle sandbox](../sandboxes/home.md).