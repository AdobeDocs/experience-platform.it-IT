---
title: Reimposta ID unione
description: Azione obsoleta che consente di separare gli eventi denominati sulla stessa pagina.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Reimposta ID unione

>[!IMPORTANT]
>
>Azione obsoleta. Utilizza le impostazioni [Raccogli clic sul collegamento interno](../configure/data-collection.md#collect-internal-link-clicks).

Il tipo di azione **[!UICONTROL Reset merge ID]** consente di separare gli eventi chiamati sulla stessa pagina. Viene generalmente utilizzato in scenari di collegamento interno in cui è possibile che si desiderino inviare più payload ad Adobe. Questa azione ti consente di reimpostare l’ID unione di un evento in modo che non venga considerato parte dello stesso evento dopo il suo arrivo in Edge Network.

Se desideri controllare il modo in cui più eventi sulla stessa pagina vengono separati o uniti, utilizza l&#39;opzione [Raccogli clic sui collegamenti interni](../configure/data-collection.md#collect-internal-link-clicks) durante la configurazione dell&#39;estensione tag.
