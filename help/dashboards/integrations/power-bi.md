---
title: Modelli di rapporto Power BI per dashboard di Platform
description: Utilizza i modelli di report per esplorare i dati di Experience Platform utilizzando Power BI.
exl-id: fb98a79f-3d82-4e11-b08a-b7cb06414462
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# Modelli di report Power BI per dashboard

La funzione del modello di rapporto Power BI consente di creare rapporti coinvolgenti con dati provenienti da Adobe Experience Platform. Il processo di installazione semplificato installa automaticamente widget standard per Profilo cliente in tempo reale, segmentazione e destinazioni. L’installazione collega inoltre Power BI ai modelli di dati per personalizzare ed estendere facilmente i modelli di rapporto. Questi rapporti possono essere condivisi in tutta l’organizzazione senza che i destinatari abbiano bisogno delle credenziali per la tua organizzazione su Platform.

Questo documento fornisce istruzioni su come collegare Adobe Experience Platform all’applicazione Power BI e utilizzare modelli di rapporto per condividere informazioni chiave sui dati di Platform con utenti esterni.

## Introduzione

Prima di continuare con questa esercitazione, è consigliabile avere una buona comprensione di [composizione dello schema](../../xdm/schema/composition.md) in Experience Platform, e come gli attributi sono inclusi nel Profilo del cliente in tempo reale tramite il [schema unione](../../xdm/schema/composition.md#union).

Per installare l’integrazione con l’applicazione Power BI, gli utenti devono prima aver acquisito le seguenti autorizzazioni di Platform:

- Gestire le query
- Gestire le sandbox

Per informazioni su come assegnare queste autorizzazioni, leggere il [controllo di accesso](../../access-control/home.md) documentazione.

Per seguire questa esercitazione, devi disporre anche di un account Power BI . Per creare un account, passa alla pagina [Homepage Power BI](https://powerbi.microsoft.com/en-us/) e seguire il processo di registrazione. Gli utenti per questo account di Power BI devono inoltre abilitare **Creare un’area di lavoro** all&#39;interno delle impostazioni del Power BI. Questa impostazione si trova nelle impostazioni tenant del portale di amministrazione Power BI. Se il tuo account è fornito dal tenant o dal datore di lavoro, contatta il tuo amministratore per abilitare questa impostazione.

![Creazione delle impostazioni dell&#39;area di lavoro in Power BI Admin Portal.](../images/power-bi/create-workspace-settings.png)

>[!NOTE]
>
>Affinché la scheda Dashboard sia visibile nella navigazione a sinistra dell’interfaccia utente di Platform e nella vista Inventario dashboard , è necessario disporre dell’accesso a qualsiasi dashboard Profilo, Segmentazione o Destinazione come parte della licenza di Platform.

## Installare l’integrazione dell’applicazione Power BI

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Dashboard]** nel menu di navigazione a sinistra per aprire [!UICONTROL Dashboard] workspace. La [!UICONTROL Sfoglia] visualizza un elenco delle visualizzazioni del dashboard attualmente disponibili. Per ulteriori informazioni sulla visualizzazione delle dashboard disponibili, consulta [documentazione di inventario](../inventory.md).

Quindi, seleziona la **[!UICONTROL Integrazioni]** scheda . Viene visualizzata la pagina di integrazione dell&#39;applicazione Power BI. Da qui, seleziona **[!UICONTROL Installa]** per avviare l&#39;installazione.

>[!NOTE]
>
>La [!UICONTROL Installa] Il pulsante è disattivato a meno che non si disponga delle autorizzazioni Gestione servizi query e Gestione sandbox.

![Schermata Dettagli Power BI con il pulsante Installa evidenziato.](../images/power-bi/details-screen.png)

### Fornire le credenziali

Il primo passaggio del processo di installazione consiste nel fornire credenziali non in scadenza per l&#39;integrazione dell&#39;applicazione Power BI. Sono disponibili due opzioni per fornire: [[!UICONTROL Crea nuove credenziali]](#create-new-credentials) o [[!UICONTROL Usa credenziali esistenti]](#use-existing-credentials). Seleziona l’interruttore appropriato per continuare.

#### Crea nuove credenziali {#create-new-credentials}

Durante la generazione delle nuove credenziali sono necessari due campi: [!UICONTROL Nome] e [!UICONTROL Assegnato a]. La [!UICONTROL Assegnato a] Il campo si riferisce all&#39;indirizzo e-mail associato al tuo account Power BI.

![Schermata Genera nuove credenziali di Power BI.](../images/power-bi/generate-new-credentials.png)

>[!IMPORTANT]
>
>La creazione di credenziali non in scadenza richiede l&#39;assegnazione di determinate autorizzazioni e ruoli. Le autorizzazioni necessarie sono Manage Sandbox (Gestisci sandbox) e Manage Query Service Integration (Gestisci integrazione servizio query). I ruoli richiesti sono i ruoli di amministratore e sviluppatore di Adobe Experience Platform. Per informazioni su come assegnare queste autorizzazioni, leggere il [controllo di accesso](../../access-control/home.md) documentazione.

Per ulteriori informazioni sulla generazione di credenziali del servizio query non in scadenza, consulta la [guida alle credenziali non in scadenza](../../query-service/ui/credentials.md#non-expiring-credentials).

Dopo aver generato le credenziali non in scadenza per la prima volta, un file JSON viene scaricato in quel computer. Questo file JSON può quindi essere condiviso con altri utenti come credenziali per completare il processo di installazione.

#### Usa credenziali esistenti {#use-existing-credentials}

È inoltre possibile caricare un file di credenziali JSON per passare la convalida. Questi file JSON contenenti i valori delle credenziali non in scadenza vengono scaricati nel computer locale in uso quando viene creata una credenziale non in scadenza.

>[!IMPORTANT]
>
>Per utilizzare una credenziale esistente non in scadenza, è necessario che all’utente sia già stata assegnata una credenziale. Se all&#39;utente non è stata assegnata una credenziale e non è possibile crearne una nuova utilizzando Adobe Admin Console, l&#39;utente non può procedere con il processo di installazione.

Seleziona **[!UICONTROL Carica file di credenziali]**, quindi seleziona il file JSON appropriato da caricare nella finestra di dialogo visualizzata.

![Schermata delle credenziali di Power BI con il pulsante Carica file delle credenziali evidenziato.](../images/power-bi/upload-credential-file.png)

Dopo aver fornito le credenziali non in scadenza, queste vengono convalidate automaticamente da Platform. Una volta completata la convalida, viene visualizzato un messaggio di conferma. Seleziona **[!UICONTROL Successivo]** rivedere l&#39;accordo di consenso per la domanda di Power BI.

![Le credenziali non in scadenza sono state convalidate correttamente con il pulsante Successivo evidenziato.](../images/power-bi/successfully-uploaded-credential-file.png)

### Fornire il consenso

Viene visualizzata la visualizzazione del consenso. Seleziona **[!UICONTROL Verifica il consenso]** per aprire una nuova finestra che descrive le autorizzazioni necessarie affinché Power BI possa accedere ai dati e utilizzarli in base ai termini di servizio e all’informativa sulla privacy.

![Viene visualizzato il consenso fornito con il pulsante Rivedi consenso evidenziato.](../images/power-bi/provide-consent-display.png)

Seleziona **[!UICONTROL Accetta]** concedere ad Power BI l’autorizzazione per accedere e utilizzare i dati della tua Platform.

![Richiesta di autorizzazioni per l&#39;applicazione Power BI.](../images/power-bi/permissions.png)

>[!NOTE]
>
>Se si esce dal processo di installazione in qualsiasi momento prima di fornire il consenso, l&#39;integrazione dell&#39;applicazione Power BI non verrà installata nell&#39;inventario delle dashboard.

Dopo aver fornito il consenso, il modello di rapporto viene installato automaticamente nell’ambiente Power BI come parte del processo di installazione. Power BI utilizza quindi le credenziali non in scadenza per accedere a Platform, esegue in sequenza tutte le query SQL e compila il modello di report con i dati restituiti.

Seleziona **[!UICONTROL Fine]** per tornare all’inventario del dashboard.

![Viene visualizzato il consenso fornito con il pulsante Fine evidenziato.](../images/power-bi/finish-consent-review.png)

Ora che il modello di rapporto Power BI è installato, viene visualizzato nell’elenco delle dashboard disponibili sotto la sezione [!UICONTROL Sfoglia] scheda . Seleziona **[!UICONTROL Power BI]** dall’elenco per passare all’ambiente Power BI.

![Power BI elencato nell’inventario delle dashboard.](../images/power-bi/power-bi-dashboard-inventory.png)

>[!IMPORTANT]
>
>Gli amministratori di Power BI devono assicurarsi che gli utenti dispongano delle autorizzazioni di accesso appropriate per visualizzare queste dashboard nell’ambiente Power BI.

## Area di lavoro Power BI

Dopo aver effettuato l’accesso a [lo spazio di lavoro Power BI](https://dxt.powerbi.com), i modelli di report sono disponibili per ciascuno dei servizi a cui hai accesso. I modelli di rapporto includono profili, segmenti e dashboard di destinazioni **only** se dispongono delle autorizzazioni di visualizzazione corrispondenti.

Per impostazione predefinita, i widget standard da profili, segmenti e destinazioni sono disponibili nei rapporti modello Power BI .

>[!NOTE]
>
>È necessario disporre delle autorizzazioni di modifica abilitate per un determinato dashboard per consentire l’installazione di tale dashboard nell’ambiente Power BI.

![Report del modello di profilo di Power BI tramite widget standard di profilo di Platform.](../images/power-bi/profile-report-template.png)

Una volta installato un dashboard in Power BI, i modelli di report vengono visualizzati per impostazione predefinita a tutti gli utenti. Se desideri limitare l’accesso a qualsiasi modello di report, assicurati di disabilitare l’accesso per gli utenti in questione dall’ambiente Power BI.

## Personalizzare il modello di rapporto Power BI

Utilizzando widget personalizzati, puoi aggiungere attributi personalizzati al modello dati per arricchire i modelli di rapporto forniti da Power BI.

>[!NOTE]
>
>Gli attributi che è possibile utilizzare per i widget personalizzati dipendono da ciò che è disponibile nello schema di unione. Per scoprire come visualizzare ed esplorare gli schemi di unione a vantaggio dei widget personalizzati, consulta la sezione [guida all’interfaccia utente per schema unione](../../profile/ui/union-schema.md).

### Creare un widget personalizzato

I widget personalizzati vengono creati tramite la Libreria widget. Consulta la sezione [Panoramica della Libreria widget](../customize/widget-library.md) per un’introduzione alla funzione e al [esercitazione per la creazione di un widget personalizzato](../customize/custom-widgets.md) per istruzioni specifiche.

>[!IMPORTANT]
>
>I widget personalizzati appena creati sono **not** sincronizzato automaticamente tra le dashboard di Adobe Experience Platform e i modelli di report Power BI. Eventuali widget personalizzati creati nell’interfaccia utente di Platform devono essere ricreati manualmente all’interno dell’ambiente Power BI.

### Ricrea il widget personalizzato nell&#39;ambiente Power BI

Una volta che il dashboard dispone delle metriche e degli attributi appropriati contenuti nei widget personalizzati, puoi modificare il modello di rapporto visualizzato dall’interno dell’ambiente Power BI. Consulta la sezione [Documentazione Power BI](https://docs.microsoft.com/it-IT/power-bi/) per informazioni su come modificare un rapporto tramite la relativa interfaccia utente.

## Eliminare l’integrazione dell’applicazione Power BI

Per eliminare il dashboard, accedi all’inventario del dashboard e seleziona l’icona Elimina (![](../images/power-bi/delete-icon.png)) accanto al nome del dashboard.

>[!NOTE]
>
>Solo l’utente che ha installato la dashboard Power BI può eliminare l’integrazione dall’interfaccia utente di Platform.

![La scheda Sfoglia della schermata di inventario delle dashboard viene visualizzata con il pulsante Sfoglia ed è evidenziata l’icona Elimina.](../images/power-bi/delete-power-bi-dashboard.png)

Viene visualizzato un puntatore di conferma. Seleziona **[!UICONTROL Elimina]** per confermare il processo.

>[!IMPORTANT]
>
>L’eliminazione del dashboard Power BI dall’interfaccia utente della piattaforma comporta **not** elimina i modelli di rapporto disponibili nell’ambiente Power BI. Per eliminare completamente le informazioni contenute nei modelli di report Power BI, è necessario accedere al proprio account Power BI ed eliminare i modelli di report da tale ambiente. Una volta eliminato, un utente può reinstallare il dashboard Power BI seguendo le stesse istruzioni di installazione descritte in precedenza.

## Passaggi successivi

Leggendo questo documento, puoi comprendere meglio come i modelli di report Power BI possono essere integrati in Platform per condividere informazioni di dati accattivanti dai tuoi profili, segmenti o dashboard di destinazioni. Consulta la sezione [panoramica sulla personalizzazione del dashboard](../customize/overview.md) per ulteriori informazioni sulla personalizzazione delle dashboard.
