---
title: Accesso all’ECID
description: Scopri come accedere all’Experience Cloud ID dalla preparazione dati o dai tag
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: 19e85ef4dbaeb90712ad9cd6ad4cb9a1a6b0c6a5
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# Accesso all’ECID

[!DNL Experience Cloud Identity (ECID)] è un identificatore permanente assegnato a un utente quando visita il sito Web. In alcune circostanze, potrebbe essere preferibile accedere a [!DNL ECID] (ad esempio per inviarlo a terzi). Un altro caso d&#39;uso è l&#39;impostazione di [!DNL ECID] in un campo XDM personalizzato, oltre a averlo nella mappa delle identità.

Puoi accedere all&#39;ECID tramite [Preparazione dati per raccolta dati](/help/datastreams/data-prep.md) (consigliato) o tramite tag.

## Accesso all’ECID tramite la preparazione dati (metodo preferito) {#accessing-ecid-data-prep}

Questo metodo utilizza [Preparazione dati per la raccolta dati](/help/datastreams/data-prep.md) per configurare una mappatura personalizzata per `ECID`.

Per informazioni su come utilizzare questa funzione, consulta la documentazione di [Preparazione per la raccolta dati](/help/datastreams/data-prep.md).

Se desideri impostare l&#39;ECID in un campo XDM personalizzato, oltre a averlo nella mappa delle identità, puoi farlo impostando `source` sul seguente percorso:

```js
xdm.identityMap.ECID[0].id
```

Quindi, imposta la destinazione su un percorso XDM in cui il campo è di tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Tag

Se devi accedere a [!DNL ECID] sul lato client, utilizza l&#39;approccio tag come descritto di seguito.

1. Assicurati che la tua proprietà sia configurata con [sequenza componenti regola](/help/tags/ui/managing-resources/rules.md#sequencing) abilitata.
1. Crea una nuova regola. Questa regola deve essere utilizzata esclusivamente per acquisire [!DNL ECID] senza altre azioni importanti.
1. Aggiungi un evento [!UICONTROL Library Loaded] alla regola.
1. Aggiungi un&#39;azione [!UICONTROL Custom Code] alla regola con il seguente codice (supponendo che il nome configurato per l&#39;istanza di SDK sia `alloy` e che non esista già un elemento dati con lo stesso nome):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salva la regola.

Dovresti quindi essere in grado di accedere a [!DNL ECID] nelle regole successive utilizzando `%ECID%` o `_satellite.getVar("ECID")`, come faresti per accedere a qualsiasi altro elemento dati.
