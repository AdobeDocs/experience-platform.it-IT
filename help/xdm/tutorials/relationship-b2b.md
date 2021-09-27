---
title: Definire una relazione tra due schemi in tempo reale Customer Data Platform B2B Edition
description: Scopri come definire una relazione molti-a-uno tra due schemi in Real-time Customer Data Platform B2B Edition.
source-git-commit: 5fd82b02eb25f3d575de695c2f2b14a5e5b18400
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 0%

---

# Definire una relazione tra due schemi in Real-time Customer Data Platform B2B Edition

>[!NOTE]
>
>Se non utilizzi Real-time Customer Data Platform B2B Edition, consulta la guida alla [creazione di una relazione non B2B](./relationship-ui.md) .

Real-time Customer Data Platform B2B Edition fornisce diverse classi Experience Data Model (XDM) che acquisiscono entità dati B2B fondamentali, tra cui [account](../classes/b2b/business-account.md), [opportunità](../classes/b2b/business-opportunity.md), [campagne](../classes/b2b/business-campaign.md) e altro ancora. Costruendo schemi basati su queste classi e abilitandoli per l&#39;utilizzo in [Profilo cliente in tempo reale](../../profile/home.md), puoi unire i dati provenienti da origini diverse in una rappresentazione unificata denominata schema di unione.

Tuttavia, gli schemi di unione possono contenere solo campi acquisiti da schemi che condividono la stessa classe. Qui entrano in gioco le relazioni tra schemi. Implementando relazioni negli schemi B2B, puoi descrivere come queste entità business si relazionano tra loro e possono includere attributi di più classi nei casi di utilizzo della segmentazione a valle.

Il diagramma seguente fornisce un esempio di correlazione tra le diverse classi B2B in un’implementazione di base:

![Relazioni tra le classi B2B](../images/tutorials/relationship-b2b/classes.png)

Questa esercitazione descrive i passaggi per definire una relazione molti-a-uno tra due schemi in Real-time CDP B2B Edition.

>[!NOTE]
>
>Questa esercitazione si concentra su come stabilire manualmente le relazioni tra schemi B2B nell’interfaccia utente di Platform. Se si inseriscono dati da una connessione sorgente B2B, è possibile utilizzare un&#39;utilità di generazione automatica per creare gli schemi, le identità e le relazioni richiesti. Per ulteriori informazioni su [utilizzando l&#39;utilità di generazione automatica](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md), consulta la documentazione sulle origini di spazi dei nomi e schemi B2B .

## Introduzione

Questa esercitazione richiede una buona comprensione di [!DNL XDM System] e dell’Editor di schema nell’ interfaccia utente di [!DNL Experience Platform] . Prima di iniziare questa esercitazione, consulta la seguente documentazione:

* [Sistema XDM in Experience Platform](../home.md): Panoramica di XDM e della sua implementazione in  [!DNL Experience Platform].
* [Nozioni di base sulla composizione](../schema/composition.md) dello schema: Introduzione dei blocchi costitutivi degli schemi XDM.
* [Crea uno schema utilizzando [!DNL Schema Editor]](create-schema-ui.md): Un’esercitazione che illustra le nozioni di base su come creare e modificare gli schemi nell’interfaccia utente di .

## Definire uno schema di origine e di destinazione

È previsto che siano già stati creati i due schemi che verranno definiti nella relazione. A scopo dimostrativo, questa esercitazione crea una relazione tra le opportunità aziendali (definite in uno schema &quot;[!DNL Opportunities]&quot;) e il relativo account aziendale associato (definito in uno schema &quot;[!DNL Accounts]&quot;).

Le relazioni dello schema sono rappresentate da un campo dedicato all&#39;interno di uno **schema di origine** che fa riferimento al campo di identità principale di uno **schema di destinazione**. Nei passaggi successivi, &quot;[!DNL Opportunities]&quot; funge da schema di origine, mentre &quot;[!DNL Accounts]&quot; agisce come schema di destinazione.

### Informazioni sulle identità nelle relazioni B2B

Per stabilire una relazione, entrambi gli schemi devono avere identità principali definite ed essere abilitati per [!DNL Real-time Customer Profile]. Quando imposti un’identità primaria per un’entità B2B, ricorda che gli ID di entità basati su stringhe possono sovrapporsi se li raccogli tra sistemi o posizioni diversi, il che potrebbe causare conflitti di dati in Platform.

Per questo motivo, tutte le classi B2B standard contengono campi &quot;key&quot; conformi al tipo di dati [[!UICONTROL B2B Source]](../data-types/b2b-source.md). Questo tipo di dati fornisce campi per un identificatore di stringa per l’entità B2B, insieme ad altre informazioni contestuali sull’origine dell’identificatore. Uno di questi campi, `sourceKey`, concatena i valori degli altri campi nel tipo di dati per produrre un identificatore completamente univoco per l’entità. Questo campo deve sempre essere utilizzato come identità principale per gli schemi di entità B2B.

![campo sourceKey](../images/tutorials/relationship-b2b/sourcekey.png)

>[!NOTE]
>
>Quando [imposti un campo XDM come identità](../ui/fields/identity.md), devi fornire uno spazio dei nomi di identità per definire l&#39;identità in. Può trattarsi di uno spazio dei nomi standard fornito dall’Adobe o di uno spazio dei nomi personalizzato definito dall’organizzazione. In pratica, lo spazio dei nomi è semplicemente una stringa contestuale e può essere impostato su qualsiasi valore desideri, purché sia significativo per la tua organizzazione per la classificazione del tipo di identità. Per ulteriori informazioni, consulta la panoramica sui [namespace di identità](../../identity-service/namespaces.md) .

A scopo di riferimento, le sezioni seguenti descrivono la struttura di ogni schema utilizzato in questa esercitazione prima che sia stata definita una relazione. Prendi nota della posizione in cui sono state definite le identità principali nella struttura dello schema e negli spazi dei nomi personalizzati utilizzati.

### [!DNL Opportunities] schema

Lo schema di origine &quot;[!DNL Opportunities]&quot; è basato sulla classe [!UICONTROL Opportunità aziendali XDM]. Uno dei campi forniti dalla classe `opportunityKey` funge da identificatore per lo schema. Nello specifico, il campo `sourceKey` sotto l&#39;oggetto `opportunityKey` viene impostato come identità principale dello schema in uno spazio dei nomi personalizzato denominato [!DNL B2B Opportunity].
Come mostrato in **[!UICONTROL Proprietà schema]**, questo schema è stato abilitato per l&#39;utilizzo in [!DNL Real-time Customer Profile].

![Schema opportunità](../images/tutorials/relationship-b2b/opportunities.png)

### [!DNL Accounts] schema

Lo schema di destinazione &quot;[!DNL Accounts]&quot; è basato sulla classe [!UICONTROL Account XDM]. Il campo a livello principale `accountKey` contiene la `sourceKey` che agisce come identità principale in uno spazio dei nomi personalizzato denominato [!DNL B2B Account]. Questo schema è stato abilitato anche per l’utilizzo in Profilo.

![Schema account](../images/tutorials/relationship-b2b/accounts.png)

## Definire un campo di relazione per lo schema di origine {#relationship-field}

Per definire una relazione tra due schemi, lo schema di origine deve disporre di un campo dedicato che faccia riferimento all’identità primaria dello schema di destinazione. Le classi B2B standard includono campi chiave sorgente dedicati per le entità business comunemente correlate. Ad esempio, la classe [!UICONTROL XDM Business Opportunity] contiene i campi chiave di origine per un account correlato (`accountKey`) e una campagna correlata (`campaignKey`). Tuttavia, è anche possibile aggiungere altri campi [!UICONTROL B2B Source] allo schema utilizzando gruppi di campi personalizzati se sono necessari più componenti di quelli predefiniti.

>[!NOTE]
>
>Attualmente, è possibile definire solo relazioni molti-a-uno da uno schema di origine a uno schema di destinazione. Per le relazioni uno-a-molti, è necessario definire il campo di relazione nello schema che rappresenta i &quot;molti&quot;.

Per impostare un campo di relazione, seleziona l’icona a forma di freccia (![Icona a freccia](../images/tutorials/relationship-b2b/arrow.png)) accanto al campo in questione all’interno dell’area di lavoro. Nel caso dello schema [!DNL Opportunities], si tratta del campo `accountKey.sourceKey` poiché l&#39;obiettivo è quello di stabilire una relazione molti-a-uno con un account.

![Pulsante Relazione](../images/tutorials/relationship-b2b/relationship-button.png)

Viene visualizzata una finestra di dialogo che consente di specificare i dettagli della relazione. Il tipo di relazione viene impostato automaticamente su **[!UICONTROL Many-to-one]**.

![Dialogo tra relazioni](../images/tutorials/relationship-b2b/relationship-dialog.png)

In **[!UICONTROL Schema di riferimento]**, utilizza la barra di ricerca per trovare il nome dello schema di destinazione. Quando si evidenzia il nome dello schema di destinazione, il campo **[!UICONTROL Riferimento allo spazio dei nomi dell&#39;identità]** si aggiorna automaticamente allo spazio dei nomi dell&#39;identità principale dello schema.

![Schema di riferimento](../images/tutorials/relationship-b2b/reference-schema.png)

In **[!UICONTROL Nome relazione dallo schema corrente]** e **[!UICONTROL Nome relazione dallo schema di riferimento]**, fornire rispettivamente nomi descrittivi per la relazione nel contesto degli schemi di origine e di destinazione. Al termine, selezionare **[!UICONTROL Salva]** per applicare le modifiche e salvare lo schema.

![Nome relazione](../images/tutorials/relationship-b2b/relationship-name.png)

L’area di lavoro viene visualizzata nuovamente, con il campo di relazione ora contrassegnato con il nome descrittivo fornito in precedenza. Il nome della relazione viene elencato anche nella barra a sinistra per un riferimento semplice.

![Relazione applicata](../images/tutorials/relationship-b2b/relationship-applied.png)

Se si visualizza la struttura dello schema di destinazione, il marcatore di relazione viene visualizzato accanto al campo di identità principale dello schema e nella barra a sinistra.

![Marcatore di relazione schema di destinazione](../images/tutorials/relationship-b2b/destination-relationship.png)

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente una relazione molti-a-uno tra due schemi utilizzando il tag [!DNL Schema Editor]. Una volta acquisiti i dati utilizzando set di dati basati su questi schemi e attivati nell’archivio dati Profilo, puoi utilizzare gli attributi di entrambi gli schemi per i casi di utilizzo della segmentazione multiclasse. Per ulteriori informazioni, consulta la documentazione su Real-time CDP B2B Edition .
