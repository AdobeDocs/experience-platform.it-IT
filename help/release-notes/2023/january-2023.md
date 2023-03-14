---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2023
description: Note sulla versione di gennaio 2023 per Adobe Experience Platform.
source-git-commit: 6388c72aa0be8f5f91efaaa6a0edd22f3eb99de8
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 6%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 gennaio 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [Assurance](#assurance)
- [Raccolta dati](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Servizi di intelligenza artificiale/apprendimento automatico {#ai-ml}

I servizi di intelligenza artificiale e apprendimento automatico consentono agli analisti e ai professionisti del marketing di sfruttare la potenza dell’intelligenza artificiale e dell’apprendimento automatico nei casi di utilizzo dell’esperienza del cliente. Questo consente agli analisti di marketing di impostare previsioni, senza la necessità di competenze scientifiche sui dati, specifiche per le esigenze di un’azienda utilizzando configurazioni a livello aziendale.

### IA per l’attribuzione

Attribution AI viene utilizzato per attribuire crediti ai punti di contatto che conducono a eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Ambito dell’HIPAA | I clienti Healthcare Shield ora possono ricevere, utilizzare, mantenere o trasmettere informazioni protette sulla salute in Attribution AI e in alcune altre applicazioni basate sull’Experience Platform. Healthcare Shield è per i clienti del settore sanitario che sono soggetti interessati o partner commerciali ai sensi dell’HIPAA. Per ulteriori informazioni, consulta la documentazione su [HIPAA e prodotti e servizi per l’Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Modifica colonne aggiuntive del set di dati di punteggio | È ora possibile aggiungere o rimuovere colonne aggiuntive di set di dati di punteggio (colonne di reporting) quando si modificano modelli esistenti. Questo estende la flessibilità dei punteggi di attribuzione per fornirti informazioni approfondite su dimensioni aggiuntive dopo la creazione di un modello. Consulta la [Guida all’interfaccia utente di Attribution](../../intelligent-services/attribution-ai/user-guide.md) per ulteriori informazioni. |

{style="table-layout:auto"}

Consulta la sezione [Servizi di IA/ML](../../intelligent-services/attribution-ai/overview.md) panoramica per ulteriori informazioni.

### IA per l’analisi dei clienti

IA per l’analisi dei clienti per Real-time Customer Data Platform viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Ambito dell’HIPAA | I clienti Healthcare Shield ora possono ricevere, utilizzare, mantenere o trasmettere informazioni protette sulla salute in IA per l’analisi dei clienti per Real-time Customer Data Platform e alcune altre applicazioni basate su Experienci Platform. Healthcare Shield è per i clienti del settore sanitario che sono soggetti interessati o partner commerciali ai sensi dell’HIPAA. Per ulteriori informazioni, consulta la documentazione su [HIPAA e prodotti e servizi per l’Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Consulta la sezione [Servizi di IA/ML](../../intelligent-services/customer-ai/overview.md) panoramica per ulteriori informazioni.

## Assurance {#assurance}

Adobe Assurance consente di verificare, verificare, simulare e convalidare la modalità di raccolta dei dati o di gestione delle esperienze nell’app mobile.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Editor di convalida | Sono stati aggiunti nuovi miglioramenti all’editor di convalida. Questi miglioramenti includono colonne di convalida, nuovi strumenti di creazione del codice e viste migliorate. |

{style="table-layout:auto"}

Per ulteriori informazioni su Assurance, leggere [Documentazione di Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuova schermata iniziale | La pagina principale dell’interfaccia utente di Data Collection è stata aggiornata per includere informazioni utili sull’onboarding e collegamenti per ottimizzare la produttività. Ciò include:<ol><li>Documentazione e flussi di lavoro consigliati per iniziare</li><li>Proprietà, regole ed elementi dati recenti</li><li>Estensioni popolari</li><li>Nuovi aggiornamenti delle estensioni con una funzione di installazione rapida</li></ol> |
| Invia dati a [!DNL Google Ads] utilizzo dell’inoltro degli eventi | Ora puoi utilizzare la [[!DNL Google Ads Enhanced Conversions] Estensione API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) per l’inoltro di eventi, in combinazione con [Segreti Google Oauth 2](../../tags/ui/event-forwarding/secrets.md#google-oauth2), per inviare in modo sicuro i dati lato server a [!DNL Google Ads] in tempo reale. |

{style="table-layout:auto"}

## Destinazioni (aggiornato il 2 febbraio) {#destinations}

[!DNL Destinations] sono integrazioni preconfigurate con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione dei tipi di pubblico di Adobe Experience Cloud (Beta)](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Utilizza il [!UICONTROL (Beta) Tipi di pubblico di Adobe Experience Cloud] connessione per condividere segmenti da Experience Platform a varie soluzioni Experience Platform, come Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo. |
| [Connessione profilo Pega](../../destinations/catalog/personalization/pega-profile.md) | Utilizza il [!DNL Pega Profile Connector] in Adobe Experience Platform per creare una connessione in uscita al tuo [!DNL Amazon] Archiviazione S3 per esportare periodicamente i dati del profilo in file CSV da Adobe Experience Platform nei propri bucket S3. In entrata [!DNL Pega Customer Decision Hub], è possibile pianificare processi di dati per importare questi dati profilo dall’archiviazione S3 per aggiornare [!DNL Pega Customer Decision Hub] profilo. |
| [(Beta) Il punto di contatto CRM dell&#39;UE](../../destinations/catalog/advertising/tradedesk-emails.md) | Con il rilascio di EUID (European Unified ID), ora ne vengono visualizzati due [!DNL The Trade Desk - CRM] destinazioni in [catalogo delle destinazioni](/help/destinations/catalog/overview.md). <ul><li> Se si trovano dati nell&#39;UE, utilizzare il **[!DNL The Trade Desk - CRM (EU)]** destinazione.</li><li> Se i dati vengono originati nelle aree APAC o NAMER, utilizzare **[!DNL The Trade Desk - CRM (NAMER & APAC)]** destinazione. </li></ul> |

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Miglioramento dei criteri di consenso per contenuti multimediali a pagamento per integrazioni con destinazioni di streaming | Un [miglioramento dell’applicazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) il [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations) per casi d’uso di attivazione di contenuti multimediali a pagamento. Quando i profili non sono più qualificati per un criterio di consenso, Experience Platform ora comunica in modo proattivo la propria uscita dal criterio alle destinazioni di streaming. <br> <b>Nota</b>: questa funzionalità è disponibile solo per i clienti di **[!UICONTROL Privacy e sicurezza]** e quelli di **[!UICONTROL Healthcare Shield]**. |
| Nuove opzioni delimitatore per i connettori di destinazione dell’archiviazione cloud beta | Tre nuove opzioni delimitatore (due punti `:`, Pipe, Punto E Virgola `;`) sono ora disponibili per le nuove destinazioni dell’archiviazione cloud beta: [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) BLOB di Azure](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Archiviazione Azure Data Lake Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Data Landing Zone (Beta)](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP (beta)](/help/destinations/catalog/cloud-storage/sftp.md). <br> Leggi le informazioni sui [opzioni di formattazione file](/help/destinations/ui/batch-destinations-file-formatting-options.md) per destinazioni basate su file. |
| Nuovo parametro opzionale disponibile in [campi dati cliente](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) configurazioni in [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: utilizza questo parametro quando devi creare un campo di dati cliente il cui valore deve essere univoco in tutti i flussi di dati di destinazione impostati dall’organizzazione di un utente. <br> Ad esempio, il **[!UICONTROL Alias di integrazione]** campo in [[!UICONTROL Personalizzazione personalizzata]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) la destinazione deve essere univoca, il che significa che due flussi di dati separati verso questa destinazione non possono avere lo stesso valore per questo campo. |

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Correzione o miglioramento</b></td>
        <td><b>Descrizione</b></td>
    </tr>
    <tr>
        <td>Aggiornamento del comportamento di esportazione nelle destinazioni basate su file (PLAT-123316)</td>
        <td>È stato risolto un problema nel comportamento di <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">attributi obbligatori</a> durante l’esportazione di file di dati in destinazioni batch. <br> In precedenza, ogni record nei file di output veniva verificato per contenere entrambi: <ol><li>Un valore non nullo del <code>mandatoryField</code> colonna e</li><li>Valore non nullo in almeno uno degli altri campi non obbligatori.</li></ol> La seconda condizione è stata rimossa. Di conseguenza, è possibile che nei file di dati esportati vengano visualizzate più righe di output, come illustrato nell’esempio seguente:<br> <b> Comportamento di esempio prima della versione di gennaio 2023 </b> <br> Campo obbligatorio: <code>emailAddress</code> <br> <b>Dati di input da attivare</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Output di attivazione</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Comportamento di esempio dopo la versione di gennaio 2023 </b> <br> <b>Output di attivazione</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Convalida dell’interfaccia utente e dell’API per le mappature richieste e le mappature duplicate (PLAT-123316)</td>
        <td>La convalida ora viene applicata come segue nell’interfaccia utente e nell’API quando <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">campi di mappatura</a> nel flusso di lavoro attiva destinazioni:<ul><li><b>Mappature richieste</b>: se la destinazione è stata impostata dallo sviluppatore di destinazione con le mappature richieste (ad esempio, <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> target), quindi le mappature richieste devono essere aggiunte dall’utente quando attiva i dati nella destinazione. </li><li><b>Mappature duplicate</b>: nel passaggio di mappatura del flusso di lavoro di attivazione, puoi aggiungere valori duplicati nei campi sorgente ma non nei campi di destinazione. Consulta la tabella seguente per un esempio di combinazioni di mappatura consentite e non consentite. <br><table><thead><tr><th>Consentito/non consentito</th><th>Campo di origine</th><th>Campo di destinazione</th></tr></thead><tbody><tr><td>Consentito</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>alias e-mail2</li></ul></td></tr><tr><td>Non consentito</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti e utilizzare gli attributi dei clienti a scopo di personalizzazione.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti al nome visualizzato della struttura dello schema | In precedenza, i nomi dei campi venivano visualizzati nell’interfaccia utente, ma ora i nomi visualizzati per i campi schema nell’area di lavoro dello schema sono più facili da leggere. |

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversione]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Classe per il tracciamento dei dati di conversione, ad esempio le conversioni di valuta. |
| Gruppo di campi | [[!UICONTROL Dettagli tasso di conversione valuta]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Un gruppo di campi per [!UICONTROL Conversione] classe, acquisendo ulteriori dettagli relativi alla conversione della valuta. |
| Gruppo di campi | [[!UICONTROL Mappa dei risultati della valutazione dei criteri di consenso con i metadati]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Acquisisce i dettagli dei risultati della valutazione di più criteri di consenso, incluse le informazioni sui metadati relativi alle entrate e alle uscite dei criteri di consenso. |

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della pubblicità]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Il `ID` il campo è stato rinominato in `name`, e il precedente `name` il campo è ora `friendlyName`. |
| Tipo di dati | [[!UICONTROL Dettagli della proposta di decisione]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | È stato aggiunto un `selectionStrategy` campo che acquisisce i dettagli di una strategia di selezione. |
| Gruppo di campi | [[!UICONTROL Evento esperienza - Interazioni proposte]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Il gruppo di campi è ora compatibile con [!UICONTROL Evento passaggio percorso] classe. |
| Tipo di dati | [[!UICONTROL Informazioni dettagli errore]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Il `ID` il campo è stato rinominato in `name`. |
| Tipo di dati | [[!UICONTROL Informazioni multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | È stata ripristinata una modifica del pattern alla proprietà del segmento video. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati Qoe]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | È stato rimosso il `droppedFrameCount` campo. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Rinominato il `isAuthorized` campo a `authorized`, e ha aggiornato i `type` a una stringa quando in precedenza era un valore booleano. |
| Tipo di dati | [[!UICONTROL Spedizione]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Sono stati aggiunti diversi nuovi campi: `shipDate`, `trackingNumber`, e `trackingURL`. |
| Gruppo di campi | [[!UICONTROL Campi entità AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Sono stati aggiunti diversi nuovi campi: `journeyNodeID`, `journeyNodeName`, e `journeyModeType`. |
| Gruppo di campi | [[!UICONTROL Evento esperienza del consumatore]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Il gruppo di campi è ora compatibile anche con [!UICONTROL Metriche di riepilogo] classe. |
| Gruppo di campi | [[!UICONTROL Attivatori prodotto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Il `productTriggers` il campo è ora nidificato in un `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Trigger relativi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Il `relativeTriggers` il campo è ora nidificato in un `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Gravi Trigger]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Il `severeTriggers` il campo è ora nidificato in un `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Attivatori meteo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Il `weatherTriggers` il campo è ora nidificato in un `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Account aziendali correlati a XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Il gruppo di campi è ora stabile. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta [Panoramica del sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di offrire ai tuoi clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Real-Time Customer Profile puoi visualizzare una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, del sistema CRM e di terze parti. Il profilo ti consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

**Prossima rimozione** {#deprecation}

Per rimuovere la ridondanza nel ciclo di vita dell’iscrizione al segmento, il `Existing` lo stato diventerà obsoleto dal [mappa di iscrizione al segmento](../../xdm/field-groups/profile/segmentation.md) alla fine di marzo 2023. Un annuncio di follow-up includerà la data esatta di deprecazione.

Dopo la rimozione, i profili qualificati in un segmento verranno rappresentati come `Realized` e i profili non qualificati continueranno a essere rappresentati come `Exited`. Questo porterà la parità con le destinazioni basate su file con `Active` e `Expired` stati dei segmenti.

Questa modifica potrebbe interessarti se utilizzi [destinazioni enterprise](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hub, API HTTP) e dispongono di processi downstream automatizzati basati su `Existing` stato. Se questo è il caso, controlla le integrazioni a valle. Se ti interessa identificare profili nuovi e qualificati oltre un certo periodo di tempo, puoi utilizzare una combinazione di `Realized` stato e `lastQualificationTime` nella mappa di iscrizione al segmento. Per ulteriori informazioni, contatta il rappresentante del tuo Adobe.

Per ulteriori informazioni su Real-Time Customer Profile, inclusi tutorial e best practice per l’utilizzo dei dati del profilo, leggi [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo commerciabile di persone all’interno della tua base clienti. I segmenti possono essere basati su dati record (ad esempio informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Importazione di valori in blocco nel Generatore di segmenti | Segment Builder ora supporta l’importazione di più valori, caricando un file CSV o TSV o inserendo manualmente valori separati da virgola. Ulteriori informazioni sono disponibili nella sezione [Guida al Generatore di segmenti](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Scadenza iscrizione a pubblico esterno | Per impostazione predefinita, le appartenenze a un pubblico esterno vengono mantenute per 30 giorni. Per conservarli più a lungo, utilizzare `validUntil` durante l’acquisizione dei dati sul pubblico. |
| Scadenza dell’iscrizione a un segmento generato dalla piattaforma | Qualsiasi appartenenza a un segmento presente in `Exited` per più di 30 giorni, in base al `lastQualificationTime` sarà soggetto a eliminazione. |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consultare il [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, software di terze parti e sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| Consenti l&#39;accesso degli utenti alle sottocartelle delle origini di archiviazione cloud | È ora possibile definire l’accesso a una sottocartella specifica dell’origine di archiviazione cloud al momento della creazione di un nuovo account. Una volta creati, gli utenti potranno accedere solo ai dati della sottocartella consentita. Questa funzione è disponibile per le seguenti origini di archiviazione cloud: [Archiviazione BLOB di Azure](../../sources/connectors/cloud-storage/blob.md), [Archiviazione cloud Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilità beta di [!DNL SugarCRM] | [!DNL SugarCRM] Le origini di sono ora disponibili in versione beta. Utilizza il [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] per importare i dati dal tuo [!DNL SugarCRM] da Experience Platform. Per ulteriori informazioni, leggere [[!DNL SugarCRM] panoramica](../../sources/connectors/crm/sugarcrm.md). |