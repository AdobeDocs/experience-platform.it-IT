---
title: Regole
description: Scopri come funzionano le estensioni tag in Adobe Experience Platform.
exl-id: 2beca2c9-72b7-4ea0-a166-50a3b8edb9cd
source-git-commit: 85413e4a8b604dd9111ca4d47ad6a1ec49d8f547
workflow-type: tm+mt
source-wordcount: '1973'
ht-degree: 81%

---

# Regole

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

I tag in Adobe Experience Platform seguono un sistema basato su regole. Cercano le interazione degli utenti e i relativi dati. Quando i criteri descritti nelle tue regole vengono soddisfatti, la regola attiva l&#39;estensione, lo script o il codice lato client identificato.

Genera le regole per integrare dati e funzionalità di tecnologie marketing e annunci che unificano prodotti diversi in un&#39;unica soluzione.

## Struttura delle regole

**Eventi (If):** la regola deve cercare l&#39;evento. Ciò viene definito scegliendo un evento, eventuali condizioni applicabili ed eventuali eccezioni.

**Azioni (Then):** gli attivatori si manifestano dopo che gli eventi di una regola si sono verificati e tutte le condizioni sono state soddisfatte. Una regola di tag può attivare tutte le azioni discrete che desideri e controllare l’ordine in cui si verificano tali azioni. Ad esempio, una singola regola per una pagina di ringraziamento per l&#39;e-commerce può attivare gli strumenti di analisi e i tag di terze parti da una singola regola. Non è necessario creare regole separate per ogni estensione o tag.

Puoi aggiungere più tipi di evento. Più eventi sono collegati con un operatore OR, pertanto le condizioni della regola saranno valutate se uno qualsiasi degli eventi viene soddisfatto.

>[!IMPORTANT]
>
>Le modifiche diventano effettive solo dopo la loro [pubblicazione](../publishing/overview.md).

### Eventi e condizioni (if)

Gli eventi con qualsiasi condizione sono la porzione *If* di una regola.

Se si verifica un evento specificato, vengono valutate le condizioni, quindi vengono eseguite le azioni specificate, se necessario.

* **Eventi**: specifica uno o più eventi che devono aver luogo affinché la regola venga attivata. Gli eventi multipli sono collegati da un operatore OR. Uno qualsiasi degli eventi specificati attiva la regola.

* **Condizioni**: restringi l’evento configurando eventuali condizioni che devono essere soddisfatte affinché l’evento possa attivare la regola. Un&#39;eccezione è definita come condizione NOT. Condizioni multiple sono collegate da un AND.

Gli eventi disponibili dipendono dalle estensioni installate. Per informazioni sugli eventi nell&#39;estensione Core, consulta [Tipi di evento estensione Core](../../extensions/web/core/overview.md#core-extension-event-types).

### Azioni (then)

Le azioni sono la parte *Then* di una regola. Definiscono ciò che si desidera che accada quando la regola viene eseguita. Se quando viene attivato un evento le condizioni restituiscono true come risultato e le eccezioni restituiscono false, le azioni vengono eseguite. Puoi trascinare e rilasciare azioni per ordinarle come desideri.

## Creare una regola

Crea una regola specificando le azioni che si verificano se viene soddisfatta una condizione.

1. Apri la scheda [!UICONTROL Regole], quindi seleziona **[!UICONTROL Crea nuova regola]**.

   ![](../../images/launch-rule-builder.jpg)

1. Denomina la regola.
1. Fai clic sull’icona **[!UICONTROL Aggiungi]** degli Eventi.
1. Scegli l’estensione e uno dei tipi di evento disponibili per tale estensione, quindi configura le Impostazioni dell’evento.

   ![](../../images/rule-event-config.png)

   I tipi di evento disponibili dipendono dall’estensione selezionata. Le impostazioni dell’evento variano a seconda del tipo di evento. Alcuni eventi non dispongono di impostazioni da configurare.

   >[!IMPORTANT]
   >
   >In una regola lato client, gli elementi dati sono tokenizzati con un simbolo `%` all’inizio e alla fine del nome. Ad esempio, `%viewportHeight%`. In una regola per l’inoltro degli eventi, gli elementi dati vengono tokenizzati, con `{{` all’inizio e `}}` alla fine del nome dell’elemento dati. Ad esempio, `{{viewportHeight}}`.

   Per fare riferimento ai dati provenienti dalla rete Edge, il percorso dell’elemento dati deve essere `arc.event._<element>_`.

   `arc` sta per Adobe Response Context (Contesto di risposta Adobe).

   Ad esempio: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Se il percorso specificato non è corretto, i dati non vengono raccolti.

1. Imposta il parametro Ordine, quindi seleziona **[!UICONTROL Mantieni modifiche]**.

   L&#39;ordine predefinito per tutti i componenti della regola è 50. Se vuoi che una di queste venga eseguita prima, impostala con un numero inferiore a 50.

   * L&#39;ordine dell&#39;esecuzione equivale all&#39;ordine dei numeri. 1 precede 3. 3 precede 10. 10 viene precede 100 ecc.
   * Le regole che hanno lo stesso ordine vengono eseguite senza nessun ordine specifico.
   * Le regole vengono attivate in ordine, ma non necessariamente completate nello stesso ordine. Se la Regola A e la Regola B condividono un evento e assegni l&#39;ordine in modo che la Regola A arrivi per prima, se la Regola A esegue un elemento in modo asincrono, non c&#39;è garanzia che la Regola A termini prima dell&#39;avvio della Regola B.

      Se desideri che venga eseguita in un secondo momento, impostala con un numero maggiore di 50. Per ulteriori informazioni sull&#39;ordinamento, consulta [Ordinamento delle regole](rules.md#rule-ordering).

1. Fai clic sull’icona **[!UICONTROL Aggiungi]** delle Condizioni, quindi scegli un tipo di logica, un’estensione, un tipo di condizione e configura le impostazioni della condizione. Quindi, seleziona **[!UICONTROL Mantieni modifiche]**.

   ![](../../images/condition-settings.png)

   I tipi di condizioni disponibili dipendono dall’estensione selezionata. Le impostazioni delle condizioni variano a seconda del tipo di condizione.

   Tipo di logica:

   * Il tipo di logica Standard consente di eseguire azioni se la condizione viene soddisfatta
   * Il tipo logica Eccezione impedisce l&#39;esecuzione delle azioni se la condizione viene soddisfatta

   (Avanzata) Timeout: questa opzione è disponibile quando la sequenza dei componenti della regola è abilitata sulla proprietà. Questo attributo definisce il tempo massimo consentito per l’esecuzione della condizione. Se viene raggiunto il timeout, la condizione non riesce e il resto delle condizioni e delle azioni della regola verrà rimosso dalla coda di elaborazione. Il valore predefinito è 2000 ms.

   È possibile aggiungere tutte le condizioni desiderate. Più condizioni all’interno della stessa regola sono collegate da AND.

1. Fai clic sull’icona **[!UICONTROL Aggiungi]** delle Azioni, quindi scegli l’estensione e uno dei tipi di azione disponibili, configura le impostazioni per l’azione e seleziona **[!UICONTROL Mantieni modifiche]**.

   ![](../../images/action-settings.png)

   I tipi di azioni disponibili dipendono dall’estensione selezionata. Le impostazioni delle azioni variano a seconda del tipo di azione.

   (Avanzata) Wait to run next action (Attendi di eseguire l’azione successiva): questa opzione è disponibile quando la sequenza dei componenti della regola è abilitata sulla proprietà. Se questa opzione è selezionata, i tag non chiameranno l’azione successiva fino al completamento di questa. Se questa opzione è deselezionata, l’azione successiva inizia a essere eseguita immediatamente. Il valore predefinito è **[!UICONTROL Selezionata]**.

   (Avanzata) Timeout: questa opzione è disponibile quando la sequenza dei componenti della regola è abilitata sulla proprietà. Definisce il tempo massimo consentito per il completamento dell’azione. Se viene raggiunto il timeout, l’azione non riesce e tutte le azioni successive per questa regola verranno rimosse dalla coda di elaborazione. Il valore predefinito è 2000 ms.


1. Rivedi la regola, quindi seleziona **[!UICONTROL Salva regola]**.

   Successivamente, quando [pubblichi](../publishing/overview.md), aggiungi questa regola a una libreria e distribuiscila.

Quando crei o modifichi regole, puoi salvarle e distribuirle nella [libreria attiva](../publishing/libraries.md#active-library). In questo modo la tua libreria viene salvata immediatamente e viene eseguita una build. Viene visualizzato lo stato della build.

## Ordine regole {#rule-ordering}

L&#39;ordinamento delle regole consente di controllare l&#39;ordine di esecuzione per le regole che condividono un evento. Ogni regola contiene un numero intero che determina la sua priorità dell&#39;ordine (il valore predefinito è 50). Le regole che contengono valori più bassi per il loro ordine vengono eseguite prima di quelle con valori più alti.

Considera un set di cinque regole che condividono tutti un evento e hanno priorità predefinita:

* Se esiste una regola che desideri eseguire per ultima, puoi modificare quel componente della regola e assegnargli un numero maggiore di 50 (ad esempio, 60).
* Se vuoi eseguire prima una regola, puoi modificarla e assegnargli un numero inferiore a 50 (ad esempio, 40).

>[!NOTE]
>
>In ultima analisi, la responsabilità dell’esecuzione delle azioni è dello sviluppatore dell’estensione del tipo di evento utilizzato. Gli sviluppatori di estensioni Adobe assicurano che le loro estensioni funzionino come previsto. Adobe fornisce indicazioni agli sviluppatori di estensioni di terze parti per eseguire correttamente questa operazione, ma non può garantire il modo in cui vengono seguite queste linee guida.

Si consiglia vivamente di ordinare le regole con numeri positivi compresi tra 1 e 100 (il valore predefinito è 50). Poiché l&#39;ordine delle regole deve essere mantenuto manualmente, è consigliabile mantenere lo schema di ordinazione il più semplice possibile. In presenza di casi edge in cui questa restrizione è troppo limitativa, i tag supportano i numeri di ordine delle regole tra +/- 2.147.483.648.

### Gestione delle regole lato client

L&#39;ordine di caricamento delle regole dipende dal fatto che l&#39;azione delle regole sia configurata con JavaScript, HTML o altro codice lato client, e che le regole utilizzino un evento fine pagina, principale o un altro tipo di evento.

Puoi utilizzare `document.write` tra gli script personalizzati indipendentemente dagli eventi configurati per la regola.

Puoi ordinare diversi tipi di codici personalizzati tra loro. Ad esempio, puoi utilizzare un&#39;azione codice personalizzato JavaScript, poi un&#39;azione codice personalizzato HTML, quindi un&#39;azione codice personalizzato JavaScript. I tag assicurano che vengano eseguite in tale ordine.

## Raggruppamento di regole

Gli eventi e le condizioni delle regole sono sempre raggruppati nella libreria principale di tag. Le azioni possono essere raggruppate nella libreria principale o caricate in ritardo come risorse secondarie, a seconda delle necessità. Il fatto che le azioni siano raggruppate o meno è determinato dal tipo di evento della regola.

### Regole con eventi “Core - libreria caricata” o “Core - parte superiore della pagina”

Questi eventi devono essere eseguiti quasi sempre (a meno che le condizioni non vengano valutate come false), quindi per maggiore efficienza vengono raggruppati nella libreria principale, il file a cui fa riferimento il codice da incorporare.

* **JavaScript:** JavaScript è incorporato nella libreria principale di tag. Lo script personalizzato viene racchiuso in un tag script e scritto nel documento utilizzando `document.write`. Se la regola dispone di più script personalizzati, questi vengono scritti in ordine.

* **HTML:** il codice HTML è incorporato nella libreria principale di tag. `document.write` viene utilizzato per scrivere il codice HTML nel documento. Se la regola dispone di più script personalizzati, questi vengono scritti in ordine.

### Regole con qualsiasi altro evento

Adobe non è in grado di garantire che vengano attivate altre regole e che sia necessario il relativo codice di azione. Per questo motivo, le azioni per tutti i tipi di evento non elencati sopra non vengono incluse nella libreria principale. Vengono invece archiviate come risorse secondarie e a cui fa riferimento la libreria principale quando necessario.

* **JavaScript:** il JavaScript viene caricato dal server come testo normale, racchiuso in un tag script e aggiunto al documento utilizzando Postscribe. Se la regola dispone di più script personalizzati JavaScript, questi verranno caricati in parallelo dal server, ma vengono eseguiti nello stesso ordine configurato nella regola.
* **HTML:** l’HTML viene caricato dal server e aggiunto al documento utilizzando Postscribe. Se la regola dispone di più script personalizzati HTML, questi verranno caricati in parallelo dal server, ma vengono eseguiti nello stesso ordine configurato nella regola.

## Sequenza dei componenti della regola {#sequencing}

Il comportamento dell’ambiente runtime dei dipende dall’abilitazione o meno di **[!UICONTROL Esegui componenti regola in sequenza]** per la tua proprietà. Questa impostazione determina se i componenti di una regola possono essere valutati in parallelo (in modo asincrono) o se devono essere valutati in sequenza.

>[!IMPORTANT]
>
>Questa impostazione determina solo il modo in cui le condizioni e le azioni vengono valutate all&#39;interno di ogni regola e non influisce sulla sequenza in cui le regole stesse vengono eseguite sulla proprietà. Fai riferimento alla sezione precedente su [ordinamento delle regole](#rule-ordering) per ulteriori informazioni su come determinare l’ordine di esecuzione per più regole.
>
>In [inoltro eventi](../event-forwarding/overview.md) , le azioni delle regole vengono sempre eseguite in sequenza e questa impostazione non è disponibile. Nel creare la regola è importante accertarsi che l’ordine sia corretto.

### Abilitata

Se l’impostazione è abilitata quando un evento viene attivato in fase di runtime, le condizioni e le azioni della regola vengono aggiunte a una coda di elaborazione (in base all’ordine definito) ed elaborate una alla volta in base al criterio FIFO (first in, first out). La regola attende il completamento del componente prima di passare a quello successivo.

Se una condizione risulta false o raggiunge il timeout definito, le condizioni e le azioni successive della regola vengono rimosse dalla coda.

Se un’azione ha esito negativo o raggiunge il timeout definito, le azioni successive della regola vengono rimosse dalla coda. 

### Disabilitata

Se l’impostazione è disabilitata, quando un evento viene attivato in fase di runtime, le condizioni della regola vengono valutate immediatamente. Più condizioni vengono valutate in parallelo.

Se tutte le condizioni risultano true (e le eccezioni risultano false), le azioni della regola vengono eseguite immediatamente. Le azioni vengono richiamate in ordine, ma i tag non attendono che un’azione sia completata prima di chiamare quella successiva. Se le azioni sono sincronizzate, vengono comunque eseguite in ordine. Se una o più azioni sono asincrone, alcune vengono eseguite in parallelo.
