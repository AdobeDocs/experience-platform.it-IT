---
title: Accesso all’ECID
description: Scopri come accedere all’ID Experience Cloud dalla preparazione dati o dai tag
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# Accesso all’ECID

Il [!DNL Experience Cloud Identity (ECID)] è un identificatore permanente assegnato a un utente quando visita il sito web. In alcune circostanze, potrebbe essere preferibile accedere al [!DNL ECID] (ad esempio per inviarlo a terzi). Un altro caso d’uso è l’impostazione di [!DNL ECID] in un campo XDM personalizzato, oltre a averlo nella mappa delle identità.

Puoi accedere all’ECID tramite [Preparazione per la raccolta dati](../../../../edge/datastreams/data-prep.md) (consigliato) o tramite tag.

## Accesso all’ECID tramite la preparazione dati (metodo preferito) {#accessing-ecid-data-prep}

Se desideri impostare l’ECID in un campo XDM personalizzato, oltre a averlo nella mappa identità, puoi farlo impostando il `source` al seguente percorso:

```js
xdm.identityMap.ECID[0].id
```

Quindi, imposta la destinazione su un percorso XDM in cui il campo è di tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Tag

Se devi accedere a [!DNL ECID] sul lato client, utilizza l’approccio tag come descritto di seguito.

1. Assicurati che la proprietà sia configurata con [sequenza dei componenti della regola](../../../ui/managing-resources/rules.md#sequencing) abilitato.
1. Crea una nuova regola.
1. Aggiungi un [!UICONTROL Libreria caricata] alla regola.
1. Aggiungi un [!UICONTROL Condizione personalizzata] alla regola con il seguente codice (supponendo che il nome configurato per l&#39;istanza dell&#39;SDK sia `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salva la regola.

Dovresti quindi essere in grado di accedere al [!DNL ECID] nelle regole successive utilizzando `%ECID%` o `_satellite.getVar("ECID")`, come faresti per accedere a qualsiasi altro elemento dati.
