---
title: Scambio indice
description: Connettiti a Index Exchange (Index) e attiva i dati in modo che i segmenti di pubblico possano essere targetizzati da offerte create nell’interfaccia utente dell’indice.
source-git-commit: 4ecd3b60a6b45a94285785049fd4dee99d7c9bdf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 2%

---


# [!DNL Index Exchange] {#index-exchange}

## Panoramica {#overview}

[!DNL Index] è una piattaforma pubblicitaria globale lato offerta che consente ai proprietari di contenuti multimediali di massimizzare il valore dei contenuti su ogni schermo. Con oltre 20 anni di leadership nel settore, [!DNL Index] mette in contatto i marchi più grandi del mondo con i più importanti produttori di esperienze per offrire esperienze consumer di alta qualità.

Utilizza questo connettore di destinazione per esportare segmenti di pubblico da Adobe Experience Platform direttamente nella piattaforma di pubblicità programmatica di [!DNL Index Exchange].

Una volta esportati, questi segmenti di pubblico possono essere utilizzati per eseguire il targeting delle offerte da parte di proprietari di contenuti multimediali, partner di marketplace o condivisi con editori e curatori dai fornitori di marketplace.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Index]. Per domande o richieste di aggiornamento, contattale direttamente all&#39;indirizzo [technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com).

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Index Exchange], ecco alcuni esempi di casi d&#39;uso che i clienti di Experience Platform possono risolvere utilizzando questa destinazione.

### Targeting degli utenti su piattaforme mobili, web e CTV {#targeting-users}

Proprietari di contenuti multimediali, partner di marketplace o fornitori di marketplace che desiderano inviare tipi di pubblico da Experience Platform a [!DNL Index] per il targeting degli utenti su piattaforme mobili, web e CTV, utilizzando un&#39;ampia gamma di identificatori.

### Targeting di contenuti specifici su piattaforme mobili, web e CTV {#targeting-content}

Proprietari di contenuti multimediali, partner di marketplace o fornitori di marketplace che desiderano inviare tipi di pubblico da Experience Platform a [!DNL Index] per indirizzare l&#39;attività agli utenti che esaminano contenuti specifici per piattaforme mobili, web e CTV utilizzando URL specifici, bundle di app o ID di contenuti.

## Prerequisiti {#prerequisites}

I segmenti di pubblico devono essere registrati con [!DNL Index] utilizzando un processo aggiuntivo quando si utilizza questa destinazione prima che vengano visualizzati nel tuo account. Rivolgiti al rappresentante del tuo account [!DNL Index Exchange] per assistenza su questo processo.

## Identità supportate {#supported-identities}

[!DNL Index] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

[!DNL Index Exchange] destinazioni supportano un solo tipo di identità per caricamento. È necessario specificare il tipo di identificatore appropriato durante la configurazione dei dettagli della destinazione (vedere la sezione [&quot;Compila dettagli destinazione&quot;](#destination-details) di seguito).

Per caricare più tipi di identità, creare istanze separate della destinazione [!DNL Index Exchange] per ogni tipo di identità.

| Identità di destinazione | Descrizione | Considerazioni |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | Se l’identità di origine è uno spazio dei nomi GAID, seleziona GAID come identità di destinazione. |
| IDFA | Apple ID per inserzionisti | Se l&#39;identità di origine è uno spazio dei nomi IDFA, selezionare l&#39;identità di destinazione IDFA. |
| AID di Windows | ID Advertising di Windows | Se l&#39;identità di origine è uno spazio dei nomi di Windows AID, selezionare l&#39;identità di destinazione di Windows AID. |
| extern_id | ID utente personalizzati | Se l’identità di origine è uno spazio dei nomi personalizzato, seleziona questa identità di destinazione. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione spiega quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/overview.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
| --------- | ---------- | --------- | 
| Tipo di esportazione | **[!UICONTROL Segment export]** | Esporta tutti i membri di un segmento (pubblico) con gli identificatori (IDFA, GAID o altri) utilizzati nella destinazione [!DNL Index Exchange]. |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Esporta i file nelle piattaforme a valle a intervalli di 3, 6, 8, 12 o 24 ore. Ulteriori informazioni sulle [destinazioni basate su file batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione di controllo di accesso **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Dettagli destinazione](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]: immettere un nome per consentire il riconoscimento della destinazione in un secondo momento.
* [!UICONTROL Description]: immettere una descrizione per identificare la destinazione in seguito.
* [!UICONTROL Identifier Type]: selezionare il tipo di identificatore fornito dall&#39;indice che corrisponde all&#39;identificatore che si sta inviando a [!DNL Index]. Consulta la tabella dei tipi di identificatori supportati di seguito. Se non si è sicuri del tipo di identificatore da utilizzare, contattare il rappresentante [!DNL Index]. Per inviare più tipi di identificatori, crea istanze separate di questa destinazione.
* [!UICONTROL Account ID]: immetti l&#39;ID account [!DNL Index]. Questo non corrisponde all’ID dell’editore. Se non sei sicuro dell&#39;ID da utilizzare, contatta il tuo rappresentante [!DNL Index].

#### Tipi di identificatori supportati

| Tipo di identificatore | Descrizione |
|------------------ | ------------- |
| [!DNL appbundle] | Bundle per app mobile |
| [!DNL contentid] | ID contenuto |
| [!DNL deviceid] | ID dispositivo (es. IDFA, GAID, WAID, ecc.) |
| [!DNL ip] | Indirizzo IP |
| [!DNL postcode] | CAP |
| [!DNL url] | URL sito |
| [!DNL ppid_xxx] | Per gli identificatori PPID, rivolgiti al rappresentante del tuo account [!DNL Index Exchange] per assistenza. |

{style="table-layout:auto"}

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso questa destinazione. Seleziona uno o più avvisi dall’elenco per abbonarti alle notifiche di stato per il flusso di dati. Per ulteriori informazioni, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).
Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione di segmenti di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](/help/destinations/ui/activate-batch-profile-destinations.md).

### Mappare attributi e identità {#map}

Selezione dei campi di origine:

* Seleziona un identificatore (in genere spazi dei nomi come IDFA o uno spazio dei nomi ID personalizzato). Deve corrispondere al tipo di identificatore selezionato durante la configurazione della destinazione. Ad esempio, quando si utilizza l’identificatore IDFA come campo di origine, la destinazione deve essere stata impostata con il tipo di identificatore &quot;deviceid&quot;.

Selezione dei campi di destinazione:

* I nomi dei campi di destinazione vengono ignorati e non sono importanti. La destinazione si preoccupa solo del tipo di identificatore inviato, che è determinato dal tipo di identificatore selezionato durante la configurazione della destinazione.

![Mappa attributi e identità](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### Registra segmenti con [!DNL Index] {#register-segments}

Prima o dopo l&#39;attivazione dei dati nella destinazione, contattare il rappresentante [!DNL Index] per registrare i segmenti che si intende attivare. Il tuo rappresentante fornirà istruzioni su come registrare ulteriori dettagli del segmento, inclusi nomi, ID, descrizioni e prezzi, se applicabili.

## Dati esportati / Convalida esportazione dati {#exported-data}

Una volta completata la registrazione, i segmenti saranno disponibili per il targeting nel tuo account [!DNL Index]. Per verificare che i dati vengano ricevuti correttamente, contattare il rappresentante [!DNL Index], che può fornire dettagli sul volume di dati del segmento ricevuti.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni di Experience Platform sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come Experience Platform applica la governance dei dati, consulta la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
