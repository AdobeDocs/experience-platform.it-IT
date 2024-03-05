---
title: Configurare l’estensione tag Web SDK
description: Scopri come configurare l’estensione tag Experienci Platform Web SDK nell’interfaccia utente Tag.
exl-id: 22425daa-10bd-4f06-92de-dff9f48ef16e
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 6%

---

# Configurare l’estensione tag Web SDK

Il [!DNL Web SDK] L’estensione tag invia i dati a Adobe Experience Cloud dalle proprietà web tramite Experienci Platform Edge Network.

L’estensione ti consente di inviare in streaming dati a Platform, sincronizzare le identità, elaborare i segnali di consenso dei clienti e raccogliere automaticamente i dati contestuali.

Questo documento spiega come configurare l’estensione tag nell’interfaccia utente Tag.

## Installare l’estensione tag Web SDK {#install}

L&#39;estensione tag Web SDK richiede una proprietà in cui installare. Se non lo hai già fatto, consulta la documentazione su [creazione di una proprietà tag](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html?lang=it).

Dopo aver creato una proprietà, aprila e seleziona la **[!UICONTROL Estensioni]** sulla barra laterale sinistra.

Seleziona la **[!UICONTROL Catalogo]** scheda. Dall’elenco delle estensioni disponibili, individua [!DNL Web SDK] e seleziona **[!UICONTROL Installa]**.

![Immagine che mostra l’interfaccia utente Tag con l’estensione Web SDK selezionata](assets/web-sdk-install.png)

Dopo aver selezionato **[!UICONTROL Installa]**, è necessario configurare l’estensione tag Web SDK e salvare la configurazione.

>[!NOTE]
>
>L’estensione tag viene installata solo dopo il salvataggio della configurazione. Consulta le sezioni successive per scoprire come configurare l’estensione tag.

## Configurare le impostazioni delle istanze {#general}

Le opzioni di configurazione nella parte superiore della pagina indicano a Adobe Experience Platform dove instradare i dati e quali configurazioni utilizzare sul server.

![Immagine che mostra le impostazioni generali dell’estensione tag Web SDK nell’interfaccia utente Tag](assets/web-sdk-ext-general.png)

* **[!UICONTROL Nome]**: l’estensione Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Il nome viene utilizzato per inviare dati a più organizzazioni con una configurazione di tag. Il nome dell&#39;istanza viene impostato automaticamente su `alloy`. Tuttavia, puoi modificare il nome dell’istanza con qualsiasi nome di oggetto JavaScript valido.
* **[!UICONTROL ID organizzazione IMS]**: ID dell’organizzazione a cui si desidera inviare i dati in Adobe. Nella maggior parte dei casi, utilizza il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, compila questo campo con il valore della seconda organizzazione a cui desideri inviare i dati.
* **[!UICONTROL Dominio Edge]**: dominio da cui l’estensione invia e riceve i dati. L’Adobe consiglia di utilizzare un dominio di prima parte (CNAME) per questa estensione. Il dominio predefinito di terze parti funziona per gli ambienti di sviluppo ma non è adatto per gli ambienti di produzione. Le istruzioni su come impostare un first party CNAME sono disponibili [qui](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html?lang=it).

## Configurare le impostazioni dello stream di dati {#datastreams}

Questa sezione consente di selezionare gli stream di dati da utilizzare per ciascuno dei tre ambienti disponibili (produzione, staging e sviluppo).

Quando una richiesta viene inviata alla rete Edge, viene utilizzato un ID dello stream di dati per fare riferimento alla configurazione lato server. Puoi aggiornare la configurazione senza dover apportare modifiche al codice sul tuo sito web.

Consulta la guida su [flussi di dati](../../../../datastreams/overview.md) per scoprire come configurare un flusso di dati.

Puoi scegliere uno stream di dati dai menu a discesa disponibili, oppure selezionare **[!UICONTROL Inserisci i valori]** e inserisci un ID dello stream di dati personalizzato per ogni ambiente.

![Immagine che mostra le impostazioni dello stream di dati dell’estensione tag Web SDK nell’interfaccia utente Tag](assets/web-sdk-ext-datastreams.png)

## Configurare le impostazioni della privacy {#privacy}

Questa sezione ti consente di configurare il modo in cui Web SDK gestisce i segnali di consenso degli utenti dal sito web. In particolare, consente di selezionare il livello predefinito di consenso presunto di un utente se non è stata fornita alcuna preferenza di consenso esplicito.

Il livello di consenso predefinito non viene salvato nel profilo utente.

![Immagine che mostra le impostazioni di privacy dell’estensione tag Web SDK nell’interfaccia utente Tag](assets/web-sdk-ext-privacy.png)

| [!UICONTROL Livello di consenso predefinito] | Descrizione |
| --- | --- |
| [!UICONTROL In entrata] | Raccogli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL Uscita] | Elimina gli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL In sospeso] | Metti in coda eventi che si verificano prima che l’utente fornisca le preferenze di consenso. Quando vengono fornite le preferenze di consenso, gli eventi vengono raccolti o eliminati in base alle preferenze fornite. |
| [!UICONTROL Fornito dall’elemento dati] | Il livello di consenso predefinito è determinato da un elemento dati separato da te definito. Quando utilizzi questa opzione, devi specificare l’elemento dati utilizzando il menu a discesa fornito. |

>[!TIP]
>
>Utilizzare **[!UICONTROL Uscita]** o **[!UICONTROL In sospeso]** se hai bisogno del consenso esplicito dell’utente per le operazioni aziendali.

## Configurare le impostazioni di identità {#identity}

Questa sezione ti consente di definire il comportamento dell’SDK web quando si tratta di gestire l’identificazione dell’utente.

![Immagine che mostra le impostazioni di identità dell’estensione tag Web SDK nell’interfaccia utente Tag](assets/web-sdk-ext-identity.png)

* **[!UICONTROL Migrazione di ECID da VisitorAPI]**: questa opzione è attivata per impostazione predefinita. Quando questa funzione è abilitata, l&#39;SDK può leggere `AMCV` e `s_ecid` cookie e impostare `AMCV` cookie utilizzato da [!DNL Visitor.js]. Questa funzione è importante durante la migrazione a Web SDK, in quanto alcune pagine potrebbero ancora utilizzare [!DNL Visitor.js]. Questa opzione consente all’SDK di continuare a utilizzare lo stesso [!DNL ECID] in modo che gli utenti non vengano identificati come due utenti distinti.
* **[!UICONTROL Utilizzare i cookie di terze parti]**: quando questa opzione è abilitata, Web SDK tenta di memorizzare un identificatore utente in un cookie di terze parti. In caso di esito positivo, l’utente viene identificato come un singolo utente mentre si sposta tra più domini, anziché essere identificato come un utente separato su ciascun dominio. Se questa opzione è abilitata, l’SDK potrebbe ancora non essere in grado di memorizzare l’identificatore utente in un cookie di terze parti se il browser non supporta i cookie di terze parti o se è stato configurato dall’utente per non consentire i cookie di terze parti. In questo caso, l’SDK memorizza l’identificatore solo nel dominio di prime parti.

  >[!IMPORTANT]
  >>I cookie di terze parti non sono compatibili con [ID dispositivo di prime parti](../../../../web-sdk/identity/first-party-device-ids.md) funzionalità di Web SDK.
Puoi utilizzare gli ID dispositivo di prime parti oppure cookie di terze parti, ma non puoi utilizzare entrambe le funzioni contemporaneamente.
  >
## Configurare le impostazioni di personalizzazione {#personalization}

Questa sezione ti consente di configurare come nascondere determinate parti di una pagina durante il caricamento del contenuto personalizzato. In questo modo i visitatori potranno vedere solo la pagina personalizzata.

![Immagine che mostra le impostazioni di personalizzazione dell’estensione tag Web SDK nell’interfaccia utente Tag](assets/web-sdk-ext-personalization.png)

* **[!UICONTROL Migrare Target da at.js a Web SDK]**: utilizza questa opzione per abilitare [!DNL Web SDK] per leggere e scrivere la versione precedente `mbox` e `mboxEdgeCluster` cookie utilizzati da at.js `1.x` o `2.x` librerie. Questo ti aiuta a mantenere il profilo visitatore durante il passaggio da una pagina che utilizza l’SDK per web a una pagina che utilizza at.js `1.x` o `2.x` e viceversa.

### Stile pre-hiding {#prehiding-style}

L’editor di stili che nasconde anticipatamente ti consente di definire regole CSS personalizzate per nascondere sezioni specifiche di una pagina. Quando la pagina viene caricata, Web SDK utilizza questo stile per nascondere le sezioni che devono essere personalizzate, recupera la personalizzazione e quindi rimuove le sezioni della pagina personalizzata. In questo modo, i visitatori visualizzano le pagine già personalizzate senza visualizzare il processo di recupero della personalizzazione.

### Frammento pre-hiding {#prehiding-snippet}

Il frammento pre-hiding è utile quando la libreria SDK Web viene caricata in modo asincrono. In questa situazione, per evitare sfarfallii, consigliamo di nascondere il contenuto prima che venga caricata la libreria dell’SDK web.

Per utilizzare il frammento pre-hiding, copiarlo e incollarlo all&#39;interno del `<head>` della pagina.

>[!IMPORTANT]
>
Quando si utilizza il frammento pre-hiding, l&#39;Adobe consiglia di utilizzare lo stesso [!DNL CSS] regola come quella utilizzata da [stile pre-hiding](#prehiding-style).

## Configurare le impostazioni di raccolta dati {#data-collection}

![Immagine che mostra le impostazioni di raccolta dati dell’estensione tag Web SDK nell’interfaccia utente Tag](assets/web-sdk-ext-collection.png)

* **[!UICONTROL Funzione callback]**: la funzione di callback fornita nell’estensione è denominata anche [`onBeforeEventSend` funzione](/help/web-sdk/commands/configure/onbeforeeventsend.md) nella libreria. Questa funzione consente di modificare gli eventi a livello globale prima che vengano inviati alla rete Edge.
* **[!UICONTROL Abilita raccolta dati di clic]**: Web SDK può raccogliere automaticamente le informazioni sul clic del collegamento. Per impostazione predefinita, questa funzione è abilitata, ma può essere disabilitata utilizzando questa opzione. I collegamenti sono etichettati anche come collegamenti di download se contengono una delle espressioni di download elencate in [!UICONTROL Qualificatore collegamento di download] casella di testo. In questo Adobe vengono forniti alcuni qualificatori predefiniti per i collegamenti di download. Puoi modificarli in base alle tue esigenze.
* **[!UICONTROL Dati contestuali raccolti automaticamente]**: per impostazione predefinita, Web SDK raccoglie alcuni dati contestuali relativi a dispositivo, web, ambiente e contesto del luogo. Se non desideri raccogliere questi dati o desideri solo raccogliere determinate categorie di dati, seleziona **[!UICONTROL Informazioni specifiche sul contesto]** e seleziona i dati che desideri raccogliere. Consulta [`context`](/help/web-sdk/commands/configure/context.md) per ulteriori informazioni.

## Configurare gli override dello stream di dati {#datastream-overrides}

Gli override dello stream di dati consentono di definire configurazioni aggiuntive per gli stream di dati, che vengono passate alla rete Edge tramite il Web SDK.

Questo consente di attivare comportamenti diversi dello stream di dati rispetto a quelli predefiniti, senza creare un nuovo stream di dati o modificare le impostazioni esistenti.

L’override della configurazione dello stream di dati è un processo costituito da due passaggi:

1. Innanzitutto, devi definire gli override della configurazione dello stream di dati nella [pagina di configurazione dello stream di dati](/help/datastreams/configure.md).
2. Quindi, devi inviare le sostituzioni a Edge Network tramite un comando Web SDK o utilizzando l’estensione tag Web SDK.

Visualizzare lo stream di dati [documentazione sulle sostituzioni di configurazione](/help/datastreams/overrides.md) per istruzioni dettagliate su come ignorare le configurazioni dello stream di dati.

In alternativa al passaggio delle sostituzioni tramite un comando Web SDK, puoi configurare le sostituzioni nella schermata dell’estensione tag mostrata di seguito.

>[!IMPORTANT]
>
Le sostituzioni dello stream di dati devono essere configurate in base all’ambiente. Gli ambienti di sviluppo, staging e produzione hanno tutti sostituzioni separate. Puoi copiare le impostazioni tra di esse utilizzando le opzioni dedicate mostrate nella schermata seguente.

![L’immagine che mostra le sostituzioni della configurazione dello stream di dati utilizzando la pagina dell’estensione tag di Web SDK.](assets/datastream-overrides.png)

## Configurare le impostazioni avanzate

Utilizza il **[!UICONTROL Percorso base perimetrale]** se è necessario modificare il percorso di base utilizzato per interagire con la rete Edge. Questo non dovrebbe richiedere l’aggiornamento, ma nel caso in cui partecipi a una versione beta o alpha, Adobe potrebbe chiederti di modificare questo campo.

![Immagine che mostra le impostazioni avanzate utilizzando la pagina dell’estensione tag Web SDK.](assets/advanced-settings.png)
