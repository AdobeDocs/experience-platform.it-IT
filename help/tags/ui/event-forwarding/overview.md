---
title: Panoramica sull’inoltro degli eventi
description: Scopri la funzione di inoltro degli eventi di Adobe Experience Platform, che consente di utilizzare l’Edge Network di Experience Platform per eseguire attività senza modificare l’implementazione dei tag.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 7%

---

# Panoramica sull’inoltro degli eventi

>[!NOTE]
>
>L’inoltro di eventi è una funzione a pagamento inclusa nelle offerte Adobe Real-Time Customer Data Platform Connections, Prime o Ultimate.

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch è ora una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’inoltro degli eventi in Adobe Experience Platform consente di inviare i dati degli eventi raccolti a una destinazione per l’elaborazione lato server. L’inoltro di eventi diminuisce il peso delle pagine web e delle app utilizzando Adobe Experience Platform Edge Network per eseguire attività normalmente eseguite sul client. Implementate in modo simile ai tag, le regole di inoltro degli eventi possono trasformare e inviare dati a nuove destinazioni, ma invece di inviarli da un’applicazione client come un browser web, vengono inviati dai server di Adobe.

Questo documento fornisce una panoramica di alto livello sull’inoltro degli eventi in Experience Platform.

![Inoltro eventi nell&#39;ecosistema di raccolta dati.](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Per informazioni sul modo in cui l&#39;inoltro degli eventi si inserisce nell&#39;ecosistema di raccolta dati di Experience Platform, consulta la [panoramica sulla raccolta dati](../../../collection/home.md).

L&#39;inoltro degli eventi combinato con Adobe Experience Platform [Web SDK](/help/web-sdk/home.md) e [Mobile SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/mobile-sdk/overview.html?lang=it) offre i seguenti vantaggi:

**Prestazioni**:

* Effettua una singola chiamata da una pagina che contiene un payload di dati che poi viene federata sul lato server per ridurre il traffico di rete lato client e offrire un’esperienza più veloce ai clienti.
* Riduci il tempo necessario al caricamento delle pagine web per migliorare le prestazioni del sito.
* Diminuisci il numero di tecnologie lato client necessarie per fornire la tua esperienza e inviare dati a molte destinazioni.

**Governance dei dati**:

* Aumenta la trasparenza e il controllo su quali dati vengono inviati e dove su tutte le proprietà.

## Differenze tra inoltro eventi e tag {#differences-from-tags}

In termini di configurazione, l&#39;inoltro degli eventi utilizza molti degli stessi concetti dei tag, ad esempio [regole](../managing-resources/rules.md), [elementi dati](../managing-resources/data-elements.md) e [estensioni](../managing-resources/extensions/overview.md). La differenza principale tra i due può essere riassunta come segue:

* I tag **raccolgono** dati evento da un sito Web o da un&#39;app mobile nativa e li inviano ad Experience Platform Edge Network.
* L&#39;inoltro degli eventi **invia** i dati degli eventi in arrivo da Experience Platform Edge Network a un endpoint che rappresenta una destinazione finale o un endpoint che fornisce i dati con cui desideri arricchire il payload originale.

Mentre i tag raccolgono i dati dell’evento direttamente dal sito o dall’app mobile nativa tramite gli SDK Experience Platform Web e Mobile, l’inoltro degli eventi richiede che i dati dell’evento siano già inviati tramite Experience Platform Edge Network per essere inoltrati alle destinazioni. In altre parole, per utilizzare l’inoltro degli eventi è necessario implementare Experience Platform Web o Mobile SDK nella proprietà digitale (tramite tag o utilizzando codice non elaborato).

### Proprietà {#properties}

L&#39;inoltro degli eventi mantiene un proprio archivio di proprietà separato dai tag, che puoi visualizzare nell&#39;interfaccia utente di Experience Platform o di Data Collection selezionando **[!UICONTROL Inoltro eventi]** nell&#39;area di navigazione a sinistra.

>[!TIP]
>
>Utilizza il nella guida del prodotto nel pannello a destra per ulteriori informazioni sull’inoltro degli eventi e visualizzare le risorse disponibili aggiuntive.

![Proprietà di inoltro eventi nell&#39;interfaccia utente di Data Collection.](../../images/ui/event-forwarding/overview/properties.png)

Tutte le proprietà di inoltro eventi elencano **[!UICONTROL Edge]** come piattaforma. Non fanno distinzione tra web e mobile perché elaborano solo i dati ricevuti da Experience Platform Edge Network, che a sua volta può ricevere i dati di eventi dalle piattaforme web e mobili.

### Estensioni {#extensions}

L&#39;inoltro degli eventi dispone di un proprio catalogo di estensioni compatibili, ad esempio l&#39;estensione [Core](../../extensions/server/core/overview.md) e l&#39;estensione [Adobe Cloud Connector](../../extensions/server/cloud-connector/overview.md). Puoi visualizzare le estensioni disponibili per le proprietà di inoltro degli eventi nell&#39;interfaccia utente selezionando **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seguito da **[!UICONTROL Catalogo]**.

Puoi visualizzare le risorse aggiuntive disponibili per ulteriori informazioni su questa funzione selezionando ![informazioni](../../images/ui/event-forwarding/overview/about.png) dal pannello a destra.

![Estensioni di inoltro eventi nell&#39;interfaccia utente di Data Collection.](../../images/ui/event-forwarding/overview/extensions.png)

### Elementi dati {#data-elements}

I tipi di elementi dati disponibili nell&#39;inoltro degli eventi sono limitati al catalogo di [estensioni](#extensions) compatibili che li forniscono.

Anche se gli elementi dati stessi vengono creati e configurati nello stesso modo nell’inoltro degli eventi come per i tag, esistono alcune importanti differenze di sintassi per quanto riguarda il modo in cui fanno riferimento ai dati provenienti da Experience Platform Edge Network.

#### Dati di riferimento da Experience Platform Edge Network {#data-element-path}

Per fare riferimento ai dati di Experience Platform Edge Network, devi creare un elemento dati che fornisca un percorso valido per tali dati. Durante la creazione dell&#39;elemento dati nell&#39;interfaccia utente, selezionare **[!UICONTROL Core]** per l&#39;estensione e **[!UICONTROL Path]** per il tipo.

Il valore **[!UICONTROL Path]** per l&#39;elemento dati deve seguire il pattern `arc.event.{ELEMENT}` (ad esempio: `arc.event.xdm.web.webPageDetails.URL`). Questo percorso deve essere specificato correttamente per poter inviare i dati.

Puoi visualizzare le risorse aggiuntive disponibili per ulteriori informazioni su questa funzione selezionando ![informazioni](../../images/ui/event-forwarding/overview/about.png) dal pannello a destra.

![Esempio di un elemento dati di tipo percorso per l&#39;inoltro di eventi.](../../images/ui/event-forwarding/overview/data-reference.png)

### Regole {#rules}

La creazione di regole nelle proprietà di inoltro degli eventi funziona in modo simile ai tag, con la differenza fondamentale che non è possibile selezionare eventi come componenti regola. Al contrario, una regola di inoltro degli eventi elabora tutti gli eventi ricevuti dal [flusso di dati](../../../datastreams/overview.md) e inoltra tali eventi alle destinazioni se vengono soddisfatte determinate condizioni.

Inoltre, esiste un timeout di 30 secondi che si applica a un singolo evento durante l’elaborazione in tutte le regole (e quindi tutte le azioni) all’interno di una proprietà di inoltro degli eventi. Ciò significa che tutte le regole e tutte le azioni per un singolo evento devono essere completate in questo intervallo di tempo.

Puoi visualizzare le risorse aggiuntive disponibili per ulteriori informazioni su questa funzione selezionando ![informazioni](../../images/ui/event-forwarding/overview/about.png) dal pannello a destra.

![Regole di inoltro degli eventi nell&#39;interfaccia utente di Data Collection.](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenizzazione dell&#39;elemento dati {#tokenization}

Nelle regole di tag, gli elementi dati sono tokenizzati con un simbolo `%` all&#39;inizio e alla fine del nome (ad esempio: `%viewportHeight%`). Nelle regole di inoltro degli eventi, gli elementi dati sono tokenizzati con `{{` all&#39;inizio e `}}` alla fine del nome dell&#39;elemento dati (ad esempio: `{{viewportHeight}}`).

Puoi visualizzare le risorse aggiuntive disponibili per ulteriori informazioni su questa funzione selezionando ![informazioni](../../images/ui/event-forwarding/overview/about.png) dal pannello a destra.

![Esempio di un elemento dati di tipo percorso per l&#39;inoltro di eventi.](../../images/ui/event-forwarding/overview/tokenization.png)

#### Sequenza di azioni della regola {#action-sequencing}

La sezione [!UICONTROL Azioni] di una regola di inoltro eventi viene sempre eseguita in sequenza. Ad esempio, se una regola ha due azioni, la seconda azione non inizia l’esecuzione fino al completamento dell’azione precedente (e nei casi in cui è prevista una risposta da un endpoint, tale endpoint ha risposto). Quando si salva una regola, occorre assicurarsi che l&#39;ordine delle azioni sia corretto. Questa sequenza di esecuzione non può essere eseguita in modo asincrono come con le regole di tag.

## Segreti {#secrets}

L’inoltro degli eventi consente di creare, gestire e archiviare segreti che possono essere utilizzati per l’autenticazione sui server a cui stai inviando i dati. Consulta la guida sui [segreti](./secrets.md) sui diversi tipi di segreti disponibili e su come implementarli nell&#39;interfaccia utente.

## Panoramica video {#video}

Il video seguente ha lo scopo di aiutarti a comprendere meglio l’inoltro degli eventi e le connessioni Real-Time CDP.

>[!VIDEO](https://video.tv.adobe.com/v/3429308)

## Passaggi successivi

Questo documento fornisce un’introduzione di alto livello all’inoltro degli eventi. Per ulteriori informazioni sulla configurazione di questa funzionalità per la tua organizzazione, consulta la [guida introduttiva](./getting-started.md).
