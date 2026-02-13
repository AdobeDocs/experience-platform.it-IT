---
title: Impostazioni di configurazione dello stream di dati
description: Configura lo stream di dati a cui inviare i dati utilizzando l’estensione tag Web SDK.
exl-id: 2d2504c6-b3f9-4e7b-aff4-a8d8d6c4e3dd
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---

# Impostazioni di configurazione dello stream di dati {#datastreams}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datastreams"
>title="Stream di dati"
>abstract="Obbligatorio. Imposta lo stream di dati all’interno dell’Edge Network a cui desideri inviare i dati."

Questa sezione di configurazione consente di determinare a quale [flusso di dati](/help/datastreams/overview.md) si desidera inviare i dati. **È necessario un ID dello stream di dati per tutti i dati inviati ad Edge Network.**

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Datastreams]**.

![Immagine che mostra le impostazioni dello stream di dati dell&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag](../assets/web-sdk-ext-datastreams.png)

Quando selezioni gli stream di dati, puoi farlo per ogni [ambiente](/help/tags/ui/publishing/environments.md) ([!UICONTROL Development], [!UICONTROL Staging] e [!UICONTROL Production]). Questi campi sono utili quando desideri separare i dati inviati tra ambienti di sviluppo, staging e produzione. Consente un flusso di lavoro comodo in cui non è necessario preoccuparsi di inviare dati allo stream di dati errato, purché si installi il caricatore di tag corretto in ogni ambiente rispettivo.

Puoi popolare gli ID dello stream di dati utilizzando uno dei seguenti metodi:

* **[!UICONTROL Choose from list]**: ogni ambiente contiene due menu a discesa che consentono di selezionare la sandbox e lo stream di dati per l&#39;ambiente selezionato. I valori in ciascun menu a discesa dipendono dai [flussi di dati](/help/datastreams/overview.md) configurati all&#39;interno di ciascuna [sandbox](/help/sandboxes/ui/overview.md).

* **[!UICONTROL Enter values]**: in alternativa all&#39;utilizzo dei menu a discesa per selezionare lo stream di dati desiderato, è possibile specificare manualmente l&#39;ID dello stream di dati direttamente. Ogni ambiente ti consente di inserire direttamente un ID dello stream di dati o di compilare questo campo utilizzando un [elemento dati](/help/tags/ui/managing-resources/data-elements.md).
