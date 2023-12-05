---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2023
description: Note sulla versione di Adobe Experience Platform di gennaio 2023.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: d23f1cc9dd0155aceae78bf938d35463e9c38181
workflow-type: tm+mt
source-wordcount: '2224'
ht-degree: 99%

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

I servizi di intelligenza artificiale e apprendimento automatico consentono agli analisti e ai professionisti del marketing di sfruttare il potere dell’intelligenza artificiale e dell’apprendimento automatico nei casi d’uso dell’esperienza cliente. Questo consente agli analisti di marketing di impostare previsioni, senza la necessità di competenze di data science, specifiche per le esigenze di un’azienda, utilizzando configurazioni di livello aziendale.

### IA per l’attribuzione

L’IA per l’attribuzione viene utilizzata per attribuire crediti ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzata dai marketer per quantificare l’impatto di ogni punto di contatto di marketing lungo i percorsi della clientela.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzionalità di preparazione HIPAA | I clienti Healthcare Shield ora possono ricevere, utilizzare, mantenere o trasmettere informazioni protette sulla salute nell’IA per l’attribuzione e in alcune altre applicazioni basate su Experience Platform. L’Healthcare Shield è per i clienti nel settore dell’assistenza sanitaria che sono soggetti interessati o partner commerciali ai sensi dell’HIPAA. Per ulteriori informazioni, consulta la documentazione su [HIPAA e prodotti e servizi Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| Modificare colonne aggiuntive del set di dati di punteggio | È ora possibile aggiungere o rimuovere colonne aggiuntive di set di dati di punteggio (colonne di reporting) quando si modificano modelli esistenti. Questo estende la flessibilità dei punteggi di attribuzione per fornirti approfondimenti sulle dimensioni aggiuntive dopo la creazione di un modello. Per ulteriori informazioni, consulta la [Guida all’interfaccia utente di Attribution](../../intelligent-services/attribution-ai/user-guide.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la panoramica sui [Servizi di IA/ML](../../intelligent-services/attribution-ai/overview.md).

### IA per l’analisi dei clienti

L’IA per l’analisi dei clienti per Real-time Customer Data Platform viene utilizzata per generare punteggi di propensione personalizzati, come l’abbandono e la conversione per singoli profili su larga scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di apprendimento automatico né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

**Funzioni aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Funzionalità di preparazione HIPAA | I clienti Healthcare Shield ora possono ricevere, utilizzare, mantenere o trasmettere informazioni protette sulla salute nell’IA per l’analisi dei clienti per Real-time Customer Data Platform e alcune altre applicazioni basate su Experience Platform. L’Healthcare Shield è per i clienti nel settore dell’assistenza sanitaria che sono soggetti interessati o partner commerciali ai sensi dell’HIPAA. Per ulteriori informazioni, consulta la documentazione su [HIPAA e prodotti e servizi per Adobe](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

Per ulteriori informazioni, consulta la panoramica sui [Servizi di IA/ML](../../intelligent-services/customer-ai/overview.md).

## Assurance {#assurance}

Adobe Assurance consente di controllare, provare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze all’interno delle tue applicazioni mobili.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Editor di convalida | Sono stati aggiunti nuovi miglioramenti all’Editor di convalida. Questi miglioramenti includono colonne di convalida, nuovi strumenti di creazione del codice e viste migliorate. |

{style="table-layout:auto"}

Per ulteriori informazioni su Assurance, consulta la [documentazione di Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuova schermata iniziale | La pagina Home dell’interfaccia utente della Raccolta dati è stata aggiornata per includere informazioni utili sull’onboarding e collegamenti per ottimizzare la produttività. Ciò include:<ol><li>Documentazione e flussi di lavoro consigliati per iniziare</li><li>Proprietà, regole ed elementi dati recenti</li><li>Estensioni popolari</li><li>Nuovi aggiornamenti delle estensioni con una funzione di installazione rapida</li></ol> |
| Inviare dati a [!DNL Google Ads] utilizzando l’inoltro degli eventi | Ora puoi utilizzare l’[[!DNL Google Ads Enhanced Conversions] estensione API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) per l’inoltro di eventi, in combinazione con i [segreti OAuth 2 di Google](../../tags/ui/event-forwarding/secrets.md#google-oauth2), per inviare in modo sicuro i dati lato server a [!DNL Google Ads] in tempo reale. |

{style="table-layout:auto"}

## Destinazioni (aggiornato il 2 febbraio) {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [Connessione ai tipi di pubblico di Adobe Experience Cloud (Beta)](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Utilizza la connessione ai [!UICONTROL Tipi di pubblico di Adobe Experience Cloud (Beta)] per condividere segmenti da Experience Platform a varie soluzioni di Experience Platform, come Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo. |
| [Connessione profilo Pega](../../destinations/catalog/personalization/pega-profile.md) | Utilizza il [!DNL Pega Profile Connector] in Adobe Experience Platform per creare una connessione in uscita alla tua Archiviazione S3 [!DNL Amazon] ed esportare periodicamente i dati del profilo in file CSV da Adobe Experience Platform nei tuoi bucket S3. In [!DNL Pega Customer Decision Hub], è possibile pianificare processi di dati per importare questi dati profilo dall’archiviazione S3 per aggiornare il profilo di [!DNL Pega Customer Decision Hub]. |
| [Connessione Trade Desk al CRM dell’UE (Beta)](../../destinations/catalog/advertising/tradedesk-emails.md) | Con il rilascio dell’EUID (European Unified ID), nel [catalogo delle destinazioni](/help/destinations/catalog/overview.md) ora vengono visualizzate due destinazioni [!DNL The Trade Desk - CRM]. <ul><li> Se i dati vengono originati nell’UE, utilizza la destinazione **[!DNL The Trade Desk - CRM (EU)]**.</li><li> Se i dati vengono originati nelle aree geografiche APAC o NAMER, utilizza la destinazione **[!DNL The Trade Desk - CRM (NAMER & APAC)]**. </li></ul> |

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Miglioramento dei criteri di consenso dei paid media per integrazioni con destinazioni di streaming | Un [miglioramento dell’applicazione dei criteri di consenso](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations) per casi d’uso di attivazione di paid media. Quando i profili non sono più qualificati per un criterio di consenso, Experience Platform ora comunica in modo proattivo l’uscita dal criterio alle destinazioni di streaming.<br> <b>Nota</b>: questa funzionalità è disponibile solo per i clienti di **[!UICONTROL Privacy and Security Shield]** e quelli di **[!UICONTROL Healthcare Shield]**. |
| Nuove opzioni del delimitatore per i connettori di destinazione dell’archiviazione cloud beta | Tre nuove opzioni del delimitatore (due punti `:`, barra verticale, punto e virgola `;`) sono ora disponibili per le nuove destinazioni dell’archiviazione cloud versione beta: [Amazon S3 (Beta)](/help/destinations/catalog/cloud-storage/amazon-s3.md), [BLOB di Azure (Beta)](/help/destinations/catalog/cloud-storage/azure-blob.md), [Azure Data Lake Storage Gen2 (Beta)](/help/destinations/catalog/cloud-storage/adls-gen2.md), [Data Landing Zone (Beta)](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [ Google Cloud Storage (Beta)](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP (Beta)](/help/destinations/catalog/cloud-storage/sftp.md). <br> Per le informazioni basate su file, consulta le informazioni sulle [opzioni di formattazione file](/help/destinations/ui/batch-destinations-file-formatting-options.md). |
| Nuovo parametro opzionale disponibile nelle configurazioni del [campi dati cliente](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) in [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: utilizza questo parametro quando è necessario creare un campo di dati cliente il cui valore deve essere univoco in tutti i flussi di dati di destinazione impostati dall’organizzazione di un utente. <br> Ad esempio, il campo **[!UICONTROL Alias di integrazione]** in [[!UICONTROL Personalizzazione personalizzata]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) la destinazione deve essere univoca, vale a dire che due flussi di dati separati verso questa destinazione non possono avere lo stesso valore per questo campo. |

**Correzioni di problemi e miglioramenti** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Correzione o miglioramento</b></td>
        <td><b>Descrizione</b></td>
    </tr>
    <tr>
        <td>Aggiornamento del comportamento di esportazione nelle destinazioni basate su file (PLAT-123316)</td>
        <td>È stato risolto un problema nel comportamento degli <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">attributi obbligatori</a> durante l’esportazione di file di dati in destinazioni batch. <br> In precedenza, ogni record nei file di output veniva verificato in modo che contenesse sia: <ol><li>Un valore non nullo della colonna <code>mandatoryField</code> e</li><li>Un valore non nullo in almeno uno degli altri campi non obbligatori.</li></ol> La seconda condizione è stata rimossa. Di conseguenza, è possibile che nei file di dati esportati vengano visualizzate più righe di output, come illustrato nell’esempio seguente:<br> <b>Esempio di comportamento prima della versione di gennaio 2023 </b> <br>Campo obbligatorio: <code>emailAddress</code> <br> <b>Dati di input da attivare</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Output di attivazione</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Comportamento di esempio dopo la versione di gennaio 2023 </b> <br> <b>Output di attivazione</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>Convalida dell’interfaccia utente e dell’API per le mappature richieste e le mappature duplicate (PLAT-123316)</td>
        <td>La convalida ora viene applicata nell’interfaccia utente e nell’API quando i <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">campi di mappatura</a> nel flusso di lavoro di attivazione delle destinazioni nel modo seguente:<ul><li><b>Mappature richieste</b>: se la destinazione è stata impostata dallo sviluppatore di destinazione con le mappature richieste (ad esempio, la destinazione <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html">Google Ad Manager 360</a>), le mappature richieste devono essere aggiunte dall’utente durante l’attivazione dei dati nella destinazione. </li><li><b>Mappature duplicate</b>: nel passaggio di mappatura del flusso di lavoro di attivazione, è possibile aggiungere valori duplicati nei campi di orgine ma non nei campi di destinazione. Consulta la tabella seguente per un esempio di combinazioni di mappatura consentite e non consentite. <br><table><thead><tr><th>Consentito/non consentito</th><th>Campo di origine</th><th>Campo di destinazione</th></tr></thead><tbody><tr><td>Consentito</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>e-mail alias2</li></ul></td></tr><tr><td>Non consentito</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Miglioramenti al nome visualizzato della struttura ad albero | In precedenza, i nomi dei campi venivano visualizzati nell’interfaccia utente, ma ora i nomi visualizzati per i campi schema nell’area di lavoro dello schema sono più facili da leggere. |

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversione]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Classe per il tracciamento dei dati di conversione, ad esempio le conversioni di valuta. |
| Gruppo di campi | [[!UICONTROL Dettagli del tasso di conversione valuta]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Un gruppo di campi per la classe [!UICONTROL Conversione], che acquisisce ulteriori dettagli relativi alla conversione della valuta. |
| Gruppo di campi | [[!UICONTROL Mappa dei risultati della valutazione dei criteri di consenso con metadati]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.json) | Acquisisce i dettagli dei risultati della valutazione di più criteri di consenso, incluse le informazioni sui metadati relativi alle entrate e alle uscite dai criteri di consenso. |

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della pubblicità]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | Il campo `ID` è stato rinominato in `name`, e il precedente campo `name` è ora `friendlyName`. |
| Tipo di dati | [[!UICONTROL Dettagli della proposta di decisione]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | È stato aggiunto un campo `selectionStrategy` che acquisisce i dettagli di una strategia di selezione. |
| Gruppo di campi | [[!UICONTROL Evento esperienza: interazioni della proposta]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Il gruppo di campi è ora compatibile con la classe [!UICONTROL Evento passaggio del percorso]. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dell’errore]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | Il campo `ID` è stato rinominato in `name`. |
| Tipo di dati | [[!UICONTROL Informazioni sui file multimediali]](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/media.schema.json) | È stata ripristinata una modifica del pattern alla proprietà del segmento video. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati QoE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | È stato rimosso il campo `droppedFrameCount`. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli della sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Rinominato il campo `isAuthorized` in `authorized`, e aggiornato il relativo `type` in una stringa che in precedenza era un valore booleano. |
| Tipo di dati | [[!UICONTROL Spedizione]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Sono stati aggiunti diversi nuovi campi: `shipDate`, `trackingNumber`, e `trackingURL`. |
| Gruppo di campi | [[!UICONTROL Campi entità AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Sono stati aggiunti diversi nuovi campi: `journeyNodeID`, `journeyNodeName`, e `journeyModeType`. |
| Gruppo di campi | [[!UICONTROL Evento esperienza consumatore]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Il gruppo di campi è ora compatibile anche con la classe [!UICONTROL Metriche di riepilogo]. |
| Gruppo di campi | [[!UICONTROL Trigger del prodotto]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | Il campo `productTriggers` è ora nidificato in un oggetto `weather`. |
| Gruppo di campi | [[!UICONTROL Trigger relativi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | Il campo `relativeTriggers` è ora nidificato in un oggetto `weather`. |
| Gruppo di campi | [[!UICONTROL Trigger gravi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Il campo `severeTriggers` è ora nidificato in un oggetto `weather`. |
| Gruppo di campi | [[!UICONTROL Trigger meteo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | Il campo `weatherTriggers` è ora nidificato in un oggetto `weather`. |
| Gruppo di campi | [[!UICONTROL Account aziendali correlati a XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Il gruppo di campi è ora stabile. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la [Panoramica sul sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di promuovere esperienze coordinate, coerenti e pertinenti per la tua clientela, indipendentemente da dove e quando interagisce con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati clienti in una visualizzazione unificata che offre un account utilizzabile e dotato di marca temporale per ogni interazione con il cliente.

**Prossima funzione obsoleta** {#deprecation}

Per rimuovere la ridondanza nel ciclo di vita dell’appartenenza al segmento, lo stato `Existing` diventerà obsoleto dalla [mappa di appartenenza al segmento](../../xdm/field-groups/profile/segmentation.md) alla fine di marzo 2023. Un annuncio di follow-up includerà la data esatta della deprecazione.

Dopo la deprecazione, i profili qualificati in un segmento verranno rappresentati come `Realized` e i profili non qualificati continueranno a essere rappresentati come `Exited`. Questo porterà la parità con le destinazioni basate su file con stati dei segmenti `Active` e `Expired`.

Se utilizzi le [destinazioni Enterprise](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hub, API HTTP) e disponi di processi downstream automatizzati basati su stati `Existing`, questa modifica potrebbe interessarti. Se questo è il caso, controlla le integrazioni a valle. Se ti interessa identificare profili nuovi e qualificati oltre un certo periodo di tempo, puoi utilizzare una combinazione di stati `Realized` e il `lastQualificationTime` nella mappa di appartenenza al segmento. Per ulteriori informazioni, contatta il rappresentante Adobe.

Per ulteriori informazioni sul Profilo cliente in tempo reale, inclusi tutorial e best practice per l’utilizzo dei dati del profilo, inizia consultando la [Panoramica sul Profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Importazione in blocco dei valori in Segment Builder | Segment Builder ora supporta l’importazione di più valori, caricando un file CSV o TSV oppure inserendo manualmente valori separati da virgola. Ulteriori informazioni sono disponibili nella sezione [Guida a Segment Builder](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| Scadenza appartenenza al pubblico esterno | Per impostazione predefinita, le appartenenze a un pubblico esterno vengono mantenute per 30 giorni. Per conservarle più a lungo, utilizza il campo `validUntil` durante l’acquisizione dei dati sul pubblico. |
| Scadenza dell’appartenenza a un segmento generata dalla piattaforma | Qualsiasi appartenenza a un segmento nello stato di `Exited` per più di 30 giorni, basato sul campo `lastQualificationTime` sarà soggetta a eliminazione. |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da origini esterne e consente di strutturarli, etichettarli e migliorarli utilizzando i servizi di Platform. Puoi acquisire dati da diverse origini, ad esempio da applicazioni Adobe, dall’archiviazione basata su cloud, da software di terze parti e dal sistema CRM.

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

| Funzione | Descrizione |
| --- | --- |
| Consentire l’accesso utente alle sottocartelle delle origini di archiviazione cloud | Al momento della creazione di un nuovo account, è ora possibile definire l’accesso a una sottocartella specifica dell’origine di archiviazione cloud. Una volta creato, gli utenti potranno accedere solo ai dati della sottocartella consentita. Questa funzione è disponibile per le seguenti origini di archiviazione cloud: [Archiviazione BLOB di Azure](../../sources/connectors/cloud-storage/blob.md), [Archiviazione cloud Google](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilità in versione beta di [!DNL SugarCRM] | Le origini [!DNL SugarCRM] sono ora disponibili in versione beta. Utilizza le origini [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] per importare i dati dal tuo account [!DNL SugarCRM] su Experience Platform. Per ulteriori informazioni, consulta la [[!DNL SugarCRM] panoramica](../../sources/connectors/crm/sugarcrm.md). |
