---
title: Governance dei dati in Query Service
description: Questa panoramica descrive i principali elementi di governance dei dati in Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: c98ae492b12fb5b9596f19a3d64785090439f7e1
workflow-type: tm+mt
source-wordcount: '3182'
ht-degree: 0%

---

# Governance dei dati in Query Service

Adobe Experience Platform riunisce i dati provenienti da più sistemi aziendali e consente di pulire, modellare, manipolare e arricchire i dati tramite Query Service in base alle esigenze. Questo consente agli addetti al marketing di identificare, comprendere e coinvolgere i clienti in modo migliore. Garantire un’adeguata governance dei dati è un aspetto fondamentale della gestione delle informazioni personali, in quanto alcuni dati possono essere soggetti a restrizioni di utilizzo in base a politiche organizzative e normative legali. È fondamentale garantire che i dati acquisiti e le relative operazioni siano conformi ai criteri di utilizzo dei dati definiti.

La governance dei dati in Query Service consente di gestire i dati dei clienti e garantire la conformità alle normative, alle restrizioni e alle policy applicabili all’utilizzo dei dati. Questo svolge un ruolo chiave nel garantire che i criteri di utilizzo siano stati applicati in base alle normative definite dalla tua azienda.

Si consiglia alle organizzazioni che eseguono regolarmente l’elaborazione dei dati di delineare, mettere in pratica e applicare queste linee guida per creare un ambiente consapevole della privacy per tutti gli utenti.

Le seguenti categorie sono fondamentali per rispettare le normative sulla conformità dei dati quando si utilizza Query Service:

1. Sicurezza
1. Audit
1. Utilizzo dati
1. Privacy
1. Igiene dei dati

Questo documento esamina ciascuna delle diverse aree di governance e illustra come facilitare la conformità dei dati quando si utilizza Query Service. Consulta la [panoramica su governance, privacy e sicurezza](../../landing/governance-privacy-security/overview.md) per informazioni più ampie su come Experience Platform consente di gestire i dati dei clienti e garantire la conformità.

## Sicurezza {#security}

La sicurezza dei dati è il processo di protezione dei dati da accessi non autorizzati e di garanzia di accesso sicuro per tutto il loro ciclo di vita. L’accesso sicuro viene mantenuto in Experience Platform tramite l’applicazione di ruoli e autorizzazioni tramite funzionalità quali il controllo degli accessi basato su ruoli e il controllo degli accessi basato su attributi. Credenziali, SSL e crittografia dei dati vengono utilizzati anche per garantire la protezione dei dati in Experience Platform.

La sicurezza relativa a Query Service è suddivisa nelle seguenti categorie:

* [Controllo dell&#39;accesso](#access-control): l&#39;accesso è controllato tramite ruoli e autorizzazioni che includono set di dati e autorizzazioni a livello di colonna.
* Protezione dei dati tramite [connettività](#connectivity): i dati vengono protetti tramite Experience Platform e client esterni tramite una connessione limitata con credenziali in scadenza o credenziali senza scadenza.
* Protezione dei dati tramite [crittografia e chiavi gestite dal cliente](#encryption-and-customer-managed-keys): accesso controllato tramite crittografia quando i dati sono inattivi.

### Controllo degli accessi {#access-control}

Il controllo degli accessi in Adobe Experience Platform è gestito da autorizzazioni basate sul ruolo che determinano gli utenti che possono utilizzare le funzionalità di Query Service. Allo stesso modo, puoi controllare l’accesso a attributi di dati specifici tramite la gestione delle etichette su schemi e campi di dati.

Questa sezione descrive le autorizzazioni di controllo di accesso necessarie che un utente deve disporre per utilizzare completamente le funzioni di Query Service. Per istruzioni dettagliate sull&#39;assegnazione dell&#39;accesso a un profilo di prodotto, consulta i documenti su [gestione delle autorizzazioni](../../access-control/ui/permissions.md) e [gestione degli utenti](../../access-control/ui/users.md).

#### Autorizzazioni rilevanti

I permessi di controllo d&#39;accesso pertinenti sono definiti nelle tabelle seguenti in base al loro livello di ambito.

**Autorizzazioni di esecuzione query**

Per eseguire query in Query Service, è necessario assegnare a un utente un ruolo con la seguente autorizzazione:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Manage Queries] | Questa autorizzazione consente agli utenti di eseguire esplorazione dei dati e query batch, in grado di leggere un set di dati esistente o scrivere dati su set di dati. Sono incluse sia `CREATE TABLE AS SELECT` (`CTAS`) che `INSERT INTO AS SELECT` (`ITAS`) query. |

**Autorizzazioni del set di dati**

Questa sezione funge da guida per l’accesso basato su risorse necessario per accedere ai set di dati durante l’esecuzione di query sui dati tramite Query Service.

Tramite l’interfaccia Autorizzazioni è possibile definire il controllo dell’accesso basato su risorse per un set di dati e uno schema con le seguenti autorizzazioni:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Manage Datasets] | Questa autorizzazione fornisce accesso in sola lettura per gli schemi e consente di accedere a set di dati di lettura, creazione, modifica ed eliminazione da utilizzare con Query Service. |
| [!UICONTROL View Datasets] | Questa autorizzazione consente l’accesso in sola lettura per i set di dati e gli schemi da utilizzare con Query Service. |

#### Controllo dell’accesso per colonne/campi

La funzione di controllo dell&#39;accesso basato su attributi consente agli utenti di Query Service di limitare l&#39;accesso ai dati utente critici. L’accesso può essere concesso o limitato in base alle autorizzazioni assegnate a un ruolo. L’accesso degli utenti alle singole colonne è controllato dalle relative etichette di utilizzo dei dati e dai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

L’assegnazione di tag a gruppi di campi e classi dello schema con le etichette di utilizzo dei dati applica restrizioni di utilizzo a tutti gli schemi con gli stessi gruppi di campi e le stesse classi. Per informazioni complete su questa funzione, consulta la panoramica sul controllo degli accessi basato su [attributi](../../access-control/abac/overview.md).

Questa funzione ti consente di concedere diritti di accesso su colonne riservate ai gruppi di utenti di tua scelta. Il controllo degli accessi su una colonna può limitare sia le funzionalità di lettura che quelle di scrittura per un particolare tipo di utente.

Il controllo degli accessi per le colonne può essere applicato a livello di schema sia per gli schemi standard che per quelli ad hoc. Applica le etichette di utilizzo dei dati agli schemi XDM per limitare l’accesso a una o più colonne. L’etichettatura dei dati viene applicata in modo coerente, anche per i set di dati creati tramite Query Service utilizzando uno schema predefinito o uno schema ad hoc generato come parte dell’operazione CTAS.

Una volta applicato il livello di accesso appropriato utilizzando etichette e ruoli, quando un utente tenta di accedere ai dati non accessibili si verifica il seguente comportamento di sistema:

1. Se a un utente è stato negato l’accesso a una delle colonne all’interno di uno schema, all’utente viene negata anche l’autorizzazione di lettura o scrittura sulla colonna con restrizioni. Questo vale per i seguenti scenari comuni:

   * **Caso 1**: quando un utente tenta di eseguire una query che interessa solo una colonna con restrizioni, il sistema genera un errore che indica che la colonna non esiste.
   * **Caso 2**: quando un utente tenta di eseguire una query con più colonne, inclusa una colonna con restrizioni, il sistema restituisce l&#39;output solo per tutte le colonne senza restrizioni.

1. Se un utente tenta di accedere a un campo calcolato, deve avere accesso a tutti i campi utilizzati nella composizione oppure il sistema nega l’accesso anche al campo calcolato.

#### Controlli di accesso per le viste

Query Service consente di utilizzare SQL ANSI standard per le istruzioni [`CREATE VIEW`](../sql/syntax.md#create-view). Per i flussi di lavoro con dati altamente sensibili, è necessario applicare i controlli appropriati durante la creazione delle viste.

La parola chiave `CREATE VIEW` definisce una visualizzazione di una query, ma la visualizzazione non è materializzata fisicamente. La query viene invece eseguita ogni volta che in una query viene fatto riferimento alla visualizzazione. Quando un utente crea una visualizzazione da un set di dati, le regole di controllo dell&#39;accesso basate su ruolo e attributo per il set di dati padre sono **non** applicate gerarchicamente. Di conseguenza, è necessario impostare in modo esplicito le autorizzazioni per ciascuna delle colonne al momento della creazione di una visualizzazione.

#### Creare restrizioni di accesso basate sul campo per i set di dati accelerati {#create-field-based-access-restrictions-on-accelerated-datasets}

Con la funzionalità di controllo degli accessi [basato su attributi](../../access-control/abac/overview.md) è possibile definire ambiti di utilizzo organizzativi o dati sui set di dati fact e di dimensione nell&#39;[archivio accelerato](../data-distiller/sql-insights/send-accelerated-queries.md). Questo consente agli amministratori di gestire l’accesso a segmenti specifici e di gestire meglio l’accesso concesso a utenti o gruppi di utenti.

Per creare restrizioni di accesso basate sui campi per i set di dati accelerati, puoi utilizzare le query CTAS di Query Service per creare set di dati accelerati e strutturarli in base a schemi XDM o schemi ad hoc esistenti. Gli amministratori possono quindi [aggiungere e modificare le etichette di utilizzo dei dati per lo schema](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) o [schema ad hoc](./ad-hoc-schema-labels.md#edit-governance-labels). È possibile applicare, creare e modificare etichette agli schemi dall&#39;area di lavoro [!UICONTROL Labels] nell&#39;interfaccia utente di [!UICONTROL Schemas].

Le etichette di utilizzo dei dati possono anche essere [applicate o modificate direttamente nel set di dati](../../data-governance/labels/user-guide.md#add-labels) tramite l&#39;interfaccia utente dei set di dati o create dall&#39;area di lavoro [!UICONTROL Labels] del controllo di accesso. Per ulteriori informazioni, consulta la guida su come [creare una nuova etichetta](../../access-control/abac/ui/labels.md).

L’accesso degli utenti alle singole colonne può quindi essere controllato dalle etichette di utilizzo dei dati associate e dai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

### Connettività {#connectivity}

Query Service è accessibile tramite l’interfaccia utente di Experience Platform o creando una connessione con client esterni compatibili. L’accesso a tutti i fronti disponibili è controllato da un set di credenziali.

#### Connettività tramite client esterni

L’accesso a Query Service tramite un client di terze parti richiede le credenziali per l’autorizzazione. Queste credenziali sono obbligatorie per accedere a Query Service con qualsiasi client esterno compatibile. È possibile connettersi ai client esterni utilizzando [credenziali in scadenza](#expiring-credentials) o [credenziali senza scadenza](#non-expiring-credentials).

#### Tempo di connessione limitato tramite credenziali in scadenza {#expiring-credentials}

[Le credenziali in scadenza](../ui/credentials.md) consentono agli utenti di creare una connessione temporanea con un client esterno. Questo set di credenziali è valido solo per 24 ore. La scadenza di questi tipi di credenziali può essere visualizzata insieme alla scheda delle credenziali nel dashboard Servizio query.

![La scheda delle credenziali nell&#39;area di lavoro di Query Service con le credenziali in scadenza evidenziate.](../images/data-governance/overview/expiring-credentials.png)

#### Credenziali senza scadenza {#non-expiring-credentials}

[Le credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials) consentono di creare una connessione permanente con un client esterno, semplificando la connessione a Query Service senza la necessità di una password manuale.

Per abilitare l&#39;opzione di generazione delle credenziali senza scadenza, è necessario seguire il [flusso di lavoro preliminare](../ui/credentials.md#prerequisites) descritto. Come parte di questo processo, l’amministratore dell’organizzazione deve configurare le autorizzazioni per il profilo di prodotto, consentendo all’amministratore di controllare quali account dispongono dell’accesso per utilizzare credenziali senza scadenza.

Agli account utente tecnici autorizzati con credenziali senza scadenza possono essere assegnati ruoli per garantire una governance dei dati appropriata definendo l’ambito del loro accesso in lettura e scrittura in base alle loro responsabilità e esigenze. Consulta la sezione precedente su [utilizzo di autorizzazioni basate su ruoli tramite il controllo degli accessi](#access-control) per gestire l&#39;accesso a Query Service.

Una volta completato il flusso di lavoro dei prerequisiti, gli utenti autorizzati possono ora [generare le credenziali di connessione richieste](../ui/credentials.md#generate-credentials).

#### Crittografia dei dati SSL

Per una maggiore sicurezza, Query Service fornisce supporto nativo per le connessioni SSL per crittografare le comunicazioni client/server. Experience Platform supporta varie opzioni SSL per soddisfare le tue esigenze di sicurezza dei dati e bilanciare il sovraccarico di elaborazione dovuto alla crittografia e allo scambio di chiavi.

Per ulteriori informazioni, tra cui come connettersi utilizzando il valore del parametro SSL `verify-full`, vedere la guida sulle [opzioni SSL disponibili per le connessioni client di terze parti a Query Service](../clients/ssl-modes.md).

### Crittografia e chiavi gestite dal cliente (CMK) {#encryption-and-customer-managed-keys}

La crittografia è l&#39;utilizzo di un processo algoritmico per trasformare i dati in testo codificato e illeggibile per garantire che le informazioni siano protette e inaccessibili senza una chiave di decrittografia.

La conformità dei dati di Query Service garantisce che i dati siano sempre crittografati. I dati in transito sono sempre conformi a HTTPS e i dati a riposo sono crittografati in un archivio Azure Data Lake utilizzando chiavi a livello di sistema. Per ulteriori informazioni, vedere la documentazione su [come vengono crittografati i dati in Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md). Per informazioni dettagliate su come i dati inattivi vengono crittografati nell&#39;archiviazione Azure Data Lake, consulta la [documentazione ufficiale di Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

I dati in transito sono sempre conformi HTTPS. Analogamente, quando i dati sono inattivi nel data lake, la crittografia viene eseguita con la chiave di gestione del cliente (CMK), già supportata da Data Lake Management. The currently supported version is TLS1.2. See the [customer-managed keys (CMK) documentation](../../landing/governance-privacy-security/customer-managed-keys/overview.md) to learn how to set up your own encryption keys for data stored in Adobe Experience Platform.


## Audit {#audit}

Query Service records user activity and categorizes that activity in different log types. Logs supply information on **who** performed **what** action, and **when**. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita e altri attributi relativi al tipo di azione.

Any of the log categories can be requested as desired by an Experience Platform user. This section provides details on the type of information captured for Query Service and where this information can be accessed.

### Query logs {#query-logs}

The query logs UI allows you to monitor and review execution details for all queries that have been run either via the Query Editor or the Query Service API. This brings transparency to Query Service activities, allowing you to check the metadata for **all** the queries that have been executed across Query Service. It includes all types of queries whether it is an exploratory, batch, or scheduled query.

Query logs can be accessed either through the Experience Platform UI in the [!UICONTROL Logs] tab of the [!UICONTROL Queries] workspace.

![The Queries log tab with the details panel highlighted.](../images/data-governance/overview/queries-log.png)

### Registri di controllo {#audit-logs}

Audit logs contain more detailed information than query logs and enable you to filter logs based on attributes such as user, date, type of query, and so on. Beyond the details available in query log UI, Audit Logs stores details on individual users along with their session data or connectivity to a third-party client.

By providing an exact record of user actions, an audit trail can help with troubleshooting issues and help your business effectively comply with corporate data stewardship policies and regulatory requirements. Audit logs provide a record of all Experience Platform activities. Using audit logs you can audit user actions relating to query execution, templates, and scheduled queries to increase the transparency and visibility of actions performed by users in Query Service.

The following table indicates the query categories captured by audit logs and the action types they record:

| Categoria | Tipo di azione |
|---|---|
| Query | Esegui |
| Modello di query | Create, Delete, Update |
| Query pianificata | Create, Delete, Update |

Below is a list of three extended server logs that hold more details than those found within the query logs. The extended logs are found within the audit logs query categories:

1. **Meta query logs**: When a query is executed, various associated backend sub-queries (such as parsing) are executed. These types of queries are known as &quot;metadata&quot; queries. Their relevant details can be found in audit logs.
1. **Session logs**: The system creates a session entry log for a user when they log into Query Service regardless of whether they execute a query.
1. **Third-party client connection logs**: A connectivity audit log is generated when a user successfully connects Query Service to a third-party client.

See the [audit logs overview](../../landing/governance-privacy-security/audit-logs/overview.md) for more information on how audit logs can help your organization approach data compliance.

## Utilizzo dati {#data-usage}

The Data Governance framework in Experience Platform provides a uniform way to responsibly use data across all Adobe solutions, services, and platforms. It coordinates the systemic approach to capture, communicate, and use metadata across the entirety of Adobe Experience Cloud. This in turn, helps data controllers label data according to the marketing actions needed, and the restrictions placed on that data from these intended marketing actions. See the overview on [data usage labels](../../data-governance/labels/overview.md) for more information on how Data Governance allows you to apply data usage labels to datasets and fields.

It is best practice to work towards data compliance at every stage of the data&#39;s journey. To this end, derived datasets that use ad hoc schemas should be appropriately labeled as part of the Data Governance framework. There are two types of derived datasets formed by Query Service: datasets that use a standard schema and datasets that use an ad hoc schema.

>[!NOTE]
>
>Datasets that are created using Query Service are referred to as &quot;derived datasets&quot;.

As ad hoc schemas are created by an individual user for a specific purpose, the XDM schema fields are namespaced for that particular dataset and not intended for use across different datasets. As a result, ad hoc schemas are not visible by default in the Experience Platform UI. Although there is no difference in the application of data usage labels between both standard and ad hoc schemas, ad hoc schemas created by Query Service for the purpose of labelling must first be made visible in the Experience Platform UI. See the guide on [discovering ad hoc schemas within the Experience Platform UI](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) for more details.

After you have accessed the schema, you can [apply labels to individual fields](../../xdm/tutorials/labels.md). Once a schema has been labeled, all datasets that derive from that schema inherit those labels. From here, you can set up data usage policies that can restrict data with certain labels from being activated to certain destinations. For more information, see the overview on [data usage policies](../../data-governance/policies/overview.md).

## Privacy {#privacy}

[Privacy Service](../../privacy-service/home.md) helps you manage customer requests to access and delete their data in accordance with legal privacy regulations. It does this by searching the data for pre-existing identifiers, and either accesses or deletes that data depending on the privacy job requested. Data must be properly labeled in order for the service to determine which fields to access or delete during privacy jobs. Data that is subject to privacy requests must contain customer identity information in order to tie the disparate pieces of data with the individual person to whom the privacy request applies to. Query Service can enrich the data it uses with a unique identifier for the purpose of satisfying privacy jobs.

Privacy requests can be sent to the data lake or the Profile data store. Records deleted from the data lake do not result in the deletion of profiles that were made from those records. Also, a privacy job to delete personal information from the data lake does not delete their profile so any information (that contains that profile ID) ingested after the completion of the privacy job updates that profile as normal. This reaffirms the need to properly identify data used in hoc schemas.

See the Privacy Service documentation for more information on [identity data for privacy requests](../../privacy-service/identity-data.md) and how to configure your data operations and leverage Adobe technologies to effectively retrieve the appropriate identity information for customer privacy requests.

Query Service features for data governance simplify and streamline the process of data categorization and adherence to data usage regulations. Once the data has been identified, Query Service enables you to allocate the primary identity on all output datasets. You **must** add identities into the dataset to facilitate data privacy requests and work towards data compliance.

Schema data fields can be set as an identity field through the Experience Platform UI and Query Service also allows you to [mark the primary identities by using the SQL command &#39;ALTER TABLE&#39;](../sql/syntax.md#alter-table). Setting an identity using the `ALTER TABLE` command is especially useful when datasets are created using SQL rather than directly from a schema through the Experience Platform UI. See the documentation for instructions on how to [define identity fields in the UI](../../xdm/ui/fields/identity.md) when using standard schemas.

## Igiene dei dati {#data-hygiene}

&quot;Data hygiene&quot; refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. These processes make sure that datasets are accurate and consistent across all systems. It is important to ensure adequate data hygiene along every step of the data&#39;s journey and even from the initial data storage location. In Experience Platform Query Service, this is either the data lake or the accelerated store.

You can assign an identity to a derived dataset to allow their data management following Experience Platform&#39;s centralized data hygiene services.

Conversely, when you create an aggregated dataset on the accelerated store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any newly derived dataset queries using the same dataset source.

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform.
