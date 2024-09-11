---
title: Amazon Ads
description: Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori di Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie. L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, incluso Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sull’DSP di Amazon.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 56971631eb7ab2ef3dd2dcf077ee3b52f131ffe7
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 2%

---

# (Beta) Connessione Amazon Ads {#amazon-ads}

## Panoramica {#overview}

[!DNL Amazon Ads] offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori di Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie.

L&#39;integrazione di [!DNL Amazon Ads] con Adobe Experience Platform fornisce l&#39;integrazione chiavi in mano ai prodotti [!DNL Amazon Ads], inclusi Amazon DSP (ADSP) e Amazon Marketing Cloud (AMC).

Utilizzando la destinazione [!DNL Amazon Ads] in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l&#39;attivazione nell&#39;DSP di Amazon.  Inoltre, gli utenti possono caricare i propri dati in [!DNL Amazon Marketing Cloud] per comprendere le prestazioni in base al pubblico, alle dimensioni fornite dall&#39;inserzionista, all&#39;appartenenza ai segmenti di Amazon o ad altri segnali disponibili in AMC. Dopo aver caricato i tipi di pubblico degli inserzionisti in AMC, gli utenti possono utilizzare [!DNL Amazon Marketing Cloud] per modificare, migliorare o aggiungere ai membri del pubblico utilizzando i segnali di Amazon provenienti da [!DNL Amazon Marketing Cloud].

AMC riunisce segnali univoci provenienti da tutte le proprietà possedute e gestite da Amazon, che si estendono su diversi tipi di media, tra cui display, video, streaming TV, audio e annunci sponsorizzati. Gli utenti possono inviare facilmente segmenti curati da Adobe Experience Platform ad AMC per migliorare l’apprendimento, ad esempio i gruppi del pubblico sul mercato, le coorti di lifestyle e i modelli di brand engagement. I segmenti aumentati possono quindi essere utilizzati per ottimizzare le attivazioni multimediali nell’DSP di Amazon.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team *[!DNL Amazon Ads]*. Attualmente si tratta di un prodotto beta la cui funzionalità è soggetta a modifiche. Per qualsiasi richiesta di informazioni o di aggiornamento, contattarli direttamente all&#39;indirizzo *`amc-support@amazon.com`.*

## Casi d’uso {#use-cases}

Per capire meglio come e quando utilizzare la destinazione *[!DNL Amazon Ads]*, ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Attivazione e targeting {#activation-and-targeting}

Questa integrazione con l&#39;DSP di Amazon consente agli inserzionisti [!DNL Amazon Ads] di trasmettere i tipi di pubblico CDP dell&#39;inserzionista da Adobe Experience Platform all&#39;DSP di Amazon per creare tipi di pubblico dell&#39;inserzionista per il targeting pubblicitario. I tipi di pubblico possono essere selezionati nell’DSP di Amazon per il targeting positivo e negativo (soppressione).

### Analytics e misurazione {#analytics-and-measurement}

Questa integrazione con [!DNL Amazon Marketing Cloud] (AMC) consente a [!DNL Amazon Ads] inserzionisti di passare segmenti CDP da Adobe Experience Platform Form ad AMC. Gli inserzionisti possono quindi unire gli input CDP con [!DNL Amazon Ads] segnali e condurre analisi personalizzate su argomenti quali l&#39;impatto mediatico, i segmenti di pubblico e i percorsi di clienti in un formato conforme alla privacy. Ad esempio, un inserzionista può caricare un elenco dei propri clienti esistenti per comprendere le prestazioni aggregate della campagna pubblicitaria, o statistiche aggregate di eventi di conversione su Amazon, come la visualizzazione di una pagina dei dettagli di un prodotto, l’aggiunta di un prodotto a un carrello o l’acquisto di un prodotto.

### Ottimizzazione di Advertising

Questa integrazione con [!DNL Amazon Marketing Cloud] (AMC) consente agli inserzionisti di caricare i propri elenchi di clienti e di utilizzare [!DNL Amazon Marketing Cloud] SQL per eseguire analisi di sovrapposizione, eliminazioni, aggiunte o ottimizzazioni ai tipi di pubblico in modo ricorrente prima di creare un pubblico pronto per l&#39;attivazione in Amazon DSP per il targeting.

## Prerequisiti {#prerequisites}

Per utilizzare la connessione [!DNL Amazon Ads] con Adobe Experience Platform, gli utenti devono prima avere accesso a un account Amazon DSP Advertiser o a un&#39;istanza [!DNL Amazon Marketing Cloud]. Per eseguire il provisioning di queste istanze, visitare la pagina seguente del sito Web [!DNL Amazon Ads]:

* [Introduzione all&#39;DSP di Amazon](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Introduzione al Marketing Cloud Amazon](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identità supportate {#supported-identities}

La connessione *[!DNL Amazon Ads]* supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service//features/namespaces.md). Per ulteriori dettagli sulle identità supportate da [!DNL Amazon Ads], visita il [Centro di supporto per l&#39;DSP di Amazon](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione *[!DNL Amazon Ads]*. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

Viene visualizzata l&#39;interfaccia di connessione [!DNL Amazon Ads] in cui sono stati selezionati per la prima volta gli account dell&#39;inserzionista a cui si desidera connettersi. Al momento della connessione, verrai reindirizzato a Adobe Experience Platform con una nuova connessione, fornita con l’ID dell’account inserzionista selezionato. Seleziona l’Account dell’inserzionista appropriato nella schermata di configurazione della destinazione per procedere.

* **[!UICONTROL Token Bearer]**: compila il token Bearer per l&#39;autenticazione nella destinazione.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Connessione Amazon Ads]**: selezionare l&#39;ID per l&#39;account [!DNL Amazon Ads] di destinazione utilizzato per la destinazione.

>[!NOTE]
>
>Dopo aver salvato la configurazione di destinazione, non potrai modificare l&#39;ID inserzionista [!DNL Amazon Ads], anche se effettui di nuovo l&#39;autenticazione tramite il tuo account Amazon. Per utilizzare un ID inserzionista [!DNL Amazon Ads] diverso, è necessario creare una nuova connessione di destinazione. Gli inserzionisti che sono già configurati su un’integrazione con ADSP per devono creare un nuovo flusso di destinazione se desiderano che i loro tipi di pubblico vengano consegnati ad AMC o a un altro account ADSP.

* **[!UICONTROL Regione dell&#39;inserzionista]**: seleziona l&#39;area appropriata in cui è ospitato l&#39;inserzionista. Per ulteriori informazioni sui marketplace supportati da ogni area geografica, visita la [documentazione di Amazon Ads](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Configura nuova destinazione](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

La connessione [!DNL Amazon Ads] supporta l&#39;indirizzo e-mail con hash e i numeri di telefono con hash per la corrispondenza delle identità. La schermata seguente fornisce un esempio di corrispondenza compatibile con la connessione [!DNL Amazon Ads]:

![Mappatura di Adobe ad Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Per mappare gli indirizzi e-mail con hash, selezionare lo spazio dei nomi dell&#39;identità `Email_LC_SHA256` come campo di origine.
* Per mappare i numeri di telefono con hash, selezionare lo spazio dei nomi dell&#39;identità `Phone_SHA256` come campo di origine.
* Per mappare indirizzi e-mail o numeri di telefono senza hash, seleziona gli spazi dei nomi di identità corrispondenti come campi di origine e seleziona l&#39;opzione `Apply Transformation` per fare in modo che Platform esegua l&#39;hashing delle identità al momento dell&#39;attivazione.
* *NUOVO a partire dalla versione di settembre 2024*: Amazon Ads richiede di mappare un campo contenente un valore `countryCode` in formato ISO a 2 caratteri per facilitare il processo di risoluzione delle identità (ad esempio: US, GB, MX, CA e così via). Le connessioni senza mappature `countryCode` avranno un impatto negativo sulle percentuali di corrispondenza delle identità.

Selezionare un determinato campo di destinazione una sola volta in una configurazione di destinazione del connettore [!DNL Amazon Ads].  Ad esempio, se invii un’e-mail aziendale, non puoi mappare anche l’e-mail personale nella stessa configurazione di destinazione.

Si consiglia vivamente di mappare tutti i campi disponibili. Se è disponibile un solo attributo di origine, è possibile mappare un singolo campo. La destinazione [!DNL Amazon Ads] utilizza tutti i campi mappati a scopo di mappatura, ottenendo percentuali di corrispondenza più elevate se vengono forniti più campi. Per ulteriori informazioni sugli identificatori accettati, visita la [pagina della guida del pubblico con hash di Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Dati esportati / Convalida esportazione dati {#exported-data}

Dopo aver caricato il pubblico, puoi verificare che sia stato creato e caricato correttamente seguendo la procedura riportata di seguito:

**Per Amazon DSP**

Passa a **[!UICONTROL ID inserzionista]** > **[!UICONTROL Tipi di pubblico]** > **[!UICONTROL Tipi di pubblico inserzionista]**. Se il pubblico è stato creato correttamente e soddisfa il numero minimo di membri, verrà visualizzato lo stato `Active`. Ulteriori dettagli sulle dimensioni e sulla portata del pubblico sono disponibili nel pannello Previsioni di portata sul lato destro dell’interfaccia utente di Amazon DSP.

![Convalida della creazione del pubblico di Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Per[!DNL Amazon Marketing Cloud]**

Nel browser dello schema a sinistra, individua il pubblico in **[!UICONTROL Inserzionista caricato]** > **[!UICONTROL aep_audiences]**. Puoi quindi eseguire una query sul pubblico nell’editor SQL AMC con la seguente clausola:

`select count(user_id) from adobeexperienceplatf_audience_view_000xyz where external_audience_segment_name = '1234567'`

![Convalida della creazione del pubblico del Marketing Cloud Amazon](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriore documentazione, visitare le seguenti [!DNL Amazon Ads] risorse della Guida:

* [Centro assistenza DSP Amazon](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti alla documentazione apportati al connettore di destinazione.

+++ Visualizza changelog

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Maggio 2024 | Aggiornamento della funzionalità e della documentazione | È stata aggiunta l&#39;opzione di mappatura per esportare il parametro `countryCode` in Amazon Ads. Utilizza `countryCode` nel [passaggio di mappatura](#map) per migliorare le percentuali di corrispondenza delle identità con Amazon. |
| Marzo 2024 | Aggiornamento della funzionalità e della documentazione | È stata aggiunta l&#39;opzione per esportare i tipi di pubblico da utilizzare in [!DNL Amazon Marketing Cloud] (AMC). |
| Maggio 2023 | Aggiornamento della funzionalità e della documentazione | <ul><li>È stato aggiunto il supporto per la selezione dell&#39;area dell&#39;inserzionista nel [flusso di lavoro della connessione di destinazione](#destination-details).</li><li>È stata aggiornata la documentazione per riflettere l’aggiunta della selezione per Regione inserzionista. Per ulteriori informazioni sulla selezione della regione dell&#39;inserzionista corretta, consulta la [documentazione di Amazon](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Marzo 2023 | Versione iniziale | Versione di destinazione iniziale e documentazione pubblicata. |

{style="table-layout:auto"}

+++
