---
title: Governance dei dati in Query Service
description: Questa panoramica descrive i principali elementi di governance dei dati in Experience Platform Query Service.
exl-id: 37543d43-bd8c-4bf9-88e5-39de5efe3164
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '3129'
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

La sicurezza dei dati è il processo di protezione dei dati da accessi non autorizzati e di garanzia di accesso sicuro per tutto il loro ciclo di vita. L’accesso sicuro viene mantenuto in Experience Platform attraverso l’applicazione di ruoli e autorizzazioni da parte di funzionalità quali il controllo dell’accesso basato su ruoli e il controllo dell’accesso basato su attributi. Credenziali, SSL e crittografia dei dati vengono utilizzati anche per garantire la protezione dei dati in Platform.

La sicurezza relativa a Query Service è suddivisa nelle seguenti categorie:

* [Controllo dell&#39;accesso](#access-control): l&#39;accesso è controllato tramite ruoli e autorizzazioni che includono set di dati e autorizzazioni a livello di colonna.
* Protezione dei dati tramite [connettività](#connectivity): i dati vengono protetti tramite Platform e client esterni tramite una connessione limitata con credenziali in scadenza o credenziali senza scadenza.
* Protezione dei dati tramite [crittografia e chiavi gestite dal cliente](#encryption-and-customer-managed-keys): accesso controllato tramite crittografia quando i dati sono inattivi.

### Controllo degli accessi {#access-control}

Il controllo degli accessi in Adobe Experience Platform consente di utilizzare [Adobe Admin Console](https://adminconsole.adobe.com/) per gestire l&#39;accesso alle funzionalità di Query Service utilizzando le autorizzazioni basate sul ruolo. Allo stesso modo, puoi controllare l’accesso a attributi di dati specifici tramite la gestione delle etichette su schemi e campi di dati.

Questa sezione descrive le autorizzazioni di controllo di accesso necessarie che un utente deve disporre per utilizzare completamente le funzioni di Query Service. Per istruzioni dettagliate sull&#39;assegnazione dell&#39;accesso a un profilo di prodotto, consulta i documenti su [gestione delle autorizzazioni](../../access-control/ui/permissions.md) e [gestione degli utenti](../../access-control/ui/users.md).

#### Autorizzazioni rilevanti

I permessi di controllo d&#39;accesso pertinenti sono definiti nelle tabelle seguenti in base al loro livello di ambito.

**Autorizzazioni di esecuzione query**

Per eseguire query in Query Service, è necessario assegnare a un utente un ruolo con la seguente autorizzazione:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Gestisci query] | Questa autorizzazione consente agli utenti di eseguire esplorazione dei dati e query batch, in grado di leggere un set di dati esistente o scrivere dati su set di dati. Sono incluse sia `CREATE TABLE AS SELECT` (`CTAS`) che `INSERT INTO AS SELECT` (`ITAS`) query. |

**Autorizzazioni del set di dati**

Questa sezione funge da guida per l’accesso basato su risorse necessario per accedere ai set di dati durante l’esecuzione di query sui dati tramite Query Service.

Tramite l’interfaccia Autorizzazioni è possibile definire il controllo dell’accesso basato su risorse per un set di dati e uno schema con le seguenti autorizzazioni:

| Autorizzazione | Descrizione |
|---|---|
| [!UICONTROL Gestisci set di dati] | Questa autorizzazione fornisce accesso in sola lettura per gli schemi e consente di accedere a set di dati di lettura, creazione, modifica ed eliminazione da utilizzare con Query Service. |
| [!UICONTROL Visualizza set di dati] | Questa autorizzazione consente l’accesso in sola lettura per i set di dati e gli schemi da utilizzare con Query Service. |

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

Con la funzionalità di controllo degli accessi [basato su attributi](../../access-control/abac/overview.md) è possibile definire ambiti di utilizzo organizzativi o dati sui set di dati fact e di dimensione nell&#39;[archivio accelerato](../data-distiller/customizable-insights/send-accelerated-queries.md). Questo consente agli amministratori di gestire l’accesso a segmenti specifici e di gestire meglio l’accesso concesso a utenti o gruppi di utenti.

Per creare restrizioni di accesso basate sui campi per i set di dati accelerati, puoi utilizzare le query CTAS di Query Service per creare set di dati accelerati e strutturarli in base a schemi XDM o schemi ad hoc esistenti. Gli amministratori possono quindi [aggiungere e modificare le etichette di utilizzo dei dati per lo schema](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field) o [schema ad hoc](./ad-hoc-schema-labels.md#edit-governance-labels). Puoi applicare, creare e modificare le etichette negli schemi dall&#39;area di lavoro [!UICONTROL Etichette] nell&#39;interfaccia utente [!UICONTROL Schemi].

Le etichette di utilizzo dei dati possono anche essere [applicate o modificate direttamente nel set di dati](../../data-governance/labels/user-guide.md#add-labels) tramite l&#39;interfaccia utente dei set di dati oppure create dall&#39;area di lavoro [!UICONTROL Etichette] del controllo di accesso. Per ulteriori informazioni, consulta la guida su come [creare una nuova etichetta](../../access-control/abac/ui/labels.md).

L’accesso degli utenti alle singole colonne può quindi essere controllato dalle etichette di utilizzo dei dati associate e dai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

### Connettività {#connectivity}

Query Service è accessibile tramite l’interfaccia utente di Platform o creando una connessione con client esterni compatibili. L’accesso a tutti i fronti disponibili è controllato da un set di credenziali.

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

Per una maggiore sicurezza, Query Service fornisce supporto nativo per le connessioni SSL per crittografare le comunicazioni client/server. Platform supporta varie opzioni SSL per soddisfare le tue esigenze di sicurezza dei dati e bilanciare il sovraccarico di elaborazione della crittografia e dello scambio di chiavi.

Per ulteriori informazioni, tra cui come connettersi utilizzando il valore del parametro SSL `verify-full`, vedere la guida sulle [opzioni SSL disponibili per le connessioni client di terze parti a Query Service](../clients/ssl-modes.md).

### Crittografia e chiavi gestite dal cliente (CMK) {#encryption-and-customer-managed-keys}

La crittografia è l&#39;utilizzo di un processo algoritmico per trasformare i dati in testo codificato e illeggibile per garantire che le informazioni siano protette e inaccessibili senza una chiave di decrittografia.

La conformità dei dati di Query Service garantisce che i dati siano sempre crittografati. I dati in transito sono sempre conformi a HTTPS e i dati in transito sono crittografati in un archivio Azure Data Lake utilizzando chiavi a livello di sistema. Per ulteriori informazioni, vedere la documentazione su [come vengono crittografati i dati in Adobe Experience Platform](../../landing/governance-privacy-security/encryption.md). Per informazioni dettagliate sulla modalità di crittografia dei dati inattivi nell&#39;archiviazione di Azure Data Lake, vedere la [documentazione ufficiale di Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

I dati in transito sono sempre conformi HTTPS. Analogamente, quando i dati sono inattivi nel data lake, la crittografia viene eseguita con la chiave di gestione del cliente (CMK), già supportata da Data Lake Management. La versione attualmente supportata è TLS1.2. Consulta la [documentazione sulle chiavi gestite dal cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md) per scoprire come impostare le tue chiavi di crittografia per i dati archiviati in Adobe Experience Platform.


## Audit {#audit}

Query Service registra l’attività dell’utente e la categorizza in diversi tipi di registro. I registri forniscono informazioni su **chi** ha eseguito **cosa** e **quando**. Ogni azione registrata contiene metadati che indicano il tipo di azione, la data e l’ora, l’ID e-mail dell’utente che l’ha eseguita e altri attributi relativi al tipo di azione.

Un utente di Platform può richiedere una qualsiasi delle categorie di registro. Questa sezione fornisce dettagli sul tipo di informazioni acquisite per Query Service e su dove è possibile accedere a tali informazioni.

### Registri query {#query-logs}

L’interfaccia utente dei registri di query ti consente di monitorare e rivedere i dettagli di esecuzione di tutte le query eseguite tramite l’editor delle query o l’API del servizio di query. Ciò garantisce trasparenza alle attività di Query Service, consentendo di controllare i metadati per **tutte** le query eseguite in Query Service. Include tutti i tipi di query, sia quelle esplorative, batch o pianificate.

È possibile accedere ai registri delle query tramite l&#39;interfaccia utente di Platform nella scheda [!UICONTROL Registri] dell&#39;area di lavoro [!UICONTROL Query].

![Scheda Registro query con il pannello dei dettagli evidenziato.](../images/data-governance/overview/queries-log.png)

### Registri di audit {#audit-logs}

I registri di audit contengono informazioni più dettagliate rispetto ai registri di query e consentono di filtrare i registri in base ad attributi quali utente, data, tipo di query e così via. Oltre ai dettagli disponibili nell’interfaccia utente del registro delle query, i registri di controllo memorizzano i dettagli sui singoli utenti, insieme ai relativi dati di sessione o alla connettività a un client di terze parti.

Grazie alla registrazione esatta delle azioni degli utenti, un audit trail può essere utile per risolvere eventuali problemi e aiutare la tua azienda a rispettare in modo efficace le politiche aziendali di gestione dei dati e i requisiti normativi. I registri di audit forniscono un registro di tutte le attività di Platform. Utilizzando i registri di audit è possibile controllare le azioni degli utenti relative all’esecuzione delle query, ai modelli e alle query pianificate per aumentare la trasparenza e la visibilità delle azioni eseguite dagli utenti in Query Service.

La tabella seguente indica le categorie di query acquisite dai registri di audit e i tipi di azioni da essi registrati:

| Categoria | Tipo di azione |
|---|---|
| Query | Esegui |
| Modello di query | Crea, Elimina, Aggiorna |
| Query pianificata | Crea, Elimina, Aggiorna |

Di seguito è riportato un elenco di tre registri server estesi che contengono più dettagli di quelli trovati all’interno dei registri di query. I registri estesi si trovano all’interno delle categorie di query dei registri di audit:

1. **Registri di meta query**: quando viene eseguita una query, vengono eseguite varie sottoquery di back-end associate, ad esempio l&#39;analisi. Questi tipi di query sono noti come query &quot;metadati&quot;. I relativi dettagli sono disponibili nei registri di audit.
1. **Registri di sessione**: il sistema crea un registro di voci di sessione per un utente quando accede a Query Service, indipendentemente dal fatto che esegua una query.
1. **Registri di connessione client di terze parti**: viene generato un registro di controllo della connettività quando un utente connette correttamente Query Service a un client di terze parti.

Consulta la [panoramica dei registri di audit](../../landing/governance-privacy-security/audit-logs/overview.md) per ulteriori informazioni su come i registri di audit possono aiutare la tua organizzazione a gestire la conformità dei dati.

## Utilizzo dati {#data-usage}

Il framework per la governance dei dati in Platform fornisce un modo uniforme per utilizzare in modo responsabile i dati in tutte le soluzioni, i servizi e le piattaforme di Adobi. Coordina l&#39;approccio sistemico per l&#39;acquisizione, la comunicazione e l&#39;utilizzo dei metadati in tutto Adobe Experience Cloud. Questo a sua volta, aiuta i titolari del trattamento dei dati ad etichettare i dati in base alle azioni di marketing necessarie e alle restrizioni imposte a tali dati da tali azioni di marketing previste. Per ulteriori informazioni su come la governance dei dati consente di applicare etichette di utilizzo ai set di dati e ai campi, consulta la panoramica sulle [etichette di utilizzo dei dati](../../data-governance/labels/overview.md).

È buona prassi lavorare per garantire la conformità dei dati in ogni fase del percorso dei dati. A tal fine, i set di dati derivati che utilizzano schemi ad hoc dovrebbero essere etichettati in modo appropriato come parte del framework di governance dei dati. Esistono due tipi di set di dati derivati formati da Query Service: set di dati che utilizzano uno schema standard e set di dati che utilizzano uno schema ad hoc.

>[!NOTE]
>
>I set di dati creati con Query Service sono denominati &quot;set di dati derivati&quot;.

Poiché gli schemi ad hoc vengono creati da un singolo utente per uno scopo specifico, i campi dello schema XDM hanno un namespace per quel particolare set di dati e non sono destinati all’utilizzo in set di dati diversi. Di conseguenza, gli schemi ad hoc non sono visibili per impostazione predefinita nell’interfaccia utente di Experience Platform. Sebbene non vi siano differenze nell’applicazione delle etichette di utilizzo dei dati tra schemi standard e ad hoc, gli schemi ad hoc creati da Query Service a scopo di etichettatura devono prima essere resi visibili nell’interfaccia utente di Platform. Per ulteriori dettagli, consulta la guida su [individuazione di schemi ad hoc nell&#39;interfaccia utente di Platform](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas).

Dopo aver effettuato l&#39;accesso allo schema, è possibile [applicare etichette ai singoli campi](../../xdm/tutorials/labels.md). Una volta etichettato uno schema, tutti i set di dati derivati da tale schema ereditano tali etichette. Da qui puoi impostare criteri di utilizzo dei dati che possono limitare l’attivazione di dati con determinate etichette per determinate destinazioni. Per ulteriori informazioni, consulta la panoramica sui [criteri di utilizzo dei dati](../../data-governance/policies/overview.md).

## Privacy {#privacy}

[Privacy Service](../../privacy-service/home.md) consente di gestire le richieste dei clienti di accedere ai propri dati ed eliminarli in conformità alle normative legali sulla privacy. A tale scopo, cerca nei dati gli identificatori preesistenti e accede o elimina tali dati a seconda del processo di privacy richiesto. I dati devono essere correttamente etichettati affinché il servizio possa determinare quali campi accedere o eliminare durante i processi relativi alla privacy. I dati oggetto di richieste di accesso a dati personali devono contenere informazioni sull’identità del cliente, in modo da collegare le diverse parti di dati con la singola persona a cui si applica la richiesta di accesso a dati personali. Query Service può arricchire i dati utilizzati con un identificatore univoco allo scopo di soddisfare i processi relativi alla privacy.

Le richieste di accesso ai dati personali possono essere inviate al data lake o all’archivio dati del profilo. I record eliminati dal data lake non determinano l’eliminazione dei profili creati da tali record. Inoltre, un processo di privacy per eliminare le informazioni personali dal data lake non elimina il loro profilo, pertanto tutte le informazioni (che contengono tale ID profilo) acquisite dopo il completamento del processo di privacy lo aggiornano come di consueto. Ciò ribadisce la necessità di identificare correttamente i dati utilizzati negli schemi ad hoc.

Consulta la documentazione di Privacy Service per ulteriori informazioni su [dati di identità per le richieste di privacy](../../privacy-service/identity-data.md) e su come configurare le operazioni sui dati e sfruttare le tecnologie Adobe per recuperare in modo efficace le informazioni di identità appropriate per le richieste di privacy dei clienti.

Le funzioni di Query Service per la governance dei dati semplificano e semplificano il processo di categorizzazione dei dati e il rispetto delle normative sull’utilizzo dei dati. Una volta identificati i dati, Query Service consente di allocare l’identità primaria a tutti i set di dati di output. **devi** aggiungere identità al set di dati per facilitare le richieste di privacy dei dati e lavorare per la conformità dei dati.

I campi dati dello schema possono essere impostati come campo di identità tramite l&#39;interfaccia utente di Platform e Query Service consente inoltre di [contrassegnare le identità primarie utilizzando il comando SQL &#39;ALTER TABLE&#39;](../sql/syntax.md#alter-table). L&#39;impostazione di un&#39;identità tramite il comando `ALTER TABLE` è particolarmente utile quando i set di dati vengono creati utilizzando SQL anziché direttamente da uno schema tramite l&#39;interfaccia utente di Platform. Consulta la documentazione per istruzioni su come [definire i campi di identità nell&#39;interfaccia utente](../../xdm/ui/fields/identity.md) quando si utilizzano schemi standard.

## Igiene dei dati {#data-hygiene}

Per &quot;igiene dei dati&quot; si intende il processo di riparazione o rimozione di dati che potrebbero essere obsoleti, imprecisi, formattati in modo errato, duplicati o incompleti. Questi processi garantiscono l’accuratezza e la coerenza dei set di dati in tutti i sistemi. È importante garantire un’igiene dei dati adeguata in ogni fase del percorso dei dati e anche dal luogo di archiviazione iniziale. In Experience Platform Query Service, si tratta del data lake o dell’archivio accelerato.

Puoi assegnare un’identità a un set di dati derivato per consentirne la gestione seguendo i servizi centralizzati di igiene dei dati di Platform.

Al contrario, quando si crea un set di dati aggregato nell’archivio accelerato, i dati aggregati non possono essere utilizzati per derivare i dati originali. In seguito a questa aggregazione di dati, viene eliminata la necessità di inoltrare richieste di igiene dei dati.

Un’eccezione a questo scenario è il caso dell’eliminazione. Se in un set di dati è richiesta un’eliminazione di igiene dei dati e prima che l’eliminazione sia completata, viene eseguita un’altra query di set di dati derivati, il set di dati derivato acquisirà informazioni dal set di dati originale. In questo caso, è necessario tenere presente che se è stata inviata una richiesta di eliminazione di un set di dati, non è necessario eseguire query di set di dati derivati utilizzando la stessa origine del set di dati.

Per ulteriori informazioni sull&#39;igiene dei dati in Adobe Experience Platform, vedere [panoramica sull&#39;igiene dei dati](../../hygiene/home.md).
