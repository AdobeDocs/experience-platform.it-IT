---
title: Aggiornamenti dell'architettura a Real-Time CDP B2B edition
description: Leggi questo documento per scoprire gli aggiornamenti completi dell’architettura a Real-Time CDP B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: d958a947-e195-4dd4-a04c-63ad82829728
source-git-commit: da288d1a917df85b3c003bc6592fda7a6f1eafe7
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 1%

---

# Aggiornamento dell&#39;architettura a Real-Time CDP B2B edition

>[!IMPORTANT]
>
>Questo documento illustra gli aggiornamenti dell’architettura alle edizioni B2B e B2P di Real-Time CDP. Gli aggiornamenti non richiederanno azioni da parte della maggior parte dei clienti. Tuttavia, esistono tipi di pubblico che non possono essere aggiornati automaticamente. Adobe collaborerà direttamente con te per affrontare questi scenari. Consulta questo documento per informazioni su come gli aggiornamenti influenzeranno le funzioni esistenti di Adobe Experience Platform. In caso di domande, contatta il team del tuo account Adobe.

Adobe ha riprogettato le edizioni B2B e B2P di Real-Time CDP per migliorare la scalabilità, le prestazioni e l’affidabilità, supportando allo stesso tempo casi d’uso B2B più avanzati. Per garantire che tutti i clienti beneficino di questi miglioramenti, Adobe aggiornerà tutti i clienti B2B e B2P esistenti alla nuova architettura.

Utilizza l’architettura avanzata per i seguenti vantaggi:

* **Scalabilità dell&#39;acquisizione dei dati**: è stato migliorato il supporto per le relazioni B2B ad alta cardinalità, ad esempio gli account connessi a migliaia di persone.
* **Valutazione del pubblico efficiente e affidabile**: segmentazione più rapida e resiliente per tipi di pubblico B2B complessi.
* **risoluzione entità**: risoluzione identità migliorata per le entità B2B, migliore qualità dei dati e riduzione della duplicazione per consentire segmentazione e aggregazione più accurate.

## Nuove funzioni

Leggi quanto segue per informazioni sui miglioramenti principali inclusi nell’aggiornamento dell’architettura.

### Istantanee dell’account per l’appartenenza al pubblico

Con la nuova architettura B2B, ora vengono inclusi i dettagli di iscrizione al pubblico per le entità account nelle esportazioni di snapshot. Questa funzione ti consente di accedere allo stato del pubblico a livello di account, ai timestamp e agli indicatori di iscrizione.

Con questo aggiornamento, ora puoi:

* Abilita i team di marketing e operativi per convalidare direttamente l’iscrizione al pubblico dell’account.
* Ottieni la parità delle funzioni tra i modelli di segmentazione del profilo (persona) e dell’account, garantendo un’esperienza coerente tra le entità.

Per ulteriori informazioni, leggi la documentazione su [tipi di pubblico dell&#39;account](../segmentation/types/account-audiences.md).

### Conteggi dei pubblici per tipi di pubblico che includono entità B2B

Le stime delle dimensioni del pubblico per i tipi di pubblico con entità B2B ora sono calcolate con precisione esatta. Queste stime sono disponibili durante l’anteprima e forniscono informazioni più precise e affidabili per i tipi di pubblico che coinvolgono complesse relazioni B2B.

Con questo aggiornamento, ora puoi:

* Utilizza informazioni provenienti da stime precise sulle dimensioni del pubblico per migliorare la pianificazione e il processo decisionale durante il processo di creazione del pubblico.
* Progetta in modo confidenziale tipi di pubblico B2B complessi, con la conoscenza di stime più accurate del pubblico.
* Consente una pianificazione più intelligente delle campagne, un targeting più preciso e una migliore allocazione delle risorse.

Per ulteriori informazioni, leggi la documentazione su [tipi di pubblico dell&#39;account](../segmentation/types/account-audiences.md).

## Aggiornamenti alle funzioni esistenti

Le seguenti funzioni sono state aggiornate come parte degli aggiornamenti dell’architettura B2B.

### Aggiornamenti al pubblico con più entità con attributi B2B ed eventi di esperienza

Come parte della nuova architettura di aggiornamento, i filtri degli eventi di esperienza non possono più essere utilizzati all’interno di un singolo pubblico multi-entità che include attributi B2B.

Per ottenere la stessa logica di pubblico, puoi utilizzare il Generatore di segmenti per [aggiungere tipi di pubblico e tipi di pubblico di riferimento](../segmentation/ui/segment-builder.md#adding-audiences)

Ad esempio:

* Creare un pubblico di Experience Event
   * Definisci separatamente la condizione comportamentale. Ad esempio: &quot;Persone che hanno visitato la pagina dei prezzi negli ultimi tre giorni&quot;.
* Creare un pubblico con più entità con attributi B2B.
   * Da qui, puoi fare riferimento al pubblico di Experience Event come parte dei criteri di questo pubblico. Ad esempio: &quot;Persone che sono un **&#39;Responsabile delle decisioni&#39;** di qualsiasi opportunità in cui l&#39;account si trova nel settore **&#39;Finanza&#39;** e membro del pubblico di persone che ha visitato la pagina dei prezzi negli ultimi tre giorni.

Una volta completato l&#39;aggiornamento, è necessario creare qualsiasi nuovo pubblico con più entità con attributi B2B ed eventi di esperienza utilizzando l&#39;approccio [segmento di segmento](../segmentation/methods/edge-segmentation.md#edge-segmentation-query-types).

>[!TIP]
>
>Un **segmento di segmenti** è una definizione di segmento che contiene uno o più segmenti batch o edge. **Nota**: se utilizzi un segmento di segmenti, l&#39;annullamento del profilo avverrà **ogni 24 ore**.

### Risoluzione delle entità e unione di precedenza temporale nei tipi di pubblico B2B

Come parte dell’aggiornamento dell’architettura, Adobe sta introducendo la risoluzione delle entità per account e opportunità. La risoluzione dell’entità si basa sulla corrispondenza degli ID deterministici e sui dati più recenti. Il processo di risoluzione delle entità viene eseguito quotidianamente durante la segmentazione batch, prima di valutare tipi di pubblico con più entità con attributi B2B.

>[!BEGINSHADEBOX]

#### Come funziona la risoluzione delle entità?

* **Prima**: se è stato utilizzato un numero DUNS (Data Universal Numbering System) come identità aggiuntiva e il numero DUNS dell&#39;account è stato aggiornato in un sistema di origine come CRM, l&#39;ID account è collegato sia ai numeri DUNS vecchi che a quelli nuovi.
* **Dopo**: se il numero DUNS è stato utilizzato come identità aggiuntiva e il numero DUNS dell&#39;account è stato aggiornato in un sistema di origine come CRM, l&#39;ID account viene collegato solo al nuovo numero DUNS, riflettendo in tal modo lo stato corrente dell&#39;account in modo più accurato.

>[!ENDSHADEBOX]

Con questo aggiornamento, ora puoi:

* Utilizza le API [!DNL Profile Access] per visualizzare i profili di unione più recenti una volta completati i processi giornalieri di risoluzione delle entità.
* Utilizza la maggiore precisione e coerenza dei dati dell’account e delle opportunità per segmentazione, attivazione e analisi.

Leggi [[!DNL Profile Access] API](../profile/api/entities.md) per ulteriori informazioni.

### Supporto dei criteri di unione per tipi di pubblico B2B con più entità

I tipi di pubblico con più entità e attributi B2B ora supportano un singolo criterio di unione, ovvero il criterio di unione predefinito configurato, anziché più criteri di unione.

Per ulteriori informazioni, consulta la guida del caso di utilizzo [segmentation per Real-Time CDP B2B edition](./segmentation/b2b.md).

### La ricerca e l&#39;eliminazione dell&#39;entità B2B nell&#39;API [!DNL Profile Access] sono state dichiarate obsolete

Le seguenti funzionalità di ricerca per le entità B2B che utilizzano l&#39;API [!DNL Profile Access] sono diventate obsolete:

* Relazione account-persona
* Relazione opportunità-persona
* Campaign
* Membro della campagna
* Elenco marketing
* Membri di elenco marketing

Le richieste di eliminazione per le seguenti entità B2B che utilizzano l&#39;API [!DNL Profile Access] diventeranno obsolete:

* Account
* Relazione account-persona
* Opportunità
* Relazione opportunità-persona
* Campaign
* Membro della campagna
* Elenco marketing
* Membri di elenco marketing

Leggi [[!DNL Profile Access] API](../profile/api/entities.md) per ulteriori informazioni.

### API del processo di segmento obsoleta

Nella nuova architettura, l’endpoint &quot;create a segment job&quot; (crea un processo di segmentazione) e la valutazione flessibile del pubblico *non sono supportati.

### Ricerche nel profilo account e opportunità

Ora puoi recuperare gli schemi di account e opportunità come entità dimensione di ricerca solo dopo aver completato il processo di risoluzione giornaliero delle entità. I nuovi record acquisiti non saranno disponibili per l’arricchimento dei profili o le definizioni dei segmenti fino al completamento del successivo ciclo di risoluzione dell’entità (in genere ogni 24 ore).

<!-- ### Deprecation of audience creation via API for B2B entities

Creation of audiences using B2B entities via API is being deprecated. The list of affected B2B entities include:

* Account
* Opportunity
* Account-Person Relation
* Opportunity-Person Relation
* Campaign
* Campaign Member
* Marketing List
* Marketing List Member

Read the [segment definitions endpoint API guide](../segmentation/api/segment-definitions.md) for more information. -->

### Modifiche alle importazioni di tipi di pubblico con più entità negli strumenti sandbox

Con gli aggiornamenti dell’architettura, non sarà più possibile importare tipi di pubblico con più entità con attributi B2B ed eventi di esperienza se un pacchetto che includeva tali tipi di pubblico veniva pubblicato prima dell’aggiornamento. Questi tipi di pubblico non verranno importati e non potranno essere convertiti automaticamente nella nuova architettura. Per ovviare a questo limite, è necessario creare un nuovo pacchetto con i tipi di pubblico aggiornati e quindi importarli nelle rispettive sandbox di destinazione utilizzando gli strumenti sandbox.

Le sandbox di sviluppo verranno aggiornate alla nuova architettura. I tipi di pubblico che possono essere aggiornati automaticamente verranno aggiornati; quelli che non possono essere disabilitati. I tipi di pubblico disattivati devono essere ricreati dopo l’aggiornamento.

Per ulteriori informazioni, consulta la [guida agli strumenti per la sandbox](../sandboxes/ui/sandbox-tooling.md).
