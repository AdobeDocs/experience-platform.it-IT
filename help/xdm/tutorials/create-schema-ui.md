---
keywords: Experience Platform;home;popular topics;schema;Schema;create schema;enum;XDM individual profile;primary identity;primary idenity;enum datatype;schema design
solution: Experience Platform
title: Creare uno schema tramite l’Editor di schema.
topic: tutorials
description: Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l'Editor di schema all'interno  Experience Platform.
translation-type: tm+mt
source-git-commit: ed100e2acfcfc3dfabef6ccfbe88e98489193567
workflow-type: tm+mt
source-wordcount: '3313'
ht-degree: 0%

---


# Creazione di uno schema con l&#39;operatore [!DNL Schema Editor]

L’interfaccia utente di Adobe Experience Platform consente di creare e gestire schemi [!DNL Experience Data Model] (XDM) in un quadro visivo interattivo denominato [!DNL Schema Editor]. Questa esercitazione illustra come creare uno schema utilizzando l&#39; [!DNL Schema Editor].

>[!NOTE]
>
>A scopo dimostrativo, i passaggi di questa esercitazione includono la creazione di uno schema di esempio che descrive i membri di un programma di fidelizzazione dei clienti. Sebbene sia possibile utilizzare questi passaggi per creare uno schema diverso per scopi propri, è consigliabile seguire la creazione dello schema di esempio per apprendere le funzionalità di tale [!DNL Schema Editor].

Se invece si preferisce comporre uno schema utilizzando l&#39; [!DNL Schema Registry] API, iniziare leggendo la guida [[!DNL Schema Registry] per](../api/getting-started.md) gli sviluppatori prima di tentare l&#39;esercitazione sulla [creazione di uno schema tramite l&#39;API](create-schema-api.md).

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari aspetti di Adobe Experience Platform coinvolti nella creazione dello schema. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti concetti:

* [!DNL Experience Data Model (XDM)](../home.md): Il framework standard con cui [!DNL Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Panoramica degli schemi XDM e dei relativi blocchi costitutivi, incluse classi, mixin, tipi di dati e campi.
* [!DNL Real-time Customer Profile](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Sfogliare gli schemi esistenti nell’ [!UICONTROL Schemas] area di lavoro {#browse}

L’ [!UICONTROL Schemas] area di lavoro nell’ [!DNL Platform] interfaccia utente fornisce una visualizzazione dell’area di lavoro, [!DNL Schema Library]che consente di visualizzare la gestione degli schemi disponibili per l’organizzazione. L&#39;area di lavoro include anche l&#39;area di lavoro [!DNL Schema Editor], l&#39;area di lavoro su cui è possibile comporre uno schema durante l&#39;esercitazione.

Dopo aver effettuato l’accesso, [!DNL Experience Platform]selezionate **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l’ **[!UICONTROL Schemas]** area di lavoro. Nella **[!UICONTROL Browse]** scheda viene visualizzato un elenco di schemi (una rappresentazione dell&#39;oggetto [!DNL Schema Library]) che è possibile visualizzare e personalizzare. L&#39;elenco include il nome, il tipo, la classe e il comportamento (record o serie temporali) su cui si basa lo schema, nonché la data e l&#39;ora dell&#39;ultima modifica dello schema.

Selezionate l’icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per tutte le risorse del Registro di sistema, incluse classi, mixin e tipi di dati. Potete inoltre filtrare le risorse in base al fatto che siano di proprietà  Adobe o dell’organizzazione e che siano state abilitate per l’uso in [!DNL Real-time Customer Profile].

![](../images/tutorials/create-schema/schemas_filter.png)

## Creare e assegnare un nome a uno schema {#create}

Per iniziare a comporre uno schema, selezionare **[!UICONTROL Create Schema]** nell&#39;angolo superiore destro dell&#39; **[!UICONTROL Schemas]** area di lavoro. Viene visualizzato un menu a discesa che consente di scegliere tra le classi principali [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent], oppure di sfogliare altre classi disponibili. Ai fini di questa esercitazione, selezionare **[!UICONTROL XDM Individual Profile]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Viene [!DNL Schema Editor] visualizzata la finestra. Questo è il quadro su cui si compone lo schema. Quando si arriva all&#39;editor, nella **[!UICONTROL Structure]** sezione del quadro viene automaticamente creato uno schema senza titolo, insieme ai campi standard inclusi in tutti gli schemi basati sulla [!UICONTROL XDM Individual Profile] classe. La classe assegnata per lo schema è elencata in **[!UICONTROL Class]** nella sezione **[!UICONTROL Composition]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>È possibile [modificare la classe di uno schema](#change-class) in qualsiasi momento durante il processo di composizione iniziale prima che lo schema sia stato salvato, ma questo deve essere fatto con estrema cautela. I mixin sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà il quadro e tutti i campi aggiunti.

Utilizzare i campi a destra dell&#39;editor per fornire un nome visualizzato e una descrizione facoltativa per lo schema. Una volta inserito un nome, il quadro si aggiorna per riflettere il nuovo nome dello schema.

![](../images/tutorials/create-schema/name_schema.png)

Quando si decide un nome per lo schema, è necessario tenere presenti diverse considerazioni importanti:

* I nomi dello schema devono essere brevi e descrittivi in modo che lo schema possa essere facilmente trovato in un secondo momento.
* I nomi degli schemi devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro. Ad esempio, se l&#39;organizzazione dispone di programmi di fedeltà separati per marchi diversi, sarebbe opportuno assegnare al proprio schema il nome &quot;Marca A Fedeltà Membri&quot; in modo da distinguere facilmente gli altri schemi di fedeltà che si potrebbero definire in seguito.
* È inoltre possibile utilizzare la descrizione dello schema per fornire eventuali informazioni contestuali aggiuntive relative allo schema.

Questa esercitazione costituisce uno schema per l&#39;acquisizione di dati relativi ai membri di un programma fedeltà, pertanto lo schema è denominato &quot;Membri fedeltà&quot;.

## Aggiungere un mixin {#mixin}

È ora possibile iniziare ad aggiungere campi allo schema aggiungendo mixin. Un mixin è un gruppo di uno o più campi spesso utilizzati insieme per descrivere un concetto particolare. Questa esercitazione utilizza i mixin per descrivere i membri del programma fedeltà e acquisire informazioni chiave come nome, compleanno, numero di telefono, indirizzo e molto altro.

Per aggiungere un mixin, selezionate **[!UICONTROL Add]** nella **[!UICONTROL Mixins]** sottosezione.

![](../images/tutorials/create-schema/add_mixin_button.png)

Viene visualizzata una nuova finestra di dialogo con un elenco dei mixin disponibili. Ciascun mixin è destinato solo a una classe specifica, pertanto nella finestra di dialogo sono elencati solo i mixin compatibili con la classe selezionata (in questo caso, la [!DNL XDM Individual Profile] classe).

Selezionando un mixin dall’elenco, questo viene visualizzato nella barra a destra. Inoltre, sul lato destro del mixin selezionato viene visualizzata un’icona che consente di visualizzare in anteprima la struttura dei campi disponibili. Selezionate il **[!UICONTROL Profile Person Details]** mixin, quindi selezionate **[!UICONTROL Add Mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Lo schema quadro viene nuovamente visualizzato. La **[!UICONTROL Mixins]** sezione ora elenca &quot;[!UICONTROL Profile Person Details]&quot; e la **[!UICONTROL Structure]** sezione include i campi che hanno contribuito al mixin. Potete selezionare il nome del mixin sotto alla **[!UICONTROL Mixins]** sezione per evidenziare i campi specifici che fornisce all&#39;interno del quadro.

![](../images/tutorials/create-schema/person_details_structure.png)

Questo mixin fornisce diversi campi sotto il nome di primo livello &quot;[!UICONTROL person]&quot; con il tipo di dati &quot;[!UICONTROL Person]&quot;. Questo gruppo di campi descrive informazioni su un individuo, quali nome, data di nascita e genere.

>[!NOTE]
>
>Tenere presente che i campi possono utilizzare tipi scalari (come stringa, integer, array o data), nonché qualsiasi tipo di dati (un gruppo di campi che rappresenta un concetto comune) definito all&#39;interno del [!DNL Schema Registry].

Il campo &quot;[!UICONTROL name]&quot; ha un tipo di dati &quot;[!UICONTROL Full name]&quot;, il che significa che descrive anche un concetto comune e contiene campi secondari relativi al nome come nome, cognome, titolo di cortesia e suffisso.

Selezionare i diversi campi all&#39;interno del quadro per visualizzare tutti i campi aggiuntivi che contribuiscono alla struttura dello schema.

## Aggiungere un altro mixin {#mixin-2}

Ora potete ripetere gli stessi passaggi per aggiungere un altro mixin. Quando visualizzate la **[!UICONTROL Add Mixin]** finestra di dialogo, il mixin &quot;[!UICONTROL Profile Person Details]&quot; è stato disattivato e il pulsante di scelta accanto non può essere selezionato. Ciò impedisce la duplicazione accidentale di mixin già inclusi nello schema corrente.

Ora è possibile aggiungere &quot;[!DNL Profile Personal Details" mixin] dalla finestra di dialogo.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Una volta aggiunto, il quadro viene nuovamente visualizzato. &quot;[!UICONTROL Profile Personal Details]&quot; è ora elencato **[!UICONTROL Mixins]** nella **[!UICONTROL Composition]** sezione e i campi per l&#39;indirizzo della casa, il telefono cellulare e altro ancora sono stati aggiunti in **[!UICONTROL Structure]**.

Simili al campo &quot;[!UICONTROL name]&quot;, i campi appena aggiunti rappresentano concetti relativi a più campi. Ad esempio, &quot;[!UICONTROL homeAddress]&quot; ha un tipo di dati &quot;[!UICONTROL Address]&quot; e &quot;[!UICONTROL mobilePhone]&quot; ha un tipo di dati &quot;[!UICONTROL Phone Number]&quot;. È possibile selezionare ciascuno di questi campi per espanderli e visualizzare i campi aggiuntivi inclusi nel tipo di dati.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definire un nuovo mixin {#define-mixin}

Lo schema &quot;[!UICONTROL Loyalty Members]&quot; è concepito per acquisire dati relativi ai membri di un programma fedeltà, pertanto richiederà alcuni campi specifici relativi alla fedeltà. Non sono disponibili mixin standard che contengono i campi necessari, pertanto sarà necessario definire un nuovo mixin.

Questa volta, quando aprite la *[!UICONTROL Add Mixin]* finestra di dialogo, selezionate **[!UICONTROL Create New Mixin]**. Vi verrà quindi chiesto di fornire un **[!UICONTROL Display Name]** e **[!UICONTROL Description]** per il vostro mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Come per i nomi delle classi, il nome del mixin deve essere breve e semplice, descrivendo il contributo del mixin allo schema. Anche questi sono univoci, quindi non sarà possibile riutilizzare il nome e quindi dovrà essere sicuro che sia sufficientemente specifico.

Per questa esercitazione, denominate il nuovo mixin &quot;[!UICONTROL Loyalty Details]&quot;.

Selezionare **[!UICONTROL Add Mixin]** per tornare al [!DNL Schema Editor]. &quot;[!UICONTROL Loyalty Details]&quot; dovrebbe ora apparire sotto **[!UICONTROL Mixins]** il lato sinistro del quadro, ma non ci sono campi associati ad esso ancora e quindi non ci sono nuovi campi sotto **[!UICONTROL Structure]**.

## Aggiunta di campi al mixin {#mixin-fields}

Dopo aver creato il mixin &quot;[!UICONTROL Loyalty Details]&quot;, è ora di definire i campi che il mixin contribuirà allo schema.

Per iniziare, selezionate il nome del mixin nella **[!UICONTROL Mixins]** sezione. A questo scopo, le proprietà del mixin vengono visualizzate sul lato destro dell&#39;editor e viene visualizzato un **[!UICONTROL Add Field]** pulsante accanto al nome dello schema sotto **[!UICONTROL Structure]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Selezionare **[!UICONTROL Add Field]** accanto a &quot;[!DNL Loyalty Members]&quot; per creare un nuovo nodo nella struttura. Questo nodo (denominato &quot;_tenantId&quot; in questo esempio) rappresenta l&#39;ID tenant dell&#39;organizzazione IMS, preceduto da un carattere di sottolineatura. La presenza dell&#39;ID tenant indica che i campi che si sta aggiungendo sono contenuti nello spazio dei nomi dell&#39;organizzazione.

In altre parole, i campi che state aggiungendo sono univoci per la vostra organizzazione e verranno salvati in [!DNL Schema Registry] un&#39;area specifica accessibile solo alla vostra organizzazione. I campi definiti devono sempre essere aggiunti allo spazio nomi tenant per evitare conflitti con nomi di altre classi, mixin, tipi di dati e campi standard.

All&#39;interno di quel nodo con nome è presente un &quot;[!UICONTROL New Field]&quot;. Questo è l&#39;inizio del mixin &quot;[!UICONTROL Loyalty Details]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Utilizzando i controlli a destra dell’editor, potete iniziare creando un campo &quot;[!DNL loyalty]&quot; con il tipo &quot;[!UICONTROL Object]&quot; che verrà utilizzato per contenere i campi relativi alla fidelizzazione. Al termine, selezionate **[!UICONTROL Apply]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Le modifiche vengono applicate e viene visualizzato l&#39;oggetto &quot;[!DNL loyalty]&quot; appena creato. Selezionate **[!UICONTROL Add Field]** accanto all’oggetto per aggiungere altri campi relativi alla fedeltà. Viene visualizzato un &quot;[!UICONTROL New Field]&quot; e la **[!UICONTROL Field Properties]** sezione è visibile sul lato destro del quadro.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Ogni campo richiede le seguenti informazioni:

* **[!UICONTROL Field Name]:** Nome del campo, scritto in cammello. Esempio: loyaltyLevel
* **[!UICONTROL Display Name]:** Il nome del campo, scritto nel caso del titolo. Esempio: Livello fedeltà
* **[!UICONTROL Type]:** Il tipo di dati del campo. Ciò include i tipi scalari di base e qualsiasi tipo di dati definito nel [!DNL Schema Registry]. Esempi: [!UICONTROL string], [!UICONTROL integer], [!UICONTROL boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone Number]ecc.
* **[!UICONTROL Description]:** Una descrizione facoltativa del campo deve essere inclusa, scritta in caso di frase, con un massimo di 200 caratteri.

Il primo campo dell&#39; [!DNL Loyalty] oggetto sarà una stringa denominata &quot;[!DNL loyaltyId]&quot;. Quando si imposta il tipo di nuovo campo su &quot;[!UICONTROL String]&quot;, la **[!UICONTROL Field Properties]** sezione viene compilata con diverse opzioni per l&#39;applicazione di vincoli, inclusi **[!UICONTROL Default Value]**, **[!UICONTROL Format]** e **[!UICONTROL Maximum Length]**.

![](../images/tutorials/create-schema/string_constraints.png)

Sono disponibili diverse opzioni di vincolo a seconda del tipo di dati selezionato. Poiché &quot;[!DNL loyaltyId]&quot; sarà un indirizzo e-mail, selezionate &quot;[!UICONTROL email]&quot; dal menu a **[!UICONTROL Format]** discesa. Selezionate **[!UICONTROL Apply]** per applicare le modifiche.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Aggiunta di altri campi al mixin {#mixin-fields-2}

Ora che avete aggiunto il campo &quot;[!DNL loyaltyId]&quot;, potete aggiungere altri campi per acquisire informazioni relative alla fedeltà, ad esempio:

* Points (integer)
* Member-from (data)

Ogni campo viene aggiunto selezionando **[!UICONTROL Add Field]** l&#39;oggetto fedeltà e compilando le informazioni richieste.

Una volta completato, l&#39;oggetto Fedeltà conterrà campi per ID fedeltà, punti e membro da.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Aggiungere un campo enum al mixin {#enum}

Durante la definizione dei campi in [!DNL Schema Editor], è possibile applicare alcune opzioni aggiuntive ai tipi di campo di base per fornire ulteriori vincoli sui dati che il campo può contenere. I casi di utilizzo di questi vincoli sono illustrati nella tabella seguente:

| Vincolo | Descrizione |
| --- | --- |
| [!UICONTROL Required] | Indica che il campo è obbligatorio per l&#39;inserimento dei dati. Eventuali dati caricati in un dataset basato su questo schema che non contiene questo campo avranno esito negativo al momento dell&#39;inserimento. |
| [!UICONTROL Array] | Indica che il campo contiene un array di valori, ciascuno con il tipo di dati specificato. Ad esempio, se si utilizza questo vincolo su un campo con un tipo di dati &quot;[!UICONTROL String]&quot;, il campo conterrà un array di stringhe. |
| [!UICONTROL Enum] | Indica che questo campo deve contenere uno dei valori di un elenco enumerato di possibili valori. |
| [!UICONTROL Identity] | Indica che questo campo è un campo identità. Ulteriori informazioni sui campi di identità sono disponibili [più avanti in questa esercitazione](#identity-field). |
| [!UICONTROL Relationship] | Sebbene sia possibile dedurre le relazioni dello schema utilizzando lo schema unione e [!DNL Real-time Customer Profile], ciò vale solo per gli schemi che condividono la stessa classe. Il [!UICONTROL Relationship] vincolo indica che questo campo fa riferimento all&#39;identità primaria di uno schema basato su una classe diversa, implicando una relazione tra i due schemi. Per ulteriori informazioni, consulta l’esercitazione sulla [definizione di una relazione](./relationship-ui.md) . |

Per questa esercitazione, l&#39; [!DNL "loyalty"] oggetto nello schema richiede un nuovo campo enum che descrive il &quot;livello di fedeltà&quot; di un cliente, dove il valore può essere solo una delle quattro opzioni possibili. Per aggiungere questo campo allo schema, selezionare **[!UICONTROL Add Field]** accanto all&#39;oggetto &quot;[!DNL loyalty]&quot; e compilare i campi obbligatori per **[!UICONTROL Field name]** e **[!UICONTROL Display name]**. Per **[!UICONTROL Type]**, seleziona &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Dopo che è stato selezionato il tipo, vengono visualizzate ulteriori caselle di controllo per il campo, comprese quelle per **[!UICONTROL Array]**, **[!UICONTROL Enum]** e **[!UICONTROL Identity]**.

Selezionare la **[!UICONTROL Enum]** casella di controllo per aprire la **[!UICONTROL Enum values]** sezione sottostante. Qui è possibile inserire il **[!UICONTROL Value]** (in camelCase) e **[!UICONTROL Label]** (un nome opzionale, intuitivo per il lettore in Case Titolo) per ogni livello di fedeltà accettabile.

Una volta completate tutte le proprietà del campo, selezionare **[!UICONTROL Apply]** per aggiungere il campo &quot;[!DNL loyaltyLevel]&quot; all&#39;oggetto &quot;[!DNL loyalty]&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversione di un oggetto multicampo in un tipo di dati {#datatype}

L&#39;oggetto &quot;[!DNL loyalty]&quot; ora contiene diversi campi specifici per la fedeltà e rappresenta una struttura dati comune che potrebbe essere utile in altri schemi. Questa [!DNL Schema Editor] opzione consente di applicare facilmente oggetti multicampo riutilizzabili convertendo la struttura di tali oggetti in tipi di dati.

I tipi di dati consentono l&#39;uso coerente di strutture con più campi e offrono maggiore flessibilità rispetto a un mixin, perché possono essere utilizzati ovunque all&#39;interno di uno schema. A tal fine, è possibile impostare il **[!UICONTROL Type]** valore del campo su quello di qualsiasi tipo di dati definito nel [!DNL Schema Registry].

Per convertire l&#39;oggetto &quot;[!DNL loyalty]&quot; in un tipo di dati, selezionare il campo &quot;[!DNL loyalty]&quot; in **[!UICONTROL Structure]**, quindi selezionare **[!UICONTROL Convert to new data type]** sul lato destro dell&#39;editor sotto **[!UICONTROL Field Properties]**. Viene visualizzato un puntatore verde che conferma la corretta conversione dell’oggetto.

![](../images/tutorials/create-schema/convert-data-type.png)

Ora, quando si guarda sotto, **[!UICONTROL Structure]** si può vedere che il campo &quot;[!DNL loyalty]&quot; ha un tipo di dati &quot;[!DNL Loyalty]&quot; e i campi hanno icone di blocco piccole accanto a essi, a indicare che non sono più campi singoli ma fanno parte di un tipo di dati multicampo.

![](../images/tutorials/create-schema/loyalty_data_type.png)

In uno schema futuro, ora è possibile assegnare a un campo il **[!UICONTROL Type]** nome di &quot;[!DNL Loyalty]&quot; e includere automaticamente campi per ID, livello fedeltà, membro da e punti.

## Impostare un campo dello schema come campo di identità {#identity-field}

La struttura di dati standard fornita dagli schemi può essere sfruttata per identificare i dati appartenenti allo stesso individuo tra più origini, consentendo l&#39;utilizzo di diversi casi a valle, come segmentazione, reporting, analisi della scienza dei dati e altro ancora. Per unire i dati in base alle singole identità, i campi chiave devono essere contrassegnati come campi &quot;[!UICONTROL Identity]&quot; all’interno degli schemi applicabili.

[!DNL Experience Platform] consente di identificare facilmente un campo identità mediante l&#39;uso di una **[!UICONTROL Identity]** casella di controllo nell&#39; [!DNL Schema Editor]. Tuttavia, è necessario determinare quale campo è il candidato migliore per utilizzare come identità, in base alla natura dei dati.

Ad esempio, ci possono essere migliaia di membri del programma fedeltà appartenenti allo stesso &quot;livello fedeltà&quot;, ma ogni membro del programma fedeltà ha un &quot;[!DNL loyaltyId]&quot; univoco (che in questo caso è l&#39;indirizzo e-mail del singolo membro). Il fatto che &quot;[!DNL loyaltyId]&quot; sia un identificatore univoco per ogni membro lo rende un buon candidato per un campo di identità, mentre il &quot;livello di fedeltà&quot; non lo è.

>[!IMPORTANT]
>
>I passaggi descritti di seguito descrivono come aggiungere un descrittore di identità a un campo dello schema esistente. In alternativa alla definizione dei campi di identità all&#39;interno della struttura dello schema stesso, è possibile utilizzare un `identityMap` campo per contenere le informazioni di identità.
>
>Se si prevede di utilizzare `identityMap`, tenere presente che sostituirà direttamente qualsiasi identità primaria aggiunta allo schema. Per ulteriori informazioni, consulta la sezione `identityMap` in [Nozioni di base sulla composizione](../schema/composition.md#identityMap) dello schema.

Nella **[!UICONTROL Structure]** sezione dell&#39;editor, selezionate il campo &quot;[!DNL loyaltyId]&quot; e la **[!UICONTROL Identity]** casella di controllo appare sotto **[!UICONTROL Field Properties]**. Selezionare la casella e l&#39;opzione per impostare l&#39; **[!UICONTROL Primary Identity]** aspetto. Selezionate anche questa casella.

Successivamente, è necessario fornire un&#39;indicazione **[!UICONTROL Identity Namespace]** dall&#39;elenco degli spazi dei nomi predefiniti nel menu a discesa. Poiché &quot;[!DNL loyaltyId]&quot; è l&#39;indirizzo e-mail del cliente, selezionate &quot;[!UICONTROL Email]&quot; dal menu a discesa. Selezionate **[!UICONTROL Apply]** per confermare gli aggiornamenti al campo &quot;[!DNL loyaltyId]&quot;.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Per un elenco dei namespace standard e delle relative definizioni, consultate la documentazione [del servizio](../../identity-service/troubleshooting-guide.md#standard-namespaces)identità.

Ora tutti i dati inseriti nel campo &quot;[!DNL loyaltyId]&quot; saranno utilizzati per identificare il singolo e unire una singola vista del cliente.

>[!NOTE]
>
>Una volta impostato un campo dello schema come identità principale, si riceverà un messaggio di errore se si tenta in seguito di impostare come principale un altro campo dello schema. Ogni schema può contenere un solo campo identità principale.

Per ulteriori informazioni sull&#39;utilizzo delle identità in [!DNL Experience Platform], consulta la [!DNL Identity Service](../../identity-service/home.md) documentazione.

## Abilita lo schema da utilizzare in [!DNL Real-time Customer Profile] {#profile}

[!DNL Real-time Customer Profile](../../profile/home.md) sfrutta i dati di identità [!DNL Experience Platform] per fornire una visione olistica di ciascun cliente. Il servizio crea solidi profili a 360° degli attributi del cliente e account con marca temporale di ogni interazione che i clienti hanno avuto in tutti i sistemi integrati con [!DNL Experience Platform].

Affinché uno schema possa essere abilitato per l&#39;uso con [!DNL Real-time Customer Profile], è necessario che sia definita un&#39;identità primaria. Se si tenta di abilitare uno schema senza prima definire un&#39;identità primaria, verrà visualizzato un messaggio di errore.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Per attivare lo schema &quot;Membri fedeltà&quot; da utilizzare in [!DNL Profile], iniziare selezionando &quot;[!DNL Loyalty Members]&quot; nella **[!UICONTROL Structure]** sezione dell&#39;editor.

Sul lato destro dell&#39;editor, vengono visualizzate informazioni sullo schema, incluso il nome visualizzato, la descrizione e il tipo. Oltre a queste informazioni, è disponibile un pulsante di **[!UICONTROL Profile]** attivazione/disattivazione.

![](../images/tutorials/create-schema/profile-toggle.png)

Selezionare **[!UICONTROL Profile]** e viene visualizzato un puntatore che richiede di confermare l&#39;abilitazione dello schema per [!DNL Profile].

![](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>Una volta che uno schema è stato abilitato [!DNL Real-time Customer Profile] e salvato, non può essere disabilitato.

Selezionate **[!UICONTROL Enable]** per confermare la scelta. È possibile selezionare di nuovo l&#39; **[!UICONTROL Profile]** interruttore per disabilitare lo schema, se lo si desidera, ma una volta che lo schema è stato salvato mentre [!DNL Profile] è abilitato, non può più essere disabilitato.

## Passaggi successivi e risorse aggiuntive

Dopo aver completato la composizione di uno schema &quot;Membri fedeltà&quot;, è possibile visualizzare lo schema completo nel quadro. Selezionare **[!UICONTROL Save]** e lo schema verrà salvato nel [!DNL Schema Library], rendendolo accessibile dal [!DNL Schema Registry].

È ora possibile utilizzare il nuovo schema per acquisire i dati in [!DNL Platform]. Tenere presente che una volta che lo schema è stato utilizzato per acquisire i dati, è possibile apportare solo modifiche aggiuntive. Per ulteriori informazioni sul controllo delle versioni dello schema, vedere le [nozioni di base della composizione](../schema/composition.md) dello schema.

È ora possibile seguire l&#39;esercitazione sulla [definizione di una relazione di schema nell&#39;interfaccia utente](./relationship-ui.md) per aggiungere un nuovo campo di relazione allo schema &quot;Membri fedeltà&quot;.

Lo schema &quot;Membri fedeltà&quot; è disponibile anche per la visualizzazione e la gestione tramite l&#39; [!DNL Schema Registry] API. Per iniziare a lavorare con l&#39;API, leggete la guida [[!DNL Schema Registry API] ](../api/getting-started.md)per gli sviluppatori.

### Risorse video

>[!WARNING]
>
>L’ [!DNL Platform] interfaccia utente mostrata nei video seguenti è obsoleta. Per informazioni sulle ultime funzionalità e videate dell’interfaccia, consulta la documentazione precedente.

Il video seguente mostra come creare uno schema semplice nell’ [!DNL Platform] interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

Il seguente video è pensato per comprendere meglio come utilizzare mixin e classi.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive relative all&#39;utilizzo dell&#39; [!DNL Schema Editor].

### Create a new class {#create-new-class}

[!DNL Experience Platform] consente di definire uno schema basato su una classe univoca per l&#39;organizzazione.

Nell’ **[!UICONTROL Schemas]** area di lavoro, selezionate **[!UICONTROL Create schema]**, quindi selezionate **[!UICONTROL Browse]** dal menu a discesa.

![](../images/tutorials/create-schema/browse-classes.png)

Viene visualizzata una finestra di dialogo che consente di selezionare da un elenco di classi disponibili. Nella parte superiore della finestra di dialogo, selezionare **[!UICONTROL Create New Class]**. È quindi possibile assegnare alla nuova classe un nome **[!UICONTROL Display Name]** (breve, descrittivo, univoco e di facile utilizzo per la classe), un nome **[!UICONTROL Description]** e un **[!UICONTROL Behavior]** (&quot;[!UICONTROL Record]&quot; o &quot;[!UICONTROL Time Series]&quot;) per i dati che lo schema definirà.

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>Durante la creazione di uno schema che implementa una classe definita dall&#39;organizzazione, tenere presente che i mixin sono disponibili solo per le classi compatibili. Poiché la classe definita è nuova, nella finestra di dialogo *Aggiungi mixin* non sono presenti mixin compatibili. Al contrario, sarà necessario selezionare **[!UICONTROL Create New Mixin]** e definire un mixin da utilizzare con tale classe. Al successivo comporre uno schema che implementa la nuova classe, il mixin definito verrà elencato e sarà disponibile per l&#39;uso.

### Modificare la classe di uno schema {#change-class}

È possibile modificare la classe di uno schema in qualsiasi punto del processo di composizione iniziale prima che lo schema sia stato salvato.

>[!WARNING]
>
>La riassegnazione della classe per uno schema deve essere eseguita con estrema cautela. I mixin sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà il quadro e tutti i campi aggiunti.

Per riassegnare una classe, selezionate **[!UICONTROL Assign]** nella parte sinistra del quadro.

![](../images/tutorials/create-schema/assign_class_button.png)

Viene visualizzata una finestra di dialogo in cui sono elencate tutte le classi disponibili, incluse quelle definite dall&#39;organizzazione (il proprietario è &quot;[!UICONTROL Customer]&quot;) e le classi standard definite dal Adobe .

Selezionate una classe dall’elenco per visualizzarne la descrizione sul lato destro della finestra di dialogo. Potete anche selezionare **[!UICONTROL Preview Class Structure]** per visualizzare i campi e i metadati associati alla classe. Selezionare **[!UICONTROL Assign class]** per continuare.

![](../images/tutorials/create-schema/assign_class.png)

Viene visualizzata una nuova finestra di dialogo in cui viene richiesto di confermare l&#39;assegnazione di una nuova classe. Selezionare **[!UICONTROL Assign]** per confermare.

![](../images/tutorials/create-schema/assign-confirm.png)

Dopo aver confermato la modifica della classe, il quadro verrà reimpostato e tutti i progressi della composizione andranno persi.