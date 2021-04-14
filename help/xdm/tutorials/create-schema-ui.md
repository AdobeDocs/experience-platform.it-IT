---
keywords: Experience Platform;home;argomenti popolari;interfaccia utente;XDM;sistema XDM;modello dati esperienza;modello dati esperienza;modello dati esperienza;modello dati;modello dati;modello dati;editor schema;Editor schema;schema;schema;schemi;schemi;schemi;creare
solution: Experience Platform
title: Creare uno schema utilizzando l’Editor di schema
topic: tutorial
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per creare uno schema utilizzando Schema Editor all’interno di Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
translation-type: tm+mt
source-git-commit: 53bf2ad757b24ad294af32101124e8047580807a
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 0%

---

# Creare uno schema utilizzando [!DNL Schema Editor]

L’interfaccia utente di Adobe Experience Platform consente di creare e gestire gli schemi [!DNL Experience Data Model] (XDM) in un’area di lavoro visiva interattiva denominata [!DNL Schema Editor]. Questa esercitazione illustra come creare uno schema utilizzando [!DNL Schema Editor].

>[!NOTE]
>
>A scopo dimostrativo, i passaggi di questa esercitazione consistono nella creazione di uno schema di esempio che descrive i membri di un programma fedeltà cliente. Mentre è possibile utilizzare questi passaggi per creare uno schema diverso per scopi propri, si consiglia innanzitutto di seguire la creazione dello schema di esempio per apprendere le funzionalità di [!DNL Schema Editor].

Se invece preferisci comporre uno schema utilizzando l&#39;API [!DNL Schema Registry], inizia leggendo la [[!DNL Schema Registry] guida per gli sviluppatori](../api/getting-started.md) prima di provare l&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API](create-schema-api.md).

## Introduzione

Questa esercitazione richiede una comprensione approfondita dei vari aspetti di Adobe Experience Platform coinvolti nella creazione dello schema. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti concetti:

* [[!DNL Experience Data Model (XDM)]](../home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../schema/composition.md) dello schema: Panoramica degli schemi XDM e dei relativi blocchi predefiniti, inclusi classi, mixin, tipi di dati e campi.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Apri l&#39;area di lavoro [!UICONTROL Schemas] {#browse}

L’ area di lavoro [!UICONTROL Schemas] nell’ interfaccia utente di [!DNL Platform] fornisce una visualizzazione del [!DNL Schema Library], che consente di visualizzare gestire gli schemi disponibili per la tua organizzazione. L’area di lavoro include anche la sezione [!DNL Schema Editor], l’area di lavoro su cui è possibile comporre uno schema durante questa esercitazione.

Dopo aver effettuato l&#39;accesso a [!DNL Experience Platform], seleziona **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro **[!UICONTROL Schemas]**. La scheda **[!UICONTROL Browse]** visualizza un elenco di schemi (una rappresentazione del [!DNL Schema Library]) che è possibile visualizzare e personalizzare. L&#39;elenco include il nome, il tipo, la classe e il comportamento (record o serie temporali) su cui si basa lo schema, nonché la data e l&#39;ora dell&#39;ultima modifica dello schema.

Per ulteriori informazioni, consulta la guida sull’ [esplorazione delle risorse XDM esistenti nell’interfaccia utente](../ui/explore.md) .

## Creare e denominare uno schema {#create}

Per iniziare a comporre uno schema, seleziona **[!UICONTROL Create schema]** nell’angolo in alto a destra dell’area di lavoro **[!UICONTROL Schemas]**. Viene visualizzato un menu a discesa che consente di scegliere tra le classi principali [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent]. Se queste classi non soddisfano le tue esigenze, puoi anche selezionare **[!UICONTROL Browse]** per scegliere tra altre classi disponibili o [creare una nuova classe](#create-new-class).

Ai fini di questa esercitazione, seleziona **[!UICONTROL XDM Individual Profile]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Poiché hai scelto una classe XDM standard su cui basare lo schema, viene visualizzata la finestra di dialogo **[!UICONTROL Add mixin]**, che consente di iniziare immediatamente ad aggiungere campi allo schema. Per il momento, seleziona **[!UICONTROL Cancel]** per uscire dalla finestra di dialogo.

![](../images/tutorials/create-schema/cancel-mixin.png)

Viene visualizzato il simbolo [!DNL Schema Editor]. Questa è l&#39;area di lavoro su cui comporre lo schema. All’arrivo nell’editor viene automaticamente creato uno schema senza titolo nella sezione **[!UICONTROL Structure]** dell’area di lavoro, insieme ai campi standard inclusi in tutti gli schemi basati su tale classe. La classe assegnata per lo schema è inoltre elencata in **[!UICONTROL Class]** nella sezione **[!UICONTROL Composition]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>È possibile [modificare la classe di uno schema](#change-class) in qualsiasi momento durante il processo di composizione iniziale prima che lo schema sia stato salvato, ma questo deve essere fatto con estrema cautela. I mixin sono compatibili solo con determinate classi e pertanto la modifica della classe reimposterà l’area di lavoro e gli eventuali campi aggiunti.

Utilizza i campi a destra dell’editor per fornire un nome visualizzato e una descrizione facoltativa per lo schema. Una volta immesso un nome, l’area di lavoro viene aggiornata per riflettere il nuovo nome dello schema.

![](../images/tutorials/create-schema/name_schema.png)

Quando si decide un nome per lo schema, è necessario tenere presenti diverse considerazioni importanti:

* I nomi dello schema devono essere brevi e descrittivi in modo che lo schema possa essere trovato facilmente in un secondo momento.
* I nomi di schema devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro. Ad esempio, se la tua organizzazione dispone di programmi di fidelizzazione separati per marchi diversi, è consigliabile assegnare un nome allo schema &quot;Membri fedeltà di marchio&quot; per distinguere facilmente gli altri schemi relativi alla fedeltà che potresti definire in seguito.
* Puoi inoltre utilizzare la descrizione dello schema per fornire eventuali informazioni contestuali aggiuntive relative allo schema.

Questa esercitazione crea uno schema per acquisire i dati relativi ai membri di un programma fedeltà e pertanto lo schema è denominato &quot;Membri fedeltà&quot;.

## Aggiungi un mixin {#mixin}

Ora puoi iniziare ad aggiungere campi allo schema aggiungendo mixin. Un mixin è un gruppo di uno o più campi che vengono spesso utilizzati insieme per descrivere un particolare concetto. Questa esercitazione utilizza i mixin per descrivere i membri del programma fedeltà e acquisire informazioni chiave come nome, compleanno, numero di telefono, indirizzo e altro ancora.

Per aggiungere un mixin, seleziona **[!UICONTROL Add]** nella sottosezione **[!UICONTROL Mixins]** .

![](../images/tutorials/create-schema/add_mixin_button.png)

Viene visualizzata una nuova finestra di dialogo con un elenco dei mixin disponibili. Ogni mixin è destinato solo a una classe specifica, pertanto la finestra di dialogo elenca solo i mixin compatibili con la classe selezionata (in questo caso, la classe [!DNL XDM Individual Profile]). Se utilizzi una classe XDM standard, l’elenco dei mixin verrà ordinato in modo intelligente in base alla popolarità dell’utilizzo.

![](../images/tutorials/create-schema/mixin-popularity.png)

Quando si seleziona un mixin dall’elenco, questo viene visualizzato nella barra a destra. Puoi selezionare più mixin, se lo desideri, aggiungendo ciascuno di essi all’elenco nella barra a destra, prima di confermare. Inoltre, sul lato destro del mixin attualmente selezionato viene visualizzata un’icona che consente di visualizzare in anteprima la struttura dei campi disponibili.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Quando visualizzi l’anteprima di un mixin, nella barra a destra viene fornita una descrizione dettagliata dello schema del mixin. Puoi anche navigare tra i campi del mixin nell’area di lavoro fornita. Quando selezioni campi diversi, la barra a destra si aggiorna e mostra i dettagli del campo in questione. Seleziona **[!UICONTROL Back]** una volta terminata l&#39;anteprima per tornare alla finestra di dialogo di selezione del mixin.

![](../images/tutorials/create-schema/preview-mixin.png)

Per questa esercitazione, seleziona il mixin **[!UICONTROL Demographic Details]**, quindi seleziona **[!UICONTROL Add mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

L&#39;area di lavoro dello schema viene visualizzata nuovamente. La sezione **[!UICONTROL Mixins]** ora elenca &quot;[!UICONTROL Demographic Details]&quot; e la sezione **[!UICONTROL Structure]** include i campi aggiunti dal mixin. Puoi selezionare il nome del mixin sotto la sezione **[!UICONTROL Mixins]** per evidenziare i campi specifici che fornisce all&#39;interno dell&#39;area di lavoro.

![](../images/tutorials/create-schema/person_details_structure.png)

Questo mixin contribuisce a diversi campi sotto il nome di livello principale `person` con il tipo di dati &quot;[!UICONTROL Person]&quot;. Questo gruppo di campi descrive informazioni su un individuo, tra cui nome, data di nascita e genere.

>[!NOTE]
>
>Tenere presente che i campi possono utilizzare tipi scalari (come stringa, numero intero, matrice o data), nonché qualsiasi tipo di dati (un gruppo di campi che rappresenta un concetto comune) definito all&#39;interno di [!DNL Schema Registry].

Il campo `name` ha un tipo di dati &quot;[!UICONTROL Person name]&quot;, il che significa che descrive anche un concetto comune e contiene campi secondari relativi al nome, come nome, cognome, titolo di cortesia e suffisso.

Seleziona i diversi campi all’interno dell’area di lavoro per visualizzare eventuali campi aggiuntivi che contribuiscono alla struttura dello schema.

## Aggiungi un altro mixin {#mixin-2}

Ora puoi ripetere gli stessi passaggi per aggiungere un altro mixin. Quando visualizzi la finestra di dialogo **[!UICONTROL Add mixin]**, noterai che il mixin &quot;[!UICONTROL Demographic Details]&quot; è stato disattivato e che la casella di controllo accanto non può essere selezionata. Questo impedisce la duplicazione accidentale di mixin già inclusi nello schema corrente.

Per questa esercitazione, seleziona il mixin &quot;[!DNL Personal Contact Details]&quot; dalla finestra di dialogo, quindi seleziona **[!UICONTROL Add mixin]** per aggiungerlo allo schema.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Una volta aggiunto, l’area di lavoro viene visualizzata nuovamente. &quot;[!UICONTROL Personal Contact Details]&quot; è ora elencato in **[!UICONTROL Mixins]** nella sezione **[!UICONTROL Composition]** e i campi per l&#39;indirizzo della casa, il telefono cellulare e altro sono stati aggiunti in **[!UICONTROL Structure]**.

Analogamente al campo `name` , i campi appena aggiunti rappresentano concetti relativi a più campi. Ad esempio, `homeAddress` ha un tipo di dati &quot;[!UICONTROL Postal address]&quot; e `mobilePhone` ha un tipo di dati &quot;[!UICONTROL Phone number]&quot;. Puoi selezionare ciascuno di questi campi per espanderli e visualizzare i campi aggiuntivi inclusi nel tipo di dati.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definire un mixin personalizzato {#define-mixin}

Lo schema &quot;[!UICONTROL Loyalty Members]&quot; è inteso per acquisire dati relativi ai membri di un programma fedeltà, pertanto richiederà alcuni campi specifici relativi alla fidelizzazione.

Esiste un mixin standard [!UICONTROL Loyalty Details] che puoi aggiungere allo schema per acquisire i campi comuni relativi a un programma fedeltà. Anche se sei fortemente incoraggiato a utilizzare mixin standard per rappresentare i concetti acquisiti dai tuoi schemi, la struttura del mixin fedeltà standard potrebbe non essere in grado di acquisire tutti i dati rilevanti per il tuo particolare programma fedeltà. In questo scenario, puoi scegliere di definire un nuovo mixin personalizzato per acquisire invece questi campi.

Apri nuovamente la finestra di dialogo **[!UICONTROL Add Mixin]**, ma questa volta seleziona **[!UICONTROL Create New Mixin]** vicino alla parte superiore. Ti viene quindi chiesto di fornire un nome e una descrizione visualizzati per il tuo mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Come per i nomi delle classi, il nome del mixin deve essere breve e semplice, descrivendo il contributo del mixin allo schema. Anche questi sono univoci, quindi non potrai riutilizzare il nome e devi quindi assicurarti che sia sufficientemente specifico.

Per questa esercitazione, denomina il nuovo mixin &quot;Dettagli fedeltà&quot;.

Seleziona **[!UICONTROL Add mixin]** per tornare al percorso [!DNL Schema Editor]. &quot;[!UICONTROL Loyalty Details]&quot; dovrebbe ora apparire sotto **[!UICONTROL Mixins]** sul lato sinistro dell&#39;area di lavoro, ma non sono ancora presenti campi associati ad essa e quindi non vengono visualizzati nuovi campi sotto **[!UICONTROL Structure]**.

## Aggiungi campi al mixin {#mixin-fields}

Dopo aver creato il mixin &quot;Dettagli fedeltà&quot;, è ora di definire i campi che il mixin contribuirà allo schema.

Per iniziare, seleziona il nome del mixin nella sezione **[!UICONTROL Mixins]** . Una volta fatto questo, le proprietà del mixin appaiono sul lato destro dell&#39;editor e un&#39;icona **più (+)** appare accanto al nome dello schema sotto **[!UICONTROL Structure]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Seleziona l&#39;icona **più (+)** accanto a &quot;[!DNL Loyalty Members]&quot; per creare un nuovo nodo nella struttura. Questo nodo (denominato `_tenantId` in questo esempio) rappresenta l’ID tenant dell’organizzazione IMS, preceduto da un trattino basso. La presenza dell’ID tenant indica che i campi da aggiungere sono contenuti nello spazio dei nomi dell’organizzazione.

In altre parole, i campi che stai aggiungendo sono univoci per la tua organizzazione e verranno salvati in [!DNL Schema Registry] in un’area specifica accessibile solo dalla tua organizzazione. I campi definiti devono sempre essere aggiunti allo spazio dei nomi del tenant per evitare conflitti con nomi di altre classi, mixin, tipi di dati e campi standard.

All&#39;interno di quel nodo con namespace c&#39;è un &quot;[!UICONTROL New Field]&quot;. Questo è l&#39;inizio del mixin &quot;[!UICONTROL Loyalty Details]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Utilizzando i controlli a destra dell’editor, inizia con la creazione di un campo `loyalty` con il tipo &quot;[!UICONTROL Object]&quot; che verrà utilizzato per contenere i campi relativi alla fidelizzazione. Al termine, seleziona **[!UICONTROL Apply]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Le modifiche vengono applicate e viene visualizzato l&#39;oggetto `loyalty` appena creato. Seleziona l’icona **più (+)** accanto all’oggetto per aggiungere altri campi relativi alla fedeltà. Viene visualizzato un &quot;[!UICONTROL New Field]&quot; e la sezione **[!UICONTROL Field properties]** è visibile sul lato destro dell&#39;area di lavoro.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Ogni campo richiede le seguenti informazioni:

* **[!UICONTROL Field Name]:** Il nome del campo, scritto in cammello. Esempio: loyaltyLevel
* **[!UICONTROL Display Name]:** Il nome del campo, scritto nel title case. Esempio: Livello fedeltà
* **[!UICONTROL Type]:** il tipo di dati del campo. Ciò include i tipi scalari di base e tutti i tipi di dati definiti in [!DNL Schema Registry]. Esempi: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone number], ecc.
* **[!UICONTROL Description]:** Una descrizione facoltativa del campo deve essere inclusa, scritta in caso di frase, con un massimo di 200 caratteri.

Il primo campo dell&#39;oggetto `Loyalty` sarà una stringa denominata `loyaltyId`. Quando si imposta il tipo di nuovo campo su &quot;[!UICONTROL String]&quot;, la sezione **[!UICONTROL Field properties]** viene compilata con diverse opzioni per l&#39;applicazione di vincoli, tra cui valore predefinito, formato e lunghezza massima.

![](../images/tutorials/create-schema/string_constraints.png)

Sono disponibili diverse opzioni di vincolo a seconda del tipo di dati selezionato. Poiché `loyaltyId` sarà un indirizzo e-mail, seleziona &quot;[!UICONTROL email]&quot; dal menu a discesa **[!UICONTROL Format]**. Seleziona **[!UICONTROL Apply]** per applicare le modifiche.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Aggiungi altri campi al mixin {#mixin-fields-2}

Dopo aver aggiunto il campo `loyaltyId` , puoi aggiungere altri campi per acquisire informazioni relative alla fidelizzazione, ad esempio:

* Punti (numero intero)
* Membro dal (data)

Per aggiungere ogni campo allo schema, seleziona l’icona **più (+)** accanto all’oggetto `loyalty` e compila le informazioni richieste.

Una volta completato, l’oggetto Fedeltà conterrà campi per ID fedeltà, punti e membri dal momento in cui è stato eseguito il binding.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Aggiungi un campo enum al mixin {#enum}

Durante la definizione dei campi in [!DNL Schema Editor], è possibile applicare alcune opzioni aggiuntive ai tipi di campi di base per fornire ulteriori vincoli sui dati che il campo può contenere. I casi d’uso per questi vincoli sono descritti nella tabella seguente:

| Vincolo | Descrizione |
| --- | --- |
| [!UICONTROL Required] | Indica che il campo è obbligatorio per l’inserimento dei dati. Eventuali dati caricati in un set di dati basato su questo schema che non contiene questo campo avranno esito negativo al momento dell’inserimento. |
| [!UICONTROL Array] | Indica che il campo contiene una matrice di valori, ciascuno con il tipo di dati specificato. Ad esempio, se si utilizza questo vincolo su un campo con un tipo di dati &quot;[!UICONTROL String]&quot;, il campo conterrà una matrice di stringhe. |
| [!UICONTROL Enum] | Indica che il campo deve contenere uno dei valori di un elenco enumerato di valori possibili. |
| [!UICONTROL Identity] | Indica che il campo è un campo di identità. Ulteriori informazioni sui campi di identità sono fornite [più avanti in questa esercitazione](#identity-field). |
| [!UICONTROL Relationship] | Mentre le relazioni dello schema possono essere dedotte mediante l&#39;uso dello schema di unione e di [!DNL Real-time Customer Profile], questo vale solo per gli schemi che condividono la stessa classe. Il vincolo [!UICONTROL Relationship] indica che questo campo fa riferimento all&#39;identità primaria di uno schema basato su una classe diversa e implica una relazione tra i due schemi. Per ulteriori informazioni, consulta l’esercitazione su [definizione di una relazione](./relationship-ui.md) . |

>[!NOTE]
>
>Tutti i campi obbligatori, di identità o di relazione vengono visualizzati nella barra a sinistra, consentendo di individuare facilmente tali campi indipendentemente dalla complessità dello schema.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Per questa esercitazione, l&#39;oggetto [!DNL "loyalty"] nello schema richiede un nuovo campo enum che descrive il &quot;livello di fedeltà&quot; di un cliente, dove il valore può essere solo una delle quattro opzioni possibili. Per aggiungere questo campo allo schema, seleziona l’icona **più (+)** accanto all’oggetto `loyalty` e compila i campi obbligatori per **[!UICONTROL Field name]** e **[!UICONTROL Display name]**. Per **[!UICONTROL Type]**, seleziona &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

Dopo la selezione del relativo tipo, vengono visualizzate ulteriori caselle di controllo per il campo, incluse le caselle **[!UICONTROL Array]**, **[!UICONTROL Enum]** e **[!UICONTROL Identity]**.

Seleziona la casella di controllo **[!UICONTROL Enum]** per aprire la sezione **[!UICONTROL Enum values]** sottostante. Qui puoi inserire i valori **[!UICONTROL Value]** (in camelCase) e **[!UICONTROL Label]** (un nome opzionale e facile da leggere nel caso Titolo) per ogni livello di fedeltà accettabile.

Dopo aver completato tutte le proprietà del campo, selezionare **[!UICONTROL Apply]** per aggiungere il campo &quot;[!DNL loyaltyLevel]&quot; all&#39;oggetto `loyalty`.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Convertire un oggetto con più campi in un tipo di dati {#datatype}

L’oggetto `loyalty` ora contiene diversi campi specifici per la fidelizzazione e rappresenta una struttura dati comune che potrebbe essere utile in altri schemi. La funzione [!DNL Schema Editor] consente di applicare rapidamente oggetti multicampo riutilizzabili convertendo la struttura di tali oggetti in tipi di dati.

I tipi di dati consentono l’uso coerente di strutture a più campi e offrono maggiore flessibilità rispetto a un mixin, in quanto possono essere utilizzati ovunque all’interno di uno schema. A questo scopo, imposta il valore **[!UICONTROL Type]** del campo su quello di qualsiasi tipo di dati definito in [!DNL Schema Registry].

Per convertire l&#39;oggetto `loyalty` in un tipo di dati, selezionare il campo `loyalty` in **[!UICONTROL Structure]**, quindi selezionare **[!UICONTROL Convert to new data type]** sul lato destro dell&#39;editor in **[!UICONTROL Field properties]**. Viene visualizzato un puntatore verde che conferma la corretta conversione dell’oggetto.

![](../images/tutorials/create-schema/convert-data-type.png)

Ora, quando cerchi sotto **[!UICONTROL Structure]**, puoi vedere che il campo `loyalty` ha un tipo di dati &quot;[!DNL Loyalty]&quot; e i campi hanno icone di blocco piccole accanto a essi, il che indica che non sono più campi singoli ma fanno parte di un tipo di dati con più campi.

![](../images/tutorials/create-schema/loyalty_data_type.png)

In uno schema futuro, ora puoi assegnare un campo come tipo &quot;[!DNL Loyalty]&quot; e questo includerebbe automaticamente campi per ID, livello fedeltà, membro da e punti.

>[!NOTE]
>
>Puoi anche creare e modificare tipi di dati personalizzati in modo indipendente dalla modifica degli schemi. Per ulteriori informazioni, consulta la guida sulla [creazione e modifica di tipi di dati](../ui/resources/data-types.md) .

## Campi dello schema di ricerca e filtro

Lo schema ora contiene diversi mixin oltre ai campi forniti dalla relativa classe base. Quando lavori con schemi di grandi dimensioni, puoi selezionare le caselle di controllo accanto ai nomi misti nella barra a sinistra per filtrare i campi visualizzati in base solo a quelli forniti dai mixin interessati.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Se si cerca un campo specifico nello schema, è anche possibile utilizzare la barra di ricerca per filtrare i campi visualizzati per nome, indipendentemente dal mixin in cui sono forniti.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>Quando si visualizzano i campi corrispondenti, la funzione di ricerca tiene conto dei filtri mixin selezionati. Se una query di ricerca non visualizza i risultati previsti, potrebbe essere necessario verificare di non filtrare i mixin rilevanti.

## Imposta un campo schema come campo di identità {#identity-field}

La struttura dati standard fornita dagli schemi può essere sfruttata per identificare i dati appartenenti alla stessa persona su più origini, consentendo diversi casi d’uso a valle, come segmentazione, reporting, analisi della scienza dei dati e altro ancora. Per unire i dati in base alle singole identità, i campi chiave devono essere contrassegnati come campi [!UICONTROL Identity] all’interno degli schemi applicabili.

[!DNL Experience Platform] consente di identificare facilmente un campo di identità tramite l’uso di una  **[!UICONTROL Identity]** casella di controllo in  [!DNL Schema Editor]. Tuttavia, è necessario determinare quale campo è il candidato migliore per utilizzare come identità, in base alla natura dei dati.

Ad esempio, ci possono essere migliaia di membri del programma fedeltà appartenenti allo stesso &quot;livello fedeltà&quot;, ma ogni membro del programma fedeltà ha un `loyaltyId` univoco (che in questo caso è l&#39;indirizzo e-mail del singolo membro). Il fatto che `loyaltyId` sia un identificatore univoco per ciascun membro lo rende un buon candidato per un campo di identità, mentre `loyaltyLevel` non lo è.

>[!IMPORTANT]
>
>I passaggi descritti di seguito spiegano come aggiungere un descrittore di identità a un campo di schema esistente. Invece di definire i campi di identità all’interno della struttura dello schema stesso, puoi utilizzare un campo `identityMap` per contenere le informazioni di identità.
>
>Se prevedi di utilizzare `identityMap`, ricorda che ignorerà direttamente qualsiasi identità primaria aggiunta allo schema. Per ulteriori informazioni, consulta la sezione su `identityMap` nella [guida alle nozioni di base sulla composizione dello schema](../schema/composition.md#identityMap) .

Nella sezione **[!UICONTROL Structure]** dell’editor, seleziona il campo `loyaltyId` e la casella di controllo **[!UICONTROL Identity]** viene visualizzata in **[!UICONTROL Field properties]**. Seleziona la casella e l’opzione per impostarla come viene visualizzato il simbolo **[!UICONTROL Primary identity]**. Seleziona anche questa casella.

>[!NOTE]
>
>Ogni schema può contenere un solo campo di identità principale. Una volta impostato un campo schema come identità principale, riceverai un messaggio di errore se in seguito tenti di impostare un altro campo di identità nello schema come principale.

Successivamente, devi fornire un **[!UICONTROL Identity namespace]** dall’elenco dei namespace predefiniti nel menu a discesa. Poiché `loyaltyId` è l&#39;indirizzo e-mail del cliente, seleziona &quot;[!UICONTROL Email]&quot; dal menu a discesa. Seleziona **[!UICONTROL Apply]** per confermare gli aggiornamenti al campo `loyaltyId` .

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Per un elenco dei namespace standard e delle relative definizioni, consulta la [[!DNL Identity Service] documentazione](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Dopo aver applicato la modifica, l&#39;icona relativa a `loyaltyId` mostra un simbolo di impronta digitale che indica che ora si tratta di un campo di identità.

![](../images/tutorials/create-schema/identity-applied.png)

Ora tutti i dati acquisiti nel campo `loyaltyId` verranno utilizzati per identificare l’individuo e unire una singola vista del cliente. Per ulteriori informazioni sull&#39;utilizzo delle identità in [!DNL Experience Platform], consulta la documentazione [[!DNL Identity Service]](../../identity-service/home.md) .

## Abilita lo schema da utilizzare in [!DNL Real-time Customer Profile] {#profile}

[[!DNL Real-time Customer Profile]](../../profile/home.md) sfrutta i dati di identità in  [!DNL Experience Platform] per fornire una visione olistica di ogni singolo cliente. Il servizio crea solidi profili a 360° degli attributi del cliente e account con marca temporale di ogni interazione che i clienti hanno avuto in qualsiasi sistema integrato con [!DNL Experience Platform].

Affinché uno schema possa essere abilitato per l&#39;uso con [!DNL Real-time Customer Profile], deve avere un&#39;identità primaria definita. Se tenti di abilitare uno schema senza prima definire un&#39;identità principale, riceverai un messaggio di errore.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Per abilitare lo schema &quot;Membri fedeltà&quot; da utilizzare in [!DNL Profile], inizia selezionando &quot;[!DNL Loyalty Members]&quot; nella sezione **[!UICONTROL Structure]** dell&#39;editor.

Sul lato destro dell’editor, vengono visualizzate informazioni sullo schema, compreso il nome visualizzato, la descrizione e il tipo. Oltre a queste informazioni, è disponibile un pulsante di attivazione/disattivazione **[!UICONTROL Profile]** .

![](../images/tutorials/create-schema/profile-toggle.png)

Selezionare **[!UICONTROL Profile]** e viene visualizzato un puntatore che richiede di confermare l&#39;abilitazione dello schema per [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Una volta che uno schema è stato abilitato per [!DNL Real-time Customer Profile] e salvato, non può essere disabilitato.

Seleziona **[!UICONTROL Enable]** per confermare la scelta. È possibile selezionare nuovamente l&#39;interruttore **[!UICONTROL Profile]** per disattivare lo schema, se lo si desidera, ma una volta che lo schema è stato salvato mentre [!DNL Profile] è abilitato, non può più essere disabilitato.

## Passaggi successivi e risorse aggiuntive

Al termine della composizione dello schema, puoi vedere lo schema completo nell’area di lavoro. Seleziona **[!UICONTROL Save]** e lo schema verrà salvato nel [!DNL Schema Library], rendendolo accessibile dal [!DNL Schema Registry].

Il nuovo schema può ora essere utilizzato per acquisire dati in [!DNL Platform]. Ricorda che una volta che lo schema è stato utilizzato per acquisire i dati, è possibile apportare solo modifiche aggiuntive. Per ulteriori informazioni sul controllo delle versioni dello schema, consulta le [nozioni di base sulla composizione dello schema](../schema/composition.md) .

È ora possibile seguire l&#39;esercitazione su [definizione di una relazione di schema nell&#39;interfaccia utente](./relationship-ui.md) per aggiungere un nuovo campo di relazione allo schema &quot;Membri fedeltà&quot;.

Lo schema &quot;Membri fedeltà&quot; è disponibile anche per essere visualizzato e gestito utilizzando l&#39;API [!DNL Schema Registry]. Per iniziare a lavorare con l&#39;API, leggi la [[!DNL Schema Registry API] guida per gli sviluppatori](../api/getting-started.md).

### Risorse video

>[!WARNING]
>
>L’ [!DNL Platform] interfaccia utente mostrata nei video seguenti non è aggiornata. Fai riferimento alla documentazione precedente per le ultime schermate e funzionalità dell’interfaccia utente.

Il video seguente mostra come creare uno schema semplice nell’ interfaccia utente [!DNL Platform] .

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

Il seguente video è pensato per comprendere meglio come si lavora con mixin e classi.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Appendice

Le sezioni seguenti forniscono informazioni aggiuntive relative all&#39;utilizzo di [!DNL Schema Editor].

### Crea una nuova classe {#create-new-class}

[!DNL Experience Platform] offre la flessibilità di definire uno schema basato su una classe univoca per la tua organizzazione. Per informazioni su come creare una nuova classe, consulta la guida [creazione e modifica di classi nell&#39;interfaccia utente](../ui/resources/classes.md#create).

### Modificare la classe di uno schema {#change-class}

È possibile modificare la classe di uno schema in qualsiasi punto durante il processo di composizione iniziale prima che lo schema sia stato salvato.

>[!WARNING]
>
>La riassegnazione della classe per uno schema deve essere eseguita con estrema cautela. I mixin sono compatibili solo con determinate classi e pertanto la modifica della classe reimposterà l’area di lavoro e gli eventuali campi aggiunti.

Per informazioni su come modificare la classe di uno schema, consulta la guida alla [gestione degli schemi nell&#39;interfaccia utente](../ui/resources/schemas.md).
