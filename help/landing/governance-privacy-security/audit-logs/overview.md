---
title: Panoramica dei registri di controllo
description: Scopri come i registri di audit consentono di vedere chi ha eseguito determinate azioni in Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 49%

---

# Registri di controllo {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Azioni principali"
>abstract="Questo widget mostra i principali tipi di azioni che sono state eseguite in Experience Platform nell’intervallo di tempo selezionato. Per visualizzare l’elenco di tutte le azioni registrate in Platform, seleziona **Audit** nella barra di navigazione a sinistra."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Utenti principali"
>abstract="Questo widget mostra gli utenti che hanno eseguito il maggior numero di azioni in Experience Platform nell’intervallo temporale selezionato. Per visualizzare l’elenco di tutte le azioni registrate in Platform, seleziona **Audit** nella barra di navigazione a sinistra."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Monitorare le attività degli utenti in Platform"
>abstract="<h2>Descrizione</h2><p>Puoi monitorare l’attività degli utenti per vari servizi e funzionalità di Platform in forma di registri di audit. Questi registri formano un audit trail che registra <b>chi</b> ha eseguito <b>quale</b> azione e <b>quando</b>. I registri di audit possono essere utili per risolvere eventuali problemi relativi a Platform e aiutare la tua azienda a rispettare in modo efficace le politiche di gestione dei dati aziendali e i requisiti normativi.</p>"

Al fine di aumentare la trasparenza e la visibilità delle attività eseguite nel sistema, Adobe Experience Platform consente di controllare le attività degli utenti per vari servizi e funzionalità sotto forma di &quot;registri di audit&quot;. Questi registri costituiscono un audit trail che può essere utile per risolvere i problemi su Platform e aiutare la tua azienda a rispettare in modo efficace le politiche aziendali di gestione dei dati e i requisiti normativi.

In un certo senso, un registro di audit comunica **chi** ha eseguito **quale** azione, e **quando** l’a eseguita. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita ed eventuali attributi aggiuntivi relativi al tipo di azione.

Questo documento descrive i registri di audit in Platform, tra cui come visualizzarli e gestirli nell’interfaccia utente o nell’API.

## Tipi di eventi acquisiti dai registri di audit {#category}

La tabella seguente illustra le azioni per le quali le risorse vengono registrate dai registri di audit:

| Risorsa | Azioni |
| --- | --- |
| [Criterio di controllo dell’accesso (controllo dell’accesso basato su attributi)](../../../access-control/home.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Account (Adobe)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [istanza Attribution AI](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li></ul> |
| [Registri di controllo](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Esporta</li></ul> |
| [Classe](../../../xdm/schema/composition.md#class) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| Attributo calcolato | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Istanza di Customer AI](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li></ul> |
| [Set di dati](../../../catalog/datasets/overview.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita per [Profilo cliente in tempo reale](../../../profile/home.md)</li><li>Disattiva per profilo</li><li>Aggiungi dati</li><li>Elimina batch</li></ul> |
| [Datastream](../../../edge/datastreams/overview.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li><li>[Modifica mappatura](../../../edge/datastreams/data-prep.md)</li></ul> |
| [Tipi di dati](../../../xdm/schema/composition.md#data-type) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Destinazione](../../../destinations/home.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li><li>Attivazione set di dati</li><li>Rimozione set di dati</li><li>Attivazione profilo</li><li>Rimozione profilo</li></ul> |
| [Gruppo di campi](../../../xdm/schema/composition.md#field-group) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Grafico delle identità](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Visualizzazione</li></ul> |
| [Spazio dei nomi dell’identità](../../../identity-service/ui/identity-graph-viewer.md) | <ul><li>Crea</li><li>Aggiornamento</li></ul> |
| [Criterio di unione](../../../profile/merge-policies/overview.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Profilo di prodotto](../../../access-control/home.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Query](../../../query-service/ui/overview.md) | <ul><li>Esegui</li></ul> |
| [Modello di query](../../../query-service/ui/overview.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Ruolo (controllo dell’accesso basato su attributi)](../../../access-control/home.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Aggiungi utente</li><li>Rimuovi utente</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Ripristino</li><li>Elimina</li></ul> |
| [Query pianificata](../../../query-service/ui/overview.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita per Profilo</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Crea</li><li>Elimina</li><li>Attivazione segmento</li><li>Rimozione segmento</li></ul> |
| [Flusso di dati sorgente](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Crea</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disattiva</li><li>Attivazione set di dati</li><li>Rimuovi set di dati</li><li>Attivazione profilo</li><li>Rimozione profilo</li></ul> |
| [Ordine di lavoro](../../../hygiene/home.md) | <ul><li>Crea</li></ul> |

## Accedere ai registri di audit

Se questa funzione è abilitata per la tua organizzazione, i registri di audit vengono raccolti automaticamente quando si verifica un’attività. Non è necessario abilitare manualmente la raccolta dei registri.

Per visualizzare ed esportare i registri di audit, è necessario disporre del **[!UICONTROL Visualizza registro attività utente]** autorizzazione di controllo dell’accesso concessa (disponibile nella sezione [!UICONTROL Governance dei dati] categoria). Per informazioni su come gestire le singole autorizzazioni per le funzionalità di Platform, consulta [documentazione sul controllo degli accessi](../../../access-control/home.md).

## Gestione dei registri di audit nell’interfaccia utente {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Istruzioni"
>abstract="<ul><li>Seleziona <b>Audit</b> nel pannello di navigazione a sinistra. L’area di lavoro Audit mostra un elenco di registri registrati, ordinati per impostazione predefinita dalla più recente alla meno recente.</li>   <li> NOTA: i registri di audit vengono conservati per 365 giorni dopo i quali verranno cancellati dal sistema. Pertanto, puoi tornare indietro solo per un periodo massimo di 365 giorni. Se è necessario esaminare i dati più vecchi di 365 giorni, devi esportare i registri a cadenza regolare per soddisfare i requisiti dei criteri interni. </li><li>Seleziona un evento dall’elenco per visualizzarne i dettagli nella barra a destra. </li><li>Seleziona l’icona a imbuto (filtro) per visualizzare un elenco di filtri con cui limitare i risultati. Vengono visualizzati solo gli ultimi 1.000 record, a prescindere dai filtri selezionati. </li><li>Per esportare l’elenco corrente dei registri di audit, seleziona **Scarica registro**.</li><li>Per ulteriori informazioni su questa funzione, consulta la sezione <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=it">panoramica dei registri di audit</a> su Experience League.</li></ul>"

Puoi visualizzare i registri di controllo per diverse funzioni di Experience Platform all’interno di **[!UICONTROL Audit]** nell’interfaccia utente di Platform. Nell’area di lavoro viene visualizzato un elenco dei registri registrati, per impostazione predefinita ordinati dal più recente al meno recente.

![Dashboard dei registri di controllo](../../images/audit-logs/audits.png)

I registri di audit vengono conservati per 365 giorni dopo i quali verranno eliminati dal sistema. Pertanto, puoi tornare indietro solo per un periodo massimo di 365 giorni. Se hai bisogno di dati per più di 365 giorni, devi esportare i registri a cadenza regolare per soddisfare i requisiti delle politiche interne.

Seleziona un evento dall’elenco per visualizzarne i dettagli nella barra a destra.

![Dettagli evento](../../images/audit-logs/select-event.png)

### Filtrare i registri di audit

>[!NOTE]
Poiché si tratta di una nuova funzione, i dati visualizzati risalgono solo a marzo 2022. A seconda della risorsa selezionata, i dati precedenti potrebbero essere disponibili da gennaio 2022.


Seleziona l’icona funnel (![Icona Filtro](../../images/audit-logs/icon.png)) per visualizzare un elenco di controlli filtro che consentono di limitare i risultati. Vengono visualizzati solo gli ultimi 1.000 record, indipendentemente dai filtri selezionati.

![Filtri](../../images/audit-logs/filters.png)

Nell’interfaccia utente sono disponibili i seguenti filtri per gli eventi di audit:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Categoria] | Utilizza il menu a discesa per filtrare i risultati visualizzati in base a [categoria](#category). |
| [!UICONTROL Azione] | Filtra per azione. Attualmente solo [!UICONTROL Crea] e [!UICONTROL Elimina] Le azioni possono essere filtrate. |
| [!UICONTROL Utente] | Inserisci l’ID utente completo (ad esempio, `johndoe@acme.com`) per filtrare in base all&#39;utente. |
| [!UICONTROL Stato] | Filtra in base al fatto che l’azione sia stata consentita (completata) o negata per mancanza di [controllo degli accessi](../../../access-control/home.md) autorizzazioni. |
| [!UICONTROL Data] | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in base al quale filtrare i risultati. I dati possono essere esportati con un periodo di lookback di 90 giorni (ad esempio, da 2021-12-15 a 2022-03-15). Questo può variare a seconda del tipo di evento. |

Per rimuovere un filtro, seleziona la &quot;X&quot; sull’icona della pillola per il filtro in questione, oppure seleziona **[!UICONTROL Cancella tutto]** per rimuovere tutti i filtri.

![Cancella filtri](../../images/audit-logs/clear-filters.png)

### Esportare i registri di audit

Per esportare l’elenco corrente dei registri di audit, seleziona **[!UICONTROL Scarica registro]**.

![Scarica registro](../../images/audit-logs/download.png)

Nella finestra di dialogo visualizzata, seleziona il formato preferito (scegliendo **[!UICONTROL CSV]** o **[!UICONTROL JSON]**), quindi seleziona **[!UICONTROL Scarica]**. Il browser scarica il file generato e lo salva nel computer.

![Seleziona formato di download](../../images/audit-logs/select-download-format.png)

## Gestione dei registri di audit nell’API

Tutte le azioni che possono essere eseguite nell’interfaccia utente possono essere eseguite anche utilizzando le chiamate API. Per maggiori informazioni, consulta la [documentazione delle API ](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Gestione dei registri di audit per Adobe Admin Console

Per informazioni su come gestire i registri di audit per le attività in Adobe Admin Console, consulta i seguenti [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Passaggi successivi e risorse aggiuntive

Questa guida illustra come gestire i registri di audit in Experience Platform. Per ulteriori informazioni su come monitorare le attività di Platform, consulta la documentazione su [Observability Insights](../../../observability/home.md) e [monitoraggio dell’acquisizione dei dati](../../../ingestion/quality/monitor-data-ingestion.md).

Per comprendere meglio i registri di audit in Experience Platform, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
