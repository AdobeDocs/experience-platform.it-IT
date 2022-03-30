---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: 04d35137a301492794ab8c0c67183cf5c76f2105
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 30 marzo 2022**

Nuove funzioni in Adobe Experience Platform:

- [Registri di controllo](#audit-logs)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Experience Data Model (XDM)](#xdm)
- [[!DNL Query Service]](#query-service)
- [Origini](#sources)

## Registri di controllo {#audit-logs}

L’Experience Platform ti consente di controllare l’attività dell’utente per vari servizi e funzionalità. I registri di controllo forniscono informazioni su chi ha fatto cosa e quando.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Registri di controllo per Dataset, Schema, Classe, Gruppo di campi, Tipo di dati, Sandbox, Destinazione, Segmento, Criteri di unione, Attributo calcolato, Profilo di prodotto e account (Adobe) | Sono le risorse registrate dai registri di controllo. Se la funzione è abilitata, i registri di controllo vengono raccolti automaticamente quando si verifica l’attività. Non è necessario abilitare manualmente la raccolta di registri. |
| Esportare i registri di controllo | I registri di controllo possono essere scaricati come `CSV` o `JSON` file. I file generati vengono salvati direttamente nel computer. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui registri di controllo in Platform, consulta [panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## Avvisi {#alerts}

L’Experience Platform ti consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite [!UICONTROL Avvisi] nell’interfaccia utente di Platform e può scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove regole di avviso | Sono ora disponibili due nuove regole di avviso per le origini relative all’inserimento dei dati. Vedi la panoramica su [regole di avviso](../../observability/alerts/rules.md) per l’elenco aggiornato dei tipi di avviso. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sugli avvisi in Platform, consulta [panoramica degli avvisi](../../observability/alerts/overview.md).

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più [!DNL dashboards] attraverso cui puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

### Dashboard di profili

Nel dashboard Profili viene visualizzata un’istantanea dei dati dell’attributo (record) dell’organizzazione all’interno dell’archivio profili in Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget Profili non segmentati | Il widget fornisce il numero totale di tutti i profili non collegati ad alcun segmento. Il numero generato è accurato rispetto all’ultima istantanea e rappresenta l’opportunità di attivazione del profilo in tutta l’organizzazione. Consulta la sezione [documentazione dei widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |
| Widget Andamento profili non segmentati | Questo widget fornisce un grafico a linee illustrativo del numero di profili che non sono collegati ad alcun segmento in un dato periodo di tempo. La tendenza può essere visualizzata per periodi di 30 giorni, 90 giorni e 12 mesi. Consulta la sezione [documentazione dei widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |
| Profili non segmentati per widget di identità | Questo widget classifica il numero totale di profili non segmentati in base al loro identificatore univoco. I dati vengono visualizzati in un grafico a barre. Consulta la sezione [documentazione dei widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |
| Widget per profili di identità singoli | Questo widget fornisce un conteggio dei profili della tua organizzazione con un solo tipo di ID che ne crea l&#39;identità, un&#39;e-mail o un ECID. Consulta la sezione [documentazione dei widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |

Per ulteriori informazioni sulle dashboard Profiles , consulta [Panoramica delle dashboard dei profili](../../dashboards/guides/profiles.md).

### Dashboard delle destinazioni

Nel dashboard Destinazioni viene visualizzata un&#39;istantanea delle destinazioni abilitate dall&#39;organizzazione in Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget conteggio destinazioni | Il widget fornisce il numero totale di endpoint disponibili in cui un pubblico può essere attivato e consegnato all&#39;interno del sistema. Questo numero include sia le destinazioni attive che quelle inattive. Consulta la sezione [documentazione sui widget standard delle destinazioni](../../dashboards/guides/destinations.md#standard-widgets) per ulteriori informazioni. |

Per ulteriori informazioni sulle dashboard Destinazioni in Platform, consulta [Panoramica delle dashboard delle destinazioni](../../dashboards/guides/destinations.md).

## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

| Funzione | Descrizione |
| --- | --- |
| Aggiunta o rimozione di singoli campi standard per uno schema | L’interfaccia utente dell’Editor di schema ora consente di aggiungere parti di gruppi di campi standard agli schemi, fornendo maggiore flessibilità per i campi che si sceglie di includere senza dover creare risorse personalizzate da zero.<br><br>È ora inoltre possibile definire campi personalizzati ad hoc direttamente all’interno della struttura dello schema e assegnarli a un gruppo di campi personalizzato nuovo o esistente senza dover prima creare o modificare il gruppo di campi.<br><br>Consulta la guida su [creazione e modifica di schemi nell’interfaccia utente](../../xdm/ui/resources/schemas.md) per ulteriori informazioni su questi nuovi flussi di lavoro. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| `table_exists` | Il comando nuova funzione viene utilizzato per verificare se nel sistema esiste o meno una tabella. Il comando restituisce un valore booleano: `true` se la tabella **does** esistono e `false` se la tabella **not** esistono. Consulta la sezione [Documentazione sulla sintassi SQL](../../query-service/sql/syntax.md) per ulteriori informazioni. |

Per ulteriori informazioni sulle funzioni disponibili, consulta [Panoramica del servizio query](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire l’inserimento dei dati in tutto il sistema.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove sorgenti ora disponibili per l’utilizzo B2B | Ora puoi utilizzare tutte le sorgenti disponibili su Platform per i casi di utilizzo B2B. Consulta la sezione [catalogo fonti](../../sources/home.md) per un elenco completo delle origini disponibili. |
| Disponibilità generale di nuove [!DNL Oracle Eloqua] source | Ora puoi utilizzare la [!DNL Oracle Eloqua] sorgente per acquisire facilmente i dati dal [!DNL Oracle Eloqua] istanza (account, campagna, contatti) a Platform. Consulta la documentazione su [creazione di un [!DNL Oracle Eloqua] connessione sorgente](../../sources/connectors/oracle-eloqua.md) per ulteriori informazioni. |
| Miglioramenti API per [!DNL Data Landing Zone] | La [!DNL Data Landing Zone] ora supporta il rilevamento automatico delle proprietà del file quando si utilizza il [!DNL Flow Service] API. Consulta la documentazione su [creazione di un [!DNL Data Landing Zone] connessione sorgente](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
