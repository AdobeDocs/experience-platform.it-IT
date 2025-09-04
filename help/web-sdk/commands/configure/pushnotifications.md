---
title: pushNotifications
description: Configura le notifiche push per Web SDK per abilitare i messaggi push basati su browser.
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 2%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> Le notifiche push per il Web SDK sono attualmente in **beta**. La funzionalità e la documentazione potrebbero cambiare.

La proprietà `pushNotifications` consente di configurare le notifiche push per le applicazioni Web. Questa funzione consente all’app web di ricevere messaggi inviati da un server, anche quando il sito web non è attualmente caricato nel browser o anche quando il browser non è in esecuzione.

## Prerequisiti {#prerequisites}

Prima di configurare le notifiche push, assicurati di disporre di:

1. **Autorizzazione utente**: gli utenti devono concedere esplicitamente l&#39;autorizzazione per le notifiche
2. **Lavoratore del servizio**: per il funzionamento delle notifiche push è necessario un processo di lavoro del servizio registrato
3. **Chiavi VAPID**: genera chiavi VAPID (Voluntary Application Server Identification) per comunicazioni protette

## Genera chiavi VAPID {#generate-vapid-keys}

Per generare le chiavi VAPID, installare il pacchetto NPM `web-push` ed eseguire:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Viene generata una coppia di chiavi pubblica e privata. Utilizza la chiave pubblica nella configurazione del Web SDK e archivia la chiave privata nel canale delle notifiche push di Adobe Journey Optimizer.

## Configurare le notifiche push tramite l’estensione tag Web SDK {#configure-push-notifications-tag-extension}

Per abilitare e configurare le notifiche push, segui la procedura riportata di seguito:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Estensioni]**, quindi fai clic su **[!UICONTROL Configura]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. **Abilita le notifiche push** dalla sezione &quot;Componenti di compilazione personalizzati&quot;.
1. Scorri verso il basso per individuare la sezione [!UICONTROL Notifiche push].
1. Immetti la chiave pubblica VAPID nel campo **[!UICONTROL Chiave pubblica VAPID]**.
1. Fai clic su **[!UICONTROL Salva]**, quindi pubblica le modifiche.

>[!NOTE]
>
> Le notifiche push devono essere abilitate esplicitamente nella configurazione dell’estensione tag. La funzione è disabilitata per impostazione predefinita.

## Configurare le notifiche push tramite la libreria JavaScript di Web SDK {#configure-push-notifications-javascript}

Impostare l&#39;oggetto `pushNotifications` durante l&#39;esecuzione del comando `configure`:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey:
      "BEl62iUYgUivElbkzaBgNL3r3vOAhvJyFXjS6FjjRRojYD4NElJkLBJKZvS3xAAh4_gE3WnMaZNu_KGP4jAQlJz",
  },
});
```

## Proprietà {#properties}

| Proprietà | Tipo | Obbligatorio | Descrizione |
| ------ | ------ | -------- | ----- |
| `vapidPublicKey` | Stringa | Sì | Chiave pubblica VAPID utilizzata per l’abbonamento push. Deve essere una stringa con codifica Base64. |

## Considerazioni importanti {#important-considerations}

- **Sicurezza**: le sottoscrizioni push sono associate alla chiave pubblica VAPID specifica utilizzata durante la sottoscrizione. Se modifichi le chiavi VAPID, le sottoscrizioni esistenti vengono automaticamente annullate e ricreate con la nuova chiave.
- **Memorizzazione in cache**: Web SDK gestisce automaticamente gli aggiornamenti delle sottoscrizioni confrontando l&#39;ECID corrente e i dettagli delle sottoscrizioni con i valori memorizzati nella cache. I dati di abbonamento vengono inviati solo quando vengono rilevate modifiche.
- **Requisito del lavoratore del servizio**: le notifiche push richiedono un lavoratore del servizio registrato. Assicurati che il tuo service worker sia configurato correttamente per gestire gli eventi push.

## Passaggi successivi {#next-steps}

Dopo aver configurato le notifiche push, utilizzare il comando [`sendPushSubscription`](../sendPushSubscription.md) per registrare le sottoscrizioni push con Adobe Experience Platform.
