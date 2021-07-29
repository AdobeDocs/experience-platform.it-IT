---
title: 'Accesso all’ECID '
description: Estensione Adobe Experience Platform Web SDK Sfruttamento di ECID nei tag
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 5%

---


# Accesso all’ECID

Il [!DNL Experience Cloud Identity (ECID)] è un identificatore permanente per un visitatore del sito web. In alcune circostanze, potresti preferire accedere all’ECID (ad esempio per inviarlo a terzi).

Per accedere all’ECID all’interno dei tag, l’Adobe consiglia quanto segue:

1. Verifica che la proprietà sia configurata con [sequenza dei componenti della regola](https://experienceleague.adobe.com/docs/launch/using/ui/rules.html?lang=en#rule-component-sequencing) abilitata.
1. Crea una nuova regola.
1. Aggiungi un evento [!UICONTROL Library Loaded] alla regola.
1. Aggiungi un&#39;azione [!UICONTROL Condizione personalizzata] alla regola con il seguente codice (supponendo che il nome configurato per l&#39;istanza SDK sia `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salva la regola.

A questo punto dovresti essere in grado di accedere all’ECID nelle regole successive utilizzando `%ECID%` o `_satellite.getVar("ECID")` come faresti con qualsiasi altro elemento dati.
