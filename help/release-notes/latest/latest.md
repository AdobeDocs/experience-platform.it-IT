---
title: Note sulla versione di Adobe Experience Platform - Gennaio 2023
description: Le note sulla versione di gennaio 2023 per Adobe Experience Platform.
source-git-commit: 4d69d0dbb1dd72279a6999cf2cda94e9fb380572
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 gennaio 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Assurance](#assurance)
- [Raccolta dati](#data-collection)
- [[!DNL Destinations]](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Profilo cliente in tempo reale](#profile)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Assurance {#assurance}

Adobe Assurance ti consente di controllare, provare, simulare e convalidare il modo in cui raccogli i dati o distribuisci le esperienze nell’app mobile.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Editor di convalida | Sono stati aggiunti nuovi miglioramenti all’editor di convalida. Questi miglioramenti includono colonne di convalida, nuovi strumenti per la creazione del codice e visualizzazioni migliorate. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su Assurance, leggere il [Documentazione di affidabilità](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuova schermata principale | La home page dell’interfaccia utente di raccolta dati è stata aggiornata con informazioni utili sull’onboarding e collegamenti per semplificare la produttività. Ciò include:<ol><li>Documentazione e flussi di lavoro consigliati per iniziare</li><li>Proprietà, regole ed elementi dati recenti</li><li>Estensioni popolari</li><li>Nuovi aggiornamenti di estensione con una funzione di installazione rapida</li></ol> |
| Invia dati a [!DNL Google Ads] utilizzo dell&#39;inoltro eventi | Ora puoi utilizzare la [[!DNL Google Ads Enhanced Conversions] Estensione API](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) per l&#39;inoltro di eventi, combinato con [Google Oauth 2 segreti](../../tags/ui/event-forwarding/secrets.md#google-oauth2), per inviare in modo sicuro i dati lato server a [!DNL Google Ads] in tempo reale. |

{style=&quot;table-layout:auto&quot;}

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni**

| Destinazione | Descrizione |
| ----------- | ----------- |
| [(Beta) Connessione di Adobe Experience Cloud Audiences](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Utilizza la [!UICONTROL (Beta) Pubblico Adobe Experience Cloud] connessione per condividere segmenti da Experience Platform a diverse soluzioni di Experience Platform, come ad Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target o Marketo. |
| [Connessione profilo Pega](../../destinations/catalog/personalization/pega-profile.md) | Utilizza la [!DNL Pega Profile Connector] in Adobe Experience Platform per creare una connessione in uscita diretta al tuo [!DNL Amazon] Archiviazione S3 per esportare periodicamente i dati del profilo in file CSV da Adobe Experience Platform nei bucket S3 personalizzati. In [!DNL Pega Customer Decision Hub], è possibile pianificare i processi dati per importare i dati del profilo dall&#39;archiviazione S3 per aggiornare [!DNL Pega Customer Decision Hub] profilo. |
| [(Beta) La connessione UE CRM per il settore commerciale](../../destinations/catalog/advertising/tradedesk-emails.md) | Con il rilascio di EUID (ID unificato europeo), ne vedrai due [!DNL The Trade Desk - CRM] destinazioni nel [catalogo delle destinazioni](/help/destinations/catalog/overview.md). <ul><li> Se si raccolgono dati nell&#39;UE, utilizzare il **[!DNL The Trade Desk - CRM (EU)]** destinazione.</li><li> Se si ottengono dati nelle aree APAC o NAMER, utilizzare il **[!DNL The Trade Desk - CRM (NAMER & APAC)]** destinazione. </li></ul> |

**Funzionalità nuove o aggiornate**

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Nuove opzioni di delimitazione per i connettori di destinazione dell&#39;archiviazione cloud beta | Tre nuove opzioni di delimitazione (due punti) `:`, Pipe, Punto e virgola `;`) sono ora disponibili per le nuove destinazioni di archiviazione cloud beta - [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [BLOB di Azure (Beta)](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) Data Landing Zone](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> Informazioni sul supporto [opzioni di formattazione dei file](/help/destinations/ui/batch-destinations-file-formatting-options.md) per le destinazioni basate su file. |
| Nuovo parametro opzionale disponibile in [campi dati del cliente](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) configurazioni [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: Utilizza questo parametro quando devi creare un campo dati cliente il cui valore deve essere univoco in tutti i flussi dati di destinazione impostati dall&#39;organizzazione di un utente. <br> Ad esempio, il **[!UICONTROL Alias di integrazione]** nel campo [[!UICONTROL Personalizzazione personalizzata]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) La destinazione deve essere univoca, il che significa che due flussi di dati separati per questa destinazione non possono avere lo stesso valore per questo campo. |

**Correzioni e miglioramenti** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>Correzione o miglioramento</b></td>
        <td><b>Descrizione</b></td>
    </tr>
    <tr>
        <td>È stato aggiornato il comportamento di esportazione nelle destinazioni basate su file (PLAT-123316)</td>
        <td>È stato risolto un problema nel comportamento di <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">attributi obbligatori</a> durante l’esportazione di file di dati in destinazioni batch. <br> In precedenza, ogni record nei file di output veniva verificato per contenere: <ol><li>Un valore non nullo del <code>mandatoryField</code> colonna e</li><li>Un valore non nullo su almeno uno degli altri campi non obbligatori.</li></ol> La seconda condizione è stata rimossa. Di conseguenza, potresti vedere più righe di output nei file di dati esportati, come mostrato nell’esempio seguente:<br> <b> Comportamento del campione prima della versione di gennaio 2023 </b> <br> Campo obbligatorio: <code>emailAddress</code> <br> <b>Dati di input da attivare</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>Uscita attivazione</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> Comportamento del campione dopo la versione di gennaio 2023 </b> <br> <b>Uscita attivazione</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
</table>

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disattivazione dei valori consigliati per i campi stringa | Ora puoi [disattivare i singoli valori consigliati per i campi stringa](../../xdm/ui/fields/enum.md) in [!UICONTROL Schemi] workspace, inclusi quelli provenienti da componenti standard. Questa funzione è disponibile solo per i campi con valori consigliati e non è supportata per i vincoli di enumerazione. |

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Conversione]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | Classe per il tracciamento dei dati di conversione come le conversioni di valuta. |
| Gruppo di campi | [[!UICONTROL Dettagli tasso di conversione valuta]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | Un gruppo di campi per [!UICONTROL Conversione] classe, acquisendo ulteriori dettagli relativi alla conversione di valuta. |
| Gruppo di campi | [[!UICONTROL I risultati della valutazione delle politiche di consenso vengono mappati con i metadati]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | Acquisisce i dettagli del risultato della valutazione di più criteri di consenso, comprese le informazioni sui metadati relativi alle entrate e all’esistenza dei criteri di consenso. |

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli pubblicitari]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | La `ID` è stato rinominato in `name`e il precedente `name` il campo è ora `friendlyName`. |
| Tipo di dati | [[!UICONTROL Dettagli della proposta di decisione]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | Aggiunta di un `selectionStrategy` campo che acquisisce i dettagli di una strategia di selezione. |
| Gruppo di campi | [[!UICONTROL Evento esperienza - Interazioni proposte]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | Il gruppo di campi è ora compatibile con [!UICONTROL Evento passaggio percorso] classe. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli degli errori]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | La `ID` è stato rinominato in `name`. |
| Tipo di dati | [[!UICONTROL Informazioni multimediali]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | Ripristino di una modifica del pattern nella proprietà del segmento video. |
| Tipo di dati | [[!UICONTROL Informazioni sui dettagli dei dati QE]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | È stato rimosso il `droppedFrameCount` campo . |
| Tipo di dati | [[!UICONTROL Informazioni sulla sessione]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | Rinominato il `isAuthorized` campo a `authorized`e ha aggiornato il `type` a una stringa quando in precedenza era un valore booleano. |
| Tipo di dati | [[!UICONTROL Spedizione]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Sono stati aggiunti diversi nuovi campi: `shipDate`, `trackingNumber`e `trackingURL`. |
| Gruppo di campi | [[!UICONTROL Campi di entità AJO]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | Sono stati aggiunti diversi nuovi campi: `journeyNodeID`, `journeyNodeName`e `journeyModeType`. |
| Gruppo di campi | [[!UICONTROL Evento esperienza consumatore]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | Il gruppo di campi è ora compatibile anche con [!UICONTROL Metriche di riepilogo] classe. |
| Gruppo di campi | [[!UICONTROL Trigger dei prodotti]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | La `productTriggers` è ora nidificato sotto a `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Trigger relativi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | La `relativeTriggers` è ora nidificato sotto a `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Trigger severi]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | La `severeTriggers` è ora nidificato sotto a `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Trigger del tempo]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | La `weatherTriggers` è ora nidificato sotto a `weather` oggetto. |
| Gruppo di campi | [[!UICONTROL Account commerciali correlati a XDM]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | Il gruppo di campi è ora stabile. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Profilo cliente in tempo reale {#profile}

Adobe Experience Platform ti consente di fornire ai clienti esperienze coordinate, coerenti e pertinenti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo consente di consolidare i dati dei clienti in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

**Prossima deprecazione** {#deprecation}

Per rimuovere la ridondanza nel ciclo di vita dell’appartenenza al segmento, la `Existing` lo stato verrà dichiarato obsoleto dal [mappa di appartenenza del segmento](../../xdm/field-groups/profile/segmentation.md) alla fine di marzo 2023. Un annuncio di follow-up includerà la data esatta di deprecazione.

Dopo un post obsoleto, i profili qualificati in un segmento saranno rappresentati come `Realized` e i profili squalificati continueranno a essere rappresentati come `Exited`. In questo modo la parità con le destinazioni basate su file con `Active` e `Expired` stati dei segmenti.

Questa modifica potrebbe interessarti se utilizzi [destinazioni aziendali](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) e dispongono di processi a valle automatizzati, in base al `Existing` stato. Controlla le integrazioni downstream se questo è il caso per te. Se sei interessato a identificare i nuovi profili qualificati oltre un certo periodo di tempo, considera l&#39;utilizzo di una combinazione dei `Realized` lo stato e `lastQualificationTime` nella mappa di appartenenza al segmento. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

Per ulteriori informazioni sul Profilo del cliente in tempo reale, compresi tutorial e best practice per l’utilizzo dei dati del profilo, consulta la sezione [Panoramica del profilo cliente in tempo reale](../../profile/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| ------- | ----------- |
| Scadenza dell’appartenenza al segmento generata dalla piattaforma | Qualsiasi appartenenza al segmento presente nella `Exited` per più di 30 giorni, in base alla `lastQualificationTime` sarà soggetto a eliminazione. |
| Scadenza dell&#39;iscrizione a un pubblico esterno | Per impostazione predefinita, le appartenenze al pubblico esterno vengono mantenute per 30 giorni. Per conservarli più a lungo, utilizza le `validUntil` durante l’acquisizione dei dati sul pubblico. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e consente di strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

| Funzione | Descrizione |
| --- | --- |
| Consenti accesso utente alle sottocartelle delle origini di archiviazione cloud | È ora possibile definire l’accesso a una sottocartella specifica dell’origine di archiviazione cloud durante la creazione di un nuovo account. Una volta creati, gli utenti potranno accedere solo ai dati della sottocartella consentita. Questa funzione è disponibile per le seguenti origini di archiviazione cloud: [Archiviazione BLOB di Azure](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md)e [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| Disponibilità beta [!DNL SugarCRM] | [!DNL SugarCRM] le origini sono ora disponibili in versione beta. Utilizza la [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] origini per ottenere i dati dal [!DNL SugarCRM] conto all&#39;Experience Platform. Per ulteriori informazioni, consulta la sezione [[!DNL SugarCRM] panoramica](../../sources/connectors/crm/sugarcrm.md). |