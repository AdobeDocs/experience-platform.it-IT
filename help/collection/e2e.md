---
title: Panoramica della raccolta dati end-to-end
description: Panoramica di alto livello su come inviare dati evento alle soluzioni Adobe Experience Cloud utilizzando le tecnologie di raccolta dati fornite da Adobe Experience Platform.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 1b2c0c2e5b05e30b6cf0e284f15f28989c580efe
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 0%

---

# Panoramica sulla raccolta dati end-to-end

In Adobe Experience Platform, per raccolta dati si intendono diverse tecnologie che lavorano insieme per raccogliere i dati da trasferire ad altri prodotti Adobe o a destinazioni di terze parti. Per inviare i dati dell’evento dall’applicazione a Adobe Experience Platform Edge Network, è importante comprendere queste tecnologie di base e come configurarle in modo da inviare i dati alle destinazioni richieste, quando necessario.

Questa guida fornisce un tutorial di alto livello su come inviare un evento tramite la rete Edge utilizzando le tecnologie di raccolta dati. In particolare, l&#39;esercitazione descrive i passaggi necessari per installare e configurare l&#39;estensione tag Adobe Experience Platform Web SDK all&#39;interno dell&#39;interfaccia utente di raccolta dati (precedentemente Adobe Experience Platform Launch).

>[!NOTE]
>
>Puoi anche scegliere di installare e configurare manualmente l’SDK se non desideri utilizzare i tag, ma i passaggi circostanti devono comunque essere completati come descritto di seguito.

## Prerequisiti

Questa esercitazione utilizza l’interfaccia utente di raccolta dati per creare uno schema, configurare un datastream e installare l’SDK per web. Per eseguire queste azioni nell&#39;interfaccia utente, è necessario avere accesso ad almeno una proprietà Web insieme ai seguenti [diritti di proprietà](../tags/ui/administration/user-permissions.md#property-rights):

* Sviluppa
* Gestire le estensioni

Per informazioni su come concedere l&#39;accesso a proprietà e diritti di proprietà, consulta la guida sulla [gestione delle autorizzazioni per i tag](../tags/ui/administration/manage-permissions.md) .

Per utilizzare i vari prodotti di raccolta dati menzionati in questa guida, devi anche avere accesso ai datastreams e la possibilità di creare e gestire gli schemi. Se hai bisogno di accedere a una di queste funzioni, contatta il tuo CSM per ottenere l&#39;accesso necessario. Se non hai acquistato Adobe Experience Platform, Adobe ti fornirà l’accesso necessario per utilizzare l’SDK senza costi aggiuntivi.

Se disponi già dell&#39;accesso a Platform, assicurati di avere abilitato tutte le [autorizzazioni](../access-control/home.md#permissions) nelle seguenti categorie:

* Modellazione dati
* Identità

Per informazioni su come concedere autorizzazioni per le funzionalità di Platform agli utenti, consulta la [panoramica dell’interfaccia utente di controllo accessi](../access-control/ui/overview.md) .

## Riepilogo del processo

Il processo di configurazione della rete Edge per il sito Web può essere riassunto come segue:

1. [Creare uno ](#schema) schema determina la struttura dei dati quando vengono inviati alla rete Edge.
1. [Crea un ](#datastream) datastreamper configurare le destinazioni a cui desideri inviare i dati.
1. [Installa e configura l&#39;](#sdk) SDK per web per l&#39;invio di dati al datastream quando si verificano determinati eventi sul sito web.

Una volta inviati i dati alla rete Edge, è anche possibile [configurare l&#39;inoltro eventi](#event-forwarding) se l&#39;organizzazione dispone di una licenza per questo.

## Creare uno schema {#schema}

[Experience Data Model (XDM)](../xdm/home.md) è una specifica open-source che fornisce strutture e definizioni comuni per i dati sotto forma di schemi. In altre parole, XDM è un modo per strutturare e formattare i dati in modo che sia fruibile da Edge Network e da altre applicazioni Adobe Experience Cloud.

Il primo passo per configurare le operazioni di raccolta dati è creare uno schema XDM per rappresentare i dati. In un passaggio successivo di questa esercitazione, mapperai i dati che desideri inviare alla struttura di questo schema.

>[!NOTE]
>
>Gli schemi XDM sono molto personalizzabili. Invece di essere eccessivamente prescrittivi, i passaggi descritti di seguito si concentrano specificamente sui requisiti di schema per l&#39;SDK per web. Al di fuori di questi parametri, puoi definire liberamente la struttura rimanente dei tuoi dati come desideri.

Nell’interfaccia utente Raccolta dati, seleziona **[!UICONTROL Schemi]** nel menu di navigazione a sinistra. Da qui puoi visualizzare un elenco degli schemi creati in precedenza appartenenti all’organizzazione. Per continuare, seleziona **[!UICONTROL Crea schema]**, quindi seleziona **[!UICONTROL XDM ExperienceEvent]** dal menu a discesa.

![Area di lavoro degli schemi](./images/e2e/schemas.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di iniziare ad aggiungere gruppi di campi allo schema. Per inviare eventi utilizzando l&#39;SDK per web, devi aggiungere il gruppo di campi **[!UICONTROL AEP Web SDK ExperienceEvent Mixin]**. Questo gruppo di campi contiene le definizioni degli attributi di dati raccolti automaticamente dalla libreria SDK per web.

Utilizza la barra di ricerca per restringere l’elenco in modo da facilitare la ricerca di questo gruppo di campi. Una volta trovata, selezionala dall&#39;elenco prima di selezionare **[!UICONTROL Aggiungi gruppi di campi]**.

![Area di lavoro degli schemi](./images/e2e/add-field-group.png)

Viene visualizzata l’area di lavoro dello schema, che mostra una struttura ad albero dello schema XDM, inclusi i campi forniti dal gruppo di campi SDK per web.

![Struttura dello schema](./images/e2e/schema-structure.png)

Seleziona il campo principale nella struttura per aprire **[!UICONTROL Proprietà schema]** nella barra a destra, dove puoi fornire un nome e una descrizione facoltativa per lo schema.

![Denomina lo schema](./images/e2e/name-schema.png)

Se desideri aggiungere altri campi allo schema, puoi farlo selezionando **[!UICONTROL Aggiungi]** nella sezione **[!UICONTROL Gruppi di campi]** nella barra a sinistra.

![Aggiungi gruppi di campi](./images/e2e/add-field-groups.png)

>[!NOTE]
>
>Consulta la guida sull’ [aggiunta di gruppi di campi](../xdm/ui/resources/schemas.md#add-field-groups) nella documentazione XDM per passaggi dettagliati su come cercare diversi gruppi di campi in base ai tuoi casi d’uso.
>
>Si consiglia di aggiungere solo campi per i dati che si prevede di inviare tramite la rete Edge. Dopo aver aggiunto i campi a uno schema e averlo salvato, è possibile apportare solo modifiche aggiuntive allo schema in seguito. Per ulteriori informazioni, consulta la sezione sulle [regole di evoluzione dello schema](../xdm/schema/composition.md#evolution) .

Dopo aver aggiunto i campi necessari, seleziona **[!UICONTROL Salva]** per salvare lo schema.

![Salva lo schema](./images/e2e/save-schema.png)

## Creare un flusso di dati {#datastream}

Un datastream è una configurazione che indica alla rete Edge in cui desideri inviare i dati. In particolare, un datastream specifica a quali prodotti di Experience Cloud si desidera inviare i dati e come si desidera che i dati vengano gestiti e memorizzati in ciascun prodotto.

>[!NOTE]
>
>Se desideri utilizzare [inoltro eventi](../tags/ui/event-forwarding/overview.md) (partendo dal presupposto che la tua organizzazione disponga di una licenza per la funzionalità), devi abilitarlo per un datastream nello stesso modo in cui abiliti i prodotti Adobe. I dettagli su questo processo sono descritti in una sezione [successiva](#event-forwarding).

Nell’interfaccia utente di raccolta dati, seleziona **[!UICONTROL Datastreams]**. Da qui, è possibile selezionare un datastream esistente dall&#39;elenco da modificare, oppure è possibile creare una nuova configurazione selezionando **[!UICONTROL Nuovo Datastream]**.

![Datastream](./images/e2e/datastreams.png)

I requisiti di configurazione per un datastream dipendono dai prodotti e dalle funzionalità a cui invii i dati. Per informazioni dettagliate sulle opzioni di configurazione per ciascun prodotto, consulta la [panoramica dei datastreams](../edge/fundamentals/datastreams.md).

## Installare e configurare l’SDK per web

Dopo aver creato uno schema e un datastream, il passaggio successivo consiste nell’installare e configurare l’SDK per web di Platform per iniziare a inviare dati alla rete Edge.

>[!NOTE]
>
>Questa sezione utilizza l’interfaccia utente di raccolta dati per configurare l’estensione tag SDK per web, ma puoi anche installarla e configurarla utilizzando il codice non elaborato. Per ulteriori informazioni, consulta le seguenti guide:
>
>* [Installare l’SDK](../edge/fundamentals/installing-the-sdk.md)
>* [Configurare l&#39;SDK](../edge/fundamentals/configuring-the-sdk.md)

>
>Inoltre, anche se desideri utilizzare solo l&#39;inoltro eventi, devi comunque installare e configurare l&#39;SDK come descritto prima di configurare l&#39;inoltro eventi in un [passaggio successivo](#event-forwarding).

Il processo può essere riassunto come segue:

1. [Installa Adobe Experience Platform Web SDK su una ](#install-sdk) proprietà di tag per accedere alle sue funzionalità.
1. [Crea un elemento dati oggetto XDM ](#data-element) per mappare le variabili sul sito web alla struttura dello schema XDM creato in precedenza.
1. [Crea una ](#rule) regola per comunicare all’SDK quando deve inviare dati alla rete Edge.
1. [Crea e installa una ](#library) libreria per implementare la regola sul tuo sito web.

### Installare l’SDK su una proprietà tag {#install-sdk}

Seleziona **[!UICONTROL Tag]** nel menu di navigazione a sinistra per visualizzare un elenco delle proprietà dei tag. Puoi scegliere una proprietà esistente da modificare, se lo desideri, oppure puoi selezionare **[!UICONTROL Nuova proprietà]**.

![Proprietà](./images/e2e/properties.png)

Se crei una nuova proprietà, fornisci un nome descrittivo e imposta [!UICONTROL Platform] su **[!UICONTROL Web]**. Fornisci il dominio completo per la proprietà web, quindi seleziona **[!UICONTROL Salva]**.

![Crea proprietà](./images/e2e/create-property.png)

Viene visualizzata la pagina della panoramica della proprietà. Da qui, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Catalogo]**. Trova l’elenco per l’SDK per web di Platform (utilizzando facoltativamente la barra di ricerca per limitare i risultati) e seleziona **[!UICONTROL Installa]**.

![Installare l’SDK per web](./images/e2e/install-sdk.png)

Viene visualizzata la pagina di configurazione per l&#39;SDK. La maggior parte dei valori richiesti viene compilata automaticamente con valori predefiniti che è possibile scegliere di modificare se lo si desidera.

![Configurare l’SDK per web](./images/e2e/configure-sdk.png)

Prima di installare l’SDK, tuttavia, devi selezionare un datastream in modo che sappia dove inviare i dati. In **[!UICONTROL Datastreams]**, utilizza il menu a discesa per selezionare il datastream configurato in un [passaggio precedente](#datastream). Una volta impostato il datastream, seleziona **[!UICONTROL Salva]** per completare l&#39;installazione dell&#39;SDK nella proprietà.

![Imposta datastream e salva](./images/e2e/set-datastream.png)

### Creare un elemento dati XDM {#data-element}

Affinché l&#39;SDK invii dati alla rete Edge, questi devono essere mappati sullo schema XDM creato in un [passaggio precedente](#schema). Questa mappatura viene eseguita utilizzando un elemento dati.

Nell&#39;interfaccia utente, seleziona **[!UICONTROL Elementi dati]**, quindi seleziona **[!UICONTROL Crea nuovo elemento dati]**.

![Crea nuovo elemento dati](./images/e2e/data-elements.png)

Nella schermata successiva, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]** nel menu a discesa [!UICONTROL Estensione], quindi seleziona **[!UICONTROL Oggetto XDM]** per il tipo di elemento dati.

![Tipo di oggetto XDM](./images/e2e/xdm-object.png)

Viene visualizzata la finestra di dialogo di configurazione per il tipo di oggetto XDM. La finestra di dialogo seleziona automaticamente la sandbox di Platform e da qui puoi visualizzare tutti gli schemi creati in quella sandbox. Seleziona dall’elenco lo schema XDM creato in precedenza.

![Tipo di oggetto XDM](./images/e2e/select-schema.png)

Viene visualizzata la struttura dello schema. Tutti i campi con un asterisco (**\***) indicano i campi che verranno compilati automaticamente all’attivazione degli eventi. Per tutti gli altri campi, è possibile esplorare la struttura dello schema e compilare il resto dei dati.

![Mappatura di dati su campi XDM](./images/e2e/map-schema.png)

>[!NOTE]
>
>La schermata precedente illustra come mappare una variabile accessibile a livello globale dal lato client del sito web (`cartAbandonsTotal`) a un campo XDM facendo riferimento al suo nome nel campo [!UICONTROL Valore], circondato da segni di percentuale (`%`).
>
>Per compilare questi campi è inoltre possibile utilizzare altri elementi dati creati in precedenza. Per ulteriori informazioni, consulta il riferimento su [elementi dati](../tags/ui/managing-resources/data-elements.md) nella documentazione dei tag .

Una volta completata la mappatura dei dati sullo schema, fornisci un nome per l&#39;elemento dati prima di selezionare **[!UICONTROL Salva]**.

![Denomina e salva elemento dati](./images/e2e/name-and-save.png)

### Creare una regola

Dopo aver salvato l’elemento dati, il passaggio successivo consiste nel creare una regola che lo invierà alla rete Edge ogni volta che si verifica un determinato evento sul sito web (ad esempio quando un cliente aggiunge un prodotto a un carrello).

Puoi impostare regole per praticamente qualsiasi evento che può verificarsi sul tuo sito web. Ad esempio, in questa sezione viene illustrato come creare una regola che si attivi quando un cliente invia un modulo. Il seguente HTML rappresenta una semplice pagina web con un modulo &quot;Aggiungi al carrello&quot;, che sarà oggetto della regola:

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

Nell’interfaccia utente Raccolta dati, seleziona **[!UICONTROL Regole]** nel menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Crea nuova regola]**.

![Regole](./images/e2e/rules.png)

Nella schermata successiva, specifica un nome per la regola. Da qui, il passaggio successivo consiste nel determinare l&#39;evento per la regola (in altre parole, quando la regola verrà attivata). Seleziona **[!UICONTROL Aggiungi]** in [!UICONTROL Eventi].

![Regola di nome](./images/e2e/name-rule.png)

Viene visualizzata la pagina di configurazione dell’evento. Per configurare un evento, devi innanzitutto selezionare il tipo di evento. I tipi di evento vengono forniti dalle estensioni. Per impostare un evento &quot;invio modulo&quot;, ad esempio, seleziona l’estensione **[!UICONTROL Core]**, quindi seleziona il tipo di evento **[!UICONTROL Submit]** sotto la categoria **[!UICONTROL Form]** .

>[!NOTE]
>
>Per ulteriori informazioni sui diversi tipi di eventi forniti da estensioni Web di Adobe, tra cui come configurarli, consulta la sezione [Guida di riferimento delle estensioni Adobe](../tags/extensions/web/overview.md) nella documentazione sui tag.

L’evento di invio del modulo consente di utilizzare un [selettore CSS](https://www.w3schools.com/css/css_selectors.asp) per fare riferimento a un elemento specifico su cui attivare la regola. Nell’esempio seguente, viene utilizzato l’ID `add-to-cart-form` in modo che questa regola venga attivata solo per il modulo &quot;Aggiungi al carrello&quot;. Seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;evento alla regola.

![Configurazione evento](./images/e2e/event-config.png)

Viene visualizzata nuovamente la pagina di configurazione della regola, che mostra che l’evento è stato aggiunto. Puoi limitare il valore &quot;[!UICONTROL If]&quot; aggiungendo ulteriori condizioni alla regola.

In caso contrario, il passaggio successivo consiste nell’aggiungere un’azione da eseguire nella regola quando viene attivata. Seleziona **[!UICONTROL Aggiungi]** in **[!UICONTROL Azioni]** per continuare.

![Aggiungi azione](./images/e2e/add-action.png)

Viene visualizzata la pagina di configurazione dell’azione. Per ottenere l&#39;invio dei dati alla rete Edge, selezionare **[!UICONTROL Adobe Experience Platform Web SDK]** per l&#39;estensione e **[!UICONTROL Invia evento]** per il tipo di azione.

![Tipo di azione](./images/e2e/action-type.png)

La schermata si aggiorna e mostra opzioni aggiuntive per configurare l’azione Invia evento. In **[!UICONTROL Tipo]** è possibile specificare un valore di tipo personalizzato per compilare il campo `eventType` XDM. In **[!UICONTROL Dati XDM]**, specificare il nome del tipo di dati XDM creato in precedenza (circondato da segni di percentuale) oppure selezionare l&#39;icona del database (![Icona del database](./images/e2e/database-symbol.png)) per selezionarlo da un elenco. Si tratta dei dati che verranno infine inviati alla rete Edge.

Al termine, seleziona **[!UICONTROL Mantieni modifiche]**.

![Configurazione azione](./images/e2e/action-config.png)

Al termine della configurazione della regola, seleziona **[!UICONTROL Salva]** per completare il processo.

![Salva regola](./images/e2e/save-rule.png)

### Creare e installare una libreria {#library}

Una volta configurata la regola, puoi aggiungerla a una libreria di tag, generarla in un ambiente e installarla sul tuo sito web.

>[!NOTE]
>
>Se non hai ancora configurato un ambiente nell’interfaccia utente di raccolta dati, devi farlo prima di poter creare una build. Per ulteriori informazioni, consulta la sezione sulla [configurazione di un ambiente per una proprietà web](../tags/ui/publishing/environments.md#web-configuration) nella documentazione sui tag .

Per informazioni su come creare una libreria, aggiungere estensioni e regole alla libreria e creare tale libreria in un ambiente, consulta la guida alla [gestione delle librerie](../tags/ui/publishing/libraries.md) nella documentazione sui tag. Quando crei la libreria, accertati di includere l’estensione Platform Web SDK e le regole di raccolta dati create in precedenza.

Dopo aver creato la libreria e aver assegnato la relativa build a un ambiente, puoi installarlo sul lato client del sito web. Per ulteriori informazioni, consulta la sezione sull’ [installazione di ambienti](../tags/ui/publishing/environments.md#installation) .

Dopo aver installato l&#39;ambiente sul sito web, puoi [testare l&#39;implementazione](../tags/ui/publishing/embed-code-testing.md) utilizzando Adobe Experience Platform Debugger.

## Configurare l’inoltro eventi (facoltativo) {#event-forwarding}

>[!NOTE]
>
>L’inoltro degli eventi è disponibile solo per le organizzazioni autorizzate.

Dopo aver configurato l’SDK per l’invio di dati alla rete Edge, puoi impostare l’inoltro eventi per indicare alla rete Edge in cui desideri che tali dati vengano inviati.

Per utilizzare l&#39;inoltro eventi, è innanzitutto necessario creare una proprietà di inoltro eventi. Seleziona **[!UICONTROL Inoltro evento]** nella barra di navigazione a sinistra, quindi seleziona **[!UICONTROL Nuova proprietà]**. Immetti un nome per la proprietà prima di selezionare **[!UICONTROL Salva]**.

Una volta creata la proprietà di inoltro di un evento, il passaggio successivo consiste nel creare una regola che determini dove devono essere inviati i dati. Le regole per le proprietà di inoltro eventi sono costruite in modo simile alle proprietà dei tag, con l&#39;eccezione che non è possibile specificare alcun evento (poiché l&#39;inoltro eventi riguarda solo gli eventi che riceve direttamente dal datastream). Per l&#39;azione della regola, puoi utilizzare una delle estensioni di inoltro eventi disponibili oppure utilizzare codice personalizzato per distribuire l&#39;evento.

![Regola di inoltro eventi](./images/e2e/event-forwarding-rule.png)

Come in precedenza, dopo aver configurato la regola, devi aggiungerla a una libreria e generarla in un ambiente.

Al termine della compilazione, il passaggio finale è quello di aggiornare il datastream [configurato in precedenza](#datastream) e abilitare l&#39;inoltro eventi. Per iniziare, vai a **[!UICONTROL Datastreams]** e seleziona il datastream in questione dall&#39;elenco. Da qui, abilita l’opzione per l’inoltro eventi e fornisci i nomi della proprietà e dell’ambiente appena configurati.

![Archivio dati inoltro eventi](./images/e2e/event-forwarding-datastream.png)

## Passaggi successivi

Questa guida fornisce una panoramica completa e dettagliata su come inviare dati alla rete Edge tramite l’SDK per web di Platform. Per ulteriori informazioni sui vari componenti e servizi interessati, consulta la documentazione collegata a in questa guida.
