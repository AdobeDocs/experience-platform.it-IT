---
title: Accesso all’ECID
description: Estensione Adobe Experience Platform Web SDK che sfrutta l’ECID nei tag
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 5%

---

# Accesso all’ECID

Il [!DNL Experience Cloud Identity (ECID)] è un identificatore permanente di un visitatore del sito web. In alcune circostanze, potrebbe essere preferibile accedere all’ECID (ad esempio per inviarlo a terzi).

Per accedere all’ECID all’interno dei tag, l’Adobe consiglia quanto segue:

1. Assicurati che la proprietà sia configurata con [sequenza dei componenti della regola](../../tags/ui/managing-resources/rules.md#sequencing) abilitato.
1. Crea una nuova regola.
1. Aggiungi un [!UICONTROL Libreria caricata] alla regola.
1. Aggiungi un [!UICONTROL Condizione personalizzata] alla regola con il seguente codice (supponendo che il nome configurato per l&#39;istanza dell&#39;SDK sia `alloy`):

   ```javascript
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salva la regola.

Dovresti quindi essere in grado di accedere all’ECID nelle regole successive utilizzando `%ECID%` o `_satellite.getVar("ECID")` come faresti con qualsiasi altro elemento dati.
