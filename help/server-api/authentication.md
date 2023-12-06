---
title: Autenticazione
description: Scopri come configurare l’autenticazione per l’API del server di rete Edge di Adobe Experience Platform.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# Autenticazione {#authentication}

## Panoramica

Il [!DNL Edge Network Server API] gestisce sia la raccolta dati autenticati che non autenticati, a seconda dell’origine degli eventi e del dominio di raccolta API.

Per ogni richiesta, il [!DNL Server API] verifica lo stream di dati [!DNL access type] impostazione. Utilizzando questa impostazione, i clienti possono configurare un flusso di dati per accettare dati autenticati o sia dati autenticati che non autenticati. Per impostazione predefinita, entrambi i tipi di dati sono accettati.

Per informazioni dettagliate sulla configurazione del tipo di accesso allo stream di dati, consulta la documentazione su come [creare e configurare uno stream di dati](../datastreams/overview.md#create).

Di seguito è riportato un riepilogo del comportamento, in base allo stream di dati [!DNL Access Type] e l’endpoint su cui viene ricevuta la richiesta.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| misto (impostazione predefinita) | Non autentica la richiesta | Autentica la richiesta |
| autenticato | Autentica la richiesta | Autentica la richiesta |

Chiamate API provenienti da un server privato su `server.adobedc.net` deve sempre essere autenticato.

## Prerequisiti {#prerequisites}

Prima di poter effettuare chiamate al [!DNL Server API], assicurati di soddisfare i seguenti prerequisiti:

* Hai un account organizzazione con accesso a Adobe Experience Platform.
* Il tuo account di Experience Platform ha `developer` e `user` ruoli abilitati per il profilo di prodotto API Adobe Experience Platform. Contatta il tuo [Admin Console](../access-control/home.md) per abilitare questi ruoli per il tuo account.
* Hai un Adobe ID. Se non disponi di un Adobe ID, vai al [Console Adobe Developer](https://developer.adobe.com/console) e crea un nuovo account.

## Raccogli le credenziali {#credentials}

Per effettuare chiamate alle API di Platform, devi prima completare la sezione [tutorial sull’autenticazione](../landing/api-authentication.md). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experienci Platform, come mostrato di seguito:

* Autorizzazione: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Le risorse di Experienci Platform possono essere isolate in specifiche sandbox virtuali. Nelle richieste alle API di Platform, puoi specificare il nome e l’ID della sandbox in cui verrà eseguita l’operazione. Si tratta di parametri facoltativi.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experienci Platform, consulta la sezione [documentazione di panoramica sulla sandbox](../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione di tipo multimediale aggiuntiva:

* Tipo di contenuto: `application/json`

## Configurare le autorizzazioni di scrittura del set di dati {#dataset-write-permissions}

Per configurare le autorizzazioni di scrittura del set di dati, vai a [Admin Console](https://adminconsole.adobe.com), individua il profilo di prodotto associato alla chiave API e imposta le seguenti autorizzazioni:

* In [!UICONTROL Sandbox] , seleziona la sandbox dello stream di dati.
* In [!UICONTROL Gestione dati] , seleziona la sezione **[!UICONTROL Gestione set di dati]** autorizzazione.

## Risoluzione dei problemi di autorizzazione {#troubleshooting-authorization}

| Codice errore | Messaggio di errore | Descrizione |
| --- | --- | --- |
| `EXEG-0500-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato in una delle seguenti situazioni:  <ul><li>Il `authorization` valore di intestazione mancante.</li><li>Il `authorization` il valore dell’intestazione non include il necessario `Bearer` token.</li><li>Il token di autorizzazione fornito è in un formato non valido.</li><li>Lo stream di dati richiede l’autenticazione, ma nella richiesta mancano intestazioni richieste.</li></ul> |
| `EXEG-0501-401` | Token di autorizzazione utente non valido | Questo messaggio di errore viene visualizzato in una delle seguenti situazioni: <ul><li>Nella chiamata API manca il necessario `x-user-token` intestazione.</li><li>Il token utente fornito è in un formato non valido.</li></ul> |
| `EXEG-0502-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato quando il token di autorizzazione fornito ha un formato valido (JWT), ma la firma non è valida. Controlla la [tutorial sull’autenticazione](../landing/api-authentication.md) per scoprire come ottenere un token JWT valido. |
| `EXEG-0503-401` | Token di autorizzazione non valido | Questo messaggio di errore viene visualizzato quando il token di autorizzazione fornito è scaduto. Passare attraverso [tutorial sull’autenticazione](../landing/api-authentication.md) per generare un nuovo token. |
| `EXEG-0504-401` | Manca il contesto di prodotto richiesto | Questo messaggio di errore viene visualizzato in una delle seguenti situazioni:  <ul><li>L’account sviluppatore non ha accesso al contesto di prodotto di Adobe Experience Platform.</li><li>L’account aziendale non ha ancora diritto a Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Manca l’ambito del token di autorizzazione richiesto | Questo errore si applica solo all&#39;autenticazione dell&#39;account del servizio. Il messaggio di errore viene visualizzato quando il token di autorizzazione del servizio incluso nella chiamata appartiene a un account del servizio che non ha accesso a `acp.foundation` Ambito IMS. |
| `EXEG-0506-401` | Sandbox non accessibile in scrittura | Questo messaggio di errore viene visualizzato quando l’account sviluppatore non dispone di `WRITE` accedere alla sandbox di Experience Platform in cui è definito lo stream di dati. |
