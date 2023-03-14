---
title: Configurare l’estensione Adobe Experience Platform Web SDK
description: Configurare l’estensione tag Adobe Experience Platform Web SDK nell’interfaccia utente.
exl-id: 96d32db8-0c9a-49f0-91f3-0244522d66df
source-git-commit: 3ab02646968222c0ad09c1d8ce8fda04de7aaac6
workflow-type: tm+mt
source-wordcount: '1041'
ht-degree: 7%

---

# Configurare l’estensione Adobe Experience Platform Web SDK

L’estensione tag Adobe Experience Platform Web SDK invia i dati a Adobe Experience Cloud dalle proprietà web tramite la rete Edge di Adobe Experience Platform. L’estensione ti consente di inviare in streaming dati a Platform, sincronizzare le identità, elaborare i segnali di consenso dei clienti e raccogliere automaticamente i dati contestuali.

Questo documento illustra come configurare l’estensione nell’interfaccia utente.

## Introduzione

Se l’estensione Platform Web SDK è già stata installata per una proprietà, apri la proprietà nell’interfaccia utente e seleziona la **[!UICONTROL Estensioni]** scheda. In Platform Web SDK, seleziona **[!UICONTROL Configura]**.

![](../assets/extension/overview/configure.png)

Se non hai ancora installato l&#39;estensione, fai clic sul pulsante **[!UICONTROL Catalogo]** scheda. Dall’elenco delle estensioni disponibili, individua l’estensione Platform Web SDK e seleziona **[!UICONTROL Installa]**.

![](../assets/extension/overview/install.png)

In entrambi i casi, si apre la pagina di configurazione per Platform Web SDK. Le sezioni seguenti spiegano le opzioni di configurazione dell&#39;estensione.

![](../assets/extension/overview/config-screen.png)

## Opzioni di configurazione generali

Le opzioni di configurazione nella parte superiore della pagina indicano a Adobe Experience Platform dove instradare i dati e quali configurazioni utilizzare sul server.

### [!UICONTROL Nome]

L&#39;estensione Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Il nome viene utilizzato per inviare dati a più organizzazioni con una configurazione di tag.

Il nome predefinito dell&#39;estensione è &quot;[!DNL alloy]&quot;. Tuttavia, è possibile modificare il nome dell&#39;istanza e inserire un nome oggetto JavaScript valido.

### **[!UICONTROL ID organizzazione IMS]**

Il [!UICONTROL ID organizzazione IMS] è l’organizzazione a cui si desidera inviare i dati in Adobe. Nella maggior parte dei casi, utilizza il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, compila questo campo con il valore della seconda organizzazione a cui desideri inviare i dati.

### **[!UICONTROL Dominio Edge]**

Il [!UICONTROL Dominio Edge] è il dominio da cui l’estensione Adobe Experience Platform invia e riceve i dati. L’Adobe consiglia di utilizzare un dominio di prima parte (CNAME) per questa estensione. Il dominio predefinito di terze parti funziona per gli ambienti di sviluppo ma non è adatto per gli ambienti di produzione. Le istruzioni su come impostare un first party CNAME sono disponibili [qui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=it).

## [!UICONTROL Stream di dati]

Quando viene inviata una richiesta a Adobe Experience Platform Edge Network, viene utilizzato un ID dello stream di dati per fare riferimento alla configurazione lato server. Puoi aggiornare la configurazione senza dover apportare modifiche al codice sul tuo sito web.

Consulta la guida su [flussi di dati](../datastreams/overview.md) per ulteriori informazioni.


## [!UICONTROL Privacy]

![](../assets/extension/overview/privacy.png)

Il [!UICONTROL Privacy] consente di configurare il modo in cui l’SDK gestisce i segnali di consenso degli utenti dal sito web. In particolare, consente di selezionare il livello predefinito di consenso presunto di un utente se non è stata fornita alcuna preferenza di consenso esplicito. Il livello di consenso predefinito non viene salvato nel profilo dell’utente. La tabella seguente suddivide ciò che ogni opzione comporta:

| [!UICONTROL Livello di consenso predefinito] | Descrizione |
| --- | --- |
| [!UICONTROL In] | Raccogli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL Uscita] | Elimina gli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL In sospeso] | Metti in coda eventi che si verificano prima che l’utente fornisca le preferenze di consenso. Quando vengono fornite le preferenze di consenso, gli eventi vengono raccolti o eliminati in base alle preferenze fornite. |
| [!UICONTROL Fornito dall’elemento dati] | Il livello di consenso predefinito è determinato da un elemento dati separato da te definito. Quando utilizzi questa opzione, devi specificare l’elemento dati utilizzando il menu a discesa fornito. |

Utilizzare Out o Pending se si richiede il consenso esplicito dell&#39;utente per le operazioni aziendali.

## [!UICONTROL Identità]

![](../assets/extension/overview/identity.png)

### [!UICONTROL Migrazione di ECID da VisitorAPI]

L’opzione è abilitata per impostazione predefinita. Quando questa funzione è abilitata, l&#39;SDK può leggere i cookie AMCV e s_ecid e impostare il cookie AMCV utilizzato da Visitor.js. Questa funzione è importante durante la migrazione a Adobe Experience Platform Web SDK, in quanto alcune pagine potrebbero usare ancora Visitor.js. Consente all’SDK di continuare a utilizzare lo stesso ECID in modo che gli utenti non vengano identificati come due utenti separati.

### [!UICONTROL Utilizzare i cookie di terze parti]

Questa opzione consente all&#39;SDK di tentare di memorizzare un identificatore utente in un cookie di terze parti. In caso di esito positivo, l’utente viene identificato come un singolo utente mentre si sposta tra più domini, anziché essere identificato come un utente separato su ciascun dominio. Se questa opzione è abilitata, l’SDK potrebbe ancora non essere in grado di memorizzare l’identificatore utente in un cookie di terze parti se il browser non supporta i cookie di terze parti o se è stato configurato dall’utente per non consentire i cookie di terze parti. In questo caso, l’SDK memorizza l’identificatore solo nel dominio di prime parti.

## [!UICONTROL Personalizzazione]

![](../assets/extension/overview/personalization.png)

Se desideri nascondere determinate parti se il tuo sito viene caricato mentre è presente contenuto personalizzato, puoi specificare gli elementi da nascondere nell’editor di stili per il pre-hiding. È quindi possibile copiare il frammento predefinito di pre-hiding fornito e incollarlo all&#39;interno del `<head>`del sito HTML.

## [!UICONTROL Raccolta dati]

![](../assets/extension/overview/data-collection.png)

### [!UICONTROL Funzione callback]

La funzione di callback fornita nell&#39;estensione è denominata anche [`onBeforeEventSend` funzione](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=it) nella libreria. Questa funzione consente di modificare gli eventi a livello globale prima che vengano inviati ad Adobe Edge Network. Per informazioni più dettagliate su come utilizzare questa funzione, consulta [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#modifying-events-globally).

### [!UICONTROL Fai clic su raccolta dati]

L&#39;SDK può raccogliere automaticamente le informazioni sul clic del collegamento. Per impostazione predefinita, questa funzione è abilitata, ma può essere disabilitata utilizzando questa opzione. I collegamenti sono etichettati anche come collegamenti di download se contengono una delle espressioni di download elencate in [!UICONTROL Qualificatore collegamento di download] casella di testo. In questo Adobe vengono forniti alcuni qualificatori predefiniti per i collegamenti di download, che possono essere modificati in qualsiasi momento.

### [!UICONTROL Dati contestuali raccolti automaticamente]

Per impostazione predefinita, l&#39;SDK raccoglie alcuni dati contestuali relativi a dispositivo, web, ambiente e contesto del luogo. Se desideri visualizzare un elenco delle informazioni raccolte dall’Adobe, puoi trovarlo [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=en). Se non desideri che questi dati vengano raccolti o se desideri solo determinate categorie di dati raccolti, puoi modificare queste opzioni.

## [!UICONTROL Impostazioni avanzate]

![](../assets/extension/overview/advanced-settings.png)

### [!UICONTROL Percorso base perimetrale]

Utilizza questo campo se devi modificare il percorso di base utilizzato per interagire con Adobe Edge Network. Questo non dovrebbe richiedere l’aggiornamento, ma nel caso in cui partecipi a una versione beta o alpha, Adobe potrebbe chiederti di modificare questo campo.
