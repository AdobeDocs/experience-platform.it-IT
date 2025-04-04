---
title: Modelli di rapporti Power BI per dashboard di Experience Platform
description: Utilizza i modelli di rapporto per esplorare i dati di Experience Platform utilizzando Power BI.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 0%

---

# Modelli di rapporti Power BI per dashboard

La funzione per modelli di report di Power BI consente di creare report convincenti compilati con dati provenienti da Adobe Experience Platform. Il processo di installazione semplificato installa automaticamente i widget standard per Real-Time Customer Profile, segmentazione e destinazioni. L’installazione collega anche Power BI ai modelli di dati in modo da poter personalizzare ed estendere facilmente i modelli di rapporto. Questi rapporti possono essere condivisi in tutta l’organizzazione senza che i destinatari abbiano bisogno di credenziali per l’organizzazione su Experience Platform.

Questo documento fornisce istruzioni su come collegare Adobe Experience Platform all’applicazione Power BI e utilizzare modelli di rapporto per condividere informazioni chiave sui dati di Experience Platform con utenti esterni.

## Introduzione

Prima di continuare con questa esercitazione, è consigliabile avere una buona conoscenza della [composizione dello schema](../../xdm/schema/composition.md) in Experience Platform e del modo in cui gli attributi vengono inclusi nel Profilo cliente in tempo reale tramite lo [schema di unione](../../xdm/schema/composition.md#union).

Per installare l’integrazione dell’applicazione Power BI, gli utenti devono aver acquisito le seguenti autorizzazioni Experience Platform:

- Gestire le query
- Gestire le sandbox

Per informazioni su come assegnare queste autorizzazioni, leggere la documentazione del [controllo di accesso](../../access-control/home.md).

Per seguire questa esercitazione, è necessario disporre di un account Power BI. Per creare un account, passare alla [home page di Power BI](https://powerbi.microsoft.com/en-us/) e seguire la procedura di abbonamento. Gli utenti di questo account Power BI devono abilitare anche l&#39;impostazione **Crea area di lavoro** nelle impostazioni Power BI. Questa impostazione si trova nelle impostazioni tenant del portale di amministrazione di Power BI. Se l’account è fornito dal tenant o dal datore di lavoro, contatta il rispettivo amministratore per abilitare questa impostazione.

![Impostazioni area di lavoro per la creazione del portale di amministrazione di Power BI.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Affinché la scheda Dashboard sia visibile nell’area di navigazione a sinistra dell’interfaccia utente di Experience Platform, è necessario avere accesso a qualsiasi dashboard di Profilo, Segmentazione o Destinazione nell’ambito della licenza di Experience Platform.

## Installare l’integrazione dell’applicazione Power BI

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Dashboard]** nell&#39;area di navigazione a sinistra per aprire l&#39;area di lavoro [!UICONTROL Dashboard]. Nella scheda [!UICONTROL Sfoglia] è visualizzato un elenco delle visualizzazioni del dashboard attualmente disponibili. Per ulteriori informazioni sulla visualizzazione delle dashboard disponibili, consulta la [documentazione di inventario](../inventory.md).

Quindi, seleziona la scheda **[!UICONTROL Integrazioni]**. Viene visualizzata la pagina di integrazione dell’applicazione Power BI. Da qui, selezionare **[!UICONTROL Installa]** per avviare l&#39;installazione.

>[!NOTE]
>
>Il pulsante [!UICONTROL Installa] è disabilitato a meno che non si disponga delle autorizzazioni Gestione e Gestione sandbox di Query Service.

![Schermata dei dettagli di Power BI con il pulsante Installa evidenziato.](../images/power-bi/details-screen.png)

### Immetti le credenziali

Il primo passaggio del processo di installazione consiste nel fornire credenziali senza scadenza per l&#39;integrazione dell&#39;applicazione Power BI. Sono disponibili due opzioni per specificare: [[!UICONTROL Crea nuove credenziali]](#create-new-credentials) o [[!UICONTROL Usa credenziali esistenti]](#use-existing-credentials). Seleziona l’interruttore appropriato per continuare.

#### Crea nuove credenziali {#create-new-credentials}

Durante la generazione delle nuove credenziali sono disponibili due campi obbligatori: [!UICONTROL Nome] e [!UICONTROL Assegnato a]. Il campo [!UICONTROL Assegnato a] si riferisce all&#39;indirizzo e-mail associato al tuo account Power BI.

![Power BI genera nuova schermata delle credenziali.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>La creazione di credenziali senza scadenza richiede l’assegnazione di determinate autorizzazioni e ruoli. Le autorizzazioni necessarie sono Gestisci sandbox e Gestisci integrazione servizio query. I ruoli richiesti sono amministratore di Adobe Experience Platform e ruoli sviluppatore. Per informazioni su come assegnare queste autorizzazioni, leggere la documentazione del [controllo di accesso](../../access-control/home.md).

Per ulteriori informazioni sulla generazione di credenziali di Query Service senza scadenza, consulta la [guida sulle credenziali senza scadenza](../../query-service/ui/credentials.md#non-expiring-credentials).

Dopo aver generato le credenziali senza scadenza per la prima volta, in tale computer viene scaricato un file JSON. Questo file JSON può quindi essere condiviso con altri utenti come credenziali per completare il processo di installazione.

#### Usa credenziali esistenti {#use-existing-credentials}

Per superare la convalida è inoltre possibile caricare un file di credenziali JSON. Questi file JSON contenenti i valori delle credenziali senza scadenza vengono scaricati nel computer locale utilizzato quando si crea una credenziale senza scadenza.

>[!IMPORTANT]
>
>Per utilizzare una credenziale esistente senza scadenza, è necessario che all&#39;utente siano già state assegnate delle credenziali. Se all&#39;utente non è stata assegnata alcuna credenziale e non è possibile crearne una nuova utilizzando Adobe Admin Console, l&#39;utente non può procedere con il processo di installazione.

Selezionare **[!UICONTROL Carica file delle credenziali]**, quindi selezionare il file JSON appropriato da caricare nella finestra di dialogo visualizzata.

![Schermata delle credenziali di Power BI con il pulsante Carica file delle credenziali evidenziato.](../images/power-bi/upload-credential-file.png)

Dopo aver fornito le credenziali senza scadenza, queste vengono convalidate automaticamente da Experience Platform. Dopo la convalida viene visualizzato un messaggio di conferma. Seleziona **[!UICONTROL Avanti]** per rivedere il contratto di consenso per l&#39;applicazione Power BI.

![La schermata delle credenziali senza scadenza è stata convalidata con il pulsante Avanti evidenziato.](../images/power-bi/successfully-uploaded-credential-file.png)

### Fornisci consenso

Viene visualizzata la visualizzazione del consenso. Seleziona **[!UICONTROL Rivedi il consenso]** per aprire una nuova finestra in cui sono specificate le autorizzazioni necessarie affinché Power BI possa accedere ai tuoi dati e utilizzarli in base ai termini del servizio e all&#39;informativa sulla privacy.

![Viene visualizzato il consenso fornito con il pulsante Rivedi consenso evidenziato.](../images/power-bi/provide-consent-display.png)

Seleziona **[!UICONTROL Accetta]** per concedere a Power BI l&#39;autorizzazione per accedere e utilizzare i tuoi dati di Experience Platform.

![Richiesta di autorizzazioni per l&#39;applicazione Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Se si esce dal processo di installazione in un qualsiasi momento prima di fornire il consenso, l&#39;integrazione dell&#39;applicazione Power BI non verrà installata nell&#39;inventario delle dashboard.

Dopo aver fornito il consenso, il modello di report viene installato automaticamente nell’ambiente Power BI come parte del processo di installazione. Power BI utilizza quindi le credenziali senza scadenza per accedere ad Experience Platform, eseguire in sequenza tutte le query SQL e popolare il modello di rapporto con i dati restituiti.

Seleziona **[!UICONTROL Fine]** per tornare all&#39;inventario del dashboard.

![Fornire il consenso con il pulsante Fine evidenziato.](../images/power-bi/finish-consent-review.png)

Ora che il modello di report Power BI è installato, viene visualizzato nell&#39;elenco dei dashboard disponibili nella scheda [!UICONTROL Sfoglia]. Selezionare **[!UICONTROL Power BI]** dall&#39;elenco per passare all&#39;ambiente Power BI.

![Power BI elencato nell&#39;inventario dei dashboard.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Gli amministratori di Power BI devono assicurarsi che gli utenti dispongano delle autorizzazioni di accesso appropriate per visualizzare queste dashboard nell’ambiente Power BI.

## Area di lavoro Power BI

Dopo aver effettuato l&#39;accesso a [l&#39;area di lavoro di Power BI](https://dxt.powerbi.com), i modelli di report sono disponibili per ciascuno dei servizi a cui hai accesso. I modelli di report includono profili, segmenti e dashboard di destinazioni **solo** se dispongono delle autorizzazioni di visualizzazione corrispondenti.

Per impostazione predefinita, i widget standard da profili, segmenti e destinazioni sono disponibili nei rapporti modello di Power BI.

>[!NOTE]
>
>Per consentire l’installazione del dashboard nell’ambiente Power BI, è necessario che siano abilitate le autorizzazioni di modifica per un determinato dashboard.

![Report modello profilo Power BI con widget profilo Experience Platform standard.](../images/power-bi/profile-report-template.png)

Dopo l’installazione di un dashboard in Power BI, per impostazione predefinita i modelli di rapporto vengono visualizzati a tutti gli utenti. Se desideri limitare l’accesso a qualsiasi modello di rapporto, accertati di disabilitare l’accesso per gli utenti in questione dall’ambiente Power BI.

## Personalizzare il modello di rapporto di Power BI

Tramite l’utilizzo di widget personalizzati, puoi aggiungere attributi personalizzati al modello di dati per arricchire i modelli di rapporto forniti da Power BI.

>[!NOTE]
>
>Gli attributi che è possibile utilizzare per i widget personalizzati dipendono da ciò che è disponibile nello schema di unione. Per informazioni su come visualizzare ed esplorare gli schemi di unione a vantaggio dei widget personalizzati, consulta la [guida dell&#39;interfaccia utente dello schema di unione](../../profile/ui/union-schema.md).

### Creare un widget personalizzato

I widget personalizzati vengono creati tramite la Libreria widget. Per un&#39;introduzione alla funzionalità, vedere la [Panoramica sulla libreria dei widget](../customize/widget-library.md) e il [tutorial per la creazione di un widget personalizzato](../customize/custom-widgets.md) per istruzioni specifiche.

>[!IMPORTANT]
>
>I nuovi widget personalizzati creati sono **not** sincronizzati automaticamente tra le dashboard di Adobe Experience Platform e i modelli di report di Power BI. Eventuali widget personalizzati creati nell’interfaccia utente di Experience Platform devono essere ricreati manualmente all’interno dell’ambiente Power BI.

### Ricreare il widget personalizzato nell’ambiente Power BI

Una volta che il dashboard dispone delle metriche e degli attributi appropriati contenuti nei widget personalizzati, puoi modificare il modello di report visualizzato dall’ambiente Power BI. Consulta la [documentazione di Power BI](https://docs.microsoft.com/en-us/power-bi/) per informazioni su come modificare un report tramite la relativa interfaccia utente.

## Eliminare l’integrazione dell’applicazione Power BI

Per eliminare il dashboard, passare all&#39;inventario del dashboard e selezionare l&#39;icona Elimina (![icona Elimina](/help/images/icons/delete.png)) accanto al nome del dashboard.

>[!NOTE]
>
>Solo l’utente che ha installato il dashboard di Power BI può eliminare l’integrazione dall’interfaccia utente di Experience Platform.

![Scheda Sfoglia della schermata di inventario dei dashboard visualizzata con il pulsante Sfoglia e l&#39;icona Elimina evidenziata.](../images/power-bi/delete-power-bi-dashboard.png)

Viene visualizzato un messaggio di conferma. Seleziona **[!UICONTROL Elimina]** per confermare il processo.

>[!IMPORTANT]
>
>L&#39;eliminazione del dashboard di Power BI dall&#39;interfaccia utente di Experience Platform **non** comporta l&#39;eliminazione dei modelli di report disponibili nell&#39;ambiente Power BI. Se desideri eliminare completamente le informazioni contenute nei modelli di rapporto di Power BI, devi accedere al tuo account Power BI ed eliminare i modelli di rapporto da tale ambiente. Una volta eliminato, l’utente può reinstallare il dashboard di Power BI seguendo le stesse istruzioni di installazione descritte in precedenza.

## Passaggi successivi

Una volta letto questo documento, sarai in grado di comprendere meglio come i modelli di rapporto di Power BI possono essere integrati in Experience Platform per condividere informazioni irresistibili sui dati provenienti dalle dashboard di profili, segmenti o destinazioni. Per ulteriori informazioni sulla personalizzazione delle dashboard, consulta la [panoramica sulla personalizzazione delle dashboard](../customize/overview.md).
