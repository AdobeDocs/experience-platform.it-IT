---
keywords: Experience Platform;guida introduttiva;contenuto;tag contenuto
solution: Experience Platform
title: Guida introduttiva all’assegnazione tag dei contenuti
description: L’assegnazione tag dei contenuti utilizza le API Adobe I/O. Per effettuare chiamate alle API Adobe I/O e all’integrazione della console di I/O, devi prima completare il tutorial di autenticazione.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: a42bb4af3ec0f752874827c5a9bf70a66beb6d91
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 7%

---

# Guida introduttiva all’assegnazione tag dei contenuti

[!DNL Content tagging] utilizza le API Adobe I/O. Per effettuare chiamate alle API Adobe I/O e all&#39;integrazione della console di I/O, devi prima completare l&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

Tuttavia, quando arrivi al passaggio **Aggiungi API**, l&#39;API si trova sotto la Creative Cloud invece di Adobe Experience Platform, come mostrato nella schermata seguente:

![aggiunta di tag contenuto](./images/add-api-updated.png)

Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Adobe I/O, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Creazione di un ambiente Postman (facoltativo)

Dopo aver configurato il progetto e l’API in Adobe Developer Console, puoi scaricare un file di ambiente per Postman. In **[!UICONTROL API]** nella barra a sinistra del progetto, seleziona **[!UICONTROL Tag contenuto]**. Verrà aperta una nuova scheda contenente una scheda con etichetta &quot;[!DNL Try it out]&quot;. Seleziona **Scarica per Postman** per scaricare un file JSON utilizzato per configurare l&#39;ambiente postman.

![scarica per postman](./images/add-to-postman-updated.png)

Dopo aver scaricato il file, apri Postman e seleziona l&#39;**icona ingranaggio** in alto a destra per aprire la finestra di dialogo **gestisci ambienti**.

![icona ingranaggio](./images/select-gear-icon.png)

Quindi, seleziona **Importa** dalla finestra di dialogo **Gestisci ambienti**.

![importa](./images/import-updated.png)

Viene eseguito il reindirizzamento e viene richiesto di selezionare un file di ambiente dal computer. Seleziona il file JSON scaricato in precedenza, quindi seleziona **Apri** per caricare l&#39;ambiente.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Sei stato reindirizzato alla scheda *Gestisci ambienti* con un nuovo nome di ambiente popolato. Seleziona il nome dell’ambiente per visualizzare e modificare le variabili disponibili in Postman. È comunque necessario popolare manualmente `JWT_TOKEN` e `ACCESS_TOKEN`. Questi valori avrebbero dovuto essere ottenuti durante il completamento dell&#39;[esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct-updated.png)

Una volta completate, le variabili dovrebbero avere un aspetto simile alla schermata seguente. Seleziona **Aggiorna** per completare la configurazione dell&#39;ambiente.

![](./images/final-environment-updated.png)

Ora puoi selezionare l’ambiente dal menu a discesa nell’angolo in alto a destra e compilare automaticamente tutti i valori salvati. È sufficiente modificare di nuovo i valori in qualsiasi momento per aggiornare tutte le chiamate API.

![esempio](./images/select-environment-updated.png)

Per ulteriori informazioni sull&#39;utilizzo delle API Adobe I/O con Postman, consulta il post di Medium sull&#39;utilizzo di [Postman per l&#39;autenticazione JWT con Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi {#next-steps}

Dopo aver ottenuto tutte le credenziali, è possibile impostare un processo di lavoro personalizzato per [!DNL Content tagging]. I documenti seguenti forniscono informazioni utili per comprendere il framework di estensibilità e la configurazione dell’ambiente.

Per ulteriori informazioni su Extensibility Framework, leggere innanzitutto il documento [introduzione all&#39;estensibilità](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=it). Questo documento illustra i prerequisiti e i requisiti di provisioning.

Per ulteriori informazioni sulla configurazione di un ambiente per [!DNL Content tagging], leggere la guida di [configurazione di un ambiente per sviluppatori](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html?lang=it). Questo documento fornisce istruzioni di configurazione che consentono di sviluppare per il servizio Asset Compute.
