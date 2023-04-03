---
title: Guida alla risoluzione dei problemi di Adobe Experience Platform Assurance
description: Questo documento illustra le soluzioni ai problemi comuni durante l'utilizzo di Adobe Experience Platform Assurance.
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 3%

---


# Risoluzione dei problemi di Adobe Experience Platform Assurance

Se riscontri problemi durante il funzionamento di Assurance, consulta i suggerimenti negli argomenti di problema seguenti per risolvere i problemi più comuni.

Per abilitare un’implementazione più fluida e per scoprire eventuali problemi potenziali, assicurati che la registrazione SDK sia attivata per [Abilita registrazione debug](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) nella sezione Introduzione .

Puoi modificare i livelli di registro SDK utilizzando [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel) API.

## Problemi relativi a dispositivi e app

### Il codice QR non apre l&#39;app

* Accedi direttamente al collegamento. Copia il collegamento da **Dettagli sessione**. Incollalo nella barra degli indirizzi del browser del dispositivo per aprirlo. Se non si apre, consulta la sezione . [L&#39;app non apre il collegamento](#app-does-not-open-link).
* Utilizzare un lettore QR diverso. Per iOS 11 o versione successiva, utilizza l’app Foto per leggere il codice QR.

### L&#39;app non apre il collegamento

* Verifica che l’implementazione dei collegamenti profondi sia configurata correttamente nell’app.
   * **Android:** Collegamenti profondi (collegamenti app)
      * [Creare collegamenti profondi al contesto dell’app](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** Schema URL personalizzato o collegamenti universali
      * [Definizione di uno schema URL personalizzato per l’app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Supporto dei collegamenti universali nell’app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Per Android, la `startSession` L’API non deve essere chiamata esplicitamente. Per iOS, utilizza l’API come descritto in [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Viene visualizzata una sovrapposizione di autenticazione, ma l&#39;app non riesce a connettersi

* Garantire la connettività Internet del dispositivo tramite il browser web del dispositivo.
* Se l’app non si è mai connessa correttamente al servizio Assurance, assicurati che sia configurato correttamente per l’affidabilità. Consulta le istruzioni sull’installazione del [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md) Libreria SDK.
* Verifica che la sessione corrisponda al collegamento e sia inserita correttamente per la sessione prevista. Vedi [Messaggio di log &quot;Le informazioni sull&#39;OrgID non sono disponibili&quot;](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (questo è poco comune e pertinente solo se hai accesso a più di un’istanza ORG).

### Debug in Adobe Analytics

**Stato post-elaborazione - Nessun flag di debug**

Nella visualizzazione Eventi di Analytics, se gli eventi non riescono con lo stato di post-elaborazione &quot;Nessun flag di debug&quot;, la versione corrente di Adobe Analytics o di Assurance SDK potrebbe non supportare la funzione di debug di Analytics.
Aggiorna le estensioni Adobe Analytics e Assurance SDK alle versioni più recenti per risolvere il problema.

| Requisiti minimi di versione | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Reagisce alla compatibilità MobileCore e AEPAsssure nativi

| Versione di AEP Assurance | Versione core per dispositivi mobili | Istruzioni di installazione |
| --------------------- | ------------------- | ------------------- |
| react-native-aepAssurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepAssurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Se utilizzi `react-native-acpcore` con Assurance, l&#39;applicazione React Native può non riuscire a generare con uno dei seguenti messaggi di errore:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

oppure

```
AppDelegate: AEPAssurance.h file not found
```

**Soluzione**

Se si verifica, scarica il tuo `react-native-aepassurance` utilizzando il seguente comando npm:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Questo errore si verifica perché la `react-native-acpcore` estensione **only** compatibile con `react-native-aepassurance` versioni 2.x.x e successive.
