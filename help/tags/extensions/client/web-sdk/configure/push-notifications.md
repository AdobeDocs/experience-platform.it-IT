---
title: Impostazioni delle notifiche push
description: Configura le impostazioni delle notifiche push per l’estensione tag Web SDK.
exl-id: 96ab7ea8-7180-46bb-9c15-eecba2009c52
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Impostazioni delle notifiche push {#push-notifications}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_pushnotifications"
>title="Notifiche push"
>abstract="Imposta una chiave pubblica VAPID per l&#39;autenticazione delle notifiche push."

>[!AVAILABILITY]
>
>Le notifiche push per il Web SDK sono attualmente in **beta**. La funzionalità e la documentazione sono soggette a modifiche.

Questa sezione di configurazione consente di impostare una chiave pubblica VAPID per l’autenticazione delle notifiche push.

>[!NOTE]
>
>Questa funzionalità deve essere prima abilitata utilizzando [Componenti di compilazione personalizzati](custom-build-components.md). Per impostazione predefinita è disabilitata.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi fai clic su **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Espandere **[!UICONTROL Custom build components]**, quindi abilitare **[!UICONTROL Push notifications]**.
1. In [!UICONTROL SDK instances], scorrere verso il basso per individuare la sezione [!UICONTROL Push Notifications].
1. Immettere la chiave pubblica VAPID nel campo **[!UICONTROL VAPID Public Key]**.

![Immagine che mostra le impostazioni delle notifiche push tramite l&#39;estensione tag Web SDK](../assets/push-notifications.png)

Sono disponibili i seguenti campi:

## [!UICONTROL VAPID public key]

Chiave pubblica VAPID utilizzata per le sottoscrizioni push. È una stringa con codifica Base64.

## [!UICONTROL Application ID]

ID applicazione associato alla chiave pubblica VAPID.

## [!UICONTROL Tracking dataset ID]

ID del set di dati per il tracciamento e l’analisi delle notifiche push.

## Notifiche push tramite la libreria JavaScript

Questa sezione è l&#39;equivalente tag di [`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md) durante la configurazione della libreria JavaScript. La pagina collegata fornisce inoltre informazioni sui prerequisiti e sulla generazione di una chiave pubblica VAPID.
