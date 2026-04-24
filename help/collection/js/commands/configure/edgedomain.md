---
title: edgeDomain
description: Determina il dominio a cui desideri inviare i dati.
exl-id: 6beb5116-cd23-42fd-934c-5cf84d1d7153
source-git-commit: 2d3c31e399989652a0472bbe2174ca8d8554ba30
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 3%

---

# `edgeDomain`

La proprietà `edgeDomain` consente di modificare il dominio in cui il Web SDK invia i dati. L’utilizzo di un dominio personalizzato può contribuire a ridurre l’impatto degli ad blocker.

>[!NOTE]
>
>Questa proprietà non cambia la posizione in cui vengono impostati i cookie. Il Web SDK imposta sempre [cookie di prime parti](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=it), indipendentemente da dove invierà i dati.

Il valore utilizzato per `edgeDomain` dipende dalla partecipazione al [programma di certificazione gestito da Adobe](https://experienceleague.adobe.com/it/docs/core-services/interface/data-collection/adobe-managed-cert):

**Se la tua organizzazione partecipa al programma di certificazione gestito da Adobe**, imposta il valore sul dominio di prime parti selezionato durante la configurazione del certificato. In genere questo valore è un sottodominio di proprietà dell’organizzazione. Ad esempio, `data.example.com`. I record CNAME della tua organizzazione inoltrano tali dati ad Adobe.

**Se la tua organizzazione non partecipa al programma di certificazione**, imposta il valore su un sottodominio di `data.adobedc.net`. Per coerenza, Adobe consiglia di utilizzare l’ID azienda IMS assegnato da Adobe della tua organizzazione. Ad esempio, `example.data.adobedc.net`. Per determinare l’ID società IMS, effettua le seguenti operazioni:

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. In qualsiasi punto dell&#39;interfaccia di Experience Cloud, premere `[Cmd]` + `[I]` (macOS) o `[Ctrl]` + `[I]` (Windows).
1. Verrà visualizzato **[!UICONTROL User data debugger]**. Seleziona la scheda **[!UICONTROL Assigned orgs]**.
1. Espandi l’organizzazione IMS desiderata.
1. Individua il campo **[!UICONTROL Tenant]**. Questo valore è il sottodominio consigliato di `data.adobedc.net` da utilizzare.

Impostare la stringa `edgeDomain` durante l&#39;esecuzione del comando `configure`. Se si omette questa proprietà durante la configurazione di SDK, per impostazione predefinita viene utilizzato il valore `edge.adobedc.net`. Anche se il valore predefinito è accettabile, Adobe considera una best practice impostare un valore specifico per l’organizzazione.

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  edgeDomain: "data.example.com"
});
```

## Dominio Edge tramite l’estensione tag Web SDK

L&#39;estensione tag equivalente a questa proprietà è il campo **[!UICONTROL Edge domain]** nelle [impostazioni di configurazione dell&#39;istanza di SDK](/help/tags/extensions/client/web-sdk/configure/general.md) durante la configurazione dell&#39;estensione.
