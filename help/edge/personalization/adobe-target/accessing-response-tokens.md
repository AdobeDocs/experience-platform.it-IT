---
title: Accesso ai token di risposta tramite Adobe Experience Platform Web SDK
description: Scopri come accedere ai token di risposta con Adobe Experience Platform Web SDK.
keywords: personalizzazione;target;adobe target;renderdecisions;sendEvent;decisionScopes;result.decisions,response token;
source-git-commit: 5ae7488e715ff97d2b667c40505b79433eb74f49
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Accesso ai token di risposta

Il contenuto di personalizzazione restituito da Adobe Target include [token di risposta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html), che sono dettagli sull&#39;attività, l&#39;offerta, l&#39;esperienza, il profilo utente, le informazioni geografiche e altro ancora. Questi dettagli possono essere condivisi con strumenti di terze parti o utilizzati per il debug. I token di risposta possono essere configurati nell’interfaccia utente di Adobe Target.

Per accedere a qualsiasi contenuto di personalizzazione, fornisci una funzione di callback quando invii un evento. Questo callback viene chiamato dopo che l&#39;SDK ha ricevuto una risposta dal server. Al callback viene fornito un oggetto `result` che può contenere una proprietà `propositions` contenente eventuali contenuti di personalizzazione restituiti. Di seguito è riportato un esempio di fornitura di una funzione di callback.

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

In questo esempio, `result.propositions`, se esiste, è un array contenente proposizioni di personalizzazione relative all’evento. Per ulteriori informazioni sul contenuto di `result.propositions`, consulta [Rendering del contenuto di personalizzazione](../rendering-personalization-content.md) .

Supponi di voler raccogliere tutti i nomi delle attività da tutte le proposizioni di cui è stato eseguito automaticamente il rendering dall’SDK per web e inviarli in un singolo array. È quindi possibile inviare il singolo array a una terza parte. In questo caso:

1. Estrarre le proposizioni dall&#39;oggetto `result`.
1. Passate in rassegna ogni proposta.
1. Determina se l&#39;SDK ha eseguito il rendering della proposta.
1. In tal caso, eseguire il ciclo tra i vari elementi della proposta.
1. Recupera il nome dell&#39;attività dalla proprietà `meta` , che è un oggetto contenente i token di risposta.
1. Invia il nome dell’attività a un array.
1. Invia i nomi delle attività a una terza parte.

Il codice sarà il seguente:

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
              activityNames.push(item.meta);
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


