---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;schema;schemas;
solution: Experience Platform
title: Creare e modificare schemi nell’interfaccia utente
description: Scoprite le nozioni di base su come creare e modificare gli schemi nell’interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: efa1d8efb26f4196f6724702784ccd13a9337a8a
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---


# Creare e modificare schemi nell’interfaccia utente

Questa guida fornisce una panoramica su come creare, modificare e gestire schemi di Experience Data Model (XDM) per la tua organizzazione nell&#39;interfaccia utente di Adobe Experience Platform.

>[!IMPORTANT]
>
>Gli schemi XDM sono estremamente personalizzabili e pertanto i passaggi necessari per creare uno schema possono variare a seconda del tipo di dati che si desidera acquisire dallo schema. Di conseguenza, questo documento copre solo le interazioni di base che è possibile eseguire con gli schemi nell&#39;interfaccia utente ed esclude i passaggi correlati quali la personalizzazione di classi, mixin, tipi di dati e campi.
>
>Per una panoramica completa del processo di creazione dello schema, seguire l&#39;esercitazione [sulla creazione dello schema](../../tutorials/create-schema-ui.md) per creare uno schema di esempio completo e acquisire dimestichezza con le numerose funzionalità della [!DNL Schema Editor].

## Prerequisiti

Questa guida richiede una buona conoscenza del sistema XDM. Per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema  Experience Platform, fare riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base della composizione dello schema](../../schema/composition.md) per una panoramica della struttura degli schemi.

## Creare un nuovo schema {#create}

Nell&#39;area di lavoro [!UICONTROL Schemas], selezionare **[!UICONTROL Create schema]** nell&#39;angolo superiore destro. Nel menu a discesa visualizzato, è possibile scegliere tra **[!UICONTROL XDM Individual Profile]** e **[!UICONTROL XDM ExperienceEvent]** come classe base per lo schema. In alternativa, è possibile selezionare **[!UICONTROL Browse]** per selezionare dall&#39;elenco completo delle classi disponibili oppure [creare una nuova classe personalizzata](./classes.md#create).

![](../../images/ui/resources/schemas/create-schema.png)

Dopo aver selezionato una classe, viene visualizzato il simbolo [!DNL Schema Editor] e la struttura di base dello schema (fornita dalla classe) viene visualizzata nell&#39;area di lavoro. Da qui, è possibile utilizzare la barra a destra per aggiungere un **[!UICONTROL Display name]** e **[!UICONTROL Description]** per lo schema.

![](../../images/ui/resources/schemas/schema-details.png)

È ora possibile iniziare a creare la struttura dello schema [aggiungendo mixin](#add-mixins).

## Modificare uno schema esistente {#edit}

>[!NOTE]
>
>Una volta che uno schema è stato salvato e utilizzato per l&#39;inserimento dei dati, è possibile apportare solo modifiche aggiuntive. Per ulteriori informazioni, vedere le [regole dell&#39;evoluzione dello schema](../../schema/composition.md#evolution).

Per modificare uno schema esistente, selezionare la scheda **[!UICONTROL Browse]**, quindi selezionare il nome dello schema da modificare.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>È possibile utilizzare le funzionalità di ricerca e filtro dell&#39;area di lavoro per facilitare la ricerca dello schema. Per ulteriori informazioni, consulta la guida [Esplora risorse XDM](../explore.md).

Dopo aver selezionato uno schema, il simbolo [!DNL Schema Editor] viene visualizzato con la struttura dello schema visualizzata nel quadro. Ora è possibile [aggiungere mixin](#add-mixins) allo schema, oppure [modificare mixin personalizzati esistenti](./mixins.md#edit) se lo schema ne utilizza uno.

## Aggiunta di mixaggi a uno schema {#add-mixins}

>[!NOTE]
>
>In questa sezione viene illustrato come aggiungere mixin esistenti a uno schema. Se desiderate creare un nuovo mixin personalizzato, consultate la guida alla [creazione e modifica di mixin](./mixins.md#create).

Dopo aver aperto uno schema all&#39;interno di [!DNL Schema Editor], è possibile aggiungere campi allo schema tramite l&#39;uso di mixin. Per iniziare, selezionare **[!UICONTROL Add]** accanto a **[!UICONTROL Mixins]** nella barra a sinistra.

![](../../images/ui/resources/schemas/add-mixin-button.png)

Nella finestra di dialogo visualizzata, potete selezionare i mixin desiderati dall’elenco. Potete selezionare più mixin dall’elenco, con ciascun mixin selezionato che appare nella barra a destra.

![](../../images/ui/resources/schemas/add-mixin.png)

>[!TIP]
>
>Per qualsiasi mixin elencato, potete selezionare l&#39;icona di anteprima (![](../../images/ui/resources/schemas/preview-icon.png)) per visualizzare la struttura dei campi forniti dal mixin prima di decidere di aggiungerlo allo schema.

Dopo aver scelto il mixin, selezionare **[!UICONTROL Add mixin]** per aggiungerli allo schema.

![](../../images/ui/resources/schemas/add-mixin-finish.png)

La [!DNL Schema Editor] viene visualizzata di nuovo con i campi forniti dal mixin rappresentati nel quadro.

![](../../images/ui/resources/schemas/mixins-added.png)

## Abilita uno schema per il profilo cliente in tempo reale {#profile}

[I ](../../../profile/home.md) profili cliente in tempo reale consentono di acquisire dati da fonti diverse per creare una visione completa di ogni singolo cliente. Se si desidera che i dati acquisiti da uno schema partecipino a questo processo, è necessario abilitare lo schema per l&#39;utilizzo in [!DNL Profile].

>[!IMPORTANT]
>
>Per abilitare uno schema per [!DNL Profile], è necessario che sia definito un campo di identità principale. Per ulteriori informazioni, vedere la guida relativa alla [definizione dei campi identità](../fields/identity.md).

Per abilitare lo schema, iniziare selezionando il nome dello schema nella barra a sinistra, quindi selezionare l&#39;opzione **[!UICONTROL Profile]** nella barra a destra.

![](../../images/ui/resources/schemas/profile-toggle.png)

Viene visualizzato un messaggio di avviso che avvisa che, una volta attivato e salvato, uno schema non può essere disabilitato. Selezionare **[!UICONTROL Enable]** per continuare.

![](../../images/ui/resources/schemas/profile-confirm.png)

Il quadro viene nuovamente visualizzato con l&#39;attivazione dell&#39;opzione [!UICONTROL Profile].

>[!IMPORTANT]
>
>Poiché lo schema non è ancora salvato, questo è il punto di non ritorno se si cambia idea di consentire allo schema di partecipare al profilo cliente in tempo reale: dopo aver salvato uno schema abilitato, non sarà più possibile disattivarlo. Selezionare di nuovo l&#39;opzione **[!UICONTROL Profile]** per disabilitare lo schema.

Per completare il processo, selezionare **[!UICONTROL Save]** per salvare lo schema.

![](../../images/ui/resources/schemas/profile-enabled.png)

Lo schema ora è abilitato per l&#39;uso in Real-time Customer Profile (Profilo cliente in tempo reale). Quando Platform (Piattaforma) trasferisce i dati in set di dati basati su questo schema, questi verranno incorporati nei dati del profilo amalgamato.

## Modificare la classe di uno schema {#change-class}

È possibile modificare la classe di uno schema in qualsiasi punto del processo di composizione iniziale prima che lo schema sia stato salvato.

>[!WARNING]
>
>La riassegnazione della classe per uno schema deve essere eseguita con estrema cautela. I mixin sono compatibili solo con determinate classi, pertanto la modifica della classe reimposterà il quadro e tutti i campi aggiunti.

Per riassegnare una classe, selezionate **[!UICONTROL Assign]** nella parte sinistra del quadro.

![](../../images/ui/resources/schemas/assign-class-button.png)

Viene visualizzata una finestra di dialogo in cui sono elencate tutte le classi disponibili, incluse quelle definite dall&#39;organizzazione (il proprietario è &quot;[!UICONTROL Customer]&quot;), nonché le classi standard definite dal Adobe .

Selezionate una classe dall’elenco per visualizzarne la descrizione sul lato destro della finestra di dialogo. Potete anche selezionare **[!UICONTROL Preview class structure]** per visualizzare i campi e i metadati associati alla classe. Selezionare **[!UICONTROL Assign class]** per continuare.

![](../../images/ui/resources/schemas/assign-class.png)

Viene visualizzata una nuova finestra di dialogo in cui viene richiesto di confermare l&#39;assegnazione di una nuova classe. Selezionare **[!UICONTROL Assign]** per confermare.

![](../../images/ui/resources/schemas/assign-confirm.png)

Dopo aver confermato la modifica della classe, il quadro verrà reimpostato e tutti i progressi della composizione andranno persi.

## Passaggi successivi

In questo documento sono state illustrate le nozioni di base per la creazione e la modifica degli schemi nell’interfaccia utente della piattaforma. È vivamente consigliato di consultare l&#39;esercitazione sulla creazione di [schemi](../../tutorials/create-schema-ui.md) per un flusso di lavoro completo per la creazione di uno schema completo nell&#39;interfaccia utente, inclusa la creazione di mixin personalizzati e di tipi di dati per casi di utilizzo univoci.

Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemas]](../overview.md).

Per informazioni su come gestire gli schemi nell&#39;API [!DNL Schema Registry], consulta la [guida dell&#39;endpoint degli schemi](../../api/schemas.md).