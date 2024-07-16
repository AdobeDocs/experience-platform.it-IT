---
title: Autenticazione e accesso all’API di Privacy Service
description: Scopri come eseguire l’autenticazione nell’API Privacy Service e come interpretare le chiamate API di esempio nella documentazione.
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 15%

---

# Autenticazione e accesso all’API di Privacy Service

Questa guida fornisce un’introduzione ai concetti di base che devi conoscere prima di tentare di effettuare chiamate all’API di Adobe Experience Platform Privacy Service.

## Prerequisiti {#prerequisites}

Questa guida richiede una buona conoscenza di [Privacy Service](../home.md) e di come consente di gestire le richieste di accesso ed eliminazione da parte degli interessati (clienti) in tutte le applicazioni Adobe Experience Cloud.

Per creare le credenziali di accesso per l’API, un amministratore dell’organizzazione deve aver precedentemente configurato i profili di prodotto per Privacy Service in Adobe Admin Console. Il profilo di prodotto assegnato a un’integrazione API determina di quali autorizzazioni dispone l’integrazione quando si accede alle funzionalità di Privacy Service. Per ulteriori informazioni, consulta la guida su [gestione delle autorizzazioni di Privacy Service](../permissions.md).

## Raccogliere i valori per le intestazioni richieste {#gather-values-required-headers}

Per effettuare chiamate all’API Privacy Service, devi innanzitutto raccogliere le credenziali di accesso da utilizzare nelle intestazioni richieste:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Questi valori vengono generati utilizzando [Adobe Developer Console](https://developer.adobe.com/console). `{ORG_ID}` e `{API_KEY}` devono essere generati una sola volta e possono essere riutilizzati nelle chiamate API future. Tuttavia, `{ACCESS_TOKEN}` è temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi per generare questi valori sono descritti in dettaglio di seguito.

### Configurazione una tantum {#one-time-setup}

Vai a [Adobe Developer Console](https://developer.adobe.com/console) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nel tutorial su come [creare un progetto vuoto](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/), nella documentazione di Developer Console.

Dopo aver creato un nuovo progetto, seleziona **[!UICONTROL Aggiungi al progetto]** e scegli **[!UICONTROL API]** dal menu a discesa.

![Opzione API selezionata dal menu a discesa [!UICONTROL Aggiungi al progetto] dalla pagina dei dettagli del progetto in Developer Console](../images/api/getting-started/add-api-button.png)

#### Seleziona l’API Privacy Service {#select-privacy-service-api}

Viene visualizzata la schermata **[!UICONTROL Add an API]** (Aggiungi un’API). Seleziona **[!UICONTROL Experience Cloud]** per restringere l&#39;elenco delle API disponibili, quindi seleziona la scheda per **[!UICONTROL API Privacy Service]** prima di selezionare **[!UICONTROL Next]**.

![Scheda API Privacy Service selezionata dall&#39;elenco delle API disponibili](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>Seleziona l&#39;opzione **[!UICONTROL Visualizza documenti]** per passare alla documentazione completa di riferimento dell&#39;[API Privacy Service](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) in una finestra del browser separata.

Quindi, seleziona il tipo di autenticazione per generare token di accesso e accedere all’API Privacy Service.

>[!IMPORTANT]
>
>Selezionare il metodo **[!UICONTROL OAuth Server-to-Server]**, in quanto questo sarà l&#39;unico metodo supportato per gli spostamenti in avanti. Il metodo **[!UICONTROL Service Account (JWT)]** è obsoleto. Anche se le integrazioni che utilizzano il metodo di autenticazione JWT continueranno a funzionare fino al 1° gennaio 2025, Adobe consiglia vivamente di migrare le integrazioni esistenti al nuovo metodo server-to-server OAuth prima di tale data. Ulteriori informazioni nella sezione [!BADGE Obsoleto]{type=negative}[Genera un token Web JSON (JWT)](/help/landing/api-authentication.md#jwt).

![Selezionare il metodo di autenticazione server-to-server Oauth.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### Assegnare autorizzazioni tramite profili di prodotto {#product-profiles}

Il passaggio finale della configurazione consiste nel selezionare i profili di prodotto da cui questa integrazione erediterà le relative autorizzazioni. Se selezioni più di un profilo, i relativi set di autorizzazioni verranno combinati per l’integrazione.

>[!NOTE]
>
I profili di prodotto e le autorizzazioni granulari che forniscono vengono creati e gestiti dagli amministratori tramite Adobe Admin Console. Per ulteriori informazioni, consulta la guida sulle [autorizzazioni Privacy Service](../permissions.md).

Al termine, selezionare **[!UICONTROL Salva API configurata]**.

![Selezione di un singolo profilo di prodotto dall&#39;elenco prima del salvataggio della configurazione](../images/api/getting-started/select-product-profiles.png)

Una volta aggiunta l&#39;API al progetto, nella pagina **[!UICONTROL API Privacy Service]** per il progetto vengono visualizzate le credenziali seguenti, necessarie in tutte le chiamate alle API Privacy Service:

* `{API_KEY}` ([!UICONTROL ID client])
* `{ORG_ID}` ([!UICONTROL ID organizzazione])

![Informazioni sull&#39;integrazione dopo l&#39;aggiunta di un&#39;API in Developer Console.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### Autenticazione per ogni sessione {#authentication-each-session}

L&#39;ultima credenziale richiesta da raccogliere è `{ACCESS_TOKEN}`, utilizzata nell&#39;intestazione Autorizzazione. A differenza dei valori per `{API_KEY}` e `{ORG_ID}`, per continuare a utilizzare l&#39;API è necessario generare un nuovo token ogni 24 ore.

In generale, esistono due metodi per generare un token di accesso:

* [Genera il token manualmente](#manual-token) per il test e lo sviluppo.
* [Generazione automatica dei token](#auto-token) per le integrazioni API.

#### Generare manualmente un token {#manual-token}

Per generare manualmente un nuovo `{ACCESS_TOKEN}`, passa a **[!UICONTROL Credenziali]** > **[!UICONTROL Server-to-Server OAuth]** e seleziona **[!UICONTROL Genera token di accesso]**, come illustrato di seguito.

![Registrazione schermata della modalità di generazione di un token di accesso nell&#39;interfaccia utente di Developer Console.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

Viene generato un nuovo token di accesso, e un pulsante consente di copiarlo negli Appunti. Questo valore viene utilizzato per l’intestazione [!DNL Authorization] richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`.

#### Generazione automatica dei token {#auto-token}

Puoi inoltre utilizzare un ambiente e una raccolta Postman per generare i token di accesso. Per ulteriori informazioni, leggere la sezione relativa all&#39;utilizzo di [Postman per l&#39;autenticazione e il test delle chiamate API](/help/landing/api-authentication.md#use-postman) nella guida di Experience Platform per l&#39;autenticazione API.

## Lettura delle chiamate API di esempio {#read-sample-api-calls}

Ogni guida dell’endpoint fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/api-guide.md#sample-api) nella guida introduttiva per le API di Platform.

## Passaggi successivi {#next-steps}

Ora che sai quali intestazioni utilizzare, puoi iniziare a effettuare chiamate all’API Privacy Service. Seleziona una delle guide endpoint per iniziare:

* [Processi di privacy](./privacy-jobs.md)
* [Consenso](./consent.md)
