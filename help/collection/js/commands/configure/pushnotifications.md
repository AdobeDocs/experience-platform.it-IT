---
title: pushNotifications
description: Configura le notifiche push per Web SDK per abilitare i messaggi push basati su browser.
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 3%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>Le notifiche push per il Web SDK sono attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

La proprietà `pushNotifications` consente di configurare le notifiche push per le applicazioni Web. Questa funzione consente all’app web di ricevere messaggi inviati da un server, anche quando il sito web non è attualmente caricato nel browser.

## Prerequisiti {#prerequisites}

Prima di configurare le notifiche push, assicurati di disporre di:

1. **Autorizzazione utente**: gli utenti devono concedere esplicitamente l&#39;autorizzazione per le notifiche
2. **Lavoratore del servizio**: per il funzionamento delle notifiche push è necessario un processo di lavoro del servizio registrato
3. **Chiavi VAPID**: genera chiavi VAPID (Voluntary Application Server Identification) per comunicazioni protette
4. **ID applicazione**: ID app utilizzato per il salvataggio delle chiavi VAPID in Adobe Journey Optimizer -> Canali -> Impostazioni push -> Credenziali push
5. **ID del set di dati di tracciamento**: l&#39;ID del set di dati di sistema denominato &quot;Set di dati dell&#39;evento di tracciamento push di AJO&quot;. Ottieni questo da Adobe Journey Optimizer -> Set di dati

## Genera chiavi VAPID {#generate-vapid-keys}

Per generare le chiavi VAPID, installare il pacchetto NPM `web-push` ed eseguire:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Questa azione genera una coppia di chiavi pubblica e privata. Utilizza la chiave pubblica nella configurazione del Web SDK e archivia la chiave privata nel canale delle notifiche push di Adobe Journey Optimizer.

## Installa il service worker

Il codice di service worker deve essere gestito dallo stesso dominio del sito Web. Scarica il codice del service worker dalla rete CDN di Adobe e ospita il file JavaScript dal tuo server. Il codice di lavoro del servizio Web SDK è disponibile utilizzando la seguente struttura URL:

- **Minificato**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Completo**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Di seguito è riportato un esempio di installazione di service worker:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Implementazione

Impostare l&#39;oggetto `pushNotifications` durante l&#39;esecuzione del comando `configure`:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Proprietà {#properties}

| Proprietà | Tipo | Obbligatorio | Descrizione |
|---|---|---|---|
| **`vapidPublicKey`** | Stringa | Sì | Chiave pubblica VAPID utilizzata per le sottoscrizioni push. Deve essere una stringa con codifica Base64. |
| **`applicationId`** | Stringa | Sì | ID applicazione associato alla chiave pubblica VAPID. |
| **`trackingDatasetId`** | Stringa | Sì | ID del set di dati di sistema utilizzato per il tracciamento delle notifiche push. |

## Considerazioni importanti {#important-considerations}

- **Sicurezza**: le sottoscrizioni push sono associate alla chiave pubblica VAPID specifica utilizzata durante la sottoscrizione. Se modifichi le chiavi VAPID, le sottoscrizioni esistenti vengono automaticamente annullate e ricreate con la nuova chiave.
- **Memorizzazione in cache**: Web SDK gestisce automaticamente gli aggiornamenti delle sottoscrizioni confrontando l&#39;ECID corrente e i dettagli delle sottoscrizioni con i valori memorizzati nella cache. I dati di abbonamento vengono inviati solo quando vengono rilevate modifiche.
- **Requisito del lavoratore del servizio**: le notifiche push richiedono un lavoratore del servizio registrato. Assicurati che il tuo service worker sia configurato correttamente per gestire gli eventi push.

## Configurare le notifiche push tramite l’estensione tag Web SDK {#configure-push-notifications-tag-extension}

L&#39;estensione tag Web SDK equivalente a questa proprietà è la sezione [[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md) durante la configurazione dell&#39;estensione.

## Passaggi successivi {#next-steps}

Dopo aver configurato le notifiche push, utilizza il comando [sendPushSubscription](../sendpushsubscription.md) per registrare le sottoscrizioni push con Adobe Experience Platform.
