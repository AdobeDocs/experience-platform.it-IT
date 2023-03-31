---
title: Accesso all’ECID
description: Scopri come accedere all’ID Experience Cloud (ECID) nei tag Adobe Experience Platform
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 5%

---


# Accesso all’ECID

La [!DNL Experience Cloud ID (ECID)] è un identificatore di Experience Cloud permanente che può aiutarti a identificare i visitatori del tuo sito web. In alcune circostanze, ad esempio l’invio dell’identificatore a una piattaforma di terze parti, potrebbe essere necessario accedere al [!DNL ECID].

Per accedere al [!DNL ECID] all’interno dei tag, segui i passaggi seguenti:

1. Verifica che la proprietà sia configurata con [sequenza dei componenti della regola](../../tags/ui/managing-resources/rules.md#sequencing) abilitato.
2. Crea una nuova regola.
3. Aggiungi un [!UICONTROL Libreria caricata] alla regola.
4. Aggiungi un [!UICONTROL Condizione personalizzata] alla regola, con il seguente codice (supponendo che il nome configurato per l&#39;istanza SDK sia `alloy`):

   ```javascript
   return alloy("getIdentity")
       .then(function(result) {
           _satellite.setVar("ECID", result.identity.ECID);
       });
   ```

5. Salva la regola.

Ora dovresti essere in grado di accedere al [!DNL ECID] nelle regole successive, utilizzando `%ECID%` o `_satellite.getVar("ECID")`, simile alla modalità di accesso a qualsiasi altro elemento dati.
