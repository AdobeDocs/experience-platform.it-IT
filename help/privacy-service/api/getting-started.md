---
title: Guida introduttiva all’API di Privacy Service
description: Scopri come eseguire l’autenticazione nell’API di Privacy Service e come interpretare le chiamate API di esempio nella documentazione.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 14%

---

# Guida introduttiva all’API di Privacy Service

Questa guida fornisce un’introduzione ai concetti di base da conoscere prima di tentare di effettuare chiamate all’API Privacy Service.

## Prerequisiti

Questa guida richiede una buona comprensione delle seguenti funzioni:

* [Adobe Experience Platform Privacy Service](../home.md): Fornisce un’API RESTful e un’interfaccia utente che consentono di gestire le richieste di accesso e di cancellazione dalle persone interessate (clienti) nelle applicazioni Adobe Experience Cloud.

## Raccogli i valori delle intestazioni richieste

Per effettuare chiamate all’API Privacy Service, devi prima raccogliere le credenziali di accesso da utilizzare nelle intestazioni richieste:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Ciò comporta l’ottenimento delle autorizzazioni per gli sviluppatori per Adobe Experience Platform in Adobe Admin Console e la generazione delle credenziali in Adobe Developer Console.

### Accesso degli sviluppatori a Experience Platform

Per ottenere l’accesso degli sviluppatori a [!DNL Platform], segui i passaggi iniziali in [Experience Platform di esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Una volta raggiunto il passaggio &quot;Generate access credentials in Adobe Developer Console&quot; (Genera credenziali di accesso in Console), torna a questa esercitazione per generare le credenziali specifiche di Privacy Service.

### Generare le credenziali di accesso

Utilizzando Adobe Developer Console, è necessario generare le tre credenziali di accesso seguenti:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Le `{ORG_ID}` e `{API_KEY}` deve essere generato solo una volta e può essere riutilizzato nelle chiamate API future. Tuttavia, il tuo `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi per generare questi valori sono descritti in dettaglio di seguito.

#### Configurazione una tantum

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nell’esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione di Adobe Developer Console .

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Aggiungi API]** sulla **[!UICONTROL Panoramica del progetto]** schermo.

![](../images/api/getting-started/add-api-button.png)

Viene visualizzata la schermata **[!UICONTROL Add an API]** (Aggiungi un’API). Seleziona **[!UICONTROL API Privacy Service]** dall’elenco delle API disponibili prima di selezionare **[!UICONTROL Successivo]**.

![](../images/api/getting-started/add-privacy-service-api.png)

La **[!UICONTROL Configurare l’API]** viene visualizzata la schermata . Seleziona l’opzione per **[!UICONTROL Generare una coppia di chiavi]**, quindi seleziona **[!UICONTROL Genera coppia di chiavi]** nell&#39;angolo in basso a destra.

![](../images/api/getting-started/generate-key-pair.png)

La coppia di chiavi viene generata automaticamente e un file ZIP contenente una chiave privata e un certificato pubblico viene scaricato nel computer locale (da utilizzare in un passaggio successivo). Seleziona **[!UICONTROL Salva API configurata]** per completare la configurazione.

![](../images/api/getting-started/key-pair-generated.png)

Una volta aggiunta l’API al progetto, la pagina del progetto viene nuovamente visualizzata nella pagina **Panoramica API di Privacy Service** pagina. Da qui, scorri verso il basso fino al **[!UICONTROL Account di servizio (JWT)]** , che fornisce le seguenti credenziali di accesso necessarie in tutte le chiamate all’API di Privacy Service:

* **[!UICONTROL ID CLIENT]**: L’ID client è il `{API_KEY}` per deve essere fornito nell’intestazione x-api-key.
* **[!UICONTROL ID ORGANIZZAZIONE]**: L&#39;ID organizzazione è il `{ORG_ID}` valore che deve essere utilizzato nell’intestazione x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticazione per ogni sessione

L&#39;ultima credenziale richiesta da raccogliere è la tua `{ACCESS_TOKEN}`, utilizzato nell’intestazione Autorizzazione . A differenza dei valori per `{API_KEY}` e `{ORG_ID}`, per continuare a utilizzare , è necessario generare un nuovo token ogni 24 ore [!DNL Platform] API.

Per generare una nuova `{ACCESS_TOKEN}`, apri la chiave privata scaricata in precedenza e incolla il suo contenuto nella casella di testo accanto a **[!UICONTROL Genera token di accesso]** prima di selezionare **[!UICONTROL Genera token]**.

![](../images/api/getting-started/paste-private-key.png)

Viene generato un nuovo token di accesso, e un pulsante consente di copiarlo negli Appunti. Questo valore viene utilizzato per l&#39;intestazione Autorizzazione richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Lettura di chiamate API di esempio

Questa esercitazione fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/api-guide.md#sample-api) nella guida introduttiva per le API di Platform.

## Passaggi successivi

Ora che conosci le intestazioni da utilizzare, sei pronto per iniziare a effettuare chiamate all’API di Privacy Service. Seleziona una delle guide dell&#39;endpoint da iniziare:

* [Lavori sulla privacy](./privacy-jobs.md)
* [Consenso](./consent.md)
