---
title: Governance dei dati nel servizio query
description: Questa panoramica descrive i principali elementi della governance dei dati in Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: c1ec6f949bd0ab9ec3b1ccc58baf74d8c71deca0
workflow-type: tm+mt
source-wordcount: '2667'
ht-degree: 0%

---

# Governance dei dati nel servizio query

Adobe Experience Platform unisce i dati provenienti da più sistemi aziendali e consente di pulire, modellare, manipolare e arricchire i dati tramite Query Service in base alle tue esigenze. Questo consente agli esperti di marketing di identificare, comprendere e coinvolgere i clienti in un modo migliore. Garantire un&#39;adeguata governance dei dati è un aspetto fondamentale della gestione delle informazioni personali, in quanto alcuni dati possono essere soggetti a restrizioni di utilizzo basate su politiche organizzative e normative legali. È fondamentale garantire che i dati acquisiti e le relative operazioni siano conformi ai criteri di utilizzo dei dati definiti.

La governance dei dati all’interno di Query Service consente di gestire i dati dei clienti e garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Questo svolge un ruolo chiave quando si assicurano che i criteri di utilizzo siano stati applicati in base ai regolamenti definiti dalla tua azienda.

Si consiglia alle organizzazioni che eseguono regolarmente il trattamento dei dati di delineare, mettere in pratica e applicare queste linee guida per creare un ambiente consapevole della privacy per tutti gli utenti.

Le seguenti categorie sono fondamentali per rispettare le normative sulla conformità dei dati quando si utilizza Query Service:

1. Sicurezza
1. Audit
1. Utilizzo dei dati
1. Privacy
<!-- 1. Data hygiene -->

Questo documento esamina ciascuno dei diversi ambiti di governance e illustra come semplificare la conformità dei dati quando si utilizza Query Service. Consulta la sezione [panoramica su governance, privacy e sicurezza](../../landing/governance-privacy-security/overview.md) per informazioni più ampie su come Experience Platform consente di gestire i dati dei clienti e garantire la conformità.

## Sicurezza

La sicurezza dei dati è il processo di protezione dei dati dall&#39;accesso non autorizzato e di garanzia dell&#39;accesso sicuro per tutto il suo ciclo di vita. L’accesso sicuro viene mantenuto in Experience Platform tramite l’applicazione di ruoli e autorizzazioni tramite funzionalità quali il controllo degli accessi basato su ruoli e il controllo degli accessi basato su attributi. Le credenziali, SSL e la crittografia dei dati vengono inoltre utilizzate per garantire la protezione dei dati in Platform.

La sicurezza relativa al servizio query è suddivisa nelle seguenti categorie:

* [Controllo dell&#39;accesso](#access-control): L&#39;accesso è controllato tramite ruoli e autorizzazioni, incluse le autorizzazioni a livello di set di dati e di colonna.
* Protezione dei dati tramite [connettività](#connectivity): I dati vengono protetti tramite Platform e client esterni ottenendo una connessione limitata con credenziali in scadenza o con credenziali in scadenza.
* Protezione dei dati tramite [crittografia e chiavi a livello di sistema](#encryption): La sicurezza dei dati è garantita dalla crittografia quando i dati sono a riposo.

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### Controllo degli accessi {#access-control}

Il controllo degli accessi in Adobe Experience Platform consente di utilizzare [Adobe Admin Console](https://adminconsole.adobe.com/) per gestire l’accesso alle funzionalità del servizio query utilizzando autorizzazioni basate su ruoli. Allo stesso modo, puoi controllare l’accesso a attributi di dati specifici tramite la gestione delle etichette su schemi e campi di dati.

Questa sezione delinea le autorizzazioni di controllo di accesso necessarie che un utente deve disporre per utilizzare completamente le funzionalità del servizio query. Vedi i documenti su [gestione delle autorizzazioni](../../access-control/ui/permissions.md) e [gestione utenti](../../access-control/ui/users.md) per istruzioni dettagliate sull’assegnazione dell’accesso a un profilo di prodotto.

#### Autorizzazioni rilevanti

Le autorizzazioni relative al controllo degli accessi sono definite nelle tabelle seguenti in base al loro livello di ambito.

**Autorizzazioni di esecuzione query**

Per eseguire query all’interno di Query Service, è necessario assegnare a un utente un ruolo con la seguente autorizzazione:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Gestire le query] | Questa autorizzazione consente agli utenti di eseguire l’esplorazione dei dati e le query batch, che possono leggere un set di dati esistente o scrivere dati sui set di dati. Ciò include entrambi `CREATE TABLE AS SELECT` (`CTAS`) e `INSERT INTO AS SELECT` (`ITAS`). |

**Autorizzazioni del set di dati**

Questa sezione funge da guida per l’accesso basato sulle risorse necessario per accedere ai set di dati durante l’esecuzione di query sui dati tramite Query Service.

Tramite l’interfaccia Autorizzazioni è possibile definire un controllo di accesso basato su risorse per un set di dati e uno schema con le seguenti autorizzazioni:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Gestire i set di dati] | Questa autorizzazione fornisce l’accesso in sola lettura per gli schemi e consente l’accesso alla lettura, alla creazione, alla modifica e all’eliminazione dei set di dati da utilizzare con Query Service. |
| [!UICONTROL Visualizzare i set di dati] | Questa autorizzazione consente l’accesso in sola lettura per i set di dati e gli schemi da utilizzare con Query Service. |

#### Controllo di accesso per colonne/campi

La funzione di controllo degli accessi basata sugli attributi consente agli utenti del servizio query di limitare l’accesso ai dati utente critici. L’accesso può essere concesso o limitato in base alle autorizzazioni assegnate a un ruolo. L’accesso dell’utente alle singole colonne è controllato dalle etichette di utilizzo dei dati pertinenti e dai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

L’assegnazione di tag ai gruppi e alle classi di campi dello schema con etichette di utilizzo dei dati applica restrizioni di utilizzo dei dati a tutti gli schemi con gli stessi gruppi e classi di campi. Vedi la panoramica su [controllo dell&#39;accesso basato sugli attributi](../../access-control/abac/overview.md) per informazioni complete su questa funzione.

Questa funzione ti consente di concedere i diritti di accesso su colonne riservate ai gruppi di utenti di tua scelta. Il controllo degli accessi su una colonna può limitare le funzionalità di lettura e scrittura per un particolare tipo di utente.

Il controllo degli accessi per le colonne può essere applicato a livello di schema sia per gli schemi standard che per quelli ad hoc. Applica le etichette di utilizzo dei dati agli schemi XDM per limitare l’accesso a una o più colonne. L’etichettatura dei dati viene applicata in modo coerente, anche per i set di dati creati tramite Query Service utilizzando uno schema predefinito o uno schema ad hoc generato come parte dell’operazione CTAS.

Una volta applicato il livello di accesso appropriato utilizzando etichette e ruoli, si verifica il seguente comportamento del sistema quando un utente tenta di accedere ai dati non accessibili:

1. Se a un utente è stato negato l&#39;accesso a una delle colonne di uno schema, all&#39;utente viene inoltre negata l&#39;autorizzazione a leggere o scrivere nella colonna con restrizioni. Ciò vale per i seguenti scenari comuni:

   * **Caso 1**: Quando un utente tenta di eseguire una query che interessa solo una colonna con restrizioni, il sistema genera un errore che la colonna non esiste.
   * **Caso 2**: Quando un utente tenta di eseguire una query con più colonne, inclusa una colonna con restrizioni, il sistema restituisce l&#39;output solo per tutte le colonne senza restrizioni.

1. Se un utente tenta di accedere a un campo calcolato, deve avere accesso a tutti i campi utilizzati nella composizione oppure il sistema nega l’accesso anche al campo calcolato.

#### Controlli di accesso per le visualizzazioni

Query Service consente di utilizzare SQL ANSI standard per [`CREATE VIEW`](../sql/syntax.md#create-view) dichiarazioni. Per i flussi di lavoro con dati altamente sensibili, è necessario applicare controlli appropriati durante la creazione di visualizzazioni.

La `CREATE VIEW` keyword definisce una visualizzazione di una query ma la visualizzazione non è materializzata fisicamente. Al contrario, la query viene eseguita ogni volta che viene fatto riferimento alla visualizzazione in una query. Quando un utente crea una visualizzazione da un set di dati, le regole di controllo dell’accesso basate su ruoli e attributi per il set di dati principale sono **not** applicato gerarchicamente. Di conseguenza, è necessario impostare in modo esplicito le autorizzazioni per ciascuna colonna quando viene creata una visualizzazione.

### Connettività {#connectivity}

Query Service è accessibile tramite l’interfaccia utente di Platform o tramite la creazione di una connessione con client compatibili esterni. L&#39;accesso a tutti i fronti disponibili è controllato da un insieme di credenziali.

#### Connettività attraverso client esterni

L’accesso a Query Service tramite un client di terze parti richiede le credenziali per l’autorizzazione. Queste credenziali sono obbligatorie per accedere a Query Service con uno qualsiasi dei client esterni compatibili. È possibile connettersi a client esterni utilizzando [credenziali in scadenza](#expiring-credentials) o [credenziali non in scadenza](#non-expiring-credentials).

#### Tempo di connessione limitato tramite credenziali in scadenza {#expiring-credentials}

[Credenziali in scadenza](../ui/credentials.md) consentire agli utenti di creare una connessione temporanea con un client esterno. Questo insieme di credenziali è valido solo per 24 ore. La scadenza di questi tipi di credenziali può essere visualizzata insieme alla scheda delle credenziali nel dashboard Servizio query.

![La scheda delle credenziali nell’area di lavoro Servizio query con le credenziali in scadenza evidenziate.](../images/data-governance/overview/expiring-credentials.png)

#### Credenziali non in scadenza {#non-expiring-credentials}

[Credenziali non in scadenza](../ui/credentials.md#non-expiring-credentials) consente di creare una connessione permanente con un client esterno, facilitando la connessione a Query Service senza la necessità di una password manuale.

Per abilitare l&#39;opzione di generazione di credenziali non in scadenza, è necessario seguire i [flusso di lavoro preliminare](../ui/credentials.md#prerequisites). In questa fase, l’amministratore dell’organizzazione deve configurare le autorizzazioni per il profilo di prodotto, assegnando all’amministratore il controllo sugli account a cui può accedere per utilizzare le credenziali non in scadenza.

Gli account utente tecnici autorizzati con credenziali non in scadenza possono essere assegnati ruoli per garantire un’adeguata governance dei dati definendo l’ambito del loro accesso in lettura e scrittura in base alle loro responsabilità e esigenze. Vedi la sezione precedente su [utilizzo di autorizzazioni basate su ruoli tramite il controllo degli accessi](#access-control) per gestire l’accesso al servizio query.

Una volta completato il flusso di lavoro dei prerequisiti, gli utenti autorizzati ora possono [genera le credenziali di connessione richieste](../ui/credentials.md#generate-credentials).

#### Crittografia dei dati SSL

Per una maggiore sicurezza, Query Service fornisce supporto nativo per le connessioni SSL per crittografare le comunicazioni client/server. Platform supporta varie opzioni SSL per soddisfare le tue esigenze di sicurezza dei dati e bilanciare il sovraccarico di elaborazione della crittografia e dello scambio di chiavi.

Consulta la guida disponibile [Opzioni SSL per connessioni client di terze parti a Query Service](../clients/ssl-modes.md) per ulteriori informazioni, inclusa la modalità di connessione tramite `verify-full` Valore del parametro SSL.

### Crittografia {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

La cifratura è l’uso di un processo algoritmico per trasformare i dati in testo codificato e illeggibile in modo da garantire che le informazioni siano protette e inaccessibili senza una chiave di decrittografia.

La conformità ai dati del servizio query assicura che i dati siano sempre crittografati. I dati in transito sono sempre conformi a HTTPS e i dati a riposo sono crittografati in un archivio Azure Data Lake utilizzando le chiavi a livello di sistema. Consulta la documentazione su [cifratura dei dati in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html) per ulteriori informazioni. Per informazioni dettagliate sul modo in cui i dati a riposo vengono crittografati in Azure Data Lake Storage, consulta la sezione [documentazione ufficiale di Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## Audit {#audit}

Query Service registra l’attività dell’utente e classifica tale attività in diversi tipi di log. Informazioni di fornitura dei registri su **chi** eseguito **cosa** e **quando**. Ogni azione registrata in un registro contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che ha eseguito l’azione e gli attributi aggiuntivi relativi al tipo di azione.

Qualsiasi categoria di registro può essere richiesta come desiderato da un utente di Platform. Questa sezione fornisce dettagli sul tipo di informazioni acquisite per Query Service e su dove è possibile accedere a tali informazioni.

### Registro delle query {#query-logs}

L’interfaccia utente dei registri di query consente di monitorare e rivedere i dettagli di esecuzione per tutte le query eseguite tramite l’editor delle query o l’API del servizio query. Questo porta trasparenza alle attività del servizio query, consentendoti di controllare i metadati per **tutto** le query eseguite in Query Service. Include tutti i tipi di query, sia che si tratti di una query esplorativa, batch o pianificata.

I registri di query sono accessibili tramite l’interfaccia utente di Platform nella [!UICONTROL Registri] della scheda [!UICONTROL Query] workspace.

![Scheda Registro query con il pannello dei dettagli evidenziato.](../images/data-governance/overview/queries-log.png)

### Registri di controllo {#audit-logs}

I registri di controllo contengono informazioni più dettagliate rispetto ai registri di query e consentono di filtrare i registri in base ad attributi quali utente, data, tipo di query e così via. Oltre ai dettagli disponibili nell’interfaccia utente del registro delle query, i registri di controllo memorizzano i dettagli sui singoli utenti insieme ai relativi dati di sessione o alla connettività a un client di terze parti.

Fornendo un registro esatto delle azioni degli utenti, un audit trail può aiutare a risolvere i problemi e aiutare la tua azienda a rispettare efficacemente le politiche di gestione dei dati aziendali e i requisiti normativi. I registri di controllo forniscono un record di tutte le attività di Platform. Utilizzando i registri di controllo è possibile controllare le azioni degli utenti relative all’esecuzione delle query, ai modelli e alle query pianificate per aumentare la trasparenza e la visibilità delle azioni eseguite dagli utenti in Query Service.

La tabella seguente indica le categorie di query acquisite dai log di controllo e i tipi di azione registrati:

| Categoria | Tipo di azione |
|---|---|
| Query | Esegui |
| Modello di query | Crea, Elimina, Aggiorna |
| Query pianificata | Crea, Elimina, Aggiorna |

Di seguito è riportato un elenco di tre log di server estesi che contengono più dettagli di quelli trovati all&#39;interno dei log di query. I registri estesi si trovano nelle categorie di query dei registri di controllo:

1. **Registri di query meta**: Quando viene eseguita una query, vengono eseguite varie sottoquery di backend associate (ad esempio l’analisi). Questi tipi di query sono noti come query &quot;metadati&quot;. I relativi dettagli pertinenti sono reperibili nei registri di audit.
1. **Registri di sessione**: Il sistema crea un registro delle voci di sessione per un utente quando accede a Query Service indipendentemente dal fatto che esegua una query.
1. **Log di connessione client di terze parti**: Un registro di controllo della connettività viene generato quando un utente collega correttamente Query Service a un client di terze parti.

Consulta la sezione [panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md) per ulteriori informazioni su come i registri di controllo possono aiutare la tua organizzazione ad affrontare la conformità dei dati.

## Utilizzo dei dati {#data-usage}

Il framework per la governance dei dati in Platform offre un modo uniforme di utilizzare i dati in modo responsabile tra tutte le soluzioni, i servizi e le piattaforme di Adobe. Coordina l&#39;approccio sistemico per l&#39;acquisizione, la comunicazione e l&#39;utilizzo dei metadati sull&#39;intero Adobe Experience Cloud. In questo modo, i titolari del trattamento possono a loro volta assegnare ai dati l’etichetta in base alle azioni di marketing necessarie e alle restrizioni imposte ai dati da tali azioni di marketing previste. Vedi la panoramica su [etichette di utilizzo dei dati](../../data-governance/labels/overview.md) per ulteriori informazioni su come la governance dei dati consente di applicare etichette di utilizzo dei dati a set di dati e campi.

È buona prassi lavorare per la conformità dei dati in ogni fase del percorso dei dati. A tal fine, i set di dati derivati che utilizzano schemi ad hoc devono essere etichettati in modo appropriato come parte del framework di governance dei dati. Esistono due tipi di set di dati derivati formati da Query Service: set di dati che utilizzano uno schema standard e set di dati che utilizzano uno schema ad hoc.

>[!NOTE]
>
>I set di dati creati tramite Query Service sono denominati &quot;set di dati derivati&quot;.

Poiché gli schemi ad hoc vengono creati da un singolo utente per uno scopo specifico, i campi dello schema XDM vengono separati con un namespace per quel particolare set di dati e non sono destinati all’uso in diversi set di dati. Di conseguenza, gli schemi ad hoc non sono visibili per impostazione predefinita nell’interfaccia utente di Experience Platform. Sebbene non vi sia alcuna differenza nell’applicazione delle etichette di utilizzo dei dati tra schemi standard e ad hoc, gli schemi ad hoc creati da Query Service allo scopo di etichettare devono prima essere resi visibili nell’interfaccia utente di Platform. Consulta la guida su [scoperta di schemi ad hoc nell’interfaccia utente di Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) per ulteriori dettagli.

Dopo aver effettuato l&#39;accesso allo schema, puoi [applicare etichette ai singoli campi](../../xdm/tutorials/labels.md). Una volta che uno schema è stato etichettato, tutti i set di dati che derivano da tale schema ereditano tali etichette. Da qui, puoi impostare criteri di utilizzo dei dati che possono impedire l’attivazione di dati con determinate etichette su determinate destinazioni. Per ulteriori informazioni, consulta la panoramica su [criteri di utilizzo dei dati](../../data-governance/policies/overview.md).

## Privacy {#privacy}

[Privacy Service](../../privacy-service/home.md) consente di gestire le richieste dei clienti per accedere e cancellare i loro dati in conformità alle normative sulla privacy legali. A tal fine, cerca i dati per gli identificatori preesistenti e accede o elimina tali dati a seconda del processo di privacy richiesto. I dati devono essere etichettati correttamente affinché il servizio determini quali campi accedere o eliminare durante i processi di privacy. I dati soggetti a richieste di privacy devono contenere informazioni di identità del cliente al fine di collegare le varie parti di dati con la persona a cui si applica la richiesta di privacy. Query Service può arricchire i dati utilizzati con un identificatore univoco allo scopo di soddisfare i processi di privacy.

Le richieste di privacy possono essere inviate al data lake o all’archivio dati del profilo. I record eliminati dal data lake non comportano l&#39;eliminazione dei profili creati da tali record. Inoltre, un lavoro sulla privacy per eliminare le informazioni personali dal data lake non elimina il loro profilo in modo che eventuali informazioni (che contengono tale ID profilo) acquisite dopo il completamento del processo sulla privacy aggiornino tale profilo come normale. Ciò conferma la necessità di identificare correttamente i dati utilizzati negli schemi ad hoc.

Per ulteriori informazioni, consulta la documentazione di Privacy Service . [dati di identità per le richieste di privacy](../../privacy-service/identity-data.md) e come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste sulla privacy dei clienti.

Le funzioni Query Service per la governance dei dati semplificano e semplificano il processo di categorizzazione dei dati e il rispetto delle normative sull’utilizzo dei dati. Una volta identificati i dati, Query Service consente di allocare l’identità principale su tutti i set di dati di output. You **deve** aggiungi le identità nel set di dati per facilitare le richieste sulla privacy dei dati e lavorare per la conformità dei dati.

I campi dati schema possono essere impostati come campo di identità tramite l’interfaccia utente di Platform e Query Service consente inoltre di: [contrassegnare le identità principali utilizzando il comando SQL &quot;ALTER TABLE&quot;](../sql/syntax.md#alter-table). Impostazione di un&#39;identità tramite `ALTER TABLE` Questo comando è particolarmente utile quando i set di dati vengono creati utilizzando SQL anziché direttamente da uno schema tramite l’interfaccia utente di Platform. Consulta la documentazione per le istruzioni su come [definire i campi di identità nell’interfaccia utente](../../xdm/ui/fields/identity.md) quando si utilizzano schemi standard.

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
