---
keywords: Experience Platform;home;argomenti popolari;intervallo date
title: Iscriviti alle notifiche degli eventi di Adobe I/O
description: Questo documento descrive come abbonarsi alle notifiche di eventi Adobe I/O per i servizi Adobe Experience Platform. Vengono inoltre fornite informazioni di riferimento sui tipi di evento disponibili, insieme ai collegamenti a ulteriore documentazione su come interpretare i dati evento restituiti per ogni evento applicabile [!DNL Platform] servizio.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 3%

---

# Abbonati alle notifiche di eventi di Adobe I/O

[!DNL Observability Insights] ti consente di abbonarti alle notifiche degli eventi di Adobe I/O relative alle attività di Adobe Experience Platform. Questi eventi vengono inviati a un webhook configurato per facilitare l’automazione efficiente del monitoraggio delle attività.

Questo documento descrive come abbonarsi alle notifiche di eventi Adobe I/O per i servizi Adobe Experience Platform. Vengono inoltre fornite informazioni di riferimento sui tipi di evento disponibili, insieme ai collegamenti a ulteriore documentazione su come interpretare i dati evento restituiti per ogni evento applicabile [!DNL Platform] servizio.

## Introduzione

Questo documento richiede una buona conoscenza dei webhook e di come collegarli da un&#39;applicazione a un&#39;altra. Consulta la sezione [[!DNL I/O Events] documentazione](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) per un’introduzione ai webhook.

## Creare un webhook

Per ricevere [!DNL I/O Event] notifiche, è necessario registrare un webhook specificando un URL univoco come parte dei dettagli di registrazione dell’evento.

Puoi configurare il webhook utilizzando il client desiderato. Per un indirizzo del webhook temporaneo da utilizzare come parte di questa esercitazione, visita [Webhook.site](https://webhook.site/) e copia l’URL univoco fornito.

![](../images/notifications/webhook-url.png)

Durante il processo di convalida iniziale, [!DNL I/O Events] invia un `challenge` parametro di query in una richiesta GET al webhook. Devi configurare il webhook in modo che restituisca il valore di questo parametro nel payload di risposta. Se utilizzi Webhook.site, seleziona **[!DNL Edit]** nell’angolo in alto a destra, quindi immetti `$request.query.challenge$` in **[!DNL Response body]** prima di selezionare **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Creare un nuovo progetto nella console Adobe Developer

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nel tutorial su [creazione di un progetto vuoto](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) nella documentazione della console Adobe Developer.

## Iscriviti agli eventi

Dopo aver creato un nuovo progetto, passa alla schermata di panoramica del progetto. Da qui, seleziona **[!UICONTROL Aggiungi evento]**.

![](../images/notifications/add-event-button.png)

Viene visualizzata una finestra di dialogo che consente di aggiungere un provider di eventi al progetto:

* Se ti abboni agli avvisi di Experience Platform, seleziona **[!UICONTROL Notifiche della piattaforma]**
* Se ti iscrivi a Adobe Experience Platform [!DNL Privacy Service] notifiche, seleziona **[!UICONTROL Eventi Privacy Service]**

Dopo aver scelto un provider di eventi, seleziona **[!UICONTROL Successivo]**.

![](../images/notifications/event-provider.png)

Nella schermata successiva viene visualizzato un elenco dei tipi di evento a cui iscriversi. Seleziona gli eventi a cui desideri abbonarti, quindi seleziona **[!UICONTROL Successivo]**.

>[!NOTE]
>
>Se non sai a quali eventi abbonarti per il servizio che stai lavorando, consulta la seguente documentazione:
>
>* [Notifiche della piattaforma](./rules.md)
>* [Notifiche Privacy Service](../../privacy-service/privacy-events.md)


![](../images/notifications/choose-event-subscriptions.png)

Nella schermata successiva viene richiesto di creare un token web JSON (JWT). Puoi generare automaticamente una coppia di chiavi o caricare la tua chiave pubblica generata nel terminale.

Ai fini di questa esercitazione, viene seguita la prima opzione. Seleziona la casella delle opzioni per **[!UICONTROL Generare una coppia di chiavi]**, quindi seleziona la **[!UICONTROL Genera coppia di chiavi]** nell&#39;angolo in basso a destra.

![](../images/notifications/generate-keypair.png)

Quando la coppia di chiavi viene generata, viene scaricata automaticamente dal browser. Devi archiviare questo file in modo autonomo poiché non viene mantenuto in Developer Console.

La schermata successiva consente di rivedere i dettagli della coppia di chiavi appena generata. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

![](../images/notifications/keypair-generated.png)

Nella schermata successiva, fornisci un nome e una descrizione per la registrazione dell’evento in [!UICONTROL Dettagli registrazione evento] sezione. Si consiglia di creare un nome univoco e facilmente identificabile per distinguere la registrazione di questo evento da quella di altri sullo stesso progetto.

![](../images/notifications/registration-details.png)

Più in basso nella stessa schermata sotto [!UICONTROL Come ricevere gli eventi] è possibile configurare la modalità di ricezione degli eventi. **[!UICONTROL Webhook]** consente di fornire un indirizzo di webhook personalizzato per la ricezione di eventi, mentre **[!UICONTROL Azione runtime]** consente di fare lo stesso con [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Per questo tutorial, seleziona **[!UICONTROL Webhook]** e fornisci l’URL del webhook creato in precedenza. Al termine, seleziona **[!UICONTROL Salva eventi configurati]** per completare la registrazione dell&#39;evento.

![](../images/notifications/receive-events.png)

Viene visualizzata la pagina dei dettagli per la registrazione dell&#39;evento appena creata, in cui è possibile modificarne la configurazione, esaminare gli eventi ricevuti, eseguire la traccia di debug e aggiungere nuovi provider di eventi.

![](../images/notifications/registration-complete.png)

## Passaggi successivi

Seguendo questa esercitazione, hai registrato un webhook per ricevere [!DNL I/O Event] notifiche per [!DNL Experience Platform] e/o [!DNL Privacy Service]. Per informazioni dettagliate sugli eventi disponibili e su come interpretare i payload di notifica per ciascun servizio, consulta la seguente documentazione:

* [[!DNL Privacy Service] notifiche](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notifiche](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (origini) notifiche](../../sources/notifications.md)

Consulta la [[!DNL Observability Insights] panoramica](../home.md) per ulteriori informazioni su come monitorare le attività in [!DNL Experience Platform] e [!DNL Privacy Service].
