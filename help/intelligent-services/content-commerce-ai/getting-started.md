---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: Guida introduttiva a Content and Commerce AI]
topic: Getting started
description: Content and Commerce AI utilizza  API I/O Adobe. Per effettuare chiamate alle API I/O  Adobe e all'integrazione della console I/O, è innanzitutto necessario completare l'esercitazione sull'autenticazione.
translation-type: tm+mt
source-git-commit: 9ee888b02b4a402200ca4fcaed4a59c0a7eb94cd
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---


# Getting started with [!DNL Content and Commerce AI]

>[!NOTE]
>
>Content and Commerce AI è in versione beta. La documentazione è soggetta a modifiche.

[!DNL Content and Commerce AI] utilizza  API I/O Adobe. Per effettuare chiamate alle API I/O  Adobe e all&#39;integrazione della console di I/O, è innanzitutto necessario completare l&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione.

Tuttavia, quando si passa al passaggio **Aggiungi API** , l&#39;API si trova in  Experience Cloud invece che in Adobe Experience Platform, come mostrato nella schermata seguente:

![aggiunta di contenuto e AI di Commerce](./images/add-api.png)

Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste in tutte le chiamate API I/O  Adobe, come illustrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Creare un ambiente Postman (facoltativo)

Dopo aver configurato il progetto e l&#39;API in  Adobe Developer Console, potete scaricare un file di ambiente per Postman. Sotto **[!UICONTROL APIs]** la barra a sinistra del progetto, selezionate **[!UICONTROL Content and Commerce AI]**. Si apre una nuova scheda contenente una scheda con etichetta &quot;[!DNL Try it out]&quot;. Selezionate **Scarica per Postman** per scaricare un file JSON usato per configurare l’ambiente postman.

![download per postman](./images/add-to-postman.png)

Dopo aver scaricato il file, apri Postman e seleziona l&#39;icona **** ingranaggio in alto a destra per aprire la finestra di dialogo degli ambienti **di** gestione.

![icona ingranaggio](./images/select-gear-icon.png)

Quindi, selezionate **Importa** dalla finestra di dialogo **Gestisci ambienti** .

![import](./images/import.png)

Viene reindirizzato e viene richiesto di selezionare un file di ambiente dal computer. Selezionate il file JSON scaricato in precedenza, quindi selezionate **Apri** per caricare l’ambiente.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Viene nuovamente eseguito il reindirizzamento alla scheda *Gestisci ambienti* con un nuovo nome di ambiente popolato. Selezionate il nome dell’ambiente per visualizzare e modificare le variabili disponibili in Postman. È comunque necessario compilare manualmente il `JWT_TOKEN` e `ACCESS_TOKEN`. Questi valori avrebbero dovuto essere ottenuti durante il completamento dell&#39;esercitazione [di](../../tutorials/authentication.md)autenticazione.

![](./images/re-direct.png)

Una volta completate, le variabili dovrebbero essere simili a quelle dello screenshot di seguito. Selezionate **Aggiorna** per completare la configurazione dell’ambiente.

![](./images/final-environment.png)

Ora potete selezionare l&#39;ambiente dal menu a discesa nell&#39;angolo in alto a destra e compilare automaticamente tutti i valori salvati. È sufficiente modificare nuovamente i valori in qualsiasi momento per aggiornare tutte le chiamate API.

![esempio](./images/select-environment.png)

Per ulteriori informazioni sull&#39;utilizzo  API I/O di Adobe tramite Postman, vedere il post Medium sull&#39; [uso di Postman per l&#39;autenticazione JWT  Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere le chiamate](../../landing/troubleshooting.md) API di esempio nella guida alla risoluzione dei problemi del Experience Platform .

## Passaggi successivi {#next-steps}

Una volta ottenute tutte le credenziali, è possibile impostare un lavoratore personalizzato per [!DNL Content and Commerce AI]. I documenti seguenti aiutano a comprendere il framework di estensibilità e la configurazione dell&#39;ambiente.

Per ulteriori informazioni sul framework di estensibilità, consultare innanzitutto il documento [introduttivo all’estensibilità](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) . Questo documento descrive i prerequisiti e i requisiti di provisioning.

Per ulteriori informazioni sulla configurazione di un ambiente per [!DNL Content and Commerce AI], consultare la guida alla [configurazione di un ambiente](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html)di sviluppo. Questo documento fornisce istruzioni di configurazione che consentono di sviluppare per il servizio di calcolo delle risorse.