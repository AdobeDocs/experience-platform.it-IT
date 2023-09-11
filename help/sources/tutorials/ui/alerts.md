---
keywords: Experience Platform;home;argomenti popolari; avvisi
description: È possibile abbonarsi agli avvisi durante la creazione di un flusso di dati, per ricevere messaggi di avviso relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso.
title: Iscriviti agli avvisi contestuali nell’interfaccia utente di
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: 9120377f5f2048579d7e2a4740cfcbc56d49d61a
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 6%

---

# Iscriviti agli avvisi per i flussi di dati di origini nell’interfaccia utente

>[!NOTE]
>
>Gli avvisi non sono supportati nelle sandbox non di produzione. Per abbonarti agli avvisi, devi assicurarti di utilizzare una sandbox di produzione.

Adobe Experience Platform ti consente di abbonarti agli avvisi basati su eventi relativi alle attività di Adobe Experience Platform. Gli avvisi riducono o eliminano la necessità di eseguire il polling [[!DNL Observability Insights] API](../../../observability/api/overview.md) per verificare se un processo è stato completato, se è stata raggiunta una determinata fase cardine all’interno di un flusso di lavoro o se si sono verificati errori.

È possibile abbonarsi agli avvisi durante la creazione di un flusso di dati per ricevere messaggi di avviso relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso.

Questo documento descrive come abbonarsi e ricevere messaggi di avviso per i flussi di dati di origine.

## Introduzione

Questo documento richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sorgenti](../../home.md): [!DNL Experience Platform] consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi.
* [Osservabilità](../../../observability/home.md): [!DNL Observability Insights] consente di monitorare le attività di Platform tramite l’utilizzo di metriche statistiche e notifiche di eventi.
   * [Avvisi](../../../observability/alerts/overview.md): quando viene raggiunto un determinato set di condizioni nelle operazioni di Platform (ad esempio un potenziale problema quando il sistema supera una soglia), Platform può inviare messaggi di avviso a tutti gli utenti dell’organizzazione che sono abbonati.

## Iscriviti agli avvisi nell’interfaccia utente {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Iscriversi agli avvisi delle origini"
>abstract="Gli avvisi consentono di ricevere notifiche in base allo stato dei flussi di dati delle origini. Puoi impostare le notifiche di avviso per ottenere aggiornamenti se il flusso di dati è stato avviato, ha avuto esito positivo o negativo o non ha acquisito dati."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Devi abilitare le notifiche istantanee delle e-mail per il tuo account Platform per ricevere le notifiche di avviso basate su e-mail per i flussi di dati.

Puoi abilitare gli avvisi per i flussi di dati durante il [!UICONTROL Dettagli del flusso di dati] passaggio del flusso di lavoro origini nell&#39;area di lavoro origini.

![dataflow-detail](../../images/tutorials/alerts/dataflow-detail.png)

Gli avvisi disponibili per i flussi di dati di origine sono:

>[!NOTE]
>
>Le origini di streaming non sono attualmente supportate dagli avvisi. È possibile abbonarsi solo alle notifiche di avviso per le origini batch.

| Avvisi | Descrizione |
| --- | --- |
| Inizio esecuzione flusso origini | Questo avviso invia un messaggio all’avvio del flusso di dati sorgente. |
| Esecuzione del flusso di origini completata | Questo avviso invia un messaggio quando i dati provenienti dall’origine vengono acquisiti correttamente in Platform. |
| Errore di esecuzione del flusso origini | Questo avviso ti invia un messaggio in caso di errore nel flusso di dati. |

Seleziona gli avvisi a cui desideri abbonarti, quindi seleziona **[!UICONTROL Successivo]** per rivedere e completare il flusso di dati.

![select-alerts](../../images/tutorials/alerts/select-alerts.png)

Consulta le seguenti guide per i passaggi dettagliati sulla creazione di un flusso di dati di origini nell’interfaccia utente:

* [Advertising](./dataflow/advertising.md)
* [Archiviazione cloud](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [Database](./dataflow/databases.md)
* [E-commerce](./dataflow/ecommerce.md)
* [File locali](./create/local-system/local-file-upload.md)
* [Automazione del marketing](./dataflow/marketing-automation.md)
* [Pagamenti](./dataflow/payments.md)
* [Protocoli](./dataflow/protocols.md)

## Ricezione di avvisi

Una volta eseguito il flusso di dati, puoi ricevere avvisi tramite l’interfaccia utente o tramite e-mail.

### Nell’interfaccia utente

Gli avvisi sono rappresentati nell’interfaccia utente da un’icona di notifica nell’intestazione superiore dell’interfaccia utente di Platform. Seleziona l’icona di notifica per visualizzare messaggi di avviso specifici relativi ai flussi di dati.

![notifica](../../images/tutorials/alerts/notification.png)

Viene visualizzato il pannello delle notifiche, con un elenco degli aggiornamenti di stato sul flusso di dati creato.

![finestra di avviso](../../images/tutorials/alerts/alert-window.png)

Puoi passare il cursore del mouse su un messaggio di avviso per contrassegnarli come letti oppure selezionare l’icona dell’orologio per impostare promemoria futuri sullo stato del flusso di dati.

![promemoria](../../images/tutorials/alerts/remind-me.png)

Seleziona il messaggio di avviso per visualizzare informazioni specifiche sul flusso di dati.

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

Il [!UICONTROL Panoramica sull’esecuzione del flusso di dati] viene visualizzata. Nella metà superiore della schermata viene visualizzata una panoramica del flusso di dati, con informazioni sugli attributi, l’ID di esecuzione del flusso di dati corrispondente e un riepilogo di errore di alto livello.

![panoramica del flusso di dati](../../images/tutorials/alerts/dataflow-overview.png)

Nella metà inferiore della pagina viene visualizzato qualsiasi [!UICONTROL Errori di esecuzione del flusso di dati] che si è verificato durante la fase di esecuzione del flusso di dati. Da qui, puoi visualizzare in anteprima la diagnostica degli errori o utilizzare [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) per scaricare la diagnostica degli errori o il manifesto del file che corrisponde al flusso di dati.

![dataflow-run-errors](../../images/tutorials/alerts/dataflow-run-error.png)

Per ulteriori informazioni sulla gestione degli errori del flusso di dati, consulta la guida su [monitoraggio dei flussi di dati di origine nell’interfaccia utente](../../../dataflows/ui/monitor-sources.md).

### Per e-mail

Gli avvisi per i flussi di dati vengono inviati anche via e-mail. Seleziona il nome del flusso di dati nel corpo dell’e-mail per visualizzare ulteriori informazioni sul flusso di dati.

![e-mail](../../images/tutorials/alerts/email.png)

Analogamente all’avviso dell’interfaccia utente, il [!UICONTROL Panoramica sull’esecuzione del flusso di dati] viene visualizzata una pagina, che offre un’interfaccia per analizzare eventuali errori associati al flusso di dati.

![panoramica del flusso di dati](../../images/tutorials/alerts/dataflow-overview.png)

## Abbonati e annulla l’abbonamento agli avvisi

È possibile abbonarsi a più avvisi o annullare l’abbonamento agli avvisi stabiliti per un flusso di dati esistente in [!UICONTROL Flussi dati] pagina. Individua il flusso di dati creato dall’elenco, quindi seleziona i puntini di sospensione (`...`) per visualizzare un menu a discesa di opzioni. Quindi, seleziona **[!UICONTROL Abbonare gli avvisi]** per modificare le impostazioni degli avvisi del flusso di dati.

![opzioni](../../images/tutorials/alerts/options.png)

Viene visualizzata una finestra popup che fornisce un elenco di avvisi relativi alle origini. Seleziona gli avvisi a cui vuoi abbonarti o deseleziona gli avvisi a cui vuoi annullare l’abbonamento. Al termine, seleziona **[!UICONTROL Salva]**.

![salva](../../images/tutorials/alerts/save.png)

## Passaggi successivi

Questo documento fornisce una guida dettagliata su come abbonarsi agli avvisi contestuali per i flussi di dati di origine. Per ulteriori informazioni, vedere [guida dell’interfaccia utente avvisi](../../../observability/alerts/ui.md).