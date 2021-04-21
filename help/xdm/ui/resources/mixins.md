---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;mixin;mixin;
solution: Experience Platform
title: Creare e modificare mixin nell’interfaccia utente
description: Scopri come creare e modificare i mixin nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 240b857d-75ad-42fd-9249-050cbc5306a9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Creare e modificare i mixin nell’interfaccia utente

In Experience Data Model (XDM), i mixin sono componenti riutilizzabili che definiscono uno o più campi che implementano determinate funzioni quali dettagli personali, preferenze alberghiere o indirizzo. I mixin devono essere inclusi come parte di uno schema che implementa una classe compatibile.

Un mixin definisce con quali classi è compatibile, in base al comportamento dei dati che il mixin rappresenta (record o serie temporali). Ciò significa che non tutti i mixin sono disponibili per l&#39;uso con tutte le classi.

Adobe Experience Platform fornisce molti mixin standard che coprono un&#39;ampia gamma di casi d&#39;uso di marketing. Tuttavia, puoi anche creare e modificare i tuoi mixin personalizzati per definire concetti aggiuntivi relativi alla tua attività all’interno dei tuoi schemi XDM. Questa guida fornisce una panoramica su come creare, modificare e gestire mixin personalizzati per la tua organizzazione nell’interfaccia utente di Platform.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema Experience Platform, fai riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base sulla composizione dello schema](../../schema/composition.md) per sapere in che modo i mixin contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità di [!DNL Schema Editor].

## Crea un nuovo mixin {#create}

Per creare un nuovo mixin, devi innanzitutto selezionare uno schema a cui verrà aggiunto il mixin. È possibile scegliere di [creare un nuovo schema](./schemas.md#create) o [selezionare uno schema esistente da modificare](./schemas.md#edit).

Una volta aperto lo schema in [!DNL Schema Editor], seleziona **[!UICONTROL Add]** accanto alla sezione [!UICONTROL Mixins] nella barra a sinistra.

![](../../images/ui/resources/mixins/add-mixin-button.png)

Viene visualizzata una finestra di dialogo che mostra un elenco dei mixin esistenti per la tua organizzazione. Nella parte superiore della finestra di dialogo, seleziona **[!UICONTROL Create new mixin]**. Qui puoi fornire un **[!UICONTROL Display name]** e **[!UICONTROL Description]** per il mixin. Al termine, seleziona **[!UICONTROL Add mixin]**.

![](../../images/ui/resources/mixins/create-mixin.png)

Il [!DNL Schema Editor] viene rivisualizzato, con il nuovo mixin elencato nella barra a sinistra. Poiché si tratta di un mixin nuovo, al momento non fornisce alcun campo allo schema, e quindi l’area di lavoro rimane invariata. Ora puoi iniziare [aggiungendo campi al mixin](#add-fields).

## Modifica un mixin esistente {#edit}

>[!NOTE]
>
>Solo i mixin personalizzati definiti dall’organizzazione possono essere modificati e personalizzati completamente. Per i mixin di base definiti dall’Adobe, solo i nomi visualizzati dei relativi campi possono essere modificati nel contesto dei singoli schemi. Per ulteriori informazioni, consulta la sezione sulla [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names) .
>
>Una volta salvato e utilizzato un mixin personalizzato in uno schema per l’inserimento dei dati, è possibile apportare solo modifiche aggiuntive al mixin in seguito. Per ulteriori informazioni, consulta le [regole di evoluzione dello schema](../../schema/composition.md#evolution) .

Per modificare un mixin esistente, devi prima aprire uno schema che utilizza il mixin all&#39;interno di [!DNL Schema Editor]. È possibile [selezionare uno schema esistente da modificare](./schemas.md#edit) oppure [creare un nuovo schema](./schemas.md#create) e aggiungere il mixin in questione.

Una volta aperto lo schema nell&#39;editor, puoi iniziare ad aggiungere i campi [al mixin](#add-fields).

## Aggiungi campi a un mixin {#add-fields}

Per aggiungere campi a un mixin in [!DNL Schema Editor], inizia selezionando il nome del mixin nella barra a sinistra, quindi seleziona l&#39;icona **più (+)** accanto al nome dello schema nell&#39;area di lavoro.

![](../../images/ui/resources/mixins/add-field-button.png)

Nell’area di lavoro viene visualizzato un **[!UICONTROL New field]** e la barra a destra viene aggiornata per mostrare i controlli necessari per configurare le proprietà del campo. Per passaggi specifici su come configurare e aggiungere il campo al mixin, consulta la guida [Definizione dei campi nell&#39;interfaccia utente](../fields/overview.md#define) .

Continua ad aggiungere tutti i campi necessari al mixin. Al termine, seleziona **[!UICONTROL Save]** per salvare sia lo schema che il mixin.

![](../../images/ui/resources/mixins/complete-mixin.png)

Se lo stesso mixin è già utilizzato in altri schemi, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Passaggi successivi

Questa guida illustra come creare e modificare i mixin utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], consulta la [[!UICONTROL Schemas] panoramica dell&#39;area di lavoro](../overview.md).

Per informazioni su come gestire i mixin utilizzando l&#39;API [!DNL Schema Registry], consulta la [guida all&#39;endpoint mixins](../../api/mixins.md).
