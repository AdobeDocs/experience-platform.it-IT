---
title: Configurare l’estensione Adobe Experience Platform Web SDK
description: Come configurare l'estensione tag Adobe Experience Platform Web SDK nell'interfaccia utente.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 6%

---

# Configurare l’estensione Adobe Experience Platform Web SDK

L’estensione tag Adobe Experience Platform Web SDK invia i dati a Adobe Experience Cloud dalle proprietà web tramite Adobe Experience Platform Edge Network. L’estensione ti consente di inviare dati in streaming a Platform, sincronizzare le identità, elaborare i segnali di consenso dei clienti e raccogliere automaticamente i dati contestuali.

Questo documento illustra come configurare l&#39;estensione nell&#39;interfaccia utente di .

## Introduzione

Se l’estensione Platform Web SDK è già stata installata per una proprietà, apri la proprietà nell’interfaccia utente e seleziona la **[!UICONTROL Estensioni]** scheda . In Platform Web SDK, seleziona **[!UICONTROL Configura]**.

![](../images/extension/overview/configure.png)

Se non hai ancora installato l&#39;estensione, seleziona la **[!UICONTROL Catalogo]** scheda . Dall’elenco delle estensioni disponibili, trova l’estensione Platform Web SDK e seleziona **[!UICONTROL Installa]**.

![](../images/extension/overview/install.png)

In entrambi i casi, arrivi alla pagina di configurazione dell’SDK per web di Platform. Le sezioni seguenti illustrano le opzioni di configurazione dell&#39;estensione.

![](../images/extension/overview/config-screen.png)

## Opzioni di configurazione generali

Le opzioni di configurazione nella parte superiore della pagina indicano a Adobe Experience Platform dove indirizzare i dati e quali configurazioni utilizzare sul server.

### [!UICONTROL Nome]

L&#39;estensione Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Il nome viene utilizzato per inviare dati a più organizzazioni con una configurazione di tag.

Il nome dell&#39;estensione viene impostato automaticamente su &quot;[!DNL alloy]&quot;. Tuttavia, è possibile modificare il nome dell&#39;istanza e inserire un nome oggetto JavaScript valido.

### **[!UICONTROL ID organizzazione IMS]**

La [!UICONTROL ID organizzazione IMS] è l’organizzazione a cui si desidera inviare i dati in un Adobe. Nella maggior parte dei casi, utilizza il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, compila questo campo con il valore della seconda organizzazione a cui desideri inviare i dati.

### **[!UICONTROL Dominio Edge]**

La [!UICONTROL Dominio Edge] è il dominio da cui l’estensione Adobe Experience Platform invia e riceve i dati. Adobe consiglia di utilizzare un dominio di prima parte (CNAME) per questa estensione. Il dominio predefinito di terze parti funziona per gli ambienti di sviluppo ma non è adatto per gli ambienti di produzione. Le istruzioni su come impostare un first party CNAME sono disponibili [qui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=it).

## [!UICONTROL Stream di dati]

Quando viene inviata una richiesta a Adobe Experience Platform Edge Network, viene utilizzato un ID di datastream per fare riferimento alla configurazione lato server. Puoi aggiornare la configurazione senza dover apportare modifiche al codice sul sito web.

Consulta la guida su [datastreams](../datastreams/overview.md) per ulteriori informazioni.


## [!UICONTROL Privacy]

![](../images/extension/overview/privacy.png)

La [!UICONTROL Privacy] La sezione ti consente di configurare in che modo l’SDK gestisce i segnali di consenso degli utenti provenienti dal tuo sito web. Nello specifico, ti consente di selezionare il livello di consenso predefinito che si presume di un utente se non è stata fornita alcuna altra preferenza di consenso esplicito. Il livello di consenso predefinito non viene salvato nel profilo dell’utente. La tabella seguente suddivide ciò che ogni opzione comporta:

| [!UICONTROL Livello di consenso predefinito] | Descrizione |
| --- | --- |
| [!UICONTROL In] | Raccogliere eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL Uscita] | Elimina gli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL In sospeso] | Eseguire la coda degli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. Quando vengono fornite le preferenze di consenso, gli eventi vengono raccolti o scartati a seconda delle preferenze fornite. |
| [!UICONTROL Fornito dall’elemento dati] | Il livello di consenso predefinito è determinato da un elemento dati separato definito dall’utente. Quando utilizzi questa opzione, devi specificare l’elemento dati utilizzando il menu a discesa fornito. |

Utilizzare Out o Pending se si richiede un consenso esplicito dell’utente per le operazioni aziendali.

## [!UICONTROL Identità]

![](../images/extension/overview/identity.png)

### [!UICONTROL Migrare ECID da VisitorAPI]

Questa opzione è attivata per impostazione predefinita. Quando questa funzione è abilitata, l’SDK può leggere i cookie AMCV e s_ecid e impostare il cookie AMCV utilizzato da Visitor.js. Questa funzione è importante quando si esegue la migrazione all’SDK Web di Adobe Experience Platform, in quanto alcune pagine potrebbero ancora utilizzare Visitor.js. Consente all’SDK di continuare a utilizzare lo stesso ECID in modo che gli utenti non vengano identificati come due utenti separati.

### [!UICONTROL Utilizzare i cookie di terze parti]

Questa opzione consente all’SDK di tentare di memorizzare un identificatore utente in un cookie di terze parti. In caso di esito positivo, l’utente viene identificato come singolo utente mentre naviga tra più domini, anziché come utente separato in ciascun dominio. Se questa opzione è abilitata, l’SDK potrebbe comunque non essere in grado di memorizzare l’identificatore utente in un cookie di terze parti se il browser non supporta i cookie di terze parti o se è stato configurato dall’utente per non consentire i cookie di terze parti. In questo caso, l’SDK memorizza l’identificatore solo nel dominio di prime parti.

## [!UICONTROL Personalizzazione]

![](../images/extension/overview/personalization.png)

Se desideri nascondere alcune parti del sito durante il caricamento del contenuto personalizzato, puoi specificare gli elementi da nascondere nell’editor di stili di pre-hiding. Puoi quindi copiare il frammento predefinito fornito e incollarlo all’interno del `<head>`elemento del sito HTML.

## [!UICONTROL Raccolta dati]

![](../images/extension/overview/data-collection.png)

### [!UICONTROL Funzione di callback]

La funzione di callback fornita nell&#39;estensione è anche chiamata [`onBeforeEventSend` Funzione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en) nella biblioteca. Questa funzione ti consente di modificare gli eventi a livello globale prima che vengano inviati ad Adobe Edge Network. Informazioni più dettagliate su come utilizzare questa funzione sono disponibili [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Fare clic sulla raccolta dati]

L&#39;SDK può raccogliere automaticamente le informazioni sul clic del collegamento. Per impostazione predefinita, questa funzione è abilitata ma può essere disabilitata utilizzando questa opzione. I collegamenti vengono anche etichettati come collegamenti di download se contengono una delle espressioni di download elencate nella sezione [!UICONTROL Download del qualificatore del collegamento] casella di testo. Adobe offre alcuni qualificatori di collegamento per il download predefiniti, che possono essere modificati in qualsiasi momento.

### [!UICONTROL Dati contestuali raccolti automaticamente]

Per impostazione predefinita, l’SDK raccoglie alcuni dati contestuali relativi a dispositivi, web, ambiente e contesto. Se desideri visualizzare un elenco delle informazioni raccolte dagli Adobi, puoi trovarle [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Se non si desidera raccogliere questi dati o si desidera raccogliere solo determinate categorie di dati, è possibile modificare queste opzioni.

## [!UICONTROL Impostazioni avanzate]

![](../images/extension/overview/advanced-settings.png)

### [!UICONTROL Percorso base bordo]

Utilizza questo campo se devi modificare il percorso di base utilizzato per interagire con Adobe Edge Network. Questo non dovrebbe richiedere l’aggiornamento, ma nel caso in cui partecipi a una versione beta o alfa, in Adobe potrebbe essere richiesto di modificare questo campo.
