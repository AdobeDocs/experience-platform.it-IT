---
title: Creare e configurare gli stream di dati
description: Scopri come collegare l’integrazione Web SDK lato client con altri prodotti Adobe e destinazioni di terze parti.
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: f99370a9bff156b5cf9ecf286a1f8bc09eccc06a
workflow-type: tm+mt
source-wordcount: '2813'
ht-degree: 52%

---


# Creare e configurare gli stream di dati

Questo documento descrive i passaggi per la configurazione di uno [stream di dati](./overview.md) nell’interfaccia utente.

## Accedere all’area di lavoro dello [!UICONTROL stream di dati]

Puoi creare e gestire stream di dati nell’interfaccia utente Raccolta dati o in quella di Experience Platform selezionando **[!UICONTROL Stream di dati]** nel menu di navigazione a sinistra.

![Scheda Stream di dati nell’interfaccia utente Raccolta dati](assets/configure/datastreams-tab.png)

La scheda **[!UICONTROL Stream di dati]** riporta un elenco di stream di dati esistenti, incluso il nome intuitivo, l’ID e la data dell’ultima modifica. Per [visualizzarne i dettagli e configurare i servizi](#view-details), selezionare il nome di uno stream di dati.

Per visualizzare altre opzioni per un particolare flusso di dati, selezionare l&#39;icona Altro (**...**). Per aggiornare la [configurazione di base](#configure) per lo stream di dati, selezionare **[!UICONTROL Modifica]**. Per rimuovere lo stream di dati, selezionare **[!UICONTROL Elimina]**.

![Opzioni per modificare o eliminare uno stream di dati esistente](assets/configure/edit-datastream.png)

## Creare un flusso di dati {#create}

Per creare uno stream di dati, inizia selezionando **[!UICONTROL Nuovo stream di dati]**.

![Seleziona nuovo stream di dati](assets/configure/new-datastream-button.png)

Viene visualizzata l’area di lavoro relativa alla creazione dello stream di dati, partendo dal passaggio di configurazione. Da qui, è necessario fornire un nome e una descrizione facoltativa per lo stream di dati.

Se si configura un datastream da utilizzare in Experience Platform e si utilizza anche Web SDK, è necessario selezionare anche uno schema [Experience Data Model (XDM) basato su eventi](../xdm/classes/experienceevent.md) per rappresentare i dati che si intende acquisire.

![Configurazione di base per uno stream di dati](assets/configure/configure.png)

### Configurare la geolocalizzazione e la ricerca di rete {#geolocation-network-lookup}

Le impostazioni di geolocalizzazione e ricerca di rete consentono di definire il livello di granularità dei dati a livello di rete e geografico che si desidera raccogliere.

Espandi la sezione **[!UICONTROL Geolocalizzazione e ricerca di rete]** per configurare le impostazioni descritte di seguito.

![Schermata di configurazione dello stream di dati con le impostazioni di geolocalizzazione e ricerca di rete evidenziate.](assets/configure/geolookup.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Ricerca geolocalizzazione] | Abilita le ricerche di geolocalizzazione per le opzioni selezionate in base all’indirizzo IP del visitatore. Le opzioni disponibili includono: <ul><li>**Paese**: compila `xdm.placeContext.geo.countryCode`</li><li>**Codice postale**: compila `xdm.placeContext.geo.postalCode`</li><li>**Stato/Provincia**: compila `xdm.placeContext.geo.stateProvince`</li><li>**DMA**: compila `xdm.placeContext.geo.dmaID`</li><li>**Città**: popola `xdm.placeContext.geo.city`</li><li>**Latitudine**: compila `xdm.placeContext.geo._schema.latitude`</li><li>**Longitudine**: compila `xdm.placeContext.geo._schema.longitude`</li></ul>La selezione di **[!UICONTROL Città]**, **[!UICONTROL Latitudine]** o **[!UICONTROL Longitudine]** fornisce coordinate fino a due punti decimali, indipendentemente dalle altre opzioni selezionate. Questa è considerata granularità a livello di città.<br> <br>Se non si seleziona alcuna opzione, le ricerche di geolocalizzazione vengono disattivate. La geolocalizzazione si verifica prima di [!UICONTROL IP Obfuscation], il che significa che non è interessata dall&#39;impostazione [!UICONTROL IP Obfuscation]. |
| [!UICONTROL Ricerca in rete] | Abilita le ricerche di rete per le opzioni selezionate in base all&#39;indirizzo IP del visitatore. Le opzioni disponibili includono: <ul><li>**Gestore**: compila `xdm.environment.carrier`</li><li>**Dominio**: popola `xdm.environment.domain`</li><li>**ISP**: compila `xdm.environment.ISP`</li></ul> |

Se si abilita uno dei campi sopra indicati per la raccolta dati, assicurarsi di impostare correttamente la proprietà dell&#39;array [`context`](/help/web-sdk/commands/configure/context.md) durante la configurazione dell&#39;SDK Web.

I campi di ricerca di geolocalizzazione utilizzano la stringa di array `context` `"placeContext"`, mentre i campi di ricerca di rete utilizzano la stringa di array `context` `"environment"`.

Inoltre, accertati che nello schema esista ogni campo XDM desiderato. In caso contrario, puoi aggiungere allo schema il gruppo di campi `Environment Details` fornito dall&#39;Adobe.

### Configurare la ricerca del dispositivo {#geolocation-device-lookup}

Le impostazioni di **[!UICONTROL Ricerca dispositivi]** consentono di selezionare le informazioni specifiche del dispositivo che si desidera raccogliere.

Espandi la sezione **[!UICONTROL Ricerca dispositivi]** per configurare le impostazioni descritte di seguito.

![Schermata di configurazione dello stream di dati con le impostazioni di ricerca del dispositivo evidenziate.](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>Le impostazioni mostrate nella tabella seguente si escludono a vicenda. Non è possibile selezionare contemporaneamente le informazioni dell&#39;agente utente *e i dati di ricerca dispositivo*.

| Impostazione | Descrizione |
| --- | --- |
| **[!UICONTROL Mantieni intestazioni agente utente e suggerimenti client]** | Seleziona questa opzione per raccogliere solo le informazioni memorizzate nella stringa dell’agente utente. Questa impostazione è selezionata per impostazione predefinita. Popola `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL Utilizzare la ricerca del dispositivo per raccogliere le informazioni seguenti]** | Seleziona questa opzione se desideri raccogliere una o più delle seguenti informazioni specifiche per il dispositivo: <ul><li>**[!UICONTROL Informazioni dispositivo]**:<ul><li>**Produttore dispositivo**: compila `xdm.device.manufacturer`</li><li>**Modello dispositivo**: compila `xdm.device.modelNumber`</li><li>**Nome marketing**: compila `xdm.device.model`</li></ul></li><li>**[!UICONTROL Informazioni hardware]**: <ul><li>**Tipo di hardware**: compila `xdm.device.type`</li><li>**Altezza visualizzazione**: compila `xdm.device.screenHeight`</li><li>**Larghezza visualizzazione**: compila `xdm.device.screenWidth`</li><li>**Profondità colore visualizzazione**: compila `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL Informazioni sul browser]**: <ul><li>**Fornitore browser**: compila `xdm.environment.browserDetails.vendor`</li><li>**Nome browser**: compila `xdm.environment.browserDetails.name`</li><li>**Versione browser**: compila `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL Informazioni sul sistema operativo]**: <ul><li>**Fornitore sistema operativo**: compila `xdm.environment.operatingSystemVendor`</li><li>**Nome sistema operativo**: compila `xdm.environment.operatingSystem`</li><li>**Versione sistema operativo**: compila `xdm.environment.operatingSystemVersion`</li></ul></li></ul>Non è possibile raccogliere le informazioni di ricerca del dispositivo insieme all’agente utente e agli hint client. La scelta di raccogliere le informazioni sul dispositivo disattiva la raccolta degli hint dell’agente utente e del client e viceversa. |
| **[!UICONTROL Non raccogliere informazioni sul dispositivo]** | Selezionare questa opzione se non si desidera raccogliere informazioni sulla ricerca del dispositivo. Non vengono raccolti dati relativi a dispositivi, hardware, browser, sistema operativo, agenti utente o suggerimenti client. |

Se si abilita uno dei campi sopra indicati per la raccolta dati, assicurarsi di impostare correttamente la proprietà dell&#39;array [`context`](/help/web-sdk/commands/configure/context.md) durante la configurazione dell&#39;SDK Web.

Le informazioni sul dispositivo e sull&#39;hardware utilizzano la stringa di array `context` `"device"`, mentre le informazioni sul browser e sul sistema operativo utilizzano la stringa di array `context` `"environment"`.

Inoltre, accertati che nello schema esista ogni campo XDM desiderato. In caso contrario, puoi aggiungere allo schema il gruppo di campi `Environment Details` fornito dall&#39;Adobe.

### Configurare le opzioni avanzate {#@advanced-options}

Per visualizzare le opzioni di configurazione avanzate, selezionare **[!UICONTROL Opzioni avanzate]**. Qui puoi configurare impostazioni aggiuntive per lo stream di dati, ad esempio offuscamento dell’IP, cookie dell’ID di prima parte e altro ancora.

![Opzioni di configurazione avanzate](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> L’utente è responsabile di aver ottenuto tutte le autorizzazioni, i consensi, le autorizzazioni e le autorizzazioni necessari in base alle leggi e alle normative applicabili per raccogliere, elaborare e trasmettere dati personali, incluse informazioni precise sulla geolocalizzazione.
> 
> La selezione dell’offuscamento dell’indirizzo IP non influisce sul livello di informazioni di geolocalizzazione derivate dall’indirizzo IP e inviate alle soluzioni Adobe configurate. Le ricerche per geolocalizzazione devono essere limitate o disabilitate separatamente.

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Offuscamento IP] | Indica il tipo di offuscamento dell’indirizzo IP da applicare allo stream di dati. Qualsiasi elaborazione basata sull’IP del cliente è influenzata dall’impostazione di offuscamento dell’IP. Ciò include tutti i servizi di Experience Cloud che ricevono dati dallo stream di dati. <p>Opzioni disponibili:</p> <ul><li>**[!UICONTROL Nessuno]**: disabilita l’offuscamento dell’indirizzo IP. L’indirizzo IP completo dell’utente viene inviato tramite lo stream di dati.</li><li>**[!UICONTROL Parziale]**: per gli indirizzi IPv4, offusca l’ultimo ottetto dell’indirizzo IP dell’utente. Per gli indirizzi IPv6, offusca gli ultimi 80 bit dell’indirizzo. <p>Esempi:</p> <ul><li>IPv4: `1.2.3.4` -> `1.2.3.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL Completo]**: offusca l’intero indirizzo IP. <p>Esempi:</p> <ul><li>IPv4: `1.2.3.4` -> `0.0.0.0`</li><li>IPv6: `2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> Impatto dell’offuscamento dell’IP su altri prodotti Adobe: <ul><li>**Adobe Target**: l&#39;offuscamento dell&#39;IP a livello di flusso di dati [!UICONTROL IP] viene applicato prima dell&#39;[!UICONTROL offuscamento dell&#39;IP] eseguito in Adobe Target, a tutti gli indirizzi IP presenti nella richiesta. Ad esempio, se l&#39;opzione [!UICONTROL IP obfuscation] a livello di flusso di dati è impostata su **[!UICONTROL Full]** e l&#39;opzione Adobe Target IP obfuscation è impostata su **[!UICONTROL Last octet obfuscation]**, Adobe Target riceve un IP completamente offuscato. Se l&#39;opzione [!UICONTROL IP obfuscation] a livello di flusso di dati è impostata su **[!UICONTROL Partial]** e l&#39;opzione Adobe Target IP obfuscation è impostata su **[!UICONTROL Full]**, Adobe Target riceve un IP parzialmente offuscato e applica l&#39;offuscamento completo su di esso. L’offuscamento dell’IP di Adobe Target viene gestito indipendentemente dallo stream di dati. Per ulteriori dettagli, consulta la documentazione di Adobe Target sull’[offuscamento dell’indirizzo IP](https://experienceleague.adobe.com/docs/target-dev/developer/implementation/privacy/privacy.html) e la [geolocalizzazione](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html).</li><li>**Audience Manager**: l&#39;impostazione [!UICONTROL IP obfuscation] a livello di flusso di dati viene applicata prima dell&#39;[!UICONTROL IP obfuscation] eseguito in Audience Manager a tutti gli indirizzi IP presenti nella richiesta. Qualsiasi ricerca di geolocalizzazione eseguita da Audience Manager è influenzata dall’opzione di [!UICONTROL offuscamento dell’indirizzo IP] a livello di stream di dati. Una ricerca di geolocalizzazione in Audience Manager, basata su un IP completamente offuscato, determina una regione sconosciuta e tutti i segmenti basati sui dati di geolocalizzazione risultanti non vengono realizzati. Per ulteriori informazioni, consulta la documentazione di Audience Manager sull’[offuscamento dell’indirizzo IP](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html).</li><li>**Adobe Analytics**: se l&#39;impostazione di offuscamento dell&#39;IP a livello di flusso di dati è impostata su **[!UICONTROL Full]**, Adobe Analytics considera l&#39;indirizzo IP vuoto. Questo influisce su qualsiasi elaborazione di Analytics che dipende dall’indirizzo IP, come le ricerche di geolocalizzazione e il filtro IP. Affinché Analytics riceva gli indirizzi IP non offuscati o parzialmente offuscati, imposta l&#39;impostazione di offuscamento dell&#39;IP su **[!UICONTROL Parziale]** o **[!UICONTROL Nessuno]**. Gli indirizzi IP parzialmente offuscati e non offuscati possono essere ulteriormente offuscati all’interno di Analytics. Consulta la [documentazione](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html?lang=it) di Adobe Analytics per informazioni dettagliate su come abilitare l&#39;offuscamento dell&#39;IP in Analytics. Se l&#39;indirizzo IP è completamente offuscato e l&#39;hit della pagina non ha né un [!DNL ECID] né un [!DNL VisitorID], Analytics rilascia l&#39;hit anziché generare un [ID di fallback](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-ids.html?lang=en), che è parzialmente basato sull&#39;indirizzo IP.</li></ul> |
| [!UICONTROL ID cookie di prime parti] | Quando è abilitata, questa impostazione comunica alla rete Edge di fare riferimento a un cookie specificato durante la ricerca di un [ID dispositivo di prime parti](../web-sdk/identity/first-party-device-ids.md), anziché cercare questo valore nella mappa di identità.<br><br>Quando si abilita questa impostazione, è necessario fornire il nome del cookie che deve memorizzare l&#39;ID. |
| [!UICONTROL Sincronizzazione ID di terze parti] | Le sincronizzazioni ID possono essere raggruppate in contenitori per consentire di eseguire diverse sincronizzazioni ID in momenti diversi. Quando è abilitata, questa impostazione consente di specificare quale contenitore di sincronizzazioni ID viene eseguito per tale stream di dati. |
| [!UICONTROL ID contenitore sincronizzazione ID di terze parti] | ID numerico del contenitore da utilizzare per la sincronizzazione dell’ID di terze parti. |
| [!UICONTROL Override ID contenitore] | In questa sezione puoi definire altri ID contenitore di sincronizzazione ID di terze parti da utilizzare per sostituire quello predefinito. |
| [!UICONTROL Tipo di accesso] | Definisce il tipo di autenticazione accettato dalla rete Edge per lo stream di dati. <ul><li>**[!UICONTROL Autenticazione mista]**: quando è selezionata questa opzione, la rete Edge accetta sia richieste autenticate che non autenticate. Seleziona questa opzione quando intendi utilizzare Web SDK o l’[SDK Mobile](https://developer.adobe.com/client-sdks/home/), insieme all’[API del server](../server-api/overview.md). </li><li>**[!UICONTROL Solo autenticate]**: quando è selezionata questa opzione, la rete Edge accetta solo richieste autenticate. Seleziona questa opzione quando intendi utilizzare solo l’API del server e desideri impedire l’elaborazione di richieste non autenticate da parte della rete Edge.</li></ul> |
| [!UICONTROL Media Analytics] | Abilita l&#39;elaborazione dei dati di tracciamento streaming per l&#39;integrazione Edge Network tramite SDK Experience Platform o [API Media Edge](https://developer.adobe.com/cja-apis/docs/endpoints/media-edge/getting-started/). Scopri di più su Media Analytics nella [documentazione](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=it). |

Da qui, se stai configurando uno stream di dati per Experience Platform, segui il tutorial sulla [Preparazione dei dati per la raccolta dati](./data-prep.md) per mappare i dati su uno schema di eventi di Platform prima di tornare a questa guida. Diversamente, seleziona **[!UICONTROL Salva]** e passa alla sezione successiva.

## Visualizzare i dettagli dello stream di dati {#view-details}

Dopo aver configurato un nuovo stream di dati o averne selezionato uno esistente da visualizzare, viene visualizzata la pagina Dettagli dello stream di dati. Qui puoi trovare ulteriori informazioni sullo stream di dati, incluso il relativo ID.

![Pagina dei dettagli dello stream di dati.](assets/configure/view-details.png)

Dalla schermata Dettagli dello stream di dati, puoi [aggiungere servizi](#add-services) per attivare le funzionalità dei prodotti Adobe Experience Cloud a cui hai accesso. Puoi modificare anche la [configurazione di base](#create) dello stream di dati, aggiornare le relative [regole di mappatura](./data-prep.md), [copiare lo stream di dati](#copy) oppure eliminarlo completamente.

## Aggiungere servizi a uno stream di dati {#add-services}

Nella pagina dei dettagli di uno stream di dati, seleziona **[!UICONTROL Aggiungi servizio]** per iniziare ad aggiungere i servizi disponibili per lo stream di dati.

![Seleziona Aggiungi servizio per continuare.](assets/configure/add-service.png)

Nella schermata successiva, utilizza il menu a discesa per selezionare un servizio da configurare per tale stream di dati. In questo elenco vengono visualizzati solo i servizi a cui si ha accesso.

![Selezionare un servizio dall&#39;elenco.](assets/configure/service-selection.png)

Seleziona il servizio desiderato, compila le opzioni di configurazione visualizzate e quindi seleziona **[!UICONTROL Salva]** per aggiungere il servizio allo stream di dati. Tutti i servizi aggiunti vengono visualizzati nella vista Dettagli dello stream di dati.

![Servizi aggiunti a uno stream di dati](assets/configure/services-added.png)

Le sottosezioni seguenti descrivono le opzioni di configurazione per ciascun servizio.

>[!NOTE]
>
>Ogni configurazione del servizio contiene un’opzione **[!UICONTROL abilitata]** che si attiva automaticamente quando il servizio viene selezionato. Per disabilitare il servizio selezionato per lo stream di dati, seleziona di nuovo l’opzione **[!UICONTROL abilitata]**.

### Impostazioni di Adobe Analytics {#analytics}

Questo servizio controlla se e il modo in cui i dati vengono inviati ad Adobe Analytics. Vedi [Invio di dati ad Adobe Analytics](/help/web-sdk/use-cases/adobe-analytics.md).

![Impostazioni dello stream di dati di Adobe Analytics.](assets/configure/analytics-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL ID suite di rapporti] | **(Obbligatorio)** L’ID della suite di rapporti di Analytics a cui desideri inviare i dati. Questo ID si trova nell’interfaccia utente di Adobe Analytics in [!UICONTROL Amministrazione] > [!UICONTROL Suite di rapporti]. Se sono specificate più suite di rapporti, i dati vengono copiati in ogni suite. |
| [!UICONTROL Spazio dei nomi ID visitatore] | (Facoltativo) Lo spazio dei nomi che desideri utilizzare per l&#39;Adobe Analytics [visitorID](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/visitorid.html?lang=it). Quando si invia un evento con un valore specificato per questo spazio dei nomi, verrà utilizzato automaticamente come `visitorID` in Analytics. |
| [!UICONTROL Override della suite di rapporti] | In questa sezione puoi aggiungere altri ID della suite di rapporti da utilizzare in sostituzione di quello predefinito. |

### Impostazioni di Adobe Audience Manager {#audience-manager}

Questo servizio controlla se e il modo in cui i dati vengono inviati ad Adobe Audience Manager. Per inviare dati ad Audience Manager, è sufficiente abilitare questa sezione. Le altre impostazioni sono facoltative, ma consigliate.

![Adobe delle impostazioni dello stream di dati di Audience Manager.](assets/configure/audience-manager-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Destinazioni cookie abilitate] | Consente all’SDK di condividere informazioni sui segmenti tramite le [destinazioni dei cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html?lang=it) da [!DNL Audience Manager]. |
| [!UICONTROL Destinazioni URL abilitate] | Consente all’SDK di condividere informazioni sui segmenti tramite le [destinazioni URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html?lang=it) da [!DNL Audience Manager]. |

### Impostazioni di Adobe Experience Platform {#aep}

>[!IMPORTANT]
>
>Quando abiliti uno stream di dati per Platform, prendi nota della sandbox Platform attualmente in uso, come mostrato nella barra multifunzione superiore dell’interfaccia utente.
>
>![Sandbox selezionata](assets/configure/platform-sandbox.png)
>
>In Adobe Experience Platform le sandbox sono partizioni virtuali che consentono di isolare i dati e le implementazioni da parte di altri all’interno dell’organizzazione. Una volta creato uno stream di dati, la relativa sandbox non può essere modificata. Per ulteriori dettagli sul ruolo delle sandbox in Experience Platform, consulta la [documentazione sulle sandbox](../sandboxes/home.md).

Il servizio controlla se e in che modo i dati vengono inviati ad Adobe Experience Platform.

![Impostazioni dello stream di dati di Adobe Experience Platform.](assets/configure/platform-config.png)

| Impostazione | Descrizione |
|---| --- |
| [!UICONTROL Set di dati di evento] | **(Obbligatorio)** Seleziona il set di dati di Platform a cui verranno trasmessi in streaming i dati dell’evento cliente. Lo schema deve utilizzare la [classe XDM ExperienceEvent](../xdm/classes/experienceevent.md). Per aggiungere altri set di dati, seleziona **[!UICONTROL Aggiungi set di dati di evento]**. |
| [!UICONTROL Set di dati di profilo] | Seleziona il set di dati di Platform a cui verranno inviati i dati attributo del cliente. Lo schema deve utilizzare la [classe Profilo XDM individuale](../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Abilita l’Offer decisioning per le implementazioni dell’SDK web. Per ulteriori dettagli sull&#39;implementazione, consulta la guida su [utilizzo di Offer Decisioning con Web SDK](../web-sdk/personalization/offer-decisioning/offer-decisioning-overview.md).<br><br>Per ulteriori informazioni sulle funzionalità di Offer Decisioning, consulta la [documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioning/get-started-decision/starting-offer-decisioning.html?lang=it). |
| [!UICONTROL Segmentazione Edge] | Abilita la [segmentazione Edge](../segmentation/ui/edge-segmentation.md) per questo flusso di dati. Quando [Web SDK](../web-sdk/home.md) o [Edge Network Server API](../server-api/overview.md) invia dati tramite uno stream di dati con segmentazione Edge abilitata, tutte le appartenenze aggiornate al pubblico per il profilo in questione vengono rimandate nella risposta.<br><br>Puoi utilizzare questa opzione in combinazione con **[!UICONTROL Destinazioni Personalization]** per casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva tramite [destinazioni Edge](../destinations/ui/activate-edge-personalization-destinations.md) o [!DNL Offer Decisioning]. |
| [!UICONTROL Destinazioni di personalizzazione] | Quando viene abilitata dopo aver attivato la casella di controllo della [!UICONTROL segmentazione Edge], questa opzione consente allo stream di dati di connettersi alle destinazioni di personalizzazione, ad esempio la [Personalizzazione personalizzata](../destinations/catalog/personalization/custom-personalization.md).<br><br>Per i passaggi specifici sulla [configurazione delle destinazioni di personalizzazione](../destinations/ui/activate-edge-personalization-destinations.md), consulta la documentazione delle destinazioni. |
| [!UICONTROL Adobe Journey Optimizer] | Abilita [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it) per questo flusso di dati. <br><br> L’abilitazione di questa opzione consente allo stream di dati di restituire il contenuto personalizzato da campagne in entrata basate su web e su app in [!DNL Adobe Journey Optimizer]. Questa opzione richiede l’attivazione della [!UICONTROL segmentazione Edge]. Se [!UICONTROL Segmentazione Edge] è deselezionata, questa opzione è disattivata. |

### Impostazioni di Adobe Target {#target}

Questo servizio controlla se e in che modo i dati vengono inviati ad Adobe Target.

![Impostazioni dello stream di dati di Adobe Target.](assets/configure/target-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Token di proprietà] | [!DNL Target] consente ai clienti di controllare le autorizzazioni utilizzando le proprietà. Per ulteriori informazioni sulle proprietà, consulta la guida sulla [configurazione delle autorizzazioni Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=it) riportata nella documentazione di [!DNL Target].<br><br>Il token di proprietà si trova nell’interfaccia utente di Adobe Target in [!UICONTROL Configurazione] >[!UICONTROL Proprietà]. |
| [!UICONTROL ID ambiente di destinazione] | Gli [ambienti in Adobe Target](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=it) consentono di gestire l’implementazione in tutte le fasi di sviluppo. Questa impostazione specifica l’ambiente da utilizzare con questo stream di dati.<br><br>Si consiglia di impostare questo parametro in modo diverso per ogni ambiente di destinazione `dev`, `stage` e `prod`, per semplificare le operazioni. Tuttavia, nel caso in cui gli ambienti di Adobe Target fossero già stati definiti, è possibile utilizzarli. |
| [!UICONTROL ID spazio dei nomi destinazione di terze parti] | Lo spazio dei nomi dell’identità `mbox3rdPartyId` che desideri utilizzare per questo stream di dati. Se si utilizza un&#39;integrazione [!DNL Customer Attributes] con Adobe Target o si utilizza `thirdPartyId` per aggiornare o creare profili tramite [API dei profili Adobe Target](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profiles-api), è necessario fornire un valore dello spazio dei nomi desiderato. È necessario utilizzare questo spazio dei nomi nella sezione `IdentityMap` dello schema XDM per inviare `customerID` o `thirdPartyId` utilizzati nei caricamenti di file degli attributi del cliente o nelle chiamate API per l&#39;aggiornamento del profilo.  Per ulteriori informazioni, consulta la guida sull’[implementazione `mbox3rdPartyId`con Web SDK](../web-sdk/personalization/adobe-target/using-mbox-3rdpartyid.md). |
| [!UICONTROL Override del token di proprietà] | In questa sezione puoi definire token di proprietà aggiuntivi da utilizzare per sostituire quello predefinito. |

### Impostazioni dell’[!UICONTROL Inoltro eventi]

Questo servizio controlla se e in che modo i dati vengono inviati all’[inoltro eventi](../tags/ui/event-forwarding/overview.md).

![Sezione Inoltro eventi della schermata di configurazione dello stream di dati.](assets/configure/event-forwarding-config.png)

| Impostazione | Descrizione |
| --- | --- |
| [!UICONTROL Proprietà Launch] | **(Obbligatorio)** La proprietà di inoltro degli eventi a cui desideri inviare i dati. |
| [!UICONTROL Ambiente Launch] | **(Obbligatorio)** L’ambiente all’interno della proprietà selezionata a cui desideri inviare i dati. |

>[!NOTE]
>
>Puoi selezionare **[!UICONTROL Immetti manualmente gli ID]** per digitare i nomi delle proprietà e degli ambienti anziché utilizzare i menu a discesa.

## Copiare uno stream di dati {#copy}

Puoi creare una copia di uno stream di dati esistente e modificarne i dettagli in base alle esigenze.

>[!NOTE]
>
>Gli stream di dati possono essere copiati solo all’interno della stessa [sandbox](../sandboxes/home.md). In altre parole, non è possibile copiare uno stream di dati da una sandbox all’altra.

Nella pagina principale nell’area di lavoro [!UICONTROL Stream di dati], seleziona i puntini di sospensione (**...**) per lo stream di dati in questione, quindi seleziona **[!UICONTROL Copia]**.

![Immagine che mostra l&#39;opzione Copia selezionata dalla visualizzazione elenco dello stream di dati.](assets/configure/copy-datastream-list.png)

In alternativa, è possibile selezionare **[!UICONTROL Copia stream di dati]** dalla vista dei dettagli di un determinato stream di dati.

![Opzione Copia selezionata dalla visualizzazione dei dettagli dello stream di dati.](assets/configure/copy-datastream-details.png)

Viene visualizzata una finestra di dialogo di conferma in cui viene richiesto di fornire un nome univoco per il nuovo stream di dati da creare, insieme ai dettagli sulle opzioni di configurazione che verranno copiate. Quando è tutto pronto, seleziona **[!UICONTROL Copia]**.

![Finestra di dialogo di conferma per la copia di uno stream di dati.](assets/configure/copy-datastream-confirm.png)

La pagina principale dell’area di lavoro [!UICONTROL Stream di dati] viene nuovamente visualizzata con il nuovo stream di dati elencato.

## Passaggi successivi

Questa guida illustra come gestire gli stream di dati nell’interfaccia utente Raccolta dati. Per ulteriori informazioni su come installare e configurare Web SDK dopo la configurazione di uno stream di dati, consulta la [guida end-to-end sulla raccolta dati](../collection/e2e.md#install).
