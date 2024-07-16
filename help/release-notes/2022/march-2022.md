---
title: Note sulla versione di Adobe Experience Platform - Marzo 2022
description: Note sulla versione di Adobe Experience Platform di marzo 2022.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 13%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 30 marzo 2022**

Nuove funzioni di Adobe Experience Platform:

- [Registri di audit](#audit-logs)
- [Account correlati in Real-Time CDP B2B Edition](#related-accounts)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Raccolta dati](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Origini](#sources)

## Registri di audit {#audit-logs}

Experience Platform consente di controllare l’attività dell’utente per vari servizi e funzionalità. I registri di audit forniscono informazioni su chi ha fatto cosa e quando.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Registri di audit per set di dati, schema, classe, gruppo di campi, tipo di dati, sandbox, destinazione, segmento, criterio di unione, attributo calcolato, profilo di prodotto e account (Adobe) | Si tratta delle risorse registrate dai registri di audit. Se la funzione è abilitata, i registri di audit verranno raccolti automaticamente quando si verifica l’attività. Non è necessario abilitare manualmente la raccolta dei registri. |
| Esportare i registri di audit | I registri di controllo possono essere scaricati come file `CSV` o `JSON`. I file generati vengono salvati direttamente nel computer. |

{style="table-layout:auto"}

Per ulteriori informazioni sui registri di controllo in Platform, consulta la [panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## Account correlati in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>La funzione Account correlati è disponibile solo per i clienti della versione B2B di Real-Time CDP.

Le aziende B2B spesso dispongono di informazioni sui propri clienti archiviate in più sistemi, ciascuno dei quali include solo dati parziali o addirittura in conflitto per la stessa entità aziendale reale. Questo crea una sfida enorme: ottenere una visione accurata dei propri clienti, riducendo l&#39;efficienza e l&#39;efficacia delle attività di marketing e vendita B2B. Con il rilascio degli account correlati, [!DNL Real-Time CDP B2B] ora mostra un elenco di account simili a quelli che stai esplorando. Puoi includere i conti correlati nelle definizioni dei segmenti per ampliare la portata o applicare criteri più ampi ai segmenti.

Ulteriori informazioni sulla funzione sono disponibili nelle seguenti pagine della documentazione:

- [Panoramica degli account correlati in Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Scheda Account correlati nella guida dell’interfaccia utente del profilo account](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Come utilizzare gli account correlati nelle definizioni dei segmenti](../../rtcdp/segmentation/b2b.md#related-accounts)

Per ulteriori informazioni sulla versione B2B di Real-Time CDP, consulta la [panoramica](../../rtcdp/overview.md).

## Avvisi {#alerts}

Un Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. Puoi abbonarti a diverse regole di avviso tramite la scheda [!UICONTROL Avvisi] nell&#39;interfaccia utente di Platform e scegliere di ricevere messaggi di avviso all&#39;interno dell&#39;interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove regole di avviso | Sono ora disponibili due nuove regole di avviso per le origini relative all’acquisizione dei dati. Per un elenco aggiornato dei tipi di avviso, consulta la panoramica sulle [regole di avviso](../../observability/alerts/rules.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi in Platform, consulta la [panoramica degli avvisi](../../observability/alerts/overview.md).

## Dashboard {#dashboards}

In Adobe Experience Platform sono disponibili più [!DNL dashboards] tramite i quali è possibile visualizzare informazioni importanti sui dati dell&#39;organizzazione, acquisite durante gli snapshot giornalieri.

### Dashboard dei profili

Nel dashboard Profili viene visualizzata un’istantanea dei dati attributo (record) di cui dispone la tua organizzazione nell’archivio Profili di Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget profili non segmentati | Il widget fornisce il numero totale di tutti i profili non collegati a nessun segmento. Il numero generato è preciso all’ultima istantanea e rappresenta l’opportunità di attivazione del profilo nell’organizzazione. Per ulteriori informazioni, consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget tendenza profili non segmentati | Questo widget fornisce un grafico a linee illustrativo del numero di profili non collegati ad alcun segmento in un dato periodo di tempo. La tendenza può essere visualizzata in periodi di 30 giorni, 90 giorni e 12 mesi. Per ulteriori informazioni, consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget Profili non segmentati per identità | Questo widget categorizza il numero totale di profili non segmentati in base al loro identificatore univoco. I dati vengono visualizzati in un grafico a barre. Per ulteriori informazioni, consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget per profili di identità singoli | Questo widget fornisce un conteggio dei profili della tua organizzazione che hanno un solo tipo di ID che crea la loro identità, tramite e-mail o ECID. Per ulteriori informazioni, consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets). |

{style="table-layout:auto"}

Per ulteriori informazioni sui dashboard dei profili, consulta la [Panoramica dei dashboard dei profili](../../dashboards/guides/profiles.md).

### Dashboard di destinazione

Nel dashboard Destinazioni viene visualizzata un’istantanea delle destinazioni attivate dalla tua organizzazione in Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget conteggio destinazioni | Il widget fornisce il numero totale di endpoint disponibili in cui un pubblico può essere attivato e distribuito all’interno del sistema. Questo numero include sia destinazioni attive che inattive. Per ulteriori informazioni, consulta la [documentazione sul widget standard delle destinazioni](../../dashboards/guides/destinations.md#standard-widgets). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard di destinazione in Platform, consulta la [Panoramica delle dashboard di destinazione](../../dashboards/guides/destinations.md).

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli all’Edge Network di Adobe Experience Platform dove possono essere arricchiti, trasformati e distribuiti a destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Impostazioni globali dello stream di dati | Ora puoi configurare diverse nuove impostazioni globali durante la configurazione di un flusso di dati: geolocalizzazione, cookie ID di prime parti e sincronizzazione ID di terze parti. Per ulteriori informazioni, consulta la sezione sulla [configurazione di uno stream di dati](../../datastreams/overview.md#create) nella guida dell&#39;interfaccia utente dello stream di dati. |
| [API server Edge Network](../../server-api/overview.md) | L’API server consente ai clienti di interagire con l’Edge Network di Experience Platform utilizzando un nuovo endpoint autenticato, per potenziare una varietà di casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. |

Per ulteriori informazioni sulla raccolta dati in Platform, consulta la [panoramica sulla raccolta dati](../../collection/home.md).

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. È possibile unire qualsiasi set di dati da [!DNL Data Lake] e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l&#39;acquisizione in Real-Time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| `table_exists` | Il comando new feature viene utilizzato per confermare se una tabella esiste nel sistema. Il comando restituisce un valore booleano: `true` se la tabella **esiste** e `false` se la tabella **non** esiste. Per ulteriori informazioni, vedere la [documentazione relativa alla sintassi SQL](../../query-service/sql/syntax.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle funzionalità disponibili, consulta la [Panoramica di Query Service](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire l’acquisizione dei dati in.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove fonti ora disponibili per l’utilizzo B2B | Ora puoi utilizzare tutte le origini disponibili su Platform per i casi d’uso B2B. Per un elenco completo delle origini disponibili, vedere il [catalogo origini](../../sources/home.md). |
| Disponibilità generale della nuova origine [!DNL Oracle Eloqua] | Ora puoi utilizzare l&#39;origine [!DNL Oracle Eloqua] per acquisire facilmente i dati dall&#39;istanza [!DNL Oracle Eloqua] (account, campagna, contatti) a Platform. Per ulteriori informazioni, consulta la documentazione sulla [creazione di una [!DNL Oracle Eloqua] connessione di origine](../../sources/connectors/marketing-automation/oracle-eloqua.md). |
| Miglioramenti API per [!DNL Data Landing Zone] | L&#39;origine [!DNL Data Landing Zone] ora supporta il rilevamento automatico delle proprietà dei file quando si utilizza l&#39;API [!DNL Flow Service]. Per ulteriori informazioni, consulta la documentazione sulla [creazione di una [!DNL Data Landing Zone] connessione di origine](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, vedere [panoramica delle origini](../../sources/home.md).
