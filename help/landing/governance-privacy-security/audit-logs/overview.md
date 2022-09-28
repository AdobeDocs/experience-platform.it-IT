---
title: Panoramica dei registri di controllo
description: Scopri come i registri di audit consentono di vedere chi ha eseguito determinate azioni in Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: fdc61c920ee9ae2c66344e781334844d38b44806
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 13%

---

# Registri di controllo {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Azioni principali"
>abstract="Questo widget mostra i principali tipi di azioni che sono state eseguite in Experience Platform nell&#39;intervallo di tempo selezionato. Per visualizzare l’elenco completo delle azioni registrate in Platform, seleziona **Audit** nella navigazione a sinistra."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Utenti principali"
>abstract="Questo widget mostra gli utenti che hanno eseguito il maggior numero di azioni in Experience Platform entro l&#39;intervallo temporale selezionato. Per visualizzare l’elenco completo delle azioni registrate in Platform, seleziona **Audit** nella navigazione a sinistra."

Al fine di aumentare la trasparenza e la visibilità delle attività eseguite nel sistema, Adobe Experience Platform consente di controllare l’attività degli utenti per vari servizi e funzionalità sotto forma di &quot;registri di controllo&quot;. Questi registri formano un audit trail che può essere utile per risolvere i problemi su Platform e aiutare la tua azienda a rispettare efficacemente le politiche di gestione dei dati aziendali e i requisiti normativi.

In un certo senso, un registro di controllo comunica **chi** eseguito **cosa** e **quando**. Ogni azione registrata in un registro contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che ha eseguito l’azione e gli attributi aggiuntivi relativi al tipo di azione.

Questo documento tratta i registri di controllo di Platform, incluso come visualizzarli e gestirli nell’interfaccia utente o nell’API.

## Tipi di eventi acquisiti dai registri di audit {#category}

La tabella seguente indica le azioni sulle quali le risorse vengono registrate dai registri di controllo:

| Risorsa | Azioni |
| --- | --- |
| [Criteri di controllo degli accessi (controllo degli accessi basato sugli attributi)](../../../access-control/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Account (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Attribution AI](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li></ul> |
| [Registri di controllo](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Esporta</li></ul> |
| [Classe](../../../xdm/schema/composition.md#class) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Attributo calcolato](../../../profile/computed-attributes/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Istanza di Customer AI](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li></ul> |
| [Set di dati](../../../catalog/datasets/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita per [Profilo cliente in tempo reale](../../../profile/home.md)</li><li>Disattiva per profilo</li><li>Aggiungi dati</li><li>Elimina batch</li></ul> |
| [Datastream](../../../edge/datastreams/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li><li>[Modifica mappatura](../../../edge/datastreams/data-prep.md)</li></ul> |
| [Tipi di dati](../../../xdm/schema/composition.md#data-type) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Destinazione](../../../destinations/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li><li>Attiva set di dati</li><li>Rimozione set di dati</li><li>Attiva profilo</li><li>Rimuovi profilo</li></ul> |
| [Gruppo di campi](../../../xdm/schema/composition.md#field-group) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Grafico di identità](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Visualizzazione</li></ul> |
| [Spazio dei nomi identità](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Creare</li><li>Aggiornamento</li></ul> |
| [Criteri di unione](../../../profile/merge-policies/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Profilo di prodotto](../../../access-control/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Query](../../../query-service/ui/overview.md) | <ul><li>Esegui</li></ul> |
| [Modello di query](../../../query-service/ui/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Ruolo (controllo dell’accesso basato sugli attributi)](../../../access-control/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Aggiungi utente</li><li>Rimuovi utente</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Ripristino</li><li>Elimina</li></ul> |
| [Query pianificata](../../../query-service/ui/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita per profilo</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Creare</li><li>Elimina</li><li>Attiva segmento</li><li>Rimozione segmento</li></ul> |
| [Flusso dei dati di origine](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li><li>Attivazione set di dati</li><li>Rimozione del set di dati</li><li>Attivazione profilo</li><li>Rimozione profilo</li></ul> |
| [Ordine del lavoro](../../../hygiene/home.md) | <ul><li>Creare</li></ul> |

## Accesso ai registri di controllo

Quando la funzione è abilitata per l’organizzazione, i registri di controllo vengono raccolti automaticamente quando si verifica l’attività. Non è necessario abilitare manualmente la raccolta di registri.

Per visualizzare ed esportare i registri di controllo, è necessario disporre dei **[!UICONTROL Visualizza registro attività utente]** autorizzazione al controllo degli accessi concessa (reperibile sotto [!UICONTROL Governance dei dati] categoria). Per informazioni su come gestire le autorizzazioni individuali per le funzionalità di Platform, consulta [documentazione sul controllo degli accessi](../../../access-control/home.md).

## Gestione dei registri di controllo nell’interfaccia utente

Puoi visualizzare i registri di controllo per diverse funzioni di Experience Platform all’interno di **[!UICONTROL Audit]** nell’interfaccia utente di Platform. L&#39;area di lavoro mostra un elenco di registri registrati, ordinati per impostazione predefinita dalla più recente alla meno recente.

![Dashboard dei registri di controllo](../../images/audit-logs/audits.png)

I registri di controllo vengono conservati per 365 giorni dopo i quali verranno cancellati dal sistema. Pertanto, puoi tornare indietro solo per un periodo massimo di 365 giorni. Se hai bisogno di dati superiori a 365 giorni, devi esportare i registri a cadenza regolare per soddisfare i tuoi requisiti di politica interna.

Seleziona un evento dall’elenco per visualizzarne i dettagli nella barra a destra.

![Dettagli evento](../../images/audit-logs/select-event.png)

### Filtrare i registri di controllo

>[!NOTE]
>
>Poiché questa è una nuova funzione, i dati visualizzati risalgono solo a marzo 2022. A seconda della risorsa selezionata, i dati precedenti potrebbero essere disponibili a partire da gennaio 2022.


Seleziona l’icona funnel (![Icona Filtro](../../images/audit-logs/icon.png)) per visualizzare un elenco di controlli filtro per limitare i risultati. Vengono visualizzati solo gli ultimi 1000 record, indipendentemente dai vari filtri selezionati.

![Filtri](../../images/audit-logs/filters.png)

Nell’interfaccia utente sono disponibili i seguenti filtri per gli eventi di controllo:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Categoria] | Utilizza il menu a discesa per filtrare i risultati visualizzati in base a [categoria](#category). |
| [!UICONTROL Azione] | Filtrare per azione. Attualmente solo [!UICONTROL Crea] e [!UICONTROL Elimina] le azioni possono essere filtrate. |
| [!UICONTROL Utente] | Immetti l’ID utente completo (ad esempio, `johndoe@acme.com`) per filtrare in base all’utente. |
| [!UICONTROL Stato] | Filtrare in base al fatto che l&#39;azione sia stata consentita (completata) o negata per mancanza di [controllo di accesso](../../../access-control/home.md) autorizzazioni. |
| [!UICONTROL Data] | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in cui filtrare i risultati. I dati possono essere esportati con un periodo di lookback di 90 giorni (ad esempio dal 2021-12-15 al 2022-03-15). Questo può variare a seconda del tipo di evento. |

Per rimuovere un filtro, seleziona la &quot;X&quot; sull&#39;icona della pillola per il filtro in questione o seleziona **[!UICONTROL Cancella tutto]** per rimuovere tutti i filtri.

![Cancella filtri](../../images/audit-logs/clear-filters.png)

### Esportare i registri di controllo

Per esportare l’elenco corrente dei registri di controllo, seleziona **[!UICONTROL Scarica registro]**.

![Scarica registro](../../images/audit-logs/download.png)

Nella finestra di dialogo visualizzata, seleziona il formato desiderato (o **[!UICONTROL CSV]** o **[!UICONTROL JSON]**), quindi seleziona **[!UICONTROL Scarica]**. Il browser scarica il file generato e lo salva nel computer.

![Selezionare il formato di download](../../images/audit-logs/select-download-format.png)

## Gestione dei registri di controllo nell’API

Tutte le azioni che puoi eseguire nell’interfaccia utente possono essere eseguite anche utilizzando le chiamate API. Consulta la sezione [Documento di riferimento API](https://www.adobe.io/experience-platform-apis/references/audit-query/) per ulteriori informazioni.

## Gestione dei registri di controllo per Adobe Admin Console

Per scoprire come gestire i registri di controllo per le attività in Adobe Admin Console, consulta quanto segue [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Passaggi successivi e risorse aggiuntive

Questa guida illustra come gestire i registri di controllo in Experience Platform. Per ulteriori informazioni su come monitorare le attività di Platform, consulta la documentazione su [Informazioni sull’osservabilità](../../../observability/home.md) e [monitoraggio dell’acquisizione dei dati](../../../ingestion/quality/monitor-data-ingestion.md).

Per comprendere meglio i registri di controllo in Experience Platform, guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
