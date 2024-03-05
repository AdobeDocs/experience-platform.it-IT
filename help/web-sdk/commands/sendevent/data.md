---
title: dati
description: Scopri come inviare dati non XDM ad Adobe.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# dati

Il `data` consente di inviare dati a Adobe che non corrispondono a uno schema XDM. È utile in scenari non XDM, ad esempio per aggiornare [Profilo Adobe Target](/help/web-sdk/personalization/adobe-target/target-overview.md). Quando i dati arrivano all’Adobe, puoi utilizzare lo strumento di mappatura dello stream di dati per assegnare campi XDM a ciascun campo nel `data` proprietà.

>[!IMPORTANT]
>
>I dati all&#39;interno di questa proprietà devono avere almeno una delle azioni seguenti:
>
>* Un servizio nello stream di dati deve essere configurato per recuperare dati da una proprietà specifica nello `data` oggetto
>* Ogni proprietà deve essere mappata a un campo XDM
>
>Se un determinato campo non è mappato a un campo XDM o utilizzato da un servizio configurato, tali dati vengono persi in modo permanente.

## Utilizzare la proprietà data tramite l’estensione tag Web SDK

Fornisci un elemento dati nel **[!UICONTROL Dati]** nelle azioni di una regola di tag.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali di Adobe ID.
1. Accedi a **[!UICONTROL Raccolta dati]** > **[!UICONTROL Tag]**.
1. Seleziona la proprietà tag desiderata.
1. Accedi a **[!UICONTROL Regole]**, quindi seleziona la regola desiderata.
1. Sotto [!UICONTROL Azioni], seleziona un&#39;azione esistente o creane una.
1. Imposta il [!UICONTROL Estensione] campo a discesa per **[!UICONTROL Adobe Experience Platform Web SDK]**, e impostare [!UICONTROL Tipo di azione] a **[!UICONTROL Invia evento]**.
1. Fornisci l’elemento dati contenente l’oggetto desiderato nella **[!UICONTROL Dati]** campo.
1. Clic **[!UICONTROL Mantieni modifiche]**, quindi esegui il flusso di lavoro di pubblicazione.

## Utilizzare la proprietà data utilizzando la libreria JavaScript dell’SDK per web

Imposta il `data` come parte dell&#39;oggetto JSON all&#39;interno del parametro del `sendEvent` comando. Per i dati che intendi mappare nel flusso di dati, puoi strutturare questa proprietà come preferisci. Per i dati utilizzati da alcuni servizi, accertati che la gerarchia degli oggetti corrisponda a quanto previsto dal servizio. Puoi includere entrambi `data` oggetto e [`xdm`](xdm.md) oggetto nello stesso `sendEvent` comando.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
