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

L&#39;oggetto `data` consente di inviare un payload all&#39;Adobe che non corrisponde a uno schema XDM. È utile in scenari non XDM, ad esempio per inviare dati direttamente ad Adobe Analytics, Adobe Target o Adobe Audience Manager. Quando i dati arrivano al flusso di dati, puoi utilizzare [Mappatura preparazione dati](/help/data-prep/ui/mapping.md) per assegnare campi XDM a ciascun campo nell&#39;oggetto `data`.

>[!IMPORTANT]
>
>I dati all&#39;interno di questo oggetto devono avere almeno una delle azioni seguenti:
>
>* Un servizio nello stream di dati deve essere configurato per recuperare dati da una determinata proprietà nell&#39;oggetto `data`.
>* La proprietà specificata deve essere mappata a un campo XDM utilizzando la preparazione dati.
>
>Se una determinata proprietà non è mappata a un campo XDM o utilizzata da un servizio configurato, tali dati vengono persi in modo permanente.

## Utilizza l&#39;oggetto `data` tramite l&#39;estensione tag Web SDK {#tag-extension}

Fornisci un elemento dati nel campo **[!UICONTROL Dati]** all&#39;interno delle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il campo a discesa [!UICONTROL Estensione] su **[!UICONTROL Adobe Experience Platform Web SDK]** e imposta [!UICONTROL Tipo azione] su **[!UICONTROL Invia evento]**.
1. Fornisci l&#39;elemento dati contenente l&#39;oggetto desiderato nel campo **[!UICONTROL Dati]**.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Utilizza l&#39;oggetto `data` tramite la libreria JavaScript dell&#39;SDK Web {#library}

Impostare l&#39;oggetto `data` come parte dell&#39;oggetto JSON all&#39;interno del parametro del comando `sendEvent`. Per i dati che intendi mappare nel flusso di dati, puoi strutturare questo oggetto come preferisci. Per i dati utilizzati da alcuni servizi, accertati che la gerarchia degli oggetti corrisponda a quanto previsto dal servizio. È possibile includere sia l&#39;oggetto `data` che l&#39;oggetto [`xdm`](xdm.md) nello stesso comando `sendEvent`.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Usa l&#39;oggetto `data` con Adobe Analytics {#analytics}

È possibile utilizzare l&#39;oggetto `data` con Adobe Analytics per inviare dati a una suite di rapporti senza uno schema XDM. Le variabili sono configurate per utilizzare la stessa sintassi di [!DNL AppMeasurement] variabili, semplificando il processo di aggiornamento a Web SDK. Per ulteriori informazioni, consulta [Mappatura della variabile dell&#39;oggetto dati su Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) nella guida all&#39;implementazione di Adobe Analytics.
