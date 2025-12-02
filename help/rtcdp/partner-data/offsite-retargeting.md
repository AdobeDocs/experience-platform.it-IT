---
title: Retargeting fuori sede di visitatori non autenticati
description: Scopri come eseguire il retargeting degli utenti non autenticati utilizzando gli ID potenziali clienti per creare un attributo calcolato che può essere utilizzato per creare un pubblico di utenti non autenticati.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1358'
ht-degree: 1%

---

# Retargeting fuori sede dei visitatori non autenticati

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che dispongono di una licenza per Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Ulteriori informazioni su questi pacchetti sono disponibili nelle [descrizioni dei prodotti](https://helpx.adobe.com/it/legal/product-descriptions.html). Contatta il tuo rappresentante Adobe per ulteriori informazioni.

Scopri come creare un pubblico di visitatori non autenticati ed effettuare il retargeting utilizzando gli ID duraturi forniti dai partner.

![Infografica che mostra il flusso di dati dei partner dall&#39;acquisizione in Adobe Experience Platform all&#39;output tramite tipi di pubblico in una destinazione a valle.](../assets/offsite-retargeting/header.png)

## Perché considerare questo caso d’uso {#why-use-case}

Con la graduale eliminazione dei cookie di terze parti, gli esperti di marketing digitale devono ridefinire le proprie strategie per coinvolgere di nuovo i visitatori anonimi. I brand che scelgono di integrarsi con i fornitori di identità per il riconoscimento dei visitatori in tempo reale possono anche sfruttare gli identificatori duraturi forniti dai partner per il retargeting dei contenuti multimediali a pagamento fuori dal sito.

Nonostante l’elevato volume di traffico, molti marchi riscontrano un calo significativo nella fase di conversione. I visitatori possono interagire con i contenuti e le demo dei prodotti, ma se ne vanno senza registrarsi o effettuare un acquisto.

Non solo puoi creare tipi di pubblico basati sul coinvolgimento nel sito per personalizzare i messaggi di marketing, ma puoi anche utilizzare il supporto di Adobe per gli ID partner per coinvolgere di nuovo i visitatori su destinazioni di media a pagamento.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Quando pianifichi il retargeting di visitatori non autenticati, tieni presente i seguenti prerequisiti durante il processo di pianificazione:

- Ho impostato gli ID partner con gli spazi dei nomi di identità corretti?

Inoltre, per implementare il caso d’uso, utilizzerai le seguenti funzionalità di Real-Time CDP ed elementi dell’interfaccia utente. Verificare di disporre delle autorizzazioni di controllo dell&#39;accesso basate su attributi necessarie per tutte queste aree o richiedere all&#39;amministratore di sistema di concedere le autorizzazioni necessarie.

- [Tipi di pubblico](/help/segmentation/home.md)
- [Attributi calcolati](/help/profile/computed-attributes/overview.md)
- [Destinazioni](/help/destinations/home.md)
- [Raccolta dati](/help/collection/home.md)

## Trasmettere i dati dei partner in Real-Time CDP {#get-data-in}

Per creare un pubblico di visitatori non autenticati, devi prima inserire i dati dei tuoi partner in Real-Time CDP.

Per informazioni su come importare in modo ottimale i dati in Real-Time CDP utilizzando Web SDK, leggere le [sezioni sulla gestione dei dati e sulla raccolta dei dati degli eventi](./onsite-personalization.md#data-management) del caso di utilizzo della personalizzazione nel sito.

## Portare avanti gli ID forniti dal partner {#bring-partner-ids-forward}

Dopo aver importato gli ID forniti dal partner in un set di dati evento, devi inserire questi dati nei record del profilo. Per farlo, puoi utilizzare attributi calcolati.

Gli attributi calcolati consentono di convertire rapidamente i dati comportamentali del profilo in valori aggregati a livello di profilo. Di conseguenza, puoi utilizzare queste espressioni, ad esempio &quot;totale degli acquisti per tutta la durata&quot; nel profilo, consentendoti di utilizzare facilmente l’attributo calcolato all’interno dei tipi di pubblico. Ulteriori informazioni sugli attributi calcolati sono disponibili nella [panoramica attributi calcolati](/help/profile/computed-attributes/overview.md).

Per accedere agli attributi calcolati, selezionare **[!UICONTROL Profiles]** seguito da **[!UICONTROL Computed attributes]** e **[!UICONTROL Create computed attribute]**.

![Il pulsante [!UICONTROL Create computed attributes] è evidenziato oltre alla scheda [!UICONTROL Computed attributes] nell&#39;area di lavoro [!UICONTROL Profiles].](../assets/offsite-retargeting/create-ca.png)

Viene visualizzata la pagina **[!UICONTROL Create computed attribute]**. In questa pagina puoi utilizzare i componenti per creare l’attributo calcolato.

![Viene visualizzata l&#39;area di lavoro per la creazione di attributi calcolati.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Per informazioni più dettagliate sulla creazione di attributi calcolati, consulta la [guida dell&#39;interfaccia utente attributi calcolati](/help/profile/computed-attributes/ui.md).

Per questo caso d’uso, puoi creare un attributo calcolato che, se esiste l’ID partner, ottiene il valore più recente dell’ID partner entro le ultime 24 ore.

Utilizzando la barra di ricerca, puoi individuare e aggiungere l&#39;evento &quot;Partner ID&quot; [creato durante il caso di utilizzo della personalizzazione nel sito](#get-data-in) all&#39;area di lavoro degli attributi calcolati.

![La scheda [!UICONTROL Events] e la barra di ricerca sono evidenziate.](../assets/offsite-retargeting/ca-add-partner-id.png)

Dopo aver aggiunto l&#39;evento &quot;Partner ID&quot; alla definizione, imposta la condizione di filtro dell&#39;evento su **[!UICONTROL Exists]**, imposta la condizione di filtro dell&#39;evento su **[!UICONTROL Most Recent]** del valore dell&#39;ID partner aggiunto e con un periodo di lookback di 24 ore.

![La definizione dell&#39;attributo calcolato che si desidera creare è evidenziata.](../assets/offsite-retargeting/ca-add-definition.png)

Assegnare all&#39;attributo calcolato un nome appropriato (ad esempio &quot;ID partner&quot;) e una descrizione, quindi selezionare **[!UICONTROL Publish]** per completare il processo di creazione dell&#39;attributo calcolato.

![Le informazioni di base dell&#39;attributo calcolato che si desidera creare sono evidenziate.](../assets/offsite-retargeting/ca-publish.png)

## Creare un pubblico utilizzando l’attributo calcolato {#create-audience}

Dopo aver creato l’attributo calcolato, puoi utilizzarlo per creare un pubblico. In questo esempio, creerai un pubblico composto da visitatori che hanno visitato il tuo sito web più di 5 volte nel corso del mese ma che non si sono ancora iscritti.

Per creare un pubblico, seleziona **[!UICONTROL Audiences]**, seguito da **[!UICONTROL Create audience]**.

![Il pulsante [!UICONTROL Create audience] è evidenziato.](../assets/offsite-retargeting/create-audience.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di scegliere tra [!UICONTROL Compose audience] e [!UICONTROL Build rule]. Seleziona **[!UICONTROL Build rule]** seguito da **[!UICONTROL Create]**.

![Il pulsante [!UICONTROL Build rule] è evidenziato.](../assets/offsite-retargeting/select-build-rule.png)

Viene visualizzata la pagina Generatore di segmenti. In questa pagina puoi utilizzare i componenti per creare il pubblico.

![Viene visualizzato il Generatore di segmenti.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Per informazioni più dettagliate sull&#39;utilizzo del Generatore di segmenti, consulta la [Guida dell&#39;interfaccia utente del Generatore di segmenti](/help/segmentation/ui/segment-builder.md).

Per raggiungere l&#39;obiettivo di trovare questi visitatori, devi innanzitutto aggiungere un evento **[!UICONTROL Page View]** al pubblico. Seleziona la scheda **[!UICONTROL Events]** in **[!UICONTROL Fields]**, quindi trascina e rilascia l&#39;evento **[!UICONTROL Page View]** e aggiungilo all&#39;area di lavoro della sezione eventi.

![La scheda [!UICONTROL Events] nella sezione [!UICONTROL Fields] è evidenziata durante la visualizzazione dell&#39;evento [!UICONTROL Page View].](../assets/offsite-retargeting/add-page-view.png)

Seleziona l&#39;evento **[!UICONTROL Page View]** appena aggiunto. Modifica il periodo di lookback da **[!UICONTROL Any time]** a **[!UICONTROL This month]** e modifica la regola dell&#39;evento in modo che includa **Almeno 5**.

![Vengono visualizzati i dettagli dell&#39;evento [!UICONTROL Page View] aggiunto.](../assets/offsite-retargeting/edit-event.png)

Dopo aver aggiunto l’evento, devi aggiungere un attributo. Poiché stai lavorando con visitatori non autenticati, puoi aggiungere l’attributo calcolato appena creato. Questo attributo calcolato appena creato consente di collegare gli ID partner a un pubblico.

Per aggiungere l&#39;attributo calcolato, in **[!UICONTROL Attributes]**, selezionare **[!UICONTROL XDM Individual Profile]**, seguito da **[ID tenant dell&#39;organizzazione](/help/xdm/api/getting-started.md#know-your-tenant-id).**, **[!UICONTROL SystemComputedAttributes]** e **[!UICONTROL PartnerID]**. Aggiungere ora **[!UICONTROL Value]** dell&#39;attributo calcolato alla sezione degli attributi dell&#39;area di lavoro.

![Viene visualizzato il percorso della cartella per accedere all&#39;attributo calcolato.](../assets/offsite-retargeting/access-computed-attribute.png)

Inoltre, cercare **[!UICONTROL Personal Email]** e aggiungere l&#39;attributo **[!UICONTROL Address]** sotto **[!UICONTROL PartnerID]** alla sezione degli attributi dell&#39;area di lavoro.

![L&#39;attributo calcolato [!UICONTROL PartnerID] e l&#39;attributo [!UICONTROL Personal Email Address] sono evidenziati nell&#39;area di lavoro del Generatore di segmenti.](../assets/offsite-retargeting/added-attributes.png)

Dopo aver aggiunto gli attributi, è necessario impostare i relativi criteri di valutazione. Per **[!UICONTROL PartnerID]**, impostare il criterio su **[!UICONTROL exists]** e per **[!UICONTROL Address]**, impostare il criterio su **[!UICONTROL does not exist]**.

![I valori corretti degli attributi sono evidenziati.](../assets/offsite-retargeting/set-attribute-values.png)

Hai creato correttamente un pubblico che cerca visitatori ad alta intensità che dispongono di un ID fornito dal partner ma che non si sono ancora iscritti al tuo sito. Assegna al pubblico il nome &quot;Retargeting di utenti non autenticati&quot; e seleziona **[!UICONTROL Save]** per completare la creazione del pubblico.

![Le proprietà del pubblico sono evidenziate.](../assets/offsite-retargeting/save-audience-properties.png)

## Attiva il pubblico {#activate-audience}

Dopo aver creato correttamente il pubblico, ora puoi attivarlo nelle destinazioni a valle. Seleziona **[!UICONTROL Audiences]** nella barra di navigazione a sinistra, cerca il nuovo pubblico creato, seleziona l&#39;icona dei puntini di sospensione e seleziona **[!UICONTROL Activate to destination]**.

![Il pulsante [!UICONTROL Activate to destination] è evidenziato.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Tutti i tipi di destinazione, comprese le destinazioni basate su file, supportano l’attivazione del pubblico con gli ID partner.
>
>Per ulteriori informazioni sull&#39;attivazione di tipi di pubblico in una destinazione, leggere la [panoramica sull&#39;attivazione](/help/destinations/ui/activation-overview.md).

Viene visualizzata la pagina **[!UICONTROL Activate destination]**. In questa pagina puoi selezionare la destinazione in cui desideri attivare la destinazione. Dopo aver selezionato la destinazione desiderata, selezionare **[!UICONTROL Next]**.

![La destinazione a cui desideri attivare il pubblico è evidenziata.](../assets/offsite-retargeting/select-destination.png)

Viene visualizzata la pagina **[!UICONTROL Scheduling]**. In questa pagina puoi creare una pianificazione che determina la frequenza con cui desideri attivare il pubblico. Seleziona **[!UICONTROL Create schedule]** per creare una pianificazione per l&#39;attivazione del pubblico.

![Il pulsante [!UICONTROL Create schedule] è evidenziato.](../assets/offsite-retargeting/select-create-schedule.png)

Verrà visualizzato il popover [!UICONTROL Scheduling]. In questa pagina puoi creare la pianificazione per l’attivazione del pubblico. Dopo aver configurato la pianificazione, selezionare **[!UICONTROL Create]** per continuare.

![Viene visualizzato il popover di configurazione della pianificazione.](../assets/offsite-retargeting/configure-schedule.png)

Dopo aver confermato i dettagli della pianificazione, selezionare **[!UICONTROL Next]**.

![Vengono visualizzati i dettagli della pianificazione.](../assets/offsite-retargeting/created-schedule.png)

Viene visualizzata la pagina **[!UICONTROL Select attributes]**. In questa pagina puoi selezionare gli attributi da esportare insieme al pubblico attivato. Come minimo, includi l’ID partner, in quanto ti consentirà di identificare i visitatori di cui intendi effettuare il retargeting. Selezionare **[!UICONTROL Add new mapping]** e cercare l&#39;attributo calcolato. Dopo aver aggiunto gli attributi necessari, selezionare **[!UICONTROL Next]**.

![Il pulsante [!UICONTROL Add new mapping] e l&#39;attributo calcolato sono evidenziati.](../assets/offsite-retargeting/add-new-mapping.png)

Viene visualizzata la pagina **[!UICONTROL Review]**. In questa pagina puoi rivedere i dettagli dell’attivazione del pubblico. Se si è soddisfatti dei dettagli forniti, selezionare **[!UICONTROL Finish]**.

![Viene visualizzata la pagina [!UICONTROL Review] con i dettagli dell&#39;attivazione del pubblico.](../assets/offsite-retargeting/review-destination-activation.png)

Ora hai attivato un pubblico di utenti non autenticati su una destinazione a valle per un ulteriore retargeting.

## Altri casi d’uso {#other-use-cases}

Puoi esplorare altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

- [Coinvolgi e acquisisci nuovi clienti](./prospecting.md) utilizzando i dati dei partner.
- [Personalizza le esperienze nel sito](./offsite-retargeting.md) con il riconoscimento dei visitatori supportato dai partner.
- [Integrare i profili di prime parti](./supplement-first-party-profiles.md) con gli attributi forniti dai partner.
