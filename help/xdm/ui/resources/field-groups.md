---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;area di lavoro;gruppo di campi;gruppi di campi;
solution: Experience Platform
title: Creare e modificare gruppi di campi schema nell’interfaccia utente
description: Scopri come creare e modificare i gruppi di campi dello schema nell’interfaccia utente di Experience Platform.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Creare e modificare i gruppi di campi dello schema nell’interfaccia utente

In Experience Data Model (XDM), i gruppi di campi schema sono componenti riutilizzabili che definiscono uno o più campi che implementano determinate funzioni, ad esempio dettagli personali, preferenze alberghiere o indirizzo. I gruppi di campi devono essere inclusi come parte di uno schema che implementa una classe compatibile.

Un gruppo di campi definisce le classi con cui è compatibile, in base al comportamento dei dati che il gruppo di campi rappresenta (record o serie temporali). Ciò significa che non tutti i gruppi di campi sono disponibili per l&#39;uso con tutte le classi.

Adobe Experience Platform fornisce molti gruppi di campi standard che coprono un&#39;ampia gamma di casi d&#39;uso di marketing. Tuttavia, puoi anche creare e modificare gruppi di campi personalizzati per definire concetti aggiuntivi relativi alla tua attività all’interno degli schemi XDM. Questa guida fornisce una panoramica su come creare, modificare e gestire gruppi di campi personalizzati per la tua organizzazione nell’interfaccia utente di Platform.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Fai riferimento a [Panoramica di XDM](../../home.md) introduzione al ruolo di XDM nell&#39;ecosistema Experience Platform e [nozioni di base sulla composizione dello schema](../../schema/composition.md) per informazioni sul contributo dei gruppi di campi agli schemi XDM.

Sebbene non sia richiesto per questa guida, è consigliabile seguire anche l’esercitazione su [composizione di uno schema nell’interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità del [!DNL Schema Editor].

## Crea un nuovo gruppo di campi {#create}

Per creare un nuovo gruppo di campi, è innanzitutto necessario selezionare uno schema a cui aggiungere il gruppo di campi. Puoi scegliere di [creare un nuovo schema](./schemas.md#create) o [selezionare uno schema esistente da modificare](./schemas.md#edit).

Una volta che lo schema è aperto nel [!DNL Schema Editor], seleziona **[!UICONTROL Aggiungi]** accanto al [!UICONTROL Gruppi di campi] nella barra a sinistra.

![](../../images/ui/resources/field-groups/add-field-group.png)

Nella finestra di dialogo visualizzata, seleziona **[!UICONTROL Crea nuovo gruppo di campi]**. Qui puoi fornire un **[!UICONTROL Nome visualizzato]** e **[!UICONTROL Descrizione]** per il gruppo di campi. Al termine, seleziona **[!UICONTROL Aggiungi gruppi di campi]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

La [!DNL Schema Editor] viene nuovamente visualizzato, con il nuovo gruppo di campi elencato nella barra a sinistra. Poiché si tratta di un nuovo gruppo di campi, al momento non fornisce alcun campo allo schema, e quindi l’area di lavoro rimane invariata. Ora puoi iniziare [aggiunta di campi al gruppo di campi](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Modificare un gruppo di campi esistente {#edit}

>[!NOTE]
>
>Solo i gruppi di campi personalizzati definiti dall’organizzazione possono essere modificati e personalizzati completamente. Per i gruppi di campi di base definiti dall’Adobe, solo i nomi visualizzati dei relativi campi possono essere modificati nel contesto dei singoli schemi. Vedi la sezione su [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names) per i dettagli.
>
>Una volta salvato e utilizzato un gruppo di campi personalizzato in uno schema per l’inserimento dei dati, è possibile apportare solo modifiche aggiuntive al gruppo di campi in seguito. Consulta la sezione [regole di evoluzione dello schema](../../schema/composition.md#evolution) per ulteriori informazioni.

Per modificare un gruppo di campi esistente, è innanzitutto necessario aprire uno schema che utilizzi il gruppo di campi all’interno del gruppo [!DNL Schema Editor]. È possibile [selezionare uno schema esistente da modificare](./schemas.md#edit)oppure puoi [creare un nuovo schema](./schemas.md#create) e aggiungere il gruppo di campi in questione.

Una volta aperto lo schema nell&#39;editor, puoi iniziare [aggiunta di campi al gruppo di campi](#add-fields).

## Aggiungere campi a un gruppo di campi {#add-fields}

>[!NOTE]
>
>Questa sezione si concentra sull&#39;aggiunta di campi ai gruppi di campi personalizzati. Per informazioni su come aggiungere campi personalizzati ai gruppi di campi standard, consulta [Guida all’interfaccia utente per gli schemi](./schemas.md#custom-fields-for-standard-groups).

Per aggiungere campi a un gruppo di campi personalizzato, inizia selezionando **più (+)** accanto al nome dello schema nell’area di lavoro.

![](../../images/ui/resources/field-groups/add-field.png)

A **[!UICONTROL Nuovo campo]** nell’area di lavoro e nella barra a destra vengono visualizzati i controlli per configurare le proprietà del campo. Consulta la guida su [definizione dei campi nell’interfaccia utente](../fields/overview.md#define) per passaggi specifici su come configurare diversi tipi di campi.

Sotto **[!UICONTROL Assegna a]**, seleziona **[!UICONTROL Gruppo di campi]** , quindi utilizza il menu a discesa per selezionare il gruppo di campi desiderato dall’elenco. Puoi iniziare a digitare il nome del gruppo di campi per limitare i risultati.

![](../../images/ui/resources/field-groups/select-field-group.png)

Una volta aggiunto il campo allo schema, questo viene assegnato al gruppo di campi selezionato. Continua ad aggiungere tutti i campi necessari al gruppo di campi. Al termine, seleziona **[!UICONTROL Salva]** per salvare lo schema e il gruppo di campi.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Se lo stesso gruppo di campi è già utilizzato in altri schemi, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Passaggi successivi

Questa guida illustra come creare e modificare gruppi di campi utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità del [!UICONTROL Schemi] area di lavoro, vedi [[!UICONTROL Schemi] panoramica dell&#39;area di lavoro](../overview.md).

Per scoprire come gestire i gruppi di campi utilizzando [!DNL Schema Registry] API, vedi [guida all’endpoint dei gruppi di campi](../../api/field-groups.md).
