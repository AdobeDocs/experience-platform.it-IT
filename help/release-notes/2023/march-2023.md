---
title: Note sulla versione di Adobe Experience Platform - Marzo 2023
description: Note sulla versione di marzo 2023 per Adobe Experience Platform.
source-git-commit: e597656949ba81b4a07c2962a02ddd94c6dc23e3
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 5%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 29 marzo 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Dashboard](#dashboards)
- [Raccolta dati](#data-collection)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Experience Data Model](#xdm)
- [Servizio query](#query-service)
- [Edizione B2B di Real-Time Customer Data Platform](#b2b)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Dashboard {#dashboards}

Adobe Experience Platform offre diverse dashboard attraverso le quali puoi visualizzare informazioni importanti sui dati dell’organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate** {#dashboards-new-updated-features}

| Funzione | Descrizione |
| --- | --- |
| Dashboard definiti dall&#39;utente | Ora puoi **valori degli attributi di esempio** prima di aggiungere un attributo a un widget nel compositore di widget per dashboard definito dall&#39;utente. Alcuni valori di esempio da quella colonna di attributi sono disponibili per i singoli attributi durante la creazione di un widget.<br>Ora puoi **scambiare l&#39;asse X e Y** sul widget con il pulsante dell&#39;asse di scambio. Questo consente di risparmiare tempo e offre un’esperienza più ergonomica quando si aggiungono attributi ai widget. In questo modo si salva la necessità di trovare nuovamente entrambi gli attributi dal pannello attributi.<br> Ora puoi **modificare la posizione e il titolo della legenda** all&#39;interno dei widget. Una volta che una legenda è presente su un widget, è possibile riposizionare la legenda in qualsiasi punto del grafico e rinominare anche il titolo della legenda, come è possibile con le etichette dell&#39;asse e il titolo del widget. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere autorizzazioni di accesso e creare widget personalizzati, inizia leggendo il [panoramica delle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che ti consentono di raccogliere i dati sull’esperienza del cliente lato client e inviarli ad Adobe Experience Platform Edge Network dove possono essere arricchiti, trasformati e distribuiti su destinazioni Adobi o non Adobi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Nuovo flusso di lavoro di avvio rapido per l’API Meta Conversioni (Beta) | Accedi ai nuovi flussi di lavoro di avvio rapido in &quot;Guida introduttiva&quot; dalla schermata iniziale Raccolta dati. La [flusso di lavoro di avvio rapido per l’API Meta Conversions](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) consente ai clienti di raccogliere e inoltrare rapidamente i dati evento, lato server a Meta per le conversioni di annunci in pochi semplici passaggi. |
| Nuovo flusso di lavoro di avvio rapido per Mobile SDK (Beta) | Accedi ai nuovi flussi di lavoro di avvio rapido in &quot;Guida introduttiva&quot; dalla schermata iniziale Raccolta dati. La [flusso di lavoro di avvio rapido per Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) consente di implementare rapidamente l’SDK di Mobile e convalidare gli eventi mobile di base in pochi semplici passaggi. |
| [!DNL Braze] estensione di inoltro eventi | La [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) l’estensione di inoltro eventi consente di sfruttare i dati acquisiti in Adobe Experience Platform Edge Network e inviarli a [!DNL Braze] sotto forma di eventi lato server che utilizzano [!DNL Braze] API di tracciamento utente. |
| [!DNL Epsilon] estensione di inoltro eventi | La [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) l’estensione ti consente di sfruttare l’inoltro eventi per acquisire informazioni sull’evento in Adobe Experience Platform Edge Network e inviarle a [!DNL Epsilon] utilizzando [!DNL Epsilon] API evento. |
| [!DNL Mixpanel] estensione di inoltro eventi | La [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) L’estensione consente ai clienti di sfruttare l’inoltro eventi per acquisire informazioni sull’evento in Adobe Experience Platform Edge Network e inviarle a Mixpanel utilizzando l’API Track Events. |

{style="table-layout:auto"}

## Preparazione dei dati {#data-prep}

Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale del filtro per i dati Adobe Analytics | È ora possibile utilizzare le funzionalità di preparazione dei dati per applicare regole e condizioni per filtrare i dati di Analytics prima di acquisirli in Profilo cliente in tempo reale. Per ulteriori informazioni, consulta la guida su [filtraggio dei dati di Analytics per l’acquisizione del profilo](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| Nuove funzioni per la codifica e la decodifica delle stringhe URL | <ul><li>La `get_url_encoded` prende un URL come input e sostituisce o codifica caratteri speciali con caratteri ASCII.</li><li>La `get_url_decoded` prende un URL come input e decodifica i caratteri ASCII in caratteri speciali.</li></ul> Per ulteriori informazioni, consulta la sezione [Guida alle funzioni di preparazione dei dati](../../data-prep/functions.md). Per un elenco completo dei caratteri riservati e dei corrispondenti caratteri codificati, consulta la guida in [caratteri speciali](../../data-prep/functions.md#special-characters). |

Per ulteriori informazioni su Data Prep, consulta la sezione [Panoramica sulla preparazione dei dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

**Nuove destinazioni** {#new-destinations}

| Destinazione | Descrizione |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] connessione GA](../../destinations/catalog/personalization/adobe-commerce.md) | La [!DNL Adobe Commerce] il connettore di destinazione (ora disponibile in genere) consente di selezionare uno o più tipi di pubblico Real-Time CDP da attivare nel [!DNL Adobe Commerce] per offrire un’esperienza personalizzata dinamica ai tuoi acquirenti. |
| [[!DNL Snap Inc] connessione GA](../../destinations/catalog/advertising/snap-inc.md) | La [!DNL Snap Inc] il connettore di destinazione (ora generalmente disponibile) consente agli addetti al marketing di importare i segmenti utente creati in Experience Platform in [!DNL Snapchat Ads] e utilizzarli per eseguire il targeting dei loro annunci. |
| [(API) Oracle di connessione Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | Utilizzare la connessione basata su API per [!DNL Oracle Eloqua] pianificare ed eseguire campagne offrendo al tempo stesso un&#39;esperienza cliente personalizzata per i loro potenziali clienti in [!DNL Oracle Eloqua]. |
| [(Beta) [!DNL Amazon Ads] connection](../../destinations/catalog/advertising/amazon-ads.md) | La [!DNL Amazon Ads] l&#39;integrazione con Adobe Experience Platform fornisce un&#39;integrazione chiavi in mano a [!DNL Amazon Ads] i prodotti, compresi i [!DNL Amazon DSP (ADSP)]. Utilizzo della [!DNL Amazon Ads] in Adobe Experience Platform, gli utenti possono definire il pubblico dell’inserzionista per il targeting e l’attivazione sul [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] connection](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (precedentemente Bizible) offre agli esperti di marketing informazioni sulle attività di marketing più efficaci per incrementare le entrate e massimizzare il ritorno sull’investimento per la loro azienda. La destinazione consente il flusso di dati business-to-business (B2B) da Adobe Experience Platform a [!DNL Marketo Measure]. La scheda è disponibile solo per [!DNL Marketo Measure Ultimate] clienti. |
| [Connessione TikTok](../../destinations/catalog/social/tiktok.md) | Crea tipi di pubblico personalizzati su TikTok con i tuoi dati per il targeting con le tue campagne pubblicitarie. |
| [Connessione Zendesk](../../destinations/catalog/crm/zendesk.md) | Utilizza questa destinazione per creare e aggiornare le identità all’interno di un segmento come contatti all’interno di [!DNL Zendesk]. |

{style="table-layout:auto"}

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

| Funzionalità | Descrizione |
| ----------- | ----------- |
| Nuova autorizzazione di controllo accessi per le destinazioni: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | La nuova autorizzazione consente agli utenti di attivare i segmenti sulle destinazioni esistenti, senza visualizzare il [fase di mappatura](../../destinations/ui/activate-batch-profile-destinations.md#mapping). Gli utenti possono aggiungere e rimuovere segmenti nei flussi di lavoro di attivazione, ma non possono aggiungere o rimuovere attributi o identità mappati. |

{style="table-layout:auto"}

**Correzioni e miglioramenti** {#destinations-fixes-and-enhancements}

Stiamo rilasciando una correzione di bug per la crittografia PGP/GPG nelle destinazioni basate su file per Real-time CDP. Con questa modifica, le destinazioni basate su file esistenti che utilizzano attualmente la crittografia genereranno un nome di file con un’estensione diversa da quella precedente.

- Estensione corrente quando si utilizza la crittografia: `filename.csv`
- Estensione futura quando utilizzi la crittografia: `filename.csv.gpg`

Per informazioni più generali sulle destinazioni, consulta [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Raccomandazione CSV to schema | Ora puoi caricare i file locali per creare schemi generati da machine learning che eliminano la necessità di creare manualmente uno schema. Da [!UICONTROL Origini] , carica un file CSV di esempio e gli algoritmi di machine learning di Adobe ti suggeriranno uno schema basato sui campi di destinazione. Per ulteriori informazioni, consulta la [documentazione](../../ingestion/tutorials/map-csv/recommendations.md) dello strumento.&quot; |

{style="table-layout:auto"}

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Articolo offerta]](https://github.com/adobe/xdm/pull/1678/files) | Classe che rappresenta un&#39;offerta. |
| Classe | [[!UICONTROL Elemento decisionale]](https://github.com/adobe/xdm/pull/1678/files) | Un elemento che può essere sottoposto a decisioni. Il risultato di un processo decisionale è uno o più elementi decisionali. |
| Classe | [[!UICONTROL Timeout del server della sessione multimediale]](https://github.com/adobe/xdm/pull/1676/files) | Indica il tempo, in secondi, trascorso tra l’ultima interazione nota dell’utente e il momento in cui la sessione è stata chiusa. |
| Gruppo di campi | [[!UICONTROL Attributi calcolati del profilo XDM]](https://github.com/adobe/xdm/pull/1686/files) | In questo modo si aggiungono gli attributi calcolati dai servizi Adobe interni ai dati dei clienti in arrivo. I clienti non devono utilizzarli per acquisire i dati. |
| Tipo di dati | [[!UICONTROL Articolo Rimborso]](https://github.com/adobe/xdm/pull/1685/files) | Indica se un rimborso è associato a un ordine e definisce il tipo di rimborso, l&#39;importo e la valuta associata. |
| Tipo di dati | [[!UICONTROL Dati per categoria]](https://github.com/adobe/xdm/pull/1677/files) | Questo nuovo tipo di dati rappresenta la categoria di un prodotto. |
| Schema | [[!UICONTROL Campi di classificazione Adobe Target]](https://github.com/adobe/xdm/pull/1682/files) | È stato creato un nuovo schema XDM per i set di dati di classificazione di Target. Contiene un set di campi meta-dati che classificano le attività e le esperienze di Target. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Gruppo di campi | [[!UICONTROL Dettagli dei componenti di contenuto]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` è stato rimosso da [!UICONTROL Dettagli dei componenti di contenuto] |
| Gruppo di campi | [[!UICONTROL Tag di entità AJO]](https://github.com/adobe/xdm/pull/1672/files) | Aggiunti tag di entità AJO a [!UICONTROL Campi di entità AJO], corrispondente a un Percorso o a una campagna |
| Gruppo di campi | (Multipli) | Sono stati aggiunti diversi campi per [[!UICONTROL Campi comuni evento evento passaggio Journey Orchestration]](https://github.com/adobe/xdm/pull/1671/files) |
| Gruppo di campi | (Multipli) | [Sono stati aggiunti diversi tipi di eventi XDM per [!UICONTROL Reporting multimediale]](https://github.com/adobe/xdm/pull/1670/files). |
| Gruppo di campi | [!UICONTROL Evento di modifica Workfront] | La `Full Record` e `Accessor Employee Ids` sono stati aggiunti gruppi di campi. |
| Tipo di dati | [[!UICONTROL Voce dell’elenco dei prodotti]](https://github.com/adobe/xdm/pull/1685/files) | La [!UICONTROL Importo Rimborso] è stato aggiunto per indicare l&#39;importo rimborsato dell&#39;articolo, se presente. |
| Tipo di dati | [[!UICONTROL Ordine ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL Elenco dei rimborsi] è stato aggiunto all&#39;elenco dei rimborsi per il presente ordine. |
| Tipo di dati | [[!UICONTROL Voce di elenco prodotti ]](https://github.com/adobe/xdm/pull/1677/files) | Le categorie di prodotti sono state aggiunte all&#39;elenco dei dati della categoria del prodotto. |
| Tipo di dati | [!UICONTROL Informazioni sulla sessione] | È stato aggiunto il `pev3` campo stringa che [indica il tipo di flusso multimediale utilizzato per il reporting](https://github.com/adobe/xdm/pull/1676/files). Inoltre, è stato aggiunto il `pccr` La proprietà indica se si è verificato un reindirizzamento. |
| Tipo di dati | [!UICONTROL Elenco richieste di acquisto] | Fornisce la [proprietà elenco richieste](https://github.com/adobe/xdm/pull/1675/files). Includono nome, ID e descrizione. |
| Tipo di dati | [!UICONTROL Commerce] | La [Aggiornamento del tipo di dati Commerce](https://github.com/adobe/xdm/pull/1675/files) per includere `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`e `requisitionList`. |

{style="table-layout:auto"}

Per ulteriori informazioni su XDM in Platform, consulta la sezione [Panoramica del sistema XDM](../../xdm/home.md).

## Servizio query {#query-service}

Query Service consente di utilizzare SQL standard per eseguire query sui dati in Adobe Experience Platform [!DNL Data Lake]. Puoi unire qualsiasi set di dati da data lake e acquisire i risultati della query come nuovo set di dati da utilizzare nel reporting, in Data Science Workspace o per l’inserimento nel Profilo cliente in tempo reale.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Controllo dell&#39;accesso basato su attributi nell&#39;archivio accelerato | Utilizza il controllo dell&#39;accesso basato su attributi con Data Distiller per definire il controllo dell&#39;accesso su tutti i set di dati nell&#39;archivio accelerato. Questo controlla l’accesso ai modelli di dati personalizzati creati dagli utenti e memorizzati in un archivio accelerato per alimentare dashboard personalizzati. |

{style="table-layout:auto"}

Per ulteriori informazioni sui servizi di query, consulta la [Panoramica del servizio query](../../query-service/home.md).

## Edizione B2B di Real-Time Customer Data Platform {#b2b}

Basato su Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Riunisce i dati provenienti da più sorgenti e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli esperti di marketing di eseguire il targeting preciso di tipi di pubblico specifici e coinvolgerli in tutti i canali disponibili.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Bugfix | Per fornire una rappresentazione più accurata dei profili nel sistema, il sistema non include più i profili interni nel conteggio totale dei profili o nella metrica di pubblico indirizzabile per Real-time Customer Data Platform B2B Edition. A partire da oggi, potresti notare un calo una tantum nella metrica di conteggio totale dei profili/pubblico indirizzabile. Nessuno dei tuoi dati è stato cancellato, si tratta semplicemente di una modifica al conteggio. Contatta il tuo responsabile Adobe per eventuali dubbi |

{style="table-layout:auto"}

Per ulteriori informazioni su Real-Time CDP B2B Edition, consulta la sezione [Panoramica di Real-Time CDP B2B Edition](../../rtcdp/overview.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Metriche del profilo | Per ottenere una rappresentazione più accurata delle metriche di profilo, la suddivisione dei membri e le metriche di abbandono vengono combinate e ora vengono calcolate in un periodo di 24 ore. Ulteriori informazioni sono disponibili nella sezione [Guida all’interfaccia utente di segmentazione](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

Per ulteriori informazioni su [!DNL Segmentation Service], vedi [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Adobe Experience Platform può acquisire dati da sorgenti esterne e consente di strutturare, etichettare e migliorare tali dati utilizzando i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, software di terze parti e il sistema CRM in uso.

L’Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva che consente di impostare facilmente le connessioni sorgente per vari provider di dati. Queste connessioni di origine ti consentono di autenticare e connettersi a sistemi di archiviazione esterni e servizi CRM, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

**Funzioni aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità beta [!DNL Chatlio] | La [!DNL Chatlio] la sorgente è ora disponibile in versione beta. Utilizza la [!DNL Chatlio] origine per lo streaming [!DNL Chatlio] dati degli eventi ad Experience Platform. Per ulteriori informazioni, consulta la sezione [[!DNL Chatlio] panoramica](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| Disponibilità beta [!DNL Customer.io] | La [!DNL Customer.io] la sorgente è ora disponibile in versione beta. Utilizza la [!DNL Customer.io] origine per lo streaming ad Experience Platform dei dati degli eventi cliente. Per ulteriori informazioni, consulta la sezione [[!DNL Customer.io] panoramica](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| Disponibilità beta [!DNL Pendo] | La [!DNL Pendo] la sorgente è ora disponibile in versione beta. Utilizza la [!DNL Pendo] per lo streaming ad Experience Platform dei dati di analisi dei prodotti. Per ulteriori informazioni, consulta la sezione [[!DNL Pendo] panoramica](../../sources/connectors/analytics/pendo-webhook.md). |
| Supporto per i flussi di dati bozze | Ora puoi utilizzare l’API del servizio di flusso per impostare i flussi di dati su uno stato bozza. I flussi di dati elaborati possono essere successivamente aggiornati e pubblicati con nuove informazioni. Per ulteriori informazioni, consulta la guida su [impostazione dei flussi di dati di origine come bozze](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, consulta la sezione [panoramica di origini](../../sources/home.md).
