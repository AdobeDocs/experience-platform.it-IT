---
title: Panoramica dell’estensione Meta Pixel
description: Scopri l’estensione tag Meta Pixel in Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# [!DNL Meta Pixel] panoramica dell&#39;estensione

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) è uno strumento di analisi basato su JavaScript che consente di monitorare l’attività dei visitatori sul sito web. Le azioni dei visitatori a cui hai tracciato (chiamate conversioni) vengono inviate [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) dove possono essere utilizzati per misurare l’efficacia degli annunci, delle campagne, dei funnel di conversione e altro ancora.

La [!DNL Meta Pixel] l’estensione tag consente di sfruttare [!DNL Pixel] funzionalità nelle librerie di tag lato client. Questo documento illustra come installare l&#39;estensione e utilizzarne le funzionalità in un [regola](../../../ui/managing-resources/rules.md).

## Prerequisiti

Per utilizzare l&#39;estensione, è necessario disporre di un [!DNL Meta] account con accesso a [!DNL Ads Manager]. In particolare, devi [creare una nuova [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) e copia le sue [!DNL Pixel ID] in modo che l&#39;estensione possa essere configurata sul tuo account. Se esiste già un [!DNL Meta Pixel], invece puoi utilizzarne l’ID.

Si consiglia vivamente di utilizzare [!DNL Meta Pixel] in combinazione con [!DNL Meta Conversions API] per condividere e inviare gli stessi eventi dal lato client e dal lato server, rispettivamente, in quanto ciò potrebbe aiutare a recuperare gli eventi che non sono stati rilevati da [!DNL Meta Pixel]. Consulta la guida [[!DNL Meta Conversions API] estensione per l&#39;inoltro eventi](../../client/meta/overview.md) per informazioni su come integrarlo nelle implementazioni lato server. Tieni presente che la tua organizzazione deve avere accesso a [inoltro eventi](../../../ui/event-forwarding/overview.md) per utilizzare l&#39;estensione lato server.

## Installare l’estensione

Per installare [!DNL Meta Pixel] , passa all’interfaccia utente di raccolta dati o di Experience Platform e seleziona **[!UICONTROL Tag]** dalla navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione oppure crea una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, seleziona il **[!UICONTROL Catalogo]** scheda . Cerca il [!UICONTROL Meta pixel] scheda , quindi seleziona **[!UICONTROL Installa]**.

![La [!UICONTROL Installa] pulsante selezionato per [!UICONTROL Meta pixel] estensione nell’interfaccia utente di raccolta dati.](../../../images/extensions/client/meta/install.png)

Nella visualizzazione di configurazione visualizzata, devi fornire [!DNL Pixel] ID copiato in precedenza per collegare l&#39;estensione al tuo account . Puoi incollare l’ID direttamente nell’input oppure puoi selezionare un elemento dati esistente.

>[!TIP]
>
>L’utilizzo di un elemento dati consente di modificare dinamicamente la variabile [!DNL Pixel] ID utilizzato a seconda di altri fattori, ad esempio l’ambiente di creazione. Vedi la sezione dell&#39;appendice su [utilizzando diversi [!DNL Pixel] ID per ambienti diversi](#id-data-element) per ulteriori informazioni.

Facoltativamente, puoi anche fornire un ID evento da associare all&#39;estensione. Viene utilizzato per deduplicare eventi identici tra [!DNL Meta Pixel] e [!DNL Meta Conversions API]. Per informazioni dettagliate, consulta la sezione [deduplicazione degli eventi](../../server/meta/overview.md#event-deduplication) in panoramica per [!DNL Conversions API] estensione.

Al termine, seleziona **[!UICONTROL Salva]**

![La [!DNL Pixel] ID fornito come elemento dati nella visualizzazione di configurazione dell&#39;estensione.](../../../images/extensions/client/meta/configure.png)

L’estensione è installata e ora puoi utilizzarne varie azioni nelle regole dei tag.

## Configurare una regola di tag {#rule}

[!DNL Meta Pixel] accetta un insieme di [eventi standard](https://www.facebook.com/business/help/402791146561655), ciascuno con i propri contesti e proprietà accettate. Le azioni della regola fornite dal [!DNL Pixel] l&#39;estensione è correlata a questi tipi di evento, che consentono di categorizzare e configurare facilmente l&#39;evento a cui si invia [!DNL Meta] a seconda del tipo.

A scopo dimostrativo, questa sezione mostra come creare una regola che invia un evento di visualizzazione della pagina a [!DNL Meta].

Inizia a creare una nuova regola di tag e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Meta pixel]** per l&#39;estensione , quindi seleziona **[!UICONTROL Invia visualizzazione pagina]** per il tipo di azione.

![La [!UICONTROL Invia visualizzazione pagina] tipo di azione selezionato per una regola nell&#39;interfaccia utente Raccolta dati.](../../../images/extensions/client/meta/select-action.png)

Non è necessaria alcuna ulteriore configurazione per [!UICONTROL Invia visualizzazione pagina] azione. Seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Quando la regola è soddisfatta, seleziona **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo tag [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Conferma che [!DNL Meta] sta ricevendo dati

Dopo che la build aggiornata è stata distribuita sul sito web, puoi verificare se i dati vengono inviati come previsto generando alcuni eventi di conversione sul browser e verificare se tali eventi compaiono in [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Meta] utilizzando [!DNL Meta Pixel] estensione tag. Se prevedi di inviare anche eventi lato server a [!DNL Meta], ora puoi procedere all’installazione e alla configurazione del [[!DNL Conversions API] estensione di inoltro eventi](../../server/meta/overview.md).

Per ulteriori informazioni sui tag nell’Experience Platform, consulta [panoramica dei tag](../../../home.md).

## Appendice: Usa diversi [!DNL Pixel] ID per ambienti diversi {#id-data-element}

Se desideri testare l&#39;implementazione in ambienti di sviluppo o di staging mantenendo la produzione [!DNL Meta Pixel] analytics intatto, puoi utilizzare un elemento dati per scegliere in modo dinamico un appropriato [!DNL Pixel] ID a seconda dell&#39;ambiente utilizzato.

A questo scopo è possibile utilizzare un [!UICONTROL Codice personalizzato] elemento dati (fornito da [[!UICONTROL Core] estensione](../core/overview.md)) in combinazione con [`turbine` variabile gratuita](../../../extension-dev/turbine.md). Nel codice JavaScript dell&#39;elemento dati, utilizza il `turbine` per trovare la fase dell&#39;ambiente corrente, quindi restituire un [!DNL Pixel] ID in base al risultato.

L&#39;esempio seguente restituisce un ID produzione falso `exampleProductionKey` se utilizzato nell&#39;ambiente di produzione, e un ID diverso `exampleTestKey` quando viene utilizzato qualsiasi altro ambiente. Quando implementi questo codice, sostituisci ogni valore con la produzione e il test effettivi [!DNL Pixel] ID.

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
