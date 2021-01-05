---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;class;classes;
solution: Experience Platform
title: Creazione e modifica di classi nell'interfaccia utente
description: Scoprite come creare e modificare le classi nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---


# Creazione e modifica di classi nell&#39;interfaccia utente

In Experience Data Model (XDM), le classi definiscono gli aspetti comportamentali dei dati che uno schema conterrà (record o serie temporali). Inoltre, le classi descrivono il minor numero di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per l&#39;unione di più set di dati compatibili.

 Adobe fornisce diverse classi XDM standard (&quot;core&quot;), tra cui [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Oltre a queste classi di base, è anche possibile creare classi personalizzate per descrivere casi di utilizzo più specifici per l&#39;organizzazione.

Questo documento fornisce una panoramica su come creare, modificare e gestire le classi personalizzate nell&#39;interfaccia utente di Adobe Experience Platform.

## Prerequisiti

Questa guida richiede una buona conoscenza del sistema XDM. Fare riferimento alla [panoramica XDM](../../home.md) per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema  Experience Platform, e alle [nozioni di base della composizione dello schema](../../schema/composition.md) per scoprire in che modo le classi contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire dimestichezza con le diverse funzionalità di [!DNL Schema Editor].

## Creare una nuova classe {#create}

Nell&#39;area di lavoro **[!UICONTROL Schemas]**, selezionare **[!UICONTROL Create schema]**, quindi selezionare **[!UICONTROL Browse]** dal menu a discesa.

![](../../images/ui/resources/classes/browse-classes.png)

Viene visualizzata una finestra di dialogo che consente di selezionare da un elenco di classi disponibili. Nella parte superiore della finestra di dialogo, selezionare **[!UICONTROL Create new class]**. È quindi possibile assegnare alla nuova classe un nome visualizzato (un nome breve, descrittivo, univoco e di facile utilizzo per la classe), una descrizione e un comportamento per i dati che lo schema definirà (&quot;[!UICONTROL Record]&quot; o &quot;[!UICONTROL Time-series]&quot;).

Al termine, selezionare **[!UICONTROL Assign class]**.

![](../../images/ui/resources/classes/class-details.png)

Viene visualizzato il [!DNL Schema Editor], che mostra un nuovo schema nel quadro basato sulla classe personalizzata appena creata. Poiché non è ancora stato aggiunto alcun campo alla classe, lo schema contiene solo un campo `_id`, che rappresenta l&#39;identificatore univoco generato dal sistema che viene applicato automaticamente a tutte le risorse della [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Durante la creazione di uno schema che implementa una classe definita dall&#39;organizzazione, tenere presente che i mixin sono disponibili solo per le classi compatibili. Poiché la classe definita è nuova, nella finestra di dialogo **[!UICONTROL Add mixin]** non sono elencati mixin modo compatibile. Al contrario, sarà necessario [creare nuovi mixin](./mixins.md#create) da utilizzare con tale classe. Al successivo comporre uno schema che implementa la nuova classe, i mixin definiti verranno elencati e saranno disponibili per l&#39;uso.

È ora possibile iniziare ad aggiungere [campi alla classe](#add-fields), che verrà condivisa da tutti gli schemi che utilizzano la classe.

## Modificare una classe esistente {#edit}

>[!NOTE]
>
>È possibile modificare solo le classi personalizzate definite dall&#39;organizzazione.
>
>Inoltre, una volta che una classe è stata salvata e utilizzata per l&#39;inserimento dei dati, è possibile apportare solo modifiche aggiuntive. Per ulteriori informazioni, vedere le [regole dell&#39;evoluzione dello schema](../../schema/composition.md#evolution).

Per modificare una classe esistente, selezionare la scheda **[!UICONTROL Browse]**, quindi selezionare il nome di uno schema che utilizza la classe da modificare.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>È possibile utilizzare le funzionalità di ricerca e filtro dell&#39;area di lavoro per facilitare la ricerca dello schema. Per ulteriori informazioni, consulta la guida [Esplora risorse XDM](../explore.md).

Viene visualizzata la [!DNL Schema Editor], con la struttura dello schema visualizzata nell&#39;area di lavoro. È ora possibile iniziare [aggiungendo campi alla classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Aggiunta di campi a una classe {#add-fields}

Una volta che si dispone di uno schema che utilizza una classe personalizzata aperta in [!UICONTROL Schema Editor], è possibile iniziare ad aggiungere campi alla classe. Per aggiungere un nuovo campo, selezionare l&#39;icona **più (+)** accanto al nome dello schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Tenere presente che tutti i campi aggiunti a una classe verranno utilizzati in tutti gli schemi che utilizzano tale classe. È quindi necessario considerare attentamente quali campi saranno utili in tutti i casi di utilizzo dello schema. Se si sta pensando di aggiungere un campo che potrebbe essere visualizzato solo in alcuni schemi di questa classe, è consigliabile aggiungerlo a tali schemi [creando un mixin](./mixins.md#create).

Nell&#39;area di lavoro viene visualizzato un **[!UICONTROL New field]** e la barra laterale destra viene aggiornata per mostrare i controlli per la configurazione delle proprietà del campo. Per istruzioni su come configurare e aggiungere il campo alla classe, vedere la guida relativa alla [definizione dei campi nell&#39;interfaccia utente](../fields/overview.md#define).

Continuate ad aggiungere tutti i campi necessari alla classe. Al termine, selezionare **[!UICONTROL Save]** per salvare sia lo schema che la classe.

![](../../images/ui/resources/classes/save.png)

Se in precedenza sono stati creati schemi che utilizzano questa classe, i nuovi campi aggiunti verranno visualizzati automaticamente in tali schemi.

## Modificare la classe di uno schema {#schema}

È possibile modificare la classe dello schema in qualsiasi momento durante il processo di creazione iniziale prima che sia stato salvato. Per ulteriori informazioni, consulta la guida [creazione e modifica di schemi](./schemas.md#change-class).

## Passaggi successivi

Questo documento descrive come creare e modificare le classi utilizzando l&#39;interfaccia utente della piattaforma. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemas]](../overview.md).

Per informazioni su come gestire le classi utilizzando l&#39;API [!DNL Schema Registry], vedere la guida [endpoint classi](../../api/classes.md).