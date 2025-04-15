---
title: Panoramica dei registri di controllo
description: Scopri come i registri di audit consentono di vedere chi ha eseguito determinate azioni in Adobe Experience Platform.
role: Admin,Developer
feature: Audits
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 27%

---

# Registri di audit {#audit-logs}

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_actions"
>title="Azioni principali"
>abstract="Questo widget mostra i principali tipi di azioni che sono state eseguite in Experience Platform nell’intervallo di tempo selezionato. Per visualizzare l&#39;elenco completo delle azioni registrate in Experience Platform, seleziona **Audit** nel menu di navigazione a sinistra."

>[!CONTEXTUALHELP]
>id="platform_audits_privacyconsole_users"
>title="Utenti principali"
>abstract="Questo widget mostra gli utenti che hanno eseguito il maggior numero di azioni in Experience Platform nell’intervallo temporale selezionato. Per visualizzare l&#39;elenco completo delle azioni registrate in Experience Platform, seleziona **Audit** nel menu di navigazione a sinistra."

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_description"
>title="Monitorare le attività degli utenti in Experience Platform"
>abstract="<h2>Descrizione</h2><p>Puoi monitorare l’attività degli utenti per vari servizi e funzionalità di Experience Platform sotto forma di registri di audit. Questi registri formano un audit trail che registra <b>chi</b> ha eseguito <b>quale</b> azione e <b>quando</b>. I registri di audit possono essere utili per risolvere eventuali problemi su Experience Platform e aiutare la tua azienda a rispettare in modo efficace le politiche aziendali di gestione dei dati e i requisiti normativi.</p>"

Al fine di aumentare la trasparenza e la visibilità delle attività eseguite nel sistema, Adobe Experience Platform consente di controllare le attività degli utenti per vari servizi e funzionalità sotto forma di &quot;registri di audit&quot;. Questi registri costituiscono un audit trail che può essere utile per risolvere eventuali problemi in Experience Platform e aiutare la tua azienda a rispettare in modo efficace le politiche aziendali di gestione dei dati e i requisiti normativi.

In un certo senso, un registro di controllo comunica a **chi** ha eseguito **cosa** azione e **quando**. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita e altri attributi relativi al tipo di azione.

>[!NOTE]
>
> I metadati per le azioni **Aggiungi utente** e **Rimuovi utente** nella risorsa **Ruolo** non conterranno l&#39;ID e-mail dell&#39;utente che ha eseguito l&#39;azione. Nei registri viene invece visualizzato l’ID e-mail generato dal sistema (system@adobe.com).

Questo documento descrive i registri di audit in Experience Platform e spiega come visualizzarli e gestirli nell’interfaccia utente o nell’API.

## Tipi di eventi acquisiti dai registri di audit {#category}

La tabella seguente illustra le azioni per le quali le risorse vengono registrate dai registri di audit:

| Risorsa | Azioni |
| --- | --- |
| [Controllo degli accessi regola (basato su attributi accesso controllo)](../../../access-control/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Account (Adobe Systems)](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Attribution AI istanza](../../../intelligent-services/attribution-ai/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disabilita</li></ul> |
| [Registri di controllo](../../../landing/governance-privacy-security/audit-logs/overview.md) | <ul><li>Esporta</li></ul> |
| [Classe](../../../xdm/schema/composition.md#class) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| Attributo calcolato | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Istanza di Customer AI](../../../intelligent-services/customer-ai/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disabilita</li></ul> |
| [Set di dati](../../../catalog/datasets/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita per [Profilo cliente in tempo reale](../../../profile/home.md)</li><li>Disabilita per profilo</li><li>Aggiungi dati</li><li>Elimina batch</li></ul> |
| [Stream di dati](../../../datastreams/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disabilita</li><li>[Modifica mapping](../../../datastreams/data-prep.md)</li></ul> |
| [Tipi di dati](../../../xdm/schema/composition.md#data-type) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Destinazione](../../../destinations/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disabilita</li><li>Attivazione set di dati</li><li>Rimozione set di dati</li><li>Attivazione profilo</li><li>Rimuovi profilo</li></ul> |
| [Gruppo di campi](../../../xdm/schema/composition.md#field-group) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Grafico delle identità](../../../identity-service/features/identity-graph-viewer.md) | <ul><li>Visualizzazione</li></ul> |
| [Namespace Identity](../../../identity-service/features/namespaces.md) | <ul><li>Creare</li><li>Aggiornamento</li></ul> |
| [Unisci regola](../../../profile/merge-policies/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Profilo di prodotto](../../../access-control/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Query](../../../query-service/ui/overview.md) | <ul><li>Esegui</li></ul> |
| [Modello query](../../../query-service/ui/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Ruolo (basato su attributi accesso controllo)](../../../access-control/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Aggiungi utente</li><li>Rimuovi utente</li></ul> |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Ripristino</li><li>Elimina</li></ul> |
| [Query pianificata](../../../query-service/ui/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Attiva per profilo</li></ul> |
| [Segmento](../../../segmentation/home.md) | <ul><li>Creare</li><li>Elimina</li><li>Attivazione segmento</li><li>Rimozione segmento</li></ul> |
| [Flusso dati Source](../../../sources/connectors/tutorials/ui/../../../tutorials/ui/update.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita</li><li>Disabilita</li><li>Attivazione set di dati</li><li>Rimozione set di dati</li><li>Attivazione profilo</li><li>Rimozione profilo</li></ul> |
| [Ordine di lavoro](../../../hygiene/home.md) | <ul><li>Creare</li></ul> |

## Accesso ai registri di controllo

Quando la funzionalità è abilitata per l&#39;organizzazione, i registri di controllo vengono raccolti automaticamente quando si verifica l&#39;attività. Non è necessario abilitare manualmente la raccolta dei registri.

Per visualizzare ed esportare i registri di audit, è necessario disporre dell&#39;autorizzazione di controllo dell&#39;accesso **[!UICONTROL Visualizza registro attività utente]** concessa (nella categoria [!UICONTROL Governance dei dati]). Per informazioni su come gestire le singole autorizzazioni per le funzionalità di Experience Platform, consulta la [documentazione sul controllo degli accessi](../../../access-control/home.md).

## Gestione dei registri di audit nell’interfaccia utente {#managing-audit-logs-in-the-ui}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_audits_instructions"
>title="Istruzioni"
>abstract="<ul><li>Seleziona <b>Audit</b> nel pannello di navigazione a sinistra. L’area di lavoro Audit mostra un elenco di registri registrati, ordinati per impostazione predefinita dalla più recente alla meno recente.</li>   <li> NOTA: i registri di audit vengono conservati per 365 giorni dopo i quali verranno cancellati dal sistema. Pertanto, puoi tornare indietro solo per un periodo massimo di 365 giorni. Se è necessario esaminare i dati più vecchi di 365 giorni, devi esportare i registri a cadenza regolare per soddisfare i requisiti dei criteri interni. </li><li>Seleziona un evento dall’elenco per visualizzarne i dettagli nella barra a destra. </li><li>Seleziona l’icona a imbuto (filtro) per visualizzare un elenco di filtri con cui limitare i risultati. Vengono visualizzati solo gli ultimi 1.000 record, a prescindere dai filtri selezionati. </li><li>Per esportare l’elenco corrente dei registri di audit, seleziona **Scarica registro**.</li><li>Per ulteriori informazioni su questa funzione, consulta la sezione <a href="https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/audit-logs/overview.html?lang=it">panoramica dei registri di audit</a> su Experience League.</li></ul>"

Puoi visualizzare i registri di controllo per diverse funzioni di Experience Platform nell&#39;area di lavoro **[!UICONTROL Audit]** nell&#39;interfaccia utente di Experience Platform. L&#39;area di lavoro mostra un elenco di registri registrati, ordinati per impostazione predefinita dal più recente al meno recente.

![La dashboard Controlli evidenzia i controlli di audit nel menu a sinistra.](../../images/audit-logs/audits.png)

I registri di controllo vengono conservati per 365 giorni, dopodiché vengono eliminati dal sistema. Se hai bisogno di dati per più di 365 giorni, devi esportare i registri a cadenza regolare per soddisfare i requisiti delle politiche interne.

Il metodo utilizzato per richiedere i registri di audit cambia il periodo di tempo consentito e il numero di record a cui potrai accedere. [L&#39;esportazione dei registri](#export-audit-logs) consente di tornare indietro di 365 giorni (a intervalli di 90 giorni) a un massimo di 10.000 record, dove come [interfaccia utente registro attività](#filter-audit-logs) in Experience Platform visualizza gli ultimi 90 giorni a un massimo di 1000 record.

Seleziona un evento dall’elenco per visualizzarne i dettagli nella barra a destra.

![Dashboard Controlli Registro attività scheda con il pannello Dettagli evento evidenziato.](../../images/audit-logs/select-event.png)

### Filtra registri di controllo

Seleziona l&#39;icona funnel (![icona Filtra](/help/images/icons/filter.png)) per visualizzare un elenco di controlli filtro che consentono di limitare i risultati.

>[!NOTE]
>
>Il interfaccia Experience Platform visualizza solo gli ultimi 90 giorni fino a un massimo di 1000 record, indipendentemente dai filtri applicati. Se hai bisogno di log oltre a questo limite (per un massimo di 365 giorni), dovrai [esportare i](#export-audit-logs) log di controllo.

![Dashboard dei controlli di audit con il registro attività filtrato evidenziato.](../../images/audit-logs/filters.png)

Nell’interfaccia utente sono disponibili i seguenti filtri per gli eventi di audit:

| Filtro | Descrizione |
| --- | --- |
| [!UICONTROL Categoria] | Utilizza il menu a discesa per filtrare i risultati visualizzati per [categoria](#category). |
| [!UICONTROL Azione] | Filtra per azione. Le azioni disponibili per ciascun servizio sono riportate nella tabella delle risorse precedente. |
| [!UICONTROL Utente] | Immettere l&#39;ID utente completo (ad esempio, `johndoe@acme.com`) da filtrare per utente. |
| [!UICONTROL Stato] | Consente di filtrare in base al fatto che l&#39;azione sia stata consentita (completata) o negata a causa della mancanza di [autorizzazioni di controllo di accesso](../../../access-control/home.md). |
| [!UICONTROL Data] | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in base al quale filtrare i risultati. I dati possono essere esportati con un periodo di lookback di 90 giorni (ad esempio, da 2021-12-15 a 2022-03-15). Questo può variare a seconda del tipo di evento. |

Per rimuovere un filtro, seleziona la &quot;X&quot; sull&#39;icona della pillola per il filtro in questione, oppure seleziona **[!UICONTROL Cancella tutto]** per rimuovere tutti i filtri.

![Dashboard di controllo con filtro di cancellazione evidenziato.](../../images/audit-logs/clear-filters.png)

I dati del registro di controllo restituiti contengono le seguenti informazioni su tutte le query che soddisfano i criteri di filtro selezionati.

| Nome colonna | Descrizione |
|---|---|
| [!UICONTROL Timestamp] | Data e ora esatte dell&#39;azione eseguita nel formato `month/day/year hour:minute AM/PM`. |
| [!UICONTROL Nome risorsa] | Il valore del campo [!UICONTROL Nome risorsa] dipende dalla categoria scelta come filtro. |
| [!UICONTROL Categoria] | Questo campo corrisponde alla categoria selezionata nel menu a discesa del filtro. |
| [!UICONTROL Azione] | Le azioni disponibili dipendono dalla categoria scelta come filtro. |
| [!UICONTROL Utente] | Questo campo fornisce l’ID utente che ha eseguito la query. |

![Dashboard dei controlli di audit con il registro attività filtrato evidenziato.](../../images/audit-logs/filtered.png)

### Esportare i registri di audit {#export-audit-logs}

Per esportare l’elenco corrente dei registri di audit, seleziona **[!UICONTROL Scarica registro]**.

>[!NOTE]
>
>I registri possono essere richiesti con intervalli di 90 giorni, fino a 365 giorni nel passato. Tuttavia, il numero massimo di registri che possono essere restituiti durante una singola esportazione è 10.000.

![Dashboard dei controlli con [!UICONTROL Registro di download] evidenziato.](../../images/audit-logs/download.png)

Nella finestra di dialogo visualizzata, seleziona il formato preferito (**[!UICONTROL CSV]** o **[!UICONTROL JSON]**), quindi seleziona **[!UICONTROL Scarica]**. Il browser scarica il file generato e lo salva nel computer.

![Finestra di dialogo per la selezione del formato file con [!UICONTROL Download] evidenziato.](../../images/audit-logs/select-download-format.png)

## Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi di audit per ricevere notifiche per le seguenti regole:

* Creazione pubblico
* Aggiornamento pubblico
* Eliminazione pubblico
* Creazione set di dati
* Aggiornamento set di dati
* Eliminazione set di dati
* Creazione schema
* Aggiornamento schema
* Eliminazione schema

Seleziona l&#39;avviso desiderato dall&#39;elenco per iscriverti e ricevere notifiche. Per ulteriori informazioni sugli avvisi, consulta la guida alla [sottoscrizione agli avvisi utilizzando il interfaccia](../../../observability/alerts/ui.md).

## Gestione dei log di controllo nell&#39;API

Tutte le azioni che puoi eseguire nel interfaccia possono essere eseguite anche utilizzando chiamate API. Per ulteriori informazioni, consulta il [documento di riferimento API](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Gestione dei registri di audit per Adobe Admin Console

Per informazioni su come gestire i registri di audit per le attività in Adobe Admin Console, consulta il seguente [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Successivo passaggi e risorse aggiuntive

Questa guida spiega come gestire i registri di controllo in Experience Platform. Per ulteriori informazioni su come monitorare le attività di Experience Platform, consulta la documentazione relativa all&#39;osservabilità Insights](../../../observability/home.md) e [al monitoraggio dell&#39;assimilazione [](../../../ingestion/quality/monitor-data-ingestion.md)dei dati.

Per migliorare la tua comprensione dei log di controllo in Experience Platform, guarda il seguente video:

>[!VIDEO](https://video.tv.adobe.com/v/341450?quality=12&learn=on)
