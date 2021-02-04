---
keywords: ' Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;mixin;mixin;'
solution: Experience Platform
title: Creazione e modifica di mixin nell’interfaccia utente
description: Scopri come creare e modificare i mixin nell’interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: cf74c7922271035474c7f10534692983add48616
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Creazione e modifica di mixin nell’interfaccia utente

In Experience Data Model (XDM), i mixin sono componenti riutilizzabili che definiscono uno o più campi che implementano determinate funzioni come dettagli personali, preferenze alberghiere o indirizzi. Le mixine sono destinate ad essere incluse come parte di uno schema che implementa una classe compatibile.

Un mixin definisce con quali classi è compatibile, in base al comportamento dei dati che il mixin rappresenta (record o serie temporali). Ciò significa che non tutti i mixin sono disponibili per l&#39;uso con tutte le classi.

Adobe Experience Platform offre molti mixin standard che coprono un&#39;ampia gamma di casi d&#39;uso di marketing. Tuttavia, potete anche creare e modificare i vostri mixin personalizzati per definire concetti aggiuntivi relativi alla vostra attività all&#39;interno degli schemi XDM. Questa guida fornisce una panoramica su come creare, modificare e gestire i mixin personalizzati per la vostra organizzazione nell&#39;interfaccia utente della piattaforma.

## Prerequisiti

Questa guida richiede una buona conoscenza del sistema XDM. Per un&#39;introduzione al ruolo di XDM nell&#39;ecosistema  Experience Platform, fare riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base della composizione dello schema](../../schema/composition.md) per vedere in che modo i mixin contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire dimestichezza con le diverse funzionalità di [!DNL Schema Editor].

## Creare un nuovo mixin {#create}

Per creare un nuovo mixin, è innanzitutto necessario selezionare uno schema a cui verrà aggiunto il mixin. È possibile scegliere di [creare un nuovo schema](./schemas.md#create) o [selezionare uno schema esistente da modificare](./schemas.md#edit).

Dopo aver aperto lo schema in [!DNL Schema Editor], selezionare **[!UICONTROL Add]** accanto alla sezione [!UICONTROL Mixins] nella barra a sinistra.

![](../../images/ui/resources/mixins/add-mixin-button.png)

Viene visualizzata una finestra di dialogo con un elenco dei mixin esistenti per l’organizzazione. Nella parte superiore della finestra di dialogo, selezionare **[!UICONTROL Create new mixin]**. Qui è possibile specificare **[!UICONTROL Display name]** e **[!UICONTROL Description]** per il mixin. Al termine, selezionare **[!UICONTROL Add mixin]**.

![](../../images/ui/resources/mixins/create-mixin.png)

La [!DNL Schema Editor] viene visualizzata di nuovo, con il nuovo mixin elencato nella barra a sinistra. Poiché si tratta di un mixin completamente nuovo, al momento non fornisce alcun campo allo schema, pertanto il quadro rimane invariato. È ora possibile iniziare [aggiungendo campi al mixin](#add-fields).

## Modificare un mixin esistente {#edit}

>[!NOTE]
>
>È possibile modificare e personalizzare solo i mixin personalizzati definiti dall’organizzazione. Per i mixin di base definiti da  Adobe, solo i nomi visualizzati per i relativi campi possono essere modificati nel contesto dei singoli schemi. Per ulteriori informazioni, vedere la sezione relativa alla [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names).
>
>Dopo aver salvato e utilizzato un mixin personalizzato in uno schema per l&#39;inserimento dei dati, è possibile apportare solo modifiche aggiuntive al mixin in seguito. Per ulteriori informazioni, vedere le [regole dell&#39;evoluzione dello schema](../../schema/composition.md#evolution).

Per modificare un mixin esistente, è innanzitutto necessario aprire uno schema che utilizza il mixin all&#39;interno di [!DNL Schema Editor]. È possibile [selezionare uno schema esistente da modificare](./schemas.md#edit) oppure [creare un nuovo schema](./schemas.md#create) e aggiungere il mixin in questione.

Una volta aperto lo schema nell&#39;editor, è possibile iniziare ad aggiungere i campi al mixin](#add-fields).[

## Aggiungere campi a un mixin {#add-fields}

Per aggiungere campi a un mixin in [!DNL Schema Editor], iniziate selezionando il nome del mixin nella barra a sinistra, quindi selezionate l&#39;icona **più (+)** accanto al nome dello schema nel quadro.

![](../../images/ui/resources/mixins/add-field-button.png)

Nell&#39;area di lavoro viene visualizzato un **[!UICONTROL New field]** e la barra laterale destra viene aggiornata per mostrare i controlli per la configurazione delle proprietà del campo. Per istruzioni su come configurare e aggiungere il campo al mixin, consultate la guida sulla [definizione dei campi nell&#39;interfaccia utente](../fields/overview.md#define).

Continuate ad aggiungere tutti i campi necessari al mixin. Al termine, selezionare **[!UICONTROL Save]** per salvare sia lo schema che il mixin.

![](../../images/ui/resources/mixins/complete-mixin.png)

Se lo stesso mixin è già utilizzato in altri schemi, i nuovi campi aggiunti verranno automaticamente visualizzati in tali schemi.

## Passaggi successivi

Questa guida descrive come creare e modificare i mixin utilizzando l&#39;interfaccia utente della piattaforma. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemas]](../overview.md).

Per informazioni su come gestire i mixin utilizzando l&#39;API [!DNL Schema Registry], consulta la [guida dell&#39;endpoint dei mixin](../../api/mixins.md).