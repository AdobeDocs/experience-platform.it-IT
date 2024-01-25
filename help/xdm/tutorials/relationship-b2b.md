---
title: Definire una relazione tra due schemi nell’edizione B2B di Real-time Customer Data Platform
description: Scopri come definire una relazione molti-a-uno tra due schemi in Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 14032754-c7f5-46b6-90e6-c6e99af1efba
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 15%

---

# Definire una relazione molti-a-uno tra due schemi in Real-time Customer Data Platform B2B Edition {#relationship-b2b}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_reference_schema"
>title="Schema di riferimento"
>abstract="Seleziona lo schema con cui desideri stabilire una relazione. A seconda della classe dello schema, potrebbe avere anche relazioni esistenti con altre entità nel contesto B2B. Per capire in che modo le classi di schema B2B si relazionano tra loro, consulta la documentazione."

Adobe Real-time Customer Data Platform B2B Edition fornisce diverse classi Experience Data Model (XDM) che acquisiscono entità di dati B2B fondamentali, tra cui [account](../classes/b2b/business-account.md), [opportunità](../classes/b2b/business-opportunity.md), [campagne](../classes/b2b/business-campaign.md), e altro ancora. Creando schemi basati su queste classi e abilitandoli per l’utilizzo in [Profilo cliente in tempo reale](../../profile/home.md), è possibile unire dati provenienti da origini diverse in una rappresentazione unificata denominata schema di unione.

Tuttavia, gli schemi di unione possono contenere solo campi acquisiti da schemi che condividono la stessa classe. Qui entrano in gioco le relazioni tra schemi. Implementando relazioni negli schemi B2B, puoi descrivere il modo in cui queste entità aziendali si relazionano tra loro e includere attributi da più classi nei casi di utilizzo della segmentazione a valle.

Il diagramma seguente fornisce un esempio di come le diverse classi B2B possono relazionarsi tra loro in un’implementazione di base:

![Relazioni tra classi B2B](../images/tutorials/relationship-b2b/classes.png)

Questo tutorial illustra i passaggi necessari per definire una relazione molti-a-uno tra due schemi in Real-Time CDP B2B Edition.

>[!NOTE]
>
>Se non utilizzi Real-time Customer Data Platform B2B Edition o desideri creare una relazione uno-a-uno, consulta la guida su [creazione di una relazione uno-a-uno](./relationship-ui.md) invece.
>
>Questa esercitazione si concentra su come stabilire manualmente relazioni tra schemi B2B nell’interfaccia utente di Platform. Se inserisci dati da una connessione di origine B2B, puoi invece utilizzare un’utility di generazione automatica per creare gli schemi, le identità e le relazioni richiesti. Per ulteriori informazioni sugli spazi dei nomi e sugli schemi B2B, consulta la documentazione sulle origini. [utilizzo dell&#39;utilità di generazione automatica](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md).

## Introduzione

Questo tutorial richiede una buona conoscenza di [!DNL XDM System] e l’Editor di schema nel [!DNL Experience Platform] UI. Prima di iniziare questo tutorial, consulta la seguente documentazione:

* [Sistema XDM in Experience Platform](../home.md): panoramica di XDM e della relativa implementazione in [!DNL Experience Platform].
* [Nozioni di base sulla composizione dello schema](../schema/composition.md): introduzione dei blocchi predefiniti degli schemi XDM.
* [Creare uno schema utilizzando [!DNL Schema Editor]](create-schema-ui.md): tutorial che illustra le nozioni di base sulla creazione e la modifica di schemi nell’interfaccia utente di.

## Definire uno schema di origine e di riferimento

È previsto che tu abbia già creato i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questa esercitazione crea una relazione tra le opportunità di business (definite in un’ &quot;[!DNL Opportunities]&quot;) e il relativo account aziendale associato (definito in un&quot;[!DNL Accounts]&quot;).

Le relazioni tra schemi sono rappresentate da un campo dedicato all’interno di un **schema di origine** che fa riferimento al campo di identità principale di una **schema di riferimento**. Nei passaggi successivi, &quot;[!DNL Opportunities]&quot; funge da schema di origine, mentre &quot;[!DNL Accounts]&quot; funge da schema di riferimento.

### Informazioni sulle identità nelle relazioni B2B

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_identity_namespace"
>title="Spazio dei nomi delle identità di riferimento"
>abstract="Spazio dei nomi (tipo) per il campo di identità primaria dello schema di riferimento. Per poter partecipare a una relazione, nello schema di riferimento deve essere stato stabilito un campo di identità primaria. Per ulteriori informazioni sulle identità nelle relazioni B2B, consulta la documentazione."

Per stabilire una relazione, lo schema di riferimento deve avere un’identità primaria definita. Quando imposti un’identità primaria per un’entità B2B, tieni presente che gli ID di entità basati su stringhe possono sovrapporsi se vengono raccolti tra sistemi o posizioni diversi, il che potrebbe causare conflitti di dati in Platform.

Per tenere conto di ciò, tutte le classi B2B standard contengono campi &quot;chiave&quot; conformi alla [[!UICONTROL Origine B2B] tipo di dati](../data-types/b2b-source.md). Questo tipo di dati fornisce campi per un identificatore di stringa per l’entità B2B insieme ad altre informazioni contestuali sull’origine dell’identificatore. Uno di questi campi, `sourceKey`, concatena i valori degli altri campi nel tipo di dati per produrre un identificatore completamente univoco per l’entità. Questo campo deve sempre essere utilizzato come identità primaria per gli schemi di entità B2B.

![campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Quando [impostazione di un campo XDM come identità](../ui/fields/identity.md), devi fornire uno spazio dei nomi delle identità in cui definire l’identità. Può trattarsi di uno spazio dei nomi standard fornito da Adobe o di uno spazio dei nomi personalizzato definito dalla tua organizzazione. In pratica, lo spazio dei nomi è semplicemente una stringa contestuale e può essere impostato su qualsiasi valore desiderato, a condizione che sia significativo per la tua organizzazione per la categorizzazione del tipo di identità. Consulta la panoramica su [spazi dei nomi di identità](../../identity-service/features/namespaces.md) per ulteriori informazioni.

A scopo di riferimento, le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questo tutorial prima che sia stata definita una relazione. Tieni presente dove sono state definite le identità primarie nella struttura dello schema e gli spazi dei nomi personalizzati utilizzati.

### [!DNL Opportunities] schema

Lo schema di origine &quot;[!DNL Opportunities]&quot; si basa sul [!UICONTROL Opportunità di business XDM] classe. Uno dei campi forniti dalla classe, `opportunityKey`, funge da identificatore dello schema. In particolare, `sourceKey` campo sotto `opportunityKey` è impostato come identità primaria dello schema in uno spazio dei nomi personalizzato denominato [!DNL B2B Opportunity].

Come mostrato nella **[!UICONTROL Proprietà schema]**, questo schema è stato abilitato per l’utilizzo in [!DNL Real-Time Customer Profile].

![Schema Opportunità](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Lo schema di riferimento &quot;[!DNL Accounts]&quot; si basa sul [!UICONTROL Account XDM] classe. Livello principale `accountKey` contiene il `sourceKey` che funge da identità primaria in uno spazio dei nomi personalizzato denominato [!DNL B2B Account]. Questo schema è stato abilitato anche per l’utilizzo nel profilo.

![Schema Account](../images/tutorials/relationship-b2b/accounts.png)

## Definire un campo relazione per lo schema di origine {#relationship-field}

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_current"
>title="Nome della relazione dallo schema attuale"
>abstract="Etichetta che descrive la relazione dallo schema attuale allo schema di riferimento (ad esempio, “Account correlato”). Questa etichetta viene utilizzata nel profilo e nella segmentazione per fornire contesto ai dati provenienti da entità B2B correlate. Per ulteriori informazioni sulla creazione di relazioni tra schemi B2B, consulta la documentazione."

>[!CONTEXTUALHELP]
>id="platform_xdm_b2b_relationship_name_reference"
>title="Nome della relazione dallo schema di riferimento"
>abstract="Etichetta che descrive la relazione dallo schema di riferimento allo schema attuale (ad esempio, “Opportunità correlate”). Questa etichetta viene utilizzata nel profilo e nella segmentazione per fornire contesto ai dati provenienti da entità B2B correlate. Per ulteriori informazioni sulla creazione di relazioni tra schemi B2B, consulta la documentazione."

Per definire una relazione tra due schemi, lo schema di origine deve disporre di un campo dedicato che indica l’identità primaria dello schema di riferimento. Le classi B2B standard includono campi chiave di origine dedicati per le entità aziendali comunemente correlate. Ad esempio, il [!UICONTROL Opportunità di business XDM] la classe contiene campi chiave di origine per un account correlato (`accountKey`) e una campagna correlata (`campaignKey`). Tuttavia, puoi anche aggiungere altri [!UICONTROL Origine B2B] campi dello schema utilizzando gruppi di campi personalizzati, se sono necessari più componenti predefiniti.

>[!NOTE]
>
>Attualmente, è possibile definire solo relazioni molti-a-uno e uno-a-uno da uno schema di origine a uno schema di riferimento. Per le relazioni uno-a-molti, devi definire il campo relazione nello schema che rappresenta il &quot;molti&quot;.

Per impostare un campo di relazione, selezionare l&#39;icona freccia (![Icona freccia](../images/tutorials/relationship-b2b/arrow.png)) accanto al campo in questione all’interno dell’area di lavoro. Nel caso di [!DNL Opportunities] schema, questo è il `accountKey.sourceKey` poiché l’obiettivo è quello di stabilire una relazione molti-a-uno con un account.

![Pulsante di relazione](../images/tutorials/relationship-b2b/relationship-button.png)

Viene visualizzata una finestra di dialogo che consente di specificare i dettagli della relazione. Il tipo di relazione viene impostato automaticamente su **[!UICONTROL Molti a uno]**.

![Finestra di dialogo di relazione](../images/tutorials/relationship-b2b/relationship-dialog.png)

Sotto **[!UICONTROL Schema di riferimento]**, utilizza la barra di ricerca per trovare il nome dello schema di riferimento. Quando si evidenzia il nome dello schema di riferimento, **[!UICONTROL Spazio dei nomi dell’identità di riferimento]** viene aggiornato automaticamente allo spazio dei nomi dell’identità primaria dello schema.

![Schema di riferimento](../images/tutorials/relationship-b2b/reference-schema.png)

Sotto **[!UICONTROL Nome Di Relazione Dallo Schema Corrente]** e **[!UICONTROL Nome di relazione da schema di riferimento]**, forniscono nomi descrittivi per la relazione nel contesto rispettivamente degli schemi di origine e di riferimento. Al termine, seleziona **[!UICONTROL Salva]** per applicare le modifiche e salvare lo schema.

![Nome relazione](../images/tutorials/relationship-b2b/relationship-name.png)

L’area di lavoro viene nuovamente visualizzata, con il campo relazione ora contrassegnato con il nome descrittivo fornito in precedenza. Il nome della relazione è elencato anche nella barra a sinistra per un riferimento semplice.

![Relazione applicata](../images/tutorials/relationship-b2b/relationship-applied.png)

Se visualizzi la struttura dello schema di riferimento, l’indicatore di relazione viene visualizzato accanto al campo dell’identità primaria dello schema e nella barra a sinistra.

![Marcatore relazione schema di destinazione](../images/tutorials/relationship-b2b/destination-relationship.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente una relazione molti-a-uno tra due schemi utilizzando [!DNL Schema Editor]. Una volta che i dati sono stati acquisiti utilizzando set di dati basati su questi schemi e che i dati sono stati attivati nell’archivio dati Profilo, puoi utilizzare gli attributi di entrambi gli schemi per [casi d’uso della segmentazione multi-classe](../../rtcdp/segmentation/b2b.md).
