---
title: Panoramica dell’estensione Meta Pixel
description: Scopri l’estensione tag Meta Pixel in Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] panoramica dell’estensione

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) è uno strumento di analisi basato su JavaScript che consente di monitorare l’attività dei visitatori sul sito web. Le azioni dei visitatori di cui tieni traccia (denominate conversioni) vengono inviate a [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) dove possono essere utilizzati per misurare l’efficacia di annunci, campagne, funnel di conversione e altro ancora.

Il [!DNL Meta Pixel] estensione tag consente di sfruttare [!DNL Pixel] funzionalità nelle librerie di tag lato client. Questo documento illustra come installare l’estensione e utilizzarne le funzionalità in una [regola](../../../ui/managing-resources/rules.md).

## Prerequisiti

Per utilizzare l’estensione, è necessario disporre di un [!DNL Meta] account con accesso a [!DNL Ads Manager]. In particolare, devi [crea un nuovo [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) e copia i [!DNL Pixel ID] in modo che l’estensione possa essere configurata sul tuo account. Se disponi già di un [!DNL Meta Pixel], puoi invece utilizzare il relativo ID.

Si consiglia vivamente di utilizzare [!DNL Meta Pixel] in combinazione con [!DNL Meta Conversions API] per condividere e inviare gli stessi eventi rispettivamente dal lato client e dal lato server, in quanto ciò può aiutare a recuperare eventi che non sono stati raccolti da [!DNL Meta Pixel]. Consulta la guida sulla [[!DNL Meta Conversions API] estensione per l’inoltro di eventi](../../client/meta/overview.md) per i passaggi su come integrarlo nelle implementazioni lato server. Tieni presente che la tua organizzazione deve avere accesso a [inoltro eventi](../../../ui/event-forwarding/overview.md) per utilizzare l’estensione lato server.

## Installare l’estensione

Per installare [!DNL Meta Pixel] , passa all’interfaccia utente di Data Collection o all’interfaccia utente di Experience Platform e seleziona **[!UICONTROL Tag]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona quindi **[!UICONTROL Catalogo]** scheda. Cerca [!UICONTROL Meta Pixel] , quindi seleziona **[!UICONTROL Installa]**.

![Il [!UICONTROL Installa] pulsante selezionato per il [!UICONTROL Meta Pixel] nell’interfaccia utente di Data Collection.](../../../images/extensions/client/meta/install.png)

Nella vista di configurazione visualizzata, devi fornire [!DNL Pixel] ID copiato in precedenza per collegare l&#39;estensione al tuo account. Puoi incollare l’ID direttamente nell’input, oppure selezionare un elemento dati esistente.

>[!TIP]
>
>L’utilizzo di un elemento dati consente di modificare dinamicamente [!DNL Pixel] ID utilizzato a seconda di altri fattori, come l’ambiente di build. Vedere la sezione dell&#39;appendice relativa a [utilizzo di diversi [!DNL Pixel] ID per ambienti diversi](#id-data-element) per ulteriori informazioni.

Facoltativamente, puoi anche fornire un ID evento da associare all’estensione. Viene utilizzato per deduplicare eventi identici tra [!DNL Meta Pixel] e [!DNL Meta Conversions API]. Per ulteriori informazioni, consulta la sezione su [deduplicazione degli eventi](../../server/meta/overview.md#event-deduplication) in panoramica per [!DNL Conversions API] estensione.

Al termine, seleziona **[!UICONTROL Salva]**

![Il [!DNL Pixel] ID fornito come elemento dati nella vista di configurazione dell’estensione.](../../../images/extensions/client/meta/configure.png)

L’estensione è installata e ora puoi utilizzarne le varie azioni nelle regole dei tag.

## Configurare una regola di tag {#rule}

[!DNL Meta Pixel] accetta un set di predefiniti [eventi standard](https://www.facebook.com/business/help/402791146561655), ciascuno con i propri contesti e le proprietà accettate. Le azioni delle regole fornite da [!DNL Pixel] L&#39;estensione è correlata a questi tipi di evento, che consentono di categorizzare e configurare facilmente l&#39;evento a cui viene inviato [!DNL Meta] in base al tipo.

A scopo dimostrativo, questa sezione mostra come creare una regola che invia un evento di visualizzazione della pagina a [!DNL Meta].

Inizia a creare una nuova regola di tag e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Meta Pixel]** per l’estensione, seleziona **[!UICONTROL Invia visualizzazione pagina]** per il tipo di azione.

![Il [!UICONTROL Invia visualizzazione pagina] tipo di azione selezionato per una regola nell’interfaccia utente di Data Collection.](../../../images/extensions/client/meta/select-action.png)

Non è richiesta alcuna ulteriore configurazione per [!UICONTROL Invia visualizzazione pagina] azione. Seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l’azione alla configurazione della regola. Quando sei soddisfatto della regola, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo tag [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Conferma che [!DNL Meta] sta ricevendo dati

Dopo aver distribuito la build aggiornata al sito web, puoi confermare se i dati vengono inviati come previsto generando alcuni eventi di conversione sul browser e controllando se tali eventi compaiono in [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Meta] utilizzando [!DNL Meta Pixel] estensione tag. Se prevedi di inviare anche eventi lato server a [!DNL Meta], è ora possibile procedere all&#39;installazione e alla configurazione di [[!DNL Conversions API] estensione di inoltro eventi](../../server/meta/overview.md).

Per ulteriori informazioni sui tag in Experience Platform, consulta [panoramica sui tag](../../../home.md).

## Appendice: usa diversi [!DNL Pixel] ID per ambienti diversi {#id-data-element}

Se desideri testare l’implementazione in ambienti di sviluppo o di staging mantenendo la produzione [!DNL Meta Pixel] analytics intatto, puoi utilizzare un elemento dati per scegliere in modo dinamico un [!DNL Pixel] ID a seconda dell’ambiente in uso.

Per ottenere questo risultato, utilizza una [!UICONTROL Codice personalizzato] data element (fornito da [[!UICONTROL Core] estensione](../core/overview.md)) in combinazione con [`turbine` variabile libera](../../../extension-dev/turbine.md). Nel codice JavaScript dell&#39;elemento dati, utilizza `turbine` per trovare la fase dell&#39;ambiente corrente, quindi restituire un [!DNL Pixel] ID basato sul risultato.

L’esempio seguente restituisce un ID di produzione falso `exampleProductionKey` se utilizzato nell&#39;ambiente di produzione e un ID diverso `exampleTestKey` quando viene utilizzato qualsiasi altro ambiente. Quando implementi questo codice, sostituisci ogni valore con la produzione e il test effettivi [!DNL Pixel] ID.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
