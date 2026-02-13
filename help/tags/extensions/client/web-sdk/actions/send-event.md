---
title: Invia evento
description: Invia dati a Adobe Experience Platform Edge Network.
exl-id: 4ac7750e-48ab-4eb6-873d-bb2556dbf788
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---

# Invia evento

L&#39;azione **[!UICONTROL Send event]** invia un payload a un flusso di dati sull&#39;Edge Network di Adobe Experience Platform. È una caratteristica fondamentale della raccolta e della personalizzazione dei dati; quasi tutte le organizzazioni utilizzano questa azione come parte dell’implementazione di Web SDK.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Imposta il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]**, quindi imposta [!UICONTROL Action type] su **[!UICONTROL Send event]**.

## Campi generali

![Immagine dell&#39;interfaccia utente Tag di Experience Platform con le impostazioni dell&#39;istanza per il tipo di azione Invia evento.](../assets/instance-settings.png)

* **[!UICONTROL Instance]**: l&#39;istanza SDK a cui si applica l&#39;azione. Questo menu a discesa è disattivato se l’implementazione utilizza una singola istanza di SDK.
* **[!UICONTROL Use guided events]**: Abilita questa opzione per compilare o nascondere automaticamente alcuni campi per abilitare un caso d&#39;uso specifico. Questa impostazione può aiutare a ridurre il rumore delle opzioni disponibili durante la configurazione dell&#39;azione per ciascuno scopo rispettivo e segue le best practice di Adobe di [eventi di pagina superiore/inferiore](/help/collection/use-cases/personalization/top-bottom-page-events.md). L’attivazione di questa casella di controllo attiva la visualizzazione dei seguenti pulsanti di scelta:
   * **[!UICONTROL Request personalization]**: ottieni le decisioni di personalizzazione più recenti senza registrare un evento Adobe Analytics. Si chiama più comunemente nella parte superiore della pagina. Quando è selezionato, questo pulsante di opzione imposta i campi seguenti:
      * [!UICONTROL Type] è bloccato su [!UICONTROL Decisioning Proposition Fetch]
      * [!UICONTROL Render visual personalization decisions] è bloccato su abilitato
      * [!UICONTROL Automatically send a display event] è bloccato su disabilitato
   * **[!UICONTROL Collect analytics]**: registra un evento senza ottenere decisioni di personalizzazione. Si chiama più comunemente nella parte inferiore della pagina. Quando è selezionato, questo pulsante di opzione imposta i campi seguenti:
      * [!UICONTROL Include rendered propositions] è bloccato su abilitato

## Campi dati

![Immagine dell&#39;interfaccia utente Tag di Experience Platform che mostra le impostazioni dell&#39;elemento dati per il tipo di azione Invia evento.](../assets/data.png)

* **[!UICONTROL Type]**: tipo di evento. È possibile selezionare da un insieme di valori predefinito o definire un valore personalizzato. Per ulteriori informazioni, vedere [Valori accettati per `eventType`](/help/xdm/classes/experienceevent.md#accepted-values-for-eventtype). L&#39;equivalente della libreria JavaScript a questo campo è [`eventType`](/help/collection/js/commands/sendevent/eventtype.md).
* **[!UICONTROL XDM]**: payload XDM da inviare ad Adobe. In questo campo è possibile utilizzare un oggetto [XDM](../data-element-types.md#xdm-object) o una [variabile](../data-element-types.md#variable). Se sono presenti regole che popolano più oggetti XDM, è possibile utilizzare [oggetti uniti](../../core/overview.md#merged-objects) per combinarli.
* **[!UICONTROL Data]**: payload di dati da inviare ad Adobe. Alcune app e servizi non richiedono l’aderenza a uno schema XDM, ad esempio Adobe Analytics o Adobe Target. Utilizza un tipo di elemento dati [Variable](../data-element-types.md#variable) per questo campo.
* **[!UICONTROL Include rendered propositions]**: abilitare questa casella di controllo per utilizzare questo evento come evento di visualizzazione, incluse le proposte visualizzate quando &quot;invia automaticamente un evento di visualizzazione&quot; è stato deselezionato. Il campo XDM `_experience.decisioning` viene compilato con informazioni sulla personalizzazione di cui è stato eseguito il rendering.
* **[!UICONTROL Document will unload]**: abilitare questa casella di controllo per assicurarsi che l&#39;evento raggiunga il server anche se l&#39;utente si sposta dalla pagina. Questa impostazione consente agli eventi di raggiungere il server, ma le risposte di Edge Network vengono ignorate.
* **[!UICONTROL Merge ID]** _(obsoleto)_: popola il campo XDM `eventMergeId`.

## Campi di personalizzazione

![Immagine dell&#39;interfaccia utente Tag di Experience Platform con le impostazioni di Personalization per il tipo di azione Invia evento.](../assets/personalization-settings.png)

* **[!UICONTROL Scopes]**: Array di ambiti che si desidera richiedere esplicitamente alla personalizzazione. Puoi immettere gli ambiti manualmente o fornire un elemento dati. Quando si immettono manualmente gli ambiti, ogni campo rappresenta un ambito. Selezionare **[!UICONTROL Add scope]** per aggiungere altri ambiti all&#39;azione.
* **[!UICONTROL Surfaces]**: Array di superfici da interrogare con l&#39;evento. Per ulteriori informazioni, consulta [Creare esperienze Web](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) nella documentazione di Adobe Journey Optimizer. Quando si immettono manualmente le superfici, ogni campo rappresenta una superficie. Selezionare **[!UICONTROL Add surface]** per aggiungere altre superfici all&#39;azione.
* **Decisioni di personalizzazione visiva:** casella di controllo che, se abilitata, consente di eseguire il rendering del contenuto personalizzato nella pagina. Per ulteriori informazioni, vedere [Rendering automatico delle azioni DOM](/help/collection/use-cases/personalization/render-auto-pers-content.md).
* **[!UICONTROL Request default personalization]**: controlla se sono richiesti l&#39;ambito a livello di pagina e la superficie predefinita. Per impostazione predefinita, viene richiesto automaticamente durante la prima chiamata `sendEvent` del caricamento della pagina. La libreria JavaScript equivalente a questi pulsanti di scelta è [`requestDefaultPersonalization`](/help/collection/js/commands/sendevent/personalization.md). Puoi scegliere tra le seguenti opzioni:
   * **[!UICONTROL Automatic]**: comportamento predefinito. Richiedi la personalizzazione predefinita solo se non è ancora stata richiesta.
   * **[!UICONTROL Enabled]**: richiede esplicitamente l&#39;ambito della pagina e la superficie predefinita. Questo aggiorna la cache della vista SPA.
   * **[!UICONTROL Disabled]**: soppressione esplicita della richiesta per l&#39;ambito pagina e la superficie predefinita.
* **[!UICONTROL Decision context]**: mappa chiave-valore utilizzata durante la valutazione dei set di regole di Adobe Journey Optimizer per le decisioni sul dispositivo. Puoi fornire il contesto decisionale manualmente o tramite un elemento dati.

## Campi Advertising

![L&#39;interfaccia utente dei tag di Experience Platform mostra le impostazioni pubblicitarie per l&#39;azione Invia evento](../assets/send-event-advertising.png)

* **[!UICONTROL Request default advertising data]**: determina quando (o se) la libreria aggiunge informazioni pubblicitarie al payload XDM. Puoi scegliere tra le seguenti opzioni:
   * **[!UICONTROL Automatic]**: tutti i dati pubblicitari disponibili al momento dell&#39;evento vengono aggiunti al payload dell&#39;evento.
   * **[!UICONTROL Wait]**: ritardare l&#39;invio dell&#39;evento fino alla ricezione dei dati pubblicitari.
   * **[!UICONTROL Disabled]**: non aggiungere dati pubblicitari al payload dell&#39;evento. Seleziona questa opzione se la tua implementazione non utilizza Adobe Analytics o Customer Journey Analytics.

## Override della configurazione dello stream di dati

Questo comando supporta le sostituzioni della configurazione dello stream di dati, consentendoti di controllare quali app e servizi ricevono i dati. Quando imposti una sostituzione della configurazione dello stream di dati sia in un singolo comando che all’interno delle impostazioni di configurazione dell’estensione tag, il singolo comando ha la precedenza. Per ulteriori informazioni, vedere [Override della configurazione Datastream](../configure/configuration-overrides.md).
