---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Guida per gli sviluppatori di Privacy Service
description: Utilizzare l'API RESTful per gestire i dati personali dei tuoi soggetti di dati nelle applicazioni Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 5d1b22253f2b382bef83e30a4295218ba6b85331
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---


# [!DNL Privacy Service] guida per sviluppatori

Adobe Experience Platform [!DNL Privacy Service] fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire (accedere ed eliminare) i dati personali dei tuoi soggetti dati (clienti) tra le applicazioni Adobe Experience Cloud. [!DNL Privacy Service] fornisce inoltre un meccanismo centrale di controllo e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono  [!DNL Experience Cloud] le applicazioni.

Questa guida illustra come utilizzare l&#39;API [!DNL Privacy Service]. Per informazioni dettagliate sull&#39;utilizzo dell&#39;interfaccia utente, consultate la [panoramica dell&#39;interfaccia utente Privacy Service](../ui/overview.md). Per un elenco completo di tutti gli endpoint disponibili nell&#39;API [!DNL Privacy Service], vedete il riferimento [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml).

## Introduzione {#getting-started}

Questa guida richiede una buona conoscenza delle seguenti funzionalità di [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../home.md): Fornisce un&#39;API RESTful e un&#39;interfaccia utente che consentono di gestire l&#39;accesso e l&#39;eliminazione delle richieste dagli oggetti dati (clienti) tra le applicazioni Adobe Experience Cloud.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per eseguire correttamente le chiamate all&#39;API Privacy Service.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consultate la sezione relativa a [come leggere chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di [!DNL Experience Platform].

## Raccogli valori per le intestazioni richieste

Per effettuare chiamate all&#39;API [!DNL Privacy Service], è innanzitutto necessario raccogliere le credenziali di accesso da utilizzare nelle intestazioni richieste:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Ciò comporta l&#39;ottenimento delle autorizzazioni per lo sviluppatore per [!DNL Experience Platform] nell&#39;Adobe Admin Console, quindi la generazione delle credenziali in  Adobe Developer Console.

### Accesso degli sviluppatori a [!DNL Experience Platform]

Per ottenere l&#39;accesso degli sviluppatori a [!DNL Platform], segui i passaggi iniziali nell&#39; [ esercitazione sull&#39;autenticazione del Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Una volta raggiunto il passaggio &quot;Generate access Credits in  Adobe Developer Console&quot;, tornate a questa esercitazione per generare le credenziali specifiche per [!DNL Privacy Service].

### Genera credenziali di accesso

Utilizzando  Adobe Developer Console, è necessario generare le seguenti tre credenziali di accesso:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Le `{IMS_ORG}` e `{API_KEY}` devono essere generate una sola volta e possono essere riutilizzate nelle chiamate API future. Tuttavia, il `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

Le fasi di generazione di questi valori sono descritte in dettaglio di seguito.

#### Configurazione una tantum

Andate a [ Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) ed effettuate l&#39;accesso con il vostro Adobe ID . Seguite quindi i passaggi descritti nell&#39;esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione  Developer Console.

Dopo aver creato un nuovo progetto, selezionate **[!UICONTROL Add API]** nella schermata **[!UICONTROL Project Overview]**.

![](../images/api/getting-started/add-api-button.png)

Viene visualizzata la schermata **[!UICONTROL Add an API]**. Selezionare **[!UICONTROL Privacy Service API]** dall&#39;elenco delle API disponibili prima di selezionare **[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Viene visualizzata la schermata **[!UICONTROL Configure API]**. Selezionare l&#39;opzione su **[!UICONTROL Generate a key pair]**, quindi selezionare **[!UICONTROL Generate keypair]** nell&#39;angolo inferiore destro.

![](../images/api/getting-started/generate-key-pair.png)

La coppia di chiavi viene generata automaticamente e un file ZIP contenente una chiave privata e un certificato pubblico viene scaricato nel computer locale (da utilizzare in un secondo momento). Selezionare **[!UICONTROL Save configured API]** per completare la configurazione.

![](../images/api/getting-started/key-pair-generated.png)

Una volta aggiunta l&#39;API al progetto, la pagina del progetto viene nuovamente visualizzata nella pagina **Panoramica API Privacy Service**. Da qui, scorrete verso il basso fino alla sezione **[!UICONTROL Service Account (JWT)]**, che fornisce le seguenti credenziali di accesso necessarie in tutte le chiamate all&#39;API [!DNL Privacy Service]:

* **[!UICONTROL CLIENT ID]**: L&#39;ID client è il valore richiesto  `{API_KEY}` per il quale deve essere specificato nell&#39;intestazione x-api-key.
* **[!UICONTROL ORGANIZATION ID]**: L’ID organizzazione è il  `{IMS_ORG}` valore che deve essere utilizzato nell’intestazione x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticazione per ogni sessione

L&#39;ultima credenziale richiesta da raccogliere è la `{ACCESS_TOKEN}` utilizzata nell&#39;intestazione Autorizzazione. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare le API [!DNL Platform].

Per generare una nuova `{ACCESS_TOKEN}`, aprite la chiave privata precedentemente scaricata e incollatene il contenuto nella casella di testo accanto a **[!UICONTROL Generate access token]** prima di selezionare **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

Viene generato un nuovo token di accesso e viene fornito un pulsante per copiare il token negli Appunti. Questo valore viene utilizzato per l&#39;intestazione Autorizzazione richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Passaggi successivi

Ora che hai compreso quali intestazioni utilizzare, sei pronto a iniziare a effettuare chiamate all&#39;API [!DNL Privacy Service]. Il documento sui [processi di privacy](privacy-jobs.md) illustra le diverse chiamate API che potete effettuare utilizzando l&#39;API [!DNL Privacy Service]. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.
