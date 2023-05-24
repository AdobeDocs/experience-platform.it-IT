---
title: Governance dei dati in Query Service
description: Questa panoramica descrive i principali elementi di governance dei dati in Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 54a6f508818016df1a4ab2a217bc0765b91df9e9
workflow-type: tm+mt
source-wordcount: '2843'
ht-degree: 1%

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
<!-- 1. Data hygiene -->

Questo documento esamina ciascuna delle diverse aree di governance e illustra come facilitare la conformità dei dati quando si utilizza Query Service. Consulta la [panoramica su governance, privacy e sicurezza](../../landing/governance-privacy-security/overview.md) per informazioni più ampie su come Experience Platform consente di gestire i dati dei clienti e garantire la conformità.

## Sicurezza

La sicurezza dei dati è il processo di protezione dei dati da accessi non autorizzati e di garanzia di accesso sicuro per tutto il loro ciclo di vita. L’accesso sicuro viene mantenuto in Experience Platform attraverso l’applicazione di ruoli e autorizzazioni da parte di funzionalità quali il controllo dell’accesso basato su ruoli e il controllo dell’accesso basato su attributi. Credenziali, SSL e crittografia dei dati vengono utilizzati anche per garantire la protezione dei dati in Platform.

La sicurezza relativa a Query Service è suddivisa nelle seguenti categorie:

* [Controllo degli accessi](#access-control): l’accesso è controllato tramite ruoli e autorizzazioni, incluse le autorizzazioni a livello di set di dati e di colonna.
* Protezione dei dati tramite [connettività](#connectivity): i dati sono protetti tramite Platform e client esterni tramite una connessione limitata con credenziali in scadenza o con credenziali senza scadenza.
* Protezione dei dati tramite [crittografia e chiavi a livello di sistema](#encryption): la sicurezza dei dati è garantita dalla crittografia quando i dati sono inattivi.

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### Controllo degli accessi {#access-control}

Il controllo degli accessi in Adobe Experience Platform consente di utilizzare [Adobe Admin Console](https://adminconsole.adobe.com/) per gestire l’accesso alle funzioni di Query Service utilizzando le autorizzazioni basate sul ruolo. Allo stesso modo, puoi controllare l’accesso a attributi di dati specifici tramite la gestione delle etichette su schemi e campi di dati.

Questa sezione descrive le autorizzazioni di controllo di accesso necessarie che un utente deve disporre per utilizzare completamente le funzioni di Query Service. Consulta i documenti su [gestione delle autorizzazioni](../../access-control/ui/permissions.md) e [gestione degli utenti](../../access-control/ui/users.md) per istruzioni dettagliate sull’assegnazione dell’accesso a un profilo di prodotto.

#### Autorizzazioni rilevanti

I permessi di controllo d&#39;accesso pertinenti sono definiti nelle tabelle seguenti in base al loro livello di ambito.

**Autorizzazioni di esecuzione delle query**

Per eseguire query in Query Service, è necessario assegnare a un utente un ruolo con la seguente autorizzazione:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Gestire le query] | Questa autorizzazione consente agli utenti di eseguire esplorazione dei dati e query batch, in grado di leggere un set di dati esistente o scrivere dati su set di dati. Ciò include sia `CREATE TABLE AS SELECT` (`CTAS`) e `INSERT INTO AS SELECT` (`ITAS`). |

**Autorizzazioni del set di dati**

Questa sezione funge da guida per l’accesso basato su risorse necessario per accedere ai set di dati durante l’esecuzione di query sui dati tramite Query Service.

Tramite l’interfaccia Autorizzazioni è possibile definire il controllo dell’accesso basato su risorse per un set di dati e uno schema con le seguenti autorizzazioni:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Gestione set di dati] | Questa autorizzazione fornisce accesso in sola lettura per gli schemi e consente di accedere a set di dati di lettura, creazione, modifica ed eliminazione da utilizzare con Query Service. |
| [!UICONTROL Visualizzare i set di dati] | Questa autorizzazione consente l’accesso in sola lettura per i set di dati e gli schemi da utilizzare con Query Service. |

#### Controllo dell’accesso per colonne/campi

La funzione di controllo dell&#39;accesso basato su attributi consente agli utenti di Query Service di limitare l&#39;accesso ai dati utente critici. L’accesso può essere concesso o limitato in base alle autorizzazioni assegnate a un ruolo. L’accesso degli utenti alle singole colonne è controllato dalle relative etichette di utilizzo dei dati e dai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

L’assegnazione di tag a gruppi di campi e classi dello schema con le etichette di utilizzo dei dati applica restrizioni di utilizzo a tutti gli schemi con gli stessi gruppi di campi e le stesse classi. Consulta la panoramica su [controllo degli accessi basato su attributi](../../access-control/abac/overview.md) per informazioni complete su questa funzione.

Questa funzione ti consente di concedere diritti di accesso su colonne riservate ai gruppi di utenti di tua scelta. Il controllo degli accessi su una colonna può limitare sia le funzionalità di lettura che quelle di scrittura per un particolare tipo di utente.

Il controllo degli accessi per le colonne può essere applicato a livello di schema sia per gli schemi standard che per quelli ad hoc. Applica le etichette di utilizzo dei dati agli schemi XDM per limitare l’accesso a una o più colonne. L’etichettatura dei dati viene applicata in modo coerente, anche per i set di dati creati tramite Query Service utilizzando uno schema predefinito o uno schema ad hoc generato come parte dell’operazione CTAS.

Una volta applicato il livello di accesso appropriato utilizzando etichette e ruoli, quando un utente tenta di accedere ai dati non accessibili si verifica il seguente comportamento di sistema:

1. Se a un utente è stato negato l’accesso a una delle colonne all’interno di uno schema, all’utente viene negata anche l’autorizzazione di lettura o scrittura sulla colonna con restrizioni. Questo vale per i seguenti scenari comuni:

   * **Caso 1**: quando un utente tenta di eseguire una query che interessa solo una colonna con restrizioni, il sistema genera un errore che indica che la colonna non esiste.
   * **Caso 2**: quando un utente tenta di eseguire una query con più colonne, inclusa una colonna con restrizioni, il sistema restituisce l’output solo per tutte le colonne senza restrizioni.

1. Se un utente tenta di accedere a un campo calcolato, deve avere accesso a tutti i campi utilizzati nella composizione oppure il sistema nega l’accesso anche al campo calcolato.

#### Controlli di accesso per le viste

Query Service consente di utilizzare SQL ANSI standard per [`CREATE VIEW`](../sql/syntax.md#create-view) istruzioni. Per i flussi di lavoro con dati altamente sensibili, è necessario applicare i controlli appropriati durante la creazione delle viste.

Il `CREATE VIEW` parola chiave definisce una vista di una query, ma la vista non è materializzata fisicamente. La query viene invece eseguita ogni volta che in una query viene fatto riferimento alla visualizzazione. Quando un utente crea una vista da un set di dati, le regole di controllo dell’accesso basate su ruolo e attributo per il set di dati principale sono **non** applicato gerarchicamente. Di conseguenza, è necessario impostare in modo esplicito le autorizzazioni per ciascuna delle colonne al momento della creazione di una visualizzazione.

#### Creare restrizioni di accesso basate sul campo per i set di dati accelerati {#create-field-based-access-restrictions-on-accelerated-datasets}

Con il [funzionalità di controllo degli accessi basata su attributi](../../access-control/abac/overview.md) puoi definire ambiti di utilizzo organizzativi o dei dati per i set di dati fact e dimensionali nella sezione [archivio accelerato](../data-distiller/query-accelerated-store/send-accelerated-queries.md). Questo consente agli amministratori di gestire l’accesso a segmenti specifici e di gestire meglio l’accesso concesso a utenti o gruppi di utenti.

Per creare restrizioni di accesso basate sui campi per i set di dati accelerati, puoi utilizzare le query CTAS di Query Service per creare set di dati accelerati e strutturarli in base a schemi XDM o schemi ad hoc esistenti. Gli amministratori possono quindi [aggiungere e modificare le etichette di utilizzo dei dati per lo schema](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) o [schema ad hoc](./ad-hoc-schema-labels.md#edit-governance-labels). Puoi applicare, creare e modificare le etichette negli schemi dalla sezione [!UICONTROL Etichette] area di lavoro in [!UICONTROL Schemi] UI.

Le etichette di utilizzo dei dati possono anche essere [applicato o modificato direttamente sul set di dati](../../data-governance/labels/user-guide.md#add-labels) tramite l’interfaccia utente Set di dati o creati dal controllo di accesso [!UICONTROL Etichette] Workspace. Consulta la guida su come [crea una nuova etichetta](../../access-control/abac/ui/labels.md) per ulteriori informazioni.

L’accesso degli utenti alle singole colonne può quindi essere controllato dalle etichette di utilizzo dei dati associate e dai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

### Connettività {#connectivity}

Query Service è accessibile tramite l’interfaccia utente di Platform o creando una connessione con client esterni compatibili. L’accesso a tutti i fronti disponibili è controllato da un set di credenziali.

#### Connettività tramite client esterni

L’accesso a Query Service tramite un client di terze parti richiede le credenziali per l’autorizzazione. Queste credenziali sono obbligatorie per accedere a Query Service con qualsiasi client esterno compatibile. È possibile connettersi ai client esterni utilizzando [scadenza delle credenziali](#expiring-credentials) o [credenziali senza scadenza](#non-expiring-credentials).

#### Tempo di connessione limitato tramite credenziali in scadenza {#expiring-credentials}

[Credenziali in scadenza](../ui/credentials.md) consente agli utenti di creare una connessione temporanea con un client esterno. Questo set di credenziali è valido solo per 24 ore. La scadenza di questi tipi di credenziali può essere visualizzata insieme alla scheda delle credenziali nel dashboard Servizio query.

![È stata evidenziata la scheda delle credenziali nell’area di lavoro di Query Service con le credenziali in scadenza.](../images/data-governance/overview/expiring-credentials.png)

#### Credenziali senza scadenza {#non-expiring-credentials}

[Credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials) consente di creare una connessione permanente con un client esterno, semplificando la connessione a Query Service senza la necessità di una password manuale.

Per abilitare l’opzione di generazione delle credenziali senza scadenza, è necessario seguire le istruzioni [flusso di lavoro preliminare](../ui/credentials.md#prerequisites). Come parte di questo processo, l’amministratore dell’organizzazione deve configurare le autorizzazioni per il profilo di prodotto, consentendo all’amministratore di controllare quali account dispongono dell’accesso per utilizzare credenziali senza scadenza.

Agli account utente tecnici autorizzati con credenziali senza scadenza possono essere assegnati ruoli per garantire una governance dei dati appropriata definendo l’ambito del loro accesso in lettura e scrittura in base alle loro responsabilità e esigenze. Vedi la sezione precedente su [utilizzo delle autorizzazioni basate su ruoli tramite il controllo degli accessi](#access-control) per gestire l’accesso a Query Service.

Una volta completato il flusso di lavoro preliminare, gli utenti autorizzati possono ora [genera le credenziali di connessione richieste](../ui/credentials.md#generate-credentials).

#### Crittografia dei dati SSL

Per una maggiore sicurezza, Query Service fornisce supporto nativo per le connessioni SSL per crittografare le comunicazioni client/server. Platform supporta varie opzioni SSL per soddisfare le tue esigenze di sicurezza dei dati e bilanciare il sovraccarico di elaborazione della crittografia e dello scambio di chiavi.

Consulta la guida su [Opzioni SSL per le connessioni client di terze parti a Query Service](../clients/ssl-modes.md) per ulteriori informazioni, tra cui come connettersi utilizzando `verify-full` Valore del parametro SSL.

### Crittografia {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

La crittografia è l&#39;utilizzo di un processo algoritmico per trasformare i dati in testo codificato e illeggibile per garantire che le informazioni siano protette e inaccessibili senza una chiave di decrittografia.

La conformità dei dati di Query Service garantisce che i dati siano sempre crittografati. I dati in transito sono sempre conformi a HTTPS e i dati in transito sono crittografati in un archivio Azure Data Lake utilizzando chiavi a livello di sistema. Consulta la documentazione su [cifratura dei dati in Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md) per ulteriori informazioni. Per informazioni dettagliate sulla modalità di crittografia dei dati inattivi nell&#39;archiviazione di Azure Data Lake, vedere [documentazione ufficiale di Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## Audit {#audit}

Query Service registra l’attività dell’utente e la categorizza in diversi tipi di registro. Registra le informazioni di fornitura su **chi** eseguito **cosa** azione, e **quando**. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita ed eventuali attributi aggiuntivi relativi al tipo di azione.

Un utente di Platform può richiedere una qualsiasi delle categorie di registro. Questa sezione fornisce dettagli sul tipo di informazioni acquisite per Query Service e su dove è possibile accedere a tali informazioni.

### Registri query {#query-logs}

L’interfaccia utente dei registri di query ti consente di monitorare e rivedere i dettagli di esecuzione di tutte le query eseguite tramite l’editor delle query o l’API del servizio di query. Questo porta trasparenza alle attività di Query Service, consentendoti di controllare i metadati per **tutto** le query eseguite in Query Service. Include tutti i tipi di query, sia quelle esplorative, batch o pianificate.

I registri delle query sono accessibili tramite l’interfaccia utente di Platform nella [!UICONTROL Registri] scheda di [!UICONTROL Query] Workspace.

![La scheda Registro query con il pannello dei dettagli evidenziato.](../images/data-governance/overview/queries-log.png)

### Registri di controllo {#audit-logs}

I registri di audit contengono informazioni più dettagliate rispetto ai registri di query e consentono di filtrare i registri in base ad attributi quali utente, data, tipo di query e così via. Oltre ai dettagli disponibili nell’interfaccia utente del registro delle query, i registri di controllo memorizzano i dettagli sui singoli utenti, insieme ai relativi dati di sessione o alla connettività a un client di terze parti.

Grazie alla registrazione esatta delle azioni degli utenti, un audit trail può essere utile per risolvere eventuali problemi e aiutare la tua azienda a rispettare in modo efficace le politiche aziendali di gestione dei dati e i requisiti normativi. I registri di audit forniscono un registro di tutte le attività di Platform. Utilizzando i registri di audit è possibile controllare le azioni degli utenti relative all’esecuzione delle query, ai modelli e alle query pianificate per aumentare la trasparenza e la visibilità delle azioni eseguite dagli utenti in Query Service.

La tabella seguente indica le categorie di query acquisite dai registri di audit e i tipi di azioni da essi registrati:

| Categoria | Tipo di azione |
|---|---|
| Query | Esegui |
| Modello di query | Crea, Elimina, Aggiorna |
| Query pianificata | Crea, Elimina, Aggiorna |

Di seguito è riportato un elenco di tre registri server estesi che contengono più dettagli di quelli trovati all’interno dei registri di query. I registri estesi si trovano all’interno delle categorie di query dei registri di audit:

1. **Registri di meta query**: quando si esegue una query, vengono eseguite varie sottoquery di back-end associate (ad esempio, l’analisi). Questi tipi di query sono noti come query &quot;metadati&quot;. I relativi dettagli sono disponibili nei registri di audit.
1. **Registri di sessione**: il sistema crea un registro delle voci di sessione per un utente che accede a Query Service, indipendentemente dal fatto che esegua o meno una query.
1. **Registri di connessione client di terze parti**: quando un utente connette correttamente Query Service a un client di terze parti, viene generato un registro di controllo della connettività.

Consulta la [panoramica dei registri di audit](../../landing/governance-privacy-security/audit-logs/overview.md) per ulteriori informazioni su come i registri di audit possono aiutare la tua organizzazione ad affrontare il problema della conformità dei dati.

## Utilizzo dati {#data-usage}

Il framework per la governance dei dati in Platform fornisce un modo uniforme per utilizzare in modo responsabile i dati in tutte le soluzioni, i servizi e le piattaforme di Adobi. Coordina l&#39;approccio sistemico per l&#39;acquisizione, la comunicazione e l&#39;utilizzo dei metadati in tutto Adobe Experience Cloud. Questo a sua volta, aiuta i titolari del trattamento dei dati ad etichettare i dati in base alle azioni di marketing necessarie e alle restrizioni imposte a tali dati da tali azioni di marketing previste. Consulta la panoramica su [etichette di utilizzo dei dati](../../data-governance/labels/overview.md) per ulteriori informazioni su come la governance dei dati consente di applicare etichette di utilizzo ai set di dati e ai campi.

È buona prassi lavorare per garantire la conformità dei dati in ogni fase del percorso dei dati. A tal fine, i set di dati derivati che utilizzano schemi ad hoc dovrebbero essere etichettati in modo appropriato come parte del framework di governance dei dati. Esistono due tipi di set di dati derivati formati da Query Service: set di dati che utilizzano uno schema standard e set di dati che utilizzano uno schema ad hoc.

>[!NOTE]
>
>I set di dati creati con Query Service sono denominati &quot;set di dati derivati&quot;.

Poiché gli schemi ad hoc vengono creati da un singolo utente per uno scopo specifico, i campi dello schema XDM hanno un namespace per quel particolare set di dati e non sono destinati all’utilizzo in set di dati diversi. Di conseguenza, gli schemi ad hoc non sono visibili per impostazione predefinita nell’interfaccia utente di Experience Platform. Sebbene non vi siano differenze nell’applicazione delle etichette di utilizzo dei dati tra schemi standard e ad hoc, gli schemi ad hoc creati da Query Service a scopo di etichettatura devono prima essere resi visibili nell’interfaccia utente di Platform. Consulta la guida su [individuazione di schemi ad hoc nell’interfaccia utente di Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) per ulteriori dettagli.

Dopo aver effettuato l’accesso allo schema, puoi [applicare etichette ai singoli campi](../../xdm/tutorials/labels.md). Una volta etichettato uno schema, tutti i set di dati derivati da tale schema ereditano tali etichette. Da qui puoi impostare criteri di utilizzo dei dati che possono limitare l’attivazione di dati con determinate etichette per determinate destinazioni. Per ulteriori informazioni, consulta la panoramica su [criteri di utilizzo dati](../../data-governance/policies/overview.md).

## Privacy {#privacy}

[Privacy Service](../../privacy-service/home.md) consente di gestire le richieste dei clienti di accedere e cancellare i propri dati in conformità con le normative legali sulla privacy. A tale scopo, cerca nei dati gli identificatori preesistenti e accede o elimina tali dati a seconda del processo di privacy richiesto. I dati devono essere correttamente etichettati affinché il servizio possa determinare quali campi accedere o eliminare durante i processi relativi alla privacy. I dati oggetto di richieste di accesso a dati personali devono contenere informazioni sull’identità del cliente, in modo da collegare le diverse parti di dati con la singola persona a cui si applica la richiesta di accesso a dati personali. Query Service può arricchire i dati utilizzati con un identificatore univoco allo scopo di soddisfare i processi relativi alla privacy.

Le richieste di accesso ai dati personali possono essere inviate al data lake o all’archivio dati del profilo. I record eliminati dal data lake non determinano l’eliminazione dei profili creati da tali record. Inoltre, un processo di privacy per eliminare le informazioni personali dal data lake non elimina il loro profilo, pertanto tutte le informazioni (che contengono tale ID profilo) acquisite dopo il completamento del processo di privacy lo aggiornano come di consueto. Ciò ribadisce la necessità di identificare correttamente i dati utilizzati negli schemi ad hoc.

Consulta la documentazione di Privacy Service per ulteriori informazioni su [dati di identità per le richieste di privacy](../../privacy-service/identity-data.md) e come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste dei clienti sulla privacy.

Le funzioni di Query Service per la governance dei dati semplificano e semplificano il processo di categorizzazione dei dati e il rispetto delle normative sull’utilizzo dei dati. Una volta identificati i dati, Query Service consente di allocare l’identità primaria a tutti i set di dati di output. Tu **deve** aggiungi identità al set di dati per facilitare le richieste di privacy dei dati e lavorare per la conformità dei dati.

I campi dati dello schema possono essere impostati come campo di identità tramite l’interfaccia utente di Platform e Query Service consente anche di: [contrassegnare le identità primarie utilizzando il comando SQL &#39;ALTER TABLE&#39;](../sql/syntax.md#alter-table). Impostazione di un’identità tramite `ALTER TABLE` Questo comando è particolarmente utile quando i set di dati vengono creati utilizzando SQL anziché direttamente da uno schema tramite l’interfaccia utente di Platform. Consulta la documentazione per istruzioni su come [definire i campi di identità nell’interfaccia utente](../../xdm/ui/fields/identity.md) quando si utilizzano schemi standard.

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
