---
title: Accesso ai token di risposta tramite Adobe Experience Platform Web SDK
description: Scopri come accedere ai token di risposta con Adobe Experience Platform Web SDK.
keywords: personalizzazione;target;adobe target;renderDecisions;sendEvent;decisionScopes;result.Decisions,response tokens;
exl-id: fc9d552a-29ba-4693-9ee2-599c7bc76cdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Accesso ai token di risposta

Il contenuto di personalizzazione restituito da Adobe Target include [token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), ovvero dettagli sull’attività, l’offerta, l’esperienza, il profilo utente, le informazioni geografiche e altro ancora. Questi dettagli possono essere condivisi con strumenti di terze parti o utilizzati per il debug. I token di risposta possono essere configurati nell’interfaccia utente di Adobe Target.

Per accedere a qualsiasi contenuto di personalizzazione, fornisci una funzione di callback durante l’invio di un evento. Questo callback verrà richiamato dopo che l&#39;SDK avrà ricevuto una risposta corretta dal server. Il callback verrà fornito come `result` oggetto, che può contenere `propositions` contenente eventuali contenuti di personalizzazione restituiti. Di seguito è riportato un esempio di fornitura di una funzione di callback.

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

In questo esempio, `result.propositions`, se esiste, è un array contenente proposte di personalizzazione relative all’evento. Consulta [Rendering del contenuto di personalizzazione](../rendering-personalization-content.md) per ulteriori informazioni sul contenuto di `result.propositions`.

Supponiamo di voler raccogliere tutti i nomi delle attività da tutte le proposte di cui è stato eseguito il rendering automatico dall’SDK web e inviarli in un singolo array. È quindi possibile inviare il singolo array a una terza parte. In questo caso:

1. Estrarre proposte dalla `result` oggetto.
1. Eseguire un ciclo tra le proposte.
1. Determina se l’SDK ha eseguito il rendering della proposta.
1. In tal caso, scorri ciclicamente ogni elemento della proposta.
1. Recupera il nome dell’attività da `meta` , che è un oggetto contenente token di risposta.
1. Invia il nome dell’attività a un array.
1. Invia i nomi delle attività a una terza parte.

Il codice si presenterà come segue:

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
