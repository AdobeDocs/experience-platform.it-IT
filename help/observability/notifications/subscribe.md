---
keywords: Experience Platform;home;argomenti popolari;intervallo di date
solution: Experience Platform
title: Iscriviti ad Adobe I/O Event Notifications
topic-legacy: developer guide
description: Questo documento fornisce passaggi su come effettuare l’abbonamento ad Adobi I/O di notifiche di eventi per i servizi Adobe Experience Platform. Vengono inoltre fornite informazioni di riferimento sui tipi di evento disponibili, insieme a collegamenti a ulteriori informazioni su come interpretare i dati dell’evento restituiti per ciascun servizio  [!DNL Platform] applicabile.
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# Iscriviti alle notifiche dell’evento di Adobe I/O

[!DNL Observability Insights] ti consente di abbonarti alle notifiche evento di Adobe I/O relative alle attività Adobe Experience Platform. Questi eventi vengono inviati a un webhook configurato per facilitare l&#39;automazione efficiente del monitoraggio delle attività.

Questo documento fornisce passaggi su come effettuare l’abbonamento ad Adobi I/O di notifiche di eventi per i servizi Adobe Experience Platform. Vengono inoltre fornite informazioni di riferimento sui tipi di evento disponibili, insieme a collegamenti a ulteriori informazioni su come interpretare i dati dell’evento restituiti per ciascun servizio [!DNL Platform] applicabile.

## Introduzione

Questo documento richiede una comprensione funzionante dei webhook e come collegare un webhook da un&#39;applicazione a un&#39;altra. Fai riferimento alla [[!DNL I/O Events] documentazione](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) per un&#39;introduzione ai webhook.

## Crea un webhook

Per ricevere le notifiche [!DNL I/O Event], è necessario registrare un webhook specificando un URL webhook univoco come parte dei dettagli di registrazione dell&#39;evento.

Puoi configurare il tuo webhook utilizzando il client di tua scelta. Per un indirizzo webhook temporaneo da utilizzare come parte di questa esercitazione, visita [Webhook.site](https://webhook.site/) e copia l&#39;URL univoco fornito.

![](../images/notifications/webhook-url.png)

Durante il processo di convalida iniziale, [!DNL I/O Events] invia un parametro di query `challenge` in una richiesta di GET al webhook. Devi configurare il webhook per restituire il valore di questo parametro nel payload di risposta. Se utilizzi Webhook.site, seleziona **[!DNL Edit]** nell’angolo in alto a destra, quindi immetti `$request.query.challenge$` in **[!DNL Response body]** prima di selezionare **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Creare un nuovo progetto in Adobe Developer Console

Vai a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e accedi con il tuo Adobe ID. Quindi, segui i passaggi descritti nell’esercitazione su [creazione di un progetto vuoto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) nella documentazione di Adobe Developer Console.

## Iscriviti agli eventi

Dopo aver creato un nuovo progetto, accedi alla schermata di panoramica del progetto. Da qui, seleziona **[!UICONTROL Add event]**.

![](../images/notifications/add-event-button.png)

Viene visualizzata una finestra di dialogo che consente di aggiungere un provider di eventi al progetto:

* Se effettui l’abbonamento alle notifiche [!DNL Experience Platform], seleziona **[!UICONTROL Platform notifications]**
* Se effettui l’abbonamento alle notifiche Adobe Experience Platform [!DNL Privacy Service], seleziona **[!UICONTROL Privacy Service Events]**

Dopo aver scelto un provider di eventi, seleziona **[!UICONTROL Next]**.

![](../images/notifications/event-provider.png)

Nella schermata successiva viene visualizzato un elenco dei tipi di evento a cui effettuare l’abbonamento. Seleziona gli eventi a cui vuoi abbonarti, quindi seleziona **[!UICONTROL Next]**.

>[!NOTE]
>
>Se non sei sicuro degli eventi a cui effettuare l’abbonamento per il servizio con cui stai lavorando, consulta la documentazione di notifica specifica per il servizio:
>
>* [[!DNL Privacy Service] Notifiche](../../privacy-service/privacy-events.md)
>* [[!DNL Data Ingestion] Notifiche](../../ingestion/quality/subscribe-events.md)
>* [[!DNL Flow Service (sources)] Notifiche](../../sources/notifications.md)


![](../images/notifications/choose-event-subscriptions.png)

Nella schermata successiva viene richiesto di creare un token Web JSON (JWT). Puoi generare automaticamente una coppia di chiavi o caricare una tua chiave pubblica generata nel terminale.

Ai fini di questa esercitazione, viene seguita la prima opzione. Seleziona la casella delle opzioni per **[!UICONTROL Generate a key pair]**, quindi seleziona il pulsante **[!UICONTROL Generate keypair]** nell&#39;angolo in basso a destra.

![](../images/notifications/generate-keypair.png)

Quando la coppia di chiavi viene generata, viene scaricata automaticamente dal browser. Devi memorizzare questo file da solo in quanto non viene mantenuto nella Console per sviluppatori.

La schermata successiva ti consente di esaminare i dettagli della nuova coppia di chiavi generata. Seleziona **[!UICONTROL Next]** per continuare.

![](../images/notifications/keypair-generated.png)

Nella schermata successiva, fornisci un nome e una descrizione per la registrazione dell’evento nella sezione [!UICONTROL Event registration details] . Si consiglia di creare un nome univoco e facilmente identificabile per distinguere la registrazione di questo evento da altri sullo stesso progetto.

![](../images/notifications/registration-details.png)

Più in basso sullo stesso schermo nella sezione [!UICONTROL How to receive events], puoi anche configurare come ricevere gli eventi. **[!UICONTROL Webhook]** consente di fornire un indirizzo webhook personalizzato per ricevere gli eventi, mentre  **[!UICONTROL Runtime action]** consente di fare lo stesso utilizzando  [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Per questa esercitazione, seleziona **[!UICONTROL Webhook]** e fornisci l’URL del webhook creato in precedenza. Al termine, seleziona **[!UICONTROL Save configured events]** per completare la registrazione dell’evento.

![](../images/notifications/receive-events.png)

Viene visualizzata la pagina dei dettagli per la registrazione dell’evento appena creata, in cui è possibile modificarne la configurazione, esaminare gli eventi ricevuti, eseguire il tracciamento del debug e aggiungere nuovi provider di eventi.

![](../images/notifications/registration-complete.png)

## Passaggi successivi

Seguendo questa esercitazione, hai registrato un webhook per ricevere notifiche [!DNL I/O Event] per [!DNL Experience Platform] e/o [!DNL Privacy Service]. Per informazioni dettagliate sugli eventi disponibili e su come interpretare i payload di notifica per ciascun servizio, consulta la seguente documentazione:

* [[!DNL Privacy Service] Notifiche](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] Notifiche](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service (sources)] Notifiche](../../sources/notifications.md)

Per ulteriori informazioni su come monitorare le attività su [!DNL Experience Platform] e [!DNL Privacy Service], consulta la sezione [[!DNL Observability Insights] panoramica](../home.md) .
