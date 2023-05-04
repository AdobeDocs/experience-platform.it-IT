---
title: Accesso all’ECID
description: Scopri come accedere all’ID Experience Cloud da Preparazione dati o Tag
exl-id: 8e63a873-d7b5-4c6c-b14d-3c3fbc82b62f
source-git-commit: dee04f2cdeb9057ac10e27a17f9db3f065712618
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 3%

---


# Accesso all’ECID

La [!DNL Experience Cloud Identity (ECID)] è un identificatore permanente assegnato a un utente quando visita il tuo sito web. In alcune circostanze, potresti preferire accedere al [!DNL ECID] (ad esempio per inviarlo a terzi). Un altro caso d’uso è l’impostazione della variabile [!DNL ECID] in un campo XDM personalizzato, oltre a essere incluso nella mappa di identità.

Puoi accedere all’ECID tramite [Preparazione per la raccolta dei dati](../datastreams/data-prep.md) (consigliato) o tramite tag.

## Accesso all’ECID tramite Data Prep (metodo preferito) {#accessing-ecid-data-prep}

Se desideri impostare l’ECID in un campo XDM personalizzato, oltre a averlo nella mappa di identità, puoi farlo impostando la variabile `source` al seguente percorso:

```js
xdm.identityMap.ECID[0].id
```

Quindi, imposta il target su un percorso XDM in cui il campo è di tipo `string`.

![](./assets/access-ecid-data-prep.png)

## Tag

Se devi accedere al [!DNL ECID] sul lato client, utilizza l’approccio tag come descritto di seguito.

1. Verifica che la proprietà sia configurata con [sequenza dei componenti della regola](../../tags/ui/managing-resources/rules.md#sequencing) abilitato.
1. Crea una nuova regola.
1. Aggiungi un [!UICONTROL Libreria caricata] alla regola.
1. Aggiungi un [!UICONTROL Condizione personalizzata] alla regola con il seguente codice (supponendo che il nome configurato per l&#39;istanza SDK sia `alloy`):

   ```js
    return alloy("getIdentity")
      .then(function(result) {
        _satellite.setVar("ECID", result.identity.ECID);
      });
   ```

1. Salva la regola.

A quel punto dovresti essere in grado di accedere al [!DNL ECID] nelle regole successive utilizzando `%ECID%` o `_satellite.getVar("ECID")`, come qualsiasi altro elemento dati.
