---
title: Amazon Ads
description: Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori di Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie. L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, incluso Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sull’DSP di Amazon.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---

# Connessione Amazon Ads (Beta) {#amazon-ads}

## Panoramica {#overview}

Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori di libri, autori di Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie.

L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, incluso Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire i tipi di pubblico degli inserzionisti per il targeting e l’attivazione sull’DSP di Amazon.

Questa connessione supporta la creazione di tipi di pubblico nei seguenti Marketplace Amazon: `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da *Amazon Ads* team. Attualmente si tratta di un prodotto beta la cui funzionalità è soggetta a modifiche. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo *`amc-support@amazon.com`.*

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il *Amazon Ads* destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Attivazione e targeting {#activation-and-targeting}

Questa integrazione con l’DSP di Amazon consente agli inserzionisti di Amazon Ads di trasmettere i segmenti CDP dell’inserzionista da Adobe Experience Platform all’DSP di Amazon per creare tipi di pubblico dell’inserzionista per il targeting pubblicitario. I tipi di pubblico possono essere selezionati nell’DSP di Amazon per il targeting positivo e negativo (soppressione). Inoltre, utilizzando i segnali generati dal Marketing Cloud Amazon, gli inserzionisti possono ottimizzare il pubblico degli inserzionisti, sincronizzando le modifiche del pubblico con l&#39;DSP di Amazon.

## Prerequisiti {#prerequisites}

Per utilizzare la connessione Amazon Ads con Adobe Experience Platform, gli utenti devono prima avere accesso a un account Amazon DSP Advertiser (Inserzionista).  Per effettuare il provisioning di queste istanze, visita la seguente pagina sul sito web di Amazon Ads:

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
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati in *Amazon Ads* destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

Verrai indirizzato all’interfaccia di connessione di Amazon Ads dove prima verranno selezionati gli account dell’inserzionista a cui desideri connetterti.  Al momento della connessione, verrai reindirizzato a Adobe Experience Platform con una nuova connessione, fornita con l’ID dell’account inserzionista selezionato. Seleziona l’Account dell’inserzionista appropriato nella schermata di configurazione della destinazione per procedere.

* **[!UICONTROL Token Bearer]**: inserisci il token Bearer per l’autenticazione nella destinazione.

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID inserzionista di Amazon Ads]**: seleziona l’ID per l’account Amazon Ads di destinazione utilizzato per la destinazione.

Nota: dopo aver selezionato questo ID inserzionista di Amazon Ads, dovrai creare una nuova destinazione per modificare questo valore. Se autentichi nuovamente le credenziali OAuth e selezioni un nuovo ID inserzionista, le modifiche non verranno applicate.

![Configurare una nuova destinazione](../../assets/catalog/advertising/amazon_ads_image_1.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

La connessione di Amazon Ads supporta l’indirizzo e-mail con hash e i numeri di telefono con hash a scopo di corrispondenza delle identità.  La schermata seguente fornisce un esempio di corrispondenza compatibile con la connessione Amazon Ads:

![Adobe di mappatura di Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Per mappare gli indirizzi e-mail con hash, seleziona la `Email_LC_SHA256` spazio dei nomi dell’identità come campo di origine.
* Per mappare i numeri di telefono con hash, seleziona la `Phone_SHA256` spazio dei nomi dell’identità come campo di origine.
* Per mappare indirizzi e-mail o numeri di telefono senza hash, seleziona gli spazi dei nomi di identità corrispondenti come campi sorgente e seleziona la `Apply Transformation` opzione per fare in modo che Platform esegua l’hashing delle identità al momento dell’attivazione.

Si consiglia vivamente di mappare tutti i campi disponibili. Se è disponibile un solo attributo di origine, è possibile mappare un singolo campo.  La destinazione di Amazon Ads utilizzerà tutti i campi mappati a scopo di mappatura, ottenendo percentuali di corrispondenza più elevate se vengono forniti più campi. Per ulteriori informazioni sugli identificatori accettati, consulta [Pagina della guida del pubblico con hash di Amazon Ads](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Dati esportati / Convalida esportazione dati {#exported-data}

Dopo aver caricato il pubblico, puoi verificare che sia stato creato e caricato correttamente seguendo la procedura riportata di seguito:

**Per Amazon DSP**

Passa all’ID inserzionista → tipi di pubblico → inserzionisti. Se il pubblico è stato creato correttamente e soddisfa il numero minimo di membri del pubblico, verrà visualizzato lo stato `Active`.  Ulteriori dettagli sulle dimensioni e sulla portata del pubblico sono disponibili nel pannello Previsioni di portata sul lato destro dell’interfaccia utente di Amazon DSP.

![Convalida della creazione di un pubblico Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriore documentazione, consulta le seguenti risorse di aiuto di Amazon Ads:

* [Centro assistenza DSP di Amazon](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
