---
title: sendPushSubscription
description: Registrare gli abbonamenti alle notifiche push con Adobe Experience Platform.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 2%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
>Le notifiche push per il Web SDK sono attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

Il comando `sendPushSubscription` registra le sottoscrizioni di notifiche push con Adobe Experience Platform. Questo comando gestisce il recupero dei dettagli della sottoscrizione push dal browser e li invia allo stream di dati configurato. È disponibile in Web SDK versione 2.29.0 o successiva.

## Prerequisiti {#prerequisites}

Prima di utilizzare `sendPushSubscription`, assicurati di disporre di:

1. **Notifiche push configurate**: configura la proprietà di configurazione [`pushNotifications`](configure/pushnotifications.md) con la tua chiave pubblica VAPID
2. **Autorizzazione utente**: gli utenti devono aver concesso l&#39;autorizzazione per le notifiche (`Notification.permission === "granted"`)
3. **Service worker**: un service worker registrato deve essere disponibile nel sito
4. **Supporto di Push Manager**: il browser deve supportare le notifiche push e disporre dell&#39;API PushManager

Eseguire il comando `sendPushSubscription` quando si chiama l&#39;istanza configurata del Web SDK. Assicurarsi di chiamare il comando [`configure`](configure/overview.md) con le notifiche push configurate prima di chiamare il comando `sendPushSubscription`.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## Frequenza di esecuzione consigliata {#recommended-execution-frequency}

Per una funzionalità ottimale di notifica push, Adobe consiglia di eseguire il comando `sendPushSubscription` **una volta al giorno**. Questa frequenza assicura che:

* I dettagli dell’abbonamento rimangono correnti in Adobe Experience Platform
* Vengono acquisite eventuali modifiche ai token di push o allo stato dell’abbonamento
* Il profilo dell’utente rimane aggiornato con le preferenze per le notifiche push più recenti

Puoi implementarlo utilizzando un approccio simile a quello riportato di seguito:

```js
// Check if subscription data was sent today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## Come funziona {#how-it-works}

Il comando `sendPushSubscription` esegue le azioni seguenti:

1. **Convalida prerequisiti**: verifica che le notifiche push siano configurate e che l&#39;utente disponga delle autorizzazioni necessarie
2. **Attende l&#39;identità**: attende che l&#39;ECID dell&#39;utente sia disponibile
3. **Recupera la sottoscrizione**: ottiene la sottoscrizione push attiva dal service worker utilizzando la chiave VAPID configurata
4. **Verifica la presenza di modifiche**: confronta i dettagli della sottoscrizione corrente con i valori memorizzati nella cache (ECID + dettagli della sottoscrizione). Se i dettagli della sottoscrizione non sono stati modificati, il comando registra un messaggio di informazioni e restituisce senza effettuare una richiesta di rete
5. **Invia a datastream**: se vengono rilevate modifiche, trasmette i dati della sottoscrizione allo stream di dati di Adobe Experience Platform configurato
6. **Cache aggiornamenti**: memorizza i nuovi dettagli della sottoscrizione per il confronto futuro

## Gestione degli errori {#error-handling}

Condizioni di errore comuni e relativi messaggi:

| Errore | Causa |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | Configurazione pushNotifications mancante o non valida |
| `"Service workers are not supported in this browser."` | Il browser non supporta i processi di lavoro dei servizi |
| `"Push notifications are not supported in this browser."` | Il browser non supporta le notifiche push o l’API di notifica |
| `"The user has not given permission to send push notifications."` | L&#39;utente non ha concesso l&#39;autorizzazione per le notifiche (`Notification.permission === "granted"`) |
| `"No service worker registration was found."` | Nessun lavoratore del servizio registrato per l&#39;origine corrente |
| `"No VAPID public key was provided."` | Chiave pubblica VAPID mancante nella configurazione |

## Payload dati {#data-payload}

Il comando invia i dati di notifica push nel seguente formato:

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## Registrare l’abbonamento push tramite l’estensione tag Web SDK {#register-push-subscription-tag-extension}

L&#39;estensione tag Web SDK equivalente a questo campo utilizza l&#39;azione [[!UICONTROL Send Push Subscription]](/help/tags/extensions/client/web-sdk/actions/send-push-subscription.md) all&#39;interno di una regola di tag.

>[!MORELIKETHIS]
>
>* [Configurare le notifiche push](configure/pushnotifications.md)
>* [Specifica API Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [API di lavoro dei servizi](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
