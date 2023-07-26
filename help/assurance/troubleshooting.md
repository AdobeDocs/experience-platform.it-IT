---
title: Guida alla risoluzione dei problemi di Adobe Experience Platform Assurance
description: Questo documento illustra le soluzioni ai problemi comuni che si verificano quando si utilizza Adobe Experience Platform Assurance.
exl-id: 8078e6f6-ca18-4939-a417-40ebf5a52e24
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '526'
ht-degree: 100%

---

# Risoluzione dei problemi di Adobe Experience Platform Assurance

In caso di problemi con il funzionamento di Assurance, consulta i suggerimenti riportati negli argomenti di seguito per risolvere i problemi più comuni.

Per consentire un’implementazione più fluida e per scoprire eventuali problemi, assicurati che la registrazione SDK sia attivata secondo [Abilita registrazione di debug](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/) nella sezione della Guida introduttiva.

È possibile modificare i livelli di registro dell’SDK utilizzando l’API [`setLogLevel`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setloglevel).

## Problemi sul dispositivo e nell’app

### Il codice QR non apre l’app

* Accedi direttamente al collegamento. Copia il collegamento da **Dettagli sessione**. Incollalo nella barra degli indirizzi del browser del dispositivo per aprirlo. Se non si apre, consulta la sezione [L’app non apre il collegamento](#app-does-not-open-link).
* Utilizza un lettore QR diverso. Per iOS 11 o versioni successive, utilizza l’app foto per leggere il codice QR.

### L’app non apre il collegamento

* Verifica che l’implementazione del deep link sia configurata correttamente nell’app.
   * **Android:** deep link (collegamenti alle app)
      * [Creare deep link al contesto dell’app](https://developer.android.com/training/app-links/deep-linking)
   * **iOS:** schema URL personalizzato o collegamenti universali
      * [Definizione di uno schema URL personalizzato per l’app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app)
      * [Supporto dei collegamenti universali nell’app](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/supporting_universal_links_in_your_app)

>[!INFO]
>
>Per Android, non è necessario chiamare esplicitamente l’API `startSession`. Per iOS, utilizza l’API come descritto in [Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#register-aepassurance-with-mobile-core).

### Viene visualizzata la sovrapposizione dell’autenticazione, ma l’app non riesce a connettersi

* Verifica la connettività Internet del dispositivo tramite il browser web del dispositivo.
* Se l’app non è mai stata connessa correttamente al servizio Assurance, assicurati che sia configurata correttamente per Assurance. Consulta le istruzioni per l’installazione della libreria SDK di [Adobe Experience Platform Assurance](./tutorials/implement-assurance.md).
* Verifica che la sessione corrisponda al collegamento e che venga inserita correttamente per la sessione prevista. Consulta [Messaggio di registro “Informazioni OrgID non disponibili”](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/common-issues/#orgid-information-is-not-available) (non comune e rilevante solo se hai accesso a più di un’istanza ORG).

### Debug di Adobe Analytics

**Stato post-elaborazione - Nessun flag di debug**

Nella vista Eventi di Analytics, se gli eventi non riescono con lo stato post-elaborazione “Nessun flag di debug”, la versione corrente dell’SDK di Adobe Analytics o Assurance potrebbe non supportare la funzione di debug di Analytics.
Per risolvere il problema, aggiorna le estensioni di Adobe Analytics e Assurance SDK alle versioni più recenti.

| Versione minima richiesta | iOS | Android |
| --------------------------- | --- | ------- |
| Adobe Analytics | > 2.4.0 | > 1.2.6 |
| Assurance | > 1.0.0 | > 1.0.0 |

### Compatibilità di React Native MobileCore e AEPAssurance

| Versione di AEP Assurance | Versione Mobile Core | Istruzioni di installazione |
| --------------------- | ------------------- | ------------------- |
| react-native-aepassurance v2.x.x | [react-native-acpcore](https://www.npmjs.com/package/@adobe/react-native-acpcore) | `npm install @adobe/react-native-aepassurance@^2.0.0` <br/>`npm install @adobe/react-native-acpcore` |
| react-native-aepassurance v3.x.x | [react-native-aepcore](https://www.npmjs.com/package/@adobe/react-native-aepcore) | `npm install @adobe/react-native-aepassurance@^3.0.0` <br/>`npm install @adobe/react-native-aepcore` |

Se stai usando `react-native-acpcore` con Assurance, l’applicazione React Native potrebbe non riuscire a generare mostrando uno dei seguenti messaggi di errore:

```
RCTAEPAssurance:  Fatal error: Module 'AEPAssurance' not found
```

oppure

```
AppDelegate: AEPAssurance.h file not found
```

**Soluzione**

In questo caso, esegui il downgrade di `react-native-aepassurance` utilizzando il seguente comando npm:

```shell
npm install @adobe/react-native-aepassurance@^2.0.0
```

Questo errore si verifica perché l’estensione `react-native-acpcore` è **solo** compatibile con le versioni 2.x.x e successive di `react-native-aepassurance`.
