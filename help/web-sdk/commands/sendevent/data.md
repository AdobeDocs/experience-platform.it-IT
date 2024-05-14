---
title: dati
description: Scopri come inviare dati non XDM ad Adobe tramite l’oggetto dati.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

Il `data` L’oggetto ti consente di inviare un payload ad Adobe che non corrisponde a uno schema XDM. È utile in scenari non XDM, ad esempio per inviare dati direttamente ad Adobe Analytics, Adobe Target o Adobe Audience Manager. Quando i dati arrivano al flusso di dati, puoi utilizzare [Mappatura della preparazione dati](/help/data-prep/ui/mapping.md) per assegnare campi XDM a ciascun campo nel `data` oggetto.

>[!IMPORTANT]
>
>I dati all&#39;interno di questo oggetto devono avere almeno una delle azioni seguenti:
>
>* Un servizio nello stream di dati deve essere configurato per recuperare dati da una determinata proprietà in `data` oggetto.
>* La proprietà specificata deve essere mappata a un campo XDM utilizzando la preparazione dati.
>
>Se una determinata proprietà non è mappata a un campo XDM o utilizzata da un servizio configurato, tali dati vengono persi in modo permanente.

## Utilizza il `data` tramite l’estensione tag Web SDK {#tag-extension}

Fornisci un elemento dati nel **[!UICONTROL Dati]** nelle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Invia evento]**.
1. Fornisci l’elemento dati contenente l’oggetto desiderato nella **[!UICONTROL Dati]** campo.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Utilizza il `data` tramite la libreria JavaScript dell’SDK per web {#library}

Imposta il `data` come parte dell&#39;oggetto JSON all&#39;interno del parametro del `sendEvent` comando. Per i dati che intendi mappare nel flusso di dati, puoi strutturare questo oggetto come preferisci. Per i dati utilizzati da alcuni servizi, accertati che la gerarchia degli oggetti corrisponda a quanto previsto dal servizio. Puoi includere entrambi `data` oggetto e [`xdm`](xdm.md) oggetto nello stesso `sendEvent` comando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Utilizza il `data` oggetto con Adobe Analytics {#analytics}

È possibile utilizzare `data` con Adobe Analytics per inviare dati a una suite di rapporti senza uno schema XDM. Le variabili sono configurate per utilizzare la stessa sintassi di [!DNL AppMeasurement] , semplificando il processo di aggiornamento a Web SDK. Consulta [Mappatura della variabile dell’oggetto dati su Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) nella guida all’implementazione di Adobe Analytics per ulteriori informazioni.
