---
title: Definire una relazione tra due schemi nell’edizione B2B di Real-time Customer Data Platform
description: Scopri come definire una relazione molti-a-uno tra due schemi in Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: 85d6cf10599d153a15c1bd56067f57439ddd0133
workflow-type: tm+mt
source-wordcount: '1769'
ht-degree: 12%

---

# Definire una relazione molti-a-uno tra due schemi in Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Schema di riferimento"
>abstract="Seleziona lo schema con cui desideri stabilire una relazione. A seconda della classe dello schema, potrebbe avere anche relazioni esistenti con altre entità nel contesto B2B. Per capire in che modo le classi di schema B2B si relazionano tra loro, consulta la documentazione."

Adobe Real-time Customer Data Platform B2B Edition fornisce diverse classi Experience Data Model (XDM) che acquisiscono entità di dati B2B fondamentali, tra cui [account](../classes/b2b/business-account.md), [opportunità](../classes/b2b/business-opportunity.md), [campagne](../classes/b2b/business-campaign.md) e altro ancora. Creando schemi basati su queste classi e abilitandoli per l&#39;utilizzo in [Real-Time Customer Profile](../../profile/home.md), è possibile unire dati provenienti da origini diverse in una rappresentazione unificata denominata schema di unione.

Tuttavia, gli schemi di unione possono contenere solo campi acquisiti da schemi che condividono la stessa classe. Qui entrano in gioco le relazioni tra schemi. Implementando relazioni negli schemi B2B, puoi descrivere il modo in cui queste entità aziendali si relazionano tra loro e includere attributi da più classi nei casi di utilizzo della segmentazione a valle.

Il diagramma seguente fornisce un esempio di come le diverse classi B2B possono relazionarsi tra loro in un’implementazione di base:

![Relazioni classe B2B](../images/tutorials/relationship-b2b/classes.png)

Questo tutorial illustra i passaggi necessari per definire una relazione molti-a-uno tra due schemi in Real-Time CDP B2B Edition.

>[!NOTE]
>
>Se non utilizzi Real-time Customer Data Platform B2B Edition o desideri creare una relazione uno-a-uno, consulta invece la guida sulla [creazione di una relazione uno-a-uno](./relationship-ui.md).
>
>Questa esercitazione si concentra su come stabilire manualmente relazioni tra schemi B2B nell’interfaccia utente di Platform. Se inserisci dati da una connessione di origine B2B, puoi invece utilizzare un’utility di generazione automatica per creare gli schemi, le identità e le relazioni richiesti. Per ulteriori informazioni su [utilizzo dell&#39;utilità di generazione automatica](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md), vedere la documentazione sulle origini degli spazi dei nomi e degli schemi B2B.

## Introduzione

Questo tutorial richiede una buona conoscenza di [!DNL XDM System] e dell&#39;Editor di schema nell&#39;interfaccia utente di [!DNL Experience Platform]. Prima di iniziare questo tutorial, consulta la seguente documentazione:

* [Sistema XDM nell&#39;Experience Platform](../home.md): panoramica di XDM e della relativa implementazione in [!DNL Experience Platform].
* [Nozioni di base sulla composizione dello schema](../schema/composition.md): introduzione dei blocchi predefiniti degli schemi XDM.
* [Crea uno schema utilizzando  [!DNL Schema Editor]](create-schema-ui.md): un tutorial che illustra le nozioni di base sulla creazione e la modifica di schemi nell&#39;interfaccia utente.

## Definire uno schema di origine e di riferimento

È previsto che tu abbia già creato i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questa esercitazione crea una relazione tra le opportunità di business (definite in uno schema &quot;[!DNL Opportunities]&quot;) e il relativo account aziendale associato (definito in uno schema &quot;[!DNL Accounts]&quot;).

Le relazioni tra schemi sono rappresentate da un campo dedicato all&#39;interno di uno **schema di origine** che fa riferimento al campo di identità primaria di uno **schema di riferimento**. Nei passaggi seguenti, &quot;[!DNL Opportunities]&quot; funge da schema di origine, mentre &quot;[!DNL Accounts]&quot; funge da schema di riferimento.

### Informazioni sulle identità nelle relazioni B2B

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Spazio dei nomi delle identità di riferimento"
>abstract="Spazio dei nomi (tipo) per il campo di identità primaria dello schema di riferimento. Per poter partecipare a una relazione, nello schema di riferimento deve essere stato stabilito un campo di identità primaria. Per ulteriori informazioni sulle identità nelle relazioni B2B, consulta la documentazione."

Per stabilire una relazione, lo schema di riferimento deve avere un’identità primaria definita. Quando imposti un’identità primaria per un’entità B2B, tieni presente che gli ID di entità basati su stringhe possono sovrapporsi se vengono raccolti tra sistemi o posizioni diversi, il che potrebbe causare conflitti di dati in Platform.

Per tenere conto di ciò, tutte le classi B2B standard contengono campi &quot;key&quot; conformi al tipo di dati [[!UICONTROL B2B Source]](../data-types/b2b-source.md). Questo tipo di dati fornisce campi per un identificatore di stringa per l’entità B2B insieme ad altre informazioni contestuali sull’origine dell’identificatore. Uno di questi campi, `sourceKey`, concatena i valori degli altri campi nel tipo di dati per produrre un identificatore completamente univoco per l&#39;entità. Questo campo deve sempre essere utilizzato come identità primaria per gli schemi di entità B2B.

![campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Quando [imposti un campo XDM come identità](../ui/fields/identity.md), devi fornire uno spazio dei nomi identità in cui definire l&#39;identità. Può trattarsi di uno spazio dei nomi standard fornito da Adobe o di uno spazio dei nomi personalizzato definito dalla tua organizzazione. In pratica, lo spazio dei nomi è semplicemente una stringa contestuale e può essere impostato su qualsiasi valore desiderato, a condizione che sia significativo per la tua organizzazione per la categorizzazione del tipo di identità. Per ulteriori informazioni, consulta la panoramica sugli [spazi dei nomi di identità](../../identity-service/features/namespaces.md).

A scopo di riferimento, le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questo tutorial prima che sia stata definita una relazione. Tieni presente dove sono state definite le identità primarie nella struttura dello schema e gli spazi dei nomi personalizzati utilizzati.

### Schema delle opportunità

Lo schema di origine &quot;[!DNL Opportunities]&quot; è basato sulla classe [!UICONTROL Opportunità di business XDM]. Uno dei campi forniti dalla classe, `opportunityKey`, funge da identificatore per lo schema. In particolare, il campo `sourceKey` nell&#39;oggetto `opportunityKey` viene impostato come identità primaria dello schema in uno spazio dei nomi personalizzato denominato [!DNL B2B Opportunity].

Come visto in **[!UICONTROL Proprietà campo]**, questo schema è stato abilitato per l&#39;utilizzo in [!DNL Real-Time Customer Profile].

![Lo schema Opportunità nell&#39;editor schema con l&#39;oggetto opportunitàKey e l&#39;interruttore Abilita per profilo evidenziato.](../images/tutorials/relationship-b2b/opportunities.png)

### Schema [!DNL Accounts]

Lo schema di riferimento &quot;[!DNL Accounts]&quot; è basato sulla classe [!UICONTROL Account XDM]. Il campo `accountKey` a livello di radice contiene `sourceKey` che funge da identità primaria in uno spazio dei nomi personalizzato denominato [!DNL B2B Account]. Questo schema è stato abilitato anche per l’utilizzo nel profilo.

![Lo schema Account nell&#39;Editor di schema con l&#39;oggetto accountKey e l&#39;interruttore Abilita per profilo evidenziato.](../images/tutorials/relationship-b2b/accounts.png)

## Definire un campo relazione per lo schema di origine {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Nome della relazione dallo schema attuale"
>abstract="Etichetta che descrive la relazione dallo schema attuale allo schema di riferimento (ad esempio, “Account correlato”). Questa etichetta viene utilizzata nel profilo e nella segmentazione per fornire contesto ai dati provenienti da entità B2B correlate. Per ulteriori informazioni sulla creazione di relazioni tra schemi B2B, consulta la documentazione."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Nome della relazione dallo schema di riferimento"
>abstract="Etichetta che descrive la relazione dallo schema di riferimento allo schema attuale (ad esempio, “Opportunità correlate”). Questa etichetta viene utilizzata nel profilo e nella segmentazione per fornire contesto ai dati provenienti da entità B2B correlate. Per ulteriori informazioni sulla creazione di relazioni tra schemi B2B, consulta la documentazione."

Per definire una relazione tra due schemi, lo schema di origine deve disporre di un campo dedicato che indica l’identità primaria dello schema di riferimento. Le classi B2B standard includono campi chiave di origine dedicati per le entità aziendali comunemente correlate. Ad esempio, la classe [!UICONTROL Opportunità di business XDM] contiene campi chiave di origine per un account correlato (`accountKey`) e una campagna correlata (`campaignKey`). Tuttavia, è anche possibile aggiungere altri campi [!UICONTROL B2B Source] allo schema utilizzando i gruppi di campi personalizzati, se sono necessari più dei componenti predefiniti.

>[!NOTE]
>
>Attualmente, è possibile definire solo relazioni molti-a-uno e uno-a-uno da uno schema di origine a uno schema di riferimento. Per le relazioni uno-a-molti, devi definire il campo relazione nello schema che rappresenta il &quot;molti&quot;.

Per impostare un campo di relazione, seleziona il campo in questione nell&#39;area di lavoro, seguito da **[!UICONTROL Aggiungi relazione]** nella barra laterale [!UICONTROL Proprietà schema]. Nel caso dello schema [!DNL Opportunities], questo è il campo `accountKey.sourceKey` poiché l&#39;obiettivo è quello di stabilire una relazione molti-a-uno con un account.

![Editor schema con il campo sourceKey e la relazione Add evidenziati.](../images/tutorials/relationship-b2b/add-relationship.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Aggiungi relazione]. Utilizza questa finestra di dialogo per specificare i dettagli della relazione. Per impostazione predefinita, il tipo di relazione è impostato su **[!UICONTROL Many-to-one]**.

![Finestra di dialogo Aggiungi relazione con relazione schema molti-a-uno evidenziata.](../images/tutorials/relationship-b2b/relationship-dialog.png)

In **[!UICONTROL Schema di riferimento]**, utilizzare la barra di ricerca o il menu a discesa per trovare il nome dello schema di riferimento. Quando si evidenzia il nome dello schema di riferimento, il campo **[!UICONTROL Spazio dei nomi identità di riferimento]** viene aggiornato automaticamente allo spazio dei nomi dell&#39;identità primaria dello schema di riferimento.

>[!NOTE]
>
>L’elenco degli schemi di riferimento disponibili viene filtrato in modo da contenere solo schemi idonei. Agli schemi **must** è assegnata un&#39;identità primaria e possono essere una classe B2B o una classe Profilo individuale. Gli schemi di classi prospect non sono in grado di avere relazioni.

![La finestra di dialogo Aggiungi relazione con i campi Schema di riferimento e Spazio dei nomi Identità di riferimento è evidenziata.](../images/tutorials/relationship-b2b/reference-schema.png)

In **[!UICONTROL Nome relazione da schema corrente]** e **[!UICONTROL Nome relazione da schema di riferimento]**, fornire nomi descrittivi per la relazione rispettivamente nel contesto degli schemi di origine e di riferimento. Al termine, selezionare **[!UICONTROL Applica]** per confermare le modifiche e salvare la relazione.

>[!NOTE]
>
>I nomi delle relazioni non possono contenere più di 35 caratteri.

![Finestra di dialogo Aggiungi relazione con i campi Nome relazione evidenziati.](../images/tutorials/relationship-b2b/relationship-name.png)

L’area di lavoro viene nuovamente visualizzata, con il campo relazione ora contrassegnato con il nome descrittivo fornito in precedenza. Il nome della relazione è elencato anche nella barra a sinistra per un riferimento semplice.

![Editor di schema con il nuovo nome di relazione applicato.](../images/tutorials/relationship-b2b/relationship-applied.png)

Se visualizzi la struttura dello schema di riferimento, l’indicatore di relazione viene visualizzato accanto al campo dell’identità primaria dello schema e nella barra a sinistra.

![Lo schema di destinazione nell&#39;Editor schema con il nuovo indicatore di relazione evidenziato.](../images/tutorials/relationship-b2b/destination-relationship.png)

## Modificare una relazione tra schemi B2B {#edit-schema-relationship}

Una volta stabilita una relazione con lo schema, selezionare il campo relazione nello schema di origine seguito da **[!UICONTROL Modifica relazione]**.

>[!NOTE]
>
>Per visualizzare tutte le relazioni associate, seleziona il campo dell&#39;identità primaria nello schema di riferimento seguito da [!UICONTROL Visualizza relazioni].
>![Editor di schema con un campo di relazione selezionato ed evidenziata Visualizza relazione.](../images/tutorials/relationship-b2b/view-relationships.png "Editor di schema con un campo di relazione selezionato e una relazione di visualizzazione evidenziata."){width="100" zoomable="yes"}

![Editor di schema con campi di relazione e Modifica relazione evidenziati.](../images/tutorials/relationship-b2b/edit-b2b-relationship.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Modifica relazione]. Da questa finestra di dialogo è possibile modificare lo schema di riferimento e i nomi delle relazioni oppure eliminare la relazione. Impossibile modificare il tipo di relazione molti-a-uno.

![Finestra di dialogo Modifica relazione.](../images/tutorials/relationship-b2b/edit-b2b-relationship-dialog.png)

Per mantenere l’integrità dei dati ed evitare interruzioni nella segmentazione e in altri processi, considera le seguenti linee guida durante la gestione delle relazioni tra schemi e set di dati collegati:

* Evita di eliminare direttamente le relazioni se uno schema è associato a un set di dati, in quanto ciò può influire negativamente sulla segmentazione. Elimina invece il set di dati associato prima di rimuovere la relazione.
* Non è possibile modificare lo schema di riferimento senza prima eliminare la relazione esistente. Tuttavia, questo deve essere fatto con cautela, in quanto l’eliminazione di una relazione con un set di dati associato può causare conseguenze indesiderate.
* L’aggiunta di nuove relazioni a uno schema con set di dati collegati esistenti potrebbe non funzionare come previsto e causare potenziali conflitti.

## Filtrare e cercare relazioni {#filter-and-search}

Puoi filtrare e cercare relazioni specifiche all&#39;interno degli schemi dalla scheda [!UICONTROL Relazioni] dell&#39;area di lavoro [!UICONTROL Schemi]. È possibile utilizzare questa visualizzazione per individuare e gestire rapidamente le relazioni. Per istruzioni dettagliate sulle opzioni di filtro, leggi il documento su [esplorazione delle risorse dello schema](../ui/explore.md#lookup).

![Scheda Relazioni nell&#39;area di lavoro Schemi.](../images/tutorials/relationship-b2b/relationship-tab.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata creata una relazione molti-a-uno tra due schemi utilizzando [!DNL Schema Editor]. Una volta che i dati sono stati acquisiti utilizzando set di dati basati su questi schemi e tali dati sono stati attivati nell&#39;archivio dati Profilo, puoi utilizzare gli attributi di entrambi gli schemi per [casi di utilizzo di segmentazione con più classi](../../rtcdp/segmentation/b2b.md).
