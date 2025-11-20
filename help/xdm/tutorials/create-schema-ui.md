---
keywords: Experience Platform;home;argomenti popolari;ui;interfaccia utente;XDM;sistema XDM;Experience data model;Experience data model;Experience Data Model;data model;Data Model;editor schema;schema;schema;schemi;schemi;creare;;home;popular topic;ui;UI;XDM;XDM system;experience data model;Experience data model;data model;Data Model;schema editor;schema;schema;schema;schema;schemi;creare
solution: Experience Platform
title: Creare uno schema tramite l’Editor di schema
type: Tutorial
description: Questa esercitazione illustra i passaggi necessari per creare uno schema utilizzando Schema Editor all’interno di Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '4670'
ht-degree: 1%

---

# Creare uno schema utilizzando [!DNL Schema Editor]

L&#39;interfaccia utente di Adobe Experience Platform consente di creare e gestire gli schemi [!DNL Experience Data Model] (XDM) in un&#39;area di lavoro visiva e interattiva denominata [!DNL Schema Editor]. Questo tutorial illustra come creare uno schema utilizzando [!DNL Schema Editor].

A scopo dimostrativo, i passaggi di questa esercitazione comportano la creazione di uno schema di esempio che descrive i membri di un programma fedeltà dei clienti. Anche se è possibile utilizzare questi passaggi per creare uno schema diverso per le proprie esigenze, si consiglia di eseguire prima la creazione dello schema di esempio per apprendere le funzionalità di [!DNL Schema Editor].

>[!NOTE]
>
>Se acquisisci dati CSV in Experience Platform, puoi [mappare tali dati su uno schema XDM creato dai consigli generati dall&#39;intelligenza artificiale](../../ingestion/tutorials/map-csv/recommendations.md) (attualmente in versione beta) senza dover creare manualmente lo schema.
>
>Se preferisci comporre uno schema utilizzando l&#39;API [!DNL Schema Registry], inizia leggendo la [[!DNL Schema Registry] guida per gli sviluppatori](../api/getting-started.md) prima di provare l&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API](create-schema-api.md).

## Introduzione

Questo tutorial richiede una buona conoscenza dei vari aspetti di Adobe Experience Platform coinvolti nella creazione dello schema. Prima di iniziare questo tutorial, consulta la documentazione per i seguenti concetti:

* [[!DNL Experience Data Model (XDM)]](../home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../schema/composition.md): panoramica degli schemi XDM e dei relativi blocchi predefiniti, inclusi classi, gruppi di campi dello schema, tipi di dati e singoli campi.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Apri l&#39;area di lavoro [!UICONTROL Schemas] {#browse}

L&#39;area di lavoro [!UICONTROL Schemas] nell&#39;interfaccia utente [!DNL Experience Platform] fornisce una visualizzazione di [!DNL Schema Library], che consente di visualizzare e gestire gli schemi disponibili per l&#39;organizzazione. L&#39;area di lavoro include anche [!DNL Schema Editor], l&#39;area di lavoro in cui è possibile comporre uno schema in questa esercitazione.

Dopo aver effettuato l&#39;accesso a [!DNL Experience Platform], selezionare **[!UICONTROL Schemas]** nel menu di navigazione a sinistra per aprire l&#39;area di lavoro **[!UICONTROL Schemas]**. Nella scheda **[!UICONTROL Browse]** viene visualizzato un elenco di schemi (una rappresentazione di [!DNL Schema Library]) da visualizzare e personalizzare. L’elenco include il nome, il tipo, la classe e il comportamento (record o serie temporale) su cui è basato lo schema, nonché la data e l’ora dell’ultima modifica dello schema.

Per ulteriori informazioni, consulta la guida sull&#39;esplorazione delle risorse XDM esistenti nell&#39;interfaccia utente[.](../ui/explore.md)

## Creare e denominare uno schema {#create}

Per iniziare a comporre uno schema, selezionare **[!UICONTROL Create schema]** nell&#39;angolo superiore destro dell&#39;area di lavoro **[!UICONTROL Schemas]**.

![Scheda [!UICONTROL Schemas] dell&#39;area di lavoro [!UICONTROL Browse] con [!UICONTROL Create schema] evidenziato.](../images/tutorials/create-schema/create-schema-button.png)

Viene visualizzata la finestra di dialogo [!UICONTROL Create a schema]. In questa finestra di dialogo, puoi scegliere di creare manualmente uno schema aggiungendo campi e gruppi di campi, oppure puoi caricare un file CSV e utilizzare algoritmi ML per generare uno schema. Seleziona un flusso di lavoro per la creazione di uno schema dalla finestra di dialogo.

![Finestra di dialogo Crea schema con le opzioni del flusso di lavoro e seleziona evidenziato.](../images/tutorials/create-schema/create-a-schema-dialog.png)

### [!BADGE Beta]{type=Informative} Creazione manuale o assistita da ML dello schema {#manual-or-assisted}

Per informazioni su come utilizzare un algoritmo ML per consigliare una struttura di schema basata su un file caricato, consulta la [guida alla creazione di schemi supportati dall&#39;apprendimento automatico](../ui/ml-assisted-schema-creation.md). Questa guida dell’interfaccia utente si concentra sul flusso di lavoro di creazione manuale.

### Scegli una classe base {#choose-a-class}

Verrà visualizzato il flusso di lavoro [!UICONTROL Create schema]. Scegliere quindi una classe base per lo schema. È possibile scegliere tra le classi principali di [!UICONTROL XDM Individual Profile] e [!UICONTROL XDM ExperienceEvent] oppure [!UICONTROL Other] se queste classi non soddisfano le proprie esigenze. L&#39;opzione [!UICONTROL Other] classi consente di [creare una nuova classe](#create-new-class) o di scegliere tra altre classi preesistenti.

Per ulteriori informazioni su queste classi, vedere la documentazione di [[!UICONTROL XDM individual profile]](../classes/individual-profile.md) e [[!UICONTROL XDM ExperienceEvent]](../classes/experienceevent.md). Ai fini di questa esercitazione, seleziona **[!UICONTROL XDM Individual Profile]** seguito da **[!UICONTROL Next]**.

![Il flusso di lavoro [!UICONTROL Create schema] con le opzioni [!UICONTROL XDM individual profile] e [!UICONTROL Next] evidenziato.](../images/tutorials/create-schema/individual-profile-base-class.png)

### Denomina e rivedi {#name-and-review}

Dopo aver selezionato una classe, viene visualizzata la sezione [!UICONTROL Name and review]. In questa sezione, fornisci un nome e una descrizione per identificare lo schema. Ci sono diverse considerazioni importanti da fare quando si decide un nome per lo schema:

* I nomi degli schemi devono essere brevi e descrittivi in modo che lo schema possa essere facilmente trovato in un secondo momento.
* I nomi degli schemi devono essere univoci, ovvero devono essere sufficientemente specifici da non poter essere riutilizzati in futuro. Ad esempio, se l’organizzazione dispone di programmi fedeltà separati per marchi diversi, sarebbe opportuno denominare lo schema &quot;Membri fedeltà per marchio&quot; per semplificare la distinzione da altri schemi relativi alla fedeltà che potresti definire in un secondo momento.
* È inoltre possibile utilizzare la descrizione dello schema per fornire eventuali informazioni contestuali aggiuntive relative allo schema.

Questa esercitazione crea uno schema per acquisire i dati relativi ai membri di un programma fedeltà e pertanto lo schema è denominato &quot;[!DNL Loyalty Members]&quot;.

&#x200B;La struttura di base dello schema (fornita dalla classe) viene visualizzata nell’area di lavoro per rivedere e verificare la struttura di classe e schema selezionata.

Immetti un [!UICONTROL Schema display name] descrittivo nel campo di testo. Quindi, inserisci una descrizione adatta per identificare lo schema. Dopo aver rivisto la struttura dello schema e aver impostato correttamente le impostazioni, selezionare **[!UICONTROL Finish]** per creare lo schema.

![La sezione [!UICONTROL Name and review] del flusso di lavoro [!UICONTROL Create schema] con [!UICONTROL Schema display name], [!UICONTROL Description] e [!UICONTROL Finish] evidenziati.](../images/ui/resources/schemas/name-and-review.png)

### Componi lo schema {#compose-your-schema}

Verrà visualizzato [!DNL Schema Editor]. Questa è l’area di lavoro su cui comporrai lo schema. Lo schema con titolo autonomo viene creato automaticamente nella sezione **[!UICONTROL Structure]** dell&#39;area di lavoro quando si arriva nell&#39;editor, insieme ai campi standard inclusi nella classe base selezionata. La classe assegnata per lo schema è elencata anche in **[!UICONTROL Class]** nella sezione **[!UICONTROL Composition]**.

>[!NOTE]
>
>È possibile aggiornare il nome visualizzato e la descrizione facoltativa per lo schema dalla barra laterale **[!UICONTROL Schema properties]**. Una volta inserito un nuovo nome, l’area di lavoro si aggiorna automaticamente per riflettere il nuovo nome dello schema.

![Editor schema con la classe base e il diagramma schema evidenziati.](../images/tutorials/create-schema/loyalty-members-schema-editor.png)

>[!NOTE]
>
>È possibile [modificare la classe di uno schema](#change-class) in qualsiasi momento durante il processo di composizione iniziale prima che lo schema sia stato salvato, ma questo deve essere fatto con estrema cautela. I gruppi di campi sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà l’area di lavoro e tutti i campi aggiunti.

## Aggiungi un gruppo di campi {#field-group}

Ora puoi iniziare ad aggiungere campi allo schema aggiungendo gruppi di campi. Un gruppo di campi è un gruppo di uno o più campi che vengono spesso utilizzati insieme per descrivere un particolare concetto. Questa esercitazione utilizza i gruppi di campi per descrivere i membri del programma fedeltà e acquisire informazioni chiave come nome, compleanno, numero di telefono, indirizzo e altro ancora.

Per aggiungere un gruppo di campi, selezionare **[!UICONTROL Add]** nella sottosezione **[!UICONTROL Field groups]**.

![Editor di schema con il pulsante Aggiungi gruppi di campi evidenziato.](../images/tutorials/create-schema/add-field-group-button.png)

Viene visualizzata una nuova finestra di dialogo con un elenco dei gruppi di campi disponibili. Ogni gruppo di campi deve essere utilizzato solo con una classe specifica, pertanto nella finestra di dialogo vengono elencati solo i gruppi di campi compatibili con la classe selezionata (in questo caso, la classe [!DNL XDM Individual Profile]). Se utilizzi una classe XDM standard, l’elenco dei gruppi di campi verrà ordinato in modo intelligente in base alla popolarità dell’utilizzo.

![Finestra di dialogo [!UICONTROL Add field groups].](../images/tutorials/create-schema/field-group-popularity.png)

Puoi selezionare uno dei filtri nella barra a sinistra per restringere l&#39;elenco dei gruppi di campi standard a [settori](../schema/industries/overview.md) specifici, come vendita al dettaglio, servizi finanziari e sanità.

![La finestra di dialogo [!UICONTROL Add field groups] con i gruppi di campi del settore è evidenziata.](../images/tutorials/create-schema/industry-field-groups.png)

Selezionando un gruppo di campi dall’elenco, questo viene visualizzato nella barra a destra. Se necessario, puoi selezionare più gruppi di campi, aggiungendoli all’elenco nella barra a destra prima di confermare. Sul lato destro del gruppo di campi attualmente selezionato viene inoltre visualizzata un&#39;icona che consente di visualizzare in anteprima la struttura dei campi forniti.

![La finestra di dialogo [!UICONTROL Add field groups] con l&#39;icona di anteprima del gruppo di campi selezionata è evidenziata.](../images/tutorials/create-schema/preview-field-group-button.png)

Nell’anteprima di un gruppo di campi, nella barra a destra viene fornita una descrizione dettagliata dello schema del gruppo di campi. Puoi anche spostarti tra i campi del gruppo di campi nell’area di lavoro fornita. Quando selezioni diversi campi, la barra a destra si aggiorna per mostrare i dettagli del campo in questione. Selezionare **[!UICONTROL Back]** al termine dell&#39;anteprima per tornare alla finestra di dialogo di selezione del gruppo di campi.

![Anteprima della finestra di dialogo [!UICONTROL Preview field group] con il gruppo di campi Dettagli demografici.](../images/tutorials/create-schema/preview-field-group.png)

Per questo tutorial, seleziona il gruppo di campi **[!UICONTROL Demographic Details]**, quindi seleziona **[!UICONTROL Add field group]**.

![La finestra di dialogo [!UICONTROL Add field groups] con il gruppo di campi Dettagli demografici selezionato ed evidenziato [!UICONTROL Add field groups].](../images/tutorials/create-schema/demographic-details.png)

Viene visualizzata di nuovo l’area di lavoro dello schema. Nella sezione **[!UICONTROL Field groups]** sono ora elencati &quot;[!UICONTROL Demographic Details]&quot; e nella sezione **[!UICONTROL Structure]** sono inclusi i campi con il contributo del gruppo di campi. È possibile selezionare il nome del gruppo di campi nella sezione **[!UICONTROL Field groups]** per evidenziare i campi specifici che fornisce all&#39;interno dell&#39;area di lavoro.

![Editor schema con gruppi di campi Dettagli demografici evidenziati.](../images/tutorials/create-schema/demographic-details-structure.png)

>[!NOTE]
>
>Nell&#39;Editor schema, le classi e i gruppi di campi standard (generati da Adobe) sono indicati con l&#39;icona lucchetto (![Un&#39;icona lucchetto.](/help/images/icons/lock-closed.png). Il lucchetto viene visualizzato nella barra a sinistra accanto al nome della classe o del gruppo di campi, nonché accanto a qualsiasi campo nel diagramma dello schema che fa parte di una risorsa generata dal sistema.
>
>![Editor schema con l&#39;icona lucchetto evidenziata](../images/ui/explore/padlock-icon-highlight.png)

Questo gruppo di campi contribuisce a diversi campi con il nome di livello principale `person` con il tipo di dati &quot;[!UICONTROL Person]&quot;. Questo gruppo di campi descrive informazioni su un individuo, tra cui nome, data di nascita e genere.

>[!NOTE]
>
>Tenere presente che i campi possono utilizzare tipi scalari, ad esempio stringa, numero intero, matrice o data, nonché qualsiasi tipo di dati, ovvero un gruppo di campi che rappresenta un concetto comune, definito all&#39;interno di [!DNL Schema Registry].

Il campo `name` ha un tipo di dati &quot;[!UICONTROL Full name]&quot;, il che significa che descrive un concetto comune e contiene campi secondari correlati al nome come nome, cognome, titolo di cortesia e suffisso.

Seleziona i diversi campi all’interno dell’area di lavoro per visualizzare eventuali campi aggiuntivi che contribuiscono alla struttura dello schema.

## Aggiungi altri gruppi di campi {#field-group-2}

È ora possibile ripetere gli stessi passaggi per aggiungere un altro gruppo di campi. Quando questa volta visualizzi la finestra di dialogo **[!UICONTROL Add field group]**, noterai che il gruppo di campi &quot;[!UICONTROL Demographic Details]&quot; è stato disattivato e non è possibile selezionare la casella di controllo accanto ad esso. In questo modo si evita di duplicare accidentalmente i gruppi di campi già inclusi nello schema corrente.

Per questa esercitazione, selezionare i gruppi di campi standard **[!UICONTROL Personal Contact Details]** e **[!UICONTROL Loyalty Details]** dall&#39;elenco, quindi selezionare **[!UICONTROL Add field groups]** per aggiungerli allo schema.

![Finestra di dialogo [!UICONTROL Add field groups] con due nuovi gruppi di campi selezionati ed evidenziati [!UICONTROL Add field groups].](../images/tutorials/create-schema/more-field-groups.png)

L&#39;area di lavoro viene nuovamente visualizzata con i gruppi di campi aggiunti elencati in **[!UICONTROL Field groups]** nella sezione **[!UICONTROL Composition]** e i relativi campi compositi aggiunti alla struttura dello schema.

![Editor di schema con la nuova struttura di schema composita evidenziata.](../images/tutorials/create-schema/updated-structure.png)

## Definire un gruppo di campi personalizzato {#define-field-group}

Lo schema [!UICONTROL Loyalty Members] ha lo scopo di acquisire i dati relativi ai membri di un programma fedeltà e il gruppo di campi [!UICONTROL Loyalty Details] standard aggiunto allo schema fornisce la maggior parte di questi, inclusi il tipo di programma, i punti, la data di unione e altro ancora.

Tuttavia, potrebbe esserci uno scenario in cui desideri includere campi personalizzati aggiuntivi non coperti dai gruppi di campi standard per ottenere i casi d’uso. Se aggiungi campi fedeltà personalizzati, puoi scegliere tra due opzioni:

1. Crea un nuovo gruppo di campi personalizzato per acquisire questi campi. Questo è il metodo che verrà descritto in questa esercitazione.
1. Estendere il gruppo di campi [!UICONTROL Loyalty Details] standard con campi personalizzati. In questo modo [!UICONTROL Loyalty Details] verrà convertito in un gruppo di campi personalizzato e il gruppo di campi standard originale non sarà più disponibile. Per ulteriori informazioni sull&#39;aggiunta di [!UICONTROL Schemas]campi personalizzati alla struttura dei gruppi di campi standard[, consulta la guida dell&#39;interfaccia utente di &#x200B;](../ui/resources/schemas.md#custom-fields-for-standard-groups).

Per creare un nuovo gruppo di campi, seleziona **[!UICONTROL Add]** nella sottosezione **[!UICONTROL Field groups]** come prima, ma questa volta seleziona **[!UICONTROL Create New Field group]** nella parte superiore della finestra di dialogo visualizzata. Viene quindi richiesto di fornire un nome visualizzato e una descrizione per il nuovo gruppo di campi. Per questo tutorial, assegna al nuovo gruppo di campi il nome &quot;[!DNL Custom Loyalty Details]&quot;, quindi seleziona **[!UICONTROL Add field groups]**.

![La finestra di dialogo [!UICONTROL Add field groups] con [!UICONTROL Create new field group], [!UICONTROL Display name] e [!UICONTROL Description] è evidenziata.](../images/tutorials/create-schema/create-new-field-group.png)

>[!NOTE]
>
>Come per i nomi delle classi, il nome del gruppo di campi deve essere breve e semplice, e deve descrivere in che modo il gruppo di campi contribuirà allo schema. Anche queste sono univoche, pertanto non potrai riutilizzare il nome e devi assicurarti che sia sufficientemente specifico.

&quot;[!DNL Custom Loyalty Details]&quot; dovrebbe ora essere visualizzato in **[!UICONTROL Field groups]** sul lato sinistro dell&#39;area di lavoro, ma non sono ancora presenti campi associati ad essa e pertanto non verranno visualizzati nuovi campi in **[!UICONTROL Structure]**.

## Aggiungi campi al gruppo di campi {#field-group-fields}

Dopo aver creato il gruppo di campi &quot;[!DNL Custom Loyalty Details]&quot;, è ora di definire i campi che il gruppo di campi contribuirà allo schema.

Per iniziare, seleziona l&#39;icona **più (+)** accanto al nome dello schema nell&#39;area di lavoro.

![Editor di schema con l&#39;icona più evidenziata.](../images/tutorials/create-schema/add-field.png)

Nell&#39;area di lavoro viene visualizzato un segnaposto &quot;[!UICONTROL Untitled Field]&quot; e la barra a destra si aggiorna per visualizzare le opzioni di configurazione per il campo.

![Editor di schema con [!UICONTROL Untitled Field] e schema [!UICONTROL Field properties] evidenziati.](../images/tutorials/create-schema/untitled-field.png)

In questo scenario, lo schema deve avere un campo di tipo oggetto che descrive in dettaglio il livello di fedeltà corrente della persona. Utilizzando i controlli nella barra a destra, inizia a creare un campo `loyaltyTier` con tipo &quot;[!UICONTROL Object]&quot; che verrà utilizzato per contenere i campi correlati.

In **[!UICONTROL Assign to]** è necessario selezionare un gruppo di campi a cui assegnare il campo. Ricorda che tutti i campi dello schema appartengono a una classe o a un gruppo di campi e poiché questo schema utilizza una classe standard, l’unica opzione consiste nel selezionare un gruppo di campi. Inizia a digitare il nome &quot;[!DNL Custom Loyalty Details]&quot;, quindi seleziona il gruppo di campi dall&#39;elenco.

Al termine, selezionare **[!UICONTROL Apply]**.

![Editor schema con l&#39;oggetto livello fedeltà aggiunto allo schema [!UICONTROL Field properties] evidenziato.](../images/tutorials/create-schema/loyalty-tier-object.png)

Le modifiche vengono applicate e viene visualizzato l&#39;oggetto `loyaltyTier` appena creato. Poiché si tratta di un campo personalizzato, viene automaticamente nidificato all&#39;interno di un oggetto con spazio dei nomi all&#39;ID tenant dell&#39;organizzazione, preceduto da un carattere di sottolineatura (`_tenantId` in questo esempio).

![Editor schema con ID tenant e livello fedeltà evidenziati nel diagramma schema.](../images/tutorials/create-schema/tenant-id.png)

>[!NOTE]
>
>La presenza dell’oggetto ID tenant indica che i campi che stai aggiungendo sono contenuti nello spazio dei nomi della tua organizzazione.
>
>In altre parole, i campi che stai aggiungendo sono univoci per la tua organizzazione e verranno salvati in [!DNL Schema Registry] in un&#39;area specifica accessibile solo per la tua organizzazione. I campi definiti devono sempre essere aggiunti allo spazio dei nomi del tenant per evitare conflitti con i nomi di altre classi standard, gruppi di campi, tipi di dati e campi.

Per iniziare ad aggiungere i sottocampi, seleziona l&#39;icona **più (+)** accanto all&#39;oggetto `loyaltyTier`. Verrà visualizzato un nuovo segnaposto di campo e la sezione **[!UICONTROL Field properties]** sarà visibile sul lato destro dell&#39;area di lavoro.

![Editor schema con ID tenant e nuovo campo secondario aggiunto al livello fedeltà nel diagramma schema.](../images/tutorials/create-schema/new-field-in-loyalty-tier-object.png)

Ogni campo richiede le seguenti informazioni:

* **[!UICONTROL Field Name]:** Il nome del campo, preferibilmente scritto in CamelCase. Non sono consentiti spazi. Questo è il nome utilizzato per fare riferimento al campo nel codice e in altre applicazioni a valle.
   * Esempio: loyaltyLevel
* **[!UICONTROL Display Name]:** Il nome del campo, scritto in maiuscolo. Questo è il nome che verrà visualizzato nell’area di lavoro durante la visualizzazione o la modifica dello schema.
   * Esempio: livello di fedeltà
* **[!UICONTROL Type]:** Il tipo di dati del campo. Sono inclusi i tipi scalari di base e tutti i tipi di dati definiti in [!DNL Schema Registry]. Esempi: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone number], ecc.
* **[!UICONTROL Description]:** È necessario includere una descrizione facoltativa del campo con un massimo di 200 caratteri.

Il primo campo per l&#39;oggetto `loyaltyTier` sarà una stringa denominata `id`, che rappresenta l&#39;ID del livello corrente del membro fedeltà. L’ID del livello sarà univoco per ciascun membro fedeltà, poiché questa società imposta soglie di punti del livello fedeltà diverse per ciascun cliente in base a fattori diversi. Impostare il tipo del nuovo campo su &quot;[!UICONTROL String]&quot; e la sezione **[!UICONTROL Field properties]** viene compilata con diverse opzioni per l&#39;applicazione dei vincoli, inclusi il valore predefinito, il formato e la lunghezza massima. Per ulteriori informazioni, consulta la documentazione sulle [best practice per i campi di convalida dei dati](../schema/best-practices.md#data-validation-fields).

![Editor schema con i valori delle proprietà del campo per il nuovo campo ID evidenziato.](../images/tutorials/create-schema/string-constraints.png)

Poiché `id` sarà una stringa a forma libera generata in modo casuale, non sono necessari ulteriori vincoli. Seleziona **[!UICONTROL Apply]** per applicare le modifiche.

![Editor di schema con il campo ID aggiunto ed evidenziato.](../images/tutorials/create-schema/id-field-added.png)

## Aggiungi altri campi al gruppo di campi {#field-group-fields-2}

Dopo aver aggiunto il campo `id`, puoi aggiungere altri campi per acquisire informazioni sul livello fedeltà, ad esempio:

* Soglia punto corrente (numero intero): il numero minimo di punti fedeltà che il membro deve mantenere per rimanere nel livello corrente.
* Soglia punto livello successivo (numero intero): il numero di punti fedeltà che il membro deve accumulare per passare al livello successivo.
* Data di validità (data-ora): la data in cui il membro fedeltà è entrato a far parte del livello.

Per aggiungere ogni campo allo schema, seleziona l&#39;icona **più (+)** accanto all&#39;oggetto `loyalty` e compila le informazioni richieste.

Una volta completato, l&#39;oggetto `loyaltyTier` conterrà i campi per `id`, `currentThreshold`, `nextThreshold` e `effectiveDate`.

![Editor schema con l&#39;oggetto livello fedeltà evidenziato.](../images/tutorials/create-schema/loyalty-tier-object-fields.png)

## Aggiungere un campo enum al gruppo di campi {#enum}

Quando si definiscono i campi in [!DNL Schema Editor], è possibile applicare alcune opzioni aggiuntive ai tipi di campo di base per fornire ulteriori vincoli ai dati che il campo può contenere. I casi di utilizzo per questi vincoli sono illustrati nella tabella seguente:

| Vincolo | Descrizione |
| --- | --- |
| [!UICONTROL Required] | Indica che il campo è obbligatorio per l’acquisizione dei dati. Eventuali dati caricati in un set di dati basato su questo schema che non contengono questo campo non riusciranno al momento dell’acquisizione. |
| [!UICONTROL Array] | Indica che il campo contiene una matrice di valori, ciascuno con il tipo di dati specificato. Ad esempio, l&#39;utilizzo di questo vincolo su un campo con tipo di dati &quot;[!UICONTROL String]&quot; specifica che il campo conterrà una matrice di stringhe. |
| [!UICONTROL Enum & Suggested Values] | Un enum indica che questo campo deve contenere uno dei valori di un elenco enumerato di valori possibili. In alternativa, è possibile utilizzare questa opzione solo per fornire un elenco di valori suggeriti per un campo stringa senza vincolare il campo a tali valori. |
| [!UICONTROL Identity] | Indica che questo campo è un campo di identità. Ulteriori informazioni sui campi di identità sono fornite [più avanti in questa esercitazione](#identity-field). |
| [!UICONTROL Relationship] | Sebbene sia possibile dedurre le relazioni tra schemi tramite lo schema di unione e [!DNL Real-Time Customer Profile], questo vale solo per gli schemi che condividono la stessa classe. Il vincolo [!UICONTROL Relationship] indica che questo campo fa riferimento all&#39;identità primaria di uno schema basato su una classe diversa, il che implica una relazione tra i due schemi. Per ulteriori informazioni, vedere il tutorial su [definizione di una relazione](./relationship-ui.md). |

{style="table-layout:auto"}

>[!NOTE]
>
>Tutti i campi obbligatori, di identità o di relazione sono elencati nelle rispettive sezioni nella barra a sinistra, consentendo di individuare facilmente tali campi indipendentemente dalla complessità dello schema.

Per questa esercitazione, l&#39;oggetto `loyaltyTier` nello schema richiede un nuovo campo enum che descrive la classe di livello, in cui il valore può essere solo una delle quattro opzioni possibili. Per aggiungere questo campo allo schema, seleziona l&#39;icona **più (+)** accanto all&#39;oggetto `loyaltyTier` e compila i campi obbligatori per **[!UICONTROL Field name]** e **[!UICONTROL Display name]**. Per **[!UICONTROL Type]**, selezionare &quot;[!UICONTROL String]&quot;.

![Editor schema con l&#39;oggetto classe livello aggiunto ed evidenziato in [!UICONTROL Field properties].](../images/tutorials/create-schema/tier-class-type.png)

Dopo la selezione del tipo di campo vengono visualizzate ulteriori caselle di controllo, incluse quelle per **[!UICONTROL Array]**, **[!UICONTROL Enum & Suggested Values]**, **[!UICONTROL Identity]** e **[!UICONTROL Relationship]**.

Selezionare la casella di controllo **[!UICONTROL Enum & Suggested Values]**, quindi selezionare **[!UICONTROL Enum]**. Qui puoi immettere **[!UICONTROL Value]** (in camelCase) e **[!UICONTROL Display Name]** (un nome facoltativo e facile da leggere in Title Case) per ogni classe di livello fedeltà accettabile.

Dopo aver completato tutte le proprietà del campo, selezionare **[!UICONTROL Apply]** per aggiungere il campo `tierClass` all&#39;oggetto `loyaltyTier`.

![Proprietà dei campi enum e valori suggeriti completate con [!UICONTROL Apply] evidenziato.](../images/tutorials/create-schema/tier-class-enum.png)

## Convertire un oggetto multicampo in un tipo di dati {#datatype}

L&#39;oggetto `loyaltyTier` contiene ora diversi campi e rappresenta una struttura di dati comune che potrebbe essere utile in altri schemi. [!DNL Schema Editor] consente di applicare rapidamente oggetti multifampo riutilizzabili convertendo la struttura di tali oggetti in tipi di dati.

I tipi di dati consentono l’utilizzo coerente di strutture a più campi e forniscono maggiore flessibilità rispetto a un gruppo di campi, perché possono essere utilizzati ovunque all’interno di uno schema. Questa operazione viene eseguita impostando il valore **[!UICONTROL Type]** del campo su quello di qualsiasi tipo di dati definito in [!DNL Schema Registry].

Per convertire l&#39;oggetto `loyaltyTier` in un tipo di dati, selezionare il campo `loyaltyTier` nell&#39;area di lavoro, quindi selezionare **[!UICONTROL Convert to new data type]** sul lato destro dell&#39;editor in **[!UICONTROL Field properties]**.

![Editor schema con l&#39;oggetto loyaltyTier e [!UICONTROL Convert to new data type] evidenziato.](../images/tutorials/create-schema/convert-data-type.png)

Viene visualizzata una notifica che conferma che l&#39;oggetto è stato convertito correttamente. Nell&#39;area di lavoro è ora possibile vedere che il campo `loyaltyTier` contiene un&#39;icona di collegamento e la barra a destra indica che il tipo di dati è &quot;[!DNL Loyalty Tier]&quot;.

![Editor schema con l&#39;oggetto loyaltyTier e il nuovo nome visualizzato evidenziato.](../images/tutorials/create-schema/loyalty-tier-data-type.png)

In uno schema futuro, è ora possibile assegnare un campo come tipo &quot;[!DNL Loyalty Tier]&quot; e includerebbe automaticamente campi per ID, classe livello, soglie punto e data di validità.

>[!NOTE]
>
>Puoi anche creare e modificare tipi di dati personalizzati in modo indipendente dalla modifica degli schemi. Per ulteriori informazioni, consulta la guida sulla [creazione e modifica di tipi di dati](../ui/resources/data-types.md).

## Cercare e filtrare i campi dello schema

Lo schema ora contiene diversi gruppi di campi oltre ai campi forniti dalla relativa classe base. Quando si utilizzano schemi di grandi dimensioni, è possibile selezionare le caselle di controllo accanto ai nomi dei gruppi di campi nella barra a sinistra per filtrare i campi visualizzati solo in base a quelli forniti dai gruppi di campi desiderati.

![Alcune caselle di controllo sono state selezionate nella sezione Gruppi di campi dell&#39;Editor schema per ridurre le dimensioni del diagramma schema.](../images/tutorials/create-schema/filter-by-field-group.png)

Se cerchi un campo specifico nello schema, puoi anche utilizzare la barra di ricerca per filtrare i campi visualizzati per nome, indipendentemente dal gruppo di campi in cui vengono forniti.

![Campo di ricerca dell&#39;editor di schemi con i risultati rilevanti evidenziati nell&#39;area di lavoro.](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La funzione di ricerca tiene conto di tutti i filtri dei gruppi di campi selezionati durante la visualizzazione dei campi corrispondenti. Se in una query di ricerca non vengono visualizzati i risultati previsti, potrebbe essere necessario verificare che non si stia filtrando alcun gruppo di campi rilevante.

## Impostare un campo schema come campo identità {#identity-field}

La struttura dati standard fornita dagli schemi può essere utilizzata per identificare i dati appartenenti alla stessa persona da più origini, consentendo vari casi di utilizzo a valle come segmentazione, reporting, analisi della scienza dei dati e altro ancora. Per unire i dati in base alle identità individuali, i campi chiave devono essere contrassegnati come [!UICONTROL Identity] campi all&#39;interno degli schemi applicabili.

[!DNL Experience Platform] consente di identificare facilmente un campo di identità tramite l&#39;utilizzo di una casella di controllo **[!UICONTROL Identity]** in [!DNL Schema Editor]. Tuttavia, devi determinare quale campo è il candidato migliore da utilizzare come identità, in base alla natura dei tuoi dati.

Ad esempio, possono esserci migliaia di membri del programma fedeltà appartenenti allo stesso livello fedeltà e diversi che possono condividere lo stesso indirizzo fisico. In questo scenario, tuttavia, al momento dell’iscrizione ogni membro del programma fedeltà fornisce il proprio indirizzo e-mail personale. Poiché gli indirizzi e-mail personali sono in genere gestiti da una sola persona, il campo `personalEmail.address` (fornito dal gruppo di campi [!UICONTROL Personal Contact Details]) è un buon candidato per un campo di identità.

>[!IMPORTANT]
>
>I passaggi descritti di seguito descrivono come aggiungere un descrittore di identità a un campo schema esistente. In alternativa alla definizione di campi di identità all&#39;interno della struttura dello schema stesso, è possibile utilizzare un campo `identityMap` per contenere informazioni sull&#39;identità.
>
>Se prevedi di utilizzare `identityMap`, tieni presente che sostituirà qualsiasi identità primaria aggiunta direttamente allo schema. Per ulteriori informazioni, vedere la sezione su `identityMap` nella [guida di base per la composizione dello schema](../schema/composition.md#identityMap).

Selezionare il campo `personalEmail.address` nell&#39;area di lavoro e la casella di controllo **[!UICONTROL Identity]** verrà visualizzata in **[!UICONTROL Field properties]**. Selezionare la casella e l&#39;opzione per impostare la visualizzazione di **[!UICONTROL Primary identity]**. Seleziona anche questa casella.

>[!NOTE]
>
>Ogni schema può contenere un solo campo di identità principale. Una volta impostato un campo schema come identità primaria, se in seguito tenti di impostare un altro campo identità nello schema come principale, riceverai un messaggio di errore.

Successivamente, devi fornire **[!UICONTROL Identity namespace]** dall&#39;elenco di spazi dei nomi predefiniti nel menu a discesa. Poiché questo campo è l&#39;indirizzo e-mail del cliente, seleziona &quot;[!UICONTROL Email]&quot; dal menu a discesa. Selezionare **[!UICONTROL Apply]** per confermare gli aggiornamenti al campo `personalEmail.address`.

![Editor schema con l&#39;indirizzo di posta elettronica evidenziato e la casella di controllo Identità primaria abilitata.](../images/tutorials/create-schema/primary-identity.png)

>[!NOTE]
>
>Per un elenco degli spazi dei nomi standard e delle relative definizioni, consulta la [[!DNL Identity Service] documentazione](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Dopo aver applicato la modifica, l&#39;icona di `personalEmail.address` mostra un simbolo di impronta digitale che indica che si tratta di un campo di identità. Il campo è inoltre elencato nella barra a sinistra in **[!UICONTROL Identities]**.

![Editor schema con indirizzo e-mail evidenziato e campo identità evidenziato nella barra laterale della composizione dello schema.](../images/tutorials/create-schema/identity-applied.png)

Ora tutti i dati acquisiti nel campo `personalEmail.address` verranno utilizzati per identificare l&#39;individuo e unire una singola visualizzazione di quel cliente. Per ulteriori informazioni sull&#39;utilizzo delle identità in [!DNL Experience Platform], consultare la documentazione di [[!DNL Identity Service]](../../identity-service/home.md).

## Abilita lo schema da utilizzare in [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) sfrutta i dati di identità in [!DNL Experience Platform] per fornire una visualizzazione olistica di ogni singolo cliente. Il servizio crea profili robusti a 360° degli attributi del cliente e account con marca temporale di ogni interazione che i clienti hanno avuto in qualsiasi sistema integrato con [!DNL Experience Platform].

Affinché uno schema possa essere abilitato per l&#39;utilizzo con [!DNL Real-Time Customer Profile], deve avere un&#39;identità primaria definita. Riceverai un messaggio di errore se tenti di abilitare uno schema senza prima definire un’identità primaria.

![Finestra di dialogo dell&#39;identità primaria mancante.](../images/tutorials/create-schema/missing-primary-identity.png)

Per abilitare lo schema &quot;Membri fedeltà&quot; per l&#39;utilizzo in [!DNL Profile], selezionare innanzitutto il titolo dello schema nell&#39;area di lavoro.

Sul lato destro dell’editor vengono visualizzate informazioni sullo schema, tra cui il nome visualizzato, la descrizione e il tipo. Oltre a queste informazioni, è disponibile un pulsante di attivazione/disattivazione **[!UICONTROL Profile]**.

![Editor di schema con radice dello schema e interruttore Abilita per profilo evidenziati.](../images/tutorials/create-schema/profile-toggle.png)

Selezionare **[!UICONTROL Profile]** e viene visualizzata una finestra a comparsa con la richiesta di confermare che si desidera abilitare lo schema per [!DNL Profile].

![Finestra di dialogo Abilita per conferma profilo.](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>Una volta abilitato e salvato uno schema per [!DNL Real-Time Customer Profile], non è possibile disattivarlo.

Seleziona **[!UICONTROL Enable]** per confermare la scelta. È possibile selezionare di nuovo l&#39;interruttore **[!UICONTROL Profile]** per disabilitare lo schema, ma una volta che lo schema è stato salvato mentre [!DNL Profile] è abilitato, non può più essere disabilitato.

## Altre azioni {#more}

Nell’Editor di schema è inoltre possibile eseguire azioni rapide per copiare la struttura JSON dello schema o eliminare lo schema. Seleziona [!UICONTROL More] nella parte superiore della visualizzazione per visualizzare un elenco a discesa con azioni rapide.

![Editor schema con il pulsante Altro evidenziato e le opzioni dell&#39;elenco a discesa visualizzate.](../images/tutorials/create-schema/more-actions.png)

### Eliminare uno schema {#delete-a-schema}

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_profileenabledwithdatasets"
>title="Impossibile eliminare lo schema"
>abstract="Impossibile eliminare lo schema perché è stato abilitato per il profilo e presenta set di dati associati."

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_profileenablednodatasets"
>title="Impossibile eliminare lo schema"
>abstract="Impossibile eliminare lo schema perché è stato abilitato per il profilo."

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_withdatasetsnotprofileenabled"
>title="Impossibile eliminare lo schema"
>abstract="Impossibile eliminare lo schema perché presenta set di dati associati."

Uno schema può essere eliminato all&#39;interno dell&#39;interfaccia utente dall&#39;Editor di schema utilizzando le azioni [!UICONTROL More] e anche dai dettagli dello schema nella scheda [!UICONTROL Browse]. Esistono alcune condizioni che impediscono l’eliminazione di uno schema. Uno schema non può essere eliminato se:

* Lo schema è abilitato per il profilo.
* Lo schema è abilitato per Profilo e dispone di set di dati associati.
* Lo schema ha set di dati associati ma non è abilitato per il profilo.

### Copia struttura JSON {#copy-json-structure}

Selezionare **[!UICONTROL Copy JSON structure]** per generare un payload di esportazione per qualsiasi schema nella raccolta schemi. Questa azione copia la struttura JSON negli Appunti. Il JSON esportato può quindi essere utilizzato per importare lo schema e tutte le risorse correlate in una sandbox o organizzazione diversa. In questo modo la condivisione e il riutilizzo degli schemi tra ambienti diversi diventano semplici ed efficienti.

## Passaggi successivi e risorse aggiuntive

Dopo aver composto lo schema, nell’area di lavoro puoi vedere lo schema completo. Selezionare **[!UICONTROL Save]** e lo schema verrà salvato in [!DNL Schema Library], rendendolo accessibile da [!DNL Schema Registry].

Ora è possibile utilizzare il nuovo schema per acquisire dati in [!DNL Experience Platform]. Ricorda che una volta utilizzato lo schema per acquisire i dati, è possibile apportare solo modifiche aggiuntive. Per ulteriori informazioni sul controllo delle versioni dello schema, vedere le [nozioni di base sulla composizione dello schema](../schema/composition.md).

Ora puoi seguire l&#39;esercitazione su [definizione di una relazione di schema nell&#39;interfaccia utente](./relationship-ui.md) per aggiungere un nuovo campo di relazione allo schema &quot;Membri fedeltà&quot;.

È inoltre disponibile lo schema &quot;Membri fedeltà&quot; per la visualizzazione e la gestione tramite l&#39;API [!DNL Schema Registry]. Per iniziare a utilizzare l&#39;API, inizia leggendo la [[!DNL Schema Registry API] guida per gli sviluppatori](../api/getting-started.md).

### Risorse video

>[!WARNING]
>
>L&#39;interfaccia utente di [!DNL Experience Platform] mostrata nei video seguenti non è aggiornata. Per le schermate e le funzionalità più recenti dell’interfaccia utente, consulta la documentazione precedente.

Nel video seguente viene illustrato come creare uno schema semplice nell&#39;interfaccia utente [!DNL Experience Platform].

>[!VIDEO](https://video.tv.adobe.com/v/3430219?captions=ita&quality=12&learn=on)

Il video seguente ha lo scopo di rafforzare la tua comprensione del lavoro con i gruppi di campo e le classi.

>[!VIDEO](https://video.tv.adobe.com/v/3413602?captions=ita&quality=12&learn=on)

## Appendice

Nelle sezioni seguenti vengono fornite informazioni aggiuntive sull&#39;utilizzo di [!DNL Schema Editor].

### Crea una nuova classe {#create-new-class}

[!DNL Experience Platform] offre la flessibilità necessaria per definire uno schema basato su una classe univoca per la tua organizzazione. Per informazioni su come creare una nuova classe, consulta la guida su [creazione e modifica di classi nell&#39;interfaccia utente](../ui/resources/classes.md#create).

### Modificare la classe di uno schema {#change-class}

È possibile modificare la classe di uno schema in qualsiasi momento durante il processo di composizione iniziale prima che lo schema sia stato salvato.

>[!WARNING]
>
>La riassegnazione della classe per uno schema deve essere eseguita con estrema cautela. I gruppi di campi sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà l’area di lavoro e tutti i campi aggiunti.

Per informazioni su come modificare la classe di uno schema, consulta la guida su [gestione degli schemi nell&#39;interfaccia utente](../ui/resources/schemas.md#change-class).
