---
title: Creare e configurare gli stream di dati
description: Scopri come collegare l’integrazione Web SDK lato client con altri prodotti Adobe e destinazioni di terze parti.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: 9225ecfb32fd005aaf55bbca0e70cd5680cb8d85
workflow-type: tm+mt
source-wordcount: '2789'
ht-degree: 31%

---


# Creare e configurare gli stream di dati

Questo documento descrive i passaggi per la configurazione di uno [stream di dati](./overview.md) nell’interfaccia utente.

## Accedi all&#39;area di lavoro [!UICONTROL Datastreams]

È possibile creare e gestire gli stream di dati nell&#39;interfaccia utente di Data Collection o nell&#39;interfaccia utente di Experience Platform selezionando **[!UICONTROL Datastreams]** nell&#39;area di navigazione a sinistra.

![Scheda Stream di dati nell’interfaccia utente Raccolta dati](assets/configure/datastreams-tab.png)

Nella scheda **[!UICONTROL Datastreams]** viene visualizzato un elenco degli stream di dati esistenti, inclusi il nome descrittivo, l&#39;ID e la data dell&#39;ultima modifica. Per [visualizzarne i dettagli e configurare i servizi](#view-details), selezionare il nome di uno stream di dati.

Per visualizzare altre opzioni per un particolare flusso di dati, selezionare l&#39;icona Altro (**...**). Per aggiornare la [configurazione di base](#configure) per lo stream di dati, selezionare **[!UICONTROL Edit]**. Per rimuovere lo stream di dati, selezionare **[!UICONTROL Delete]**.

![Opzioni per modificare o eliminare uno stream di dati esistente](assets/configure/edit-datastream.png)

## Creare un flusso di dati {#create}

Per creare uno stream di dati, iniziare selezionando **[!UICONTROL New Datastream]**.

![Seleziona nuovo stream di dati](assets/configure/new-datastream-button.png)

Viene visualizzata l’area di lavoro relativa alla creazione dello stream di dati, partendo dal passaggio di configurazione. Da qui, è necessario fornire un nome e una descrizione facoltativa per lo stream di dati.

Se si configura un datastream da utilizzare in Experience Platform e si utilizza anche il Web SDK, è necessario selezionare anche uno schema [XDM (Experience Data Model) basato su eventi](../xdm/classes/experienceevent.md) per rappresentare i dati che si intende acquisire.

![Configurazione di base per uno stream di dati](assets/configure/configure.png)

### Configurare la geolocalizzazione e la ricerca di rete {#geolocation-network-lookup}

Le impostazioni di geolocalizzazione e ricerca di rete consentono di definire il livello di granularità dei dati a livello di rete e geografico che si desidera raccogliere.

Espandere la sezione **[!UICONTROL Geolocation and network lookup]** per configurare le impostazioni descritte di seguito.

![Schermata di configurazione dello stream di dati con le impostazioni di geolocalizzazione e ricerca di rete evidenziate.](assets/configure/geolookup.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Geo Lookup] | Abilita le ricerche di geolocalizzazione per le opzioni selezionate in base all’indirizzo IP del visitatore. Le opzioni disponibili includono: <ul><li>**Paese**: compila `xdm.placeContext.geo.countryCode`</li><li>**Codice postale**: compila `xdm.placeContext.geo.postalCode`</li><li>**Stato/Provincia**: compila `xdm.placeContext.geo.stateProvince`</li><li>**DMA**: compila `xdm.placeContext.geo.dmaID`</li><li>**Città**: popola `xdm.placeContext.geo.city`</li><li>**Latitudine**: compila `xdm.placeContext.geo._schema.latitude`</li><li>**Longitudine**: compila `xdm.placeContext.geo._schema.longitude`</li></ul>Se si seleziona **[!UICONTROL City]**, **[!UICONTROL Latitude]** o **[!UICONTROL Longitude]**, vengono fornite coordinate fino a due punti decimali, indipendentemente dalle altre opzioni selezionate. Questa è considerata granularità a livello di città.<br> <br>Se non si seleziona alcuna opzione, le ricerche di geolocalizzazione vengono disattivate. La geolocalizzazione si verifica prima di [!UICONTROL IP Obfuscation], ovvero non è interessata dall&#39;impostazione [!UICONTROL IP Obfuscation]. |
| [!UICONTROL Network Lookup] | Abilita le ricerche di rete per le opzioni selezionate in base all&#39;indirizzo IP del visitatore. Le opzioni disponibili includono: <ul><li>**Gestore di telefonia mobile**: compila `xdm.environment.carrier`</li><li>**Dominio**: popola `xdm.environment.domain`</li><li>**ISP**: compila `xdm.environment.ISP`</li><li>**Tipo di connessione**: compila `xdm.environment.connectionType`</li></ul> |

Se si abilita uno dei campi sopra indicati per la raccolta dati, assicurarsi di impostare correttamente la proprietà dell&#39;array [`context`](/help/web-sdk/commands/configure/context.md) durante la configurazione del Web SDK.

I campi di ricerca di geolocalizzazione utilizzano la stringa di array `context` `"placeContext"`, mentre i campi di ricerca di rete utilizzano la stringa di array `context` `"environment"`.

Inoltre, accertati che nello schema esista ogni campo XDM desiderato. In caso contrario, puoi aggiungere allo schema il gruppo di campi `Environment Details` fornito da Adobe.

### Configurare la ricerca del dispositivo {#geolocation-device-lookup}

Le impostazioni di **[!UICONTROL Device Lookup]** consentono di selezionare le informazioni specifiche del dispositivo da raccogliere.

Espandere la sezione **[!UICONTROL Device Lookup]** per configurare le impostazioni descritte di seguito.

![Schermata di configurazione dello stream di dati con le impostazioni di ricerca del dispositivo evidenziate.](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>Le impostazioni mostrate nella tabella seguente si escludono a vicenda. Non è possibile selezionare contemporaneamente le informazioni dell&#39;agente utente *e i dati di ricerca dispositivo*.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Keep user agent and client hints headers]** | Seleziona questa opzione per raccogliere solo le informazioni memorizzate nella stringa dell’agente utente. Questa impostazione è selezionata per impostazione predefinita. Popola `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL Use device lookup to collect the following information]** | Seleziona questa opzione se desideri raccogliere una o più delle seguenti informazioni specifiche per il dispositivo: <ul><li>**[!UICONTROL Device]** informazioni:<ul><li>**Produttore dispositivo**: compila `xdm.device.manufacturer`</li><li>**Modello dispositivo**: compila `xdm.device.modelNumber`</li><li>**Nome marketing**: compila `xdm.device.model`</li></ul></li><li>**[!UICONTROL Hardware]** informazioni: <ul><li>**Tipo di hardware**: compila `xdm.device.type`</li><li>**Altezza visualizzazione**: compila `xdm.device.screenHeight`</li><li>**Larghezza visualizzazione**: compila `xdm.device.screenWidth`</li><li>**Profondità colore visualizzazione**: compila `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL Browser]** informazioni: <ul><li>**Fornitore browser**: compila `xdm.environment.browserDetails.vendor`</li><li>**Nome browser**: compila `xdm.environment.browserDetails.name`</li><li>**Versione browser**: compila `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL Operating system]** informazioni: <ul><li>**Fornitore sistema operativo**: compila `xdm.environment.operatingSystemVendor`</li><li>**Nome sistema operativo**: compila `xdm.environment.operatingSystem`</li><li>**Versione sistema operativo**: compila `xdm.environment.operatingSystemVersion`</li></ul></li></ul>Non è possibile raccogliere le informazioni di ricerca del dispositivo insieme all’agente utente e agli hint client. La scelta di raccogliere le informazioni sul dispositivo disattiva la raccolta degli hint dell’agente utente e del client e viceversa. |
| **[!UICONTROL Do not collect any device information]** | Selezionare questa opzione se non si desidera raccogliere informazioni sulla ricerca del dispositivo. Non vengono raccolti dati relativi a dispositivi, hardware, browser, sistema operativo, agenti utente o suggerimenti client. |

Se si abilita uno dei campi sopra indicati per la raccolta dati, assicurarsi di impostare correttamente la proprietà dell&#39;array [`context`](/help/web-sdk/commands/configure/context.md) durante la configurazione del Web SDK.

Le informazioni sul dispositivo e sull&#39;hardware utilizzano la stringa di array `context` `"device"`, mentre le informazioni sul browser e sul sistema operativo utilizzano la stringa di array `context` `"environment"`.

Inoltre, accertati che nello schema esista ogni campo XDM desiderato. In caso contrario, puoi aggiungere allo schema il gruppo di campi `Environment Details` fornito da Adobe.

### Configurare le opzioni avanzate {#advanced-options}

Per visualizzare le opzioni di configurazione avanzate, selezionare **[!UICONTROL Advanced Options]**. Qui puoi configurare impostazioni aggiuntive per lo stream di dati, ad esempio offuscamento dell’IP, cookie dell’ID di prima parte e altro ancora.

![Opzioni di configurazione avanzate](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> L’utente è responsabile di aver ottenuto tutte le autorizzazioni, i consensi, le autorizzazioni e le autorizzazioni necessari in base alle leggi e alle normative applicabili per raccogliere, elaborare e trasmettere dati personali, incluse informazioni precise sulla geolocalizzazione.
> 
> La selezione dell’offuscamento dell’indirizzo IP non influisce sul livello di informazioni di geolocalizzazione derivate dall’indirizzo IP e inviate alle soluzioni Adobe configurate. Le ricerche per geolocalizzazione devono essere limitate o disabilitate separatamente.

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL IP Obfuscation] | Indica il tipo di offuscamento dell’indirizzo IP da applicare allo stream di dati. Qualsiasi elaborazione basata sull’IP del cliente è influenzata dall’impostazione di offuscamento dell’IP. Ciò include tutti i servizi Experience Cloud che ricevono dati dallo stream di dati. L’offuscamento dell’IP avviene prima dell’invio degli eventi a qualsiasi servizio a valle, ad esempio Preparazione dati. <p>Opzioni disponibili:</p> <ul><li>**[!UICONTROL None]**: disabilita l&#39;offuscamento dell&#39;IP. L’indirizzo IP completo dell’utente viene inviato tramite lo stream di dati.</li><li>**[!UICONTROL Partial]**: per gli indirizzi IPv4, offusca l&#39;ultimo ottetto dell&#39;indirizzo IP utente. Per gli indirizzi IPv6, offusca gli ultimi 80 bit dell’indirizzo. <p>Esempi:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Full]**: offusca l&#39;intero indirizzo IP. <p>Esempi:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> Impatto dell’offuscamento dell’IP su altri prodotti Adobe: <ul><li>**Adobe Target**: il livello di flusso di dati [!UICONTROL IP obfuscation] viene applicato prima dell&#39;esecuzione di [!UICONTROL IP obfuscation] in Adobe Target, a tutti gli indirizzi IP presenti nella richiesta. Ad esempio, se l&#39;opzione [!UICONTROL IP obfuscation] a livello di flusso di dati è impostata su **[!UICONTROL Full]** e l&#39;opzione di offuscamento dell&#39;IP di Adobe Target è impostata su **[!UICONTROL Last octet obfuscation]**, Adobe Target riceve un IP completamente offuscato. Se l&#39;opzione [!UICONTROL IP obfuscation] a livello di flusso di dati è impostata su **[!UICONTROL Partial]** e l&#39;opzione di offuscamento dell&#39;IP di Adobe Target è impostata su **[!UICONTROL Full]**, Adobe Target riceve un IP parzialmente offuscato e quindi applica l&#39;offuscamento completo su di esso. L’offuscamento dell’IP di Adobe Target viene gestito indipendentemente dallo stream di dati. Per ulteriori dettagli, consulta la documentazione di Adobe Target sull’[offuscamento dell’indirizzo IP](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/privacy.html) e la [geolocalizzazione](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html).</li><li>**Audience Manager**: l&#39;impostazione [!UICONTROL IP obfuscation] a livello di stream di dati viene applicata prima dell&#39;esecuzione di [!UICONTROL IP obfuscation] in Audience Manager, a tutti gli indirizzi IP presenti nella richiesta. Qualsiasi ricerca di geolocalizzazione eseguita da Audience Manager è influenzata dall&#39;opzione [!UICONTROL IP obfuscation] a livello di flusso di dati. Una ricerca di geolocalizzazione in Audience Manager, basata su un IP completamente offuscato, determina una regione sconosciuta e tutti i segmenti basati sui dati di geolocalizzazione risultanti non vengono realizzati. Per ulteriori informazioni, consulta la documentazione di Audience Manager sull’[offuscamento dell’indirizzo IP](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html).</li><li>**Adobe Analytics**: se l&#39;impostazione di offuscamento dell&#39;IP a livello di flusso di dati è impostata su **[!UICONTROL Full]**, Adobe Analytics considera l&#39;indirizzo IP vuoto. Questo influisce su qualsiasi elaborazione di Analytics che dipende dall’indirizzo IP, come le ricerche di geolocalizzazione e il filtro IP. Affinché Analytics riceva gli indirizzi IP non offuscati o parzialmente offuscati, imposta l’impostazione di offuscamento dell’IP su **[!UICONTROL Partial]** o **[!UICONTROL None]**. Gli indirizzi IP parzialmente offuscati e non offuscati possono essere ulteriormente offuscati all’interno di Analytics. Consulta la [documentazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html?lang=it) di Adobe Analytics per informazioni dettagliate su come abilitare l&#39;offuscamento dell&#39;IP in Analytics. Se l&#39;indirizzo IP è completamente offuscato e l&#39;hit della pagina non ha né un [!DNL ECID] né un [!DNL VisitorID], Analytics rilascia l&#39;hit anziché generare un [ID di fallback](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html?lang=en), che è parzialmente basato sull&#39;indirizzo IP.</li><li>**Adobe Advertising**: quando l&#39;offuscamento dell&#39;IP a livello di stream di dati è impostato su [!UICONTROL Partial] o [!UICONTROL Full], in Advertising DSP le funzionalità e i rapporti geografici (inclusi la misurazione e il retargeting) sono disabilitati, ad eccezione degli annunci TV connessi.</li></ul> |
| [!UICONTROL First Party ID Cookie] | Quando è abilitata, questa impostazione comunica alla rete Edge di fare riferimento a un cookie specificato durante la ricerca di un [ID dispositivo di prime parti](../web-sdk/identity/first-party-device-ids.md), anziché cercare questo valore nella mappa di identità.<br><br>Quando si abilita questa impostazione, è necessario fornire il nome del cookie che deve memorizzare l&#39;ID. |
| [!UICONTROL Third Party ID Sync] | Le sincronizzazioni ID possono essere raggruppate in contenitori per consentire di eseguire diverse sincronizzazioni ID in momenti diversi. Quando è abilitata, questa impostazione consente di specificare quale contenitore di sincronizzazioni ID viene eseguito per tale stream di dati. |
| [!UICONTROL Third Party ID Sync Container ID] | ID numerico del contenitore da utilizzare per la sincronizzazione dell’ID di terze parti. |
| [!UICONTROL Container ID Overrides] | In questa sezione puoi definire altri ID contenitore di sincronizzazione ID di terze parti da utilizzare per sostituire quello predefinito. |
| [!UICONTROL Access Type] | Definisce il tipo di autenticazione accettato dalla rete Edge per lo stream di dati. <ul><li>**[!UICONTROL Mixed Authentication]**: quando questa opzione è selezionata, Edge Network accetta sia le richieste autenticate che quelle non autenticate. Selezionare questa opzione quando si intende utilizzare Web SDK o [Mobile SDK](https://developer.adobe.com/client-sdks/home/) insieme alla [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/). </li><li>**[!UICONTROL Authenticated Only]**: quando questa opzione è selezionata, Edge Network accetta solo le richieste autenticate. Seleziona questa opzione se intendi utilizzare solo l’API di Edge Network e vuoi evitare che le richieste non autenticate vengano elaborate da Edge Network.</li></ul> |
| [!UICONTROL Media Analytics] | Abilita l&#39;elaborazione dei dati di tracciamento streaming per l&#39;integrazione Edge Network tramite SDK Experience Platform o [API Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/getting-started/). Scopri di più su Media Analytics nella [documentazione](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=it). |

Da qui, se stai configurando lo stream di dati per Experience Platform, segui l&#39;esercitazione su [Preparazione per la raccolta dati](./data-prep.md) per mappare i dati a uno schema di eventi Experience Platform prima di tornare a questa guida. In caso contrario, selezionare **[!UICONTROL Save]** e continuare con la sezione successiva.

>[!NOTE]
>
>Dopo aver salvato le modifiche a una configurazione dello stream di dati, attendi fino a 35 minuti affinché le modifiche vengano propagate in Edge Network. Durante questa finestra di propagazione, le richieste possono ancora essere distribuite con la configurazione precedente.

## Visualizzare i dettagli dello stream di dati {#view-details}

Dopo aver configurato un nuovo stream di dati o averne selezionato uno esistente da visualizzare, viene visualizzata la pagina Dettagli dello stream di dati. Qui puoi trovare ulteriori informazioni sullo stream di dati, incluso il relativo ID.

![Pagina dei dettagli dello stream di dati.](assets/configure/view-details.png)

Dalla schermata Dettagli dello stream di dati, puoi [aggiungere servizi](#add-services) per abilitare le funzionalità dei prodotti Adobe Experience Cloud a cui hai accesso. Puoi modificare anche la [configurazione di base](#create) dello stream di dati, aggiornare le relative [regole di mappatura](./data-prep.md), [copiare lo stream di dati](#copy) oppure eliminarlo completamente.

## Aggiungere servizi a uno stream di dati {#add-services}

Nella pagina dei dettagli di un flusso di dati, selezionare **[!UICONTROL Add Service]** per iniziare ad aggiungere i servizi disponibili per tale flusso di dati.

![Seleziona Aggiungi servizio per continuare.](assets/configure/add-service.png)

Nella schermata successiva, utilizza il menu a discesa per selezionare un servizio da configurare per tale stream di dati. In questo elenco vengono visualizzati solo i servizi a cui si ha accesso.

![Selezionare un servizio dall&#39;elenco.](assets/configure/service-selection.png)

Selezionare il servizio desiderato, compilare le opzioni di configurazione visualizzate, quindi selezionare **[!UICONTROL Save]** per aggiungere il servizio allo stream di dati. Tutti i servizi aggiunti vengono visualizzati nella vista Dettagli dello stream di dati.

![Servizi aggiunti a uno stream di dati](assets/configure/services-added.png)

Le sottosezioni seguenti descrivono le opzioni di configurazione per ciascun servizio.

>[!NOTE]
>
>Ogni configurazione del servizio contiene un interruttore **[!UICONTROL Enabled]** che viene attivato automaticamente quando il servizio viene selezionato. Per disabilitare il servizio selezionato per questo flusso di dati, selezionare di nuovo l&#39;interruttore **[!UICONTROL Enabled]**.

### Impostazioni di Adobe Advertising {#advertising}

Questo servizio è necessario per l’integrazione di Adobe Advertising con Customer Journey Analytics.

### Impostazioni di Adobe Analytics {#analytics}

Questo servizio controlla se e il modo in cui i dati vengono inviati ad Adobe Analytics. Vedi [Invio di dati ad Adobe Analytics](/help/web-sdk/use-cases/adobe-analytics.md).

![Impostazioni dello stream di dati di Adobe Analytics.](assets/configure/analytics-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Report Suite ID] | **(Obbligatorio)** L’ID della suite di rapporti di Analytics a cui desideri inviare i dati. Questo ID si trova nell&#39;interfaccia utente di Adobe Analytics in [!UICONTROL Admin] > [!UICONTROL ReportSuites]. Se sono specificate più suite di rapporti, i dati vengono copiati in ogni suite. |
| [!UICONTROL Visitor ID namespace] | (Facoltativo) Lo spazio dei nomi che desideri utilizzare per l&#39;Adobe Analytics [visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=it). Quando si invia un evento con un valore specificato per questo spazio dei nomi, verrà utilizzato automaticamente come `visitorID` in Analytics. |
| [!UICONTROL Report Suite Overrides] | In questa sezione puoi aggiungere altri ID della suite di rapporti da utilizzare in sostituzione di quello predefinito. |

### Impostazioni di Adobe Audience Manager {#audience-manager}

Questo servizio controlla se e il modo in cui i dati vengono inviati ad Adobe Audience Manager. Per inviare dati ad Audience Manager, è sufficiente abilitare questa sezione. Le altre impostazioni sono facoltative, ma consigliate.

![Impostazioni dello stream di dati di Adobe Audience Manager.](assets/configure/audience-manager-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Cookie Destinations Enabled] | Consente all’SDK di condividere informazioni sui segmenti tramite le [destinazioni dei cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html?lang=it) da [!DNL Audience Manager]. |
| [!UICONTROL URL Destinations Enabled] | Consente all’SDK di condividere informazioni sui segmenti tramite le [destinazioni URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html?lang=it) da [!DNL Audience Manager]. |

### Impostazioni di Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Quando abiliti un flusso di dati per Experience Platform, prendi nota della sandbox di Experience Platform che stai utilizzando, come mostrato nella barra multifunzione superiore dell’interfaccia utente.
>
>![Sandbox selezionata](assets/configure/platform-sandbox.png)
>
>In Adobe Experience Platform le sandbox sono partizioni virtuali che consentono di isolare i dati e le implementazioni da parte di altri all’interno dell’organizzazione. Una volta creato uno stream di dati, la relativa sandbox non può essere modificata. Per ulteriori dettagli sul ruolo delle sandbox in Experience Platform, consulta la [documentazione sulle sandbox](../sandboxes/home.md).

Il servizio controlla se e in che modo i dati vengono inviati ad Adobe Experience Platform.

![Impostazioni dello stream di dati di Adobe Experience Platform.](assets/configure/platform-config.png)

| Impostazione | Descrizione |
|---| --- |
| [!UICONTROL Event Dataset] | **(Obbligatorio)** Seleziona il set di dati di Experience Platform a cui verranno trasmessi i dati dell&#39;evento cliente. Lo schema deve utilizzare la [classe XDM ExperienceEvent](../xdm/classes/experienceevent.md). Per aggiungere altri set di dati, selezionare **[!UICONTROL Add Event Dataset]**. |
| [!UICONTROL Profile Dataset] | Seleziona il set di dati di Experience Platform che verrà utilizzato per inviare gli attributi del cliente per **consenso**, **token push** e **area attività utente**. Lo schema deve utilizzare la [classe Profilo XDM individuale](../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Abilita Offer Decisioning per le implementazioni di Web SDK. Per ulteriori dettagli sull&#39;implementazione, consulta la guida sull&#39;[utilizzo di Offer Decisioning con Web SDK](../web-sdk/personalization/offer-decisioning/offer-decisioning-overview.md).<br><br>Per ulteriori informazioni sulle funzionalità di Offer Decisioning, consulta la [documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=it). |
| [!UICONTROL Edge Segmentation] | Abilita la [segmentazione Edge](../segmentation/methods/edge-segmentation.md) per questo flusso di dati. Quando l&#39;API [Web SDK](../web-sdk/home.md) o [Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) invia dati tramite un flusso di dati con segmentazione Edge abilitata, tutte le appartenenze aggiornate al pubblico per il profilo in questione vengono rimandate nella risposta.<br><br>Puoi utilizzare questa opzione in combinazione con **Destinazioni Personalization** per casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva tramite [destinazioni Edge](../destinations/ui/activate-edge-personalization-destinations.md), [Offer Decisioning](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/decisioning/offer-decisioning/get-started-decision/starting-offer-decisioning), [Adobe Target](https://experienceleague.adobe.com/en/docs/target) o [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home) |
| [!UICONTROL Personalization Destinations] | Abilita [Personalization personalizzato](../destinations/catalog/personalization/custom-personalization.md) per questo flusso di dati. Quando l&#39;[API Web SDK](../web-sdk/home.md) o la [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) invia dati tramite un flusso di dati con destinazioni di personalizzazione abilitate, le appartenenze del pubblico e gli attributi di profilo mappati (solo per richieste API Edge Network [autenticate](https://developer.adobe.com/data-collection-apis/docs/api/)) per il profilo in questione vengono rimandati nella risposta. |
| [!UICONTROL Adobe Journey Optimizer] | Abilita [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home) per questo flusso di dati.<br><br>L&#39;abilitazione di questa opzione consente allo stream di dati di restituire contenuto personalizzato da campagne in entrata basate sul Web e sull&#39;app in Adobe Journey Optimizer.<br><br>Questa opzione richiede che il set di dati selezionato utilizzi uno schema che include il **[!UICONTROL Experience Event - Proposition Interactions]** [gruppo di campi](../xdm/ui/resources/schemas.md#add-field-groups). Questo gruppo di campi viene utilizzato per registrare tutte le interazioni dell’utente con le campagne e le esperienze Adobe Journey Optimizer. |

### Impostazioni di Adobe Target {#target}

Questo servizio controlla se e in che modo i dati vengono inviati ad Adobe Target.

![Impostazioni dello stream di dati di Adobe Target.](assets/configure/target-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Property Token] | [!DNL Target] consente ai clienti di controllare le autorizzazioni utilizzando le proprietà. Per ulteriori informazioni sulle proprietà, consulta la guida sulla [configurazione delle autorizzazioni Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=it) riportata nella documentazione di [!DNL Target].<br><br>Il token di proprietà si trova nell&#39;interfaccia utente di Adobe Target in [!UICONTROL Setup] > [!UICONTROL Properties]. |
| [!UICONTROL Target Environment ID] | Gli [ambienti in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=it) consentono di gestire l’implementazione in tutte le fasi di sviluppo. Questa impostazione specifica l’ambiente da utilizzare con questo stream di dati.<br><br>Si consiglia di impostare questo parametro in modo diverso per ogni ambiente di destinazione `dev`, `stage` e `prod`, per semplificare le operazioni. Tuttavia, nel caso in cui gli ambienti di Adobe Target fossero già stati definiti, è possibile utilizzarli. |
| [!UICONTROL Target Third Party ID namespace] | Lo spazio dei nomi delle identità `mbox3rdPartyId` che desideri utilizzare per questo stream di dati. Se si utilizza un&#39;integrazione [!DNL Customer Attributes] con Adobe Target o si utilizza `thirdPartyId` per aggiornare o creare profili tramite [API dei profili Adobe Target](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profiles-api), è necessario fornire un valore dello spazio dei nomi desiderato. È necessario utilizzare questo spazio dei nomi nella sezione `IdentityMap` dello schema XDM per inviare `customerID` o `thirdPartyId` utilizzati nei caricamenti di file degli attributi del cliente o nelle chiamate API per l&#39;aggiornamento del profilo.  Per ulteriori informazioni, consulta la guida sull’[implementazione `mbox3rdPartyId`con Web SDK](../web-sdk/personalization/adobe-target/using-mbox-3rdpartyid.md). |
| [!UICONTROL Property Token Overrides] | In questa sezione puoi definire token di proprietà aggiuntivi da utilizzare per sostituire quello predefinito. |

### [!UICONTROL Event Forwarding] impostazioni

Questo servizio controlla se e in che modo i dati vengono inviati all’[inoltro eventi](../tags/ui/event-forwarding/overview.md).

![Sezione Inoltro eventi della schermata di configurazione dello stream di dati.](assets/configure/event-forwarding-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Launch Property] | **(Obbligatorio)** La proprietà di inoltro degli eventi a cui desideri inviare i dati. |
| [!UICONTROL Launch Environment] | **(Obbligatorio)** L’ambiente all’interno della proprietà selezionata a cui desideri inviare i dati. |

>[!NOTE]
>
>È possibile selezionare **[!UICONTROL Manually enter IDs]** per digitare i nomi delle proprietà e degli ambienti invece di utilizzare i menu a discesa.

## Copiare uno stream di dati {#copy}

Puoi creare una copia di uno stream di dati esistente e modificarne i dettagli in base alle esigenze.

>[!NOTE]
>
>Gli stream di dati possono essere copiati solo all’interno della stessa [sandbox](../sandboxes/home.md). In altre parole, non è possibile copiare uno stream di dati da una sandbox all’altra.

Dalla pagina principale dell&#39;area di lavoro [!UICONTROL Datastreams], selezionare i puntini di sospensione (**....**) per lo stream di dati in questione, quindi selezionare **[!UICONTROL Copy]**.

![Immagine che mostra l&#39;opzione Copia selezionata dalla visualizzazione elenco dello stream di dati.](assets/configure/copy-datastream-list.png)

In alternativa, è possibile selezionare **[!UICONTROL Copy Datastream]** dalla visualizzazione dei dettagli di un determinato flusso di dati.

![Opzione Copia selezionata dalla visualizzazione dei dettagli dello stream di dati.](assets/configure/copy-datastream-details.png)

Viene visualizzata una finestra di dialogo di conferma in cui viene richiesto di fornire un nome univoco per il nuovo stream di dati da creare, insieme ai dettagli sulle opzioni di configurazione che verranno copiate. Al termine, selezionare **[!UICONTROL Copy]**.

![Finestra di dialogo di conferma per la copia di uno stream di dati.](assets/configure/copy-datastream-confirm.png)

La pagina principale dell&#39;area di lavoro [!UICONTROL Datastreams] viene nuovamente visualizzata con il nuovo flusso di dati elencato.

## Passaggi successivi

Questa guida illustra come gestire gli stream di dati nell’interfaccia utente Raccolta dati. Per ulteriori informazioni su come installare e configurare Web SDK dopo la configurazione di uno stream di dati, consulta la [guida end-to-end sulla raccolta dati](../collection/e2e.md#install).
