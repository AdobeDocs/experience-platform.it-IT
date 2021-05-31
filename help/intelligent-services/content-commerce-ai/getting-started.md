---
keywords: Experience Platform;guida introduttiva;contenuto ai;e-commerce;contenuti e commerce ai
solution: Experience Platform, Intelligent Services
title: Guida introduttiva a Content and Commerce AI
topic-legacy: Getting started
description: Content and Commerce AI utilizza le API di Adobe I/O. Per effettuare chiamate alle API di Adobe I/O e all’integrazione della console I/O, devi prima completare l’esercitazione sull’autenticazione.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---

# Guida introduttiva a Content and Commerce AI

>[!NOTE]
>
>Content and Commerce AI è in versione beta. La documentazione è soggetta a modifiche.

[!DNL Content and Commerce AI] utilizza le API di Adobe I/O. Per effettuare chiamate alle API di Adobe I/O e all’integrazione della console I/O, devi prima completare l’ [esercitazione sull’autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

Tuttavia, quando passi il passaggio **Aggiungi API**, l&#39;API si trova in Experience Cloud invece di Adobe Experience Platform, come mostrato nella schermata seguente:

![aggiunta di Content and Commerce AI](./images/add-api.png)

Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Adobe I/O, come mostrato di seguito:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Creare un ambiente Postman (facoltativo)

Dopo aver configurato il progetto e l’API in Adobe Developer Console, è possibile scaricare un file di ambiente per Postman. In **[!UICONTROL API]** la barra a sinistra del progetto, seleziona **[!UICONTROL Content and Commerce AI]**. Viene visualizzata una nuova scheda contenente una scheda con etichetta &quot;[!DNL Try it out]&quot;. Seleziona **Scarica per Postman** per scaricare un file JSON utilizzato per configurare l&#39;ambiente postman.

![scaricare per postman](./images/add-to-postman.png)

Dopo aver scaricato il file, apri Postman e seleziona l&#39; **icona ingranaggio** in alto a destra per aprire la finestra di dialogo **gestione ambienti**.

![icona ingranaggio](./images/select-gear-icon.png)

Quindi, seleziona **Importa** dalla finestra di dialogo **Gestisci ambienti**.

![importare](./images/import.png)

Viene reindirizzato e viene richiesto di selezionare un file di ambiente dal computer. Seleziona il file JSON scaricato in precedenza, quindi seleziona **Apri** per caricare l&#39;ambiente.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Verrai reindirizzato alla scheda *Gestisci ambienti* con un nuovo nome di ambiente popolato. Seleziona il nome dell’ambiente per visualizzare e modificare le variabili disponibili in Postman. È comunque necessario compilare manualmente i campi `JWT_TOKEN` e `ACCESS_TOKEN`. Questi valori avrebbero dovuto essere ottenuti durante il completamento dell&#39; [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en).

![](./images/re-direct.png)

Una volta completate, le variabili dovrebbero avere un aspetto simile alla schermata sottostante. Seleziona **Aggiorna** per completare la configurazione dell&#39;ambiente.

![](./images/final-environment.png)

Ora puoi selezionare l’ambiente dal menu a discesa nell’angolo in alto a destra e compilare automaticamente i valori salvati. È sufficiente modificare nuovamente i valori in qualsiasi momento per aggiornare tutte le chiamate API.

![esempio](./images/select-environment.png)

Per ulteriori informazioni sulle operazioni con le API di Adobe I/O utilizzando Postman, consulta il post di supporto su [uso di Postman per l’autenticazione JWT su Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere le chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi {#next-steps}

Una volta ottenute tutte le credenziali, è possibile impostare un processo di lavoro personalizzato per [!DNL Content and Commerce AI]. Nei documenti seguenti viene fornita assistenza per comprendere il Framework di estensibilità e la configurazione dell&#39;ambiente.

Per ulteriori informazioni sul framework di estensibilità, leggere il documento [introduzione all&#39;estensibilità](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html). Questo documento illustra i prerequisiti e i requisiti di provisioning.

Per ulteriori informazioni sulla configurazione di un ambiente per [!DNL Content and Commerce AI], leggi la guida per [la configurazione di un ambiente per sviluppatori](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Questo documento fornisce istruzioni di configurazione che consentono di sviluppare per il servizio Asset compute.
