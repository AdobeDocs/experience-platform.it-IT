---
title: Amazon Ads
description: Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori di Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie. L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, incluso Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sull’DSP di Amazon.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 2%

---

# Connessione Amazon Ads (Beta) {#amazon-ads}

## Panoramica {#overview}

Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori di Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie.

L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, incluso Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sull’DSP di Amazon.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da *Amazon Ads* team. Attualmente si tratta di un prodotto beta la cui funzionalità è soggetta a modifiche. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo *`amc-support@amazon.com`.*

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il *Amazon Ads* destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Attivazione e targeting {#activation-and-targeting}

Questa integrazione con l’DSP di Amazon consente agli inserzionisti di Amazon Ads di trasmettere il pubblico CDP dell’inserzionista da Adobe Experience Platform all’DSP di Amazon per creare il pubblico dell’inserzionista per il targeting pubblicitario. I tipi di pubblico possono essere selezionati nell’DSP di Amazon per il targeting positivo e negativo (soppressione).

## Prerequisiti {#prerequisites}

Per utilizzare la connessione Amazon Ads con Adobe Experience Platform, gli utenti devono prima avere accesso a un account Amazon DSP Advertiser (Inserzionista). Per eseguire il provisioning di queste istanze, visita la pagina seguente sul sito web di Amazon Ads:

* [Introduzione all’DSP di Amazon](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Identità supportate {#supported-identities}

Il *Amazon Ads* La connessione supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md). Per ulteriori dettagli sulle identità supportate da Amazon Ads, visita [Centro di supporto per l’DSP di Amazon](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati in *Amazon Ads* destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

Viene visualizzata l’interfaccia di connessione di Amazon Ads, dove puoi selezionare per la prima volta gli account dell’inserzionista a cui desideri connetterti. Al momento della connessione, verrai reindirizzato a Adobe Experience Platform con una nuova connessione, fornita con l’ID dell’account inserzionista selezionato. Seleziona l’Account dell’inserzionista appropriato nella schermata di configurazione della destinazione per procedere.

* **[!UICONTROL Token Bearer]**: inserisci il token Bearer per l’autenticazione nella destinazione.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID inserzionista di Amazon Ads]**: seleziona l’ID per l’account Amazon Ads di destinazione utilizzato per la destinazione.

>[!NOTE]
>
>Dopo aver salvato la configurazione di destinazione, non potrai modificare l’ID inserzionista di Amazon Ads, anche se esegui di nuovo l’autenticazione tramite il tuo account Amazon. Per utilizzare un diverso ID inserzionista di Amazon Ads, devi creare una nuova connessione di destinazione.

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

La connessione di Amazon Ads supporta l’indirizzo e-mail con hash e i numeri di telefono con hash a scopo di corrispondenza delle identità. La schermata seguente fornisce un esempio di corrispondenza compatibile con la connessione Amazon Ads:

![Adobe di mappatura di Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Per mappare gli indirizzi e-mail con hash, seleziona la `Email_LC_SHA256` spazio dei nomi dell’identità come campo di origine.
* Per mappare i numeri di telefono con hash, seleziona la `Phone_SHA256` spazio dei nomi dell’identità come campo di origine.
* Per mappare indirizzi e-mail o numeri di telefono senza hash, seleziona gli spazi dei nomi di identità corrispondenti come campi sorgente e seleziona la `Apply Transformation` opzione per fare in modo che Platform esegua l’hashing delle identità al momento dell’attivazione.

Si consiglia vivamente di mappare tutti i campi disponibili. Se è disponibile un solo attributo di origine, è possibile mappare un singolo campo. La destinazione di Amazon Ads utilizza tutti i campi mappati a scopo di mappatura, ottenendo percentuali di corrispondenza più elevate se vengono forniti più campi. Per ulteriori informazioni sugli identificatori accettati, consulta [Pagina della guida del pubblico con hash di Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Dati esportati / Convalida esportazione dati {#exported-data}

Dopo aver caricato il pubblico, puoi verificare che sia stato creato e caricato correttamente seguendo la procedura riportata di seguito:

**Per Amazon DSP**

Passa all’ID inserzionista → tipi di pubblico → inserzionisti. Se il pubblico è stato creato correttamente e soddisfa il numero minimo di membri del pubblico, verrà visualizzato lo stato `Active`. Ulteriori dettagli sulle dimensioni e sulla portata del pubblico sono disponibili nel pannello Previsioni di portata sul lato destro dell’interfaccia utente di Amazon DSP.

![Convalida della creazione di un pubblico Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriore documentazione, consulta le seguenti risorse di aiuto di Amazon Ads:

* [Centro assistenza DSP di Amazon](https://www.amazon.com/ap/signin?openid.pape.max_auth_age=28800&amp;openid.return_to=https%3A%2F%2Fadvertising.amazon.com%2Fdsp%2Fhelp%2Fss%2Fen%2Faudiences&amp;openid.identity=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.assoc_handle=amzn_bt_desktop_us&amp;openid.mode=checkid_setup&amp;openid.claimed_id=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0%2Fidentifier_select&amp;openid.ns=http%3A%2F%2Fspecs.openid.net%2Fauth%2F2.0)

## Changelog {#changelog}

Questa sezione acquisisce le funzionalità e i significativi aggiornamenti alla documentazione apportati al connettore di destinazione.

+++ Visualizza changelog

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Maggio 2023 | Aggiornamento della funzionalità e della documentazione | <ul><li>È stato aggiunto il supporto per la selezione dell’area geografica degli inserzionisti nel [flusso di lavoro di connessione di destinazione](#destination-details).</li><li>È stata aggiornata la documentazione per riflettere l’aggiunta della selezione per Regione inserzionista. Per ulteriori informazioni sulla selezione dell&#39;area dell&#39;inserzionista corretta, vedere [Documentazione di Amazon](https://advertising.amazon.com/API/docs/en-us/info/api-overview#api-endpoints).</li></ul> |
| Marzo 2023 | Versione iniziale | Versione di destinazione iniziale e documentazione pubblicata. |

{style="table-layout:auto"}

+++
