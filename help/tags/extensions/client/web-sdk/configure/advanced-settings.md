---
title: Impostazioni di configurazione avanzate
description: Configurare le impostazioni avanzate per l'estensione tag Web SDK.
source-git-commit: d6aea91d6989775ff5b6038b216ed2518f4a7d98
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Impostazioni di configurazione avanzate

Questa sezione di configurazione consente di modificare le impostazioni avanzate. Per la maggior parte delle implementazioni, Adobe consiglia di mantenere queste opzioni invariate.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Advanced Settings]**.

![Immagine che mostra le impostazioni avanzate utilizzando la pagina dell&#39;estensione tag Web SDK](../assets/advanced-settings.png)

Attualmente, è disponibile un’opzione.

## [!UICONTROL Edge base path]

Utilizza questo campo per modificare il percorso di base utilizzato per interagire con Edge Network. Adobe potrebbe richiedere la modifica di questo campo se partecipi ad alcuni test alfa o beta; in caso contrario, Adobe consiglia di lasciarlo al valore predefinito di `ee`.

Questo campo è l&#39;equivalente tag di [`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md) durante la configurazione della libreria JavaScript.
