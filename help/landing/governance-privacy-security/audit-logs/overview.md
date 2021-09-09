---
title: Panoramica dei registri di controllo
description: Scopri come i registri di controllo ti consentono di vedere chi ha eseguito le azioni in Adobe Experience Platform.
exl-id: 00baf615-5b71-4e0a-b82a-ca0ce8566e7f
source-git-commit: df269a30251cb17e337ec25787d6a1eed41e9c0b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 4%

---

# Registri di controllo (beta)

>[!IMPORTANT]
>
>La funzione dei registri di controllo in Adobe Experience Platform è attualmente in versione beta. La funzionalità descritta in questa documentazione è soggetta a modifiche.

Al fine di aumentare la trasparenza e la visibilità delle attività eseguite nel sistema, Adobe Experience Platform consente di controllare l’attività degli utenti per vari servizi e funzionalità sotto forma di &quot;registri di controllo&quot;. Questi registri formano un audit trail che può essere utile per risolvere i problemi su Platform e aiutare la tua azienda a rispettare efficacemente le politiche di gestione dei dati aziendali e i requisiti normativi.

In un senso semplice, un registro di controllo indica a **chi** ha eseguito l&#39;azione **cosa** e **quando**. Ogni azione registrata in un registro contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che ha eseguito l’azione e gli attributi aggiuntivi relativi al tipo di azione.

Questo documento tratta i registri di controllo di Platform, incluso come visualizzarli e gestirli nell’interfaccia utente o nell’API.

## Tipi di eventi acquisiti dai registri di controllo

La tabella seguente indica le azioni sulle quali le risorse vengono registrate dai registri di controllo:

| Risorsa | Azioni |
| --- | --- |
| [Sandbox](../../../sandboxes/home.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Ripristino</li><li>Elimina</li></ul> |
| [Set di dati](../../../catalog/datasets/overview.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li><li>Abilita per [Profilo cliente in tempo reale](../../../profile/home.md)</li></ul> |
| [Schema](../../../xdm/schema/composition.md) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Gruppo di campi](../../../xdm/schema/composition.md#field-group) | <ul><li>Creare</li><li>Aggiornamento</li><li>Elimina</li></ul> |
| [Destinazione](../../../destinations/home.md) | <ul><li>Attiva</li></ul> |

## Accesso ai registri di controllo

Quando la funzione è abilitata per l’organizzazione, i registri di controllo vengono raccolti automaticamente quando si verifica l’attività. Non è necessario abilitare manualmente la raccolta di registri.

Per visualizzare ed esportare i registri di controllo, devi disporre dell’autorizzazione di controllo accessi &quot;Visualizza registri di controllo&quot; (disponibile nella categoria &quot;Governance dei dati&quot;). Per informazioni su come gestire le autorizzazioni individuali per le funzionalità di Platform, consulta la [documentazione sul controllo degli accessi](../../../access-control/home.md).

## Gestione dei registri di controllo nell’interfaccia utente

Puoi visualizzare i registri di controllo per diverse funzioni di Experience Platform nell’area di lavoro **[!UICONTROL Audit]** nell’interfaccia utente di Platform. L&#39;area di lavoro mostra un elenco di registri registrati, ordinati per impostazione predefinita dalla più recente alla meno recente.

![Dashboard dei registri di controllo](../../images/audit-logs/audits.png)

Il sistema visualizza solo i registri di controllo dell’ultimo anno. Tutti i registri che superano questo limite vengono rimossi automaticamente dal sistema.

Seleziona un evento dall’elenco per visualizzarne i dettagli nella barra a destra.

![Dettagli evento](../../images/audit-logs/select-event.png)

<!-- (Planned for post-beta release)
### Export an audit log

Select **[!UICONTROL Download log]** to export an audit log.
-->

## Gestione dei registri di controllo nell’API

Tutte le azioni che puoi eseguire nell’interfaccia utente possono essere eseguite anche utilizzando le chiamate API. Per ulteriori informazioni, consulta il [documento di riferimento API](https://www.adobe.io/experience-platform-apis/references/audit-query/) .

## Gestione dei registri di controllo per Adobe Admin Console

Per informazioni su come gestire i registri di controllo per le attività in Adobe Admin Console, consulta il seguente [documento](https://helpx.adobe.com/enterprise/using/audit-logs.html).

## Passaggi successivi

Questa guida illustra come gestire i registri di controllo in Experience Platform. Per ulteriori informazioni su come monitorare le attività di Platform, consulta la documentazione su [Observability Insights](../../../observability/home.md) e [monitoraggio dell’inserimento dei dati](../../../ingestion/quality/monitor-data-ingestion.md).
