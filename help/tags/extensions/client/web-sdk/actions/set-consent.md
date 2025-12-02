---
title: Impostare il consenso
description: Imposta il consenso desiderato per il visitatore.
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Impostare il consenso

L&#39;azione **[!UICONTROL Set consent]** determina se l&#39;estensione tag deve inviare dati (consenso), ignorare dati (rinuncia) o utilizzare [il consenso predefinito](../configure/consent.md) (consenso sconosciuto). Quando un utente consente o nega il consenso sul sito, puoi utilizzare questa azione per sincronizzare le sue preferenze con l’estensione tag. L&#39;equivalente della libreria JavaScript di questa azione è il comando [`setConsent`](/help/collection/js/commands/setconsent.md).

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Imposta il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]**, quindi imposta [!UICONTROL Action type] su **[!UICONTROL Set consent]**.

L’estensione tag supporta i seguenti standard:

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: sono supportati sia gli standard 1.0 che 2.0.
* **[IAB Transparency &amp; Consent Framework](/help/landing/governance-privacy-security/consent/iab/overview.md)**: se utilizzi questo standard, il profilo cliente in tempo reale del visitatore viene aggiornato con le informazioni sul consenso se l&#39;implementazione è configurata correttamente:
   1. Lo schema di profilo individuale XDM contiene il gruppo di campi Consenso [IAB TCF 2.0](/help/xdm/field-groups/profile/iab.md).
   1. Lo schema Experience Event contiene il gruppo di campi Consenso [IAB TCF 2.0](/help/xdm/field-groups/event/iab.md).

Adobe consiglia di memorizzare separatamente le preferenze della finestra di dialogo sul consenso, ad esempio in un elemento dati. L’estensione tag non offre un modo per recuperare il consenso. Per fare in modo che le preferenze utente rimangano sincronizzate con l’estensione tag, puoi eseguire questa azione a ogni caricamento di pagina.

## Campi disponibili

Questo tipo di azione supporta le seguenti opzioni di configurazione:

* **[!UICONTROL Instance]**: l&#39;istanza SDK a cui si applica l&#39;azione. Questo menu a discesa è disattivato se l’implementazione utilizza una singola istanza di SDK.
* **[!UICONTROL Identity map]**: elemento dati che controlla come viene generato un ECID e a quali ID sono associate le informazioni sul consenso.
* **[!UICONTROL Consent information]**: determina se desideri compilare un modulo o fornire un elemento dati contenente le informazioni sul consenso.
* **[!UICONTROL Standard]**: lo standard di consenso che desideri utilizzare. Le opzioni disponibili includono &#39;[!UICONTROL Adobe]&#39; e &#39;[!UICONTROL IAB TCF]&#39;.
* **[!UICONTROL Version]**: versione dello standard di consenso che si desidera utilizzare.
* **[!UICONTROL Datastream configuration overrides]**: questo comando supporta le sostituzioni della configurazione dello stream di dati, consentendoti di controllare quali app e servizi ricevono i dati. Quando imposti una sostituzione della configurazione dello stream di dati sia in un singolo comando che all’interno delle impostazioni di configurazione dell’estensione tag, il singolo comando ha la precedenza. Per ulteriori informazioni, vedere [Override della configurazione Datastream](../configure/configuration-overrides.md).

## Creazione di una regola che aggiorna le informazioni sul consenso

Un momento ideale per utilizzare questa azione è quando le preferenze di consenso di un cliente sono cambiate. Puoi creare una regola di tag per ascoltare questa modifica.

1. All&#39;interno di una proprietà tag, passa a **[!UICONTROL Rules]** e seleziona **[!UICONTROL Add rule]**.
1. Assegnare alla regola il nome desiderato, quindi selezionare l&#39;icona &#39;`+`&#39; accanto a **[!UICONTROL Events]**.
1. Imposta le seguenti proprietà a sinistra:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. Apri l’editor a destra e utilizza il seguente codice come modello:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

1. Seleziona **[!UICONTROL Keep changes]**.

Il blocco di codice personalizzato precedente esegue due operazioni:

* Attiva la regola quando le preferenze di consenso sono cambiate.
* Imposta due elementi dati: **Stringa di consenso TCF IAB** e **RGPD di consenso TCF IAB**.

Questi elementi dati sono utili per impostare l&#39;azione &#39;[!UICONTROL Set Consent]&#39;:

1. Selezionare l&#39;icona &#39;`+`&#39; accanto a **[!UICONTROL Actions]**.
1. Imposta le seguenti proprietà a sinistra:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. Imposta le seguenti proprietà a destra:
   * **[!UICONTROL Standard]**: [!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**: [!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**: [!UICONTROL Provide a data element], con valore `%IAB TCF Consent GDPR%`

![Azione impostazione consenso IAB](../assets/iab-action.png)

>[!NOTE]
>
>Non puoi scegliere questi elementi dati utilizzando il selettore degli elementi dati perché sono stati creati tramite codice personalizzato. Digita il nome dell’elemento dati con i segni di percentuale.
