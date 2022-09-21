---
title: Panoramica sull’inoltro degli eventi
description: Scopri la funzione di inoltro degli eventi di Adobe Experience Platform, che consente di utilizzare la rete Edge di Platform per eseguire attività senza modificare l’implementazione del tag.
feature: Event Forwarding
exl-id: 18e76b9c-4fdd-4eff-a515-a681bc78d37b
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 9%

---

# Panoramica sull’inoltro degli eventi

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’inoltro degli eventi in Adobe Experience Platform consente di inviare i dati degli eventi raccolti a una destinazione per l’elaborazione sul lato server. L’inoltro degli eventi riduce il peso della pagina web e dell’app utilizzando Adobe Experience Platform Edge Network per eseguire attività normalmente eseguite sul client. Implementato in modo simile ai tag, le regole di inoltro degli eventi possono trasformare e inviare dati a nuove destinazioni, ma invece di inviare tali dati da un’applicazione client come un browser web, vengono inviati dai server di Adobe.

Questo documento fornisce una panoramica di alto livello sull’inoltro degli eventi in Platform.

![Inoltro degli eventi nell’ecosistema di raccolta dei dati](../../../collection/images/home/event-forwarding.png)

>[!NOTE]
>
>Per informazioni su come l’inoltro degli eventi si adatta all’ecosistema di raccolta dei dati in Platform, consulta la sezione [panoramica sulla raccolta dati](../../../collection/home.md).

Inoltro di eventi combinato con Adobe Experience Platform [SDK per web](../../../edge/home.md) e [SDK per dispositivi mobili](https://aep-sdks.gitbook.io/docs/) offre i seguenti vantaggi:

**Prestazioni**:

* Effettua una singola chiamata da una pagina che contiene un payload di dati che poi si unisce sul lato server per ridurre il traffico di rete lato client e fornire un’esperienza più veloce ai clienti.
* Riduce il tempo necessario al caricamento delle pagine web per migliorare le prestazioni del sito.
* Diminuisci il numero di tecnologie lato client necessarie per fornire la tua esperienza e inviare dati a molte destinazioni.

**Governance dei dati**:

* Aumenta la trasparenza e il controllo su quali dati vengono inviati dove in tutte le proprietà.

## Differenze tra inoltro eventi e tag {#differences-from-tags}

In termini di configurazione, l&#39;inoltro degli eventi utilizza molti degli stessi concetti dei tag, ad esempio [regole](../managing-resources/rules.md), [elementi dati](../managing-resources/data-elements.md)e [estensioni](../managing-resources/extensions/overview.md). La differenza principale tra i due può essere riassunta come segue:

* Tag **collezioni** i dati evento da un sito web o da un’applicazione mobile nativa e li invia a Platform Edge Network.
* Inoltro eventi **invia** i dati dell’evento in arrivo da Platform Edge Network a un endpoint che rappresenta una destinazione finale o un endpoint che fornisce i dati con cui si desidera arricchire il payload originale.

Mentre i tag raccolgono i dati evento direttamente dal sito o dall’applicazione mobile nativa tramite gli SDK per web e dispositivi mobili di Platform, l’inoltro degli eventi richiede che i dati evento siano già inviati tramite Platform Edge Network per inviarli alle destinazioni. In altre parole, per utilizzare l’inoltro degli eventi è necessario implementare l’SDK per web o mobile della piattaforma sulla proprietà digitale (tramite tag o codice non elaborato).

### Proprietà {#properties}

L’inoltro degli eventi mantiene il proprio archivio di proprietà separate dai tag, che è possibile visualizzare nell’interfaccia utente di Experience Platform o nell’interfaccia utente di raccolta dati selezionando **[!UICONTROL Inoltro eventi]** nella navigazione a sinistra.

![Proprietà di inoltro eventi nell’interfaccia utente di raccolta dati](../../images/ui/event-forwarding/overview/properties.png)

Elenco di tutte le proprietà di inoltro eventi **[!UICONTROL Bordo]** come piattaforma. Non distinguono tra web e dispositivi mobili perché elaborano solo i dati ricevuti da Platform Edge Network, che a sua volta può ricevere i dati evento dalle piattaforme web e mobili.

### Estensioni {#extensions}

L&#39;inoltro degli eventi dispone di un proprio catalogo di estensioni compatibili, ad esempio [Core](../../extensions/web/core/event-forwarding.md) estensione e [Connettore cloud di Adobe](../../extensions/web/cloud-connector/overview.md) estensione. Puoi visualizzare le estensioni disponibili per le proprietà di inoltro eventi nell’interfaccia utente selezionando **[!UICONTROL Estensioni]** nella navigazione a sinistra, seguita da **[!UICONTROL Catalogo]**.

![Estensioni dell’inoltro eventi nell’interfaccia utente Raccolta dati](../../images/ui/event-forwarding/overview/extensions.png)

### Elementi dati {#data-elements}

I tipi di elementi dati disponibili nell&#39;inoltro degli eventi sono limitati al catalogo di elementi compatibili [estensioni](#extensions) che le forniscono.

Anche se gli elementi dati stessi vengono creati e configurati nello stesso modo in cui vengono inoltrati gli eventi per i tag, esistono alcune importanti differenze di sintassi quando si tratta di come fanno riferimento ai dati da Platform Edge Network.

#### Riferimento a dati da Platform Edge Network {#data-element-path}

Per fare riferimento ai dati di Platform Edge Network, devi creare un elemento dati che fornisca un percorso valido per tali dati. Quando crei l’elemento dati nell’interfaccia utente, seleziona **[!UICONTROL Core]** per l&#39;estensione e **[!UICONTROL Percorso]** per il tipo .

La **[!UICONTROL Percorso]** il valore dell&#39;elemento dati deve seguire il pattern `arc.event.{ELEMENT}` (ad esempio: `arc.event.xdm.web.webPageDetails.URL`). Affinché i dati possano essere inviati, è necessario specificare correttamente questo percorso.

![Esempio di un elemento dati di tipo percorso per l&#39;inoltro di eventi](../../images/ui/event-forwarding/overview/data-reference.png)

### Regole {#rules}

La creazione di regole nelle proprietà di inoltro eventi funziona in modo simile ai tag, con la differenza chiave che non è possibile selezionare eventi come componenti regola. Al contrario, una regola di inoltro eventi elabora tutti gli eventi ricevuti dalla [datastream](../../../edge/datastreams/overview.md) e inoltra tali eventi alle destinazioni se sono soddisfatte determinate condizioni.

![Regole di inoltro eventi nell’interfaccia utente di raccolta dati](../../images/ui/event-forwarding/overview/rules.png)

#### Tokenizzazione dell&#39;elemento dati {#tokenization}

Nelle regole dei tag, gli elementi dati vengono token con un `%` all’inizio e alla fine del nome dell’elemento dati (ad esempio: `%viewportHeight%`). Nelle regole di inoltro degli eventi, gli elementi dati vengono invece token con `{{` all&#39;inizio e `}}` alla fine del nome dell’elemento dati (ad esempio: `{{viewportHeight}}`).

![Esempio di un elemento dati di tipo percorso per l&#39;inoltro di eventi](../../images/ui/event-forwarding/overview/tokenization.png)

#### Sequenza di azioni della regola {#action-sequencing}

La [!UICONTROL Azioni] la sezione di una regola di inoltro eventi viene sempre eseguita in sequenza. Quando si salva una regola, occorre assicurarsi che l&#39;ordine delle azioni sia corretto. Questa sequenza di esecuzione non può essere eseguita in modo asincrono come può con i tag .

## Segreti {#secrets}

L’inoltro eventi ti consente di creare, gestire e archiviare segreti che possono essere utilizzati per l’autenticazione ai server a cui stai inviando i dati. Consulta la guida su [segreti](./secrets.md) sui diversi tipi di tipi di segreti disponibili e su come vengono implementati nell’interfaccia utente.

## Passaggi successivi

Questo documento fornisce un’introduzione di alto livello all’inoltro di eventi. Per ulteriori informazioni su come impostare questa funzione per la tua organizzazione, consulta [guida introduttiva](./getting-started.md).
