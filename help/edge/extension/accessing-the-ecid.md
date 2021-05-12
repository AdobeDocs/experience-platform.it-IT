---
title: 'Accesso all’ECID '
description: Estensione Adobe Experience Platform Web SDK che sfrutta ECID in Adobe Experience Platform Launch
source-git-commit: 3002036d7366e2f7310aa62e53c7c391d9ff7a07
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 5%

---


# Accesso all’ECID

Il [!DNL Experience Cloud Identity (ECID)] è un identificatore permanente per un visitatore del sito web. In alcune circostanze, potresti preferire accedere all’ECID (ad esempio per inviarlo a terzi).

Per accedere all’ECID in Adobe Experience Platform Launch, l’Adobe consiglia quanto segue:

1. Verifica che la proprietà sia configurata con [sequenza dei componenti della regola](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) abilitata.
1. Crea una nuova regola.
1. Aggiungi un evento [!UICONTROL Library Loaded] alla regola.
1. Aggiungi un&#39;azione [!UICONTROL Custom Condition] alla regola con il seguente codice (supponendo che il nome configurato per l&#39;istanza SDK sia `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salva la regola.

A questo punto dovresti essere in grado di accedere all’ECID nelle regole successive utilizzando `%ECID%` o `_satellite.getVar("ECID")` come faresti con qualsiasi altro elemento dati.
