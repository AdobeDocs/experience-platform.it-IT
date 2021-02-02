---
keywords: ' Experience Platform;home;argomenti più diffusi;ui;interfaccia utente;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;editor schema;Editor schema;schema;schemi;schemi;creare'
solution: Experience Platform
title: Creare uno schema tramite l’Editor di schema
topic: tutorial
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per creare uno schema utilizzando Schema Editor all’interno di Experience Platform.
translation-type: tm+mt
source-git-commit: e5c5fea783aa4088d225f771905fa8b2098613cf
workflow-type: tm+mt
source-wordcount: '3455'
ht-degree: 0%

---


# Creare uno schema utilizzando la variabile [!DNL Schema Editor]

L&#39;interfaccia utente di Adobe Experience Platform consente di creare e gestire gli schemi [!DNL Experience Data Model] (XDM) in un&#39;area di lavoro visiva interattiva denominata [!DNL Schema Editor]. Questa esercitazione illustra come creare uno schema utilizzando [!DNL Schema Editor].

>[!NOTE]
>
>A scopo dimostrativo, i passaggi di questa esercitazione includono la creazione di uno schema di esempio che descrive i membri di un programma di fidelizzazione dei clienti. Sebbene sia possibile utilizzare questi passaggi per creare uno schema diverso per scopi propri, è consigliabile seguire la creazione dello schema di esempio per apprendere le funzionalità di [!DNL Schema Editor].

Se invece si preferisce comporre uno schema utilizzando l&#39;API [!DNL Schema Registry], iniziare leggendo la [[!DNL Schema Registry] guida allo sviluppatore](../api/getting-started.md) prima di provare l&#39;esercitazione su [creazione di uno schema mediante l&#39;API](create-schema-api.md).

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari aspetti di Adobe Experience Platform coinvolti nella creazione dello schema. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti concetti:

* [[!DNL Experience Data Model (XDM)]](../home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../schema/composition.md) dello schema: Panoramica degli schemi XDM e dei relativi blocchi costitutivi, incluse classi, mixin, tipi di dati e campi.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Aprire l&#39;area di lavoro [!UICONTROL Schemas] {#browse}

L&#39;area di lavoro di [!UICONTROL Schemas] nell&#39;interfaccia di [!DNL Platform] fornisce una visualizzazione di [!DNL Schema Library], consentendo di visualizzare la gestione degli schemi disponibili per la propria organizzazione. L&#39;area di lavoro include anche il [!DNL Schema Editor], il quadro su cui è possibile comporre uno schema durante l&#39;esercitazione.

Dopo aver eseguito l&#39;accesso a [!DNL Experience Platform], selezionare **[!UICONTROL Schemas]** nella barra di navigazione a sinistra per aprire l&#39;area di lavoro **[!UICONTROL Schemas]**. Nella scheda **[!UICONTROL Browse]** è visualizzato un elenco di schemi (una rappresentazione di [!DNL Schema Library]) che è possibile visualizzare e personalizzare. L&#39;elenco include il nome, il tipo, la classe e il comportamento (record o serie temporali) su cui si basa lo schema, nonché la data e l&#39;ora dell&#39;ultima modifica dello schema.

Per ulteriori informazioni, consulta la guida [Esplora risorse XDM esistenti nell&#39;interfaccia utente](../ui/explore.md).

## Creare e assegnare un nome a uno schema {#create}

Per iniziare a comporre uno schema, selezionare **[!UICONTROL Create schema]** nell&#39;angolo superiore destro dell&#39;area di lavoro **[!UICONTROL Schemas]**. Viene visualizzato un menu a discesa che consente di scegliere tra le classi [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent] di base. Se queste classi non sono adatte alle vostre esigenze, potete anche selezionare **[!UICONTROL Browse]** per scegliere tra le altre classi disponibili o [creare una nuova classe](#create-new-class).

Ai fini di questa esercitazione, selezionare **[!UICONTROL XDM Individual Profile]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Viene visualizzato il simbolo [!DNL Schema Editor]. Questo è il quadro su cui si compone lo schema. Poiché è stata scelta una classe XDM standard su cui basare lo schema, quando si arriva nell&#39;editor viene automaticamente creato uno schema senza titolo nella sezione **[!UICONTROL Structure]** del quadro, insieme ai campi standard inclusi in tutti gli schemi basati su tale classe. La classe assegnata per lo schema è elencata anche in **[!UICONTROL Class]** nella sezione **[!UICONTROL Composition]**.

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>È possibile [modificare la classe di uno schema](#change-class) in qualsiasi momento durante il processo di composizione iniziale prima che lo schema sia stato salvato, ma questo deve essere fatto con estrema cautela. I mixin sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà il quadro e tutti i campi aggiunti.

Utilizzare i campi a destra dell&#39;editor per fornire un nome visualizzato e una descrizione facoltativa per lo schema. Una volta inserito un nome, il quadro si aggiorna per riflettere il nuovo nome dello schema.

![](../images/tutorials/create-schema/name_schema.png)

Quando si decide un nome per lo schema, è necessario tenere presenti diverse considerazioni importanti:

* I nomi dello schema devono essere brevi e descrittivi in modo che lo schema possa essere facilmente trovato in un secondo momento.
* I nomi degli schemi devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro. Se, ad esempio, l&#39;organizzazione dispone di programmi di fedeltà separati per marchi diversi, sarebbe opportuno assegnare al proprio schema il nome &quot;Marca A Fedeltà Members&quot;, in modo da distinguere facilmente gli altri schemi di fedeltà definiti in seguito.
* È inoltre possibile utilizzare la descrizione dello schema per fornire eventuali informazioni contestuali aggiuntive relative allo schema.

Questa esercitazione costituisce uno schema per l&#39;acquisizione di dati relativi ai membri di un programma fedeltà, pertanto lo schema è denominato &quot;Membri fedeltà&quot;.

## Aggiungere un mixin {#mixin}

È ora possibile iniziare ad aggiungere campi allo schema aggiungendo mixin. Un mixin è un gruppo di uno o più campi spesso utilizzati insieme per descrivere un concetto particolare. Questa esercitazione utilizza i mixin per descrivere i membri del programma fedeltà e acquisire informazioni chiave come nome, compleanno, numero di telefono, indirizzo e molto altro.

Per aggiungere un mixin, selezionare **[!UICONTROL Add]** nella sottosezione **[!UICONTROL Mixins]**.

![](../images/tutorials/create-schema/add_mixin_button.png)

Viene visualizzata una nuova finestra di dialogo con un elenco dei mixin disponibili. Ciascun mixin è destinato solo a una classe specifica, pertanto nella finestra di dialogo sono elencati solo i mixin compatibili con la classe selezionata (in questo caso, la classe [!DNL XDM Individual Profile]). Se si utilizza una classe XDM standard, l&#39;elenco dei mixin verrà ordinato in modo intelligente in base alla popolarità dell&#39;utilizzo.

![](../images/tutorials/create-schema/mixin-popularity.png)

Selezionando un mixin dall’elenco, questo viene visualizzato nella barra a destra. Potete selezionare più mixin, se lo desiderate, aggiungendo ognuno all&#39;elenco nella barra a destra prima di confermare. Inoltre, sul lato destro del mixin attualmente selezionato viene visualizzata un’icona che consente di visualizzare in anteprima la struttura dei campi disponibili.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Quando visualizzate l&#39;anteprima di un mixin, nella barra a destra viene fornita una descrizione dettagliata dello schema del mixin. Potete anche scorrere i campi del mixin nel quadro fornito. Selezionando campi diversi, la barra laterale destra si aggiorna per visualizzare i dettagli relativi al campo in questione. Selezionate **[!UICONTROL Back]** al termine dell&#39;anteprima per tornare alla finestra di dialogo di selezione del mixin.

![](../images/tutorials/create-schema/preview-mixin.png)

Per questa esercitazione, selezionate il mixin **[!UICONTROL Demographic Details]**, quindi selezionate **[!UICONTROL Add mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Lo schema quadro viene nuovamente visualizzato. La sezione **[!UICONTROL Mixins]** ora elenca &quot;[!UICONTROL Demographic Details]&quot; e la sezione **[!UICONTROL Structure]** include i campi forniti dal mixin. Potete selezionare il nome del mixin nella sezione **[!UICONTROL Mixins]** per evidenziare i campi specifici che fornisce all&#39;interno del quadro.

![](../images/tutorials/create-schema/person_details_structure.png)

Questo mixin fornisce diversi campi sotto il nome di livello principale `person` con il tipo di dati &quot;[!UICONTROL Person]&quot;. Questo gruppo di campi descrive informazioni su un individuo, quali nome, data di nascita e genere.

>[!NOTE]
>
>Tenere presente che i campi possono utilizzare tipi scalari (ad esempio stringa, integer, array o data), nonché qualsiasi tipo di dati (un gruppo di campi che rappresenta un concetto comune) definito all&#39;interno di [!DNL Schema Registry].

Tenere presente che il campo `name` ha un tipo di dati &quot;[!UICONTROL Person name]&quot;, il che significa che descrive anche un concetto comune e contiene campi secondari relativi al nome come nome, cognome, titolo di cortesia e suffisso.

Selezionare i diversi campi all&#39;interno dell&#39;area di lavoro per visualizzare eventuali altri campi che contribuiscono alla struttura dello schema.

## Aggiungere un altro mixin {#mixin-2}

Ora potete ripetere gli stessi passaggi per aggiungere un altro mixin. Quando visualizzate la finestra di dialogo **[!UICONTROL Add mixin]**, il mixin &quot;[!UICONTROL Demographic Details]&quot; è stato disattivato e non è possibile selezionare la casella di controllo accanto. Ciò impedisce la duplicazione accidentale di mixin già inclusi nello schema corrente.

Per questa esercitazione, selezionate il mixin &quot;[!DNL Personal Contact Details]&quot; dalla finestra di dialogo, quindi selezionate **[!UICONTROL Add mixin]** per aggiungerlo allo schema.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Una volta aggiunto, il quadro viene nuovamente visualizzato. &quot;[!UICONTROL Personal Contact Details]&quot; è ora elencato in **[!UICONTROL Mixins]** nella sezione **[!UICONTROL Composition]** e i campi per l&#39;indirizzo della casa, il telefono cellulare e altro ancora sono stati aggiunti in **[!UICONTROL Structure]**.

Analogamente al campo `name`, i campi appena aggiunti rappresentano concetti relativi a più campi. Ad esempio, `homeAddress` ha un tipo di dati &quot;[!UICONTROL Postal address]&quot; e `mobilePhone` ha un tipo di dati &quot;[!UICONTROL Phone number]&quot;. È possibile selezionare ciascuno di questi campi per espanderli e visualizzare i campi aggiuntivi inclusi nel tipo di dati.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definire un nuovo mixin {#define-mixin}

Lo schema &quot;[!UICONTROL Loyalty Members]&quot; è concepito per acquisire dati relativi ai membri di un programma fedeltà, pertanto richiederà alcuni campi specifici relativi alla fedeltà. Non sono disponibili mixin standard che contengono i campi necessari, pertanto sarà necessario definire un nuovo mixin.

Questa volta, quando si apre la finestra di dialogo **[!UICONTROL Add Mixin]**, selezionare **[!UICONTROL Create New Mixin]**. Vi verrà quindi chiesto di fornire un nome visualizzato e una descrizione per il mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Come per i nomi delle classi, il nome del mixin deve essere breve e semplice, descrivendo il contributo del mixin allo schema. Anche questi sono univoci, quindi non sarà possibile riutilizzare il nome e quindi dovrà essere sicuro che sia sufficientemente specifico.

Per questa esercitazione, denominate il nuovo mixin &quot;Dettagli fedeltà&quot;.

Selezionare **[!UICONTROL Add mixin]** per tornare alla cartella [!DNL Schema Editor]. &quot;[!UICONTROL Loyalty Details]&quot; dovrebbe ora apparire sotto **[!UICONTROL Mixins]** sul lato sinistro del quadro, ma non ci sono ancora campi associati ad esso e quindi non ci sono nuovi campi sotto **[!UICONTROL Structure]**.

## Aggiungere campi al mixin {#mixin-fields}

Dopo aver creato il mixin &quot;Dettagli fedeltà&quot;, è ora di definire i campi che il mixin contribuirà allo schema.

Per iniziare, selezionate il nome del mixin nella sezione **[!UICONTROL Mixins]**. A questo punto, le proprietà del mixin vengono visualizzate sul lato destro dell&#39;editor e accanto al nome dello schema in **[!UICONTROL Structure]** viene visualizzata un&#39;icona **più (+)**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Selezionare l&#39;icona **più (+)** accanto a &quot;[!DNL Loyalty Members]&quot; per creare un nuovo nodo nella struttura. Questo nodo (denominato `_tenantId` in questo esempio) rappresenta l&#39;ID tenant dell&#39;organizzazione IMS, preceduto da un carattere di sottolineatura. La presenza dell&#39;ID tenant indica che i campi che si sta aggiungendo sono contenuti nello spazio dei nomi dell&#39;organizzazione.

In altre parole, i campi che state aggiungendo sono univoci per la vostra organizzazione e verranno salvati in [!DNL Schema Registry] in un&#39;area specifica accessibile solo dalla vostra organizzazione. I campi definiti devono sempre essere aggiunti allo spazio nomi tenant per evitare conflitti con nomi di altre classi, mixin, tipi di dati e campi standard.

All&#39;interno di tale nodo con nome è presente un &quot;[!UICONTROL New Field]&quot;. Questo è l&#39;inizio del mixin &quot;[!UICONTROL Loyalty Details]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Utilizzando i controlli a destra dell&#39;editor, si crea innanzitutto un campo `loyalty` con il tipo &quot;[!UICONTROL Object]&quot; che verrà utilizzato per contenere i campi relativi alla fedeltà. Al termine, selezionare **[!UICONTROL Apply]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Le modifiche vengono applicate e viene visualizzato l&#39;oggetto `loyalty` appena creato. Selezionate l&#39;icona **più (+)** accanto all&#39;oggetto per aggiungere altri campi relativi alla fedeltà. Viene visualizzato un &quot;[!UICONTROL New Field]&quot; e la sezione **[!UICONTROL Field properties]** è visibile sul lato destro del quadro.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Ogni campo richiede le seguenti informazioni:

* **[!UICONTROL Field Name]:** Il nome del campo, scritto in cammello. Esempio: loyaltyLevel
* **[!UICONTROL Display Name]:** Il nome del campo, scritto nel caso del titolo. Esempio: Livello fedeltà
* **[!UICONTROL Type]:** Il tipo di dati del campo. Ciò include tipi scalari di base e qualsiasi tipo di dati definito in [!DNL Schema Registry]. Esempi: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone number] ecc.
* **[!UICONTROL Description]:** Una descrizione facoltativa del campo deve essere inclusa, scritta in caso di frase, con un massimo di 200 caratteri.

Il primo campo per l&#39;oggetto `Loyalty` sarà una stringa denominata `loyaltyId`. Quando si imposta il tipo di nuovo campo su &quot;[!UICONTROL String]&quot;, la sezione **[!UICONTROL Field properties]** viene compilata con diverse opzioni per l&#39;applicazione di vincoli, tra cui valori predefiniti, formato e lunghezza massima.

![](../images/tutorials/create-schema/string_constraints.png)

Sono disponibili diverse opzioni di vincolo a seconda del tipo di dati selezionato. Poiché `loyaltyId` sarà un indirizzo e-mail, selezionare &quot;[!UICONTROL email]&quot; dal menu a discesa **[!UICONTROL Format]**. Selezionare **[!UICONTROL Apply]** per applicare le modifiche.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Aggiungete altri campi al mixin {#mixin-fields-2}

Dopo aver aggiunto il campo `loyaltyId`, potete aggiungere altri campi per acquisire informazioni relative alla fedeltà, ad esempio:

* Points (integer)
* Member-from (data)

Per aggiungere ciascun campo allo schema, selezionare l&#39;icona **più (+)** accanto all&#39;oggetto `loyalty` e compilare le informazioni richieste.

Una volta completato, l&#39;oggetto Fedeltà conterrà campi per ID fedeltà, punti e membro da.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Aggiungere un campo enum al mixin {#enum}

Durante la definizione dei campi in [!DNL Schema Editor], è possibile applicare alcune opzioni aggiuntive ai tipi di campo di base al fine di fornire ulteriori limitazioni ai dati che il campo può contenere. I casi di utilizzo di questi vincoli sono illustrati nella tabella seguente:

| Vincolo | Descrizione |
| --- | --- |
| [!UICONTROL Required] | Indica che il campo è obbligatorio per l&#39;inserimento dei dati. Eventuali dati caricati in un dataset basato su questo schema che non contiene questo campo avranno esito negativo al momento dell&#39;inserimento. |
| [!UICONTROL Array] | Indica che il campo contiene un array di valori, ciascuno con il tipo di dati specificato. Ad esempio, se si utilizza questo vincolo su un campo con un tipo di dati &quot;[!UICONTROL String]&quot;, il campo conterrà un array di stringhe. |
| [!UICONTROL Enum] | Indica che questo campo deve contenere uno dei valori di un elenco enumerato di possibili valori. |
| [!UICONTROL Identity] | Indica che questo campo è un campo identità. Ulteriori informazioni sui campi di identità sono fornite [più avanti in questa esercitazione](#identity-field). |
| [!UICONTROL Relationship] | Sebbene sia possibile dedurre le relazioni dello schema utilizzando lo schema unione e [!DNL Real-time Customer Profile], ciò vale solo per gli schemi che condividono la stessa classe. Il vincolo [!UICONTROL Relationship] indica che questo campo fa riferimento all&#39;identità primaria di uno schema basato su una classe diversa, implicando una relazione tra i due schemi. Per ulteriori informazioni, vedere l&#39;esercitazione su [definizione di una relazione](./relationship-ui.md). |

>[!NOTE]
>
>Tutti i campi obbligatori, di identità o di relazione sono visualizzati nella barra a sinistra, consentendo di individuare facilmente tali campi indipendentemente dalla complessità dello schema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Per questa esercitazione, l&#39;oggetto [!DNL "loyalty"] nello schema richiede un nuovo campo enum che descrive il &quot;livello di fedeltà&quot; di un cliente, dove il valore può essere solo una delle quattro opzioni possibili. Per aggiungere questo campo allo schema, selezionare l&#39;icona **plus (+)** accanto all&#39;oggetto `loyalty` e compilare i campi obbligatori per **[!UICONTROL Field name]** e **[!UICONTROL Display name]**. Per **[!UICONTROL Type]**, seleziona &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Dopo che è stato selezionato il tipo, vengono visualizzate ulteriori caselle di controllo per il campo, comprese le caselle di controllo per **[!UICONTROL Array]**, **[!UICONTROL Enum]** e **[!UICONTROL Identity]**.

Selezionare la casella di controllo **[!UICONTROL Enum]** per aprire la sezione **[!UICONTROL Enum values]** sottostante. Qui è possibile inserire i valori **[!UICONTROL Value]** (in camelCase) e **[!UICONTROL Label]** (un nome facoltativo e intuitivo per il lettore in Title Case) per ogni livello di fedeltà accettabile.

Dopo aver completato tutte le proprietà del campo, selezionare **[!UICONTROL Apply]** per aggiungere il campo &quot;[!DNL loyaltyLevel]&quot; all&#39;oggetto `loyalty`.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversione di un oggetto multicampo in un tipo di dati {#datatype}

L&#39;oggetto `loyalty` ora contiene diversi campi specifici per la fedeltà e rappresenta una struttura dati comune che potrebbe essere utile in altri schemi. [!DNL Schema Editor] consente di applicare facilmente oggetti multicampo riutilizzabili convertendo la struttura di tali oggetti in tipi di dati.

I tipi di dati consentono l&#39;uso coerente di strutture con più campi e offrono maggiore flessibilità rispetto a un mixin, perché possono essere utilizzati ovunque all&#39;interno di uno schema. A tal fine, è possibile impostare il valore **[!UICONTROL Type]** del campo su quello di qualsiasi tipo di dati definito in [!DNL Schema Registry].

Per convertire l&#39;oggetto `loyalty` in un tipo di dati, selezionare il campo `loyalty` in **[!UICONTROL Structure]**, quindi selezionare **[!UICONTROL Convert to new data type]** a destra dell&#39;editor in **[!UICONTROL Field properties]**. Viene visualizzato un puntatore verde che conferma la corretta conversione dell’oggetto.

![](../images/tutorials/create-schema/convert-data-type.png)

Ora, quando si guarda in **[!UICONTROL Structure]**, è possibile vedere che il campo `loyalty` ha un tipo di dati &quot;[!DNL Loyalty]&quot; e i campi sono dotati di icone di blocco piccole, a indicare che non sono più campi singoli ma fanno parte di un tipo di dati multicampo.

![](../images/tutorials/create-schema/loyalty_data_type.png)

In uno schema futuro, ora è possibile assegnare un campo come tipo &quot;[!DNL Loyalty]&quot; e includere automaticamente campi per ID, livello fedeltà, membro da e punti.

>[!NOTE]
>
>È inoltre possibile creare e modificare tipi di dati personalizzati indipendentemente dalla modifica degli schemi. Per ulteriori informazioni, consultare la guida relativa alla [creazione e modifica di tipi di dati](../ui/resources/data-types.md).

## Ricerca e filtro di campi dello schema

Lo schema ora contiene diversi mixin oltre ai campi forniti dalla relativa classe base. Quando lavorate con schemi più grandi, potete selezionare le caselle accanto ai nomi dei mixin nella barra a sinistra per filtrare i campi visualizzati solo in base a quelli forniti dai mixin questione.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Se si sta cercando un campo specifico nello schema, è possibile utilizzare la barra di ricerca anche per filtrare i campi visualizzati per nome, indipendentemente dal mixin cui sono forniti.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La funzione di ricerca prende in considerazione tutti i filtri mixin selezionati quando vengono visualizzati i campi corrispondenti. Se una query di ricerca non visualizza i risultati previsti, potrebbe essere necessario verificare due volte che non state filtrando i mixin rilevanti.

## Impostare un campo dello schema come campo di identità {#identity-field}

La struttura di dati standard fornita dagli schemi può essere sfruttata per identificare i dati appartenenti allo stesso individuo tra più origini, consentendo l&#39;utilizzo di diversi casi a valle, come segmentazione, reporting, analisi della scienza dei dati e altro ancora. Per unire i dati in base alle singole identità, i campi chiave devono essere contrassegnati come campi [!UICONTROL Identity] all&#39;interno degli schemi applicabili.

[!DNL Experience Platform] consente di identificare facilmente un campo identità mediante l&#39;uso di una  **[!UICONTROL Identity]** casella di controllo nell&#39; [!DNL Schema Editor]. Tuttavia, è necessario determinare quale campo è il candidato migliore per utilizzare come identità, in base alla natura dei dati.

Ad esempio, ci possono essere migliaia di membri del programma fedeltà appartenenti allo stesso &quot;livello fedeltà&quot;, ma ogni membro del programma fedeltà ha un `loyaltyId` univoco (che in questo caso è l&#39;indirizzo e-mail del singolo membro). Il fatto che `loyaltyId` sia un identificatore univoco per ciascun membro lo rende un valido candidato per un campo di identità, mentre `loyaltyLevel` non lo è.

>[!IMPORTANT]
>
>I passaggi descritti di seguito descrivono come aggiungere un descrittore di identità a un campo dello schema esistente. In alternativa alla definizione dei campi di identità all&#39;interno della struttura dello schema stesso, è anche possibile utilizzare un campo `identityMap` per contenere le informazioni di identità.
>
>Se si prevede di utilizzare `identityMap`, tenere presente che sostituirà l&#39;identità primaria aggiunta direttamente allo schema. Per ulteriori informazioni, vedere la sezione relativa a `identityMap` nella [guida di base alla composizione dello schema](../schema/composition.md#identityMap).

Nella sezione **[!UICONTROL Structure]** dell&#39;editor, selezionare il campo `loyaltyId` e la casella di controllo **[!UICONTROL Identity]** viene visualizzata sotto **[!UICONTROL Field properties]**. Selezionare la casella e l&#39;opzione per impostare questo valore come **[!UICONTROL Primary identity]** viene visualizzata. Selezionate anche questa casella.

>[!NOTE]
>
>Ogni schema può contenere un solo campo identità principale. Una volta impostato un campo dello schema come identità principale, si riceverà un messaggio di errore se si tenta in seguito di impostare come principale un altro campo dell&#39;identità nello schema.

Successivamente, è necessario fornire un **[!UICONTROL Identity namespace]** dall&#39;elenco degli spazi dei nomi predefiniti nel menu a discesa. Poiché `loyaltyId` è l&#39;indirizzo e-mail del cliente, selezionate &quot;[!UICONTROL Email]&quot; dal menu a discesa. Selezionare **[!UICONTROL Apply]** per confermare gli aggiornamenti al campo `loyaltyId`.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Per un elenco degli spazi dei nomi standard e delle relative definizioni, consultare la [[!DNL Identity Service] documentazione](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Dopo aver applicato la modifica, l&#39;icona relativa a `loyaltyId` mostra un simbolo di impronta digitale, a indicare che si tratta ora di un campo di identità.

![](../images/tutorials/create-schema/identity-applied.png)

Ora tutti i dati acquisiti nel campo `loyaltyId` verranno utilizzati per identificare l&#39;individuo e unire una singola vista del cliente. Per ulteriori informazioni sull&#39;utilizzo delle identità in [!DNL Experience Platform], consultare la documentazione di [[!DNL Identity Service]](../../identity-service/home.md).

## Abilitare lo schema da utilizzare in [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) sfrutta i dati di identità  [!DNL Experience Platform] per fornire una visione olistica di ciascun cliente. Il servizio crea solidi profili a 360° degli attributi del cliente e conti con marca temporale di ogni interazione che i clienti hanno avuto in tutti i sistemi integrati con [!DNL Experience Platform].

Affinché uno schema sia abilitato per l&#39;uso con [!DNL Real-time Customer Profile], è necessario che sia definita un&#39;identità primaria. Se si tenta di abilitare uno schema senza prima definire un&#39;identità primaria, verrà visualizzato un messaggio di errore.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Per attivare lo schema &quot;Membri fedeltà&quot; da utilizzare in [!DNL Profile], iniziare selezionando &quot;[!DNL Loyalty Members]&quot; nella sezione **[!UICONTROL Structure]** dell&#39;editor.

Sul lato destro dell&#39;editor, vengono visualizzate informazioni sullo schema, incluso il nome visualizzato, la descrizione e il tipo. Oltre a queste informazioni, è presente un **[!UICONTROL Profile]** pulsante di attivazione/disattivazione.

![](../images/tutorials/create-schema/profile-toggle.png)

Selezionare **[!UICONTROL Profile]** e viene visualizzato un puntatore che richiede di confermare l&#39;abilitazione dello schema per [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Una volta che uno schema è stato abilitato per [!DNL Real-time Customer Profile] e salvato, non può essere disabilitato.

Selezionare **[!UICONTROL Enable]** per confermare la scelta. È possibile selezionare di nuovo l&#39;interruttore **[!UICONTROL Profile]** per disabilitare lo schema, se lo si desidera, ma una volta che lo schema è stato salvato mentre [!DNL Profile] è abilitato, non può più essere disabilitato.

## Passaggi successivi e risorse aggiuntive

Dopo aver completato la composizione dello schema, è possibile visualizzare lo schema completo nell&#39;area di lavoro. Selezionare **[!UICONTROL Save]** e lo schema verrà salvato nella [!DNL Schema Library], rendendolo accessibile dalla [!DNL Schema Registry].

È ora possibile utilizzare il nuovo schema per assimilare i dati in [!DNL Platform]. Tenere presente che una volta che lo schema è stato utilizzato per acquisire i dati, è possibile apportare solo modifiche aggiuntive. Per ulteriori informazioni sul controllo delle versioni dello schema, vedere le [nozioni di base della composizione dello schema](../schema/composition.md).

È ora possibile seguire l&#39;esercitazione su [definizione di una relazione di schema nell&#39;interfaccia utente](./relationship-ui.md) per aggiungere un nuovo campo di relazione allo schema &quot;Membri fedeltà&quot;.

Lo schema &quot;Membri fedeltà&quot; è disponibile anche per la visualizzazione e la gestione tramite l&#39;API [!DNL Schema Registry]. Per iniziare a lavorare con l&#39;API, leggete la [[!DNL Schema Registry API] guida per gli sviluppatori](../api/getting-started.md).

### Risorse video

>[!WARNING]
>
>L&#39;interfaccia [!DNL Platform] mostrata nei video seguenti non è aggiornata. Per informazioni sulle ultime funzionalità e videate dell’interfaccia, consulta la documentazione precedente.

Il video seguente mostra come creare uno schema semplice nell&#39;interfaccia utente [!DNL Platform].

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

Il seguente video è pensato per comprendere meglio come utilizzare mixin e classi.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive relative all&#39;utilizzo di [!DNL Schema Editor].

### Creare una nuova classe {#create-new-class}

[!DNL Experience Platform] consente di definire uno schema basato su una classe univoca per l&#39;organizzazione. Per informazioni su come creare una nuova classe, consultare la guida relativa alla [creazione e modifica di classi nell&#39;interfaccia utente](../ui/resources/classes.md#create).

### Modificare la classe di uno schema {#change-class}

È possibile modificare la classe di uno schema in qualsiasi punto del processo di composizione iniziale prima che lo schema sia stato salvato.

>[!WARNING]
>
>La riassegnazione della classe per uno schema deve essere eseguita con estrema cautela. I mixin sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà il quadro e tutti i campi aggiunti.

Per informazioni su come modificare la classe di uno schema, vedere la guida sulla [gestione degli schemi nell&#39;interfaccia utente](../ui/resources/schemas.md).