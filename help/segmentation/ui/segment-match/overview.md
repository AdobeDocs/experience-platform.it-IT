---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Corrispondenza segmento;corrispondenza segmento
solution: Experience Platform
title: Panoramica sulla corrispondenza dei segmenti
topic-legacy: overview
description: Segment Match is a segment-sharing service in Adobe Experience Platform that allows for two or more Platform users to exchange segment data in a secure, governed, and privacy-friendly manner.
exl-id: 4e6ec2e0-035a-46f4-b171-afb777c14850
source-git-commit: 1c2b9862facfe9fbce59246c882e6373f3e2c3ef
workflow-type: tm+mt
source-wordcount: '1994'
ht-degree: 0%

---

# [!DNL Segment Match] panoramica

Adobe Experience Platform Segment Match is a segment-sharing service that allows for two or more Platform users to exchange segment data in a secure, governed, and privacy-friendly manner. [!DNL Segment Match] uses Platform privacy standards and personal identifiers such as hashed emails, hashed phone numbers, and device identifiers like IDFAs and GAIDs.

With [!DNL Segment Match] you can:

* Gestisci il processo di sovrapposizione delle identità.
* Visualizzare le stime preliminari alla condivisione.
* Applica le etichette di utilizzo dei dati per controllare se i dati possono essere condivisi con i partner.
* Gestisci la gestione del ciclo di vita del pubblico condiviso dopo la pubblicazione di un feed e continua uno scambio dinamico di dati attraverso le capacità di aggiungere, eliminare e annullare la condivisione.

[!DNL Segment Match] utilizza un processo di sovrapposizione delle identità per garantire che la condivisione dei segmenti venga eseguita in modo sicuro e incentrato sulla privacy. Un **identità sovrapposta** è un’identità che ha una corrispondenza sia nel segmento che nel segmento del partner selezionato. Prima di condividere un segmento tra un mittente e un destinatario, il processo di sovrapposizione delle identità verifica la presenza di una sovrapposizione nei namespace e nei controlli del consenso tra il mittente e il/i destinatario/i. Affinché un segmento possa essere condiviso, è necessario che entrambi i controlli di sovrapposizione passino.

Le sezioni seguenti forniscono ulteriori informazioni su [!DNL Segment Match], compresi i dettagli sulla configurazione e il relativo flusso di lavoro end-to-end.

## Configurazione

Le sezioni seguenti descrivono come impostare e configurare [!DNL Segment Match]:

### Configurare i dati di identità e i namespace {#namespaces}

The first step to getting started with [!DNL Segment Match] is to make sure you&#39;re ingesting data against the supported identity namespaces.

Gli spazi dei nomi di identità sono un componente di [Servizio Adobe Experience Platform Identity](../../../identity-service/home.md). Ogni identità cliente contiene uno spazio dei nomi associato che indica il contesto dell&#39;identità. Ad esempio, uno spazio dei nomi può distinguere un valore di &quot;name&quot;<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico.

Un&#39;identità completa include un valore ID e uno spazio dei nomi. When matching record data across profile fragments (such as when [!DNL Real-time Customer Profile] merges Profile data), both the identity value and the namespace must match.

Nel contesto [!DNL Segment Match], gli spazi dei nomi vengono utilizzati nel processo di sovrapposizione durante la condivisione dei dati.

The list of supported namespaces are as follows:

| Namespace | Descrizione |
| --------- | ----------- |
| E-mail (SHA256, minuscolo) | A namespace for pre-hashed email address. Values provided in this namespace are converted to lowercase before hashing with SHA256. È necessario tagliare gli spazi iniziali e finali prima di normalizzare l’indirizzo e-mail. This setting cannot be changed retroactively. Vedi il seguente documento su [Supporto di hashing SHA-256](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=en#hashing-support) per ulteriori informazioni. |
| Phone (SHA256_E.164) | A namespace that represents raw phone numbers that need to be hashed using both SHA256 and E.164 format. |
| ECID | Spazio dei nomi che rappresenta un valore Experience Cloud ID (ECID). Questo namespace può essere indicato anche dai seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. See the [ECID overview](../../../identity-service/ecid.md) for more information. |
| Apple IDFA (ID per gli inserzionisti) | A namespace that represents Apple ID for Advertisers. Vedi il seguente documento su [annunci basati su interessi](https://support.apple.com/en-us/HT202074) per ulteriori informazioni. |
| Google Ad ID | A namespace that represents a Google Advertising ID. See the following document on [Google Advertising ID](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) for more information. |

### Configurare la configurazione del consenso

È necessario fornire una configurazione di consenso e impostare il relativo valore predefinito su `opt-in` o `opt-out` per un controllo del consenso.

Il controllo del consenso opt-in e opt-out determina se è possibile operare con il consenso per condividere i dati utente per impostazione predefinita. Se l’impostazione predefinita per la configurazione del consenso è impostata su `opt-out`, i dati utente possono essere condivisi, a meno che un utente non rinunci esplicitamente. Se il valore predefinito è impostato su `opt-in`, i dati utente non possono essere condivisi, a meno che un utente non acconsenta esplicitamente.

Configurazione del consenso predefinito per [!DNL Segment Match] è impostato su `opt-out`. Per applicare un modello di consenso per i tuoi dati, invia una richiesta e-mail al tuo Adobe Account Manager.

Per ulteriori informazioni sulla `share` attributo utilizzato per impostare il valore del consenso per la condivisione dei dati, consulta la seguente documentazione su [gruppo di campi privacy e consenso](../../../xdm/field-groups/profile/consents.md). Per informazioni sul gruppo di campi specifico utilizzato per acquisire il consenso dei consumatori per la raccolta e l’utilizzo dei dati relativi alla privacy, alla personalizzazione e alle preferenze di marketing, consulta quanto segue [Esempio di GitHub per privacy, personalizzazione e preferenze di marketing](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/consent/consent-preferences.schema.md).

### Configurare le etichette di utilizzo dei dati

The last prerequisite you must establish is to configure a new data usage label to prevent data sharing. Tramite le etichette di utilizzo dei dati, puoi gestire i dati che possono essere condivisi attraverso [!DNL Segment Match].

Data usage labels allow you to categorize datasets and fields according to usage policies that apply to that data. Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti in Experience Platform o non appena i dati diventano disponibili per l’utilizzo in Platform.

[!DNL Segment Match] utilizza l’etichetta C11, un’etichetta di contratto specifica per [!DNL Segment Match] che puoi aggiungere manualmente a qualsiasi set di dati o attributo per assicurarti che siano esclusi dal [!DNL Segment Match] processo di condivisione dei partner. L’etichetta C11 indica i dati che non devono essere utilizzati in [!DNL Segment Match] processi. Dopo aver determinato da quali set di dati e/o campi si desidera escludere [!DNL Segment Match] e ha aggiunto l&#39;etichetta C11 di conseguenza, l&#39;etichetta viene automaticamente applicata dal [!DNL Segment Match] workflow. [!DNL Segment Match] automatically enables the [!UICONTROL Restrict data sharing] core policy. For specific instructions on how to apply data usage labels to datasets, see the tutorial on [managing data usage labels in the UI](../../../data-governance/labels/user-guide.md).

Per un elenco delle etichette di utilizzo dei dati e delle relative definizioni, consulta [glossario delle etichette di utilizzo dei dati](../../../data-governance/labels/reference.md). Per informazioni sui criteri di utilizzo dei dati, consulta [panoramica dei criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

### Comprensione [!DNL Segment Match] permissions

Sono associate due autorizzazioni [!DNL Segment Match]:

| Autorizzazione | Descrizione |
| --- | --- |
| Gestire le connessioni di Audience Share | Questa autorizzazione consente di completare il processo di handshake del partner, che collega due organizzazioni IMS per abilitare [!DNL Segment Match] flussi. |
| Manage Audience Shares | Questa autorizzazione consente di creare, modificare e pubblicare feed (il pacchetto di dati utilizzato per [!DNL Segment Match]) con partner attivi (partner che sono stati collegati dall&#39;utente amministratore con **[!UICONTROL Connessioni di Audience Share]** accesso). |

Consulta la sezione [panoramica sul controllo degli accessi](../../../access-control/home.md) per ulteriori informazioni sul controllo degli accessi e sulle autorizzazioni.

## [!DNL Segment Match] flusso di lavoro end-to-end

Dopo aver impostato i dati e i namespace di identità, la configurazione del consenso e l’etichetta di utilizzo dei dati, puoi iniziare a lavorare con [!DNL Segment Match] e le sue caratteristiche.

### Gestisci partner

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Segmenti]** dalla navigazione a sinistra, quindi seleziona **[!UICONTROL Feed]** dall’intestazione superiore.

![segment-feed.png](./images/segments-feed.png)

La [!UICONTROL Feed] contiene un elenco dei feed ricevuti dai partner e dei feed condivisi. Per visualizzare un elenco dei partner esistenti o stabilire una connessione con un nuovo partner, selezionare **[!UICONTROL Gestire i partner]**.

![manage-partners.png](./images/manage-partners.png)

Una connessione tra due partner è un &quot;handshake a due vie&quot; che funge da metodo self-service per gli utenti al fine di collegare le loro organizzazioni Platform a livello di sandbox. La connessione è necessaria per informare Platform che è stato stipulato un accordo e che Platform può facilitare i servizi di condivisione tra l’utente e i partner.

>[!NOTE]
>
>La &quot;stretta di mano bidirezionale&quot; tra te e il tuo partner è strettamente una connessione. Nessun dato viene scambiato durante questo processo.

Puoi visualizzare un elenco delle connessioni con i partner esistenti nell’interfaccia principale di [!UICONTROL Gestire i partner] schermo. Sulla barra a destra è visualizzata la [!UICONTROL Impostazione condivisione] , che offre l’opzione per generare un nuovo [!UICONTROL connect ID] nonché una casella di immissione in cui è possibile inserire un partner [!UICONTROL connect ID].

![set-connection.png](./images/establish-connection.png)

To create a new [!UICONTROL connect ID], select **[!UICONTROL Regenerate]** under [!UICONTROL Share setting] and then select the copy icon beside the newly generated ID.

![share-setting.png](./images/share-setting.png)

Per collegare un partner utilizzando i relativi [!UICONTROL connect ID], inserisci il loro valore ID univoco nella casella di immissione in [!UICONTROL Connetti partner] quindi seleziona **[!UICONTROL Richiesta]**.

![connect-partner.png](./images/connect-partner.png)

### Creare un feed {#create-feed}

>[!CONTEXTUALHELP]
>id="platform_segment_match_marketing"
>title="Casi d’uso limitati del marketing"
>abstract="Restricted marketing use cases help provide guidance to your partners to ensure shared segments are properly used per your data governance restrictions."
>text="Learn more in documentation"

A **feed** è un raggruppamento di dati (segmenti), le regole per la modalità di esposizione o utilizzo di tali dati e le configurazioni che determinano la corrispondenza dei dati con i dati dei partner. Un feed può essere gestito in modo indipendente e scambiato con altri utenti di Platform tramite [!DNL Segment Match].

Per creare un nuovo feed, seleziona **[!UICONTROL Creare un feed]** dal [!UICONTROL Feed] dashboard.

![create-feed.png](./images/create-feed.png)

L’impostazione di base di un feed include un nome, una descrizione e configurazioni relative ai casi di utilizzo del marketing e alle impostazioni di identità. Fornisci un nome e una descrizione per il feed, quindi applica i casi d’uso di marketing da cui vuoi escludere i dati. You can select more than one use case from a list that includes:

* [!UICONTROL Analytics]
* [!UICONTROL Combinare con PII]
* [!UICONTROL Targeting tra siti]
* [!UICONTROL Data Science]
* [!UICONTROL Targeting e-mail]
* [!UICONTROL Esportazione verso terzi]
* [!UICONTROL Onsite advertising]
* [!UICONTROL Onsite personalization]
* [!UICONTROL Corrispondenza segmento]
* [!UICONTROL Personalizzazione a singola identità]

Infine, seleziona i namespace di identità appropriati per il feed. Per informazioni sugli spazi dei nomi specifici supportati da [!DNL Segment Match], vedi [tabella dei dati di identità e dei namespace](#namespaces). When you are finished, select **[!UICONTROL Next]**.

![audience-sharing.png](./images/audience-sharing.png)

Una volta stabilite le impostazioni del feed, seleziona i segmenti che desideri condividere dall’elenco dei segmenti di prime parti. Puoi selezionare più segmenti dall’elenco e usare la barra a destra per gestire l’elenco dei segmenti selezionati. Once you are finished, select **[!UICONTROL Next]**.

![select-segment.png](./images/select-segments.png)

The [!UICONTROL Share] page appears, providing you with an interface to select the partners you want to share your feed with. Durante questo passaggio, puoi anche visualizzare il rapporto delle stime della sovrapposizione pre-condivisione e vedere il numero di identità sovrapposte in base allo spazio dei nomi tra te e il tuo partner, il numero di identità sovrapposte che hanno il consenso per la condivisione dei dati.

Select **[!UICONTROL Analyze by segment]** to see the estimates report.

![analyze.png](./images/analyze.png)

Il rapporto delle stime di sovrapposizione consente di gestire le verifiche di sovrapposizione e consenso per partner e per segmento prima di condividere il feed.

| Metriche | Descrizione |
| ------- | ----------- |
| Estimated identities with consent | Numero totale di identità sovrapposte che soddisfano i requisiti di consenso configurati per la tua organizzazione. |
| Identità stimate sovrapposte | Il numero di identità idonee per il segmento selezionato e che corrispondono anche al partner selezionato. Queste identità vengono visualizzate per namespace e non rappresentano singole identità di profilo. Le stime di sovrapposizione si basano sugli schizzi di profilo. |

Al termine, seleziona **[!UICONTROL Chiudi]**.

![sovrapposizione report.png](./images/overlap-report.png)

Dopo aver selezionato i partner e visualizzato il rapporto delle stime di sovrapposizione, seleziona **[!UICONTROL Successivo]** per procedere.

![share.png](./images/share.png)

La [!UICONTROL Revisione] viene visualizzato un passaggio che consente di rivedere il nuovo feed prima che venga condiviso e pubblicato. Questo passaggio include dettagli sull’impostazione di identità applicata, nonché informazioni sui casi di utilizzo di marketing, sui segmenti e sui partner selezionati.

Select **[!UICONTROL Finish]** to proceed.

![review.png](./images/review.png)

### Aggiorna feed

To add or remove segments, select **[!UICONTROL Create feed]** from the [!UICONTROL Feeds] page and then select **[!UICONTROL Existing feed]**. Nell’elenco dei feed esistenti visualizzati, selezionare il feed da aggiornare, quindi selezionare **[!UICONTROL Successivo]**.

![elenco di feed](./images/feed-list.png)

Viene visualizzato l’elenco dei segmenti. Da qui puoi aggiungere nuovi segmenti al feed e usare la barra a destra per rimuovere tutti i segmenti di cui non hai più bisogno. Una volta completata la gestione dei segmenti nel feed, seleziona **[!UICONTROL Successivo]** quindi segui i passaggi descritti sopra per completare il feed aggiornato.

![update](./images/update.png)

>[!NOTE]
>
>Quando aggiungi o rimuovi un segmento da un feed condiviso, il partner ricevente deve confermare la modifica riabilitando il [!DNL Profile] inserisci l’elenco dei feed ricevuti.

### Accettare un feed in entrata

Per visualizzare un feed in entrata, seleziona **[!UICONTROL Ricevuto]** dall&#39;intestazione del [!UICONTROL Feed] , quindi selezionate il feed da visualizzare dall’elenco. Per accettare il feed, seleziona **[!UICONTROL Abilita per profilo]** e consentire l&#39;aggiornamento dello stato da [!UICONTROL In sospeso] a [!UICONTROL Abilitato].

![Received.png](./images/received.png)

Una volta accettato un feed condiviso, puoi iniziare a utilizzare i dati condivisi per creare nuovi segmenti.

## Passaggi successivi

Leggendo questo documento, hai acquisito una comprensione [!DNL Segment Match], le sue funzionalità e il suo flusso di lavoro end-to-end. Per ulteriori informazioni su altri servizi Platform, consulta i seguenti documenti:

* [[!DNL Segmentation Service]](../../home.md)
* [[!DNL Identity Service]](../../../identity-service/home.md)
* [[!DNL Real-time Customer Profile] panoramica](../../../profile/home.md)
