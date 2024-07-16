---
title: Tipi di azioni nell’estensione Adobe Experience Platform Web SDK
description: Scopri i diversi tipi di azioni forniti dall’estensione tag Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: fb9f7757d77b221c733bbed5124fa576a6b02ed2
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---


# Tipi di azioni

Dopo aver configurato l&#39;estensione tag [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), è necessario configurare i tipi di azione.

Questa pagina descrive i tipi di azioni supportati dall&#39;estensione tag [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md).


## Applica risposta {#apply-response}

Utilizza il tipo di azione **[!UICONTROL Applica risposta]** quando desideri eseguire varie azioni in base a una risposta dell&#39;Edge Network. Questo tipo di azione viene in genere utilizzato nelle implementazioni ibride in cui il server effettua una chiamata iniziale all’Edge Network, quindi prende la risposta da tale chiamata e inizializza l’SDK web nel browser.

L’utilizzo di questo tipo di azione può ridurre i tempi di caricamento del client per i casi di utilizzo della personalizzazione ibrida.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra il tipo di azione di risposta Applica.](assets/apply-response.png)

Questo tipo di azione supporta le seguenti opzioni di configurazione:

* **[!UICONTROL Istanza]**: selezionare l&#39;istanza Web SDK in uso.
* **[!UICONTROL Intestazioni di risposta]**: seleziona l&#39;elemento dati che restituisce un oggetto contenente le chiavi e i valori di intestazione restituiti dalla chiamata al server Edge Network.
* **[!UICONTROL Corpo risposta]**: seleziona l&#39;elemento dati che restituisce l&#39;oggetto contenente il payload JSON fornito dalla risposta dell&#39;Edge Network.
* **[!UICONTROL Decisioni di personalizzazione visiva]**: abilita questa opzione per eseguire automaticamente il rendering del contenuto di personalizzazione fornito dall&#39;Edge Network e nascondere anticipatamente il contenuto per evitare sfarfallii.

## Invia evento {#send-event}

Invia un evento all&#39;Adobe [!DNL Experience Platform] in modo che Adobe Experience Platform possa raccogliere i dati inviati e agire in base a tali informazioni. Seleziona un’istanza (se ne hai più di una). Tutti i dati che desideri inviare possono essere inviati nel campo **[!UICONTROL Dati XDM]**. Utilizza un oggetto JSON conforme alla struttura dello schema XDM. Questo oggetto può essere creato sulla tua pagina o tramite un **[!UICONTROL Codice personalizzato]** **[!UICONTROL Elemento dati]**.

Esistono alcuni altri campi nel tipo di azione Invia evento che potrebbero essere utili a seconda dell’implementazione. Si noti che questi campi sono tutti facoltativi.

* **Tipo:** Questo campo consente di specificare un tipo di evento da registrare nello schema XDM. Per ulteriori informazioni, vedere [`type`](/help/web-sdk/commands/sendevent/type.md) nel comando `sendEvent`.
* **Dati:** I dati che non corrispondono a uno schema XDM possono essere inviati utilizzando questo campo. Questo campo è utile se stai tentando di aggiornare un profilo Adobe Target o di inviare gli attributi Recommendations di Target. Per ulteriori informazioni, vedere [`data`](/help/web-sdk/commands/sendevent/data.md) nel comando `sendEvent`.<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **ID set di dati:** Se devi inviare dati a un set di dati diverso da quello specificato nello stream di dati, puoi specificare tale ID qui.
* **Il documento verrà scaricato:** Se desideri che gli eventi raggiungano il server anche se l&#39;utente si sposta dalla pagina, seleziona la casella di controllo **[!UICONTROL Il documento verrà scaricato]**. Questo consente agli eventi di raggiungere il server, ma le risposte vengono ignorate.
* **Decisioni di personalizzazione visiva:** Se desideri eseguire il rendering di contenuti personalizzati sulla pagina, seleziona la casella di controllo **[!UICONTROL Decisioni di personalizzazione visiva]**. Se necessario, è inoltre possibile specificare ambiti decisionali e/o superfici. Per ulteriori informazioni sul rendering di contenuti personalizzati, consulta la [documentazione sulla personalizzazione](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content).

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

## Ottieni tracciamento Media Analytics {#get-media-analytics-tracker}

Questa azione viene utilizzata per ottenere l’API legacy di Media Analytics. Quando si configura l’azione e viene fornito il nome di un oggetto, l’API legacy di Media Analytics verrà esportata nell’oggetto finestra in questione. Se non ne viene fornito alcuno, verrà esportato in `window.Media` come avviene per la libreria Media JS corrente.

![Immagine dell&#39;interfaccia utente di Platform che mostra il tipo di azione Ottieni tracciatore di Media Analytics.](assets/get-media-analytics-tracker.png)

## Reindirizza con identità {#redirect-with-identity}

Utilizza questo tipo di azione per condividere le identità dalla pagina corrente ad altri domini. Questa azione è progettata per essere utilizzata con un tipo di evento **[!UICONTROL click]** e una condizione di confronto dei valori. Per ulteriori informazioni su come utilizzare questo tipo di azione, consulta [aggiungere un&#39;identità all&#39;URL tramite l&#39;estensione Web SDK](../../../../web-sdk/commands/appendidentitytourl.md#extension).

## Passaggi successivi {#next-steps}

Dopo aver letto questo articolo, dovresti conoscere meglio come configurare le azioni. Quindi, leggi come [configurare i tipi di elementi dati](data-element-types.md).
