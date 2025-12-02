---
title: Impostazioni di configurazione del consenso
description: Configura le impostazioni predefinite di consenso e privacy per l’estensione tag.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Impostazioni di configurazione del consenso

La sezione **[!UICONTROL Consent]** ti consente di selezionare il livello predefinito di consenso che viene utilizzato se non viene fornita alcuna preferenza di consenso esplicito. Il livello di consenso predefinito non viene salvato nei profili utente.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Consent]**.

![Immagine che mostra le impostazioni di privacy dell&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag](../assets/web-sdk-ext-privacy.png)

Questa sezione contiene un singolo set di pulsanti di scelta che determina il livello di consenso predefinito:

* **[!UICONTROL In]**: raccogli eventi che si verificano prima che l&#39;utente fornisca le preferenze di consenso.
* **[!UICONTROL Out]**: elimina gli eventi che si verificano prima che l&#39;utente fornisca le preferenze di consenso.
* **[!UICONTROL Pending]**: eventi di coda che si verificano prima che l&#39;utente fornisca le preferenze di consenso. Quando viene concesso il consenso, gli eventi in coda vengono inviati ad Adobe. Quando il consenso viene negato, gli eventi in coda vengono eliminati.
* **[!UICONTROL Provide a data element]**: selezionare un elemento dati che determina una delle impostazioni di configurazione sopra indicate. I valori validi includono le stringhe `"in"`, `"out"` o `"pending"`.

Se l&#39;organizzazione richiede il consenso esplicito dell&#39;utente per la raccolta dei dati, Adobe consiglia di impostare il consenso predefinito su **[!UICONTROL Out]** o **[!UICONTROL Pending]**.
