---
title: Amazon Ads
description: Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori di Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie. L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, incluso Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sull’DSP di Amazon.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: ba768b3148d57e9df12a34f0324c086a17a6d45a
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# Connessione Amazon Ads (Beta) {#amazon-ads}

## Panoramica {#overview}

[!DNL Amazon Ads] offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie.

Il [!DNL Amazon Ads] integrazione con Adobe Experience Platform fornisce integrazione chiavi in mano a [!DNL Amazon Ads] tra cui Amazon DSP (ADSP) e Amazon Marketing Cloud (AMC).

Utilizzo di [!DNL Amazon Ads] destinazione in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sull’DSP di Amazon.  Inoltre, gli utenti possono caricare i propri dati in [!DNL Amazon Marketing Cloud] per comprendere le prestazioni in base al pubblico, l’inserzionista ha fornito dimensioni, appartenenza ai segmenti di Amazon o altri segnali disponibili in AMC. Dopo aver caricato il pubblico degli inserzionisti in AMC, gli utenti possono utilizzare [!DNL Amazon Marketing Cloud] per modificare, migliorare o aggiungere a membri del pubblico utilizzando i segnali di Amazon dall’interno di [!DNL Amazon Marketing Cloud].

AMC riunisce segnali univoci provenienti da tutte le proprietà possedute e gestite da Amazon, che si estendono su diversi tipi di media, tra cui display, video, streaming TV, audio e annunci sponsorizzati. Gli utenti possono inviare facilmente segmenti curati da Adobe Experience Platform ad AMC per migliorare l’apprendimento, ad esempio i gruppi del pubblico sul mercato, le coorti di lifestyle e i modelli di brand engagement. I segmenti aumentati possono quindi essere utilizzati per ottimizzare le attivazioni multimediali nell’DSP di Amazon.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da *[!DNL Amazon Ads]* team. Attualmente si tratta di un prodotto beta la cui funzionalità è soggetta a modifiche. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo *`amc-support@amazon.com`.*

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il *[!DNL Amazon Ads]* destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Attivazione e targeting {#activation-and-targeting}

Questa integrazione con l’DSP di Amazon consente [!DNL Amazon Ads] gli inserzionisti devono trasmettere il pubblico CDP dell’inserzionista da Adobe Experience Platform all’DSP di Amazon per creare il pubblico dell’inserzionista per il targeting pubblicitario. I tipi di pubblico possono essere selezionati nell’DSP di Amazon per il targeting positivo e negativo (soppressione).

### Analytics e misurazione {#analytics-and-measurement}

Questa integrazione con [!DNL Amazon Marketing Cloud] (AMC) consente [!DNL Amazon Ads] agli inserzionisti di trasmettere i segmenti CDP da Adobe Experience Platform Form ad AMC. Gli inserzionisti possono quindi unire gli input di CDP con [!DNL Amazon Ads] e condurre analisi personalizzate su argomenti quali l’impatto dei contenuti multimediali, i segmenti di pubblico e i percorsi di clienti in un formato conforme alla privacy. Ad esempio, un inserzionista può caricare un elenco dei propri clienti esistenti per comprendere le prestazioni aggregate della campagna pubblicitaria, o statistiche aggregate di eventi di conversione su Amazon, come la visualizzazione di una pagina dei dettagli di un prodotto, l’aggiunta di un prodotto a un carrello o l’acquisto di un prodotto.

### Ottimizzazione della pubblicità:

Questa integrazione con [!DNL Amazon Marketing Cloud] (AMC) consente agli inserzionisti di caricare i propri elenchi di clienti e utilizzando [!DNL Amazon Marketing Cloud] SQL, esegui analisi di sovrapposizione, eliminazioni, aggiunte o ottimizzazioni ai tipi di pubblico su base periodica prima di creare un pubblico pronto per l’attivazione nell’DSP di Amazon per il targeting.

## Prerequisiti {#prerequisites}

Per utilizzare [!DNL Amazon Ads] connessione con Adobe Experience Platform, gli utenti devono prima avere accesso a un account Amazon DSP Advertiser (Inserzionista) o a un [!DNL Amazon Marketing Cloud] dell&#39;istanza. Per eseguire il provisioning di queste istanze, visita la pagina seguente nella [!DNL Amazon Ads] sito Web:

* [Introduzione all’DSP di Amazon](https://advertising.amazon.com/solutions/products/amazon-dsp)
* [Introduzione al Marketing Cloud Amazon](https://advertising.amazon.com/solutions/products/amazon-marketing-cloud)

## Identità supportate {#supported-identities}

Il *[!DNL Amazon Ads]* La connessione supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service//features/namespaces.md). Per ulteriori dettagli sulle identità supportate da [!DNL Amazon Ads], visita il [Centro di supporto per l’DSP di Amazon](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati in *[!DNL Amazon Ads]* destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

Sei portato al [!DNL Amazon Ads] interfaccia di connessione in cui selezionare per la prima volta gli account dell&#39;inserzionista a cui si desidera connettersi. Al momento della connessione, verrai reindirizzato a Adobe Experience Platform con una nuova connessione, fornita con l’ID dell’account inserzionista selezionato. Seleziona l’Account dell’inserzionista appropriato nella schermata di configurazione della destinazione per procedere.

* **[!UICONTROL Token Bearer]**: inserisci il token Bearer per l’autenticazione nella destinazione.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Connessione Amazon Ads]**: seleziona l’ID per la destinazione [!DNL Amazon Ads] account utilizzato per la destinazione.

>[!NOTE]
>
>Dopo aver salvato la configurazione di destinazione, non potrai modificare [!DNL Amazon Ads] ID inserzionista, anche se effettui di nuovo l’autenticazione tramite il tuo account Amazon. Per utilizzare un [!DNL Amazon Ads] ID inserzionista, devi creare una nuova connessione di destinazione.

* **[!UICONTROL Area Inserzionista]**: seleziona l’area appropriata in cui è ospitato l’inserzionista. Per ulteriori informazioni sui mercati supportati da ogni area geografica, visita [Documentazione di Amazon Ads](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).



![Configurare una nuova destinazione](../../assets/catalog/advertising/amazon_ads_image_4.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Il [!DNL Amazon Ads] la connessione supporta l’indirizzo e-mail con hash e i numeri di telefono con hash a scopo di corrispondenza delle identità. La schermata seguente fornisce un esempio di corrispondenza compatibile con [!DNL Amazon Ads] connessione:

![Adobe di mappatura di Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Per mappare gli indirizzi e-mail con hash, seleziona la `Email_LC_SHA256` spazio dei nomi dell’identità come campo di origine.
* Per mappare i numeri di telefono con hash, seleziona la `Phone_SHA256` spazio dei nomi dell’identità come campo di origine.
* Per mappare indirizzi e-mail o numeri di telefono senza hash, seleziona gli spazi dei nomi di identità corrispondenti come campi sorgente e seleziona la `Apply Transformation` opzione per fare in modo che Platform esegua l’hashing delle identità al momento dell’attivazione.

È possibile selezionare un determinato campo di destinazione una sola volta in una configurazione di destinazione del [!DNL Amazon Ads] connettore.  Ad esempio, se invii un’e-mail aziendale, non puoi mappare anche l’e-mail personale nella stessa configurazione di destinazione.

Si consiglia vivamente di mappare tutti i campi disponibili. Se è disponibile un solo attributo di origine, è possibile mappare un singolo campo. Il [!DNL Amazon Ads] la destinazione utilizza tutti i campi mappati a scopo di mappatura, ottenendo percentuali di corrispondenza più elevate se vengono forniti più campi. Per ulteriori informazioni sugli identificatori accettati, consulta [Pagina della guida del pubblico con hash di Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Dati esportati / Convalida esportazione dati {#exported-data}

Dopo aver caricato il pubblico, puoi verificare che sia stato creato e caricato correttamente seguendo la procedura riportata di seguito:

**Per Amazon DSP**

Accedi al tuo **[!UICONTROL ID inserzionista]** > **[!UICONTROL Tipi di pubblico]** > **[!UICONTROL Pubblico inserzionista]**. Se il pubblico è stato creato correttamente e soddisfa il numero minimo di membri del pubblico, verrà visualizzato lo stato `Active`. Ulteriori dettagli sulle dimensioni e sulla portata del pubblico sono disponibili nel pannello Previsioni di portata sul lato destro dell’interfaccia utente di Amazon DSP.

![Convalida della creazione di un pubblico Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

**Per[!DNL Amazon Marketing Cloud]**

Nel browser dello schema a sinistra, individua il pubblico in **[!UICONTROL Inserzionista caricato]** > **[!UICONTROL aep_audiences]**. Puoi quindi eseguire una query sul pubblico nell’editor SQL AMC con la seguente clausola:

`select count(user_id) from aep_audiences where audienceId = '1234567'`

![Convalida della creazione di un pubblico di Marketing Cloud Amazon](../../assets/catalog/advertising/amazon_ads_image_5.png)


## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriore documentazione, visita [!DNL Amazon Ads] risorse dell’Aiuto:

* [Centro assistenza DSP di Amazon](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti alla documentazione apportati al connettore di destinazione.

+++ Visualizza changelog

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Marzo 2024 | Aggiornamento della funzionalità e della documentazione | È stata aggiunta l’opzione per esportare i tipi di pubblico da utilizzare in [!DNL Amazon Marketing Cloud] (AMC) |
| Maggio 2023 | Aggiornamento della funzionalità e della documentazione | <ul><li>È stato aggiunto il supporto per la selezione dell’area geografica degli inserzionisti nel [flusso di lavoro di connessione di destinazione](#destination-details).</li><li>È stata aggiornata la documentazione per riflettere l’aggiunta della selezione per Regione inserzionista. Per ulteriori informazioni sulla selezione dell&#39;area dell&#39;inserzionista corretta, vedere [Documentazione di Amazon](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Marzo 2023 | Versione iniziale | Versione di destinazione iniziale e documentazione pubblicata. |

{style="table-layout:auto"}

+++
