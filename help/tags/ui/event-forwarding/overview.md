---
title: Panoramica sull’inoltro degli eventi
description: Scopri la funzione di inoltro degli eventi di Adobe Experience Platform, che consente di utilizzare la rete Edge di Platform per eseguire attività senza modificare l’implementazione del tag.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: eb9d2f9a233f4214057db5136f32fc1290ece63c
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 9%

---

# Panoramica sull’inoltro degli eventi

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’inoltro degli eventi in Adobe Experience Platform consente di inviare i dati degli eventi raccolti a una destinazione per l’elaborazione lato server. L’inoltro di eventi diminuisce il peso delle pagine web e delle app utilizzando Adobe Experience Platform Edge Network per eseguire attività normalmente eseguite sul client. Implementate in modo simile ai tag, le regole di inoltro degli eventi possono trasformare e inviare dati a nuove destinazioni, ma invece di inviarli da un’applicazione client come un browser web, vengono inviati dai server di Adobe.

Questo documento fornisce una panoramica di alto livello sull’inoltro degli eventi in Platform.

![Inoltro di eventi nell’ecosistema di raccolta dei dati](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Per informazioni su come l’inoltro degli eventi si inserisce nell’ecosistema di raccolta dati di Platform, consulta la sezione [panoramica sulla raccolta dati](../../../collection/home.md).

Inoltro di eventi in combinazione con Adobe Experience Platform [SDK per web](../../../edge/home.md) e [SDK per dispositivi mobili](https://aep-sdks.gitbook.io/docs/) offre i seguenti vantaggi:

**Prestazioni**:

* Effettua una singola chiamata da una pagina che contiene un payload di dati che poi viene federata sul lato server per ridurre il traffico di rete lato client e offrire un’esperienza più veloce ai clienti.
* Riduci il tempo necessario al caricamento delle pagine web per migliorare le prestazioni del sito.
* Diminuisci il numero di tecnologie lato client necessarie per fornire la tua esperienza e inviare dati a molte destinazioni.

**Governance dei dati**:

* Aumenta la trasparenza e il controllo su quali dati vengono inviati e dove su tutte le proprietà.

## Differenze tra inoltro eventi e tag {#differences-from-tags}

In termini di configurazione, l’inoltro degli eventi utilizza molti degli stessi concetti dei tag, ad esempio [regole](../managing-resources/rules.md), [elementi dati](../managing-resources/data-elements.md), e [estensioni](../managing-resources/extensions/overview.md). La differenza principale tra i due può essere riassunta come segue:

* Tag **raccoglie** dati evento da un sito web o da un’app mobile nativa e li invia a Platform Edge Network.
* Inoltro eventi **invia** i dati dell’evento in entrata da Platform Edge Network a un endpoint che rappresenta una destinazione finale o un endpoint che fornisce i dati con cui desideri arricchire il payload originale.

Mentre i tag raccolgono i dati dell’evento direttamente dal sito o dall’applicazione mobile nativa utilizzando gli SDK di Platform Web e Mobile, l’inoltro degli eventi richiede che i dati dell’evento siano già inviati tramite Platform Edge Network per essere inoltrati alle destinazioni. In altre parole, per utilizzare l’inoltro degli eventi è necessario implementare Platform Web SDK o Mobile SDK nella proprietà digitale (tramite tag o utilizzando codice non elaborato).

### Proprietà {#properties}

L’inoltro degli eventi mantiene un proprio archivio di proprietà separate dai tag, che puoi visualizzare nell’interfaccia utente di Experience Platform o di Data Collection selezionando **[!UICONTROL Inoltro eventi]** nel menu di navigazione a sinistra.

![Proprietà di inoltro degli eventi nell’interfaccia utente di Data Collection](../../images/ui/event-forwarding/overview/properties.png)

Elenco di tutte le proprietà di inoltro eventi **[!UICONTROL Bordo]** come piattaforma. Non distinguono tra web e mobile perché elaborano solo i dati ricevuti da Platform Edge Network, che a sua volta può ricevere i dati di eventi da piattaforme web e mobili.

### Estensioni {#extensions}

L’inoltro degli eventi dispone di un proprio catalogo di estensioni compatibili, ad esempio [Core](../../extensions/server/core/overview.md) estensione e [Connettore cloud Adobe](../../extensions/server/cloud-connector/overview.md) estensione. Puoi visualizzare le estensioni disponibili per le proprietà di inoltro degli eventi nell’interfaccia utente selezionando **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seguito da **[!UICONTROL Catalogo]**.

![Estensioni di inoltro degli eventi nell’interfaccia utente di Data Collection](../../images/ui/event-forwarding/overview/extensions.png)

### Elementi dati {#data-elements}

I tipi di elementi dati disponibili nell’inoltro degli eventi sono limitati al catalogo di compatibili [estensioni](#extensions) che li forniscono.

Anche se gli elementi dati stessi vengono creati e configurati nello stesso modo nell’inoltro degli eventi come per i tag, esistono alcune importanti differenze di sintassi per quanto riguarda il modo in cui fanno riferimento ai dati da Platform Edge Network.

#### Dati di riferimento da Platform Edge Network {#data-element-path}

Per fare riferimento ai dati da Platform Edge Network, devi creare un elemento dati che fornisca un percorso valido per tali dati. Quando crei l’elemento dati nell’interfaccia utente, seleziona **[!UICONTROL Core]** per l&#39;estensione e **[!UICONTROL Percorso]** per il tipo.

Il **[!UICONTROL Percorso]** il valore per l’elemento dati deve seguire il pattern `arc.event.{ELEMENT}` (ad esempio: `arc.event.xdm.web.webPageDetails.URL`). Questo percorso deve essere specificato correttamente per poter inviare i dati.

![Esempio di elemento dati di tipo percorso per l’inoltro di eventi](../../images/ui/event-forwarding/overview/data-reference.png)

### Regole {#rules}

La creazione di regole nelle proprietà di inoltro degli eventi funziona in modo simile ai tag, con la differenza fondamentale che non è possibile selezionare eventi come componenti regola. Al contrario, una regola di inoltro degli eventi elabora tutti gli eventi che riceve dal [flusso di dati](../../../edge/datastreams/overview.md) e inoltra tali eventi alle destinazioni se sono soddisfatte determinate condizioni.

Inoltre, esiste un timeout di 30 secondi che si applica a un singolo evento durante l’elaborazione in tutte le regole (e quindi tutte le azioni) all’interno di una proprietà di inoltro degli eventi. Ciò significa che tutte le regole e tutte le azioni per un singolo evento devono essere completate in questo intervallo di tempo.

![Regole di inoltro degli eventi nell’interfaccia utente di Data Collection](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenizzazione dell&#39;elemento dati {#tokenization}

Nelle regole di tag, gli elementi dati sono tokenizzati con un simbolo `%` all’inizio e alla fine del nome dell’elemento dati (ad esempio: `%viewportHeight%`). Nelle regole di inoltro degli eventi, gli elementi dati sono invece tokenizzati con `{{` all&#39;inizio e `}}` alla fine del nome dell’elemento dati (ad esempio: `{{viewportHeight}}`).

![Esempio di elemento dati di tipo percorso per l’inoltro di eventi](../../images/ui/event-forwarding/overview/tokenization.png)

#### Sequenza di azioni della regola {#action-sequencing}

Il [!UICONTROL Azioni] di una regola di inoltro degli eventi viene sempre eseguita in sequenza. Ad esempio, se una regola ha due azioni, la seconda azione non inizia l’esecuzione fino al completamento dell’azione precedente (e nei casi in cui è prevista una risposta da un endpoint, tale endpoint ha risposto). Quando si salva una regola, occorre assicurarsi che l&#39;ordine delle azioni sia corretto. Questa sequenza di esecuzione non può essere eseguita in modo asincrono come con le regole di tag.

## Segreti {#secrets}

L’inoltro degli eventi consente di creare, gestire e archiviare segreti che possono essere utilizzati per l’autenticazione sui server a cui stai inviando i dati. Consulta la guida su [segreti](./secrets.md) sui diversi tipi di segreti disponibili e su come implementarli nell’interfaccia utente.

## Passaggi successivi

Questo documento fornisce un’introduzione di alto livello all’inoltro degli eventi. Per ulteriori informazioni su come impostare questa funzione per la tua organizzazione, consulta [guida introduttiva](./getting-started.md).
