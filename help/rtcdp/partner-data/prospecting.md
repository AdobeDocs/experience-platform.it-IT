---
title: (Beta) Coinvolgi e acquisisci nuovi clienti attraverso la ricerca di casi d’uso
description: Scopri come coinvolgere e acquisire nuovi clienti attraverso casi di utilizzo di individuazione, grazie al supporto dei dati dei partner in Real-Time CDP.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 486e1390dfa0602bef15d196d4a1a5befdc9ff23
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 1%

---

# Coinvolgi e acquisisci nuovi clienti attraverso la ricerca di casi d’uso

>[!AVAILABILITY]
>
>* Questa funzionalità beta è disponibile per i clienti che dispongono di una licenza per Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Ulteriori informazioni su questi pacchetti sono disponibili in [descrizioni dei prodotti](https://helpx.adobe.com/legal/product-descriptions.html) e contatta il rappresentante del tuo Adobe per ulteriori informazioni.

Utilizza il supporto dati di terze parti in Real-Time CDP per espandere la tua base di profili con profili di potenziali clienti dei partner dati e interagire con loro per acquisire o raggiungere nuovi clienti.

![Panoramica visiva di alto livello sul caso di utilizzo di individuazione di potenziali clienti.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Se prendi in considerazione la possibilità di contattare e acquisire nuovi clienti utilizzando il supporto dei dati dei partner in Real-Time CDP, considera i seguenti prerequisiti nel processo di pianificazione:

* Qual è la frequenza con cui prevedi che i profili forniti dai partner vengano acquisiti in Real-Time CDP e aggiornati?
* Quali identità richiedono le destinazioni a valle?
* Assicurati che gli identificatori acquisiti siano utilizzabili a valle
* I dati del partner che stai acquisendo sono legati a un identificatore durevole ampiamente accettato, ad esempio Dati personali identificabili (PII), PII con hash o un identificatore del partner?
* Quali criteri di utilizzo dei dati è necessario conoscere dal punto di vista del partner e dal proprio team legale, di privacy o di conformità?

## Come ottenere il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

Prima di espandere Real-Time CDP per coinvolgere e acquisire nuovi clienti, assicurati di utilizzare Real-Time CDP per creare una solida base per i dati di prima parte. I flussi di lavoro per ottenere questo caso d’uso sono simili ai flussi di lavoro per interagire con i clienti noti.

![Panoramica visiva di alto livello sul caso di utilizzo di individuazione di potenziali clienti.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. As a **cliente**, concedi la licenza per i profili prospect da uno o più **partner dati** per agevolare l&#39;acquisizione dei clienti funnel.
2. As a **cliente**, puoi estendere i dati del profilo e il modello di governance per acquisire **partner** Elenco fornito di profili di potenziali clienti.
3. As a **cliente**, carichi i profili dei potenziali clienti in Real-Time CDP e definisci criteri di governance per assicurarne un utilizzo responsabile.
4. As a **cliente**, puoi creare tipi di pubblico mirati dall’elenco dei profili di potenziali clienti.
5. As a **cliente**, puoi attivare i tipi di pubblico potenziale nelle destinazioni che accettano le identità disponibili nell’elenco dei potenziali clienti.
6. Se necessario, utilizza **partner dati** per l’attivazione nell’ultimo miglio dei tipi di pubblico sulle destinazioni desiderate dei contenuti multimediali a pagamento.

## Come ottenere il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello precedente.

### Funzionalità ed elementi dell’interfaccia utente che utilizzerai {#ui-functionality-and-elements}

Man mano che completi i passaggi per implementare il caso d’uso, utilizzerai le seguenti funzionalità di Real-Time CDP ed elementi dell’interfaccia utente (elencati nell’ordine in cui verranno utilizzati). Verificare di disporre delle autorizzazioni di controllo dell&#39;accesso basate su attributi necessarie per tutte queste aree o richiedere all&#39;amministratore di sistema di concedere le autorizzazioni necessarie.

* [Identità](/help/identity-service/namespaces.md)
* [Schemi](/help/xdm/home.md)
* [Etichette di utilizzo dati](/help/data-governance/labels/overview.md)
* [Set di dati](/help/catalog/datasets/overview.md)
* [Origini](/help/sources/home.md)
* Profili (collegamento ai profili dei potenziali clienti)
* Tipi di pubblico (collegamento ai tipi di pubblico potenziali)
* [Destinazioni](/help/destinations/home.md)

### Ottenere la licenza dei dettagli del profilo di terze parti dal partner {#license-profiles-from-partner}

Questa fase è descritta nella sezione [prerequisiti](#prerequisites-and-planning) e Adobe presuppone che tu abbia stipulato i giusti accordi contrattuali con fornitori di dati affidabili per acquisire i profili di potenziali clienti forniti dal partner dati.

### Estendi i dati del profilo e il modello di governance per accogliere i profili prospect forniti dai partner {#extend-governance-model}

Per poter ricevere i profili di potenziali clienti dal partner dati, devi estendere il framework di gestione dati in Real-Time CDP per includere questo nuovo tipo di profilo.

I componenti di identità, gestione dati e governance che utilizzerai sono:

* Una nuova **[!UICONTROL ID partner]** tipo di identità per i profili forniti dal partner
* Una nuova **[!UICONTROL Profilo potenziale individuale XDM]** Classe XDM
* **(La documentazione sarà presto disponibile)** Gruppi di campi personalizzati per il supporto dei dati dei partner
* **(La documentazione sarà presto disponibile)** Etichette di terze parti che verranno aggiunte agli attributi provenienti dai partner

#### Creare uno spazio dei nomi di identità ID partner

Inizia creando un nuovo tipo di identità per i profili che riceverai dal partner. A questo scopo, nella sezione Identità devi creare un nuovo spazio dei nomi dell’identità del tipo **[!UICONTROL ID partner]**.

![Crea un nuovo spazio dei nomi ID partner.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Per ulteriori informazioni sugli spazi dei nomi ID partner, consulta [sezione tipi di identità](/help/identity-service/namespaces.md).
* Ulteriori informazioni [come definire i campi di identità](/help/xdm/ui/fields/identity.md) nell’interfaccia utente di Experience Platform.

#### Crea un nuovo schema con **[!UICONTROL Profilo potenziale individuale XDM]** classe

Avanti, in **[!UICONTROL Gestione dati]** > **[!UICONTROL Schemi]**, crea un nuovo schema e assegnalo a **[!UICONTROL Profilo potenziale individuale XDM]** classe.

![Cerca la classe Prospect individuale XDM nel generatore di schemi XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Scopri come [creare e modificare schemi nell’interfaccia utente](/help/xdm/ui/resources/schemas.md) e ottenere informazioni complete sulla classe XDM Individual Prospect Profile (collegamento in arrivo).

Il **[!UICONTROL Profilo potenziale individuale XDM]** La classe è preconfigurata con i campi mostrati di seguito. Per arricchire lo schema con gli attributi forniti dai partner per i profili di potenziali clienti, puoi creare un nuovo gruppo di campi con gli attributi previsti e aggiungerlo allo schema, oppure puoi utilizzare uno dei gruppi di campi preconfigurati forniti da Adobe.

![Campi preconfigurati per la classe Prospect singolo XDM.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Successivamente, devi selezionare l’identità partnerID creata in precedenza come identità primaria per lo schema. I record profilo devono contenere un identificatore primario. Questo passaggio è necessario per garantire che i dati del prospect possano essere caricati nell’archivio dei profili e resi disponibili per la segmentazione e l’attivazione.

>[!AVAILABILITY]
>
>Ai profili potenziali viene automaticamente limitato l’utilizzo degli spazi dei nomi ID solo per il tipo di ID partner. Questo avviene per progettazione e garantisce una separazione netta tra i profili di prime parti e quelli potenziali.

![Seleziona ID partner configurato in precedenza come identità primaria nello schema.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Lo schema non è ancora abilitato per il profilo. Attiva il pulsante del profilo per abilitare lo schema da includere nel servizio del profilo. Per ulteriori informazioni sull’abilitazione dello schema per l’utilizzo in Real-Time Customer Profile, consulta [tutorial su come creare uno schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Abilitare lo schema per il profilo.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Aggiungi l’etichetta di governance dei dati di terze parti a tutti i campi dello schema

Prendi in considerazione l’aggiunta di etichette di governance dei dati di terze parti a tutti i campi che compongono lo schema. Ciò è importante al fine di garantire un uso responsabile dei dati di terze parti e ridurre al minimo il rischio di perdita dei dati. Trova ulteriori informazioni sulle etichette di governance dei dati di terze parti (aggiungi collegamento alla documentazione in Giordania)

Per farlo, segui la procedura indicata di seguito:

1. Passa allo schema creato e seleziona il **[!UICONTROL Etichette]** scheda.
2. Seleziona tutti i campi in questo schema utilizzando il pulsante di selezione nella parte superiore, quindi fai clic sull’icona a forma di matita a destra per applicare le etichette di governance dei dati a questo schema.
3. Seleziona la **[!UICONTROL Ecosistema partner]** Etichetta dalle categorie a sinistra.
4. Scegli l’etichetta denominata **[!UICONTROL Terze parti]** e seleziona **[!UICONTROL Salva]**.
5. Tutti i campi nello schema ora riportano l’etichetta selezionata nel passaggio precedente.

>[!SUCCESS]
>
>Ora lo schema è pronto per l’uso e puoi procedere al passaggio successivo per acquisire i dati prospect dal tuo partner dati.

Anche in questo passaggio, pensa a come cambia il modello di governance dei dati quando espandi la tua strategia di gestione dati per includere i dati di terze parti forniti dal partner. Consulta le considerazioni riportate nei collegamenti alla documentazione riportati di seguito:

* (**Disponibile a breve**) Mantieni i dati di terze parti in un set di dati separato in modo che sia facile eliminarli e annullare le integrazioni.
* (**Disponibile a breve** a) Utilizzare [scadenza set di dati](/help/hygiene/ui/dataset-expiration.md) funzionalità del set di dati per i clienti che hanno acquistato il componente aggiuntivo di igiene dei dati.
* (**Disponibile a breve**) Presta attenzione quando crei set di dati derivati che estraggono dati di terze parti, perché una volta combinati, l’unica soluzione per rimuovere i dati di terze parti è quella di eliminare l’intero set di dati derivati.

### Carica l’elenco dei profili prospect e controlla la visualizzazione dei profili prospect

Dopo aver preparato il modello dati per la gestione dei profili di potenziali clienti, è ora di acquisire i dati.

#### Creare un set di dati e caricare dati prospect di esempio

Per caricare alcuni dati di esempio e popolare i profili di potenziali clienti, crea un set di dati e carica un file ricevuto dal partner dati. Completa i passaggi seguenti:

1. Accedi a **[!UICONTROL Gestione dati]** > **[!UICONTROL Set di dati]** e seleziona **[!UICONTROL Crea set di dati]**.
2. Seleziona Crea set di dati dallo schema
3. Seleziona lo schema creato in un passaggio precedente
4. Assegna un nome al set di dati e, facoltativamente, una descrizione.
5. Seleziona **[!UICONTROL Fine]**.

![Registrazione dei passaggi per creare un set di dati per i profili di potenziali clienti.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Tieni presente che, analogamente al passaggio per creare uno schema, è necessario abilitare il set di dati per l’inclusione in Real-Time Customer Profile. Per ulteriori informazioni sull’abilitazione del set di dati per l’utilizzo in Real-Time Customer Profile, consulta [tutorial su come creare uno schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Abilita il set di dati per il profilo.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Per caricare nel set di dati un file ricevuto dal partner, seleziona il set di dati, scorri verso il basso nella barra a destra e seleziona **[!UICONTROL Aggiungi dati]**. Puoi trascinare il file o selezionare **[!UICONTROL Scegli i file]** per passare al percorso del file e selezionarlo.

![Aggiungi file al set di dati.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Dopo aver caricato l’elenco dei profili dal partner dati in Real-Time CDP, passa alla [Inspect: sezione dei profili prospect caricati](#inspect-profiles) per verificare che i profili prospect siano compilati nell’interfaccia utente.

#### Acquisire dati prospect tramite i connettori di origine

Puoi impostare importazioni di file ricorrenti per acquisire i dati dal partner tramite un connettore di origine e inserire l’elenco dei profili potenziali in Real-Time CDP.

Di seguito sono elencati alcuni connettori di origine consigliati a questo scopo, ma tieni presente che qualsiasi metodo di acquisizione basato su file in Real-Time CDP funziona correttamente.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Dopo aver caricato l’elenco dei profili dal partner dati in Real-Time CDP, procedi alla sezione successiva per verificare che i profili prospect siano popolati nell’interfaccia utente.

#### Inspect i profili prospect caricati {#inspect-profiles}

Per visualizzare l’elenco dei profili prospect, passa a **[!UICONTROL Prospettive]** > **[!UICONTROL Profili]** nella barra a sinistra.

Potrebbero essere necessarie fino a due ore perché i profili di potenziali clienti che hai appena caricato in Real-Time CDP vengano visualizzati nel **[!UICONTROL Sfoglia]** visualizzazione della schermata Prospect Profile. Se nella pagina viene visualizzato il messaggio &quot;Non ci sono profili potenziali da esplorare in questo momento&quot;, riprova più tardi. Dopo un po’ di attesa, i profili potenziali dovrebbero iniziare a essere visualizzati nel **[!UICONTROL Sfoglia]** visualizzazione.

>[!TIP]
>
>Nota la presenza di **[!UICONTROL Spazio dei nomi identità]** colonna. Se lavori con più fornitori di dati, utilizza questa colonna per dedurre l’origine dei profili di potenziali clienti.

![Visualizzazione dei profili di potenziali clienti caricati in Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

È inoltre possibile selezionare qualsiasi profilo di prospect per ulteriori ispezioni, come illustrato di seguito.

![Visualizzazione di come ispezionare i profili di potenziali clienti.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

(**Disponibile a breve** a) Ulteriori informazioni sui profili di potenziali clienti.

### Creare un pubblico potenziale {#create-prospect-audiences}

Utilizza la funzionalità di segmentazione di Real-Time CDP per creare tipi di pubblico dai profili di potenziali clienti. Utilizza le regole di segmentazione desiderate per creare tipi di pubblico personalizzati.

Per iniziare e creare tipi di pubblico composti da profili di potenziali clienti, passa a **[!UICONTROL Prospettive]** > **[!UICONTROL Tipi di pubblico]**.

![Visualizzazione dei tipi di pubblico potenziali.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

L’esperienza di creazione del pubblico per i profili di potenziali clienti è diversa dall’esperienza di creazione dei tipi di pubblico per i clienti di prime parti conosciuti. Questa visualizzazione è limitata a:

* Attributi dalla classe prospect creata in precedenza.
* Solo valutazione profilo batch.
* Non supporta la creazione di tipi di pubblico in base a eventi di serie temporali.

(**Disponibile a breve** a) Ulteriori informazioni sui tipi di pubblico potenziali.

### Attivare i profili di potenziali clienti nelle destinazioni {#activate-to-destinations}

Utilizza i tipi di pubblico potenziali esportandoli nelle destinazioni. Attualmente, solo alcune destinazioni come [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) o [!BADGE Alfa]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp.md) la destinazione supporta l’attivazione dei profili prospect.

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

* [!BADGE Beta]{type=Informative}[Integrare i profili di prime parti con attributi di partner di dati attendibili](/help/rtcdp/partner-data/supplement-first-party-profiles.md) per migliorare la base di dati, ottenere nuove informazioni sulla base dei clienti e ottimizzare meglio il pubblico.
* (**Disponibile a breve**) [!BADGE Beta]{type=Informative}**Utilizzo del riconoscimento assistito dai partner** per personalizzare le esperienze nel sito durante la visita e per il retargeting fuori sito dopo la visita, senza che l’utente si autentichi o abbia antecedenti con il tuo marchio.