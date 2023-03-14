---
title: Guida introduttiva all’API di Privacy Service
description: Scopri come eseguire l’autenticazione nell’API Privacy Service e come interpretare le chiamate API di esempio nella documentazione.
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 10%

---

# Guida introduttiva all’API di Privacy Service

Questa guida fornisce un’introduzione ai concetti di base che è necessario conoscere prima di tentare di effettuare chiamate all’API di Adobe Experience Platform Privacy Service.

## Prerequisiti

Questa guida richiede una buona conoscenza di [Privacy Service](../home.md) e come consente di gestire le richieste di accesso ed eliminazione da parte degli interessati (clienti) in tutte le applicazioni Adobe Experience Cloud.

Per creare le credenziali di accesso per l’API, un amministratore dell’organizzazione deve aver precedentemente configurato i profili di prodotto per Privacy Service in Adobe Admin Console. Il profilo di prodotto assegnato a un’integrazione API determina di quali autorizzazioni dispone l’integrazione quando si accede alle funzionalità di Privacy Service. Consulta la guida su [gestione delle autorizzazioni di Privacy Service](../permissions.md) per ulteriori informazioni.

## Raccogli i valori per le intestazioni richieste

Per effettuare chiamate all’API Privacy Service, devi innanzitutto raccogliere le credenziali di accesso da utilizzare nelle intestazioni richieste:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Questi valori vengono generati utilizzando [Console Adobe Developer](https://developer.adobe.com/console). Il tuo `{ORG_ID}` e `{API_KEY}` deve essere generato una sola volta e può essere riutilizzato nelle chiamate API future. Tuttavia, `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi per generare questi valori sono descritti in dettaglio di seguito.

### Configurazione una tantum

Vai a [Adobe Developer Console](https://developer.adobe.com/console) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nel tutorial su come [creare un progetto vuoto](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/), nella documentazione di Developer Console.

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Aggiungi al progetto]** e scegli **[!UICONTROL API]** dal menu a discesa.

![L’opzione API selezionata da [!UICONTROL Aggiungi al progetto] dalla pagina dei dettagli del progetto in Console sviluppatori](../images/api/getting-started/add-api-button.png)

#### Seleziona un’API e genera una coppia di chiavi {#keypair}

Viene visualizzata la schermata **[!UICONTROL Add an API]** (Aggiungi un’API). Seleziona **[!UICONTROL Experience Cloud]** per limitare l’elenco delle API disponibili, seleziona la scheda per **[!UICONTROL API PRIVACY SERVICE]** prima di selezionare **[!UICONTROL Successivo]**.

![La scheda API Privacy Service selezionata dall’elenco delle API disponibili](../images/api/getting-started/add-privacy-service-api.png)

Il **[!UICONTROL Configurare API]** viene visualizzata la schermata. Seleziona l’opzione per **[!UICONTROL Generare una coppia di chiavi]**, quindi seleziona **[!UICONTROL Genera coppia di chiavi]**.

![Il [!UICONTROL Generare una coppia di chiavi] opzione selezionata sul [!UICONTROL Configurare API] screen](../images/api/getting-started/generate-key-pair.png)

La coppia di chiavi viene generata automaticamente e un file ZIP contenente una chiave privata e un certificato pubblico viene scaricato dal browser (da utilizzare in un passaggio successivo). Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![La coppia di chiavi generata visualizzata nell’interfaccia utente, i cui valori vengono scaricati automaticamente dal browser](../images/api/getting-started/key-pair-generated.png)

#### Assegnare autorizzazioni tramite profili di prodotto {#product-profiles}

Il passaggio finale della configurazione consiste nel selezionare i profili di prodotto da cui questa integrazione erediterà le relative autorizzazioni. Se selezioni più di un profilo, i relativi set di autorizzazioni verranno combinati per l’integrazione.

>[!NOTE]
>
>I profili di prodotto e le autorizzazioni granulari che forniscono vengono creati e gestiti dagli amministratori tramite Adobe Admin Console. Consulta la guida su [Autorizzazioni Privacy Service](../permissions.md) per ulteriori informazioni.

Al termine, seleziona **[!UICONTROL Salva API configurata]**.

![Un singolo profilo di prodotto selezionato dall’elenco prima di salvare la configurazione](../images/api/getting-started/select-product-profiles.png)

Una volta aggiunta l’API al progetto, la pagina del progetto viene visualizzata di nuovo sul **Panoramica API di Privacy Service** pagina. Da qui, scorri verso il basso fino a **[!UICONTROL Account di servizio (JWT)]** , che fornisce le seguenti credenziali di accesso necessarie in tutte le chiamate all’API Privacy Service:

* **[!UICONTROL ID CLIENT]**: l’ID client è il valore obbligatorio `{API_KEY}` che devono essere fornite nella `x-api-key` intestazione.
* **[!UICONTROL ORGANIZATION ID]**: l’ID organizzazione è il valore `{ORG_ID}` che deve essere utilizzato nell’intestazione `x-gw-ims-org-id`.

![I valori ID client e ID organizzazione visualizzati nella pagina di panoramica del progetto dopo la configurazione dell’API](../images/api/getting-started/jwt-credentials.png)

### Autenticazione per ogni sessione

L&#39;ultima credenziale richiesta da raccogliere è la tua `{ACCESS_TOKEN}`, utilizzato nell’intestazione Autorizzazione. A differenza dei valori per `{API_KEY}` e `{ORG_ID}`, per continuare a utilizzare l’API è necessario generare un nuovo token ogni 24 ore.

In generale, esistono due metodi per generare un token di accesso:

* [Generare manualmente il token](#manual-token) per test e sviluppo.
* [Generazione automatica dei token](#auto-token) per le integrazioni API.

#### Generare manualmente un token {#manual-token}

Per generare manualmente un nuovo `{ACCESS_TOKEN}`, apri la chiave privata scaricata in precedenza e incollane il contenuto nella casella di testo accanto **[!UICONTROL Genera token di accesso]** prima di selezionare **[!UICONTROL Genera token]**.

![Il token di accesso generato in precedenza viene incollato nella pagina della panoramica del progetto, con il [!UICONTROL Genera token] pulsante selezionato dopo](../images/api/getting-started/paste-private-key.png)

Viene generato un nuovo token di accesso, e un pulsante consente di copiarlo negli Appunti. Questo valore viene utilizzato per l’intestazione Autorizzazione richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`.

![Token di accesso generato copiato dall’interfaccia utente](../images/api/getting-started/generated-access-token.png)

#### Generazione automatica dei token {#auto-token}

Puoi generare nuovi token di accesso per i processi automatizzati inviando un token web JSON (JWT) tramite una richiesta POST ad Adobe Identity Management Service (IMS). Consulta il documento Console sviluppatori su [Autenticazione JWT](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) per i passaggi dettagliati.

## Lettura delle chiamate API di esempio

Ogni guida dell’endpoint fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito il codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/api-guide.md#sample-api) nella guida introduttiva per le API di Platform.

## Passaggi successivi

Ora che sai quali intestazioni utilizzare, puoi iniziare a effettuare chiamate all’API Privacy Service. Seleziona una delle guide endpoint per iniziare:

* [Lavori sulla privacy](./privacy-jobs.md)
* [Consenso](./consent.md)
