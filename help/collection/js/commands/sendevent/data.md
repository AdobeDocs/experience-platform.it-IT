---
title: dati
description: Scopri come inviare dati non XDM ad Adobe tramite l’oggetto dati.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

L&#39;oggetto `data` consente di inviare un payload ad Adobe che non corrisponde a uno schema XDM. È utile in scenari non XDM, ad esempio per inviare dati direttamente ad Adobe Analytics, Adobe Target o Adobe Audience Manager. Quando i dati arrivano al flusso di dati, puoi utilizzare [Mappatura preparazione dati](/help/data-prep/ui/mapping.md) per assegnare campi XDM a ciascun campo nell&#39;oggetto `data`. Se un prodotto è già configurato da Adobe per rilevare i campi all&#39;interno dell&#39;oggetto `data`, è possibile inviare tali dati così come sono a un flusso di dati.

>[!IMPORTANT]
>
>I dati all&#39;interno di questo oggetto devono avere almeno una delle azioni seguenti:
>
>* Un servizio nello stream di dati deve essere configurato per recuperare dati da una determinata proprietà nell&#39;oggetto `data`.
>* La proprietà specificata deve essere mappata a un campo XDM utilizzando la preparazione dati.
>
>Se una determinata proprietà non è mappata a un campo XDM o utilizzata da un servizio configurato, tali dati vengono persi in modo permanente.

Impostare l&#39;oggetto `data` come parte dell&#39;oggetto JSON all&#39;interno del parametro del comando `sendEvent`. Per i dati che intendi mappare nel flusso di dati, puoi strutturare questo oggetto come preferisci. Per i dati utilizzati da alcuni servizi, accertati che la gerarchia degli oggetti corrisponda a quanto previsto dal servizio. È possibile includere sia l&#39;oggetto `data` che l&#39;oggetto [`xdm`](xdm.md) nello stesso comando `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Usa l&#39;oggetto `data` con Adobe Analytics {#analytics}

È possibile utilizzare l&#39;oggetto `data` con Adobe Analytics per inviare dati a una suite di rapporti senza uno schema XDM. Le variabili sono configurate per utilizzare la stessa sintassi delle variabili di AppMeasurement, semplificando il processo di aggiornamento al Web SDK. Per ulteriori informazioni, consulta [Mappatura della variabile dell&#39;oggetto dati su Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) nella guida all&#39;implementazione di Adobe Analytics.

## Utilizza l&#39;oggetto `data` tramite l&#39;estensione tag Web SDK

L&#39;oggetto `data` è disponibile come elemento dati [Variable](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) quando si utilizza l&#39;estensione tag Web SDK.
