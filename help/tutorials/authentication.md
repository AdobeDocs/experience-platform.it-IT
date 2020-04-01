---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: API Authenticate e Access Experience Platform
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# Autenticazione e accesso alle API della piattaforma Experience

Questo documento fornisce un&#39;esercitazione passo-passo per ottenere l&#39;accesso a un account sviluppatore Adobe Experience Platform per effettuare chiamate alle API della piattaforma Experience.

## Autenticazione per effettuare chiamate API

Per mantenere la sicurezza delle applicazioni e degli utenti, tutte le richieste alle API di I/O Adobe devono essere autenticate e autorizzate utilizzando standard quali OAuth e JSON Web Token (JWT). Il JWT viene quindi utilizzato insieme alle informazioni specifiche del cliente per generare il token di accesso personale.

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

1. Vai alla console I/O di [Adobe](https://console.adobe.io)
2. Fate clic su **Crea un nuovo account**
3. Completare il processo di registrazione


### Diventa sviluppatore e utente per la piattaforma Experience per un&#39;organizzazione

Prima di creare integrazioni sull&#39;I/O Adobe, il vostro account deve disporre delle autorizzazioni per lo sviluppatore per un prodotto in un&#39;organizzazione IMS. Informazioni dettagliate sugli account di sviluppatori nell&#39;Admin Console sono disponibili nel documento [di](https://helpx.adobe.com/enterprise/using/manage-developers.html) supporto per la gestione degli sviluppatori.

**Accesso sviluppatore**

Contatta un amministratore di Admin Console nella tua organizzazione per aggiungere te come sviluppatore per uno dei prodotti della tua organizzazione tramite [Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

L&#39;amministratore deve assegnare l&#39;utente come sviluppatore ad almeno un profilo di prodotto per continuare.

![](images/authentication/add-developer.png)

Una volta assegnati come sviluppatore, potrete disporre dei privilegi di accesso per creare integrazioni su [Adobe I/O](https://console.adobe.io/). Queste integrazioni sono una pipeline dalle app e dai servizi esterni all&#39;API Adobe.

**Accesso utente**

L’amministratore di Admin Console deve anche aggiungere l’utente al prodotto come utente.

![](images/authentication/assign-users.png)

Come per la procedura di aggiunta di uno sviluppatore, l’amministratore deve assegnarvi almeno un profilo di prodotto per poter procedere.

![](images/authentication/assign-user-details.png)


## Configurazione una tantum

I seguenti passaggi dovranno essere eseguiti solo una volta:

* Accesso alla console Adobe I/O
* Crea integrazione
* Copia valori di accesso in basso

Una volta ottenuta l&#39;integrazione e i valori di accesso, potrete riutilizzarli per l&#39;autenticazione in futuro. Ogni fase è trattata nel dettaglio di seguito.

### Accedere alla console Adobe I/O

Andate alla console [I/O di](https://console.adobe.io/) Adobe ed effettuate l&#39;accesso con il vostro Adobe ID.

Una volta effettuato l&#39;accesso, fai clic sulla scheda **Integrazioni** nella parte superiore dello schermo. Un&#39;integrazione è un account di servizio creato per l&#39;organizzazione IMS selezionata. È possibile effettuare solo chiamate per l&#39;organizzazione IMS in cui viene creata l&#39;integrazione.

>[!NOTE]
>Se l’account è associato a più organizzazioni, il menu a discesa in alto a destra della schermata consente di passare facilmente da un’organizzazione all’altra.

### Creare un&#39;integrazione

Dalla pagina **Integrazioni** , fai clic su **Nuova integrazione** per avviare il processo. Il processo comprende tre fasi:
* Scegliere il tipo di integrazione
* Scegliere il servizio Adobe con cui effettuare l&#39;integrazione
* Aggiungere dettagli di integrazione, chiave pubblica e profilo di prodotto

![](images/authentication/integrations.png)

#### Scegliere il tipo di integrazione

Nella schermata successiva viene chiesto se desiderate accedere a un&#39;API o ricevere eventi in tempo quasi reale. Selezionate **Accedi a un&#39;API** , quindi **Continua**.

![](images/authentication/create-new-integration.png)

#### Scegliere il servizio Adobe con cui effettuare l&#39;integrazione

Se il vostro account è associato a più organizzazioni IMS, potete passare da un&#39;organizzazione all&#39;altra utilizzando il menu a discesa in alto a destra. Selezionate **Workshop** e **Experience Platform API** in **Adobe Experience Platform** per accedere alle API.

![](images/authentication/integration-select-service.png)

Fate clic su **Continua** per passare alla sezione successiva.

#### Aggiungere dettagli di integrazione, chiave pubblica e profilo di prodotto

Nella schermata successiva viene richiesto di inserire i dettagli di integrazione, immettere il certificato di chiave pubblica e selezionare un profilo di prodotto.

![](images/authentication/integration-details.png)

Innanzitutto, immettete i dettagli di integrazione. Quindi, seleziona un profilo di prodotto. I profili di prodotto concedono l’accesso granulare a un gruppo di funzioni appartenenti al servizio selezionato nei passaggi precedenti.

Per la sezione del certificato, dovete generare un certificato:

**Per le piattaforme MacOS e Linux:**

Aprite la riga di comando ed eseguite il comando seguente:

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**Per le piattaforme Windows:**

1. Scaricare un client open per generare certificati pubblici (ad esempio, client [](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip)Openssl windows)

1. Estrarre la cartella e copiarla nel percorso C:/libs/.

1. Aprite il prompt della riga di comando ed eseguite i comandi seguenti:

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

Riceverete una risposta simile a quella riportata di seguito, che richiede di inserire alcune informazioni su di voi stessi:

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

Dopo aver immesso le informazioni, vengono generati due file: `certificate_pub.crt` e `private.key`.

>[!NOTE]
>`certificate_pub.crt` scadrà tra 365 giorni. È possibile prolungare il periodo modificando il valore di `days` nel `openssl` comando precedente, ma ruotare le credenziali periodicamente è una procedura di sicurezza consigliata.

Il `private.key` sito verrà utilizzato per generare il nostro JWT nella sezione successiva.

Viene `certificate_pub.crt` utilizzato per creare una chiave API. Torna alla console di I/O di Adobe e fai clic su **Seleziona un file** per caricare il `certificate_pub.crt` file.

Fate clic su **Crea integrazione** per completare il processo.

### Copia valori di accesso giù

Dopo aver creato l&#39;integrazione, potete visualizzarne i dettagli. Fate clic su **Recupera Segreto** cliente e la schermata avrà un aspetto simile al seguente:

![](images/authentication/access-values.png)

Copiate i valori per `{API KEY}`, `{IMS ORG}` ovvero l&#39;ID organizzazione, `{CLIENT SECRET}` che verranno utilizzati nel passaggio successivo.

## Autenticazione per ogni sessione

Il passo finale è quello di generare le chiamate `{ACCESS_TOKEN}` che verranno utilizzate per autenticare le chiamate API. Il token di accesso deve essere incluso nell’intestazione Autorizzazione di ogni chiamata API effettuata ad Adobe Experience Platform. I token di accesso scadono dopo 24 ore, dopodiché è necessario generare nuovi token per continuare a utilizzare le API.

### Crea JWT

Nella pagina dei dettagli dell’integrazione nella console Adobe I/O, andate alla scheda **JWT** :

![](images/authentication/generate-jwt.png)

Nella pagina viene richiesto di inserire la sezione `private.key` creata nella sezione precedente. Aprite la riga di comando per visualizzare il contenuto del `private.key` file:

```shell
cat private.key
```

L&#39;output sarà simile al seguente:

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

Copiate l’intero output e incollatelo nel campo di testo, quindi fate clic su **Genera JWT**. Copiate il JWT generato per il passaggio successivo.

![](images/authentication/generated-jwt.png)

### Genera token di accesso

Potete generare un token di accesso tramite un comando cURL. Se non è installato cURL, è possibile installarlo utilizzando `npm install curl`. Per maggiori informazioni su cURL, consulta [qui](https://curl.haxx.se/)

Una volta installato cURL, dovrete scambiare i campi nel seguente comando con il vostro `{API_KEY}`, `{CLIENT_SECRET}`, e `{JWT_TOKEN}`:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

In caso di esito positivo, l&#39;output sarà simile al seguente:

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

Il token di accesso è il valore sotto la `access_token` chiave. Questo token di accesso `expires_in` 8639947 millisecondi (24 ore). In seguito, dovrete generare un nuovo token di accesso seguendo gli stessi passaggi sopra.

Ora sei pronto a effettuare richieste API in Adobe Experience Platform!

### Codice di accesso di prova

Per verificare se il token di accesso è valido, puoi provare a effettuare la seguente chiamata API. Questa chiamata elenca tutte le classi all&#39;interno del `global` contenitore:

>[!NOTE]
>`{API_KEY}` e `{IMS_ORG}` fare riferimento ai valori generati in precedenza.

**Richiesta**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


Se la risposta è simile a quella mostrata di seguito, la risposta `access_token` è valida e funzionante. Questa risposta è stata troncata per lo spazio.

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