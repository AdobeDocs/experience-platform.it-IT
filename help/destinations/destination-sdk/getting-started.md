---
description: Questa pagina descrive come autenticare e iniziare a utilizzare l'SDK di destinazione di Adobe Experience Platform. Include istruzioni su come ottenere le credenziali di autenticazione di Adobe I/O, un nome sandbox e l’autorizzazione per il controllo degli accessi per l’authoring di destinazione.
title: Guida introduttiva all’SDK per destinazione
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 2%

---

# Introduzione

## Panoramica {#overview}

Questa pagina descrive come autenticare e iniziare a utilizzare l&#39;SDK di destinazione di Adobe Experience Platform. Include istruzioni su come ottenere le credenziali di autenticazione di Adobe I/O, un nome sandbox e l’autorizzazione per il controllo degli accessi per l’authoring di destinazione.

## Terminologia {#terminology}

Questa guida utilizza concetti specifici di Platform, come l’organizzazione IMS e le sandbox. Consulta il [glossario di Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) per le definizioni di questi e altri termini.

## Ottieni le credenziali di autenticazione richieste {#obtain-authentication-credentials}

L&#39;SDK di destinazione utilizza il gateway [Adobe I/O](https://www.adobe.io/) per l&#39;autenticazione. Per effettuare chiamate API agli endpoint SDK di destinazione, devi fornire determinate intestazioni nelle chiamate API. Collabora con il team di Adobe Exchange per configurare l&#39;autenticazione per l&#39;utente in [Adobe Developer Console](http://console.adobe.io/).

Per effettuare correttamente le chiamate agli endpoint API dell&#39;SDK di destinazione, segui il [tutorial sull&#39;autenticazione di Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html). Avvia l&#39;esercitazione dal passaggio &quot;[Genera una chiave API, un ID organizzazione IMS e un segreto client](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot;. Il team di Adobe Exchange gestirà i passaggi precedenti. Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste nelle chiamate API dell’SDK di destinazione, come mostrato di seguito:

* `x-api-key: {API_KEY}`, noto anche come ID client
* `x-gw-ims-org-id: {IMS_ORG}`, indicato anche come ID organizzazione
* `Authorization: Bearer {ACCESS_TOKEN}`. Il token di accesso ha un tempo di scadenza di 24 ore, espresso in millisecondi, quindi dovrai aggiornarlo. Per aggiornare il token di accesso, ripeti i passaggi descritti nell’esercitazione sull’autenticazione.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Proprietà e sandbox di destinazione {#destination-ownership}

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Le richieste all’SDK di destinazione richiedono intestazioni che specificano il nome della sandbox in cui si svolge l’operazione:

* `x-sandbox-name: {SANDBOX_NAME}`

Il team Adobe Exchange ti fornisce il nome della sandbox, che devi utilizzare nelle chiamate agli endpoint dell’API SDK di destinazione.

## Controllo dell&#39;accesso basato sul ruolo (RBAC) {#rbac}

Per utilizzare gli endpoint dell&#39;API SDK di destinazione descritti nella [documentazione di riferimento](./configuration-options.md), è necessario disporre dell&#39;autorizzazione per il controllo degli accessi **[!UICONTROL Authoring delle destinazioni]**. Collabora con il team di Adobe Exchange per ottenere questa autorizzazione assegnata in [Adobe Admin Console](https://adminconsole.adobe.com/).

![Autorizzazione per l’authoring delle destinazioni](./assets/destination-authoring-permission.png)

Per ulteriori informazioni, consultare i seguenti documenti di Experience Platform sul controllo degli accessi:

* [Gestire le autorizzazioni per un profilo di prodotto](/help/access-control/ui/permissions.md)
* [Autorizzazioni disponibili per Experience Platform](/help/access-control/home.md#permissions)
* [Documentazione di Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html)

## Considerazioni aggiuntive {#additional-considerations}

* Qualsiasi modifica apportata alle configurazioni di destinazione, sia che crei o modifichi una configurazione di destinazione, deve essere rivista e approvata mediante Adobe. Le modifiche si riflettono nelle destinazioni solo dopo la revisione.
* Solo gli utenti che appartengono alla stessa organizzazione e hanno accesso alla sandbox possono modificare la configurazione di destinazione.

## Passaggi successivi {#next-steps}

Seguendo i passaggi descritti in questo articolo, hai ottenuto le credenziali di autenticazione per Adobe I/O, un nome sandbox e l’autorizzazione per il controllo degli accessi per l’authoring della destinazione. Successivamente, puoi impostare una destinazione utilizzando l’SDK di destinazione. Leggi [Usa SDK di destinazione per configurare la destinazione](./configure-destination-instructions.md) per i passaggi successivi.
