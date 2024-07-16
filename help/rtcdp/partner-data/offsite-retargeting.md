---
title: Retargeting fuori sede di visitatori non autenticati
description: Scopri come eseguire il retargeting degli utenti non autenticati utilizzando gli ID potenziali clienti per creare un attributo calcolato che può essere utilizzato per creare un pubblico di utenti non autenticati.
feature: Use Cases, Customer Acquisition
exl-id: cffa3873-d713-445a-a3e1-1edf1aa8eebb
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1462'
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

- [Tipi di pubblico](../../segmentation/home.md)
- [Attributi calcolati](../../profile/computed-attributes/overview.md)
- [Destinazioni](../../destinations/home.md)
- [SDK per web](../../web-sdk/home.md)

## Trasmettere i dati dei partner in Real-Time CDP {#get-data-in}

Per creare un pubblico di visitatori non autenticati, devi prima inserire i dati dei tuoi partner in Real-Time CDP.

Per informazioni su come importare in modo ottimale i dati in Real-Time CDP utilizzando Web SDK, leggere le [sezioni sulla gestione dei dati e sulla raccolta dei dati degli eventi](./onsite-personalization.md#data-management) del caso di utilizzo della personalizzazione nel sito.

## Portare avanti gli ID forniti dal partner {#bring-partner-ids-forward}

Dopo aver importato gli ID forniti dal partner in un set di dati evento, devi inserire questi dati nei record del profilo. Per farlo, puoi utilizzare attributi calcolati.

Gli attributi calcolati consentono di convertire rapidamente i dati comportamentali del profilo in valori aggregati a livello di profilo. Di conseguenza, puoi utilizzare queste espressioni, ad esempio &quot;totale degli acquisti per tutta la durata&quot; nel profilo, consentendoti di utilizzare facilmente l’attributo calcolato all’interno dei tipi di pubblico. Ulteriori informazioni sugli attributi calcolati sono disponibili nella [panoramica attributi calcolati](../../profile/computed-attributes/overview.md).

Per accedere agli attributi calcolati, selezionare **[!UICONTROL Profili]** seguito da **[!UICONTROL Attributi calcolati]** e **[!UICONTROL Crea attributo calcolato]**.

![Il pulsante [!UICONTROL Crea attributi calcolati] è evidenziato oltre alla scheda [!UICONTROL Attributi calcolati] nell&#39;area di lavoro [!UICONTROL Profili].](../assets/offsite-retargeting/create-ca.png)

Viene visualizzata la pagina **[!UICONTROL Crea attributo calcolato]**. In questa pagina puoi utilizzare i componenti per creare l’attributo calcolato.

![Viene visualizzata l&#39;area di lavoro per la creazione di attributi calcolati.](../assets/offsite-retargeting/ca-page.png)

>[!NOTE]
>
>Per informazioni più dettagliate sulla creazione di attributi calcolati, consulta la [guida dell&#39;interfaccia utente attributi calcolati](../../profile/computed-attributes/ui.md).

Per questo caso d’uso, puoi creare un attributo calcolato che, se esiste l’ID partner, ottiene il valore più recente dell’ID partner entro le ultime 24 ore.

Utilizzando la barra di ricerca, puoi individuare e aggiungere l&#39;evento &quot;Partner ID&quot; [creato durante il caso di utilizzo della personalizzazione nel sito](#get-data-in) all&#39;area di lavoro degli attributi calcolati.

![La scheda [!UICONTROL Eventi] e la barra di ricerca sono evidenziate.](../assets/offsite-retargeting/ca-add-partner-id.png)

Dopo aver aggiunto l&#39;evento &quot;Partner ID&quot; alla definizione, imposta la condizione di filtro dell&#39;evento su **[!UICONTROL Exists]**, imposta la condizione di filtro dell&#39;evento sul valore **[!UICONTROL Most Recent]** dell&#39;ID partner aggiunto e con un periodo di lookback di 24 ore.

![La definizione dell&#39;attributo calcolato che si desidera creare è evidenziata.](../assets/offsite-retargeting/ca-add-definition.png)

Assegna all&#39;attributo calcolato un nome appropriato (ad esempio &quot;ID partner&quot;) e una descrizione, quindi seleziona **[!UICONTROL Publish]** per completare il processo di creazione dell&#39;attributo calcolato.

![Le informazioni di base dell&#39;attributo calcolato che si desidera creare sono evidenziate.](../assets/offsite-retargeting/ca-publish.png)

## Creare un pubblico utilizzando l’attributo calcolato {#create-audience}

Dopo aver creato l’attributo calcolato, puoi utilizzarlo per creare un pubblico. In questo esempio, creerai un pubblico composto da visitatori che hanno visitato il tuo sito web più di 5 volte nel corso del mese ma che non si sono ancora iscritti.

Per creare un pubblico, seleziona **[!UICONTROL Tipi di pubblico]**, seguito da **[!UICONTROL Crea pubblico]**.

![Il pulsante [!UICONTROL Crea pubblico] è evidenziato.](../assets/offsite-retargeting/create-audience.png)

Viene visualizzata una finestra di dialogo che richiede di scegliere tra [!UICONTROL Componi pubblico] e [!UICONTROL Genera regola]. Seleziona **[!UICONTROL Genera regola]** seguito da **[!UICONTROL Crea]**.

![Il pulsante [!UICONTROL Genera regola] è evidenziato.](../assets/offsite-retargeting/select-build-rule.png)

Viene visualizzata la pagina Generatore di segmenti. In questa pagina puoi utilizzare i componenti per creare il pubblico.

![Viene visualizzato il Generatore di segmenti.](../assets/offsite-retargeting/segment-builder.png)

>[!NOTE]
>
>Per informazioni più dettagliate sull&#39;utilizzo del Generatore di segmenti, consulta la [Guida dell&#39;interfaccia utente del Generatore di segmenti](../../segmentation/ui/segment-builder.md).

Per raggiungere l&#39;obiettivo di trovare questi visitatori, devi innanzitutto aggiungere al pubblico un evento **[!UICONTROL Visualizzazione pagina]**. Seleziona la scheda **[!UICONTROL Eventi]** in **[!UICONTROL Campi]**, quindi trascina e rilascia l&#39;evento **[!UICONTROL Visualizzazione pagina]** e aggiungilo all&#39;area di lavoro della sezione eventi.

![La scheda [!UICONTROL Eventi] nella sezione [!UICONTROL Campi] è evidenziata durante la visualizzazione dell&#39;evento [!UICONTROL Visualizzazione pagina].](../assets/offsite-retargeting/add-page-view.png)

Seleziona l&#39;evento **[!UICONTROL Visualizzazione pagina]** appena aggiunto. Modifica il periodo di lookback da **[!UICONTROL In qualsiasi momento]** a **[!UICONTROL Questo mese]** e modifica la regola dell&#39;evento affinché includa **Almeno 5**.

![Vengono visualizzati i dettagli dell&#39;evento [!UICONTROL Visualizzazione pagina] aggiunto.](../assets/offsite-retargeting/edit-event.png)

Dopo aver aggiunto l’evento, devi aggiungere un attributo. Poiché stai lavorando con visitatori non autenticati, puoi aggiungere l’attributo calcolato appena creato. Questo attributo calcolato appena creato consente di collegare gli ID partner a un pubblico.

Per aggiungere l&#39;attributo calcolato, in **[!UICONTROL Attributi]**, seleziona **[!UICONTROL Profilo individuale XDM]**, seguito dall&#39;ID tenant ](../../xdm/api/getting-started.md#know-your-tenant-id) della tua organizzazione.**[**, **[!UICONTROL SystemComputedAttributes]** e **[!UICONTROL PartnerID]**. Ora aggiungi **[!UICONTROL Valore]** dell&#39;attributo calcolato alla sezione degli attributi dell&#39;area di lavoro.

![Viene visualizzato il percorso della cartella per accedere all&#39;attributo calcolato.](../assets/offsite-retargeting/access-computed-attribute.png)

Cerca inoltre **[!UICONTROL Indirizzo e-mail personale]** e aggiungi l&#39;attributo **[!UICONTROL Indirizzo]** sotto **[!UICONTROL ID partner]** alla sezione degli attributi dell&#39;area di lavoro.

![L&#39;attributo calcolato [!UICONTROL PartnerID] e l&#39;attributo [!UICONTROL Indirizzo e-mail personale] sono evidenziati nell&#39;area di lavoro del Generatore di segmenti.](../assets/offsite-retargeting/added-attributes.png)

Dopo aver aggiunto gli attributi, è necessario impostare i relativi criteri di valutazione. Per **[!UICONTROL PartnerID]**, impostare il criterio su **[!UICONTROL exists]** e per **[!UICONTROL Address]**, impostare il criterio su **[!UICONTROL does not exist]**.

![I valori corretti degli attributi sono evidenziati.](../assets/offsite-retargeting/set-attribute-values.png)

Hai creato correttamente un pubblico che cerca visitatori ad alta intensità che dispongono di un ID fornito dal partner ma che non si sono ancora iscritti al tuo sito. Assegna al pubblico un nome &quot;Retargeting di utenti non autenticati&quot; e seleziona **[!UICONTROL Salva]** per completare la creazione del pubblico.

![Le proprietà del pubblico sono evidenziate.](../assets/offsite-retargeting/save-audience-properties.png)

## Attiva il pubblico {#activate-audience}

Dopo aver creato correttamente il pubblico, ora puoi attivarlo nelle destinazioni a valle. Seleziona **[!UICONTROL Tipi di pubblico]** nella barra di navigazione a sinistra, cerca il nuovo pubblico creato, seleziona l&#39;icona con i puntini di sospensione, quindi seleziona **[!UICONTROL Attiva per destinazione]**.

![Il pulsante [!UICONTROL Attiva nella destinazione] è evidenziato.](../assets/offsite-retargeting/activate-to-destination.png)

>[!NOTE]
>
>Tutti i tipi di destinazione, comprese le destinazioni basate su file, supportano l’attivazione del pubblico con gli ID partner.
>
>Per ulteriori informazioni sull&#39;attivazione di tipi di pubblico in una destinazione, leggere la [panoramica sull&#39;attivazione](../../destinations/ui/activation-overview.md).

Viene visualizzata la pagina **[!UICONTROL Attiva destinazione]**. In questa pagina puoi selezionare la destinazione in cui desideri attivare la destinazione. Dopo aver selezionato la destinazione desiderata, selezionare **[!UICONTROL Avanti]**.

![La destinazione a cui desideri attivare il pubblico è evidenziata.](../assets/offsite-retargeting/select-destination.png)

Viene visualizzata la pagina **[!UICONTROL Pianificazione]**. In questa pagina puoi creare una pianificazione che determina la frequenza con cui desideri attivare il pubblico. Seleziona **[!UICONTROL Crea pianificazione]** per creare una pianificazione per l&#39;attivazione del pubblico.

![Il pulsante [!UICONTROL Crea pianificazione] è evidenziato.](../assets/offsite-retargeting/select-create-schedule.png)

Viene visualizzato il popover [!UICONTROL Pianificazione]. In questa pagina puoi creare la pianificazione per l’attivazione del pubblico. Dopo aver configurato la pianificazione, seleziona **[!UICONTROL Crea]** per continuare.

![Viene visualizzato il popover di configurazione della pianificazione.](../assets/offsite-retargeting/configure-schedule.png)

Dopo aver confermato i dettagli della pianificazione, seleziona **[!UICONTROL Avanti]**.

![Vengono visualizzati i dettagli della pianificazione.](../assets/offsite-retargeting/created-schedule.png)

Viene visualizzata la pagina **[!UICONTROL Seleziona attributi]**. In questa pagina puoi selezionare gli attributi da esportare insieme al pubblico attivato. Come minimo, includi l’ID partner, in quanto ti consentirà di identificare i visitatori di cui intendi effettuare il retargeting. Seleziona **[!UICONTROL Aggiungi nuova mappatura]** e cerca l&#39;attributo calcolato. Dopo aver aggiunto gli attributi necessari, seleziona **[!UICONTROL Avanti]**.

![Sono evidenziati sia il pulsante [!UICONTROL Aggiungi nuova mappatura] che l&#39;attributo calcolato.](../assets/offsite-retargeting/add-new-mapping.png)

Viene visualizzata la pagina **[!UICONTROL Rivedi]**. In questa pagina puoi rivedere i dettagli dell’attivazione del pubblico. Se sei soddisfatto dei dettagli forniti, seleziona **[!UICONTROL Fine]**.

![Viene visualizzata la pagina [!UICONTROL Rivedi], che mostra i dettagli dell&#39;attivazione del pubblico.](../assets/offsite-retargeting/review-destination-activation.png)

Ora hai attivato un pubblico di utenti non autenticati su una destinazione a valle per un ulteriore retargeting.

## Altri casi d’uso {#other-use-cases}

Puoi esplorare altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

- [Coinvolgi e acquisisci nuovi clienti](./prospecting.md) utilizzando i dati dei partner.
- [Personalizza le esperienze nel sito](./offsite-retargeting.md) con il riconoscimento dei visitatori supportato dai partner.
- [Integrare i profili di prime parti](./supplement-first-party-profiles.md) con gli attributi forniti dai partner.
