---
title: Autenticazione
description: Scopri come configurare l’autenticazione per l’API di Adobe Experience Platform Edge Network Server.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# Autenticazione {#authentication}

## Panoramica

La [!DNL Edge Network Server API] gestisce la raccolta di dati autenticati e non autenticati, a seconda dell’origine degli eventi e del dominio di raccolta API.

Per ogni richiesta, il [!DNL Server API] verifica il datastream [!DNL access type] impostazione. Utilizzando questa impostazione, i clienti possono configurare un datastream per accettare dati autenticati o sia autenticati che non autenticati. Per impostazione predefinita, vengono accettati entrambi i tipi di dati.

Per informazioni dettagliate sulla configurazione del tipo di accesso a datastream, consulta la documentazione su come [creare e configurare un datastream](../edge/datastreams/overview.md#create).

Di seguito è riportato un riepilogo del comportamento, in base al datastream [!DNL Access Type] configurazione e l&#39;endpoint in cui viene ricevuta la richiesta.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mista (predefinito) | Non autentica la richiesta | Autentica la richiesta |
| autenticato | Autentica la richiesta | Autentica la richiesta |

Chiamate API provenienti da un server privato su `server.adobedc.net` devono sempre essere autenticati.

## Prerequisiti {#prerequisites}

Prima di poter effettuare chiamate al [!DNL Server API], assicurati di soddisfare i seguenti prerequisiti:

* Hai un account organizzazione IMS con accesso a Adobe Experience Platform.
* Il tuo account Experience Platform ha `developer` e `user` ruoli abilitati per il profilo di prodotto API di Adobe Experience Platform. Contatta il tuo [Admin Console](../access-control/home.md) amministratore per abilitare questi ruoli per il tuo account.
* Lei ha un Adobe ID. Se non disponi di un Adobe ID, passa alla pagina [Console Adobe Developer](https://developer.adobe.com/console) e crea un nuovo account.

## Raccogli credenziali {#credentials}

Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](../landing/api-authentication.md). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Le risorse in Experience Platform possono essere isolate in sandbox virtuali specifiche. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui avrà luogo l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la sezione [documentazione panoramica su sandbox](../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Content-Type: `application/json`

## Configurare le autorizzazioni di scrittura del set di dati {#dataset-write-permissions}

Per configurare le autorizzazioni di scrittura del set di dati, vai alla pagina [Admin Console](https://adminconsole.adobe.com), individua il profilo di prodotto allegato alla tua chiave API e imposta le seguenti autorizzazioni:

* In [!UICONTROL Sandbox] , seleziona la sandbox di datastream.
* In [!UICONTROL Gestione dati] seleziona la sezione **[!UICONTROL Gestire i set di dati]** autorizzazione.

## Risoluzione dei problemi degli errori di autorizzazione {#troubleshooting-authorization}

| Codice di errore | Messaggio di errore | Descrizione |
| --- | --- | --- |
| `EXEG-0500-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato in una delle situazioni seguenti:  <ul><li>La `authorization` valore intestazione mancante.</li><li>La `authorization` il valore di intestazione non include il `Bearer` token.</li><li>Formato del token di autorizzazione specificato non valido.</li><li>Il datastream richiede l’autenticazione, ma alla richiesta mancano le intestazioni richieste.</li></ul> |
| `EXEG-0501-401` | Token di autorizzazione utente non valido | Questo messaggio di errore viene visualizzato in una delle situazioni seguenti: <ul><li>Nella chiamata API manca il valore richiesto `x-user-token` intestazione.</li><li>Formato del token utente specificato non valido.</li></ul> |
| `EXEG-0502-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato quando il token di autorizzazione fornito ha un formato valido (JWT), ma la firma non è valida. Controlla la [esercitazione sull&#39;autenticazione](../landing/api-authentication.md) per scoprire come ottenere un token JWT valido. |
| `EXEG-0503-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato quando il token di autorizzazione fornito è scaduto. Passare attraverso [esercitazione sull&#39;autenticazione](../landing/api-authentication.md) per generare un nuovo token. |
| `EXEG-0504-401` | Contesto prodotto richiesto mancante | Questo messaggio di errore viene visualizzato in una delle situazioni seguenti:  <ul><li>L&#39;account sviluppatore non ha accesso al contesto di prodotto Adobe Experience Platform.</li><li>L’account aziendale non ha ancora diritto ad Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Ambito del token di autorizzazione richiesto mancante | Questo errore si applica solo all&#39;autenticazione dell&#39;account del servizio. Il messaggio di errore viene visualizzato quando il token di autorizzazione del servizio incluso nella chiamata appartiene a un account di servizio che non ha accesso al `acp.foundation` Ambito IMS. |
| `EXEG-0506-401` | Sandbox non accessibile per la scrittura | Questo messaggio di errore viene visualizzato quando l’account sviluppatore non dispone di `WRITE` accesso alla sandbox di Experience Platform in cui è definito il datastream. |
