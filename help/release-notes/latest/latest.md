---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b378a920380030d51956a0910271f1b1f9f4c371
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 30 marzo 2022**

Nuove funzioni in Adobe Experience Platform:

- [Registri di controllo](#audit-logs)
- [Account correlati in Real-Time CDP B2B Edition](#related-accounts)

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Avvisi](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Raccolta dati](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Origini](#sources)

<!-- - [Experience Data Model (XDM)](#xdm) -->

## Registri di controllo {#audit-logs}

L’Experience Platform ti consente di controllare l’attività dell’utente per vari servizi e funzionalità. I registri di controllo forniscono informazioni su chi ha fatto cosa e quando.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Registri di controllo per Dataset, Schema, Classe, Gruppo di campi, Tipo di dati, Sandbox, Destinazione, Segmento, Criteri di unione, Attributo calcolato, Profilo di prodotto e account (Adobe) | Sono le risorse registrate dai registri di controllo. Se la funzione è abilitata, i registri di controllo vengono raccolti automaticamente quando si verifica l’attività. Non è necessario abilitare manualmente la raccolta di registri. |
| Esportare i registri di controllo | I registri di controllo possono essere scaricati come `CSV` o `JSON` file. I file generati vengono salvati direttamente nel computer. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sui registri di controllo in Platform, consulta [panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md).

## Account correlati in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>La funzione Account correlati è disponibile solo per i clienti di Real-Time CDP B2B Edition.

Le imprese B2B spesso presentano le informazioni sui clienti memorizzate in più sistemi, ciascuno dei quali include solo dati parziali o persino in conflitto per la stessa entità aziendale nel mondo reale. Questo crea una grande sfida nell&#39;ottenere una visione accurata dei loro clienti, riducendo così l&#39;efficienza e l&#39;efficacia dei loro sforzi di marketing e vendita B2B. Con il rilascio dei relativi account, [!DNL Real-time CDP B2B] ora mostra un elenco di account simili all’account che stai esplorando. Puoi includere gli account correlati nelle definizioni dei segmenti per ampliare la portata o applicare criteri più ampi nei segmenti.

Ulteriori informazioni sulla funzione nelle seguenti pagine della documentazione:

- [Panoramica sugli account correlati in Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Scheda Account correlati nella guida dell’interfaccia utente del profilo account](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Come utilizzare account correlati nelle definizioni dei segmenti](../../rtcdp/segmentation/b2b.md#related-accounts)

Per ulteriori informazioni su Real-time CDP B2B Edition, consulta la sezione [panoramica](../../rtcdp/overview.md).

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

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle dashboard Profiles , consulta [Panoramica delle dashboard dei profili](../../dashboards/guides/profiles.md).

## Raccolta dati {#data-collection}

Platform fornisce una suite di tecnologie che ti consentono di raccogliere dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network, da cui arricchire, trasformare e distribuire a destinazioni Adobi o non Adobi.

**Nuove funzioni**

| Funzione | Descrizione |
| --- | --- |
| Impostazioni del datastream globale | È ora possibile configurare diverse nuove impostazioni globali durante la configurazione di un datastream: posizione geografica, cookie ID di prime parti e sincronizzazione ID di terze parti. Vedi la sezione su [configurazione di un datastream](../../edge/fundamentals/datastreams.md#configure) nella guida dell’interfaccia utente di Datastreams per ulteriori informazioni. |

Per ulteriori informazioni sulla raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../collection/home.md).

### Dashboard delle destinazioni

Nel dashboard Destinazioni viene visualizzata un&#39;istantanea delle destinazioni abilitate dall&#39;organizzazione in Experience Platform.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Widget conteggio destinazioni | Il widget fornisce il numero totale di endpoint disponibili in cui un pubblico può essere attivato e consegnato all&#39;interno del sistema. Questo numero include sia le destinazioni attive che quelle inattive. Consulta la sezione [documentazione sui widget standard delle destinazioni](../../dashboards/guides/destinations.md#standard-widgets) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle dashboard Destinazioni in Platform, consulta [Panoramica delle dashboard delle destinazioni](../../dashboards/guides/destinations.md).

<!-- ## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

| Feature | Description |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>You can now also define ad-hoc custom fields directly within the schema structure and assign them to a new or existing custom field group without needing to create or edit the field group beforehand.<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md). -->

## Servizio query {#query-service}

[!DNL Query Service] consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati dal [!DNL Data Lake] e acquisisci i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento in Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| `table_exists` | Il comando nuova funzione viene utilizzato per verificare se nel sistema esiste o meno una tabella. Il comando restituisce un valore booleano: `true` se la tabella **does** esistono e `false` se la tabella **not** esistono. Consulta la sezione [Documentazione sulla sintassi SQL](../../query-service/sql/syntax.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle funzioni disponibili, consulta [Panoramica del servizio query](../../query-service/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e allo stesso tempo strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire l’inserimento dei dati in tutto il sistema.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuove sorgenti ora disponibili per l’utilizzo B2B | Ora puoi utilizzare tutte le sorgenti disponibili su Platform per i casi di utilizzo B2B. Consulta la sezione [catalogo fonti](../../sources/home.md) per un elenco completo delle origini disponibili. |
| Disponibilità generale di nuove [!DNL Oracle Eloqua] source | Ora puoi utilizzare la [!DNL Oracle Eloqua] sorgente per acquisire facilmente i dati dal [!DNL Oracle Eloqua] istanza (account, campagna, contatti) a Platform. Consulta la documentazione su [creazione di un [!DNL Oracle Eloqua] connessione sorgente](../../sources/connectors/marketing-automation/oracle-eloqua.md) per ulteriori informazioni. |
| Miglioramenti API per [!DNL Data Landing Zone] | La [!DNL Data Landing Zone] ora supporta il rilevamento automatico delle proprietà del file quando si utilizza il [!DNL Flow Service] API. Consulta la documentazione su [creazione di un [!DNL Data Landing Zone] connessione sorgente](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) per ulteriori informazioni. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni sulle sorgenti, consulta la sezione [panoramica di origini](../../sources/home.md).
