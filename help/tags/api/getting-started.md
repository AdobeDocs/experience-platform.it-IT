---
title: Autenticazione e accesso all’API di Reactor
description: Scopri come iniziare a utilizzare l’API di Reactor, compresi i passaggi per generare le credenziali di accesso richieste.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 47%

---

# Autenticazione e accesso all’API di Reactor

Per utilizzare l&#39;[API Reactor](https://developer.adobe.com/experience-platform-apis/references/reactor/) per creare e gestire le estensioni Tag, ogni richiesta deve includere le intestazioni di autenticazione seguenti:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Questa guida illustra come utilizzare Adobe Developer Console per raccogliere i valori per ciascuna di queste intestazioni, in modo da poter iniziare a effettuare chiamate all’API di Reactor.

## Accesso degli sviluppatori a Adobe Experience Platform {#gain-developer-access}

Prima di poter generare i valori di autenticazione per l’API di Reactor, devi disporre dell’accesso ad Experience Platform come sviluppatore. Per ottenere l’accesso come sviluppatore, segui i passaggi iniziali descritti nel [tutorial sull’autenticazione per Experience Platform](/help/landing/api-authentication.md). Dopo aver completato il passaggio [Accesso utente](/help/landing/api-authentication.md#gain-user-access), torna a questa esercitazione per generare le credenziali specifiche per l&#39;API di Reactor.

## Generare le credenziali di accesso {#generate-access-credentials}

Utilizzando Adobe Developer Console, è necessario generare le tre credenziali di accesso seguenti:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Una volta generati, l&#39;ID organizzazione (`{ORG_ID}`) e la chiave API (`{API_KEY}`) possono essere riutilizzati nelle chiamate API future. Il token di accesso (`{ACCESS_TOKEN}`) è invece temporaneo e deve essere rigenerato ogni 24 ore.

I passaggi per generare questi valori sono descritti in dettaglio di seguito.

### Configurazione una tantum {#one-time-setup}

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nel tutorial su come [creare un progetto vuoto](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/), nella documentazione di Developer Console.

Dopo aver creato un progetto, seleziona **Add API** (Aggiungi API) nella schermata **Project Overview** (Panoramica progetto).

![](../images/api/getting-started/add-api-button.png)

Viene visualizzata la schermata **Add an API** (Aggiungi un’API). Seleziona **Experience Platform Launch API** dall&#39;elenco delle API disponibili prima di selezionare **Next**.

![](../images/api/getting-started/add-launch-api.png)

Quindi, seleziona il tipo di autenticazione per generare token di accesso e accedere all’API di Experience Platform.

>[!IMPORTANT]
>
>Selezionare il metodo **[!UICONTROL OAuth Server-to-Server]**, in quanto questo sarà l&#39;unico metodo supportato per gli spostamenti in avanti. Il metodo **[!UICONTROL Service Account (JWT)]** è obsoleto. Anche se le integrazioni che utilizzano il metodo di autenticazione JWT continueranno a funzionare fino al 1° gennaio 2025, Adobe consiglia vivamente di migrare le integrazioni esistenti al nuovo metodo server-to-server OAuth prima di tale data. Ulteriori informazioni nella sezione [!BADGE Obsoleto]{type=negative}[Generare un token web JSON (JWT)](/help/landing/api-authentication.md#jwt) nell&#39;esercitazione di autenticazione API di Experience Platform.

Seleziona **Avanti** per continuare.

![Selezionare il metodo di autenticazione server-to-server OAuth.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

Nella schermata successiva viene richiesto di selezionare uno o più profili di prodotto da associare all’integrazione API.

>[!NOTE]
>
I profili di prodotto sono gestiti dalla tua organizzazione tramite Adobe Admin Console e contengono set specifici di autorizzazioni per le funzioni granulari. I profili di prodotto e le relative autorizzazioni possono essere gestiti solo da utenti con privilegi di amministratore all’interno della tua organizzazione. Se non sei sicuro dei profili di prodotto da selezionare per l’API, contatta l’amministratore.

Seleziona i profili di prodotto desiderati dall’elenco, quindi seleziona **Save configured API** (Salva API configurata) per completare la registrazione dell’API.

![](../images/api/getting-started/select-product-profile.png)

### Raccogli le credenziali {#gather-credentials}

Una volta aggiunta l&#39;API al progetto, nella pagina **[!UICONTROL API Experience Platform]** per il progetto vengono visualizzate le credenziali seguenti, necessarie in tutte le chiamate alle API Experience Platform:

* `{API_KEY}` ([!UICONTROL ID client])
* `{ORG_ID}` ([!UICONTROL ID organizzazione])

![Informazioni sull&#39;integrazione dopo l&#39;aggiunta di un&#39;API in Developer Console.](/help/tags/images/api/getting-started/api-integration-information.png)

### Generare un token di accesso {#generate-access-token}

Il passaggio successivo consiste nel generare una credenziale `{ACCESS_TOKEN}` da utilizzare nelle chiamate API di Experience Platform. A differenza dei valori per `{API_KEY}` e `{ORG_ID}`, è necessario generare un nuovo token ogni 24 ore per continuare a utilizzare le API di Experience Platform.

>[!TIP]
>
Questi token scadono dopo 24 ore. Se utilizzi questa integrazione per un’applicazione, è consigliabile ottenere il token Bearer a livello di programmazione dall’interno dell’applicazione.

È possibile generare i token di accesso in due modi, a seconda del caso d’uso:

* [Generare i token manualmente](#manual)
* [Generazione automatica dei token](#auto-token)

#### Generare manualmente i token di accesso {#manual}

Per generare manualmente un nuovo `{ACCESS_TOKEN}`, passa a **[!UICONTROL Credenziali]** > **[!UICONTROL Server-to-Server OAuth]** e seleziona **[!UICONTROL Genera token di accesso]**, come illustrato di seguito.

![Registrazione schermata della modalità di generazione del token di accesso e nell&#39;interfaccia utente di Developer Console.](/help/tags/images/api/getting-started/generate-access-token.gif)

Viene generato un nuovo token di accesso, e un pulsante consente di copiarlo negli Appunti. Questo valore viene utilizzato per l&#39;intestazione Autorizzazione richiesta e deve essere fornito nel formato `Bearer {ACCESS_TOKEN}`.

#### Generazione automatica dei token {#auto-token}

Puoi inoltre utilizzare un ambiente e una raccolta Postman per generare i token di accesso. Per ulteriori informazioni, leggere la sezione relativa all&#39;utilizzo di [Postman per l&#39;autenticazione e il test delle chiamate API](/help/landing/api-authentication.md#use-postman) nella guida all&#39;autenticazione API di Experience Platform.

## Verifica credenziali API {#test-api-credentials}

Seguendo i passaggi descritti in questo tutorial, dovresti disporre di valori validi per `{ORG_ID}`, `{API_KEY}` e `{ACCESS_TOKEN}`. Ora puoi testare questi valori utilizzandoli in una semplice richiesta cURL all’API di Reactor.

Per prima cosa, prova ad effettuare una chiamata API per [elencare tutte le aziende](./endpoints/companies.md#list).

>[!NOTE]
>
Se nell’organizzazione non è presente alcuna azienda, la risposta sarà lo stato HTTP 404 (Non trovato). Purché non venga restituito un errore 403 (proibito), le credenziali di accesso sono valide e funzionanti.

Una volta confermato il funzionamento delle credenziali di accesso, continua a esplorare il resto della documentazione sull’API per scoprirne le numerose funzionalità.

## Lettura delle chiamate API di esempio {#read-sample-api-calls}

Ogni guida dell’endpoint fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/api-guide.md#sample-api) nella guida introduttiva per le API di Experience Platform.

## Passaggi successivi {#next-steps}

Ora che sai quali intestazioni utilizzare, puoi iniziare a effettuare chiamate all’API di Reactor. Seleziona una delle guide endpoint per iniziare:

* [Documentazione di riferimento per l&#39;API di Reactor](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Panoramica della guida dell’API di Reactor](/help/tags/api/overview.md)
