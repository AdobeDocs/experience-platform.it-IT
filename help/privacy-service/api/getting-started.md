---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Guida all’API di Privacy Service
description: L’API di Privacy Service consente agli sviluppatori di creare e gestire le richieste dei clienti per accedere o eliminare i propri dati personali tra le applicazioni Experience Cloud, in conformità alle normative sulla privacy legali. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# [!DNL Privacy Service] Guida all’API

Adobe Experience Platform [!DNL Privacy Service] fornisce un’API RESTful e un’interfaccia utente che consentono di gestire (accedere e cancellare) i dati personali delle persone interessate (clienti) nelle applicazioni Adobe Experience Cloud. [!DNL Privacy Service] fornisce inoltre un meccanismo centrale di audit e registrazione che consente di accedere allo stato e ai risultati dei processi che coinvolgono  [!DNL Experience Cloud] le applicazioni.

Questa guida illustra come utilizzare l’ API [!DNL Privacy Service] . Per informazioni dettagliate sull&#39;utilizzo dell&#39;interfaccia utente, consulta [Panoramica dell&#39;interfaccia utente di Privacy Service](../ui/overview.md). Per un elenco completo di tutti gli endpoint disponibili nell’ API [!DNL Privacy Service], consulta il [riferimento API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml).

## Introduzione {#getting-started}

Questa guida richiede una buona comprensione delle seguenti funzioni [!DNL Experience Platform] :

* [[!DNL Privacy Service]](../home.md): Fornisce un’API RESTful e un’interfaccia utente che consentono di gestire le richieste di accesso e di cancellazione dalle persone interessate (clienti) nelle applicazioni Adobe Experience Cloud.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate all’API Privacy Service.

### Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di [!DNL Experience Platform] .

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate all&#39;API [!DNL Privacy Service], devi prima raccogliere le credenziali di accesso da utilizzare nelle intestazioni richieste:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Ciò comporta l’ottenimento delle autorizzazioni per gli sviluppatori per [!DNL Experience Platform] in Adobe Admin Console e la generazione delle credenziali in Adobe Developer Console.

### Accesso degli sviluppatori a [!DNL Experience Platform]

Per ottenere l&#39;accesso degli sviluppatori a [!DNL Platform], segui i passaggi iniziali nell&#39; [esercitazione sull&#39;autenticazione Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Una volta raggiunto il passaggio &quot;Generate access credentials in Adobe Developer Console&quot; (Genera credenziali di accesso in Developer Console), torna a questa esercitazione per generare le credenziali specifiche di [!DNL Privacy Service].

### Genera credenziali di accesso

Utilizzando Adobe Developer Console, è necessario generare le tre credenziali di accesso seguenti:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

I `{IMS_ORG}` e `{API_KEY}` devono essere generati una sola volta e possono essere riutilizzati in chiamate API future. Tuttavia, il tuo `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi per generare questi valori sono descritti in dettaglio di seguito.

#### Configurazione una tantum

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nell’esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione di Adobe Developer Console.

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Add API]** nella schermata **[!UICONTROL Project Overview]** .

![](../images/api/getting-started/add-api-button.png)

Viene visualizzata la schermata **[!UICONTROL Add an API]**. Seleziona **[!UICONTROL Privacy Service API]** dall’elenco delle API disponibili prima di selezionare **[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Viene visualizzata la schermata **[!UICONTROL Configure API]**. Seleziona l’opzione **[!UICONTROL Generate a key pair]**, quindi seleziona **[!UICONTROL Generate keypair]** nell’angolo in basso a destra.

![](../images/api/getting-started/generate-key-pair.png)

La coppia di chiavi viene generata automaticamente e un file ZIP contenente una chiave privata e un certificato pubblico viene scaricato nel computer locale (da utilizzare in un passaggio successivo). Seleziona **[!UICONTROL Save configured API]** per completare la configurazione.

![](../images/api/getting-started/key-pair-generated.png)

Una volta aggiunta l’API al progetto, la pagina del progetto viene nuovamente visualizzata nella pagina **Panoramica API di Privacy Service** . Da qui, scorri verso il basso fino alla sezione **[!UICONTROL Service Account (JWT)]** , che fornisce le seguenti credenziali di accesso necessarie in tutte le chiamate all’ API [!DNL Privacy Service] :

* **[!UICONTROL CLIENT ID]**: L’ID client è il necessario  `{API_KEY}` per deve essere fornito nell’intestazione x-api-key.
* **[!UICONTROL ORGANIZATION ID]**: L&#39;ID organizzazione è il  `{IMS_ORG}` valore che deve essere utilizzato nell&#39;intestazione x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticazione per ogni sessione

L’ultima credenziale richiesta da raccogliere è la tua `{ACCESS_TOKEN}`, utilizzata nell’intestazione Autorizzazione. A differenza dei valori per `{API_KEY}` e `{IMS_ORG}`, per continuare a utilizzare le API [!DNL Platform] è necessario generare un nuovo token ogni 24 ore.

Per generare una nuova `{ACCESS_TOKEN}`, apri la chiave privata scaricata in precedenza e incolla il relativo contenuto nella casella di testo accanto a **[!UICONTROL Generate access token]** prima di selezionare **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

Viene generato un nuovo token di accesso e viene fornito un pulsante per copiare il token negli Appunti. Questo valore viene utilizzato per l’intestazione Autorizzazione richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Passaggi successivi

Ora che conosci le intestazioni da utilizzare, sei pronto per iniziare a effettuare chiamate all’ API [!DNL Privacy Service]. Il documento sui [lavori sulla privacy](privacy-jobs.md) illustra le varie chiamate API che puoi effettuare utilizzando l&#39;API [!DNL Privacy Service]. Ogni chiamata di esempio include il formato API generale, una richiesta di esempio che mostra le intestazioni richieste e una risposta di esempio.
