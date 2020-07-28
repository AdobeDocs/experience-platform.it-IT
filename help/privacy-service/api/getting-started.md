---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida per gli sviluppatori di Privacy Service
description: Utilizzare l'API RESTful per gestire i dati personali dei tuoi soggetti di dati nelle applicazioni Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---


# [!DNL Privacy Service] guida per sviluppatori

 Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire (accedere ed eliminare) i dati personali dei soggetti dati (clienti) nelle applicazioni Adobe Experience Cloud. [!DNL Privacy Service] fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono [!DNL Experience Cloud] le applicazioni.

Questa guida illustra come utilizzare l&#39; [!DNL Privacy Service] API. Per informazioni dettagliate sull’utilizzo dell’interfaccia utente, consultate la panoramica [dell’interfaccia utente](../ui/overview.md)Privacy Service. Per un elenco completo di tutti gli endpoint disponibili nell&#39; [!DNL Privacy Service] API, consultate il riferimento [](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza delle [!DNL Experience Platform] funzioni seguenti:

* [!DNL Privacy Service](../home.md): Fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire l&#39;accesso e l&#39;eliminazione delle richieste dagli oggetti dati (clienti) tra le applicazioni Adobe Experience Cloud.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate all&#39;API Privacy Service.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, vedete la sezione [come leggere chiamate](../../landing/troubleshooting.md) API di esempio nella guida alla [!DNL Experience Platform] risoluzione dei problemi.

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate all&#39; [!DNL Privacy Service] API, dovete prima raccogliere le credenziali di accesso da utilizzare nelle intestazioni richieste:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Ciò comporta il conseguimento delle autorizzazioni per lo sviluppatore [!DNL Experience Platform] in Adobe Admin Console, quindi la generazione delle credenziali in  Adobe Developer Console.

### Accesso degli sviluppatori a [!DNL Experience Platform]

Per ottenere l&#39;accesso degli sviluppatori a [!DNL Platform], segui i passaggi iniziali nell&#39; [Experience Platform di esercitazione](../../tutorials/authentication.md)sull&#39;autenticazione. Una volta raggiunto il passaggio &quot;Generate access Credits in  Adobe Developer Console&quot;, tornate a questa esercitazione per generare le credenziali specifiche per [!DNL Privacy Service].

### Genera credenziali di accesso

Utilizzando  Adobe Developer Console, è necessario generare le seguenti tre credenziali di accesso:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

È necessario generare `{IMS_ORG}` e `{API_KEY}` solo una volta e riutilizzarli in chiamate API future. Tuttavia, `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

Le fasi di generazione di questi valori sono descritte in dettaglio di seguito.

#### Configurazione una tantum

Andate a [console](https://www.adobe.com/go/devs_console_ui) Sviluppatore di Adobe ed effettuate l&#39;accesso con il vostro Adobe ID . Attenetevi quindi ai passaggi descritti nell&#39;esercitazione sulla [creazione di un progetto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vuoto nella documentazione di  Adobe Developer Console.

Dopo aver creato un nuovo progetto, fate clic **[!UICONTROL Add API]** sulla _[!UICONTROL Project Overview]_schermata.

![](../images/api/getting-started/add-api-button.png)

Viene _[!UICONTROL Add an API]_visualizzata la schermata. Seleziona **[!UICONTROL Privacy Service API]**dall&#39;elenco delle API disponibili prima di fare clic su **[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Viene _[!UICONTROL Configure API]_visualizzata la schermata. Selezionate l’opzione da **[!UICONTROL Generate a key pair]**, quindi fate clic **[!UICONTROL Generate keypair]**nell’angolo in basso a destra.

![](../images/api/getting-started/generate-key-pair.png)

La coppia di chiavi viene generata automaticamente e un file ZIP contenente una chiave privata e un certificato pubblico viene scaricato nel computer locale (da utilizzare in un secondo momento). Selezionare **[!UICONTROL Save configured API]** per completare la configurazione.

![](../images/api/getting-started/key-pair-generated.png)

Una volta aggiunta l&#39;API al progetto, la pagina del progetto viene nuovamente visualizzata nella pagina di panoramica _dell&#39;API_ Privacy Service. Da qui, scorrete verso il basso fino alla _[!UICONTROL Service Account (JWT)]_sezione, che fornisce le seguenti credenziali di accesso richieste in tutte le chiamate all&#39;[!DNL Privacy Service]API:

* **[!UICONTROL CLIENT ID]**: L&#39;ID client è il valore richiesto `{API_KEY}` per il quale deve essere specificato nell&#39;intestazione x-api-key.
* **[!UICONTROL ORGANIZATION ID]**: L’ID organizzazione è il `{IMS_ORG}` valore che deve essere utilizzato nell’intestazione x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticazione per ogni sessione

L’ultima credenziale richiesta da raccogliere è quella `{ACCESS_TOKEN}`utilizzata nell’intestazione Autorizzazione. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare [!DNL Platform] le API.

Per generare una nuova chiave `{ACCESS_TOKEN}`, aprite la chiave privata precedentemente scaricata e incollatene il contenuto nella casella di testo accanto a _[!UICONTROL Generate access token]_prima di fare clic su **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

Viene generato un nuovo token di accesso e viene fornito un pulsante per copiare il token negli Appunti. Questo valore viene utilizzato per l’intestazione Autorizzazione richiesta e deve essere specificato nel formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Passaggi successivi

Ora che hai compreso quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all&#39; [!DNL Privacy Service] API. Il documento sui processi [di](privacy-jobs.md) privacy illustra le varie chiamate API che potete effettuare tramite l&#39; [!DNL Privacy Service] API. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.
