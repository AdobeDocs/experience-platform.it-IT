---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segment Match;segment match;home;popular topic;segmentation;Segmentation;Segment Match;segment match
solution: Experience Platform
title: Panoramica sulla corrispondenza dei segmenti
description: Segment Match è un servizio di condivisione dei segmenti in Adobe Experience Platform che consente a due o più utenti di Platform di scambiarsi i dati dei segmenti in modo sicuro, gestito e rispettoso della privacy.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1996'
ht-degree: 2%

---

# Panoramica di [!DNL Segment Match]

Adobe Experience Platform Segment Match è un servizio di condivisione dei segmenti che consente a due o più utenti di Platform di scambiarsi i dati dei segmenti in modo sicuro, gestito e rispettoso della privacy. [!DNL Segment Match] utilizza gli standard di privacy di Platform e gli identificatori personali come e-mail con hash, numeri di telefono con hash e identificatori di dispositivo come IDFA e GAID.

Con [!DNL Segment Match] è possibile:

* Gestisci il processo di sovrapposizione delle identità.
* Visualizzare le stime precedenti alla condivisione.
* Applica le etichette di utilizzo dei dati per controllare se i dati possono essere condivisi con i partner.
* Gestisci la gestione condivisa del ciclo di vita del pubblico dopo la pubblicazione di un feed e continua uno scambio dinamico di dati attraverso funzionalità di aggiunta, eliminazione e annullamento della condivisione.

[!DNL Segment Match] utilizza un processo di sovrapposizione delle identità per garantire che la condivisione dei segmenti avvenga in modo sicuro e incentrato sulla privacy. Un **identità sovrapposta** è un’identità che presenta una corrispondenza sia nel segmento che nel segmento del partner selezionato. Prima di condividere un segmento tra un mittente e un destinatario, il processo di sovrapposizione delle identità verifica la presenza di una sovrapposizione negli spazi dei nomi e nei controlli di consenso tra il mittente e il destinatario. Entrambi i controlli di sovrapposizione devono passare affinché un segmento possa essere condiviso.

Nelle sezioni seguenti vengono fornite ulteriori informazioni su [!DNL Segment Match], inclusi dettagli sulla configurazione e sul relativo flusso di lavoro end-to-end.

## Configurazione

Le sezioni seguenti descrivono come impostare e configurare [!DNL Segment Match]:

### Configurare i dati di identità e gli spazi dei nomi {#namespaces}

Il primo passaggio per iniziare a utilizzare [!DNL Segment Match] deve assicurarsi di acquisire dati in base agli spazi dei nomi di identità supportati.

Gli spazi dei nomi delle identità sono un componente di [Servizio Adobe Experience Platform Identity](../../../identity-service/home.md). Ogni identità del cliente contiene uno spazio dei nomi associato che indica il contesto dell’identità. Ad esempio, uno spazio dei nomi può distinguere un valore di &quot;name<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico.

Un’identità completa include un valore ID e uno spazio dei nomi. Quando si abbinano i dati del record tra frammenti di profilo (ad esempio quando [!DNL Real-Time Customer Profile] unisce i dati del profilo), il valore di identità e lo spazio dei nomi devono corrispondere.

Nel contesto di [!DNL Segment Match], gli spazi dei nomi vengono utilizzati nel processo di sovrapposizione durante la condivisione dei dati.

L’elenco degli spazi dei nomi supportati è il seguente:

| Namespace | Descrizione |
| --------- | ----------- |
| E-mail (SHA256, in minuscolo) | Uno spazio dei nomi per l’indirizzo e-mail con hash predefinito. I valori forniti in questo spazio dei nomi vengono convertiti in minuscolo prima dell’hashing con SHA256. Gli spazi iniziali e finali devono essere tagliati prima che un indirizzo e-mail venga normalizzato. Questa impostazione non può essere modificata retroattivamente. Platform offre due metodi per supportare l’hashing sulla raccolta dei dati, tramite [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) e attraverso [preparazione dati](../../../data-prep/functions.md#hashing). |
| Telefono (SHA256_E.164) | Uno spazio dei nomi che rappresenta i numeri di telefono non elaborati con hash che devono essere eseguiti utilizzando sia il formato SHA256 che il formato E.164. |
| ECID | Uno spazio dei nomi che rappresenta un valore ID Experience Cloud (ECID). A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Consulta la [Panoramica di ECID](../../../identity-service/ecid.md) per ulteriori informazioni. |
| Apple IDFA (ID per inserzionisti) | Spazio dei nomi che rappresenta l’ID di Apple per gli inserzionisti. Vedi il seguente documento su [annunci basati su interessi](https://support.apple.com/en-us/HT202074) per ulteriori informazioni. |
| ID Google Ad | Spazio dei nomi che rappresenta un ID Google Advertising. Vedi il seguente documento su [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) per ulteriori informazioni. |

### Configurare la configurazione del consenso

Devi fornire una configurazione di consenso e impostarne il valore predefinito su `opt-in` o `opt-out` per un controllo del consenso.

La verifica del consenso di consenso e rinuncia determina se puoi operare con il consenso alla condivisione dei dati utente per impostazione predefinita. Se la configurazione di consenso predefinita è impostata su `opt-out`, quindi i dati utente possono essere condivisi, a meno che un utente non neghi esplicitamente la rinuncia. Se il valore predefinito è impostato su `opt-in`, i dati utente non possono essere condivisi, a meno che un utente non acconsenta esplicitamente.

Configurazione del consenso predefinita per [!DNL Segment Match] è impostato su `opt-out`. Per applicare un modello di consenso ai dati, invia una richiesta e-mail al team del tuo account Adobe.

Per ulteriori informazioni su `share` utilizzato per impostare il valore del consenso per la condivisione dei dati, consulta la seguente documentazione su [gruppo di campi privacy e consensi](../../../xdm/field-groups/profile/consents.md). Per informazioni sul gruppo di campi specifico utilizzato per acquisire il consenso del consumatore alla raccolta e all’utilizzo dei dati relativi alla privacy, alla personalizzazione e alle preferenze di marketing, consulta quanto segue [Esempio di consenso per le preferenze di privacy, personalizzazione e marketing su GitHub](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Configurare le etichette di utilizzo dei dati

L’ultimo prerequisito da stabilire è configurare una nuova etichetta di utilizzo dati per impedire la condivisione dei dati. Tramite le etichette di utilizzo dei dati, puoi gestire quali dati possono essere condivisi tramite [!DNL Segment Match].

Le etichette di utilizzo dei dati consentono di categorizzare set di dati e campi in base ai criteri di utilizzo applicabili a tali dati. Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Le best practice incoraggiano i dati di etichettatura non appena vengono acquisiti in Experienci Platform o non appena i dati diventano disponibili per l’utilizzo in Platform.

[!DNL Segment Match] utilizza l’etichetta C11, un’etichetta di contratto specifica per [!DNL Segment Match] che puoi aggiungere manualmente a qualsiasi set di dati o attributo per assicurarti che sia escluso dal [!DNL Segment Match] processo di condivisione dei partner. L’etichetta C11 indica i dati che non devono essere utilizzati in [!DNL Segment Match] processi. Dopo aver determinato quali set di dati e/o campi escludere [!DNL Segment Match] e aggiunta l&#39;etichetta C11 di conseguenza, l&#39;etichetta viene automaticamente applicata dal [!DNL Segment Match] flusso di lavoro. [!DNL Segment Match] abilita automaticamente [!UICONTROL Limita la condivisione dei dati] politica di base. Per istruzioni specifiche su come applicare le etichette di utilizzo dei dati ai set di dati, consulta l’esercitazione su [gestione delle etichette di utilizzo dei dati nell’interfaccia utente](../../../data-governance/labels/user-guide.md).

Per un elenco delle etichette di utilizzo dei dati e delle relative definizioni, vedi [glossario delle etichette di utilizzo dati](../../../data-governance/labels/reference.md). Per informazioni sui criteri di utilizzo dei dati, vedi [panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

### Informazioni [!DNL Segment Match] autorizzazioni

Esistono due autorizzazioni associate a [!DNL Segment Match]:

| Autorizzazione | Descrizione |
| --- | --- |
| Gestire le connessioni di condivisione del pubblico | Questa autorizzazione consente di completare il processo di handshake del partner, che collega due organizzazioni per abilitare [!DNL Segment Match] flussi. |
| Gestire le condivisioni di pubblico | Questa autorizzazione consente di creare, modificare e pubblicare feed (il pacchetto di dati utilizzato per [!DNL Segment Match]) con partner attivi (partner che sono stati collegati dall’utente amministratore con **[!UICONTROL Connessioni condivisione pubblico]** accesso). |

Consulta la [panoramica sul controllo degli accessi](../../../access-control/home.md) per ulteriori informazioni sul controllo degli accessi e sulle autorizzazioni.

## [!DNL Segment Match] flusso di lavoro end-to-end

Dopo aver configurato i dati di identità e gli spazi dei nomi, la configurazione del consenso e l’etichetta di utilizzo dei dati, puoi iniziare a lavorare con [!DNL Segment Match] e le sue caratteristiche.

### Gestisci partner

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Segmenti]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Feed]** dall’intestazione in alto.

![segments-feed.png](./images/segments-feed.png)

Il [!UICONTROL Feed] Questa pagina contiene un elenco dei feed ricevuti dai partner e dei feed condivisi. Per visualizzare un elenco di partner esistenti o stabilire una connessione con un nuovo partner, selezionare **[!UICONTROL Gestisci partner]**.

![manage-partners.png](./images/manage-partners.png)

Una connessione tra due partner è un &quot;handshake bidirezionale&quot; che funge da metodo self-service per consentire agli utenti di connettere le organizzazioni Platform a livello di sandbox. La connessione è necessaria per informare Platform che è stato stipulato un accordo e che Platform può facilitare la condivisione di servizi tra l’utente e i suoi partner.

>[!NOTE]
>
>La &quot;stretta di mano bidirezionale&quot; tra te e il tuo partner è strettamente una connessione. Durante questo processo non vengono scambiati dati.

Puoi visualizzare un elenco delle connessioni con i partner esistenti nell’interfaccia principale della [!UICONTROL Gestisci partner] schermo. Sulla barra a destra è riportato il [!UICONTROL Condividi impostazione] , che offre l&#39;opzione di generare una nuova [!UICONTROL ID connessione] nonché una casella di immissione in cui è possibile immettere i [!UICONTROL ID connessione].

![stabilire-connessione.png](./images/establish-connection.png)

Per creare un nuovo [!UICONTROL ID connessione], seleziona **[!UICONTROL Rigenera]** in [!UICONTROL Condividi impostazione] quindi seleziona l’icona copia accanto all’ID appena generato.

![share-setting.png](./images/share-setting.png)

Per connettere un partner utilizzando il proprio [!UICONTROL ID connessione], inserisci il loro ID univoco nella casella di input in [!UICONTROL Connetti partner] e quindi seleziona **[!UICONTROL Richiesta]**.

![connect-partner.png](./images/connect-partner.png)

### Crea feed {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Casi d’uso di marketing con restrizioni"
>abstract="I casi d’uso di marketing con restrizioni forniscono indicazioni ai partner per garantire che i segmenti condivisi vengano utilizzati correttamente in base alle restrizioni di governance dei dati."
>text="Learn more in documentation"

A **feed** è un raggruppamento di dati (segmenti), le regole per l’esposizione o l’utilizzo di tali dati e le configurazioni che determinano il modo in cui i dati vengono confrontati con i dati dei partner. Un feed può essere gestito in modo indipendente e scambiato con altri utenti di Platform tramite [!DNL Segment Match].

Per creare un nuovo feed, seleziona **[!UICONTROL Crea feed]** dal [!UICONTROL Feed] dashboard.

![create-feed.png](./images/create-feed.png)

La configurazione di base di un feed include un nome, una descrizione e configurazioni relative a casi di utilizzo marketing e impostazioni di identità. Specifica un nome e una descrizione per il feed, quindi applica i casi di utilizzo di marketing da cui desideri escludere i dati. È possibile selezionare più casi d’uso da un elenco che include:

* [!UICONTROL Analytics]
* [!UICONTROL Combina con PII]
* [!UICONTROL Targeting tra siti]
* [!UICONTROL Data Science]
* [!UICONTROL Targeting e-mail]
* [!UICONTROL Esporta a terze parti]
* [!UICONTROL Pubblicità in loco]
* [!UICONTROL Personalizzazione nel sito]
* [!UICONTROL Corrispondenza segmento]
* [!UICONTROL Personalizzazione di una singola identità]

Infine, seleziona gli spazi dei nomi di identità appropriati per il feed. Per informazioni sugli spazi dei nomi specifici supportati da [!DNL Segment Match], vedere [tabella dei dati di identità e namespace](#namespaces). Al termine, seleziona **[!UICONTROL Successivo]**.

![audience-sharing.png](./images/audience-sharing.png)

Dopo aver stabilito le impostazioni del feed, seleziona i segmenti da condividere dall’elenco dei segmenti di prime parti. Puoi selezionare più segmenti dall’elenco e utilizzare la barra a destra per gestire l’elenco dei segmenti selezionati. Al termine, seleziona **[!UICONTROL Successivo]**.

![select-segments.png](./images/select-segments.png)

Il [!UICONTROL Condividi] viene visualizzata una pagina che offre un’interfaccia per selezionare i partner con cui desideri condividere il feed. Durante questo passaggio, puoi anche visualizzare il rapporto delle stime di sovrapposizione pre-condivisione e vedere il numero di identità sovrapposte per spazio dei nomi tra te e il tuo partner, il numero di identità sovrapposte che hanno il consenso per la condivisione dei dati.

Seleziona **[!UICONTROL Analizza per segmento]** per visualizzare il rapporto stime.

![analyse.png](./images/analyze.png)

Il rapporto delle stime di sovrapposizione consente di gestire i controlli di sovrapposizione e consenso per partner e per segmento prima di condividere il feed.

| Metriche | Descrizione |
| ------- | ----------- |
| Identità stimate con il consenso | Il numero totale di identità sovrapposte che soddisfano i requisiti di consenso configurati per la tua organizzazione. |
| Identità sovrapposte stimate | Il numero di identità idonee per il segmento selezionato e con corrispondenza con il partner selezionato. Queste identità vengono visualizzate per spazio dei nomi e non rappresentano singole identità di profilo. Le stime di sovrapposizione si basano sugli schizzi di profilo. |

Al termine, seleziona **[!UICONTROL Chiudi]**.

![overlap-report.png](./images/overlap-report.png)

Dopo aver selezionato i partner e visualizzato il rapporto delle stime di sovrapposizione, seleziona **[!UICONTROL Successivo]** per procedere.

![share.png](./images/share.png)

Il [!UICONTROL Revisione] viene visualizzato un passaggio che consente di rivedere il nuovo feed prima che venga condiviso e pubblicato. Questo passaggio include dettagli sull’impostazione di identità applicata, nonché informazioni sui casi di utilizzo di marketing, sui segmenti e sui partner selezionati.

Seleziona **[!UICONTROL Fine]** per procedere.

![review.png](./images/review.png)

### Aggiorna feed

Per aggiungere o rimuovere segmenti, seleziona **[!UICONTROL Crea feed]** dal [!UICONTROL Feed] pagina e quindi seleziona **[!UICONTROL Feed esistente]**. Nell&#39;elenco dei feed esistenti visualizzati, selezionare il feed da aggiornare, quindi selezionare **[!UICONTROL Successivo]**.

![elenco feed](./images/feed-list.png)

Viene visualizzato l’elenco dei segmenti. Da qui, puoi aggiungere nuovi segmenti al feed e utilizzare la barra a destra per rimuovere eventuali segmenti non più necessari. Una volta completata la gestione dei segmenti nel feed, seleziona **[!UICONTROL Successivo]** quindi segui i passaggi descritti in precedenza per completare il feed aggiornato.

![update](./images/update.png)

>[!NOTE]
>
>Quando aggiungi o rimuovi un segmento da un feed condiviso, il partner ricevente deve confermare la modifica riabilitando [!DNL Profile] nell’elenco dei feed ricevuti.

### Accetta un feed in ingresso

Per visualizzare un feed in ingresso, seleziona **[!UICONTROL Ricevuto]** dall&#39;intestazione del [!UICONTROL Feed] e quindi selezionare dall&#39;elenco il feed da visualizzare. Per accettare il feed, seleziona **[!UICONTROL Abilita per profilo]** e attendi alcuni istanti prima che lo stato venga aggiornato da [!UICONTROL In sospeso] a [!UICONTROL Abilitato].

![received.png](./images/received.png)

Una volta accettato un feed condiviso, puoi iniziare a utilizzarlo per creare nuovi segmenti.

## Passaggi successivi

Leggendo questo documento, avrai acquisito una maggiore comprensione di [!DNL Segment Match], le sue funzionalità e il relativo flusso di lavoro end-to-end. Per ulteriori informazioni su altri servizi di Platform, consulta i seguenti documenti:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [Panoramica di [!DNL Real-Time Customer Profile]](../../../profile/home.md)
