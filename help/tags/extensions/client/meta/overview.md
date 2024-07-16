---
title: Panoramica dell’estensione Meta Pixel
description: Scopri l’estensione tag Meta Pixel in Adobe Experience Platform.
exl-id: c5127bbc-6fe7-438f-99f1-6efdbe7d092e
source-git-commit: 24001da61306a00d295bf9441c55041e20f488c0
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 0%

---

# Panoramica dell&#39;estensione [!DNL Meta Pixel]

[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) è uno strumento di analisi basato su JavaScript che consente di tenere traccia dell&#39;attività dei visitatori sul sito Web. Le azioni dei visitatori che tieni traccia (dette conversioni) vengono inviate a [[!DNL Ads Manager]](https://www.facebook.com/business/tools/ads-manager) dove possono essere utilizzate per misurare l&#39;efficacia dei tuoi annunci, campagne, funnel di conversione e altro ancora.

L&#39;estensione tag [!DNL Meta Pixel] consente di sfruttare le funzionalità di [!DNL Pixel] nelle librerie tag lato client. Questo documento illustra come installare l&#39;estensione e utilizzarne le funzionalità in una [regola](../../../ui/managing-resources/rules.md).

## Prerequisiti

Per utilizzare l&#39;estensione, è necessario disporre di un account [!DNL Meta] valido con accesso a [!DNL Ads Manager]. In particolare, devi [creare un nuovo [!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755) e copiarne [!DNL Pixel ID] in modo che l&#39;estensione possa essere configurata sul tuo account. Se disponi già di un [!DNL Meta Pixel], puoi utilizzare il relativo ID.

Si consiglia vivamente di utilizzare [!DNL Meta Pixel] in combinazione con [!DNL Meta Conversions API] per condividere e inviare gli stessi eventi rispettivamente dal lato client e dal lato server, in quanto ciò potrebbe aiutare a ripristinare eventi non raccolti da [!DNL Meta Pixel]. Consulta la guida sull&#39;estensione [[!DNL Meta Conversions API] per l&#39;inoltro degli eventi](../../client/meta/overview.md) per i passaggi su come integrarla nelle implementazioni lato server. La tua organizzazione deve avere accesso a [inoltro eventi](../../../ui/event-forwarding/overview.md) per poter utilizzare l&#39;estensione lato server.

## Installare l’estensione

Per installare l&#39;estensione [!DNL Meta Pixel], passa all&#39;interfaccia utente di Data Collection o all&#39;interfaccia utente Experience Platform e seleziona **[!UICONTROL Tag]** dal menu di navigazione a sinistra. Da qui, seleziona una proprietà a cui aggiungere l’estensione o creane una nuova.

Dopo aver selezionato o creato la proprietà desiderata, seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra, quindi seleziona la scheda **[!UICONTROL Catalogo]**. Cerca la scheda [!UICONTROL Meta Pixel], quindi seleziona **[!UICONTROL Installa]**.

![Pulsante [!UICONTROL Installa] selezionato per l&#39;estensione [!UICONTROL Meta Pixel] nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/client/meta/install.png)

Nella vista di configurazione visualizzata, devi fornire l&#39;ID [!DNL Pixel] copiato in precedenza per collegare l&#39;estensione al tuo account. Puoi incollare l’ID direttamente nell’input, oppure selezionare un elemento dati esistente.

>[!TIP]
>
>L&#39;utilizzo di un elemento dati consente di modificare dinamicamente l&#39;ID [!DNL Pixel] utilizzato a seconda di altri fattori, ad esempio l&#39;ambiente di build. Per ulteriori informazioni, consulta la sezione dell&#39;appendice su [utilizzo di  [!DNL Pixel] ID diversi](#id-data-element) per ambienti diversi.

Facoltativamente, puoi anche fornire un ID evento da associare all’estensione. Utilizzato per deduplicare eventi identici tra [!DNL Meta Pixel] e [!DNL Meta Conversions API]. Per informazioni dettagliate, vedere la sezione relativa alla [deduplicazione degli eventi](../../server/meta/overview.md#event-deduplication) nella panoramica dell&#39;estensione [!DNL Conversions API].

Al termine, seleziona **[!UICONTROL Salva]**

![L&#39;ID [!DNL Pixel] fornito come elemento dati nella vista di configurazione dell&#39;estensione.](../../../images/extensions/client/meta/configure.png)

L’estensione è installata e ora puoi utilizzarne le varie azioni nelle regole dei tag.

## Configurare una regola di tag {#rule}

[!DNL Meta Pixel] accetta un set di [eventi standard](https://www.facebook.com/business/help/402791146561655) predefiniti, ciascuno con i propri contesti e le proprietà accettate. Le azioni della regola fornite dall&#39;estensione [!DNL Pixel] sono correlate a questi tipi di evento, consentendo di categorizzare e configurare facilmente l&#39;evento inviato a [!DNL Meta] in base al relativo tipo.

A scopo dimostrativo, in questa sezione viene illustrato come creare una regola che invia un evento di visualizzazione della pagina a [!DNL Meta].

Inizia a creare una nuova regola di tag e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona **[!UICONTROL Meta Pixel]** per l&#39;estensione, quindi seleziona **[!UICONTROL Invia visualizzazione pagina]** per il tipo di azione.

![Tipo di azione [!UICONTROL Invia visualizzazione pagina] selezionato per una regola nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/client/meta/select-action.png)

Non sono richieste ulteriori configurazioni per l&#39;azione [!UICONTROL Invia visualizzazione pagina]. Seleziona **[!UICONTROL Mantieni modifiche]** per aggiungere l&#39;azione alla configurazione della regola. Una volta soddisfatta la regola, selezionare **[!UICONTROL Salva nella libreria]**.

Infine, pubblica un nuovo tag [build](../../../ui/publishing/builds.md) per abilitare le modifiche alla libreria.

## Conferma che [!DNL Meta] sta ricevendo dati

Dopo aver distribuito la build aggiornata al sito Web, è possibile verificare se i dati vengono inviati come previsto generando alcuni eventi di conversione nel browser e verificando se tali eventi vengono visualizzati in [[!DNL Meta Events Manager]](https://www.facebook.com/business/help/898185560232180).

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Meta] utilizzando l&#39;estensione tag [!DNL Meta Pixel]. Se si prevede di inviare eventi lato server anche a [!DNL Meta], è ora possibile procedere all&#39;installazione e alla configurazione dell&#39;[[!DNL Conversions API] estensione inoltro eventi](../../server/meta/overview.md).

Per ulteriori informazioni sui tag in Experience Platform, consulta la [panoramica dei tag](../../../home.md).

## Appendice: utilizzare ID [!DNL Pixel] diversi per ambienti diversi {#id-data-element}

Se desideri testare l&#39;implementazione in ambienti di sviluppo o di staging mantenendo intatte le analisi di [!DNL Meta Pixel] di produzione, puoi utilizzare un elemento dati per scegliere in modo dinamico un ID [!DNL Pixel] appropriato a seconda dell&#39;ambiente in uso.

È possibile ottenere questo risultato utilizzando un elemento dati [!UICONTROL Custom Code] (fornito dall&#39;estensione [[!UICONTROL Core]](../core/overview.md)) in combinazione con la variabile libera [`turbine`](../../../extension-dev/turbine.md). Nel codice JavaScript dell&#39;elemento dati, utilizzare l&#39;oggetto `turbine` per trovare la fase dell&#39;ambiente corrente, quindi restituire un ID [!DNL Pixel] appropriato in base al risultato.

L&#39;esempio seguente restituisce un ID di produzione falso `exampleProductionKey` quando viene utilizzato nell&#39;ambiente di produzione e un ID diverso `exampleTestKey` quando viene utilizzato qualsiasi altro ambiente. Quando implementi questo codice, sostituisci ogni valore con la produzione effettiva e verifica gli ID [!DNL Pixel].

```js
return (turbine.environment.stage === "production" ? 'exampleProductionKey' : 'exampleTestKey');
```
