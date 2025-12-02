---
title: onBeforeLinkClickSend
description: Callback eseguito immediatamente prima dell'invio dei dati di tracciamento dei collegamenti.
exl-id: 8c73cb25-2648-4cf7-b160-3d06aecde9b4
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# `onBeforeLinkClickSend`

>[!IMPORTANT]
>
>Questo callback è obsoleto. Utilizza invece [`clickCollection.filterClickDetails`](clickcollection.md).

Il callback `onBeforeLinkClickSend` consente di registrare una funzione di JavaScript che può modificare i dati di tracciamento dei collegamenti inviati immediatamente prima dell&#39;invio dei dati ad Adobe. Consente di manipolare l&#39;oggetto `xdm` o `data`, inclusa la possibilità di aggiungere, modificare o rimuovere elementi. Puoi anche annullare completamente l’invio di dati in modo condizionale, ad esempio con il traffico bot lato client rilevato.

Questo callback viene eseguito solo se [`clickCollectionEnabled`](clickcollectionenabled.md) è abilitato e `filterClickDetails` non contiene una funzione registrata.

Se [`onBeforeEventSend`](onbeforeeventsend.md) e `onBeforeLinkClickSend` contengono entrambi funzioni registrate, `onBeforeLinkClickSend` viene eseguito per primo.

>[!WARNING]
>
>Questo callback consente l’utilizzo di codice personalizzato. Se un codice incluso nel callback genera un&#39;eccezione non rilevata, l&#39;elaborazione per l&#39;evento si interrompe. I dati non vengono inviati ad Adobe.

## `onBeforeLinkClickSend` e `filterClickDetails`

Il callback [`clickCollection.filterClickDetails`](clickcollection.md) è progettato per sostituire `onBeforeLinkClickSend`. Adobe consiglia vivamente di non assegnare funzioni di callback a entrambi simultaneamente. Se si assegna una funzione di callback sia a `filterClickDetails` che a `onBeforeLinkClickSend`, la libreria utilizza la logica seguente:

* Solo `filterClickDetails` viene eseguito; `onBeforeLinkClickSend` no.
* Il raggruppamento di eventi `clickCollection.eventGroupingEnabled` non funziona.
