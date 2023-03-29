---
title: Amazon Ads
description: Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori, fornitori di libri, autori Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie. L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, tra cui Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire il pubblico dell’inserzionista per il targeting e l’attivazione sul DSP Amazon.
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 732e6d3d53d983f3390941f4694d2c542d882004
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---


# (Beta) Connessione Amazon Ads {#amazon-ads}

## Panoramica {#overview}

Amazon Ads offre una serie di opzioni per aiutarti a raggiungere i tuoi obiettivi pubblicitari per venditori registrati, fornitori, fornitori di libri, autori Kindle Direct Publishing (KDP), sviluppatori di app e/o agenzie.

L’integrazione di Amazon Ads con Adobe Experience Platform fornisce un’integrazione chiavi in mano ai prodotti Amazon Ads, tra cui Amazon DSP (ADSP). Utilizzando la destinazione Amazon Ads in Adobe Experience Platform, gli utenti possono definire il pubblico dell’inserzionista per il targeting e l’attivazione sul DSP Amazon.

Questa connessione supporta la creazione di tipi di pubblico nei seguenti Marketplace di Amazon: `US`, `CA`, `MX`, `BR`.

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da *Amazon Ads* squadra. Attualmente si tratta di un prodotto beta e la funzionalità è soggetta a modifiche. Per qualsiasi richiesta di informazioni o di aggiornamento, contattali direttamente all&#39;indirizzo *`amc-support@amazon.com`.*

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la *Amazon Ads* destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Attivazione e targeting {#activation-and-targeting}

Questa integrazione con Amazon DSP consente agli inserzionisti Amazon Ads di passare i segmenti CDP degli inserzionisti da Adobe Experience Platform ad Amazon DSP per creare un pubblico degli inserzionisti per il targeting pubblicitario. I tipi di pubblico possono essere selezionati all’interno del DSP Amazon per il targeting positivo, nonché per il targeting negativo (soppressione). Inoltre, utilizzando i segnali generati tramite il Marketing Cloud Amazon, gli inserzionisti possono ottimizzare il pubblico degli inserzionisti, che sincronizzerà le modifiche al pubblico con Amazon DSP.

## Prerequisiti {#prerequisites}

Per utilizzare la connessione Amazon Ads con Adobe Experience Platform, gli utenti devono prima avere accesso a un account Amazon DSP Advertiser.  Per eseguire il provisioning di queste istanze, visita la seguente pagina sul sito web Amazon Ads:

* [Guida introduttiva ad Amazon DSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## Identità supportate {#supported-identities}

La *Amazon Ads* connection supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md). Per maggiori dettagli sulle identità supportate da Amazon Ads, visita la pagina [Centro assistenza Amazon DSP](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| phone_sha256 | Hash dei numeri di telefono con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nel *Amazon Ads* destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

Verrai indirizzato all’interfaccia di connessione di Amazon Ads, dove potrai selezionare gli account dell’inserzionista a cui desideri connetterti.  Al momento della connessione, verrai reindirizzato a Adobe Experience Platform con una nuova connessione, fornita con l’ID dell’account inserzionista selezionato. Seleziona l’account inserzionista appropriato nella schermata di configurazione della destinazione per procedere.

* **[!UICONTROL Token portatore]**: Compila il token portatore per l’autenticazione alla destinazione.

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID inserzionista Amazon Ads]**: Seleziona l’ID per l’account Amazon Ads di destinazione utilizzato per la destinazione.

Nota: dopo aver selezionato questo ID inserzionista di Amazon Ads, dovrai creare una nuova destinazione per modificare questa impostazione. Se autentichi nuovamente le credenziali OAuth e selezioni un nuovo ID inserzionista, le modifiche non verranno applicate.

![Configurare una nuova destinazione](../../assets/catalog/advertising/amazon_ads_image_1.png)

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Mappare attributi e identità {#map}

La connessione Amazon Ads supporta l’indirizzo e-mail con hash e i numeri di telefono con hash a scopo di corrispondenza delle identità.  La schermata seguente fornisce un esempio di corrispondenza compatibile con la connessione Amazon Ads:

![Mappatura di Adobe ad Amazon Ads](../../assets/catalog/advertising/amazon_ads_image_2.png)

* Per mappare gli indirizzi e-mail con hash, seleziona la `Email_LC_SHA256` spazio dei nomi identità come campo di origine.
* Per mappare i numeri di telefono con hash, seleziona la `Phone_SHA256` spazio dei nomi identità come campo di origine.
* Per mappare gli indirizzi e-mail o i numeri di telefono senza hash, seleziona gli spazi dei nomi di identità corrispondenti come campi di origine e controlla il `Apply Transformation` per impostare l’hash di Platform sulle identità al momento dell’attivazione.

È consigliabile mappare tutti i campi disponibili. Se è disponibile un solo attributo di origine, è possibile mappare un singolo campo.  La destinazione Amazon Ads utilizzerà tutti i campi mappati a scopo di mappatura, ottenendo percentuali di corrispondenza più elevate se vengono forniti più campi. Per ulteriori informazioni sugli identificatori accettati, visita il [Pagina della guida di Amazon Ads per tipi di pubblico con hash](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE).

## Esportazione di dati / Convalida esportazione dati {#exported-data}

Una volta caricato il pubblico, puoi verificare che il pubblico sia stato creato e caricato correttamente seguendo i passaggi seguenti:

**Per Amazon DSP**

Passa al tuo ID inserzionista → Tipi di pubblico → Tipi di pubblico inserzionisti. Se il pubblico è stato creato correttamente e soddisfa il numero minimo di membri del pubblico, viene visualizzato lo stato `Active`.  Ulteriori dettagli sulla dimensione e la portata del pubblico sono disponibili nel pannello Reach previsto sul lato destro dell’interfaccia utente di Amazon DSP.

![Convalida per la creazione di un pubblico in Amazon DSP](../../assets/catalog/advertising/amazon_ads_image_3.png)

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriore documentazione di aiuto, visita le seguenti risorse di aiuto di Amazon Ads:

* [Centro assistenza DSP Amazon](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
