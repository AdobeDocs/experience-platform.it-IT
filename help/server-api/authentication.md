---
title: Autenticazione
description: Scopri come configurare l’autenticazione per l’API Adobe Experience Platform Edge Network Server.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 7%

---

# Autenticazione {#authentication}

## Panoramica

[!DNL Edge Network Server API] gestisce sia la raccolta dati autenticati che non autenticati, a seconda dell&#39;origine degli eventi e del dominio della raccolta API.

Per ogni richiesta, [!DNL Server API] verifica l&#39;impostazione dello stream di dati [!DNL access type]. Utilizzando questa impostazione, i clienti possono configurare un flusso di dati per accettare dati autenticati o sia dati autenticati che non autenticati. Per impostazione predefinita, entrambi i tipi di dati sono accettati.

Per informazioni dettagliate sulla configurazione del tipo di accesso allo stream di dati, consulta la documentazione su come [creare e configurare uno stream di dati](../datastreams/overview.md#create).

Di seguito è riportato un riepilogo del comportamento, basato sulla configurazione dello stream di dati [!DNL Access Type] e sull&#39;endpoint su cui viene ricevuta la richiesta.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| misto (impostazione predefinita) | Non autentica la richiesta | Autentica la richiesta |
| autenticato | Autentica la richiesta | Autentica la richiesta |

Le chiamate API provenienti da un server privato su `server.adobedc.net` devono sempre essere autenticate.

## Prerequisiti {#prerequisites}

Prima di poter effettuare chiamate a [!DNL Server API], assicurati di soddisfare i seguenti prerequisiti:

* Hai un account organizzazione con accesso a Adobe Experience Platform.
* Nel tuo account di Experience Platform sono abilitati i ruoli `developer` e `user` per il profilo di prodotto API Adobe Experience Platform. Contatta l&#39;amministratore [Admin Console](../access-control/home.md) per abilitare questi ruoli per il tuo account.
* Hai un Adobe ID. Se non hai un Adobe ID, passa a [Adobe Developer Console](https://developer.adobe.com/console) e crea un nuovo account.

## Raccogli le credenziali {#credentials}

Per effettuare chiamate alle API di Platform, devi prima completare l&#39;[esercitazione di autenticazione](../landing/api-authentication.md). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Le risorse di Experience Platform possono essere isolate in specifiche sandbox virtuali. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui verrà eseguita l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la [documentazione di panoramica sulle sandbox](../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Tipo di contenuto: `application/json`

## Configurare le autorizzazioni di scrittura del set di dati {#dataset-write-permissions}

Per configurare le autorizzazioni di scrittura del set di dati, vai all&#39;[Admin Console](https://adminconsole.adobe.com), individua il profilo di prodotto associato alla tua chiave API e imposta le seguenti autorizzazioni:

* Nella sezione [!UICONTROL Sandbox], seleziona la sandbox dello stream di dati.
* Nella sezione [!UICONTROL Gestione dati], seleziona l&#39;autorizzazione **[!UICONTROL Gestione set di dati]**.

## Risoluzione dei problemi di autorizzazione {#troubleshooting-authorization}

| Codice errore | Messaggio di errore | Descrizione |
| --- | --- | --- |
| `EXEG-0500-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato in una delle seguenti situazioni:  <ul><li>Valore di intestazione `authorization` mancante.</li><li>Il valore dell&#39;intestazione `authorization` non include il token `Bearer` richiesto.</li><li>Il token di autorizzazione richiesto è in un formato non valido.</li><li>Lo stream di dati richiede l’autenticazione, ma nella richiesta mancano intestazioni richieste.</li></ul> |
| `EXEG-0501-401` | Token di autorizzazione utente non valido | Questo messaggio di errore viene visualizzato in una delle seguenti situazioni: <ul><li>Nella chiamata API manca l&#39;intestazione `x-user-token` richiesta.</li><li>Il token utente fornito è in un formato non valido.</li></ul> |
| `EXEG-0502-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato quando il token di autorizzazione fornito ha un formato valido (JWT), ma la firma non è valida. Controlla l&#39;[esercitazione sull&#39;autenticazione](../landing/api-authentication.md) per scoprire come ottenere un token JWT valido. |
| `EXEG-0503-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato quando il token di autorizzazione fornito è scaduto. Segui l&#39;[esercitazione sull&#39;autenticazione](../landing/api-authentication.md) per generare un nuovo token. |
| `EXEG-0504-401` | Contesto prodotto richiesto mancante | Questo messaggio di errore viene visualizzato in una delle seguenti situazioni:  <ul><li>L’account sviluppatore non ha accesso al contesto di prodotto di Adobe Experience Platform.</li><li>L’account aziendale non ha ancora diritto a Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Manca l’ambito del token di autorizzazione richiesto | Questo errore si applica solo all&#39;autenticazione dell&#39;account del servizio. Il messaggio di errore viene visualizzato quando il token di autorizzazione del servizio incluso nella chiamata appartiene a un account del servizio che non ha accesso all&#39;ambito IMS `acp.foundation`. |
| `EXEG-0506-401` | Sandbox non accessibile in scrittura | Questo messaggio di errore viene visualizzato quando l&#39;account sviluppatore non ha accesso `WRITE` alla sandbox di Experience Platform in cui è definito lo stream di dati. |
