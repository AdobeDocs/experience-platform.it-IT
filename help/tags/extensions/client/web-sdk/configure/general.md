---
title: Impostazioni di configurazione dell’istanza di SDK
description: Configurare le impostazioni generali per l'istanza di Web SDK.
exl-id: cc22b8b3-88c6-4030-91b4-60e14a3b0f42
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---

# Impostazioni di configurazione dell’istanza di SDK {#sdk-instance}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_sdkinstance"
>title="Istanze di SDK"
>abstract="Imposta il nome dell’istanza SDK, l’organizzazione IMS a cui appartiene e il dominio edge."

Questa sezione di configurazione definisce il nome dell’istanza di Web SDK, l’organizzazione IMS a cui si applica e la posizione a cui desideri inviare i dati. Per impostazione predefinita, un&#39;istanza è denominata `alloy`.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Individuare il nome dell&#39;istanza appena sotto il pannello a soffietto [!UICONTROL SDK instances] espanso.

![Immagine che mostra le impostazioni generali dell&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag](../assets/web-sdk-ext-general.png)

Sono disponibili le seguenti opzioni:

## [!UICONTROL Name]

L’estensione tag Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Il nome viene utilizzato per inviare dati a più organizzazioni senza che siano necessarie librerie di tag di Web SDK duplicate. È possibile modificare il nome dell&#39;istanza in qualsiasi nome di oggetto JavaScript valido.

## [!UICONTROL IMS organization ID]

ID dell’organizzazione a cui si desidera inviare i dati in Adobe. Nella maggior parte dei casi, utilizza il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, compila questo campo con il valore della seconda organizzazione a cui desideri inviare i dati.

## [!UICONTROL Edge domain]

Il dominio da cui l’estensione invia e riceve i dati. Per impostazione predefinita, il campo contiene `<COMPANYID>.data.adobedc.net`. Le implementazioni precedenti potrebbero contenere un valore predefinito di `edge.adobedc.net`, anch&#39;esso valido.

Nella maggior parte dei casi, Adobe consiglia di utilizzare un dominio di prime parti. Per istruzioni su come impostare un dominio di prime parti idoneo per la raccolta dei dati, vedere il [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/it/docs/core-services/interface/data-collection/adobe-managed-cert). Per istruzioni sull&#39;impostazione di questo valore, consulta anche [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) nella documentazione della libreria JavaScript.
