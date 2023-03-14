---
title: Note sulla versione di Adobe Experience Platform, marzo 2022
description: Note sulla versione di marzo 2022 per Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 30 marzo 2022**

Nuove funzioni di Adobe Experience Platform:

- [Registri di controllo](#audit-logs)
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
| Esportare i registri di audit | I registri di audit possono essere scaricati come `CSV` o `JSON` file. I file generati vengono salvati direttamente nel computer. |

{style="table-layout:auto"}

Per ulteriori informazioni sui registri di audit in Platform, consulta [panoramica dei registri di audit](../../landing/governance-privacy-security/audit-logs/overview.md).

## Account correlati in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>La funzione Account correlati è disponibile solo per i clienti della versione B2B di Real-Time CDP.

Le aziende B2B spesso dispongono di informazioni sui propri clienti archiviate in più sistemi, ciascuno dei quali include solo dati parziali o addirittura in conflitto per la stessa entità aziendale reale. Questo crea una sfida enorme: ottenere una visione accurata dei propri clienti, riducendo l&#39;efficienza e l&#39;efficacia delle attività di marketing e vendita B2B. Con il rilascio dei relativi conti, [!DNL Real-Time CDP B2B] ora mostra un elenco di account simili a quelli che stai esplorando. Puoi includere i conti correlati nelle definizioni dei segmenti per ampliare la portata o applicare criteri più ampi ai segmenti.

Ulteriori informazioni sulla funzione sono disponibili nelle seguenti pagine della documentazione:

- [Panoramica sugli account correlati in Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Scheda Account correlati nella guida dell’interfaccia utente del profilo account](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Come utilizzare gli account correlati nelle definizioni dei segmenti](../../rtcdp/segmentation/b2b.md#related-accounts)

Per ulteriori informazioni sulla versione B2B di Real-Time CDP, consulta [panoramica](../../rtcdp/overview.md).

## Avvisi {#alerts}

Un Experience Platform consente di abbonarti agli avvisi basati su eventi per varie attività di Platform. È possibile abbonarsi a diverse regole di avviso tramite [!UICONTROL Avvisi] nell’interfaccia utente di Platform e può scegliere di ricevere messaggi di avviso all’interno dell’interfaccia utente stessa o tramite notifiche e-mail.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove regole di avviso | Sono ora disponibili due nuove regole di avviso per le origini relative all’acquisizione dei dati. Consulta la panoramica su [regole di avviso](../../observability/alerts/rules.md) per l’elenco aggiornato dei tipi di avviso. |

{style="table-layout:auto"}

Per ulteriori informazioni sugli avvisi in Platform, consulta [panoramica degli avvisi](../../observability/alerts/overview.md).

## Dashboard {#dashboards}

Adobe Experience Platform offre più [!DNL dashboards] attraverso cui è possibile visualizzare informazioni importanti sui dati dell’organizzazione, acquisite durante le istantanee giornaliere.

### Dashboard dei profili

Nel dashboard Profili viene visualizzata un’istantanea dei dati attributo (record) di cui dispone la tua organizzazione nell’archivio profili di Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget profili non segmentati | Il widget fornisce il numero totale di tutti i profili non collegati a nessun segmento. Il numero generato è preciso all’ultima istantanea e rappresenta l’opportunità di attivazione del profilo nell’organizzazione. Consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |
| Widget tendenza profili non segmentati | Questo widget fornisce un’illustrazione del grafico a linee per il numero di profili che non sono collegati a nessun segmento in un determinato periodo di tempo. La tendenza può essere visualizzata in periodi di 30 giorni, 90 giorni e 12 mesi. Consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |
| Widget Profili non segmentati per identità | Questo widget categorizza il numero totale di profili non segmentati in base al loro identificatore univoco. I dati vengono visualizzati in un grafico a barre. Consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |
| Widget per profili di identità singoli | Questo widget fornisce un conteggio dei profili della tua organizzazione che hanno un solo tipo di ID che crea la loro identità, tramite e-mail o ECID. Consulta la [documentazione sui widget standard dei profili](../../dashboards/guides/profiles.md#standard-widgets) per ulteriori informazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard dei profili, consulta [Panoramica delle dashboard dei profili](../../dashboards/guides/profiles.md).

### Dashboard di destinazione

Nel dashboard Destinazioni viene visualizzata un’istantanea delle destinazioni abilitate dalla tua organizzazione in Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget conteggio destinazioni | Il widget fornisce il numero totale di endpoint disponibili in cui un pubblico può essere attivato e distribuito all’interno del sistema. Questo numero include sia destinazioni attive che inattive. Consulta la [documentazione widget standard destinazioni](../../dashboards/guides/destinations.md#standard-widgets) per ulteriori informazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard di Destinazioni in Platform, consulta [Panoramica delle dashboard di Destinazioni](../../dashboards/guides/destinations.md).

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, dove possono essere arricchiti, trasformati e distribuiti a destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Impostazioni globali dello stream di dati | Ora puoi configurare diverse nuove impostazioni globali durante la configurazione di un flusso di dati: geolocalizzazione, cookie ID di prime parti e sincronizzazione ID di terze parti. Consulta la sezione su [configurazione di uno stream di dati](../../edge/datastreams/overview.md#create) per ulteriori informazioni, consulta la guida all’interfaccia utente per gli stream di dati. |
| [API del server di rete Edge](../../server-api/overview.md) | L’API server consente ai clienti di interagire con la rete Edge di Experience Platform utilizzando un nuovo endpoint autenticato, per supportare una varietà di casi di utilizzo di raccolta dati, personalizzazione, pubblicità e marketing. |

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati da [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’acquisizione in Real-time Customer Profile.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| `table_exists` | Il comando new feature viene utilizzato per confermare se una tabella esiste nel sistema. Il comando restituisce un valore booleano: `true` se la tabella **fa** esistono, e `false` se la tabella non **non** esiste. Consulta la [Documentazione sulla sintassi SQL](../../query-service/sql/syntax.md) per ulteriori informazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle funzioni disponibili, consulta [Panoramica di Query Service](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e allo stesso tempo strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire l’acquisizione dei dati in.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove fonti ora disponibili per l’utilizzo B2B | Ora puoi utilizzare tutte le origini disponibili su Platform per i casi d’uso B2B. Consulta la [catalogo origini](../../sources/home.md) per un elenco completo delle fonti disponibili. |
| Disponibilità generale di nuovi [!DNL Oracle Eloqua] sorgente | Ora puoi utilizzare la [!DNL Oracle Eloqua] per acquisire facilmente i dati dalle tue [!DNL Oracle Eloqua] (account, campagna, contatti) su Platform. Consulta la documentazione su [creazione di un [!DNL Oracle Eloqua] connessione sorgente](../../sources/connectors/marketing-automation/oracle-eloqua.md) per ulteriori informazioni. |
| Miglioramenti API per [!DNL Data Landing Zone] | Il [!DNL Data Landing Zone] la sorgente ora supporta il rilevamento automatico delle proprietà dei file quando si utilizza [!DNL Flow Service] API. Consulta la documentazione su [creazione di [!DNL Data Landing Zone] connessione sorgente](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) per ulteriori informazioni. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta [panoramica sulle origini](../../sources/home.md).
