---
title: Tipi di azioni nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di azioni forniti dall’estensione tag Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: c3b05dfd57b3335230e9abb40de6f2e1ee5ee6fa
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 1%

---


# Tipi di azioni

Dopo aver configurato l&#39;estensione tag [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), è necessario configurare i tipi di azione.

Questa pagina descrive i tipi di azioni supportati dall&#39;estensione tag [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md).

## Applicare le proposte {#apply-propositions}

Il tipo di azione **[!UICONTROL Applica proposte]** consente di eseguire il rendering delle proposte nelle applicazioni a pagina singola senza incrementare le metriche.

Questo tipo di azione è utile quando si lavora con applicazioni a pagina singola in cui viene eseguito nuovamente il rendering di parti della pagina, sovrascrivendo potenzialmente eventuali personalizzazioni già applicate alla pagina.

Puoi utilizzare questo tipo di azione per vari casi d’uso, ad esempio:

1. **Rendering offerte mbox HTML**. Le proposte esplicitamente richieste tramite un ambito o una superficie da un&#39;azione **[!UICONTROL Invia evento]** non vengono sottoposte a rendering automaticamente. È possibile utilizzare il tipo di azione **[!UICONTROL Applica proposizioni]** per indicare a Web SDK dove eseguirne il rendering specificando i metadati della proposta.
2. **Eseguire il rendering delle offerte per una visualizzazione in un&#39;applicazione a pagina singola**. Durante il rendering di un evento di modifica della visualizzazione, se i dati di analisi non sono ancora pronti, puoi utilizzare l&#39;azione **[!UICONTROL Applica proposte]** per eseguire il rendering delle proposte di visualizzazione nella parte superiore della pagina. Per ulteriori dettagli, vedi [eventi di inizio e fine pagina (seconda visualizzazione pagina - opzione 2)](../../../../web-sdk/use-cases/top-bottom-page-events.md). Per utilizzare questa proprietà, immettere un **[!UICONTROL Nome visualizzazione]** nel modulo.
3. **Riesegui rendering delle proposte**. Quando il sito utilizza un framework come React per eseguire nuovamente il rendering del contenuto, potrebbe essere necessario riapplicare la personalizzazione. In questi casi è possibile utilizzare il tipo di azione **[!UICONTROL Applica proposizioni]**.

Questo tipo di azione non invierà un evento di visualizzazione per le proposte sottoposte a rendering. Tiene traccia delle proposte sottoposte a rendering in modo che possano essere incluse nelle chiamate **[!UICONTROL Invia evento]** successive.


![Interfaccia utente tag di Platform che mostra il tipo di azione Applica proposte.](assets/apply-propositions.png)

Questo tipo di azione supporta i campi seguenti:

* **[!UICONTROL Proposte]**: array di oggetti delle proposte di cui si desidera eseguire nuovamente il rendering.
* **[!UICONTROL Nome visualizzazione]**: nome della visualizzazione da riprodurre.
* **[!UICONTROL Metadati della proposta]**: oggetto che determina il modo in cui le offerte HTML possono essere applicate. Puoi fornire queste informazioni tramite il modulo o un elemento dati. Contiene le seguenti proprietà:
   * **[!UICONTROL Ambito]**
   * **[!UICONTROL Selettore]**
   * **[!UICONTROL Tipo azione]**

## Applica risposta {#apply-response}

Utilizza il tipo di azione **[!UICONTROL Applica risposta]** quando desideri eseguire varie azioni in base a una risposta dell&#39;Edge Network. Questo tipo di azione viene in genere utilizzato nelle implementazioni ibride in cui il server effettua una chiamata iniziale all’Edge Network, quindi prende la risposta da tale chiamata e inizializza l’SDK web nel browser.

L’utilizzo di questo tipo di azione può ridurre i tempi di caricamento del client per i casi di utilizzo della personalizzazione ibrida.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra il tipo di azione di risposta Applica.](assets/apply-response.png)

Questo tipo di azione supporta le seguenti opzioni di configurazione:

* **[!UICONTROL Istanza]**: selezionare l&#39;istanza Web SDK in uso.
* **[!UICONTROL Intestazioni di risposta]**: seleziona l&#39;elemento dati che restituisce un oggetto contenente le chiavi e i valori di intestazione restituiti dalla chiamata al server Edge Network.
* **[!UICONTROL Corpo risposta]**: seleziona l&#39;elemento dati che restituisce l&#39;oggetto contenente il payload JSON fornito dalla risposta dell&#39;Edge Network.
* **[!UICONTROL Decisioni di personalizzazione visiva]**: abilita questa opzione per eseguire automaticamente il rendering del contenuto di personalizzazione fornito dall&#39;Edge Network e nascondere anticipatamente il contenuto per evitare sfarfallii.

## Valuta set di regole {#evaluate-rulesets}

Questo tipo di azione attiva manualmente la valutazione del set di regole. I set di regole vengono restituiti da Adobe Journey Optimizer per supportare funzioni come i messaggi nel browser.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra il tipo di azione di risposta Valuta set di regole.](assets/evaluate-rulesets.png)

Questo tipo di azione supporta le seguenti opzioni:

* **[!UICONTROL Decisioni di personalizzazione visiva]**: abilita questa opzione per eseguire il rendering delle decisioni di personalizzazione visiva per gli elementi del set di regole corrispondenti.
* **[!UICONTROL Contesto della decisione]**: si tratta di una mappa chiave-valore utilizzata durante la valutazione dei set di regole di Adobe Journey Optimizer per il decisioning sul dispositivo. Puoi fornire il contesto decisionale manualmente o tramite un elemento dati.

## Ottieni tracciamento Media Analytics {#get-media-analytics-tracker}

Questa azione viene utilizzata per ottenere l’API legacy di Media Analytics. Quando si configura l’azione e viene fornito il nome di un oggetto, l’API legacy di Media Analytics verrà esportata nell’oggetto finestra in questione. Se non ne viene fornito alcuno, verrà esportato in `window.Media` come avviene per la libreria Media JS corrente.

![Immagine dell&#39;interfaccia utente di Platform che mostra il tipo di azione Ottieni tracciatore di Media Analytics.](assets/get-media-analytics-tracker.png)

## Reindirizza con identità {#redirect-with-identity}

Utilizza questo tipo di azione per condividere le identità dalla pagina corrente ad altri domini. Questa azione è progettata per essere utilizzata con un tipo di evento **[!UICONTROL click]** e una condizione di confronto dei valori. Per ulteriori informazioni su come utilizzare questo tipo di azione, consulta [aggiungere un&#39;identità all&#39;URL tramite l&#39;estensione Web SDK](../../../../web-sdk/commands/appendidentitytourl.md#extension).

## Invia evento {#send-event}

Invia un evento ad Experience Platform in modo che Platform possa raccogliere i dati inviati e agire in base a tali informazioni. Tutti i dati che desideri inviare possono essere inviati nel campo **[!UICONTROL Dati XDM]**. Utilizzare un oggetto [!DNL JSON] conforme alla struttura dello schema [!DNL XDM]. Questo oggetto può essere creato sulla tua pagina o tramite un **[!UICONTROL Codice personalizzato]** **[!UICONTROL Elemento dati]**.

Il tipo di azione **[!UICONTROL Invia evento]** supporta i campi e le impostazioni descritti di seguito. Questi campi sono tutti facoltativi.

### Impostazioni delle istanze {#instance}

Utilizza il selettore **[!UICONTROL Istanza]** per scegliere l&#39;istanza dell&#39;SDK Web che desideri configurare. Se disponi di una sola istanza, questa viene preselezionata.

![Immagine dell&#39;interfaccia utente Tag piattaforma che mostra le impostazioni dell&#39;istanza per il tipo di azione Invia evento.](assets/instance-settings.png)

* **[!UICONTROL Istanza]**: selezionare l&#39;istanza dell&#39;SDK Web che si desidera configurare. Se disponi di una sola istanza, questa verrà preselezionata.
* **[!UICONTROL Utilizza eventi guidati]**: abilita questa opzione per compilare o nascondere automaticamente alcuni campi per abilitare un particolare caso d&#39;uso. L’attivazione di questa opzione attiva la visualizzazione delle seguenti impostazioni.

  >[!NOTE]
  >
  >Gli eventi guidati mostrati di seguito sono correlati a [eventi principali e finali della pagina](../../../../web-sdk/use-cases/top-bottom-page-events.md).
   * **[!UICONTROL Richiedi personalizzazione]**: questo evento deve essere chiamato nella parte superiore della pagina. Quando è selezionato, questo evento imposta i campi seguenti:
      * **[!UICONTROL Tipo]**: **[!UICONTROL Recupero proposta di decisione]**
      * **[!UICONTROL Invia automaticamente un evento di visualizzazione]**: **[!UICONTROL false]**
      * Per eseguire automaticamente il rendering della personalizzazione in questo caso, abilita l&#39;opzione **[!UICONTROL Esegui rendering delle decisioni di personalizzazione visiva]**.
   * **[!UICONTROL Raccogli analisi]**: questo evento deve essere chiamato nella parte inferiore della pagina. Quando è selezionato, questo evento imposta i campi seguenti:
      * **[!UICONTROL Includi proposte sottoposte a rendering]**: **[!UICONTROL true]**
      * Le impostazioni di **[!UICONTROL Personalization]** sono nascoste


### Dati {#data}

![Immagine dell&#39;interfaccia utente Tag piattaforma che mostra le impostazioni degli elementi dati per il tipo di azione Invia evento.](assets/data.png)

* **[!UICONTROL Tipo]**: questo campo consente di specificare un tipo di evento da registrare nello schema XDM. Per ulteriori informazioni, vedere [`type`](/help/web-sdk/commands/sendevent/type.md) nel comando `sendEvent`.
* **[!UICONTROL XDM]**:
* **[!UICONTROL Dati]**: utilizzare questo campo per inviare dati che non corrispondono a uno schema XDM. Questo campo è utile se stai tentando di aggiornare un profilo Adobe Target o di inviare gli attributi Recommendations di Target. Per ulteriori informazioni, vedere [`data`](/help/web-sdk/commands/sendevent/data.md) nel comando `sendEvent`.
* **[!UICONTROL Includi proposte sottoposte a rendering]**: abilita questa opzione per includere tutte le proposte sottoposte a rendering, ma non è stato inviato un evento di visualizzazione. Utilizzalo insieme a **[!UICONTROL Invia automaticamente un evento di visualizzazione]** disabilitato. Questa impostazione aggiorna il campo XDM `_experience.decisioning` con informazioni sulle proposte sottoposte a rendering.
* **[!UICONTROL Il documento verrà scaricato]**: abilitare questa opzione per assicurarsi che gli eventi raggiungano il server anche se l&#39;utente si sposta dalla pagina. Questo consente agli eventi di raggiungere il server, ma le risposte vengono ignorate.
* **[!UICONTROL ID unione]**: **Questo campo è obsoleto**. Verrà popolato il campo XDM `eventMergeId`.

### Personalizzazione {#personalization}

![Immagine dell&#39;interfaccia utente Tag piattaforma che mostra le impostazioni di Personalization per il tipo di azione Invia evento.](assets/personalization-settings.png)

* **[!UICONTROL Ambiti]**: selezionare gli ambiti (Adobe Target [!DNL mboxes]) che si desidera richiedere esplicitamente alla personalizzazione. Puoi immettere gli ambiti manualmente o fornendo un elemento dati.
* **[!UICONTROL Superfici]**: imposta le superfici Web disponibili nella pagina per la personalizzazione. Per ulteriori dettagli, consulta la [documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html).
* **Decisioni di personalizzazione visiva:** Se desideri eseguire il rendering di contenuti personalizzati sulla pagina, seleziona la casella di controllo **[!UICONTROL Decisioni di personalizzazione visiva]**. Se necessario, è inoltre possibile specificare ambiti decisionali e/o superfici. Per ulteriori informazioni sul rendering di contenuti personalizzati, consulta la [documentazione sulla personalizzazione](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content).
* **[!UICONTROL Richiedi personalizzazione predefinita]**: utilizza questa sezione per controllare se sono richiesti l&#39;ambito a livello di pagina (mbox globale) e la superficie predefinita (superficie Web basata sull&#39;URL corrente). Per impostazione predefinita, questo viene richiesto automaticamente durante la prima chiamata `sendEvent` del caricamento della pagina. Puoi scegliere tra le seguenti opzioni:
   * **[!UICONTROL Automatico]**: comportamento predefinito. Richiedi la personalizzazione predefinita solo se non è ancora stata richiesta. Corrisponde a `requestDefaultPersonalization` non impostato nel comando Web SDK.
   * **[!UICONTROL Abilitato]**: richiede esplicitamente l&#39;ambito della pagina e la superficie predefinita. Questo aggiorna la cache di visualizzazione SPA. Corrisponde a `requestDefaultPersonalization` impostato su `true`.
   * **[!UICONTROL Disabilitato]**: elimina esplicitamente la richiesta per l&#39;ambito della pagina e la superficie predefinita. Corrisponde a `requestDefaultPersonalization` impostato su `false`.
* **[!UICONTROL Contesto della decisione]**: si tratta di una mappa chiave-valore utilizzata durante la valutazione dei set di regole di Adobe Journey Optimizer per il decisioning sul dispositivo. Puoi fornire il contesto decisionale manualmente o tramite un elemento dati.

### Override della configurazione dello stream di dati {#datastream-overrides}

Gli override dello stream di dati consentono di definire configurazioni aggiuntive per gli stream di dati, che vengono passate alla rete Edge tramite il Web SDK.

Questo consente di attivare comportamenti diversi dello stream di dati rispetto a quelli predefiniti, senza creare un nuovo stream di dati o modificare le impostazioni esistenti. Per ulteriori dettagli, consulta la documentazione su [configurazione delle sostituzioni dello stream di dati](web-sdk-extension-configuration.md#datastream-overrides).

## Invia evento multimediale {#send-media-event}

Invia un evento multimediale a Adobe Experience Platform e/o Adobe Analytics. Questa azione è utile quando tieni traccia degli eventi multimediali sul sito web. Seleziona un’istanza (se ne hai più di una). L&#39;azione richiede un `playerId` che rappresenti un identificatore univoco per una sessione multimediale tracciata. Inoltre, all&#39;avvio di una sessione multimediale, è necessario un elemento dati **[!UICONTROL Quality of Experience]** e `playhead`.

![Immagine dell&#39;interfaccia utente di Platform che mostra la schermata Invia evento multimediale.](assets/send-media-event.png)

Il tipo di azione **[!UICONTROL Invia evento multimediale]** supporta le proprietà seguenti:

* **[!UICONTROL Istanza]**: l&#39;istanza Web SDK in uso.
* **[!UICONTROL Tipo di evento multimediale]**: il tipo di evento multimediale da tracciare.
* **[!UICONTROL ID lettore]**: identificatore univoco della sessione multimediale.
* **[!UICONTROL Testina di riproduzione]**: la posizione corrente della riproduzione multimediale, in secondi.
* **[!UICONTROL Dettagli sessione multimediale]**: quando si invia un evento di avvio multimediale, è necessario specificare i dettagli richiesti della sessione multimediale.
* **[!UICONTROL Dettagli capitolo]**: in questa sezione è possibile specificare i dettagli del capitolo quando si invia un evento multimediale di inizio capitolo.
* **[!UICONTROL Dettagli Advertising]**: quando si invia un evento `AdBreakStart`, è necessario specificare i dettagli pubblicitari richiesti.
* **[!UICONTROL Dettagli del pod di Advertising]**: dettagli sul pod pubblicitario durante l&#39;invio di un evento `AdStart`.
* **[!UICONTROL Dettagli errore]**: dettagli sull&#39;errore di riproduzione che viene tracciato.
* **[!UICONTROL Dettagli aggiornamento stato]**: lo stato del lettore che viene aggiornato.
* **[!UICONTROL Metadati personalizzati]**: i metadati personalizzati sull&#39;evento multimediale di cui viene eseguito il tracciamento.
* **[!UICONTROL Qualità dell&#39;esperienza]**: la qualità dei contenuti multimediali dei dati dell&#39;esperienza che vengono tracciati.

## Impostare il consenso {#set-consent}

Dopo aver ricevuto il consenso dell’utente, questo deve essere comunicato a Adobe Experience Platform Web SDK utilizzando il tipo di azione &quot;Imposta consenso&quot;. Attualmente sono supportati due tipi di consenso standard: &quot;Adobe&quot; e &quot;IAB-TCF&quot;. Consulta [Preferenze di supporto per il consenso del cliente](../../../../web-sdk/commands/setconsent.md). Quando si utilizza Adobe versione 2.0, è supportato solo un valore di elemento dati. Dovrai creare un elemento dati che venga risolto nell’oggetto di consenso.

In questa azione, ti viene fornito anche un campo facoltativo per includere una Identity Map, in modo che le identità possano essere sincronizzate una volta ricevuto il consenso. La sincronizzazione è utile quando il consenso è configurato come &quot;In sospeso&quot; o &quot;Out&quot; perché la chiamata di consenso è probabilmente la prima chiamata da attivare.

## Aggiorna variabile {#update-variable}

Utilizza questa azione per modificare un oggetto XDM a seguito di un evento. Questa azione ha lo scopo di creare un oggetto a cui è possibile fare successivamente riferimento da un&#39;azione **[!UICONTROL Invia evento]**, per registrare l&#39;oggetto XDM dell&#39;evento.

Per utilizzare questo tipo di azione è necessario aver definito un elemento dati [variable](data-element-types.md#variable). Dopo aver scelto un elemento dati variabile da modificare, viene visualizzato un editor simile a quello dell&#39;elemento dati [XDM](data-element-types.md#xdm-object).

![](assets/update-variable.png)

Lo schema XDM utilizzato per l&#39;editor è lo schema selezionato nell&#39;elemento dati [!UICONTROL variable]. Puoi impostare una o più proprietà dell&#39;oggetto facendo clic su una delle proprietà nella struttura a sinistra, quindi modificando il valore a destra.Ad esempio, nella schermata seguente, la proprietà productby viene impostata sull&#39;elemento dati &quot;Produced by data element&quot;.

![](assets/update-variable-set-property.png)

Esistono alcune differenze tra l’editor nell’azione aggiorna variabile e l’editor nell’elemento dati dell’oggetto XDM. Innanzitutto, l’azione aggiorna variabile ha un elemento a livello principale etichettato &quot;xdm&quot;. Se fai clic su questo elemento, puoi specificare un elemento dati da utilizzare per impostare l’intero oggetto. In secondo luogo, l’azione aggiorna variabile dispone di caselle di controllo per cancellare i dati dall’oggetto xdm. Fai clic su una delle proprietà a sinistra, quindi seleziona la casella di controllo a destra per deselezionare il valore. Questo cancellerà il valore corrente prima di impostare qualsiasi valore sulla variabile.

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti conoscere meglio come configurare le azioni. Quindi, leggi come [configurare i tipi di elementi dati](data-element-types.md).
