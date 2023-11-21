---
title: Coinvolgi e acquisisci nuovi clienti senza dipendere dai cookie di terze parti
description: Scopri come coinvolgere e acquisire nuovi clienti attraverso possibili casi d’uso, senza affidarti a cookie di terze parti.
feature: Use Cases, Customer Acquisition
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: 3353866aa2d52c784663f355183e940e727b2af7
workflow-type: tm+mt
source-wordcount: '2077'
ht-degree: 86%

---

# Coinvolgi e acquisisci nuovi clienti senza dipendere dai cookie di terze parti

>[!AVAILABILITY]
>
>* Questa funzionalità è disponibile per i clienti che dispongono di una licenza per Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Ulteriori informazioni su questi pacchetti sono disponibili nelle [descrizioni dei prodotti](https://helpx.adobe.com/it/legal/product-descriptions.html). Contatta il tuo rappresentante Adobe per ulteriori informazioni.

Utilizza il supporto dati di terze parti in Real-Time CDP per espandere la tua base di profili con profili di potenziali clienti dai partner dati e interagisci con loro per acquisire o raggiungere nuovi clienti.

![Panoramica visiva di alto livello su un caso d’uso di potenziale cliente.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Perché considerare questo caso d’uso {#why-this-use-case}

I brand si trovano ad affrontare contemporaneamente sfide impegnative relative all’esecuzione responsabile di casi d’uso di acquisizione clienti top-of-the-funnel senza dipendere dai cookie di terze parti, da budget limitati e da una maggiore domanda di trasparenza e ritorno sulla spesa pubblicitaria.

Adobe Real-time Customer Data Platform può aiutare i brand a passare in modo sicuro i casi di utilizzo supportati dalla piattaforma di gestione dati (DMP, Data Management Platform) a alternative senza cookie, in modo da portare avanti la sofisticazione e la potenza complete della segmentazione self-service, della cura del pubblico e dell’attivazione in un unico sistema. Il tutto senza compromettere l&#39;attenzione costante di Adobe sull&#39;uso responsabile dei dati tramite un framework brevettato per la governance dei dati e il consenso.

Ad esempio, segui i passaggi descritti in questo caso d’uso quando devi eseguire una campagna per attrarre potenziali utenti affinché diventino clienti noti.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Se stai valutando la possibilità di contattare e acquisire nuovi clienti, tieni presente i seguenti prerequisiti nel processo di pianificazione:

* Qual è la cadenza con cui si prevede che gli attributi forniti dai partner vengano acquisiti in Real-Time CDP e aggiornati?
* Quali identità richiedono le destinazioni a valle?
* Assicurati che gli identificatori acquisiti siano utilizzabili a valle
* I dati del partner che stai acquisendo sono legati a un identificatore durevole ampiamente accettato, ad esempio le Informazioni di identificazione personale (PII), PII con hash o un identificatore del partner?
* Quali criteri di utilizzo dei dati è necessario conoscere dal punto di vista del partner e da parte del team legale, di privacy o di conformità?

## Come utilizzare il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

Prima di espandere Real-Time CDP per coinvolgere e acquisire nuovi clienti, assicurati di utilizzare Real-Time CDP per creare una solida base per i dati di prime parti. I flussi di lavoro per ottenere questo caso d’uso sono simili ai flussi di lavoro per interagire con clienti noti.

![Panoramica visiva di alto livello sul caso d’uso potenziale dei clienti.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Come **cliente**, concedi la licenza per i profili di potenziali clienti da uno o più **partner dati** per agevolare l’acquisizione dei clienti funnel.
2. Come **cliente**, puoi estendere i dati del profilo e il modello di governance per acquisire l’elenco di profili di potenziali clienti fornito dai **partner**.
3. Come **cliente**, carichi i profili di potenziali clienti in Real-Time CDP e definisci criteri di governance per assicurarne un utilizzo responsabile.
4. Come **cliente**, puoi creare tipi di pubblico mirati dall’elenco dei profili di potenziali clienti.
5. Come **cliente**, puoi attivare i tipi di pubblico potenziale nelle destinazioni che accettano le identità disponibili nell’elenco dei potenziali clienti.
6. Se necessario, utilizza il **partner dati** per l’attivazione nell’ultimo miglio dei tipi di pubblico sulle destinazioni desiderate dei contenuti multimediali a pagamento.

## Procedura dettagliata del video {#video-walkthrough}

Il tutorial video seguente illustra come raggiungere e coinvolgere i potenziali tipi di pubblico:

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## Come utilizzare il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a un ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello qui sopra.

### Funzionalità ed elementi dell’interfaccia utente che utilizzerai {#ui-functionality-and-elements}

Man mano che completi i passaggi per implementare il caso d’uso, utilizzerai le funzionalità di Real-Time CDP ed elementi dell’interfaccia utente seguenti (elencati nell’ordine in cui verranno utilizzati). Assicurati di disporre delle autorizzazioni di controllo degli accessi basate su attributi necessarie per tutte queste aree o richiedi all’amministratore di sistema di concedere le autorizzazioni necessarie.

* [Identità](/help/identity-service/namespaces.md)
* [Schemi](/help/xdm/home.md)
* [Etichette di utilizzo dei dati](/help/data-governance/labels/overview.md)
* [Set di dati](/help/catalog/datasets/overview.md)
* [Origini](/help/sources/home.md)
* [Profili potenziali](/help/profile/ui/prospect-profile.md)
* [Pubblico potenziale](/help/segmentation/ui/prospect-audience.md)
* [Destinazioni](/help/destinations/home.md)

### Ottenere la licenza dei dettagli del profilo di terze parti dal partner {#license-profiles-from-partner}

Questa fase è descritta nella sezione [prerequisiti](#prerequisites-and-planning) e Adobe presuppone che tu abbia stipulato i giusti accordi contrattuali con fornitori di dati affidabili per acquisire profili di potenziali clienti forniti dal partner di dati.

### Estendi i dati del profilo e il modello di governance per adattarli agli attributi forniti dai profili di potenziali clienti {#extend-governance-model}

Per poter ricevere i profili di potenziali clienti dal partner dati, è necessario estendere il framework di gestione dati in Real-Time CDP per includere questo nuovo tipo di profilo.

I componenti di identità, gestione dati e governance che utilizzerai sono:

* Un nuovo tipo di identità **[!UICONTROL ID partner]** per i profili forniti dal partner
* Una nuova classe XDM del **[!UICONTROL Profilo individuale potenziale cliente XDM]**
* **(La documentazione sarà presto disponibile)** Gruppi di campi personalizzati per il supporto dei dati dei partner
* **(La documentazione sarà presto disponibile)** Etichette di terze parti che verranno aggiunte agli attributi provenienti dai partner

#### Creare uno spazio dei nomi identità dell’ID partner {#create-partner-id-namespace}

Inizia creando un nuovo tipo di identità per i profili che riceverai dal partner. A questo scopo, nella sezione Identità devi creare un nuovo spazio dei nomi identità del tipo **[!UICONTROL ID partner]**.

![Crea un nuovo spazio dei nomi identità di ID partner.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Per ulteriori informazioni sullo spazio dei nomi ID partner, consulta la [sezione sui tipi di identità](/help/identity-service/namespaces.md).
* Ulteriori informazioni su [come definire i campi di identità](/help/xdm/ui/fields/identity.md) nell’interfaccia utente di Experience Platform.

#### Crea un nuovo schema con la classe del **[!UICONTROL Profilo individuale potenziale cliente XDM]**

Poi, in **[!UICONTROL Gestione dati]** > **[!UICONTROL Schemi]**, crea un nuovo schema e assegnalo alla classe del **[!UICONTROL Profilo individuale potenziale cliente XDM]**.

![Cerca la classe del Profilo individuale potenziale cliente XDM nel generatore di schemi XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Ulteriori informazioni su come [creare e modificare schemi nell’interfaccia utente](/help/xdm/ui/resources/schemas.md) e ottenere informazioni complete sulla classe del Profilo individuale potenziale cliente XDM (collegamento in arrivo).

La classe del **[!UICONTROL Profilo individuale potenziale cliente XDM]** è preconfigurata con i campi mostrati di seguito. Per arricchire lo schema con gli attributi forniti dai partner per i profili di potenziali clienti, puoi creare un nuovo gruppo di campi con gli attributi previsti e aggiungerlo allo schema, oppure puoi utilizzare uno dei gruppi di campi preconfigurati forniti da Adobe.

![Campi preconfigurati per la classe Profilo individuale potenziale cliente XDM.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Successivamente, devi selezionare l’identità partnerID creata in precedenza come identità primaria per lo schema. I record del profilo devono contenere un identificatore primario. Questo passaggio è necessario per garantire che i dati del potenziale cliente possano essere caricati nell’archivio dei profili e resi disponibili per la segmentazione e l’attivazione.

>[!AVAILABILITY]
>
>I profili dei potenziali clienti vengono limitati automaticamente all’utilizzo degli spazi dei nomi ID del tipo di ID partner. Si tratta di una caratteristica di progettazione e garantisce una separazione netta tra i profili di prime parti e quelli di potenziali clienti.

![Seleziona l’ID partner configurato in precedenza come identità primaria nello schema.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Tieni presente che lo schema non è ancora abilitato per il profilo. Attiva/disattiva il pulsante del profilo per abilitare l’inclusione di questo schema nel servizio del profilo. Per ulteriori informazioni sull’abilitazione dello schema per l’utilizzo nel Profilo cliente in tempo reale, consulta il [tutorial su come creare uno schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Abilitare lo schema per il profilo.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Aggiungere l’etichetta di governance dei dati di terze parti a tutti i campi dello schema

Prendi in considerazione l’aggiunta di etichette di governance dei dati di terze parti a tutti i campi che compongono lo schema. Ciò è importante al fine di garantire un uso responsabile dei dati di terze parti e ridurre al minimo il rischio di perdite di dati. Ulteriori informazioni su [etichette di governance dei dati di terze parti](../../data-governance/labels/reference.md#partner-ecosystem-labels).

Per farlo, segui la procedura indicata di seguito:

1. Passa allo schema creato e seleziona la scheda **[!UICONTROL Etichette]**.
2. Seleziona tutti i campi in questo schema utilizzando il pulsante di selezione nella parte superiore, quindi fai clic sull’icona a forma di matita sulla destra per applicare le etichette di governance dei dati a questo schema.
3. Seleziona l’etichetta **[!UICONTROL Ecosistema partner]** dalle categorie sulla sinistra.
4. Scegli l’etichetta denominata **[!UICONTROL Terze parti]** e seleziona **[!UICONTROL Salva]**.
5. Tieni presente che tutti i campi nello schema ora presentano l’etichetta selezionata nel passaggio precedente.

>[!SUCCESS]
>
>Ora lo schema è pronto per l’uso e puoi procedere al passaggio successivo per acquisire i dati dei potenziali clienti dal tuo partner di dati.

Anche in questo passaggio, tieni presente come cambia il modello di governance dei dati quando espandi la tua strategia di gestione dati per includere i dati di terze parti forniti dal partner. Consulta le considerazioni riportate nei collegamenti alla documentazione qui di seguito:

* (**Disponibile a breve**) Conservazione dei dati di terze parti in un set di dati separato in modo che sia facile eliminarli e annullare le integrazioni.
* (**Disponibile a breve**) Utilizzo della funzionalità [scadenza set di dati](/help/hygiene/ui/dataset-expiration.md) per il set di dati di clienti che hanno acquistato il componente aggiuntivo di igiene dei dati.
* (**Disponibile a breve**) Presta attenzione durante la creazione di set di dati derivati che estraggono dati di terze parti, perché una volta combinati, l’unica soluzione per rimuovere i dati di terze parti è quella di eliminare l’intero set di dati derivati.

### Carica l’elenco dei profili di potenziali clienti e controlla la vista dei profili di potenziali clienti

Dopo aver preparato il modello dati per la gestione dei profili di potenziali clienti, è il momento di acquisire i dati.

#### Creare un set di dati e caricare dati di potenziali clienti di esempio

Per caricare alcuni dati di esempio e popolare i profili di potenziali clienti, crea un set di dati e carica un file ricevuto dal partner di dati. Segui i passaggi seguenti:

1. Accedi a **[!UICONTROL Gestione dati]** > **[!UICONTROL Set di dati]** e seleziona **[!UICONTROL Crea set di dati]**.
2. Seleziona Crea set di dati da schema
3. Seleziona lo schema creato in un passaggio precedente
4. Assegna un nome al set di dati e, facoltativamente, una descrizione.
5. Seleziona **[!UICONTROL Fine]**.

![Una registrazione dei passaggi per creare un set di dati per i profili di potenziali clienti.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Tieni presente che, analogamente al passaggio per la creazione di uno schema, è necessario abilitare il set di dati da includere nel Profilo cliente in tempo reale. Per ulteriori informazioni sull’abilitazione del set di dati per l’utilizzo nel Profilo cliente in tempo reale, consulta il [tutorial sulla creazione di uno schema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Abilitare seti di dati per profilo.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Per caricare nel set di dati un file ricevuto dal partner, seleziona il set di dati, scorri verso il basso nella barra a destra e seleziona **[!UICONTROL Aggiungi dati]**. Puoi trascinare il file o selezionare **[!UICONTROL Scegli file]** per passare alla posizione del file e selezionarla.

![Aggiungere file al set di dati.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Dopo aver caricato l’elenco di profili dal partner di dati in Real-Time CDP, passa a [Controllare la sezione sui profili di potenziali clienti caricati](#inspect-profiles), per verificare che i profili del potenziale cliente siano compilati nell’interfaccia utente.

#### Acquisire dati del potenziale cliente tramite connettori di origine

Puoi impostare importazioni di file ricorrenti per acquisire i dati dal partner tramite un connettore di origine e inserire l’elenco dei profili di potenziali clienti in Real-Time CDP.

Di seguito sono elencati alcuni connettori di origine consigliati a questo scopo, ma tieni presente che qualsiasi metodo di acquisizione basato su file in Real-Time CDP funziona correttamente.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Dopo aver caricato l’elenco dei profili dal partner di dati in Real-Time CDP, passa alla sezione successiva per verificare che i profili di potenziali clienti siano compilati nell’interfaccia utente.

#### Controllare i profili di potenziali clienti caricati {#inspect-profiles}

Per visualizzare l’elenco dei profili di potenziali clienti, passa a **[!UICONTROL Potenziali clienti]** > **[!UICONTROL Profili]** nella barra a sinistra.

Perché i profili di potenziali clienti appena caricati in Real-Time CDP vengano visualizzati nella vista **[!UICONTROL Sfoglia]** della schermata Profilo potenziale cliente, potrebbero volerci fino a due ore. Se nella pagina viene visualizzato il messaggio “Non ci sono profili di potenziali clienti da sfogliare in questo momento”, riprova più tardi. Dopo una breve attesa, nella vista **[!UICONTROL Sfoglia]** dovresti iniziare a vedere i profili di potenziali clienti.

>[!TIP]
>
>Tieni presente la colonna **[!UICONTROL Spazio dei nomi identità]**. Se lavori con più fornitori di dati, utilizza questa colonna per dedurre l’origine dei profili di potenziali clienti.

![Vista dei profili di potenziali clienti caricati in Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

È possibile inoltre selezionare qualsiasi profilo di potenziale cliente per effettuare ulteriori controlli, come illustrato di seguito.

![Vista di come controllare i profili di potenziali clienti.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

Ulteriori informazioni su [profili potenziali](/help/profile/ui/prospect-profile.md).

### Creare tipi di pubblico potenziale {#create-prospect-audiences}

Utilizza la funzionalità segmentazione di Real-Time CDP per creare tipi di pubblico dai profili di potenziali clienti. Utilizza le regole di segmentazione desiderate per creare tipi di pubblico personalizzati.

Per iniziare e creare tipi di pubblico composti da profili di potenziali clienti, passa a **[!UICONTROL Potenziali clienti]** > **[!UICONTROL Tipi di pubblico]**.

![Vista di tipi di pubblico potenziali.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

L’esperienza di creazione del pubblico per profili di potenziali clienti è diversa dall’esperienza di creazione dei tipi di pubblico per clienti di prime parti noti. Questa vista è limitata a:

* attributi dalla classe di potenziale cliente creata in precedenza.
* Solo valutazione del profilo in batch.
* Non supporta la creazione di tipi di pubblico in base a eventi di serie temporali.

Ulteriori informazioni su [audience potenziali](/help/segmentation/ui/prospect-audience.md).

### Attivare profili di potenziali clienti nelle destinazioni {#activate-to-destinations}

Utilizza i tipi di pubblico di potenziali clienti esportandoli nelle destinazioni. Attualmente, solo alcune destinazioni di archiviazione cloud supportano l’attivazione di profili potenziali.

![Destinazioni che supportano i potenziali tipi di pubblico.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[Ulteriori informazioni](/help/destinations/ui/activate-prospect-audiences.md) informazioni sull’attivazione di potenziali clienti in destinazioni di archiviazione cloud.

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

* [Puoi integrare i profili di prime parti con attributi di partner di dati affidabili, per migliorare la base di dati, acquisire nuove informazioni sulla base dei clienti e una migliore ottimizzazione del pubblico.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* [Personalizzare le esperienze nel sito per visitatori sconosciuti utilizzando il riconoscimento dei visitatori supportato dai partner](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita senza che l’utente si autentichi o abbia una storia precedente con il tuo marchio.
* [Attivazione estesa di profili di potenziali clienti e tipi di pubblico di potenziali clienti](/help/destinations/ui/activate-prospect-audiences.md) per selezionare le destinazioni.
