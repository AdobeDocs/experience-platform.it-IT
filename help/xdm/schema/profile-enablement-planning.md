---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;schema;set di dati;pianificazione;abilitazione
solution: Experience Platform
title: Pianificazione dell’abilitazione del profilo cliente in tempo reale
description: Esamina le considerazioni chiave da valutare prima di abilitare schemi e set di dati per Real-Time Customer Profile.
source-git-commit: da40dfde57b17b6a7387451eec48569174ad544b
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Pianificazione dell’abilitazione del profilo cliente in tempo reale

Utilizza questa pagina per verificare che lo schema e il set di dati siano pronti prima di abilitarli per Real-Time Customer Profile. Completa questa revisione della pianificazione dopo aver progettato i campi dello schema, ma prima di abilitare lo schema per il profilo. L’abilitazione del profilo applica modifiche comportamentali permanenti al modello di dati. Non è possibile annullare l’abilitazione dello schema e l’abilitazione di un set di dati influisce sul modo in cui i relativi record vengono elaborati all’interno di Real-Time Customer Profile. Esamina queste indicazioni per evitare abilitazione involontaria, problemi di qualità dei dati o vincoli a lungo termine nella progettazione dello schema.

L’abilitazione di Profilo determina il modo in cui i dati vengono uniti, uniti e attivati in Experience Platform. Planning garantisce che la struttura dello schema, la configurazione dell’identità e lo scopo del set di dati siano corretti prima di apportare la modifica. Dopo aver completato questa revisione della pianificazione, è possibile procedere all&#39;attivazione dei dati per il profilo nell&#39;interfaccia utente **[!UICONTROL Schema Editor]** o **[!UICONTROL Dataset]**.

## Prerequisiti

Prima di utilizzare questa guida alla pianificazione, assicurati di disporre di:

* Progettato uno schema utilizzando l&#39;API **[!UICONTROL Schema Editor]** o Schema Registry. Per iniziare, consulta l&#39;[esercitazione per la creazione dello schema](../tutorials/create-schema-ui.md).
* È stato configurato almeno un campo di identità nello schema. Per istruzioni, consulta la [guida alla configurazione del campo Identity](../ui/fields/identity.md).
* Comprensione di base di [Real-Time Customer Profile](../../profile/home.md) e utilizzo degli schemi per creare visualizzazioni cliente unificate.
* Autorizzazioni appropriate per abilitare schemi e set di dati per il profilo. Se non hai accesso alle opzioni di abilitazione del profilo, contatta l’amministratore di sistema.

Se non hai completato questi prerequisiti, inizia con l&#39;[esercitazione per la creazione di schemi](../tutorials/create-schema-ui.md) prima di procedere con questa guida alla pianificazione.

## Perché la pianificazione è importante {#why-planning-matters}

L’abilitazione del profilo cambia in modo permanente il modo in cui Experience Platform tratta i dati. Le seguenti modifiche permanenti si applicano a schemi e set di dati.

**Schemi**: quando si abilita uno schema per il profilo, non è possibile disabilitarlo o eliminarlo. Inoltre, non puoi rimuovere o rinominare i campi dallo schema dopo l’acquisizione dei dati. Questo significa che la progettazione dello schema deve essere completa e stabile prima di abilitare Profilo, in quanto non è possibile annullare la decisione o semplificare la struttura in un secondo momento.

**Set di dati**: quando abiliti un set di dati per il profilo, Real-Time Customer Profile utilizza i record per generare e aggiornare i profili. Rivedi il comportamento di abilitazione del set di dati nella [guida utente del set di dati](../../catalog/datasets/enable-for-profile.md). A differenza degli schemi, puoi disabilitare o eliminare il set di dati in un secondo momento, ma così facendo si rimuovono i record di profilo associati e si possono influenzare la segmentazione o i flussi di lavoro di attivazione. Considera l’impatto a valle prima di apportare modifiche a un set di dati abilitato.

Poiché queste modifiche influiscono sui processi a valle, verifica che uno schema e i relativi set di dati siano appropriati per il profilo prima di abilitarli.

### Informazioni sul flusso di lavoro di abilitazione

Devi abilitare sia lo schema che i set di dati che utilizzano tale schema per il profilo. Abilita le risorse nel seguente ordine:

1. **Abilita lo schema per il profilo**: abilitare innanzitutto il profilo nello schema in **[!UICONTROL Schema Editor]**. Questo consente di abilitare per il profilo qualsiasi set di dati che utilizza questo schema.
2. **Abilita singoli set di dati per il profilo**: dopo aver abilitato lo schema, abilita il profilo in ogni set di dati che deve contribuire ai profili cliente unificati.

Non puoi abilitare un set di dati per il profilo se il relativo schema non è già abilitato. Lo schema funge da prerequisito per l’abilitazione del set di dati. Questo processo in due fasi assicura che il modello dati venga convalidato prima che Real-Time Customer Profile inizi l’elaborazione dei record.

## Quando abilitare uno schema o un set di dati per il profilo {#when-to-enable}

Verifica che l’abilitazione del profilo sia appropriata per i tuoi dati.

Abilita profilo nelle situazioni seguenti:

* I dati contribuiscono a un profilo cliente unificato.
* I dati sono necessari per la segmentazione o i flussi di lavoro di attivazione.
* Lo schema include campi di identità che rappresentano una persona o una chiave a livello di cliente.
* Il set di dati contiene eventi esperienza o attributi di profilo che devono essere uniti tra i canali. Rivedi la classe [XDM ExperienceEvent](../classes/experienceevent.md) per confermare i requisiti dell&#39;evento.

## Quando non si desidera abilitare uno schema o un set di dati per il profilo {#when-not-to-enable}

Evita di abilitare il profilo nei seguenti casi:

* Lo schema rappresenta dati di ricerca o di solo riferimento.
* Il set di dati contiene dati di test, temporanei o non di produzione.
* I dati non identificano una persona o vengono utilizzati solo a scopo di reporting.
* Schema sperimentale o strutturalmente incompleto.

L’abilitazione di Profilo in questi scenari può creare profili non necessari, aumentare l’utilizzo della licenza o introdurre vincoli di schema a lungo termine.

## Considerazioni chiave prima di abilitare il profilo {#key-considerations}

Esamina le considerazioni in questa sezione per assicurarti che lo schema e il set di dati supportino i casi d’uso dei profili e la governance dei dati a lungo termine. Prima di abilitare Profile, verifica la struttura dello schema, la configurazione delle identità e lo scopo del set di dati.

### Preparazione dello schema

Rivedi la struttura dello schema per confermare che supporta i requisiti del profilo. Lo schema deve contenere i campi necessari per la segmentazione e l’attivazione, escludendo i campi sperimentali o non necessari a lungo termine. Ricorda che tutti i campi aggiuntivi aggiunti dopo l&#39;abilitazione devono essere additivi (per ulteriori dettagli, consulta [vincoli di immutabilità dello schema](#why-planning-matters)). Questa restrizione significa che devi convalidare attentamente la selezione del campo prima di abilitare Profilo. Per informazioni dettagliate sugli aggiornamenti consentiti, consulta le [regole di evoluzione dello schema](./composition.md#evolution).

### Configurazione identità

La configurazione dell’identità determina il modo in cui il profilo unisce i record tra i set di dati. Per prima cosa, verifica che sia selezionata un’identità primaria valida: questo campo deve essere stabile, univoco e compilato in modo coerente in tutti i record. Verifica che gli spazi dei nomi delle identità siano assegnati correttamente per evitare errori di unione. Se utilizzi identità secondarie, conferma che supportino i tuoi casi d’uso senza causare conflitti di profilo, che possono verificarsi quando individui diversi condividono lo stesso valore di identità. Real-Time Customer Profile risolve i conflitti applicando criteri di unione che determinano quali dati hanno la precedenza quando vengono uniti record in conflitto.

### Scopo del set di dati

Abilita un set di dati per il profilo solo quando contribuisce direttamente agli attributi del profilo o agli eventi esperienza utilizzati nei flussi di lavoro a valle. Evita di abilitare set di dati che contengono dati di ricerca o di riferimento non utilizzati nella segmentazione, dati di test o di esempio o record generati dal sistema operativo non destinati all’attivazione. Questi tipi di dati non contribuiscono ai profili cliente unificati e creano un sovraccarico di archiviazione non necessario. Se un set di dati non contiene campi di identità o dati di comportamento del cliente che supportano la segmentazione e l’attivazione, non abilitarlo per Profilo.

**Esempio**:

Abilita un set di dati &quot;Eventi di acquisto del cliente&quot; che contiene i dati della transazione con gli ID cliente. Real-Time Customer Profile utilizza questi eventi per creare timeline di clienti e abilitare la segmentazione in base al comportamento di acquisto.

NON abiliti un set di dati &quot;Catalogo prodotti&quot; che contiene solo dati di riferimento SKU senza identificatori cliente. L’abilitazione di questo tipo di set di dati crea un sovraccarico di storage non necessario senza contribuire ai profili unificati dei clienti.

## Elenco di controllo per la preabilitazione {#pre-enablement-checklist}

Utilizza questo elenco di controllo per confermare la fattibilità prima di abilitare uno schema o un set di dati per il profilo. Completa ogni elemento prima di abilitare il profilo.

### Controlli a livello di schema

Per prima cosa, verifica che la progettazione dello schema sia completa e stabile. Controlla lo schema per verificare che siano presenti tutti i campi obbligatori per il tuo caso d’uso e che non siano inclusi campi sperimentali o temporanei. Consulta le [best practice per la progettazione dello schema](./best-practices.md) per assicurarti che lo schema segua i modelli consigliati. Ottieni l&#39;approvazione del tuo team nell&#39;elenco dei campi finale (consulta [vincoli di immutabilità dello schema](#why-planning-matters)).

Successivamente, verifica che la configurazione dell’identità primaria sia corretta. Apri lo schema in **[!UICONTROL Schema Editor]** e individua il campo contrassegnato con l&#39;icona di identità. Verifica che questo campo sia popolato in modo coerente nei dati di origine e che lo spazio dei nomi dell’identità sia appropriato per il tuo caso d’uso. L’identità primaria deve essere stabile, univoca e presente in modo affidabile in tutti i record per garantire la corretta unione dei profili.

Infine, conferma che non è necessario rinominare o riorganizzare la struttura dello schema. Le modifiche alla struttura dello schema sono limitate solo agli aggiornamenti aggiuntivi (vedi [vincoli di immutabilità dello schema](#why-planning-matters)). Eventuali ambiguità a lungo termine nella denominazione o nell’organizzazione non possono essere corrette in un secondo momento, pertanto risolvi questi problemi prima dell’abilitazione.

### Controlli a livello di set di dati

Per ogni set di dati che intendi abilitare, inizia confermando che contiene dati relativi al profilo. Rivedi i record di esempio per verificare che contengano dati del cliente o dell’evento anziché informazioni puramente operative o di riferimento. Assicurati che i record includano valori di identità collegati ai profili dei clienti. I set di dati senza campi di identità o dati sul comportamento del cliente non devono essere abilitati per il profilo.

Determina se il set di dati deve contribuire all’unione di identità o alla segmentazione comprendendo in che modo i suoi valori di identità si relazionano con altri set di dati nell’ambiente abilitato per i profili. Valuta se i record in questo set di dati devono essere uniti con profili esistenti o creare nuovi frammenti di profilo. Consulta la [documentazione sui criteri di unione](../../profile/merge-policies/overview.md) per scoprire in che modo Real-Time Customer Profile unisce i record in diversi set di dati e come questo set di dati si inserisce nella tua strategia di identità complessiva.

Prima di abilitare il set di dati, stima il numero di valori di identità univoci in esso contenuti e verifica che tali valori di identità rappresentino i clienti effettivi anziché gli account di test o gli identificatori di sistema. Conferma che l’abilitazione di questo set di dati sia in linea con i diritti della licenza, in quanto ogni identità univoca contribuisce al conteggio del pubblico di indirizzabilità. L’abilitazione del profilo aumenta i costi di archiviazione ed elaborazione, quindi assicurati che il set di dati fornisca valore che giustifichi questo investimento.

Il completamento di questo elenco di controllo consente di evitare problemi che non possono essere risolti dopo l’abilitazione.

## Abilitazione del profilo per schema e set di dati {#enable-profile}

Dopo aver completato l’elenco di controllo per la preabilitazione, segui questi passaggi per abilitare il profilo. Come spiegato in [Informazioni sul flusso di lavoro di abilitazione](#why-planning-matters), è necessario abilitare lo schema prima di abilitare tutti i set di dati che utilizzano tale schema.

### Abilita lo schema per il profilo

Abilita prima il profilo sullo schema:

1. Passa a **[!UICONTROL Schemas]** nell&#39;interfaccia utente di Experience Platform.
2. Selezionare lo schema dall&#39;elenco per aprirlo in **[!UICONTROL Schema Editor]**.
3. Seleziona **[!UICONTROL Profile]** nella barra a destra. Nel pannello delle proprietà dello schema viene visualizzata una finestra di dialogo di conferma.
4. Selezionare **[!UICONTROL Enable]** per confermare. Lo schema è ora abilitato per il profilo.

Per istruzioni dettagliate, consulta la [guida all&#39;abilitazione dello schema](../ui/resources/schemas.md#profile) nella documentazione dell&#39;Editor di schema.

### Abilita i set di dati per il profilo

Dopo aver abilitato lo schema per il profilo, abilita ogni set di dati che deve contribuire ai profili unificati:

1. Passa a **[!UICONTROL Datasets]** nell&#39;interfaccia utente di Experience Platform.
2. Seleziona un set di dati dall’elenco per aprire la pagina dei dettagli del set di dati.
3. Seleziona **[!UICONTROL Profile]** nella barra a destra. Il pannello delle proprietà del set di dati viene aggiornato in modo da mostrare che Profilo è abilitato.

Ripeti questo processo per ogni set di dati che deve contribuire a Real-Time Customer Profile. Per istruzioni dettagliate e opzioni di abilitazione API, consulta la guida utente del set di dati a cui si fa riferimento nella sezione Prerequisiti.

### Perché l’ordine è importante

Come spiegato in [Informazioni sul flusso di lavoro di abilitazione](#why-planning-matters), è necessario abilitare lo schema prima di abilitare i set di dati. In questo modo Real-Time Customer Profile convalida la struttura dello schema e supporta le operazioni di profilo prima di consentire l’abilitazione dei set di dati, e tutti i set di dati che utilizzano lo schema ereditano le definizioni dei campi corrette per la segmentazione e l’unione di identità.

Dopo aver abilitato sia lo schema che i set di dati, Real-Time Customer Profile inizia a elaborare i record e a creare profili cliente unificati. I record acquisiti prima dell’abilitazione non vengono inclusi nei profili, a meno che non vengano riacquisiti i dati.

## Passaggi successivi {#next-steps}

Hai esaminato gli effetti permanenti dell’abilitazione del profilo, hai confermato che lo schema e i set di dati sono pronti e hai verificato che la configurazione dell’identità supporta i casi d’uso. Per approfondire la comprensione della struttura dello schema e delle relazioni tra i campi, rivedi le [nozioni di base sulla composizione dello schema](../schema/composition.md), che illustrano le regole di evoluzione dello schema e il modo in cui i campi interagiscono all&#39;interno del modello di dati. Se riscontri problemi durante o dopo l&#39;abilitazione, consulta la [guida alla risoluzione dei problemi XDM](../troubleshooting-guide.md) per i problemi e le soluzioni più comuni. Per ulteriori informazioni su come gli spazi dei nomi di identità influiscono sull&#39;unione e sulla risoluzione dei profili, consulta la [Panoramica sugli spazi dei nomi di identità](../../identity-service/features/namespaces.md).
