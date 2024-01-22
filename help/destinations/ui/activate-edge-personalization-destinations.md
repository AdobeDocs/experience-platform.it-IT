---
title: Attivare i tipi di pubblico per Edge Personalization Destinations
description: Scopri come attivare tipi di pubblico da Adobe Experience Platform a destinazioni di personalizzazione Edge per casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: fbc2a6c81682797af4674adabff358a62d973007
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 2%

---


# Attivare i tipi di pubblico per Edge Personalization Destinations

## Panoramica {#overview}

Adobe Experience Platform utilizza [segmentazione Edge](../../segmentation/ui/edge-segmentation.md) insieme a [destinazioni edge](/help/destinations/destination-types.md#edge-personalization-destinations) per consentire ai clienti di creare e indirizzare il pubblico su larga scala, in tempo reale. Questa funzionalità consente di configurare casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.

Esempi di destinazioni Edge sono [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Personalizzazione personalizzata](../../destinations/catalog/personalization/custom-personalization.md) connessioni.

>[!NOTE]
>
>Quando [configurazione della connessione Adobe Target](../catalog/personalization/adobe-target-connection.md) *senza* utilizzando un ID dello stream di dati, i casi d’uso descritti in questo articolo non sono supportati. In assenza di uno stream di dati, sono supportati solo i casi di utilizzo di personalizzazione della sessione successiva.

>[!IMPORTANT]
> 
> * Per attivare i dati e abilitare [passaggio di mappatura](#mapping) del flusso di lavoro, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions).
> * Per attivare i dati senza passare attraverso [passaggio di mappatura](#mapping) del flusso di lavoro, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva segmento senza mappatura]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions).
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}
> 
> Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Questo articolo spiega il flusso di lavoro necessario per attivare i tipi di pubblico nelle destinazioni edge di Adobe Experience Platform. Se usato insieme a [segmentazione Edge](../../segmentation/ui/edge-segmentation.md) e l’ [mappatura attributi profilo](#mapping), queste destinazioni abilitano i casi d’uso per la personalizzazione della stessa pagina e della pagina successiva nelle tue proprietà web e mobili.

Per una breve panoramica su come configurare la connessione Adobe Target per la personalizzazione Edge, guarda il video seguente.

>[!NOTE]
>
>L’interfaccia utente di Experienci Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione del video. Per informazioni aggiornate, consulta i passaggi di configurazione descritti nelle sezioni seguenti.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Per una breve panoramica su come condividere tipi di pubblico e attributi di profilo con Adobe Target e destinazioni di personalizzazione personalizzate, guarda il video seguente.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Casi d’uso {#use-cases}

Utilizza soluzioni di personalizzazione di Adobe, come Adobe Target, o piattaforme partner di personalizzazione (ad esempio, [!DNL Optimizely], [!DNL Pega]), nonché sistemi proprietari (ad esempio, CMS interno) per fornire ai clienti un&#39;esperienza di personalizzazione più approfondita tramite [Personalizzazione personalizzata](../catalog/personalization/custom-personalization.md) destinazione. Tutto questo sfruttando anche le funzionalità di raccolta dati e segmentazione di Experienci Platform Edge Network.

I casi d’uso descritti di seguito includono sia la personalizzazione del sito che la pubblicità mirata nel sito.

Per abilitare questi casi d’uso, i clienti necessitano di un modo rapido e semplice per recuperare da Experienci Platform informazioni su tipi di pubblico e attributi di profilo e per inviarle all’utente [Adobe Target](../catalog/personalization/adobe-target-connection.md) o [Personalizzazione personalizzata](../catalog/personalization/custom-personalization.md) nell&#39;interfaccia utente di Experienci Platform.

### Personalizzazione stessa pagina {#same-page}

Un utente visita una pagina del sito web. Puoi utilizzare le informazioni sulla visita della pagina corrente (ad esempio, URL di riferimento, lingua del browser, informazioni sul prodotto incorporate) per selezionare l’azione o la decisione successiva (ad esempio, personalizzazione) utilizzando [Personalizzazione personalizzata](../catalog/personalization/custom-personalization.md) connessione per piattaforme non Adobi (ad esempio, [!DNL Pega], [!DNL Optimizely] o altri.).

### Personalizzazione della pagina successiva {#next-page}

Un utente visita la pagina A del sito web. In base a questa interazione, l’utente si è qualificato per un set di tipi di pubblico. L’utente fa quindi clic su un collegamento che li porta dalla pagina A alla pagina B. I tipi di pubblico per i quali l’utente si era qualificato durante la precedente interazione sulla pagina A, insieme agli aggiornamenti del profilo determinati dalla visita del sito web corrente, verranno utilizzati per potenziare l’azione o la decisione successiva (ad esempio, quale banner pubblicitario mostrare al visitatore o, in caso di test A/B, quale versione della pagina visualizzare).

### Personalizzazione sessione successiva {#next-session}

Un utente visita diverse pagine del sito web. In base a queste interazioni, l’utente si è qualificato per un set di tipi di pubblico. L’utente termina quindi la sessione di navigazione corrente.

Il giorno successivo, l’utente ritorna allo stesso sito web del cliente. I tipi di pubblico per i quali erano qualificati durante la precedente interazione con tutte le pagine del sito web visitate, insieme agli aggiornamenti del profilo determinati dalla visita del sito web corrente, verranno utilizzati per selezionare l’azione/decisione successiva (ad esempio, quale banner pubblicitario mostrare al visitatore o, in caso di test A/B, quale versione della pagina visualizzare).

### Personalizzare un banner di una pagina iniziale {#home-page-banner}

Un’azienda di noleggio e vendita di immobili vuole personalizzare la propria pagina principale con un banner, in base alle qualifiche del pubblico in Adobe Experience Platform. L’azienda può selezionare i tipi di pubblico che dovranno ottenere un’esperienza personalizzata e inviarli ad Adobe Target come criteri di targeting per l’offerta Target.

## Prerequisiti {#prerequisites}

### Configurare uno stream di dati nell’interfaccia utente di Data Collection {#configure-datastream}

Il primo passaggio nella configurazione della destinazione di personalizzazione consiste nel configurare uno stream di dati per l’SDK per web di Experience Platform. Questa operazione viene eseguita nell’interfaccia utente di Data Collection.

Durante la configurazione dello stream di dati, in **[!UICONTROL Adobe Experience Platform]** assicurati che entrambi **[!UICONTROL Segmentazione Edge]** e **[!UICONTROL Destinazioni di personalizzazione]** sono selezionati.

![Configurazione dello stream di dati con Segmentazione Edge e Destinazioni di personalizzazione evidenziate.](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Per ulteriori informazioni su come impostare un flusso di dati, segui le istruzioni descritte nella sezione [Documentazione di Platform Web SDK](../../datastreams/configure.md#aep).

### Creare un [!DNL Active-On-Edge] criterio di unione {#create-merge-policy}

Dopo aver creato la connessione di destinazione, è necessario creare un [!DNL Active-On-Edge] criterio di unione. Il [!DNL Active-On-Edge] criterio di unione per garantire che i tipi di pubblico vengano valutati costantemente [sul bordo](../../segmentation/ui/edge-segmentation.md) e sono disponibili per i casi di utilizzo di personalizzazione in tempo reale e nella pagina successiva.

>[!IMPORTANT]
>
>Attualmente, le destinazioni Edge supportano solo l’attivazione di tipi di pubblico che utilizzano [Criterio di unione Attivo su Edge](../../segmentation/ui/segment-builder.md#merge-policies) impostato come predefinito. Se mappi tipi di pubblico che utilizzano un criterio di unione diverso su destinazioni edge, tali tipi di pubblico non verranno valutati.

Segui le istruzioni su [creazione di un criterio di unione](../../profile/merge-policies/ui-guide.md#create-a-merge-policy), e assicurati di abilitare **[!UICONTROL Criterio di unione Attivo su Edge]** attivare/disattivare.

### Creare un nuovo pubblico in Platform {#create-audience}

Dopo aver creato [!DNL Active-On-Edge] criterio di unione, devi creare un nuovo pubblico in Platform.

Segui le [audience builder](../../segmentation/ui/segment-builder.md) per creare il nuovo pubblico e assicurati di [assegnarlo](../../segmentation/ui/segment-builder.md#merge-policies) il [!DNL Active-On-Edge] criterio di unione creato nel passaggio precedente.

### Creare una connessione di destinazione {#connect-destination}

Dopo aver configurato lo stream di dati, puoi iniziare a configurare la destinazione di personalizzazione.

Segui le [tutorial sulla creazione della connessione di destinazione](../ui/connect-destination.md) per istruzioni dettagliate su come creare una nuova connessione di destinazione.

A seconda della destinazione che stai configurando, consulta i seguenti articoli per i prerequisiti specifici per la destinazione e le relative informazioni:

* [Connessione Adobe Target](../catalog/personalization/adobe-target-connection.md#parameters)
* [Connessione di personalizzazione personalizzata](../catalog/personalization/custom-personalization.md##parameters)

## Seleziona la destinazione {#select-destination}

Dopo aver completato i prerequisiti, ora puoi selezionare la destinazione di personalizzazione Edge da utilizzare per la personalizzazione della stessa pagina e della pagina successiva.

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, e seleziona la **[!UICONTROL Catalogo]** scheda.

   ![La scheda Catalogo di destinazione è evidenziata nell’interfaccia utente di Experienci Platform.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Seleziona **[!UICONTROL Attiva tipi di pubblico]** sulla scheda corrispondente alla destinazione di personalizzazione in cui desideri attivare i tipi di pubblico, come illustrato nell’immagine seguente.

   ![Attiva il controllo del pubblico evidenziato su una scheda di destinazione nel catalogo.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Seleziona la connessione di destinazione da utilizzare per attivare i tipi di pubblico, quindi fai clic su **[!UICONTROL Successivo]**.

   ![Seleziona il passaggio di destinazione nel flusso di lavoro di attivazione.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Passa alla sezione successiva a [seleziona i tipi di pubblico](#select-audiences).

## Seleziona i tipi di pubblico {#select-audiences}

Utilizza le caselle di controllo a sinistra dei nomi del pubblico per selezionare i tipi di pubblico da attivare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

Per selezionare i tipi di pubblico da attivare nella destinazione, utilizza le caselle di controllo a sinistra dei nomi dei tipi di pubblico, quindi seleziona **[!UICONTROL Successivo]**.

Puoi scegliere tra più tipi di pubblico, a seconda della loro origine:

* **[!UICONTROL Servizio di segmentazione]**: tipi di pubblico generati all’interno di Experienci Platform dal servizio di segmentazione. Consulta la [documentazione sulla segmentazione](../../segmentation/ui/overview.md) per ulteriori dettagli.
* **[!UICONTROL Caricamento personalizzato]**: tipi di pubblico generati al di fuori di Experienci Platform e caricati in Platform come file CSV. Per ulteriori informazioni sui tipi di pubblico esterni, consulta la documentazione su [importazione di un pubblico](../../segmentation/ui/overview.md#import-audience).
* Altri tipi di pubblico, derivanti da altre soluzioni di Adobe, quali [!DNL Audience Manager].

![Seleziona il passaggio del pubblico del flusso di lavoro di attivazione evidenziando diversi tipi di pubblico.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Mappa attributi {#mapping}

>[!IMPORTANT]
>
>Gli attributi del profilo possono contenere dati sensibili. Per proteggere questi dati, è necessario **[!UICONTROL Personalizzazione personalizzata]** La destinazione richiede l&#39;utilizzo di [API server di rete Edge](../../server-api/overview.md) durante la configurazione della destinazione per la personalizzazione basata su attributi. Tutte le chiamate API server devono essere effettuate in un [contesto autenticato](../../server-api/authentication.md).
>
><br>Se utilizzi già Web SDK o Mobile SDK per l’integrazione, puoi recuperare gli attributi tramite l’API server aggiungendo un’integrazione lato server.
>
><br>Se non segui i requisiti di cui sopra, la personalizzazione sarà basata solo sull’iscrizione al pubblico.

Seleziona gli attributi in base ai quali desideri abilitare i casi di utilizzo di personalizzazione per i tuoi utenti. Ciò significa che se il valore di un attributo cambia o se un attributo viene aggiunto a un profilo, tale profilo diventa un membro del pubblico e viene attivato nella destinazione di personalizzazione.

L’aggiunta di attributi è facoltativa e puoi comunque procedere al passaggio successivo e abilitare la personalizzazione della stessa pagina e della pagina successiva senza selezionare gli attributi. Se non aggiungi attributi in questo passaggio, la personalizzazione verrà comunque eseguita in base all’iscrizione al pubblico e alle qualifiche della mappa di identità per i profili.

![Immagine che mostra il passaggio di mappatura con un attributo selezionato.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Seleziona attributi sorgente {#select-source-attributes}

Per aggiungere attributi di origine, selezionare **[!UICONTROL Aggiungi nuovo campo]** controllo sul **[!UICONTROL Campo di origine]** e cerca o passa al campo dell’attributo XDM desiderato, come mostrato di seguito.

![Registrazione su schermo che mostra come selezionare un attributo target nel passaggio di mappatura.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Seleziona attributi di destinazione {#select-target-attributes}

Per aggiungere attributi di destinazione, selezionare **[!UICONTROL Aggiungi nuovo campo]** controllo sul **[!UICONTROL Campo di destinazione]** e digitare il nome dell&#39;attributo personalizzato a cui si desidera mappare l&#39;attributo di origine.

>[!NOTE]
>
>La selezione degli attributi di destinazione si applica solo al [Personalizzazione personalizzata](../catalog/personalization/custom-personalization.md) flusso di lavoro di attivazione, per supportare la mappatura dei campi con nomi descrittivi nella piattaforma di destinazione.

![Registrazione schermata che mostra come selezionare un attributo XDM nel passaggio di mappatura](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Pianificare l’esportazione del pubblico {#scheduling}

Per impostazione predefinita, il [!UICONTROL Pianificazione del pubblico] Questa pagina mostra solo i tipi di pubblico appena selezionati che hai scelto nel flusso di attivazione corrente.

Per visualizzare tutti i tipi di pubblico attivati nella destinazione, utilizza l’opzione di filtro e disattiva il **[!UICONTROL Mostra solo i nuovi tipi di pubblico]** filtro.

![Il filtro Tutti i tipi di pubblico è evidenziato.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

Il giorno **[!UICONTROL Pianificazione del pubblico]** , seleziona ogni pubblico, quindi utilizza la **[!UICONTROL Data di inizio]** e **[!UICONTROL Data di fine]** selettori per configurare l’intervallo di tempo per l’invio di dati alla destinazione.

![Passaggio di pianificazione del pubblico del flusso di lavoro di attivazione con data di inizio e di fine evidenziate.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Seleziona **[!UICONTROL Successivo]** per passare al [!UICONTROL Revisione] pagina.

## Revisione {#review}

Il giorno **[!UICONTROL Revisione]** pagina, è possibile visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni, oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Riepilogo della selezione nel passaggio di revisione.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Valutazione dei criteri di consenso {#consent-policy-evaluation}

Se l’organizzazione ha acquistato **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleziona **[!UICONTROL Visualizza i criteri di consenso applicabili]** per vedere quali criteri di consenso vengono applicati e quanti profili vengono inclusi di conseguenza nell’attivazione. Ulteriori informazioni [valutazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per ulteriori informazioni.

### Controlli dei criteri di utilizzo dei dati {#data-usage-policy-checks}

In **[!UICONTROL Revisione]** step, Experienci Platform controlla anche eventuali violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di una policy. Non puoi completare il flusso di lavoro di attivazione del pubblico finché non hai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, vedere [violazioni dei criteri di utilizzo dei dati](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) nella sezione documentazione sulla governance dei dati.

![Esempio di violazione dei criteri per i dati.](../assets/common/data-policy-violation.png)

### Filtrare i tipi di pubblico {#filter-audiences}

In questo passaggio puoi utilizzare i filtri disponibili nella pagina per visualizzare solo i tipi di pubblico la cui pianificazione o mappatura è stata aggiornata come parte di questo flusso di lavoro. Puoi anche scegliere quali colonne della tabella visualizzare.

![Registrazione dello schermo che mostra i filtri del pubblico disponibili nel passaggio di revisione.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Se si è soddisfatti della selezione e non sono state rilevate violazioni dei criteri, selezionare **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
