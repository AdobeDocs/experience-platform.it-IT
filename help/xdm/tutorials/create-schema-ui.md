---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare uno schema tramite l’Editor di schema.
topic: tutorials
translation-type: tm+mt
source-git-commit: d55dc9776968099901325c58506c5e322449368e
workflow-type: tm+mt
source-wordcount: '3462'
ht-degree: 0%

---


# Creare uno schema tramite l’Editor di schema.

Il Registro di sistema dello schema fornisce un&#39;interfaccia utente e RESTful API da cui è possibile visualizzare e gestire tutte le risorse nella  Libreria schema Adobe Experience Platform. La Libreria schema contiene le risorse rese disponibili da Adobe,  partner Experience Platform e fornitori le cui applicazioni vengono utilizzate, nonché le risorse definite e salvate nel Registro di sistema dello schema.

Questa esercitazione descrive i passaggi necessari per creare uno schema utilizzando l&#39;Editor di schema in  Experience Platform. Se si preferisce comporre uno schema utilizzando l&#39;API del Registro di sistema dello schema, iniziare leggendo la guida [per lo sviluppatore del Registro di](../api/getting-started.md) schema prima di provare a [creare uno schema utilizzando l&#39;API](create-schema-api.md).

Questa esercitazione include anche i passaggi per [definire una nuova classe](#create-new-class) da utilizzare per comporre uno schema.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari aspetti del Adobe Experience Platform  coinvolto nell&#39;utilizzo dell&#39;Editor di schema. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti concetti:

* [Experience Data Model (XDM)](../home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.
* [Nozioni di base sulla composizione](../schema/composition.md)dello schema: Panoramica degli schemi XDM e dei relativi blocchi costitutivi, incluse classi, mixin, tipi di dati e campi.
* [Profilo](../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Questa esercitazione richiede l&#39;accesso a  Experience Platform. Se non disponete dell&#39;accesso a un&#39;organizzazione IMS in  Experience Platform, rivolgetevi al vostro amministratore di sistema prima di procedere.

## Sfogliare gli schemi esistenti nell’area di lavoro Schemi {#browse}

L&#39;area di lavoro Schemi all&#39;interno  Experience Platform fornisce una visualizzazione della Libreria schema, consentendo di visualizzare e gestire tutti gli schemi disponibili e di comporne di nuovi. L&#39;area di lavoro include anche l&#39;Editor schema, l&#39;area di lavoro su cui verrà composto uno schema durante l&#39;esercitazione.

Dopo aver effettuato l&#39;accesso  Experience Platform, fate clic su **Schemi** nella barra di navigazione a sinistra per passare all&#39;area di lavoro Schemi. Viene visualizzato un elenco di schemi (una rappresentazione della Libreria schemi) in cui è possibile visualizzare, gestire e personalizzare tutti gli schemi disponibili. L&#39;elenco include il nome, il tipo, la classe e il comportamento (record o serie temporali) su cui si basa lo schema, nonché la data e l&#39;ora dell&#39;ultima modifica dello schema.

Fate clic sull’icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per tutte le risorse del Registro di sistema, incluse classi, mixin e tipi di dati.

![Visualizzazione della libreria Schema](../images/tutorials/create-schema/schemas_filter.png)

## Creare e assegnare un nome a uno schema {#create}

Per iniziare a comporre uno schema, fare clic su **Crea schema** nell&#39;angolo superiore destro dell&#39;area di lavoro Schemi.

![Pulsante Crea schema](../images/tutorials/create-schema/create_schema_button.png)

Viene visualizzato l&#39;Editor ** schema. Questo è il quadro su cui si compone lo schema. Quando si arriva all&#39;editor, viene automaticamente creato uno &quot;Schema senza titolo&quot; nella sezione *Struttura* del quadro per consentirvi di iniziare a personalizzare.

![Editor di schema](../images/tutorials/create-schema/schema_editor.png)

Sul lato destro dell&#39;editor si trovano le proprietà ** dello schema in cui è possibile specificare un nome per lo schema (utilizzando il campo Nome **** visualizzato). Una volta inserito un nome, il quadro si aggiorna per riflettere il nuovo nome dello schema.

![Area di lavoro schema](../images/tutorials/create-schema/name_schema.png)

Quando si decide un nome per lo schema, è necessario tenere presenti diverse considerazioni importanti:

* I nomi dello schema devono essere brevi e descrittivi in modo che lo schema possa essere facilmente trovato nella libreria in un secondo momento.
* I nomi degli schemi devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro. Ad esempio, se l&#39;organizzazione dispone di programmi di fedeltà separati per marchi diversi, sarebbe opportuno assegnare al proprio schema il nome &quot;Marca A Fedeltà Membri&quot; in modo da distinguere facilmente gli altri schemi di fedeltà che si potrebbero definire in seguito.
* Facoltativamente, è possibile fornire informazioni aggiuntive sullo schema utilizzando il campo **Descrizione** .

Questa esercitazione costituisce uno schema per l&#39;acquisizione di dati relativi ai membri di un programma fedeltà, pertanto lo schema è denominato &quot;Membri fedeltà&quot;.

## Assegnazione di una classe {#class}

Sul lato sinistro dell&#39;editor è presente la sezione *Composizione* . Attualmente contiene due sottosezioni: *Schema* e *classe*.

Ora che lo schema ha un nome, è ora di assegnare la classe che lo schema implementerà. Fare clic su **Assegna** accanto a *Classe*.

![](../images/tutorials/create-schema/assign_class_button.png)

Viene visualizzata la finestra di dialogo *Assegna classe* . In questa finestra viene visualizzato un elenco di tutte le classi disponibili, incluse quelle definite dall&#39;organizzazione (il proprietario è &quot;Cliente&quot;), nonché le classi standard definite da Adobe.

Fate clic sul nome della classe per visualizzare la descrizione della classe. Potete anche scegliere di **visualizzare in anteprima la struttura** delle classi per visualizzare i campi e i metadati associati alla classe.

Questa esercitazione utilizza la classe Profilo singolo XDM. Fare clic sul pulsante di scelta accanto alla classe per selezionarla, quindi fare clic su **Assegna classe**.

![Finestra di dialogo Assegna classe](../images/tutorials/create-schema/assign_class.png)

Il quadro viene nuovamente visualizzato. La sezione *Classe* ora contiene la classe selezionata (Profilo singolo XDM) e i campi forniti dalla classe Profilo singolo XDM sono ora visibili nella sezione *Struttura* .

![Classe profilo singolo XDM assegnata](../images/tutorials/create-schema/class_assigned_structure.png)

I campi vengono visualizzati nel formato &quot;fieldName&quot; | Tipo di dati&quot;. I passaggi per definire i campi dello schema nell&#39;interfaccia utente sono disponibili più avanti in questa esercitazione.

>[!NOTE]
>
>È possibile [modificare la classe di uno schema](#change-class) in qualsiasi momento durante il processo di composizione iniziale prima che lo schema sia stato salvato, ma questo deve essere fatto con estrema cautela. I mixin sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà il quadro ed eventuali campi aggiunti.

## Aggiungere un mixin {#mixin}

Ora che è stata assegnata una classe, la sezione *Composizione* contiene una terza sottosezione: *Mixin*.

È ora possibile iniziare ad aggiungere campi allo schema aggiungendo mixin. Un mixin è un gruppo di uno o più campi che descrivono un concetto particolare. Questa esercitazione utilizza i mixin per descrivere i membri del programma fedeltà e acquisire informazioni chiave come nome, compleanno, numero di telefono, indirizzo e molto altro.

Per aggiungere un mixin, fate clic su **Aggiungi** nella sottosezione *Mixins* .

![](../images/tutorials/create-schema/add_mixin_button.png)

Viene visualizzata la finestra di dialogo *Aggiungi mixin* . Le miscele sono destinate solo a classi specifiche, pertanto l&#39;elenco dei mixin mostra solo quelle compatibili con la classe selezionata (in questo caso, la classe di profilo individuale XDM).

Se si seleziona il pulsante di scelta accanto a un mixin, sarà possibile visualizzare l’ **anteprima della struttura** del mixin. Selezionate il mixin &quot;Dettagli persona profilo&quot;, quindi fate clic su **Aggiungi mixin**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Lo schema quadro viene nuovamente visualizzato. La sezione *Mixins* ora elenca il mixin &quot;Profile Person Details&quot; (Dettagli persona profilo) e la sezione *Struttura* include i campi forniti dal mixin.

![](../images/tutorials/create-schema/person_details_structure.png)

Questo mixin fornisce diversi campi sotto il nome di primo livello &quot;persona&quot; con il tipo di dati &quot;Persona&quot;. Questo gruppo di campi descrive informazioni su un individuo, quali nome, data di nascita e genere.

>[!NOTE]
>
>Tenere presente che i campi possono utilizzare tipi scalari (come stringa, integer, array o data) come tipo di dati, nonché qualsiasi &quot;tipo di dati&quot; (un gruppo di campi che rappresenta un concetto comune) nel Registro di sistema dello schema.

Il campo &quot;nome&quot; ha un tipo di dati &quot;Nome persona&quot;, che significa che descrive anche un concetto comune e contiene campi secondari relativi al nome come nome, cognome e nome completo.

Fare clic su campi diversi all&#39;interno del quadro per visualizzare tutti i campi aggiuntivi che contribuiscono alla struttura dello schema.

## Aggiungere un altro mixin {#mixin-2}

Ora potete ripetere gli stessi passaggi per aggiungere un altro mixin. Quando visualizzate la finestra di dialogo *Aggiungi mixin* , il mixin &quot;Dettagli persona profilo&quot; è stato disattivato e il pulsante di scelta accanto non può essere selezionato. Ciò impedisce la duplicazione accidentale di mixin già inclusi nello schema corrente.

È ora possibile aggiungere il mixin &quot;Dettagli personali profilo&quot; dalla finestra di dialogo *Aggiungi mixin* .

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Una volta aggiunto, il quadro viene nuovamente visualizzato. I &quot;Dettagli personali profilo&quot; ora sono elencati in *Mixins* nella sezione *Composizione* , e i campi per l&#39;indirizzo della casa, il telefono cellulare e altro ancora sono stati aggiunti in *Struttura*.

Analogamente al campo &quot;nome&quot;, i campi appena aggiunti rappresentano concetti relativi a più campi. Ad esempio, &quot;homeAddress&quot; ha un tipo di dati &quot;Address&quot; e &quot;mobilePhone&quot; ha un tipo di dati &quot;Phone Number&quot;. È possibile fare clic su ciascuno di questi campi per espanderli e visualizzare i campi aggiuntivi inclusi nel tipo di dati.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Definire un nuovo mixin {#define-mixin}

Lo schema &quot;Membri fedeltà&quot; è concepito per acquisire i dati relativi ai membri di un programma fedeltà, pertanto richiederà alcuni campi specifici relativi alla fedeltà. Non sono disponibili mixin standard che contengono i campi necessari, pertanto sarà necessario definire un nuovo mixin.

Questa volta, quando aprite la finestra di dialogo *Aggiungi mixin* , selezionate **Crea nuovo mixin**. Vi verrà quindi chiesto di fornire un Nome **** visualizzato e una **Descrizione** per il mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Come per i nomi delle classi, il nome del mixin deve essere breve e semplice, descrivendo il contributo del mixin allo schema. Anche questi sono univoci, quindi non sarà possibile riutilizzare il nome e quindi dovrà essere sicuro che sia sufficientemente specifico.

Per questa esercitazione, denominate il nuovo mixin &quot;Dettagli fedeltà&quot;.

Fare clic su **Aggiungi mixin** per tornare all&#39;editor dello schema. &quot;Dettagli fedeltà&quot; dovrebbe ora essere visualizzato in *Mixins* sul lato sinistro del quadro, ma non ci sono ancora campi associati ad esso e quindi nessun nuovo campo viene visualizzato in *Struttura*.

## Aggiunta di campi al mixin {#mixin-fields}

Dopo aver creato il mixin &quot;Dettagli fedeltà&quot;, è ora di definire i campi che il mixin contribuirà allo schema.

Per iniziare, fate clic sul nome del mixin nella sezione *Mixins* . A tale scopo, *le proprietà* mixin verranno visualizzate a destra dell’editor e accanto al nome dello schema in **Struttura** verrà visualizzato un pulsante *Aggiungi campo*.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Fate clic su **Aggiungi campo** accanto a &quot;Membri fedeltà&quot; per creare un nuovo nodo nella struttura. Questo nodo (denominato &quot;_tenantId&quot; in questo esempio) rappresenta l&#39;ID tenant dell&#39;organizzazione IMS, preceduto da un carattere di sottolineatura. La presenza dell&#39;ID tenant indica che i campi che si sta aggiungendo sono contenuti nello spazio dei nomi dell&#39;organizzazione.

In altre parole, i campi che si stanno aggiungendo sono univoci per la propria organizzazione e verranno salvati nel Registro di sistema dello schema in un&#39;area specifica accessibile solo all&#39;organizzazione IMS. I campi definiti devono sempre essere aggiunti allo spazio nomi per evitare conflitti con nomi di altre classi, mixin, tipi di dati e campi standard.

All&#39;interno di tale nodo con nome è presente un &quot;Nuovo campo&quot;. Questo è l&#39;inizio del mixin &quot;Dettagli fedeltà&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Utilizzando Proprietà ** campo a destra dell’editor, potete iniziare creando un campo &quot;fedeltà&quot; con il tipo &quot;Oggetto&quot; che verrà utilizzato per contenere i campi relativi alla fedeltà. Al termine, fate clic su **Applica**.

![](../images/tutorials/create-schema/loyalty_object.png)

Le modifiche vengono applicate e viene visualizzato l&#39;oggetto &quot;fedeltà&quot; appena creato. Fate clic su **Aggiungi campo** accanto all’oggetto per aggiungere altri campi relativi alla fedeltà. Viene visualizzato un &quot;Nuovo campo&quot; e la sezione Proprietà ** campo è visibile sul lato destro del quadro.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Ogni campo richiede le seguenti informazioni:

* **Nome campo:** Nome del campo, scritto in cammello. Esempio: loyaltyLevel
* **Nome visualizzato:** Il nome del campo, scritto nel caso del titolo. Esempio: Livello fedeltà
* **Tipo:** Il tipo di dati del campo. Ciò include tipi scalari di base e qualsiasi tipo di dati definito nel Registro di sistema dello schema. Esempi: stringa, numero intero, booleano, Persona, Indirizzo, Numero di telefono, ecc.
* **Descrizione:** Deve essere inclusa una descrizione facoltativa del campo, scritta in caso di frase. (massimo 200 caratteri)

Il primo campo per l&#39;oggetto Fedeltà sarà una stringa denominata &quot;loyaltyId&quot;. Quando si imposta il nuovo tipo di campo su &quot;Stringa&quot;, la finestra Proprietà *campo viene compilata con diverse opzioni per l&#39;applicazione di vincoli, tra cui Valore* **predefinito,** Formato **e Lunghezza****** massima.

![](../images/tutorials/create-schema/string_constraints.png)

Sono disponibili diverse opzioni di vincolo a seconda del tipo di dati selezionato. Poiché &quot;fedeltàId&quot; sarà un indirizzo e-mail, selezionate &quot;email&quot; dal menu a discesa **Formato** . Selezionate **Applica** per applicare le modifiche.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Aggiunta di altri campi al mixin {#mixin-fields-2}

Ora che avete aggiunto il campo &quot;loyaltyId&quot;, potete aggiungere altri campi per acquisire informazioni relative alla fedeltà come:

* Points (Integer)
* Membro da (data)

Per aggiungere ogni campo, fare clic su **Aggiungi campo** nell&#39;oggetto fedeltà e compilare le informazioni richieste.

Al termine, l&#39;oggetto Fedeltà conterrà campi per: ID fedeltà, punti e membro da.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Aggiungi il campo &#39;enum&#39; al mixin {#enum}

Durante la definizione dei campi nell&#39;Editor schema, è possibile applicare alcune opzioni aggiuntive ai tipi di campo di base per creare ulteriori vincoli sui dati che il campo può contenere.

Un esempio di questo è rappresentato da un campo &quot;Livello fedeltà&quot;, in cui il valore può essere solo una delle quattro opzioni possibili. Per aggiungere questo campo allo schema, fare clic su **Aggiungi campo** accanto all&#39;oggetto &quot;fedeltà&quot; e compilare i campi richiesti in Proprietà ** campo.

Per **Tipo**, selezionate &quot;Stringa&quot; e verranno visualizzate caselle di controllo aggiuntive per **Array**, **Enum** e **Identità**.

Selezionare la casella di controllo **Enum** per aprire la sezione Valori ** Enum di seguito. Qui è possibile inserire il **valore** (in camelCase) e **Label** (un nome opzionale, intuitivo e leggibile in Title Case) per ogni livello di fedeltà accettabile.

Una volta completate tutte le proprietà del campo, fare clic su **Applica** e il campo &quot;loyaltyLevel&quot; verrà aggiunto all&#39;oggetto &quot;fedeltà&quot;.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Ulteriori informazioni sui vincoli aggiuntivi disponibili:

* **Obbligatorio:** Indica che il campo è obbligatorio per l&#39;inserimento dei dati. Eventuali dati caricati in un dataset basato su questo schema che non contiene questo campo avranno esito negativo al momento dell&#39;inserimento.
* **Array:** Indica che il campo contiene un array di valori, ciascuno con il tipo di dati specificato. Ad esempio, se si seleziona un tipo di dati &quot;String&quot; e si seleziona la casella di controllo &quot;Array&quot;, il campo conterrà un array di stringhe.
* **Enum:** Indica che questo campo deve contenere uno dei valori di un elenco enumerato di possibili valori.
* **Identità:** Indica che questo campo è un campo identità. Ulteriori informazioni sui campi di identità sono disponibili [più avanti in questa esercitazione](#identity-field).

## Conversione di un oggetto multicampo in un tipo di dati {#datatype}

Dopo aver aggiunto diversi campi specifici per la fedeltà, l&#39;oggetto &quot;fedeltà&quot; ora contiene una struttura dati comune che potrebbe essere utile in altri schemi.

Se si ritiene che una struttura multi-campo possa essere riutilizzabile e si desidera avere la flessibilità di utilizzare la stessa struttura di dati altrove, l&#39;Editor schema consente di convertire tale struttura in un tipo di dati.

I tipi di dati consentono l&#39;uso coerente di strutture con più campi e offrono maggiore flessibilità rispetto a un mixin, perché possono essere utilizzati ovunque all&#39;interno di uno schema. A tal fine, imposta il **Tipo** di un campo di un mixin su quello di qualsiasi tipo di dati definito nel registro.

Per convertire l&#39;oggetto &quot;fedeltà&quot; in un tipo di dati, fare clic sul campo &quot;fedeltà&quot; in *Struttura* e selezionare **Converti in nuovo tipo** di dati a destra dell&#39;editor in Proprietà ** campo. Viene visualizzato un piccolo pop-up verde che conferma &quot;Oggetto convertito in Tipo di dati&quot;.

Ora, quando si guarda in *Struttura*, si può vedere che il campo &quot;fedeltà&quot; ha un tipo di dati &quot;Fedeltà&quot; e i campi hanno icone di blocco piccole accanto a essi, a indicare che non sono più campi singoli, ma fanno parte di una struttura multi-campo.

In uno schema futuro, è ora possibile assegnare a un campo il **Tipo** di Fedeltà e includere automaticamente i campi Livello fedeltà, Punti, Membro da e ID fedeltà.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Impostare un campo dello schema come campo di identità {#identity-field}

Gli schemi vengono utilizzati per l&#39;assimilazione di dati in  Experience Platform e i dati vengono utilizzati per identificare individui e unire insieme informazioni provenienti da più fonti. Per facilitare questo processo, i campi chiave possono essere contrassegnati come campi &quot;Identità&quot;.

 Experience Platform semplifica la denotazione di un campo identità attraverso l&#39;uso di una casella di controllo **Identità** nell&#39;Editor di schema.

Ad esempio, ci possono essere migliaia di membri del programma fedeltà appartenenti allo stesso &quot;livello&quot;, ma ogni membro del programma fedeltà ha un &quot;loyaltyId&quot; univoco (che in questo caso è l&#39;indirizzo e-mail del singolo membro). Il fatto che &quot;loyaltyId&quot; sia un identificatore univoco per ciascun membro lo rende un valido candidato per un campo di identità, mentre &quot;level&quot; non lo è.

Nella sezione *Struttura* dell’editor, fate clic sul campo &quot;loyaltyId&quot; creato e la casella di controllo **Identità** verrà visualizzata in Proprietà ** campo. Selezionare la casella e sarà possibile impostare questa opzione come identità **** principale. Controlla anche quella scatola.

Successivamente, è necessario specificare uno spazio dei nomi **identità**. Esistono diversi spazi dei nomi predefiniti, ma siccome &quot;fedeltàId&quot; è l&#39;indirizzo e-mail del membro, selezionate &quot;E-mail&quot; dall&#39;elenco a discesa. Ora puoi fare clic su **Applica** per confermare gli aggiornamenti al campo &quot;loyaltyId&quot;.

Ora tutti i dati immessi nel campo &quot;loyaltyId&quot; saranno utilizzati per identificare l&#39;individuo e unire insieme una singola vista del cliente.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Una volta impostato un campo dello schema come identità principale, si riceverà un messaggio di errore se si tenta in seguito di impostare come principale un altro campo dello schema. Ogni schema può contenere un solo campo identità principale.

Per ulteriori informazioni sull&#39;utilizzo delle identità, consulta la documentazione [Servizio](../../identity-service/home.md) identità.

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Abilitare lo schema per l&#39;utilizzo in Real-time Customer Profile {#profile}

L&#39;Editor schema consente di abilitare uno schema da utilizzare con il profilo [cliente in tempo](../../profile/home.md)reale. Il profilo fornisce una visione olistica di ogni singolo cliente creando un profilo affidabile e a 360° degli attributi del cliente e un account con marca temporale di ogni interazione che il cliente ha avuto tra i sistemi integrati con  Experience Platform.

Affinché uno schema possa essere abilitato per l&#39;uso con il profilo cliente in tempo reale, è necessario che sia definita un&#39;identità primaria. Se si tenta di abilitare uno schema senza prima definire un&#39;identità primaria, verrà visualizzato un messaggio di errore &quot;Identità principale mancante&quot;.

![](../images/tutorials/create-schema/missing_primary_identity.png)

Per attivare lo schema &quot;Membri fedeltà&quot; da utilizzare in Profilo, iniziare facendo clic su &quot;Membri fedeltà&quot; nella sezione *Struttura* dell&#39;editor.

Sul lato destro dell&#39;editor, in Proprietà ** schema, vengono visualizzate informazioni sullo schema, incluso il nome visualizzato, la descrizione e il tipo. Oltre a queste informazioni, è disponibile un pulsante di attivazione/disattivazione denominato **Profilo**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Fate clic su **Profilo** e viene visualizzato un messaggio a comparsa in cui viene richiesto di confermare l&#39;abilitazione dello schema per Profilo.

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>Una volta che uno schema è stato abilitato per il profilo cliente in tempo reale e salvato, non può essere disabilitato.

## Passaggi successivi e risorse aggiuntive

Dopo aver completato la composizione di uno schema &quot;Membri fedeltà&quot;, è possibile visualizzare lo schema completo nella sezione *Struttura* dell&#39;editor. Fare clic su **Salva** e lo schema verrà salvato nella Libreria schema, rendendola accessibile dal Registro di sistema dello schema.

Ora è possibile utilizzare il nuovo schema per acquisire dati in Platform. Tenere presente che una volta che lo schema è stato utilizzato per acquisire i dati, è possibile apportare solo modifiche aggiuntive. Per ulteriori informazioni sul controllo delle versioni dello schema, vedere le [nozioni di base della composizione](../schema/composition.md) dello schema.

Lo schema &quot;Membri fedeltà&quot; è disponibile anche per essere visualizzato e gestito utilizzando l&#39;API del Registro di sistema dello schema. Per iniziare a lavorare con l&#39;API, leggete la guida [per gli sviluppatori API del Registro di](../api/getting-started.md)schema.

>[!WARNING]
>
>L’ [!DNL Platform] interfaccia utente mostrata nei video seguenti è obsoleta. Per informazioni sulle ultime funzionalità e videate dell’interfaccia, consulta la documentazione precedente.

Il video seguente mostra come creare uno schema semplice nell’ [!DNL Platform] interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

Il seguente video è pensato per comprendere meglio come utilizzare mixin e classi.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Appendice

Le seguenti informazioni sono supplementari rispetto all&#39;esercitazione sull&#39;Editor di schema.

### Create a new class {#create-new-class}

 Experience Platform offre la flessibilità di definire uno schema basato su una classe univoca per l&#39;organizzazione.

Aprire la finestra di dialogo *Assegna classe* facendo clic su **Assegna** nella sezione *Classe* dell&#39;Editor di schema. All&#39;interno della finestra di dialogo, selezionare **Crea nuova classe**.

È quindi possibile assegnare alla nuova classe un Nome **** visualizzato (un nome breve, descrittivo, univoco e di facile utilizzo per la classe), un nome **Descrizione** e un **comportamento** (&quot;Record&quot; o &quot;Serie di ore&quot;) per i dati che lo schema definirà.

![Dettagli nuova classe](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>Durante la creazione di uno schema che implementa una classe definita dall&#39;organizzazione, tenere presente che i mixin sono disponibili solo per le classi compatibili. Poiché la classe definita è nuova, nella finestra di dialogo *Aggiungi mixin* non sono presenti mixin compatibili. Al contrario, dovrete selezionare **Crea nuovo mixin** e definire un mixin da utilizzare con tale classe. Al successivo comporre uno schema che implementa la nuova classe, il mixin definito verrà elencato e sarà disponibile per l&#39;uso.

### Modificare la classe di uno schema {#change-class}

In qualsiasi momento durante il processo di composizione dello schema iniziale, prima che lo schema venga salvato, è possibile modificare la classe su cui si basa lo schema.

>[!WARNING]
>
>Si prega di fare attenzione prima di cambiare la classe. Le miscele sono compatibili solo con determinate classi, pertanto la modifica della classe reimposta il quadro e rimuove tutti i campi aggiunti a tale punto.

Per modificare la classe, fate clic su **Assegna** accanto a *Classe* nella sezione *Composizione* dell’editor.

Quando si apre la finestra di dialogo *Assegna classe* , è possibile scegliere una nuova classe dall&#39;elenco disponibile. Fate clic su **Assegna classe** e si apre una nuova finestra di dialogo in cui viene richiesto di confermare l&#39;assegnazione di una nuova classe.

![Cambia classe](../images/tutorials/create-schema/assign_new_class_warning.png)

Se confermate la modifica della classe, il quadro verrà reimpostato e tutti i progressi della composizione andranno persi.