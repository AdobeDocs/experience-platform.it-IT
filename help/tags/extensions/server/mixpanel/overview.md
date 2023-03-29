---
keywords: estensione inoltro eventi;mixpanel;estensione inoltro eventi mixpanel
title: Estensione di inoltro eventi API di tracciamento eventi di Mixpanel
description: Questa estensione di inoltro eventi Adobe Experience Platform invia gli eventi Adobe Experience Edge Network a Mixpanel.
source-git-commit: 54aa55fbafb5e9603b109dbf015e009efd8f5e1d
workflow-type: tm+mt
source-wordcount: '2343'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] Estensione di inoltro eventi API

[[!DNL Mixpanel]](https://www.mixpanel.com) è uno strumento di analisi del prodotto che consente di acquisire dati su come gli utenti interagiscono con un prodotto digitale. Puoi analizzare i dati dei prodotti con report semplici e interattivi che ti consentono di eseguire query e visualizzare i dati con pochi clic. [!DNL Mixpanel] progettato per rendere i team più efficienti, consentendo a tutti di analizzare i dati degli utenti in tempo reale per identificare le tendenze, comprendere il comportamento degli utenti e prendere decisioni sul prodotto.

[!DNL Mixpanel] utilizza un modello basato su eventi e incentrato sull’utente che collega ogni interazione a un singolo utente. La [!DNL Mixpanel] il modello dati è basato sui concetti di utenti, eventi e proprietà.

>[!NOTE]
>
>Fai riferimento a [!DNL Mixpanel] documentazione [gestione delle identità](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) per comprendere come [!DNL Mixpanel] unisce gli eventi per creare cluster di identità. Si consiglia inoltre di rivedere il documento in [ID distinti](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) per capire come vengono utilizzati per identificare gli utenti nei dati dell’evento.

La [!DNL Mixpanel Track Events] L’estensione API ti consente di sfruttare entrambi [inoltro eventi](../../../ui/event-forwarding/overview.md) e [tag](../../../home.md) per acquisire informazioni sull’evento in Adobe Experience Platform Edge Network e inviarle a [!DNL Mixpanel] utilizzando [[!DNL Track Events] API](https://developer.mixpanel.com/reference/track-event). Questo documento illustra i casi d&#39;uso dell&#39;estensione, come installarla e come integrarne le funzionalità nell&#39;inoltro degli eventi [regole](../../../ui/managing-resources/rules.md).

## Casi d’uso

Usa questa estensione se desideri utilizzare i dati di Edge Network in [!DNL Mixpanel] per sfruttare le funzionalità di analisi dei prodotti.

Ad esempio, considera un’organizzazione retail con una presenza multicanale (sito web e dispositivi mobili). L’organizzazione acquisisce l’input transazionale o conversazionale come dati evento dalle proprie piattaforme e lo carica in [!DNL Mixpanel] utilizzo dell&#39;estensione di inoltro eventi.

I team di analisi possono quindi sfruttare [!DNL Mixpanel's] capacità di elaborare i set di dati e ricavare informazioni aziendali, che possono essere utilizzate per generare grafici, dashboard o altre visualizzazioni per informare le parti interessate del business.

Per ulteriori informazioni sui casi di utilizzo specifici per [!DNL Mixpanel], consulta la seguente documentazione:

* [Da nuovo a [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [Che cosa è [!DNL Mixpanel]?](https://developer.mixpanel.com/docs)
* [12 must-try [!DNL Mixpanel] caratteristiche](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] prerequisiti {#prerequisites-mixpanel}

È necessario disporre di un [!DNL Mixpanel] per utilizzare questa estensione. Vai a [[!DNL Mixpanel] pagina di registrazione](https://mixpanel.com/register/) per registrare e creare un account, se non ne hai già uno.

Assicurati che [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) è abilitata per il progetto. Passa a **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** e attivare/disattivare l&#39;impostazione.

<!-- (If these don't apply, do we need to include here at all?)
### API guardrails {#guardrails}

Refer to the [[!DNL Mixpanel] documentation](https://developer.mixpanel.com/reference/import-events#rate-limits) for limits and response codes. As [!DNL Mixpanel] only sends live events these limits should not apply.
-->

### Raccogli i dettagli di configurazione richiesti {#configuration-details}

Per collegare l&#39;Experience Platform a [!DNL Mixpanel] è necessario disporre dei seguenti input:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| Token di progetto | Token di progetto associato al [!DNL Mixpanel] conto. Fai riferimento a [!DNL Mixpanel] documentazione [ricerca del token di progetto](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) a titolo indicativo. | `25470xxxxxxxxxxxxxxxxxxx1289` |

## Prerequisiti per l’Experience Cloud

Questa sezione descrive i passaggi prerequisiti in Experience Cloud per tutte le implementazioni. A seconda delle esigenze di implementazione individuali, può essere utile impostare i seguenti costrutti prima di configurare l&#39;estensione:

1. A [schema](../../../../xdm/schema/composition.md) descrivere la struttura dei dati che si stanno acquisendo in Experience Cloud
1. A [datastream](https://experienceleague.adobe.com/docs/platform-learn/data-collection/event-forwarding/set-up-a-datastream.html) per indirizzare i dati in arrivo alle applicazioni Adobe Experience Cloud appropriate
1. A [set di dati](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=it) per memorizzare i dati raccolti

Per tutte le implementazioni, è necessario quanto segue sul lato Experience Cloud:

1. [Creare un segreto](#create-a-secret)
1. [Impostare le proprietà dei tag](#set-up-tag-properties)
1. [Aggiungere elementi dati nelle proprietà tag](#add-data-elements-within-tag-properties)
1. [Aggiungi regole nelle proprietà dei tag](#add-rules-within-tag-properties)

### Creare un segreto

Crea un nuovo [segreto di inoltro eventi](../../../ui/event-forwarding/secrets.md) e imposta il valore su [[!DNL Mixpanel] token di progetto](#configuration-details). Verrà utilizzato per autenticare la connessione al tuo account mantenendo al tempo stesso il valore protetto.

### Impostare le proprietà dei tag

[Creare una proprietà tag](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=en) oppure scegli una proprietà esistente da modificare. Questa proprietà verrà configurata per raccogliere le strutture di dati necessarie per [!DNL Mixpanel] vengono portati in Edge Network prima di essere inviati tramite l’inoltro eventi.

### Aggiungere elementi dati nelle proprietà tag

Se il tuo sito web utilizza [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs), devi [creare un elemento dati](../../../ui/managing-resources/data-elements.md) che utilizza **[!UICONTROL Cookie]** tipo (fornito dalla [[!UICONTROL Core] estensione tag](../../client/core/overview.md)) quindi [!DNL Mixpanel] `distinct_id` può essere letto dal cookie .

La **[!UICONTROL Nome cookie]** il valore deve corrispondere a [!DNL Mixpanel] nome cookie del sito web. Il nome deve avere un formato simile a `mp_{MIXPANEL_PROJECT_TOKEN_FOR_WEBSITE}_mixpanel`. Al termine, seleziona **[!UICONTROL Salva]**.

![Elemento dati ID distinto nelle proprietà Tag.](../../../images/extensions/server/mixpanel/distinctId-data-element.png)

>[!IMPORTANT]
>
>Nome dell’elemento dati sopra indicato (`distinctId` in questo esempio) deve corrispondere al nome utilizzato per lo stesso campo nello schema. Questo vale anche per l’elemento dati di inoltro eventi che verrà creato in seguito.

Per il secondo elemento dati, imposta il tipo su **[!UICONTROL Oggetto XDM]** (dal [Estensione Adobe Experience Platform Web SDK](../../client/sdk/overview.md)) e mapparla allo schema creato in precedenza. Quando mappi i dati, assicurati che il valore `distinct_id` elemento dati (che contiene [!DNL Mixpanel] `distinct_id` viene fatto riferimento come valore all&#39;interno di uno dei campi dello schema.

![Elemento dati oggetto XDM che associa il valore distinct_id dal cookie allo schema nelle proprietà Tag.](../../../images/extensions/server/mixpanel/xdm-data-element.png)

>[!NOTE]
>
>Se il tuo sito web non esegue il [!DNL Mixpanel] SDK, un Adobe Experience Cloud ID (ECID) verrà utilizzato come fallback `distinct_id` da trasmettere con l’evento inviato a [!DNL Mixpanel].

A seconda dello scenario, potrebbe essere necessario creare un altro elemento dati che può essere utilizzato per eseguire il mapping al nome dell&#39;evento nello schema. Questa operazione può essere eseguita utilizzando **[!UICONTROL Attributo DOM]** tipo fornito dal [!UICONTROL Core] estensione.

![Nome evento elemento dati nelle proprietà tag.](../../../images/extensions/server/mixpanel/eventname-signin-data-element.png)

### Aggiungi regole nelle proprietà dei tag

Una volta configurati gli elementi dati, puoi iniziare a creare regole che determinano a quali eventi verranno inviati i dati [!DNL Mixpanel].

Inizia creando una regola che viene attivata per l&#39;evento di identificazione utente. Questo può rappresentare login, iscrizioni, registrazioni o qualsiasi altro evento che si desidera utilizzare per l&#39;identificazione dell&#39;utente.

![Una regola di accesso nelle proprietà dei tag.](../../../images/extensions/server/mixpanel/tag-rule-complete.png)

Sotto **[!UICONTROL Eventi]**, aggiungi una condizione (specifica del sito web) che attiverà l’evento di identificazione . Di seguito è riportato un esempio di attivazione della regola di accesso con un clic dell’utente:

![Configurazione dell’evento per una regola di accesso nelle proprietà dei tag.](../../../images/extensions/server/mixpanel/tag-rule-event-config.png)

Seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l’evento alla regola.

Successivamente, sotto **[!UICONTROL Azioni]**, aggiungi le azioni risultanti che desideri che la regola esegua quando si attiva. Tra queste azioni devono essere **[!UICONTROL Invia evento]** fornito dall’estensione Platform Web SDK, che invia l’evento alla rete Edge, dove può essere rilevato dall’inoltro eventi con estensioni come [!DNL Mixpanel].

Durante la configurazione dell’azione, in **[!UICONTROL Dati XDM]** seleziona la [elemento dati creato in precedenza](#add-data-elements-within-tag-properties) che contiene `distinct_id` valore.

![Configurazione dell’azione per una regola di accesso nelle proprietà dei tag.](../../../images/extensions/server/mixpanel/tag-rule-action-config.png)

Seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;evento alla regola, quindi seleziona **[!UICONTROL Salva]** per aggiungere la regola alla libreria di tag. Da qui puoi [creare una nuova build e distribuirla nel sito web](../../../ui/publishing/overview.md).

## Installa e configura il [!DNL Mixpanel] estensione {#install}

Per installare l&#39;estensione, [creare una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nella navigazione a sinistra. In **[!UICONTROL Catalogo]** scheda , seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Mixpanel] estensione.

![Installazione di [!DNL Mixpanel] estensione.](../../../images/extensions/server/mixpanel/install-extension.png)

## Configurare gli elementi dati di inoltro eventi

Dopo aver installato l’estensione, il passaggio successivo consiste nel creare elementi di dati di inoltro eventi che acquisiranno i costrutti di dati necessari a cui verrà inviato [!DNL Mixpanel].

### Crea un `distinctId` elemento dati

Aggiungi elementi dati in inoltro eventi. Se il sito è configurato con il [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs) la [elemento dati della proprietà tag](#setup-tag-properties-data-element) sarebbe stato definito. Per l’elemento dati di inoltro eventi, ora fornisci un **[!UICONTROL Percorso]** invece.

![Aggiungi un elemento dati nell&#39;inoltro eventi.](../../../images/extensions/server/mixpanel/distinctId-ef-data-element.png)

### Crea un `event_type` elemento dati

Di seguito è riportato un esempio di un elemento dati definito per un tipo di evento:

![Tipo di evento di inoltro eventi.](../../../images/extensions/server/mixpanel/eventname-ef-data-element.png)

### Creare mappature aggiuntive degli elementi dati

La `distinctId` e `event_type` sono entrambi necessari per inviare dati a [!DNL Mixpanel], ma è anche consigliabile includere un ID utente noto e un oggetto dati personalizzato con ogni evento, se disponibile. Consulta la guida [[!DNL Mixpanel Track Events] API REST](https://developer.mixpanel.com/reference/track-event) per ulteriori indicazioni.

Di seguito sono descritte le mappature degli elementi dati consigliati.

>[!IMPORTANT]
>
>Tutti gli elementi di dati elencati di seguito devono utilizzare il **[!UICONTROL Percorso]** digita in modo che possano mappare campi specifici nello schema come descritto in **Percorso schema** colonna.
>
>Per i percorsi dello schema, devi sostituire il `{TENANT_ID}` segnaposto unico [ID tenant](../../../../xdm/api/getting-started.md#know-your-tenant_id), che funge da namespace per i campi personalizzati definiti dall’organizzazione.

| [!DNL Mixpanel] key | Percorso schema | Descrizione | Obbligatorio |
| --- | --- | --- | --- |
| [!DNL Mixpanel Distinct ID] | `arc.event.xdm._{TENANT_ID}.distinct_id` | `distinct_id` identifica l&#39;utente che ha eseguito l&#39;evento. `distinct_id` deve essere specificato su ogni evento, in quanto è fondamentale per [!DNL Mixpanel] eseguire analisi comportamentali in modo corretto ed efficiente, compresi utenti univoci, funnel, fidelizzazione, coorti e altro ancora. | Sì |
| [!DNL Event Type] | `arc.event.xdm._{TENANT_ID}.event_type` | Questo è il nome dell’evento. [!DNL Mixpanel] consiglia di mantenere il numero di nomi di eventi univoci relativamente piccolo e di utilizzare le proprietà per qualsiasi contesto variabile associato all&#39;evento.<br><br>Ad esempio, invece di tenere traccia di eventi con nomi come &quot;Registrazione a pagamento&quot; e &quot;Registrazione gratuita&quot;, è consigliabile tenere traccia di un evento denominato &quot;Registrazione&quot; e avere una proprietà denominata &quot;Tipo di account&quot; con valori potenziali &quot;paid&quot; e &quot;free&quot;. | Sì |
| [!DNL Known User ID] | `arc.event.xdm._{TENANT_ID}.LoginID` | L’ID e-mail o di accesso dell’utente, se disponibile. | No |
| [!DNL Data] | `arc.event.xdm._{TENANT_ID}.properties` | Un oggetto JSON che rappresenta tutte le proprietà relative all’evento. I dati vengono troncati a 255 caratteri. | No |

{style="table-layout:auto"}

## Configurare le regole di inoltro eventi

Una volta configurati tutti gli elementi dati, puoi iniziare a creare regole di inoltro eventi che determinano quando e come verranno inviati gli eventi a [!DNL Mixpanel]. Tuttavia, prima di configurare le regole, è importante comprendere in che modo funzionano i cluster di identità [!DNL Mixpanel] in modo che gli eventi inviati siano correttamente attribuiti ai singoli utenti.

### Informazioni sui cluster di identità in [!DNL Mixpanel]

In [!DNL Mixpanel], un cluster di identità contiene una raccolta di `distinct_id` valori collegati a un singolo utente. [!DNL Mixpanel] gestisce il clustering delle identità per ogni utente, risolvendo un singolo canale `distinct_id` da ogni cluster da utilizzare nel reporting. Puoi anche includere un identificatore personalizzato (denominato locale) `distinct_id`) per gli eventi anonimi che si verificano prima di un evento di identificazione utente.

[!DNL Mixpanel] risolve i cluster di identità tramite due metodi:

* **Identifica** : [!DNL Mixpanel] connette l&#39;identificatore scelto a un anonimo `distinct_id`. Se la [!DNL Mixpanel] L’SDK è configurato sul tuo sito web, Platform utilizzerà l’ `distinct_id` assegnato all&#39;utente attualmente connesso.
* **Alias**: [!DNL Mixpanel] unisce due non anonimi `distinct_id`s insieme se vengono passati altri criteri di unione.

>[!NOTE]
>
>Fai riferimento a [!DNL Mixpanel] documento [gestione delle identità](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) per ulteriori dettagli su questi metodi.
>
>Conferma di aver abilitato la [[!DNL Mixpanel] feature di unione delle identità](#prerequisites-mixpanel) per garantire una corretta risoluzione dei cluster di identità.

Di conseguenza, [!DNL Mixpanel] l&#39;estensione dell&#39;inoltro eventi supporta **[!UICONTROL Evento Track]** tipo di azione per la configurazione della regola.

>[!IMPORTANT]
>
>Per ogni regola, indipendentemente dal metodo di risoluzione del cluster di identità utilizzato, una delle azioni deve utilizzare il **[!UICONTROL Evento Track]** digitare. Senza questo tipo di azione, la regola non invierà eventi Adobe Experience Edge Network a [!DNL Mixpanel].

### Creare una regola di tracciamento degli eventi

Inizia a creare una nuova regola nella proprietà di inoltro eventi. Sotto **[!UICONTROL Azioni]**, aggiungi una nuova azione e imposta l&#39;estensione su **[!UICONTROL Pannello misto]**. Quindi, imposta il tipo di azione su **[!UICONTROL Evento Track]** per inviare eventi di Adobe Experience Edge Network a [!DNL Mixpanel].

| Ingresso | Descrizione |
| --- | --- |
| [!UICONTROL Token di progetto] | Questo campo deve essere mappato al token di progetto associato al [!DNL Mixpanel] conto. |
| [!UICONTROL Tipo evento] | Nome dell&#39;evento. |
| [!UICONTROL Ora evento] | Ora dell’evento. |
| [!UICONTROL ID distinto del pannello multiplo] | Questo campo deve essere mappato al `distinctId` elemento dati creato in precedenza. |
| [!UICONTROL Inserisci ID] | Questo campo deve essere mappato al `insertId` elemento dati. |
| [!UICONTROL Proprietà evento] | Scegli se fornire JSON non elaborato o utilizzare un set semplificato di input chiave-valore. |

>[!NOTE]
>
>Per ulteriori informazioni sui campi standard di un [!DNL Mixpanel] evento , fai riferimento al [documentazione ufficiale](https://developer.mixpanel.com/reference/import-events#event).

![Aggiungi una configurazione di azione della regola di inoltro eventi.](../../../images/extensions/server/mixpanel/track-event-action.png)

Una volta che [!UICONTROL Evento Track] viene aggiunta alla regola, puoi configurare le condizioni della regola in modo che si attivi solo per determinati eventi, oppure puoi lasciare vuota la sezione condizioni per attivare la regola per tutti gli eventi.

>[!IMPORTANT]
>
>Se il sito web utilizza la [!DNL Mixpanel] SDK, puoi continuare al passaggio successivo di [convalida dei dati in [!DNL Mixpanel]](#validate). Se non utilizzi il [!DNL Mixpanel] SDK, devi [creare una regola di tracciamento identità separata](#create-an-identity-tracking-rule) garantire che gli eventi appropriati e `distinct_id` vengono inviati a [!DNL Mixpanel] quando si verifica un evento di identificazione utente.

### Creare una regola di tracciamento delle identità

Se non utilizzi il [!DNL Mixpanel SDK], il passaggio successivo consiste nel creare un’altra regola. Questa regola assicura che ogni volta che si verifica un evento di identificazione dell’utente sul sito web (ad esempio un login, un abbonamento, una registrazione e così via), gli eventi appropriati e `distinct_id` vengono inviati a [!DNL Mixpanel].

Avvia il processo di creazione di una nuova regola. Per [!UICONTROL Condizioni] aggiungi una condizione che controlla se l’evento è un evento di identificazione utente. Nell’esempio seguente, la condizione utilizza un [!UICONTROL Value Comparison] (dal [!UICONTROL Core] estensione) per verificare se l&#39;evento in arrivo ha un nome evento uguale a `signin`, che indica un evento di accesso utente.

![Mostra la configurazione dell’azione per [!DNL Mixpanel] Tipi di azioni Alias e Identifica.](../../../images/extensions/server/mixpanel/ef-rule-condition.png)

Dopo aver aggiunto le condizioni appropriate alla regola, devi creare un [!UICONTROL Invia evento] per inviare eventi di Adobe Experience Edge Network a [!DNL Mixpanel].

![Aggiungi una configurazione di azione della regola di inoltro eventi.](../../../images/extensions/server/mixpanel/track-event-action.png)

>[!NOTE]
>
>Per ulteriori informazioni sulle identità in [!DNL Mixpanel], fare riferimento alla [documentazione ufficiale](https://developer.mixpanel.com/reference/create-identity).

Una volta aggiunta l’azione alla regola, seleziona **[!UICONTROL Salva]** per aggiungere la regola alla libreria di inoltro eventi. Da qui puoi [creare una nuova build e attivare le modifiche](../../../ui/publishing/overview.md).

![Aggiungi una regola di inoltro eventi per [!DNL Mixpanel] Tipi di azioni Alias e Identifica.](../../../images/extensions/server/mixpanel/ef-rule-complete.png)

## Convalida dei dati all’interno di [!DNL Mixpanel] {#validate}

Se l’implementazione ha esito positivo e gli eventi vengono raccolti, visualizzerai gli eventi all’interno del [[!DNL Mixpanel] console](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

Controlla se [!DNL Mixpanel] ha unito gli eventi di accesso al post con i valori e-mail e gli eventi creati durante l’utilizzo di **[!UICONTROL Invia evento]**. Se implementato correttamente, [!DNL Mixpanel] li associerà a un singolo [profilo utente](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## Passaggi successivi

Questa guida spiega come inviare eventi di conversione a [!DNL Mixpanel] utilizzo dell&#39;inoltro eventi. Questa estensione di inoltro eventi sfrutta la [!DNL Mixpanel] SDK e API JavaScript. Per ulteriori informazioni su queste tecnologie sottostanti, consulta la documentazione ufficiale:

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] API JavaScript](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

Per ulteriori informazioni sulle funzionalità di inoltro eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).
