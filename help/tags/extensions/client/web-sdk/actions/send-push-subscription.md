---
title: Invia abbonamento push
description: Registra, invia e raccogli dati per gli abbonamenti push al browser.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 2%

---

# Invia abbonamento push

>[!AVAILABILITY]
>
>Le notifiche push per il Web SDK sono attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

L&#39;azione **[!UICONTROL Send push subscription]** registra gli abbonamenti alle notifiche push con Adobe Experience Platform. Gestisce il recupero dei dettagli dell’abbonamento push dal browser e li invia allo stream di dati configurato. È disponibile nelle versioni 2.32.0 o successive dell’estensione Web SDK.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Impostare il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]** e impostare [!UICONTROL Action Type] su **[!UICONTROL Send push subscription]**.

L’azione non dispone di impostazioni di configurazione diverse dalla selezione di un’istanza di SDK.

Prima di utilizzare questo comando, accertati di impostare una [chiave pubblica VAPID](../configure/push-notifications.md) valida durante la configurazione dell&#39;estensione.

Questa azione è l&#39;estensione tag equivalente al comando [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md). Per informazioni sui prerequisiti, sulla frequenza di esecuzione consigliata, sul funzionamento del comando e sulla gestione degli errori, vedere la pagina collegata.

>[!MORELIKETHIS]
>
>* [Configurare le notifiche push](../configure/push-notifications.md)
>* [Specifica API Web Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [API di lavoro dei servizi](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
