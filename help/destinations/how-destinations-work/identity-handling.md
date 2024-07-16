---
title: Gestione dell’identità nel flusso di lavoro di attivazione delle destinazioni
description: Scopri come viene gestita l’esportazione delle identità nel flusso di lavoro di attivazione, a seconda del tipo di destinazione
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1163'
ht-degree: 0%

---

# Gestione dell’identità nel flusso di lavoro di attivazione delle destinazioni

Questa pagina descrive le particolarità di come le identità vengono esportate in diversi tipi di destinazione e illustra come trovare le identità disponibili per l’esportazione in base alla destinazione.

>[!TIP]
>
> Per informazioni dettagliate sulle identità, gli spazi dei nomi delle identità e le definizioni dei termini relativi alle identità, leggere la [panoramica del servizio Identity](/help/identity-service/home.md).

Ogni destinazione nel [catalogo](/help/destinations/catalog/overview.md) è leggermente diversa, quindi non esiste una configurazione unica valida per tutte le destinazioni. Tuttavia, esistono alcuni modelli che guidano la configurazione delle destinazioni e dei relativi requisiti di identità, come descritto nelle sezioni seguenti.

## Destinazioni basate su file {#file-based}

Per [destinazioni basate su file](/help/destinations/destination-types.md#file-based) (ad esempio [!DNL Amazon S3], SFTP, la maggior parte delle destinazioni di e-mail marketing come [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), la configurazione dell&#39;identità nella maggior parte di queste destinazioni è aperta, il che significa che non è necessario selezionare alcuna identità nel passaggio [Seleziona attributi](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) del flusso di lavoro di attivazione batch.

Se scegli di aggiungere identità alle esportazioni di file, tieni presente che in un&#39;esportazione è possibile selezionare solo una singola identità dallo spazio dei nomi [identità](/help/identity-service/features/identity-graph-viewer.md#access-identity-graph-viewer). Quando selezioni un&#39;identità per l&#39;esportazione, viene selezionata automaticamente come [attributo obbligatorio](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) e [chiave di deduplicazione](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Identità selezionata come attributo obbligatorio e chiave di deduplicazione.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Come soluzione alternativa, puoi aggiungere più identità all’esportazione se sono state acquisite in Experience Platform come attributi. Di seguito è riportato un esempio in cui l&#39;indirizzo e-mail dell&#39;attributo XDM è stato selezionato per l&#39;esportazione, oltre allo spazio dei nomi identità `Phone_E.164`.

![Esempio di attributo dell&#39;indirizzo e-mail selezionato per l&#39;esportazione.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Esportazione di un’identità da una mappa di identità rispetto all’esportazione di un’identità come attributo XDM: le differenze {#identity-map-or-attribute}

Il numero di record esportati può essere diverso a seconda che vengano selezionate identità di esportazione dalla mappa delle identità o che vengano acquisite come attributi in Experience Platform. [I criteri di unione](/help/profile/merge-policies/overview.md) svolgono anche un ruolo importante nel numero di record che vengono esportati quando si selezionano le identità dalla mappa delle identità.

Ad esempio, considera che da due set di dati diversi, sono presenti i seguenti frammenti di profilo che verranno uniti in un singolo profilo cliente:

**Frammento di profilo uno**

| Mappa identità | Nome | Cognome | Attributo e-mail |
|---------|----------|---------|--------|
| e-mail1, ID fedeltà1 | John | Doe | e-mail 1 |


**Frammento di profilo due**

| Mappa identità | Nome | Cognome | Attributo e-mail |
|---------|----------|---------|--------|
| e-mail2, ID fedeltà1 | John | Doe | e-mail 2 |

Il profilo unito si presenta come segue:

| Mappa identità | Nome | Cognome | Attributo e-mail |
|---------|----------|---------|--------|
| email 1, email2, Loyalty ID1 | John | Doe | e-mail 2 |

Il comportamento di esportazione varia a seconda che sia stato selezionato `IdentityMap: Email` o `xdm: personalEmail.address` per l&#39;esportazione.

Se un cliente attiva `IdentityMap: Email`, ci saranno due record nel file esportato, uno per e-mail1 e un altro per e-mail2.

Tuttavia, se un cliente attiva `xdm: personalEmail.address`, nel record sarà presente solo e-mail2, poiché il campo dell&#39;attributo e-mail include solo e-mail2. Queste situazioni possono riguardare diversi casi d’uso in cui potresti voler attivare tutti gli indirizzi e-mail che hai in archivio per un cliente, o solo l’indirizzo e-mail più recente che hai in archivio per il cliente.

Il ritiro consiste nel fatto che il numero di record esportati dipende dai criteri di unione scelti e dall&#39;eventuale selezione di identità o attributi nell&#39;esportazione.

## Destinazioni di streaming basate su API {#streaming-destinations}

Le [destinazioni di streaming basate su API](/help/destinations/destination-types.md#streaming-destination) compilate con [Destination SDK](/help/destinations/destination-sdk/overview.md) (ad esempio [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze] e altri) supportano solo ID specifici per l&#39;esportazione. Per informazioni dettagliate sulle identità specifiche che possono essere esportate in ogni destinazione, leggere la sezione *identità supportate* in ogni pagina della documentazione di destinazione (ad esempio, vedere la sezione [identità supportate](/help/destinations/catalog/advertising/pinterest.md) nella pagina di destinazione [!DNL Pinterest]).

Si noti, tuttavia, che è possibile utilizzare i dati di [grafici privati](/help/profile/merge-policies/overview.md#id-stitching) o degli attributi come identità. Ciò significa che puoi mappare gli attributi XDM al campo di identità richiesto dalla destinazione. Di seguito è riportato un esempio per la destinazione [!DNL Pinterest], in cui l&#39;attributo XDM `personalEmail.address` è mappato all&#39;identità `pinterest_audience` [!DNL Pinterest] richiesta.

>[!TIP]
>
>Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che Experience Platform esegua automaticamente l&#39;hash dei dati all&#39;attivazione. Ulteriori informazioni sull&#39;opzione **[!UICONTROL Applica trasformazione]** nell&#39;esercitazione di attivazione delle [destinazioni di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Esempio di attributo dell&#39;indirizzo e-mail mappato al campo di identità per la destinazione Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinazioni di Advertising basate su integrazioni di cookie di terze parti {#third-party-cookie-destinations}

Le destinazioni di Advertising che si basano su cookie di terze parti (ad esempio: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) non richiedono ai clienti di selezionare gli ID nel flusso di lavoro di attivazione. Per queste destinazioni, quando si imposta un flusso di lavoro di attivazione, Experience Platform cerca automaticamente la tabella di corrispondenza delle identità creata dal [[!UICONTROL servizio ID Experience Cloud]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) ed esporta tutte le identità disponibili per un profilo e supportate dalla destinazione.

Queste destinazioni richiedono una sincronizzazione ID tramite il [!UICONTROL servizio ID Experience Cloud] o tramite [!UICONTROL Experience Platform Web SDK].

Se si utilizza [!UICONTROL Experience Platform Web SDK] e il servizio legacy [!UICONTROL Experience Cloud ID] non è implementato nella pagina, è necessario assicurarsi che lo stream di dati per il sito Web in questione sia abilitato per consentire la sincronizzazione degli ID di terze parti, come descritto nella [documentazione sulla configurazione dello stream di dati](/help/datastreams/configure.md#create).

Durante la configurazione di uno stream di dati come descritto nella documentazione collegata in precedenza, è necessario assicurarsi che il cursore **[!UICONTROL Sincronizzazione ID di terze parti]** sia abilitato. La maggior parte dei clienti lascia vuoto il campo `container_id` (il valore predefinito è 0). Devi modificare questo valore solo se l’implementazione legacy dell’Audience Manager utilizza un ID contenitore specifico (tieni presente, tuttavia, che si tratterebbe della stragrande minoranza di clienti).

>[!NOTE]
>
>La maggior parte di queste destinazioni pubblicitarie sono supportate in Audience Manager (questi tipi di destinazione sono noti in Audience Manager come destinazioni basate su dispositivi. Visualizza un [elenco di tutte le destinazioni basate su dispositivi supportate in Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html)). Solo alcuni sono elencati nell’Experience Platform. Per informazioni sulla condivisione dei dati tra Experience Platform e Audience Manager, leggere la sezione relativa all&#39;abilitazione della condivisione dei dati da Experience Platform a Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#enable-aep-to-aam-data) in [. Attualmente, non è previsto il supporto di più destinazioni di cookie di terze parti.

## Destinazioni Enterprise {#enterprise-destinations}

[Le destinazioni Enterprise](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], API HTTP) non richiedono ID specifici nell&#39;esportazione dei dati, in quanto sono progettate per casi di utilizzo di integrazione Enterprise. Tuttavia, se lo desideri, puoi esportare le identità come attributi XDM o dalla mappa delle identità. Visualizza un [esempio di dati esportati nella destinazione HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), che include sia l&#39;attributo XDM `personalEmail.address` che le identità `ECID` e `email_lc_sha256` (indirizzo e-mail con hash) dalla mappa delle identità.

## Destinazioni Personalization {#personalization-destinations}

[Le destinazioni Personalization (o edge)](/help/destinations/destination-types.md#edge-personalization-destinations) (ad esempio: Adobe Target, [!DNL Custom Personalization]) non richiedono alcuna selezione di identità nel flusso di lavoro di attivazione, in quanto l&#39;integrazione è una ricerca di profilo. Il client ([!DNL Target], [!DNL Web SDK] o altri) esegue una query su [[!UICONTROL Edge]](/help/collection/home.md#edge) e recupera le informazioni di profilo necessarie per la personalizzazione nel sito.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come individuare le identità supportate o richieste per le singole destinazioni. Ora sai anche come funziona la selezione delle identità per ogni tipo di destinazione.

Quindi, puoi vedere quali [impostazioni di esportazione](/help/destinations/how-destinations-work/destinations-configurations.md) per le destinazioni sono comuni tra i tipi di destinazione, quali possono essere configurate a livello di singola destinazione dagli sviluppatori e quali impostazioni possono essere modificate dagli utenti nel flusso di lavoro di attivazione.

Puoi anche estrarre tutte le destinazioni disponibili nel [catalogo](/help/destinations/catalog/overview.md).
