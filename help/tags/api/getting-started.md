---
title: Guida introduttiva all’API di Reactor
description: Scopri come iniziare a utilizzare l’API di Reactor, compresi i passaggi per generare le credenziali di accesso richieste.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1070'
ht-degree: 1%

---

# Guida introduttiva all’API di Reactor

Per utilizzare l&#39; [API del reattore](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml), ogni richiesta deve includere le seguenti intestazioni di autenticazione:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Questa guida illustra come utilizzare Adobe Developer Console per raccogliere i valori per ciascuna di queste intestazioni, in modo da poter iniziare a effettuare chiamate all’API del reattore.

## Accesso degli sviluppatori a Adobe Experience Platform

Prima di poter generare valori di autenticazione per l’API di Reactor, devi disporre dell’accesso ad Experience Platform per gli sviluppatori. Per ottenere l&#39;accesso per gli sviluppatori, segui i passaggi iniziali nell&#39; [esercitazione sull&#39;autenticazione Experience Platform](http://www.adobe.com/go/platform-api-authentication-en). Una volta raggiunto il passaggio &quot;Generate access credentials in Adobe Developer Console&quot; (Genera credenziali di accesso in Developer Console), torna a questa esercitazione per generare le credenziali specifiche dell’API Reactor.

## Genera credenziali di accesso

Utilizzando Adobe Developer Console, è necessario generare le tre credenziali di accesso seguenti:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

L’ID organizzazione IMS (`{IMS_ORG}`) e la chiave API (`{API_KEY}`) possono essere riutilizzati nelle chiamate API future dopo che sono state generate inizialmente. Tuttavia, il token di accesso (`{ACCESS_TOKEN}`) è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi per generare questi valori sono descritti in dettaglio di seguito.

### Configurazione una tantum

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nell’esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione di Developer Console.

Dopo aver creato un progetto, seleziona **Aggiungi API** nella schermata **Panoramica progetto** .

![](../images/api/getting-started/add-api-button.png)

Viene visualizzata la schermata **Aggiungi un&#39;API** . Seleziona **Experience Platform Reactor API** dall&#39;elenco delle API disponibili prima di selezionare **Successivo**.

![](../images/api/getting-started/add-launch-api.png)

Nella schermata successiva viene richiesto di creare una credenziale JSON Web Token (JWT) per generare una nuova coppia di chiavi o caricare una tua chiave pubblica. Per questa esercitazione, seleziona l&#39;opzione **Genera una coppia di chiavi**, quindi seleziona **Genera una coppia di chiavi** nell&#39;angolo in basso a destra.

![](../images/api/getting-started/create-jwt.png)

La schermata successiva conferma che la coppia di chiavi è stata generata correttamente e che nel computer viene automaticamente scaricata una cartella compressa contenente un certificato pubblico e una chiave privata. Questa chiave privata è necessaria in un passaggio successivo per generare un token di accesso.

Seleziona **Avanti** per continuare.

![](../images/api/getting-started/keypair-generated.png)

Nella schermata successiva viene richiesto di selezionare uno o più profili di prodotto da associare all’integrazione API.

>[!NOTE]
>
>I profili di prodotto sono gestiti dalla tua organizzazione tramite Adobe Admin Console e contengono set specifici di autorizzazioni per le funzioni granulari di Adobe Experience Platform Launch. I profili di prodotto e le relative autorizzazioni possono essere gestiti solo da utenti con privilegi di amministratore all’interno della tua organizzazione. Se non sei sicuro dei profili di prodotto da selezionare per l’API, contatta l’amministratore.

Seleziona i profili di prodotto desiderati dall’elenco, quindi seleziona **Salva API configurata** per completare la registrazione API.

![](../images/api/getting-started/select-product-profile.png)

Una volta aggiunta l’API al progetto, la pagina del progetto viene nuovamente visualizzata nella pagina API di Experience Platform Reactor. Da qui, scorri verso il basso fino alla sezione **Account di servizio (JWT)**, che fornisce le seguenti credenziali di accesso necessarie in tutte le chiamate all&#39;API del reattore:

* **ID** CLIENT: L’ID client è il obbligatorio  `{API_KEY}` che deve essere fornito nell’ `x-api-key` intestazione .
* **ID** ORGANIZZAZIONE: L&#39;ID organizzazione è il  `{IMS_ORG}` valore che deve essere utilizzato nell&#39; `x-gw-ims-org-id` intestazione .

![](../images/api/getting-started/access-creds.png)

### Autenticazione per ogni sessione

Ora che disponi dei valori `{API_KEY}` e `{IMS_ORG}`, il passaggio finale genera un valore `{ACCESS_TOKEN}`.

>[!NOTE]
>
>Questi token scadono dopo 24 ore. Se utilizzi questa integrazione per un’applicazione, è consigliabile ottenere il token portatore a livello di programmazione dall’interno dell’applicazione.

Sono disponibili due opzioni per generare i token di accesso, a seconda del caso d’uso:

* [Generare manualmente i token](#manual)
* [Generare token a livello di programmazione](#program)

#### Generare manualmente i token di accesso {#manual}

Apri la chiave privata scaricata in precedenza in un editor di testo o in un browser e copia il suo contenuto. Quindi, torna alla Console per sviluppatori e incolla la chiave privata nella sezione **Genera token di accesso** nella pagina API del reattore per il progetto prima di selezionare **Genera token**.

![](../images/api/getting-started/paste-private-key.png)

Viene generato un nuovo token di accesso e viene fornito un pulsante per copiare il token negli Appunti. Questo valore viene utilizzato per l&#39;intestazione `Authorization` richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/token-generated.png)

#### Generare token di accesso a livello di programmazione {#program}

Se utilizzi l’integrazione Launch per un’applicazione, puoi generare in modo programmatico token di accesso tramite richieste API. Per eseguire questa operazione, è necessario ottenere i seguenti valori:

* ID client (`{API_KEY}`)
* Segreto client (`{SECRET}`)
* Un token web JSON (`{JWT}`)

L&#39;ID client e il segreto possono essere ottenuti dalla pagina principale del progetto, come mostrato nel [passaggio precedente](#one-time-setup).

![](../images/api/getting-started/auto-access-creds.png)

Per ottenere le credenziali JWT, passa a **Account di servizio (JWT)** nel menu di navigazione a sinistra, quindi seleziona la scheda **Genera JWT** . In questa pagina, in **Genera JWT** personalizzato, incolla il contenuto della chiave privata nella casella di testo fornita, quindi seleziona **Genera token**.

![](../images/api/getting-started/generate-jwt.png)

Il JWT generato viene visualizzato di seguito al termine dell’elaborazione, insieme a un comando cURL di esempio che puoi utilizzare per testare il token se lo desideri. Utilizza il pulsante **Copia** per copiare il token negli Appunti.

![](../images/api/getting-started/jwt-generated.png)

Una volta raccolte le credenziali, puoi integrare la chiamata API riportata di seguito nell’applicazione per generare in modo programmatico i token di accesso.

**Richiesta**

La richiesta deve inviare un payload `multipart/form-data`, fornendo le credenziali di autenticazione come mostrato di seguito:

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**Risposta**

Una risposta corretta restituisce un nuovo token di accesso, oltre al numero di secondi rimasti fino alla scadenza.

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| Proprietà | Descrizione |
| :-- | :-- |
| `access_token` | Il valore del token di accesso appena generato. Questo valore viene utilizzato per l&#39;intestazione `Authorization` richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`. |
| `expires_in` | Tempo rimanente alla scadenza del token, in millisecondi. Una volta scaduto il token, è necessario generarne uno nuovo. |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Seguendo i passaggi descritti in questa esercitazione, dovresti disporre di valori validi per `{IMS_ORG}`, `{API_KEY}` e `{ACCESS_TOKEN}`. Ora puoi testare questi valori utilizzando in una semplice richiesta cURL all’API di Reactor.

Inizia tentando di effettuare una chiamata API a [elencare tutte le aziende](./endpoints/companies.md#list).

>[!NOTE]
>
>Potresti non avere alcuna azienda nell&#39;organizzazione, nel qual caso la risposta sarà lo stato HTTP 404 (Non trovato). Se non ottieni un errore 403 (proibito), le tue credenziali di accesso sono valide e funzionanti.

Dopo aver confermato il funzionamento delle credenziali di accesso, continua a esplorare l’altra documentazione di riferimento API per scoprire le numerose funzionalità dell’API.

## Risorse aggiuntive

Librerie JWT e SDK: [https://jwt.io/](https://jwt.io/)

Sviluppo dell’API Postman: [https://www.postman.com/](https://www.postman.com/)
