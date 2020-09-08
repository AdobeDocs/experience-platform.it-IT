---
keywords: Experience Platform;home;popular topics;date range
solution: Experience Platform
title: Iscriviti  notifiche di I/O Adobe
topic: developer guide
description: In questo documento vengono fornite istruzioni su come effettuare la sottoscrizione  notifiche di eventi I/O Adobe per i servizi Adobe Experience Platform. Vengono inoltre fornite informazioni di riferimento sui tipi di evento disponibili, insieme a collegamenti verso ulteriori informazioni su come interpretare i dati dell'evento restituiti per ciascun servizio [!DNL Platform] applicativo.
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 1%

---


# Iscriviti  notifiche di I/O Adobe

[!DNL Observability Insights] consente di iscriversi  notifiche di I/O Adobe relative alle attività di Adobe Experience Platform. Questi eventi vengono inviati a un webhook configurato per facilitare l&#39;automazione efficiente del monitoraggio dell&#39;attività.

In questo documento vengono fornite istruzioni su come effettuare la sottoscrizione  notifiche di eventi I/O Adobe per i servizi Adobe Experience Platform. Vengono inoltre fornite informazioni di riferimento sui tipi di evento disponibili, insieme a collegamenti verso ulteriori informazioni su come interpretare i dati dell&#39;evento restituiti per ciascun [!DNL Platform] servizio applicabile.

## Introduzione

Questo documento richiede una buona conoscenza dei webhook e di come collegare un webhook da un&#39;applicazione a un&#39;altra. Fare riferimento alla [[!DNL I/O Events] documentazione](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) per un&#39;introduzione ai webhooks.

## Creare un webhook

Per ricevere [!DNL I/O Event] le notifiche, dovete registrare un webhook specificando un URL webhook univoco come parte dei dettagli di registrazione dell&#39;evento.

Puoi configurare il tuo webhook utilizzando il client di tua scelta. Per utilizzare un indirizzo webhook temporaneo come parte di questa esercitazione, visitate [Webhook.site](https://webhook.site/) e copiate l&#39;URL univoco fornito.

![](../images/notifications/webhook-url.png)

Durante il processo di convalida iniziale, [!DNL I/O Events] invia al webhook un parametro di `challenge` query in una richiesta di GET. Dovete configurare il webhook per restituire il valore di questo parametro nel payload di risposta. Se si utilizza Webhook.site, selezionare **[!DNL Edit]** nell&#39;angolo superiore destro, quindi immettere `$request.query.challenge$` in **[!DNL Response body]** prima di selezionare **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Creare un nuovo progetto in  Adobe Developer Console

Andate a [console](https://www.adobe.com/go/devs_console_ui) per sviluppatori di Adobi ed effettuate l&#39;accesso con il vostro Adobe ID . Attenetevi quindi ai passaggi descritti nell&#39;esercitazione sulla [creazione di un progetto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vuoto nella documentazione di  Adobe Developer Console.

## Iscriviti agli eventi

Dopo aver creato un nuovo progetto, andate alla schermata di panoramica del progetto. Da qui, selezionare **[!UICONTROL Add event]**.

![](../images/notifications/add-event-button.png)

Viene visualizzata una finestra di dialogo che consente di aggiungere un provider di eventi al progetto:

* Se state iscrivendo alle [!DNL Experience Platform] notifiche, selezionate **[!UICONTROL Platform notifications]**
* Se vi state iscrivendo alle [!DNL Privacy Service] notifiche Adobe Experience Platform, selezionate **[!UICONTROL Privacy Service Events]**

Dopo aver scelto un provider di eventi, selezionate **[!UICONTROL Next]**.

![](../images/notifications/event-provider.png)

Nella schermata successiva viene visualizzato un elenco dei tipi di evento a cui effettuare la sottoscrizione. Selezionate gli eventi a cui desiderate iscrivervi, quindi selezionate **[!UICONTROL Next]**.

>[!NOTE]
>
>Se non sai a quali eventi abbonarti per il servizio con cui stai lavorando, consulta la documentazione di notifica specifica per il servizio:
>
>* [[!DNL Privacy Service] Notifiche](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] Notifiche](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service] (origini) notifiche](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

Nella schermata successiva viene richiesto di creare un token Web JSON (JWT). Potete generare automaticamente una coppia di chiavi o caricare la vostra chiave pubblica generata nel terminale.

Ai fini di questa esercitazione, viene seguita la prima opzione. Selezionate la casella delle opzioni per **[!UICONTROL Generate a key pair]**, quindi fate **[!UICONTROL Generate keypair]** clic sul pulsante nell’angolo inferiore destro.

![](../images/notifications/generate-keypair.png)

Quando la coppia di chiavi viene generata, viene scaricata automaticamente dal browser. Il file deve essere memorizzato personalmente, in quanto non è persistente nella Developer Console.

Nella schermata successiva è possibile esaminare i dettagli della coppia di chiavi appena generata. Selezionare **[!UICONTROL Next]** per continuare.

![](../images/notifications/keypair-generated.png)

Nella schermata successiva, fornite un nome e una descrizione per la registrazione all’evento nella [!UICONTROL Event registration details] sezione. È buona norma creare un nome univoco e facilmente identificabile per distinguere la registrazione a questo evento da altri sullo stesso progetto.

![](../images/notifications/registration-details.png)

Nella stessa schermata della [!UICONTROL How to receive events] sezione, potete configurare la modalità di ricezione degli eventi in modo facoltativo. **[!UICONTROL Webhook]** consente di fornire un indirizzo webhook personalizzato per ricevere gli eventi, mentre **[!UICONTROL Runtime action]** consente di eseguire le stesse operazioni utilizzando [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Per questa esercitazione, selezionate **[!UICONTROL Webhook]** e fornite l’URL del webhook creato in precedenza. Al termine, selezionate **[!UICONTROL Save configured events]** per completare la registrazione all’evento.

![](../images/notifications/receive-events.png)

Viene visualizzata la pagina dei dettagli per la registrazione dell&#39;evento appena creata, in cui è possibile modificarne la configurazione, esaminare gli eventi ricevuti, eseguire il debug del tracciamento e aggiungere nuovi provider di eventi.

![](../images/notifications/registration-complete.png)

## Passaggi successivi

Seguendo questa esercitazione, hai registrato un webhook per ricevere [!DNL I/O Event] notifiche per [!DNL Experience Platform] e/o [!DNL Privacy Service]. Per informazioni dettagliate sugli eventi disponibili e su come interpretare i payload di notifica per ciascun servizio, consultate la seguente documentazione:

* [[!DNL Privacy Service] Notifiche](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] Notifiche](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (origini) notifiche](../../sources/notifications.md)

Consulta la [[!DNL Observability Insights] panoramica](../home.md) per ulteriori informazioni su come monitorare le attività su [!DNL Experience Platform] e [!DNL Privacy Service].