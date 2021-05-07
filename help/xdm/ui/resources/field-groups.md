---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;area di lavoro;gruppo di campi;gruppi di campi;
solution: Experience Platform
title: Creare e modificare gruppi di campi schema nell’interfaccia utente
description: Scopri come creare e modificare i gruppi di campi dello schema nell’interfaccia utente di Experience Platform.
topic: Guida utente
translation-type: tm+mt
source-git-commit: 3985ba8f46a62e8d9ea8b1f084198b245318a24f
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Creare e modificare i gruppi di campi dello schema nell’interfaccia utente

In Experience Data Model (XDM), i gruppi di campi schema sono componenti riutilizzabili che definiscono uno o più campi che implementano determinate funzioni, ad esempio dettagli personali, preferenze alberghiere o indirizzo. I gruppi di campi devono essere inclusi come parte di uno schema che implementa una classe compatibile.

Un gruppo di campi definisce le classi con cui è compatibile, in base al comportamento dei dati che il gruppo di campi rappresenta (record o serie temporali). Ciò significa che non tutti i gruppi di campi sono disponibili per l&#39;uso con tutte le classi.

Adobe Experience Platform fornisce molti gruppi di campi standard che coprono un&#39;ampia gamma di casi d&#39;uso di marketing. Tuttavia, puoi anche creare e modificare gruppi di campi personalizzati per definire concetti aggiuntivi relativi alla tua attività all’interno degli schemi XDM. Questa guida fornisce una panoramica su come creare, modificare e gestire gruppi di campi personalizzati per la tua organizzazione nell’interfaccia utente di Platform.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema di Experience Platform, fai riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base sulla composizione dello schema](../../schema/composition.md) per sapere in che modo i gruppi di campi contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità di [!DNL Schema Editor].

## Crea un nuovo gruppo di campi {#create}

Per creare un nuovo gruppo di campi, è innanzitutto necessario selezionare uno schema a cui aggiungere il gruppo di campi. È possibile scegliere di [creare un nuovo schema](./schemas.md#create) o [selezionare uno schema esistente da modificare](./schemas.md#edit).

Una volta aperto lo schema in [!DNL Schema Editor], seleziona **[!UICONTROL Add]** accanto alla sezione [!UICONTROL Field groups] nella barra a sinistra.

![](../../images/ui/resources/field-groups/add-field-group.png)

Viene visualizzata una finestra di dialogo che mostra un elenco dei gruppi di campi esistenti per l’organizzazione. Nella parte superiore della finestra di dialogo, seleziona **[!UICONTROL Create new field group]**. Qui puoi fornire un **[!UICONTROL Display name]** e **[!UICONTROL Description]** per il gruppo di campi. Al termine, seleziona **[!UICONTROL Add field group]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

Il [!DNL Schema Editor] viene visualizzato nuovamente con il nuovo gruppo di campi elencato nella barra a sinistra. Poiché si tratta di un nuovo gruppo di campi, al momento non fornisce alcun campo allo schema, e quindi l’area di lavoro rimane invariata. Ora puoi iniziare [aggiungendo campi al gruppo di campi](#add-fields).

## Modificare un gruppo di campi esistente {#edit}

>[!NOTE]
>
>Solo i gruppi di campi personalizzati definiti dall’organizzazione possono essere modificati e personalizzati completamente. Per i gruppi di campi di base definiti dall’Adobe, solo i nomi visualizzati dei relativi campi possono essere modificati nel contesto dei singoli schemi. Per ulteriori informazioni, consulta la sezione sulla [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names) .
>
>Una volta salvato e utilizzato un gruppo di campi personalizzato in uno schema per l’inserimento dei dati, è possibile apportare solo modifiche aggiuntive al gruppo di campi in seguito. Per ulteriori informazioni, consulta le [regole di evoluzione dello schema](../../schema/composition.md#evolution) .

Per modificare un gruppo di campi esistente, è innanzitutto necessario aprire uno schema che utilizzi il gruppo di campi all&#39;interno di [!DNL Schema Editor]. È possibile [selezionare uno schema esistente da modificare](./schemas.md#edit) oppure [creare un nuovo schema](./schemas.md#create) e aggiungere il gruppo di campi in questione.

Una volta aperto lo schema nell&#39;editor, puoi iniziare ad aggiungere i campi [al gruppo di campi](#add-fields).

## Aggiungere campi a un gruppo di campi {#add-fields}

Per aggiungere campi a un gruppo di campi in [!DNL Schema Editor], inizia selezionando il nome del gruppo di campi nella barra a sinistra, quindi seleziona l’icona **più (+)** accanto al nome dello schema nell’area di lavoro.

![](../../images/ui/resources/field-groups/add-field.png)

Nell’area di lavoro viene visualizzato un **[!UICONTROL New field]** e la barra a destra viene aggiornata per mostrare i controlli necessari per configurare le proprietà del campo. Per passaggi specifici su come configurare e aggiungere il campo al gruppo di campi, consulta la guida [Definizione dei campi nell’interfaccia utente](../fields/overview.md#define) .

Continua ad aggiungere tutti i campi necessari al gruppo di campi. Al termine, seleziona **[!UICONTROL Save]** per salvare sia lo schema che il gruppo di campi.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Se lo stesso gruppo di campi è già utilizzato in altri schemi, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Passaggi successivi

Questa guida illustra come creare e modificare gruppi di campi utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], consulta la [[!UICONTROL Schemas] panoramica dell&#39;area di lavoro](../overview.md).

Per informazioni su come gestire i gruppi di campi utilizzando l&#39;API [!DNL Schema Registry], consulta la [guida all&#39;endpoint dei gruppi di campi](../../api/field-groups.md).