---
title: Gestione dell’identità nel flusso di lavoro di attivazione delle destinazioni
description: Scopri come viene gestita l’esportazione delle identità nel flusso di lavoro di attivazione, a seconda del tipo di destinazione
exl-id: f4894a08-c7a9-4d57-a6d3-660c49206d6a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 3%

---

# Gestione dell’identità nel flusso di lavoro di attivazione delle destinazioni

Questa pagina descrive le particolarità di come le identità vengono esportate in diversi tipi di destinazione e illustra come trovare le identità disponibili per l’esportazione in base alla destinazione.

>[!TIP]
>
> Per informazioni complete su identità, spazi dei nomi delle identità e definizioni di termini relativi all’identità, leggi [panoramica del servizio identity](/help/identity-service/home.md).

Ogni destinazione in [catalogo](/help/destinations/catalog/overview.md) è leggermente diverso, quindi non esiste una configurazione unica per tutte le destinazioni. Tuttavia, esistono alcuni modelli che guidano la configurazione delle destinazioni e dei relativi requisiti di identità, come descritto nelle sezioni seguenti.

## Destinazioni basate su file {#file-based}

Per [destinazioni basate su file](/help/destinations/destination-types.md#file-based) (ad esempio [!DNL Amazon S3], SFTP, la maggior parte delle destinazioni del marketing e-mail come [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), l’impostazione dell’identità nella maggior parte di queste destinazioni è aperta, il che significa che non è necessario selezionare alcuna identità nella [Seleziona attributi](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) passaggio del flusso di lavoro di attivazione batch.

Se scegli di aggiungere identità alle esportazioni di file, tieni presente che una sola identità dalla [spazio dei nomi delle identità](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) può essere selezionato in un’esportazione. Quando selezioni un’identità da esportare, questa viene selezionata automaticamente come [attributo obbligatorio](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) e [chiave di deduplicazione](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Un’identità selezionata come attributo obbligatorio e chiave di deduplicazione.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Come soluzione alternativa, puoi aggiungere più identità all’esportazione se sono state acquisite in Experienci Platform come attributi. Di seguito è riportato un esempio in cui l’indirizzo e-mail dell’attributo XDM è stato selezionato per l’esportazione, oltre allo spazio dei nomi dell’identità `Phone_E.164`.

![Esempio di attributo dell’indirizzo e-mail selezionato per l’esportazione.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Esportazione di un’identità da una mappa di identità rispetto all’esportazione di un’identità come attributo XDM: le differenze {#identity-map-or-attribute}

Il numero di record esportati può essere diverso a seconda che vengano selezionate identità di esportazione dalla mappa delle identità o che vengano acquisite come attributi in Experienci Platform. [Criteri di unione](/help/profile/merge-policies/overview.md) svolge anche un ruolo importante nel numero di record che vengono esportati quando selezioni identità da identity map.

Ad esempio, considera che da due set di dati diversi, sono presenti i seguenti frammenti di profilo che verranno uniti in un singolo profilo cliente:

**Frammento di profilo 1**

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

Il comportamento di esportazione varia a seconda che sia selezionato o meno `IdentityMap: Email` o `xdm: personalEmail.address` per l&#39;esportazione.

Se un cliente si attiva `IdentityMap: Email`, nel file esportato saranno presenti due record, uno per e-mail1 e un altro per e-mail2.

Tuttavia, se un cliente attiva `xdm: personalEmail.address`, nel record sarà presente solo e-mail2, poiché il campo dell’attributo e-mail include solo e-mail2. Queste situazioni possono riguardare diversi casi d’uso in cui potresti voler attivare tutti gli indirizzi e-mail che hai in archivio per un cliente, o solo l’indirizzo e-mail più recente che hai in archivio per il cliente.

Il ritiro consiste nel fatto che il numero di record esportati dipende dai criteri di unione scelti e dall&#39;eventuale selezione di identità o attributi nell&#39;esportazione.

## Destinazioni di streaming basate su API {#streaming-destinations}

[Destinazioni di streaming basate su API](/help/destinations/destination-types.md#streaming-destination) creato con [Destination SDK](/help/destinations/destination-sdk/overview.md) (ad esempio [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]e altri) supportano solo ID specifici per l’esportazione. Per informazioni dettagliate sulle identità specifiche che possono essere esportate in ogni destinazione, leggi *identità supportate* in ogni pagina della documentazione di destinazione (ad esempio, consulta la sezione [sezione identità supportate](/help/destinations/catalog/advertising/pinterest.md) nel [!DNL Pinterest] destinazione).

Tuttavia, puoi utilizzare i dati di con la massima flessibilità [grafi privati](/help/profile/merge-policies/overview.md#id-stitching) o da attributi come identità. Ciò significa che puoi mappare gli attributi XDM al campo di identità richiesto dalla destinazione. Di seguito è riportato un esempio per [!DNL Pinterest] destinazione, in cui l’attributo XDM `personalEmail.address` è mappato al necessario [!DNL Pinterest] identità `pinterest_audience`.

>[!TIP]
>
>Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** affinché Experienci Platform esegua automaticamente l’hash dei dati all’attivazione. Ulteriori informazioni su **[!UICONTROL Applica trasformazione]** opzione in [tutorial sull’attivazione di destinazioni di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Esempio di attributo dell’indirizzo e-mail mappato al campo di identità per la destinazione Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinazioni pubblicitarie basate su integrazioni di cookie di terze parti {#third-party-cookie-destinations}

Destinazioni pubblicitarie che si basano su cookie di terze parti (ad esempio: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) non richiedono ai clienti di selezionare gli ID nel flusso di lavoro di attivazione. Per queste destinazioni, quando si imposta un flusso di lavoro di attivazione, Experienci Platform cerca automaticamente la tabella di corrispondenza delle identità creata da [[!UICONTROL Servizio ID Experience Cloud]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) ed esporta tutte le identità disponibili per un profilo e supportate dalla destinazione.

Queste destinazioni richiedono una sincronizzazione ID tramite [!UICONTROL Servizio ID Experience Cloud] o attraverso [!UICONTROL Experienci Platform Web SDK].

Se sta usando [!UICONTROL Experienci Platform Web SDK] e le versioni precedenti [!UICONTROL Servizio ID Experience Cloud] non è implementato nella pagina, quindi devi assicurarti che lo stream di dati per il sito web in questione sia abilitato per consentire la sincronizzazione degli ID di terze parti, come descritto nella [configurare la documentazione dello stream di dati](/help/datastreams/configure.md#create).

Quando configuri un flusso di dati come descritto nella documentazione collegata in precedenza, è necessario assicurarsi che il **[!UICONTROL Sincronizzazione ID di terze parti]** cursore attivato. La maggior parte dei clienti lascia il `container_id` campo vuoto (il valore predefinito è 0). Devi modificare questo valore solo se l’implementazione legacy dell’Audience Manager utilizza un ID contenitore specifico (tieni presente, tuttavia, che si tratterebbe della stragrande minoranza di clienti).

>[!NOTE]
>
>La maggior parte di queste destinazioni pubblicitarie sono supportate in Audienci Manager (questi tipi di destinazione sono noti in Audienci Manager come destinazioni basate su dispositivi. Vedi un [elenco di tutte le destinazioni basate su dispositivi supportate in Audienci Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html)). Solo alcuni sono elencati nell’Experience Platform. Per informazioni sulla condivisione dei dati tra Experience Platform e Audience Manager, consulta la sezione su [abilitazione della condivisione dei dati da Experienci Platform a Audienci Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#enable-aep-to-aam-data). Attualmente, non è previsto il supporto di più destinazioni di cookie di terze parti.

## Destinazioni Enterprise {#enterprise-destinations}

[Destinazioni Enterprise](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], API HTTP) non richiedono ID specifici nell’esportazione dei dati, in quanto sono progettati per i casi di utilizzo di integrazione Enterprise. Tuttavia, se lo desideri, puoi esportare le identità come attributi XDM o dalla mappa delle identità. Visualizza un [esempio di dati esportati nella destinazione HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), che include sia `personalEmail.address` Attributo XDM e identità `ECID` e `email_lc_sha256` (indirizzo e-mail con hash) dalla mappa delle identità.

## Destinazioni di personalizzazione {#personalization-destinations}

[Destinazioni di personalizzazione (o edge)](/help/destinations/destination-types.md#edge-personalization-destinations) (ad esempio: Adobe Target, [!DNL Custom Personalization]) non richiedono alcuna selezione di identità nel flusso di lavoro di attivazione, in quanto l’integrazione è una ricerca di profilo. Il client ([!DNL Target], [!DNL Web SDK], o altri) esegue query su [[!UICONTROL Bordo]](/help/collection/home.md#edge) e richiama le informazioni di profilo necessarie per la personalizzazione nel sito.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come individuare le identità supportate o richieste per le singole destinazioni. Ora sai anche come funziona la selezione delle identità per ogni tipo di destinazione.

Quindi, puoi leggere quali [impostazioni di esportazione](/help/destinations/how-destinations-work/destinations-configurations.md) per le destinazioni, sono comuni tra i tipi di destinazione, che possono essere configurate a livello di singola destinazione dagli sviluppatori e quali impostazioni possono essere modificate dagli utenti nel flusso di lavoro di attivazione.

Puoi anche consultare tutte le destinazioni disponibili in [catalogo](/help/destinations/catalog/overview.md).
