---
title: Panoramica end-to-end sulla raccolta dati
description: Panoramica di alto livello su come inviare dati di eventi alle soluzioni Adobe Experience Cloud utilizzando le funzionalità di raccolta dati di Adobe Experience Platform.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '2616'
ht-degree: 0%

---

# Panoramica end-to-end sulla raccolta dati

Adobe Experience Platform raccoglie e trasferisce i dati ad altri prodotti Adobe e destinazioni di terze parti. Per inviare i dati dell’evento dall’applicazione all’Edge Network Experience Platform, è importante comprendere queste tecnologie di base e configurarle in modo da fornire i dati alle destinazioni necessarie, quando necessario.

Questa guida fornisce un tutorial di alto livello su come inviare un evento tramite l’Edge Network utilizzando le funzionalità di raccolta dati di Platform. In particolare, il tutorial illustra i passaggi necessari per installare e configurare l’estensione tag Adobe Experience Platform Web SDK nell’interfaccia utente di Data Collection (precedentemente Adobe Experience Platform Launch).

>[!NOTE]
>
>Se non desideri utilizzare i tag, puoi anche scegliere di installare e configurare manualmente l’SDK, ma i passaggi successivi devono ancora essere completati come descritto di seguito.
>
>Tutti i passaggi che riguardano l’interfaccia utente di Data Collection possono essere eseguiti anche nell’interfaccia utente di Experience Platform.

## Prerequisiti

Questa esercitazione utilizza l’interfaccia utente di Data Collection per creare uno schema, configurare uno stream di dati e installare l’SDK per web. Per eseguire queste azioni nell&#39;interfaccia utente, è necessario disporre dell&#39;accesso ad almeno una proprietà Web insieme ai seguenti [diritti di proprietà](../tags/ui/administration/user-permissions.md#property-rights):

* Sviluppa
* Gestire le estensioni

Per informazioni su come concedere l&#39;accesso a proprietà e diritti di proprietà, consulta la guida su [gestione delle autorizzazioni per la raccolta dati](./permissions.md).

Per utilizzare i vari prodotti di raccolta dati menzionati in questa guida, devi anche avere accesso agli stream di dati e la possibilità di creare e gestire gli schemi. Se hai bisogno di accedere a una di queste funzioni, contatta il team del tuo account Adobe per ottenere l’accesso necessario. Se non hai acquistato Adobe Experience Platform, Adobe ti fornirà l’accesso necessario per utilizzare l’SDK senza costi aggiuntivi.

Se disponi già dell&#39;accesso a Platform, assicurati di disporre di tutte le [autorizzazioni](../access-control/home.md#permissions) per le seguenti categorie abilitate:

* Modellazione dati
* Identità

Per informazioni su come concedere autorizzazioni per le funzionalità di Platform agli utenti, consulta la [panoramica dell&#39;interfaccia utente di controllo degli accessi](../access-control/ui/overview.md).

## Riepilogo del processo

Il processo di configurazione della raccolta dati per il sito web può essere riassunto come segue:

1. [Creare uno schema](#schema) per determinare la struttura dei dati inviati all&#39;Edge Network.
1. [Crea uno stream di dati](#datastream) per configurare le destinazioni a cui inviare i dati.
1. [Installa e configura Web SDK](#sdk) per inviare dati allo stream di dati quando si verificano determinati eventi sul sito Web.

Una volta che sei in grado di inviare i dati all&#39;Edge Network, puoi anche [configurare l&#39;inoltro degli eventi](#event-forwarding) se la tua organizzazione dispone di una licenza per esso.

## Crea uno schema {#schema}

[Experience Data Model (XDM)](../xdm/home.md) è una specifica open-source che fornisce strutture e definizioni comuni per i dati sotto forma di schemi. In altre parole, XDM è un modo per strutturare e formattare i dati in modo che sia utilizzabile dall’Edge Network e da altre applicazioni Adobe Experience Cloud.

Il primo passaggio nella configurazione delle operazioni di raccolta dei dati consiste nel creare uno schema XDM per rappresentare i dati. In un passaggio successivo di questa esercitazione, mapperai i dati che desideri inviare alla struttura di questo schema.

>[!NOTE]
>
>Gli schemi XDM sono molto personalizzabili. Invece di essere eccessivamente prescrittivi, i passaggi descritti di seguito si concentrano specificamente sui requisiti dello schema per l’SDK per web. Al di fuori di questi parametri, puoi definire la struttura rimanente dei dati come preferisci.

Nell&#39;interfaccia utente, seleziona **[!UICONTROL Schemi]** nell&#39;area di navigazione a sinistra. Da qui puoi visualizzare un elenco degli schemi creati in precedenza e appartenenti alla tua organizzazione. Per continuare, seleziona **[!UICONTROL Crea schema]**, quindi seleziona **[!UICONTROL XDM ExperienceEvent]** dal menu a discesa.

![Area di lavoro Schemi](./images/e2e/schemas.png)

Viene visualizzata una finestra di dialogo che richiede di iniziare ad aggiungere gruppi di campi allo schema. Per inviare eventi tramite Web SDK, è necessario aggiungere il gruppo di campi **[!UICONTROL Mixin ExperienceEvent di AEP Web SDK]**. Questo gruppo di campi contiene le definizioni per gli attributi dei dati raccolti automaticamente dalla libreria SDK Web.

Utilizzare la barra di ricerca per limitare l&#39;elenco e semplificare la ricerca di questo gruppo di campi. Dopo averlo trovato, selezionalo dall&#39;elenco prima di selezionare **[!UICONTROL Aggiungi gruppi di campi]**.

![Area di lavoro Schemi](./images/e2e/add-field-group.png)

Viene visualizzata l’area di lavoro dello schema, con una struttura ad albero dello schema XDM che include i campi forniti dal gruppo di campi dell’SDK per web.

![Struttura dello schema](./images/e2e/schema-structure.png)

Selezionare il campo radice nella struttura per aprire **[!UICONTROL Proprietà schema]** nella barra a destra, dove è possibile fornire un nome e una descrizione facoltativa per lo schema.

![Denomina lo schema](./images/e2e/name-schema.png)

Per aggiungere altri campi allo schema, seleziona **[!UICONTROL Aggiungi]** nella sezione **[!UICONTROL Gruppi di campi]** nella barra a sinistra.

![Aggiungi gruppi di campi](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>Consulta la guida su [aggiunta di gruppi di campi](../xdm/ui/resources/schemas.md#add-field-groups) nella documentazione XDM per i passaggi dettagliati su come cercare gruppi di campi diversi in base ai tuoi casi d&#39;uso.
>
>Si consiglia di aggiungere solo campi per i dati che intendi inviare tramite l’Edge Network. Dopo aver aggiunto i campi a uno schema e averlo salvato, è possibile apportare allo schema solo modifiche aggiuntive. Per ulteriori informazioni, consulta la sezione sulle [regole dell&#39;evoluzione dello schema](../xdm/schema/composition.md#evolution).

Dopo aver aggiunto i campi necessari, seleziona **[!UICONTROL Salva]** per salvare lo schema.

![Salva schema](./images/e2e/save-schema.png)

## Creare un flusso di dati {#datastream}

Un flusso di dati è una configurazione che indica all’Edge Network dove desideri che vengano inviati i dati. In particolare, un datastream specifica a quali prodotti Experience Cloud desideri inviare i dati e come desideri che i dati vengano gestiti e memorizzati in ciascun prodotto.

>[!NOTE]
>
>Se si desidera utilizzare l&#39;[inoltro eventi](../tags/ui/event-forwarding/overview.md) (presupponendo che l&#39;organizzazione disponga della licenza per la funzionalità), è necessario abilitarla per uno stream di dati nello stesso modo in cui si abilitano i prodotti Adobe. I dettagli su questo processo sono trattati in una [sezione successiva](#event-forwarding).

Seleziona **[!UICONTROL Flussi di dati]** nel menu di navigazione a sinistra. Da qui puoi selezionare uno stream di dati esistente dall&#39;elenco da modificare, oppure puoi creare una nuova configurazione selezionando **[!UICONTROL Nuovo stream di dati]**.

![Stream di dati](./images/e2e/datastreams.png)

I requisiti di configurazione per un datastream dipendono dai prodotti e dalle funzionalità a cui invii i dati. Per informazioni dettagliate sulle opzioni di configurazione per ciascun prodotto, consulta la [panoramica sugli stream di dati](../datastreams/overview.md).

## Installare e configurare Web SDK {#install}

Dopo aver creato uno schema e un flusso di dati, il passaggio successivo consiste nell’installare e configurare Platform Web SDK per iniziare a inviare dati all’Edge Network.

>[!NOTE]
>
>Questa sezione utilizza l’interfaccia utente di Data Collection per configurare l’estensione tag Web SDK, ma puoi anche installarla e configurarla utilizzando codice non elaborato. Per ulteriori informazioni, consulta le seguenti guide:
>
>* [Installa SDK](/help/web-sdk/install/overview.md)
>* [Configurare l&#39;SDK](/help/web-sdk/commands/configure/overview.md)
>
>Inoltre, anche se desideri utilizzare solo l&#39;inoltro degli eventi, devi comunque installare e configurare l&#39;SDK come descritto prima di configurare l&#39;inoltro degli eventi in un [passaggio successivo](#event-forwarding).

Il processo può essere riassunto come segue:

1. [Installa Adobe Experience Platform Web SDK in una proprietà tag](#install-sdk) per accedere alle funzionalità.
1. [Crea un elemento dati di oggetti XDM](#data-element) per mappare le variabili sul sito Web alla struttura dello schema XDM creato in precedenza.
1. [Crea una regola](#rule) per indicare all&#39;SDK quando deve inviare i dati all&#39;Edge Network.
1. [Crea e installa una libreria](#library) per implementare la regola nel sito Web.

### Installare l’SDK su una proprietà tag {#install-sdk}

Seleziona **[!UICONTROL Tag]** nel menu di navigazione a sinistra per visualizzare un elenco di proprietà dei tag. Puoi scegliere una proprietà esistente da modificare, se lo desideri, oppure selezionare **[!UICONTROL Nuova proprietà]**.

![Proprietà](./images/e2e/properties.png)

Se crei una nuova proprietà, fornisci un nome descrittivo e imposta [!UICONTROL Platform] su **[!UICONTROL Web]**. Fornisci il dominio completo per la proprietà Web, quindi seleziona **[!UICONTROL Salva]**.

![Crea proprietà](./images/e2e/create-property.png)

Viene visualizzata la pagina della panoramica della proprietà. Da qui, seleziona **[!UICONTROL Estensioni]** nell&#39;area di navigazione a sinistra, quindi seleziona **[!UICONTROL Catalogo]**. Trovare l&#39;elenco per Platform Web SDK (se si desidera utilizzare la barra di ricerca per limitare i risultati) e selezionare **[!UICONTROL Installa]**.

![Installa Web SDK](./images/e2e/install-sdk.png)

Viene visualizzata la pagina di configurazione per l’SDK. La maggior parte dei valori richiesti viene compilata automaticamente con i valori predefiniti che puoi scegliere di modificare se lo desideri.

![Configurare Web SDK](./images/e2e/configure-sdk.png)

Prima di installare l’SDK, tuttavia, devi selezionare uno stream di dati in modo che sappia a dove inviare i dati. In **[!UICONTROL Datastreams]**, utilizza il menu a discesa per selezionare il datastream configurato in un [passaggio precedente](#datastream). Dopo aver impostato lo stream di dati, seleziona **[!UICONTROL Salva]** per completare l&#39;installazione dell&#39;SDK nella proprietà.

![Imposta lo stream di dati e salva](./images/e2e/set-datastream.png)

### Creare un elemento dati XDM {#data-element}

Affinché l&#39;SDK possa inviare dati all&#39;Edge Network, questi devono essere mappati sullo schema XDM creato in un [passaggio precedente](#schema). Questa mappatura viene eseguita tramite l’utilizzo di un elemento dati.

Nell&#39;interfaccia utente, seleziona **[!UICONTROL Elementi dati]**, quindi seleziona **[!UICONTROL Crea nuovo elemento dati]**.

![Crea nuovo elemento dati](./images/e2e/data-elements.png)

Nella schermata successiva, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]** nel menu a discesa [!UICONTROL Extension], quindi seleziona **[!UICONTROL XDM object]** per il tipo di elemento dati.

![Tipo di oggetto XDM](./images/e2e/xdm-object.png)

Viene visualizzata la finestra di dialogo di configurazione per il tipo di oggetto XDM. La finestra di dialogo seleziona automaticamente la sandbox Platform e da qui puoi visualizzare tutti gli schemi creati in tale sandbox. Seleziona dall’elenco lo schema XDM creato in precedenza.

![Tipo di oggetto XDM](./images/e2e/select-schema.png)

Viene visualizzata la struttura dello schema. Tutti i campi con un asterisco (**\***) indicano i campi che verranno compilati automaticamente quando si attivano gli eventi. Per tutti gli altri campi, puoi esplorare la struttura dello schema e compilare il resto dei dati.

![Mappatura dei dati su campi XDM](./images/e2e/map-schema.png)

>[!NOTE]
>
>La schermata precedente illustra come mappare una variabile accessibile a livello globale dal lato client del sito Web (`cartAbandonsTotal`) a un campo XDM facendo riferimento al relativo nome nel campo [!UICONTROL Valore], circondato dai segni di percentuale (`%`).
>
>Per compilare questi campi, puoi anche utilizzare altri elementi dati creati in precedenza. Per ulteriori informazioni, vedi il riferimento su [elementi dati](../tags/ui/managing-resources/data-elements.md) nella documentazione dei tag.

Dopo aver completato la mappatura dei dati sullo schema, fornisci un nome per l&#39;elemento dati prima di selezionare **[!UICONTROL Salva]**.

![Denomina e salva l&#39;elemento dati](./images/e2e/name-and-save.png)

### Creare una regola

Dopo aver salvato l’elemento dati, il passaggio successivo consiste nel creare una regola che lo invierà all’Edge Network ogni volta che si verifica un determinato evento sul sito web (ad esempio quando un cliente aggiunge un prodotto a un carrello).

Puoi impostare regole per praticamente qualsiasi evento che possa verificarsi sul sito web. Ad esempio, in questa sezione viene illustrato come creare una regola che verrà attivata quando un cliente invia un modulo. Il seguente HTML rappresenta una semplice pagina web con un modulo &quot;Aggiungi al carrello&quot;, che sarà l’oggetto della regola:

```html
<!DOCTYPE html>
<html>
<body>

  <form id="add-to-cart-form">
    <label for="item">Product:</label><br>
    <input type="text" id="item" name="item"><br>
    <label for="amount">Amount:</label><br>
    <input type="number" id="amount" name="amount" value="1"><br><br>
    <input type="submit" value="Add to Cart">
  </form> 

</body>
</html>
```

Nell&#39;interfaccia utente di Data Collection, seleziona **[!UICONTROL Regole]** nell&#39;area di navigazione a sinistra, quindi seleziona **[!UICONTROL Crea nuova regola]**.

![Regole](./images/e2e/rules.png)

Nella schermata successiva, specifica un nome per la regola. Da qui, il passaggio successivo è quello di determinare l’evento per la regola (in altre parole, quando la regola verrà attivata). Seleziona **[!UICONTROL Aggiungi]** in [!UICONTROL Eventi].

![Regola nome](./images/e2e/name-rule.png)

Viene visualizzata la pagina di configurazione dell’evento. Per configurare un evento, devi innanzitutto selezionare il tipo di evento. I tipi di evento sono forniti dalle estensioni. Per impostare un evento &quot;invio modulo&quot;, ad esempio, seleziona l&#39;estensione **[!UICONTROL Core]**, quindi seleziona il tipo di evento **[!UICONTROL Invia]** nella categoria **[!UICONTROL Modulo]**.

>[!NOTE]
>
>Per ulteriori informazioni sui diversi tipi di eventi forniti dalle estensioni Web Adobe, tra cui la relativa configurazione, vedi il [riferimento per le estensioni Adobe](../tags/extensions/client/overview.md) nella documentazione dei tag.

L&#39;evento di invio modulo consente di utilizzare un [selettore CSS](https://www.w3schools.com/css/css_selectors.asp) per fare riferimento a un elemento specifico per la regola su cui attivare. Nell&#39;esempio seguente, l&#39;ID `add-to-cart-form` viene utilizzato in modo che questa regola venga attivata solo per il modulo &quot;Aggiungi al carrello&quot;. Seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;evento alla regola.

![Configurazione evento](./images/e2e/event-config.png)

Viene visualizzata di nuovo la pagina di configurazione della regola dove si vede che l&#39;evento è stato aggiunto. È possibile limitare &quot;[!UICONTROL If]&quot; aggiungendo ulteriori condizioni alla regola.

In caso contrario, il passaggio successivo consiste nell’aggiungere un’azione da eseguire per la regola quando viene attivata. Seleziona **[!UICONTROL Aggiungi]** in **[!UICONTROL Azioni]** per continuare.

![Aggiungi azione](./images/e2e/add-action.png)

Viene visualizzata la pagina di configurazione dell’azione. Per ottenere la regola per inviare i dati all&#39;Edge Network, selezionare **[!UICONTROL Adobe Experience Platform Web SDK]** per l&#39;estensione e **[!UICONTROL Send event]** per il tipo di azione.

![Tipo azione](./images/e2e/action-type.png)

La schermata si aggiorna per mostrare opzioni aggiuntive per configurare l’azione invia evento. In **[!UICONTROL Tipo]** puoi fornire un valore di tipo personalizzato per compilare il campo XDM `eventType`. In **[!UICONTROL Dati XDM]**, fornire il nome del tipo di dati XDM creato in precedenza (racchiuso tra simboli di percentuale) oppure selezionare l&#39;icona del database (![Icona del database](./images/e2e/database-symbol.png)) per selezionarlo da un elenco. Questi sono i dati che verranno infine inviati all’Edge Network.

Al termine, seleziona **[!UICONTROL Mantieni modifiche]**.

![Configurazione azione](./images/e2e/action-config.png)

Al termine della configurazione della regola, seleziona **[!UICONTROL Salva]** per completare il processo.

![Salva regola](./images/e2e/save-rule.png)

### Creare e installare una libreria {#library}

Una volta configurata la regola, puoi aggiungerla a una libreria di tag, generarla in un ambiente e installarla sul sito web.

>[!NOTE]
>
>Se non hai ancora configurato un ambiente nell’interfaccia utente di Data Collection, devi farlo prima di poter creare una build. Per ulteriori informazioni, consulta la sezione sulla [configurazione di un ambiente per una proprietà Web](../tags/ui/publishing/environments.md#web-configuration) nella documentazione dei tag.

Per informazioni su come creare una libreria, aggiungere estensioni e regole alla libreria e creare tale libreria in un ambiente, consulta la guida su [gestione delle librerie](../tags/ui/publishing/libraries.md) nella documentazione sui tag. Quando crei la libreria, accertati di includere l’estensione Platform Web SDK e le regole di raccolta dati create in precedenza.

Dopo aver creato la libreria e aver assegnato la relativa build a un ambiente, puoi installare tale ambiente sul lato client del sito web. Per ulteriori informazioni, vedere la sezione relativa all&#39;installazione di [ambienti](../tags/ui/publishing/environments.md#installation).

Dopo aver installato l&#39;ambiente sul sito Web, puoi [testare l&#39;implementazione](../tags/ui/publishing/embed-code-testing.md) utilizzando Adobe Experience Platform Debugger.

## Configurare l’inoltro degli eventi (facoltativo) {#event-forwarding}

>[!NOTE]
>
>L’inoltro degli eventi è disponibile solo per le organizzazioni per le quali è stata concessa la licenza.

Dopo aver configurato l’SDK per l’invio dei dati all’Edge Network, puoi impostare l’inoltro degli eventi per indicare all’Edge Network dove desideri che vengano consegnati i dati.

Per utilizzare l’inoltro degli eventi, devi innanzitutto creare una proprietà di inoltro degli eventi. Seleziona **[!UICONTROL Inoltro eventi]** nella barra di navigazione a sinistra, quindi seleziona **[!UICONTROL Nuova proprietà]**. Specifica un nome per la proprietà prima di selezionare **[!UICONTROL Salva]**.

Dopo aver creato una proprietà di inoltro degli eventi, il passaggio successivo consiste nel creare una regola che determini dove devono essere inviati i dati. Le regole per le proprietà di inoltro degli eventi sono costruite in modo molto simile alle proprietà dei tag, con l’eccezione che non è possibile specificare alcun evento (poiché l’inoltro degli eventi riguarda solo gli eventi che riceve direttamente dallo stream di dati). Per l’azione della regola, puoi utilizzare una delle estensioni di inoltro degli eventi disponibili oppure il codice personalizzato per distribuire l’evento.

![Regola di inoltro eventi](./images/e2e/event-forwarding-rule.png)

Come prima, una volta configurata la regola, devi aggiungerla a una libreria e generarla in un ambiente.

Al termine della compilazione, il passaggio finale consiste nell&#39;aggiornare lo stream di dati [configurato in precedenza](#datastream) e abilitare l&#39;inoltro degli eventi. Per iniziare, passa a **[!UICONTROL Datastreams]** e seleziona lo stream di dati in questione dall&#39;elenco. Da qui, abilita l’interruttore per l’inoltro degli eventi e fornisci i nomi della proprietà e dell’ambiente appena configurati.

![Stream dati inoltro eventi](./images/e2e/event-forwarding-datastream.png)

## Passaggi successivi

Questa guida fornisce una panoramica end-to-end di alto livello su come inviare dati all’Edge Network utilizzando Platform Web SDK. Per ulteriori informazioni sui vari componenti e servizi coinvolti, consulta la documentazione accessibile dai collegamenti presenti in questa guida.
