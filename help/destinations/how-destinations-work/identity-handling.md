---
title: Gestione delle identità nel flusso di lavoro di attivazione delle destinazioni
description: Scopri come viene gestita l’esportazione di identità nel flusso di lavoro di attivazione, a seconda del tipo di destinazione
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 1%

---

# Gestione delle identità nel flusso di lavoro di attivazione delle destinazioni

Questa pagina descrive le particolarità di come le identità vengono esportate in diversi tipi di destinazione e illustra come individuare le identità disponibili per l’esportazione a seconda della destinazione.

>[!TIP]
>
> Per informazioni approfondite sulle identità, i namespace delle identità e le definizioni dei termini relativi all&#39;identità, leggere il [panoramica del servizio identità](/help/identity-service/home.md).

Ogni destinazione nel [catalogo](/help/destinations/catalog/overview.md) è leggermente diverso, quindi non esiste una configurazione adatta a tutte le destinazioni. Tuttavia, esistono alcuni pattern che guidano la configurazione delle destinazioni e i relativi requisiti di identità, come descritto nelle sezioni seguenti.

## Destinazioni basate su file {#file-based}

Per [destinazioni basate su file](/help/destinations/destination-types.md#file-based) (ad esempio [!DNL Amazon S3], SFTP, la maggior parte delle destinazioni di e-mail marketing come [!DNL Adobe Campaign], [!DNL Oracle Eloqua], [!DNL Salesforce Marketing Cloud]), la configurazione dell’identità nella maggior parte delle destinazioni è aperta, il che significa che non è necessario selezionare alcuna identità nella [Seleziona attributi](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes) passaggio del flusso di lavoro di attivazione batch.

Se scegli di aggiungere identità alle esportazioni dei file, tieni presente che solo una singola identità dalla [spazio dei nomi identità](/help/identity-service/ui/identity-graph-viewer.md#access-identity-graph-viewer) può essere selezionato in un’esportazione. Quando selezioni un’identità per l’esportazione, questa viene automaticamente selezionata come [attributo obbligatorio](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes) e [chiave di deduplicazione](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys).

![Un&#39;identità selezionata come attributo obbligatorio e chiave di deduplicazione.](/help/destinations/assets/how-destinations-work/selected-identity.png)

Come soluzione alternativa, puoi aggiungere altre identità all’esportazione se queste sono state acquisite in Experience Platform come attributi. Di seguito è riportato un esempio in cui l’indirizzo e-mail dell’attributo XDM è stato selezionato per l’esportazione, oltre allo spazio dei nomi identità `Phone_E.164`.

![Esempio di attributo dell’indirizzo e-mail selezionato per l’esportazione.](/help/destinations/assets/how-destinations-work/email-selected.png)

## Esportazione di un&#39;identità da una mappa di identità o esportazione di un&#39;identità come attributo XDM - differenze {#identity-map-or-attribute}

Il numero di record esportati può variare a seconda che si selezioni per l’esportazione di identità dalla mappa di identità o di identità che sono state acquisite come attributi in Experience Platform. [Unisci criteri](/help/profile/merge-policies/overview.md) svolge inoltre un ruolo importante nel numero di record che vengono esportati quando selezioni le identità dalla mappa di identità.

Ad esempio, tieni presente che da due set di dati diversi sono disponibili i seguenti frammenti di profilo che verranno uniti in un singolo profilo cliente:

**Frammento di profilo uno**

| Mappa identità | Nome | Cognome | Attributo e-mail |
|---------|----------|---------|--------|
| e-mail1, ID fedeltà1 | John | Doe | e-mail 1 |


**Frammento di profilo due**

| Mappa identità | Nome | Cognome | Attributo e-mail |
|---------|----------|---------|--------|
| email2, ID fedeltà1 | John | Doe | e-mail 2 |

Il profilo unito sarà simile al seguente:

| Mappa identità | Nome | Cognome | Attributo e-mail |
|---------|----------|---------|--------|
| e-mail 1, e-mail 2, ID fedeltà 1 | John | Doe | e-mail 2 |

Il comportamento di esportazione varia a seconda che sia stata selezionata l’opzione `IdentityMap: Email` o `xdm: personalEmail.address` per l&#39;esportazione.

Se un cliente attiva `IdentityMap: Email`, nel file esportato saranno presenti due record, uno per e-mail1 e uno per e-mail2.

Tuttavia, se un cliente attiva `xdm: personalEmail.address`, nel record sarà presente solo email2 , poiché il campo dell’attributo e-mail include solo email2. Queste situazioni possono risolvere diversi casi d’uso in cui puoi attivare tutti gli indirizzi e-mail che hai su file per un cliente o solo l’indirizzo e-mail più recente che hai su file per il cliente.

Il numero di record esportati dipende dai criteri di unione selezionati e dalla selezione di identità o attributi nell’esportazione.

## Destinazioni di streaming basate su API {#streaming-destinations}

[Destinazioni di streaming basate su API](/help/destinations/destination-types.md#streaming-destination) costruito con [Destination SDK](/help/destinations/destination-sdk/overview.md) (ad esempio [!DNL Facebook], [!DNL Google Customer Match], [!DNL Pinterest], [!DNL Braze]e altri) supportano solo ID specifici per l&#39;esportazione. Per informazioni dettagliate sulle identità specifiche che possono essere esportate in ogni destinazione, consulta la sezione *identità supportate* in ogni pagina della documentazione di destinazione (ad esempio, consulta [sezione identità supportate](/help/destinations/catalog/advertising/pinterest.md) in [!DNL Pinterest] pagina di destinazione).

Tieni presente, tuttavia, che hai la flessibilità di utilizzare i dati da [grafici privati](/help/profile/merge-policies/overview.md#id-stitching) o da attributi come identità. Ciò significa che puoi mappare gli attributi XDM sul campo di identità richiesto dalla destinazione. Vedi sotto un esempio per [!DNL Pinterest] destinazione, dove attributo XDM `personalEmail.address` è mappato sul [!DNL Pinterest] identità `pinterest_audience`.

>[!TIP]
>
>Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** ad Experience Platform, aggiungi automaticamente hash ai dati all’attivazione. Ulteriori informazioni sulle **[!UICONTROL Applica trasformazione]** in [esercitazione sull&#39;attivazione delle destinazioni di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md#apply-transformation).

![Esempio di attributo dell&#39;indirizzo e-mail mappato sul campo dell&#39;identità per la destinazione Pinterest.](/help/destinations/assets/how-destinations-work/email-mapped-to-identity.png)

### Destinazioni pubblicitarie basate su integrazioni di cookie di terze parti {#third-party-cookie-destinations}

Destinazioni pubblicitarie basate su cookie di terze parti (ad esempio: [!DNL Google Ads], [!DNL Google Ad Manager], [!DNL Google DV360], [!DNL Bing], [!DNL The Trade Desk]) non richiede ai clienti di selezionare gli ID nel flusso di lavoro di attivazione. Per queste destinazioni, quando imposti un flusso di lavoro di attivazione, Experience Platform cerca automaticamente la tabella di corrispondenza delle identità creata dalla [[!UICONTROL Servizio Experience Cloud ID]](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) ed esporta tutte le identità disponibili per un profilo e supportate dalla destinazione.

Queste destinazioni richiedono una sincronizzazione ID attraverso [!UICONTROL Servizio Experience Cloud ID] o attraverso [!UICONTROL Experience Platform Web SDK].

Se utilizzi [!UICONTROL Experience Platform Web SDK] e l&#39;eredità [!UICONTROL Servizio Experience Cloud ID] non è implementato nella pagina, quindi devi assicurarti che il datastream per il sito web in questione sia abilitato per consentire la sincronizzazione ID di terze parti, come descritto in [configurare la documentazione di datastream](/help/edge/datastreams/configure.md#create).

Durante la configurazione di un datastream come descritto nella documentazione collegata sopra, è necessario assicurarsi che il **[!UICONTROL Sincronizzazione ID di terze parti]** il cursore è abilitato. La maggior parte dei clienti lascerebbe `container_id` campo vuoto (il valore predefinito è 0). È necessario modificare questo valore solo se l’implementazione legacy di Audience Manager utilizzava un ID contenitore specifico (nota, tuttavia, che si tratterebbe della grande minoranza di clienti).

>[!NOTE]
>
>La maggior parte di queste destinazioni pubblicitarie è supportata in Audience Manager (questi tipi di destinazione sono noti, ad Audience Manager, come destinazioni basate su dispositivi. Vedi [elenco di tutte le destinazioni supportate basate su dispositivi nell’Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/device-based/device-based-destinations-list.html?lang=en)). Solo alcuni sono elencati nell&#39;Experience Platform. Per informazioni sulla condivisione di dati tra Experience Platform e Audience Manager, consulta la sezione su [abilitazione della condivisione dei dati da Experience Platform a Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#enable-aep-to-aam-data). Attualmente, non è previsto il supporto di più destinazioni di cookie di terze parti.

## Destinazioni aziendali {#enterprise-destinations}

[Destinazioni aziendali](/help/destinations/destination-types.md#streaming-profile-export) ([!DNL Amazon Kinesis], [!DNL Azure Event Hubs], HTTP API) non richiede ID specifici nell’esportazione dei dati, in quanto sono progettati per i casi d’uso dell’integrazione Enterprise. Tuttavia, se lo desideri, puoi esportare le identità come attributi XDM o dalla mappa di identità. Visualizzare un [esempio di dati esportati nella destinazione HTTP](/help/destinations/catalog/streaming/http-destination.md#exported-data), che include sia `personalEmail.address` Attributo XDM e identità `ECID` e `email_lc_sha256` (indirizzo e-mail con hash) dalla mappa di identità.

## Destinazioni di personalizzazione {#personalization-destinations}

[Destinazioni di personalizzazione (o edge)](/help/destinations/destination-types.md#edge-personalization-destinations) (ad esempio: Adobe Target, [!DNL Custom Personalization]) non richiede alcuna selezione di identità nel flusso di lavoro di attivazione, in quanto l’integrazione è una ricerca di profilo. Il client ([!DNL Target], [!DNL Web SDK]o altri) invia una query al [[!UICONTROL Bordo]](/help/collection/home.md#edge) e raccoglie le informazioni di profilo necessarie per la personalizzazione all’interno del sito.

<!--
![Table with all supported identities](/help/destinations/assets/how-destinations-work/identities-table.png)

-->

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora sai come scoprire quali identità sono supportate o necessarie per le singole destinazioni. Ora è anche possibile sapere come funziona la selezione dell’identità per ciascun tipo di destinazione.

Successivamente, puoi leggere quali [impostazioni di esportazione](/help/destinations/how-destinations-work/destinations-configurations.md) le destinazioni sono comuni tra i tipi di destinazione, che possono essere configurati a livello di destinazione individuale dagli sviluppatori e quali impostazioni possono essere modificate dagli utenti nel flusso di lavoro di attivazione.

Puoi anche controllare tutte le destinazioni disponibili nel [catalogo](/help/destinations/catalog/overview.md).