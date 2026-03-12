---
title: Gestire le sessioni di Query Service in Adobe Experience Platform
description: Scopri come gli amministratori possono visualizzare, monitorare e terminare le sessioni di Query Service attive per liberare la capacità inattiva e mantenere flussi di lavoro affidabili di Data Distiller.
keywords: Experience Platform;Query Service;sessioni;gestione sessione;Data Distiller;admin
solution: Experience Platform
badgeLimitedAvailability: label="Disponibilità limitata" type="Informative"
exl-id: f986177a-9a46-4fc6-927e-98b6b7dc8cfe
source-git-commit: 2117b7ad0f507b5a35595d702cb8a70e2e09f39d
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# Gestire le sessioni di Query Service

>[!AVAILABILITY]
>
>La gestione delle sessioni per Query Service è attualmente a disponibilità limitata ed è disponibile solo per le organizzazioni con **adesioni Data Distiller**. Per richiedere l’accesso, contatta il team del tuo account Adobe.

Utilizza questa guida per gestire le sessioni attive di Query Service dall’interfaccia utente di Adobe Experience Platform. La gestione delle sessioni consente agli amministratori di monitorare le sessioni simultanee dell’editor delle query nelle sandbox e liberare capacità quando gli utenti lasciano aperte le sessioni.

## Autorizzazioni necessarie per la gestione delle sessioni {#permissions}

>[!IMPORTANT]
>
>Questa funzione è destinata agli amministratori. Gli utenti finali che eseguono le query non possono gestire le sessioni.

Per visualizzare e terminare le sessioni, è necessario appartenere a un&#39;organizzazione con accesso a Data Distiller e disporre dell&#39;autorizzazione **[!UICONTROL Manage Query Session]** assegnata. Gli utenti che non dispongono delle autorizzazioni necessarie possono accedere a Query Service ma non possono visualizzare o gestire sessioni attive.

## Visualizzare le sessioni attive {#view-active-sessions}

Gli amministratori possono visualizzare tutte le sessioni di Query Service attive nelle sandbox della tua organizzazione. In Experience Platform, seleziona **[!UICONTROL Queries]** nell&#39;area di navigazione a sinistra per aprire l&#39;area di lavoro Servizio query, quindi seleziona la scheda **[!UICONTROL Admin]** per accedere alla gestione delle sessioni.

![Area di lavoro di Query Service con la scheda Amministrazione selezionata. Viene visualizzata la tabella Gestione delle sessioni in cui sono elencate le sessioni attive e inattive in più sandbox dell&#39;organizzazione.](../images/ui/session-management/session-management-admin-tab.png)

La tabella di gestione delle sessioni viene aggiornata automaticamente in tempo reale ed elenca tutte le sessioni che attualmente utilizzano la capacità di sessione concorrente di Query Service assegnata alla tua organizzazione. Ogni riga rappresenta una singola sessione aperta nell’editor delle query.

## Stato della sessione e tempo di inattività {#session-status}

La tabella delle sessioni fornisce informazioni utili per decidere se una sessione può essere terminata in modo sicuro.

| Colonna | Descrizione |
| --- | --- |
| ID utente | Adobe ID dell’utente a cui appartiene la sessione |
| Nome utente | Nome associato all’Adobe ID |
| Sandbox | Indica la sandbox in cui è in esecuzione la sessione |
| Stato sessione | Mostra se la sessione è **[!UICONTROL Active]** o **[!UICONTROL Inactive]** |
| Tempo di inattività | Visualizza per quanto tempo la sessione è stata aperta senza interazione |
| Tempo di sessione rimanente | Indica per quanto tempo la sessione può rimanere aperta prima della scadenza automatica |

### Stato sessione

**[!UICONTROL Inactive]** indica che l&#39;utente non esegue attivamente una query. Queste sessioni possono essere terminate. **[!UICONTROL Active]** indica che una query è attualmente in esecuzione. Il controllo **[!UICONTROL End session]** non è disponibile fino al completamento dell&#39;esecuzione della query.

### Tempo di inattività e tempo di sessione rimanente

Il tempo di inattività mostra quanto tempo una sessione è stata aperta senza interazione dell’utente. Il tempo di sessione rimanente indica per quanto tempo la sessione può rimanere aperta prima che venga automaticamente chiusa dal sistema. Le sessioni scadono automaticamente dopo la durata massima consentita (due ore di inattività). Questa durata è definita dal sistema e non può essere configurata.

## Termina sessioni inattive {#end-idle-sessions}

Puoi terminare le sessioni inattive per liberare la capacità delle sessioni simultanee per altri utenti. È consigliabile terminare le sessioni con un tempo di inattività elevato quando gli utenti non lavorano più attivamente.

Dalla tabella di gestione delle sessioni, selezionare **[!UICONTROL End session]** per scegliere la sessione inattiva che si desidera terminare.

![Tabella di gestione delle sessioni che mostra una sessione inattiva evidenziata dall&#39;opzione Fine sessione.](../images/ui/session-management/end-session.png)

Viene visualizzata una finestra di dialogo di conferma per evitare la terminazione accidentale. Seleziona **[!UICONTROL End session]** nella finestra di dialogo per confermare l&#39;azione.

![La finestra di dialogo di conferma della sessione di fine visualizza un messaggio di avviso e la sessione di fine viene evidenziata.](../images/ui/session-management/end-session-confirmation-dialog.png)

Al termine della sessione, la sessione viene rimossa dalla tabella, la capacità diventa immediatamente disponibile e l’azione viene registrata per il controllo.

>[!NOTE]
>
>Impossibile terminare le sessioni con stato **[!UICONTROL Active]**. Questa protezione impedisce l&#39;interruzione dei carichi di lavoro in corso.

## Comportamento della sessione dopo la terminazione {#session-behavior-after-termination}

Quando un amministratore termina una sessione, il codice dell’utente interessato rimane nell’editor senza perdere il lavoro. Se l’utente tenta di eseguire una query dopo la terminazione, il sistema rileva la sessione terminata, ristabilisce la connessione automaticamente e mantiene intatto il contenuto dell’editor delle query.

Questo comportamento assicura che gli utenti non perdano il lavoro scritto nell’editor e possano continuare una volta stabilita una nuova sessione.

## Registri di audit per la gestione delle sessioni {#audit-logs}

Il sistema registra le azioni di gestione delle sessioni per fornire visibilità e responsabilità. I registri di controllo registrano l’ID della sessione, l’utente di cui è stata terminata la sessione, l’amministratore che ha eseguito l’azione e l’ora dell’azione.

Utilizza i registri di audit per rivedere la cronologia di terminazione delle sessioni ed esaminare le disconnessioni impreviste.

Per ulteriori informazioni sulla visualizzazione dei registri di controllo, vedere la [Guida del registro di controllo di Query Service](../data-governance/audit-log-guide.md).

## Passaggi successivi {#next-steps}

Per estendere l’utilizzo di Query Service e Data Distiller, considera le seguenti risorse:

* [Scopri come gli utenti creano ed eseguono query nella guida utente di Query Editor](user-guide.md)
* [Monitorare i carichi di lavoro pianificati utilizzando la documentazione di monitoraggio delle query pianificate](monitor-queries.md)
