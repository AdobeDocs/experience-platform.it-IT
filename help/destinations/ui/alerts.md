---
keywords: Experience Platform;home;argomenti popolari; avvisi;destinazioni
description: È possibile abbonarsi agli avvisi durante la creazione di un flusso di dati, per ricevere messaggi di avviso relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso.
title: Iscriviti agli avvisi contestuali sulle destinazioni
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 8%

---

# Iscriviti agli avvisi contestuali sulle destinazioni

Adobe Experience Platform ti consente di abbonarti agli avvisi basati su eventi relativi alle attività di Adobe Experience Platform. Gli avvisi riducono o eliminano la necessità di eseguire il polling dell&#39;[[!DNL Observability Insights] API](../../observability/api/overview.md) per verificare se un processo è stato completato, se è stata raggiunta una determinata fase cardine in un flusso di lavoro o se si sono verificati errori.

È possibile abbonarsi agli avvisi durante la creazione di un flusso di dati per ricevere messaggi di avviso relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso.

Questo documento descrive come abbonarsi e ricevere messaggi di avviso per i flussi di dati di destinazione.

## Introduzione

Questo documento richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Destinazioni](../home.md): integrazioni predefinite con le piattaforme di destinazione che consentono l&#39;attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.
* [Osservabilità](../../observability/home.md): [!DNL Observability Insights] consente di monitorare le attività di Platform tramite l&#39;utilizzo di metriche statistiche e notifiche di eventi.
   * [Avvisi](../../observability/alerts/overview.md): quando viene raggiunto un determinato set di condizioni nelle operazioni di Platform (ad esempio un potenziale problema quando il sistema supera una soglia), Platform può inviare messaggi di avviso a tutti gli utenti dell&#39;organizzazione che si sono iscritti a tali condizioni.

## Iscriversi agli avvisi nell’interfaccia utente {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="Iscriversi agli avvisi di destinazione"
>abstract="Gli avvisi consentono di ricevere notifiche in base allo stato dei flussi di dati di destinazione. Puoi impostare le notifiche di avviso per ottenere aggiornamenti se il flusso di dati è stato avviato, ha avuto esito positivo o negativo o non ha inviato dati alla destinazione."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Devi abilitare le notifiche istantanee delle e-mail per il tuo account Platform per ricevere le notifiche di avviso basate su e-mail per i flussi di dati.

Puoi abilitare gli avvisi per i flussi di dati durante il passaggio [!UICONTROL Configura nuova destinazione] del flusso di lavoro [connessione di destinazione](connect-destination.md).

![Immagine dell&#39;interfaccia utente che mostra la sezione avvisi di destinazione.](../assets/ui/alerts/destination-alerts.png)

Seleziona gli avvisi a cui vuoi abbonarti, quindi seleziona **[!UICONTROL Successivo]** per rivedere e completare il flusso di dati.

Gli avvisi disponibili per i flussi di dati di destinazione sono descritti nella tabella seguente.

* Per le destinazioni di streaming, è disponibile solo l&#39;avviso [!DNL Activation Skipped Rate Exceeded].
* Per le destinazioni basate su file, sono disponibili tutti gli avvisi.

| Avvisi | Descrizione |
| --- | --- |
| Ritardo esecuzione flusso di destinazione | Questo avviso notifica quando l’esecuzione di un flusso di destinazione richiede più di 150 minuti per attivare un pubblico. |
| Errore di esecuzione del flusso di destinazione | Questo avviso notifica quando si verifica un errore durante l’attivazione di un pubblico in una destinazione. |
| Esecuzione del flusso di destinazione completata | Questo avviso ti avvisa quando un pubblico viene attivato correttamente su una destinazione. |
| Inizio esecuzione flusso di destinazione | Questo avviso notifica quando l’esecuzione di un flusso di destinazione avvia l’attivazione di un pubblico. |
| Frequenza di attivazione ignorata superata | Questo avviso notifica quando il tasso di salto dell’attivazione supera l’1% del totale delle attivazioni. Le identità vengono ignorate durante l’attivazione quando presentano attributi mancanti o violazioni del consenso. |

## Ricezione degli avvisi {#receiving-alerts}

Una volta eseguito il flusso di dati di destinazione, puoi ricevere avvisi tramite l’interfaccia utente o tramite e-mail.

### Ricezione di avvisi nell’interfaccia utente {#receiving-alerts-in-ui}

Gli avvisi sono rappresentati nell’interfaccia utente da un’icona di notifica nell’intestazione superiore dell’interfaccia utente di Platform. Seleziona l’icona di notifica per visualizzare messaggi di avviso specifici relativi ai flussi di dati.

![Immagine dell&#39;interfaccia utente con l&#39;icona di notifica nell&#39;Experience Platform](../assets/ui/alerts/notification.png)

Viene visualizzato il pannello delle notifiche, con un elenco degli aggiornamenti di stato sul flusso di dati creato.

![Immagine dell&#39;interfaccia utente che mostra il pannello di notifica](../assets/ui/alerts/alert-window.png)

Puoi passare il cursore del mouse su un messaggio di avviso per contrassegnarli come letti oppure selezionare l’icona dell’orologio per impostare promemoria futuri sullo stato del flusso di dati.

![Immagine dell&#39;interfaccia utente che mostra le opzioni del promemoria di notifica](../assets/ui/alerts/remind-me.png)

Seleziona il messaggio di avviso per visualizzare informazioni specifiche sul flusso di dati.

![Immagine dell&#39;interfaccia utente che mostra come selezionare una notifica](../assets/ui/alerts/select-alert-message.png)

Viene visualizzata la pagina [!UICONTROL Dettagli esecuzione flusso di dati]. Nella metà superiore della schermata viene visualizzata una panoramica del flusso di dati, con informazioni sugli attributi, l’ID di esecuzione del flusso di dati corrispondente e un riepilogo di errore di alto livello.

![Immagine dell&#39;interfaccia utente che mostra la pagina dei dettagli di esecuzione del flusso di dati.](../assets/ui/alerts/dataflow-overview.png)

Nella metà inferiore della pagina vengono visualizzati [!UICONTROL errori di esecuzione del flusso di dati] verificatisi durante la fase di esecuzione del flusso di dati. Da qui puoi visualizzare in anteprima la diagnostica degli errori oppure utilizzare l&#39;[[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) per scaricare la diagnostica degli errori o il manifesto del file che corrisponde al flusso di dati.

![Immagine dell&#39;interfaccia utente che mostra la pagina dei dettagli di esecuzione del flusso di dati, con un&#39;evidenziazione nella sezione errori.](../assets/ui/alerts/dataflow-run-error.png)

Per ulteriori informazioni sulla gestione degli errori del flusso di dati, consulta la guida su [monitoraggio dei flussi di dati delle destinazioni nell&#39;interfaccia utente](../../dataflows/ui/monitor-destinations.md).

### Ricezione degli avvisi tramite e-mail {#receiving-alerts-by-email}

Gli avvisi per i flussi di dati vengono inviati anche via e-mail. Seleziona il nome del flusso di dati nel corpo dell’e-mail per visualizzare ulteriori informazioni sul flusso di dati.

![Schermata di un messaggio e-mail di avviso](../assets/ui/alerts/email.png)

Analogamente all&#39;avviso dell&#39;interfaccia utente, viene visualizzata la pagina [!UICONTROL Panoramica sull&#39;esecuzione del flusso di dati], che fornisce un&#39;interfaccia per analizzare eventuali errori associati al flusso di dati.

![dataflow-overview](../assets/ui/alerts/dataflow-overview.png)

## Abbonati e annulla l’abbonamento agli avvisi {#subscribe-and-unsubscribe}

È possibile sottoscrivere altri avvisi o annullare l&#39;abbonamento agli avvisi stabiliti per un flusso di dati di destinazione esistente nella pagina Destinazioni [!UICONTROL Sfoglia].

![Immagine dell&#39;interfaccia utente che mostra la pagina Sfoglia destinazioni](../assets/ui/alerts/destination-list.png)

Individuare la connessione di destinazione per la quale si desidera ricevere avvisi e selezionare i puntini di sospensione (`...`) per visualizzare un menu a discesa di opzioni. Quindi, seleziona **[!UICONTROL Abbonati agli avvisi]** per modificare le impostazioni degli avvisi del flusso di dati di destinazione.

![Immagine dell&#39;interfaccia utente con le opzioni di destinazione](../assets/ui/alerts/destination-alerts-subscribe.png)

Viene visualizzata una finestra popup con un elenco di avvisi di destinazione. Seleziona gli avvisi a cui vuoi abbonarti o deseleziona gli avvisi a cui vuoi annullare l’abbonamento. Al termine, selezionare **[!UICONTROL Salva]**.

![Immagine dell&#39;interfaccia utente che mostra la pagina delle sottoscrizioni degli avvisi di destinazione](../assets/ui/alerts/destination-alerts-list.png)

## Passaggi successivi {#next-steps}

Questo documento fornisce una guida dettagliata su come abbonarsi agli avvisi contestuali per i flussi di dati di destinazione. Per ulteriori informazioni, vedere la [guida all&#39;interfaccia utente degli avvisi](../../observability/alerts/ui.md).
