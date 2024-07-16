---
description: Questa pagina descrive come eseguire l’autenticazione e iniziare a utilizzare il Adobe Experience Platform Destination SDK. Include istruzioni su come ottenere le credenziali di autenticazione Adobe I/O, il nome di una sandbox e l’autorizzazione di controllo dell’accesso per l’authoring della destinazione.
title: Guida introduttiva a Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 7c1d956e3b6a1314baa13fef823d73d42404516a
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Introduzione

## Panoramica {#overview}

Questa pagina descrive come eseguire l’autenticazione e iniziare a utilizzare il Adobe Experience Platform Destination SDK. Include istruzioni su come ottenere le credenziali di autenticazione Adobe I/O, il nome di una sandbox e l’autorizzazione di controllo dell’accesso per l’authoring della destinazione.

## Terminologia {#terminology}

Questa guida utilizza concetti specifici di Platform, ad esempio organizzazione e sandbox. Consulta il [glossario di Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) per le definizioni di questi e altri termini.

## Ottenere le credenziali di autenticazione richieste {#obtain-authentication-credentials}

Destination SDK utilizza il gateway [Adobe I/O](https://www.adobe.io/) per l&#39;autenticazione. Per effettuare chiamate API agli endpoint Destination SDK, devi fornire determinate intestazioni nelle chiamate API. Collabora con il team di Adobi Exchange per configurare l&#39;autenticazione per te in [Adobe Developer Console](https://developer.adobe.com/console).

Per effettuare correttamente le chiamate agli endpoint API Destination SDK, segui l&#39;[esercitazione di autenticazione di Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=it). Avvia l&#39;esercitazione dal passaggio &quot;[Generate an API key, organization ID, and client secret](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot; (Genera una chiave API, un ID organizzazione e un segreto client). Il team di Adobe Exchange gestirà i passaggi precedenti per te. Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API Destination SDK, come mostrato di seguito:

* `x-api-key: {API_KEY}`, noto anche come ID client
* `x-gw-ims-org-id: {ORG_ID}`, noto anche come ID organizzazione
* `Authorization: Bearer {ACCESS_TOKEN}`. Il token di accesso ha una scadenza di 24 ore, espressa in millisecondi, pertanto dovrai aggiornarlo. Per aggiornare il token di accesso, ripeti i passaggi descritti nel tutorial sull’autenticazione.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Proprietà della destinazione e sandbox {#destination-ownership}

Tutte le risorse in Experience Platform sono isolate in specifiche sandbox virtuali. Le richieste di Destination SDK richiedono intestazioni che specificano il nome della sandbox in cui si svolge l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Il team di Adobi Exchange fornisce il nome della sandbox, che è necessario utilizzare nelle chiamate agli endpoint API Destination SDK.

## Controllo degli accessi basato sul ruolo (RBAC) {#rbac}

Per utilizzare gli endpoint API Destination SDK descritti nella [documentazione di riferimento](functionality/configuration-options.md), è necessario disporre dell&#39;autorizzazione per il controllo degli accessi **[!UICONTROL Authoring delle destinazioni]**. Collabora con il team di Adobi Exchange per ottenere questa autorizzazione in [Adobe Admin Console](https://adminconsole.adobe.com/).

![Autorizzazione per l&#39;authoring delle destinazioni](./assets/destination-authoring-permission.png)

Per ulteriori informazioni, leggere i seguenti Experienci Platform di documenti di controllo dell&#39;accesso:

* [Gestire le autorizzazioni per un profilo di prodotto](/help/access-control/ui/permissions.md)
* [Autorizzazioni disponibili per Experience Platform](/help/access-control/home.md#permissions)
* [Documentazione di Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html)

## Considerazioni aggiuntive {#additional-considerations}

* Per le destinazioni prodotte/pubbliche, tutte le modifiche apportate alle configurazioni di destinazione, sia che si crei o modifichi una configurazione di destinazione, devono essere riviste e approvate da Adobe. Le modifiche vengono applicate alle destinazioni solo al termine della revisione. Questo non si applica alle destinazioni private che sono disponibili solo per te.
* Solo gli utenti che appartengono alla stessa organizzazione e hanno accesso alla sandbox possono modificare la configurazione di destinazione.

## Passaggi successivi {#next-steps}

Seguendo i passaggi descritti in questo articolo, hai ottenuto le credenziali di autenticazione per Adobe I/O, un nome di sandbox e l’autorizzazione di controllo dell’accesso per l’authoring della destinazione. Successivamente, puoi impostare una destinazione utilizzando Destination SDK.

* Leggi le seguenti guide di configurazione, a seconda del tipo di destinazione:

   * [Utilizzare Destination SDK per configurare una destinazione di streaming](guides/configure-destination-instructions.md)
   * [Utilizzare Destination SDK per configurare una destinazione basata su file](guides/configure-file-based-destination-instructions.md)

* Per tutte le operazioni, consulta la [documentazione API di authoring delle destinazioni](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Utilizza la [raccolta Postman API per l&#39;authoring delle destinazioni](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) per configurare la tua destinazione utilizzando gli endpoint API di Destination SDK. Per iniziare a utilizzare Postman, consulta i [passaggi per importare ambienti e raccolte](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) e una [guida video per la creazione dell&#39;ambiente Postman](https://video.tv.adobe.com/v/28832).
