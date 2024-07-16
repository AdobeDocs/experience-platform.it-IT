---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;field group;field groups;
solution: Experience Platform
title: Creare e modificare gruppi di campi schema nell’interfaccia utente
description: Scopri come creare e modificare i gruppi di campi dello schema nell’interfaccia utente di Experience Platform.
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 0e1fb15cfa56fb4c2a4a645578327f0a4bd22e68
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 8%

---

# Creare e modificare gruppi di campi schema nell’interfaccia utente {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_filter"
>title="Filtro gruppo di campi personalizzato o standard"
>abstract="L’elenco dei gruppi di campi disponibili viene prefiltrato in base alla modalità di creazione. Selezionare il pulsante di opzione per scegliere tra le opzioni Standard e Personalizzato. L’opzione Standard mostra le entità create da Adobe, mentre l’opzione Personalizzato mostra le entità create all’interno dell’organizzazione. Per ulteriori informazioni sulla creazione e la modifica di gruppi di campi, consulta la documentazione."

In Experience Data Model (XDM), i gruppi di campi di schema sono componenti riutilizzabili che definiscono uno o più campi che implementano determinate funzioni come dati personali, preferenze di hotel o indirizzo. I gruppi di campi sono destinati a essere inclusi come parte di uno schema che implementa una classe compatibile.

Un gruppo di campi definisce le classi con cui è compatibile, in base al comportamento dei dati che il gruppo di campi rappresenta (record o serie temporali). Ciò significa che non tutti i gruppi di campi sono disponibili per l&#39;utilizzo con tutte le classi.

Adobe Experience Platform fornisce molti gruppi di campi standard che coprono un&#39;ampia gamma di casi d&#39;uso di marketing. Tuttavia, puoi anche creare e modificare i tuoi gruppi di campi personalizzati per definire concetti aggiuntivi relativi alla tua attività all’interno degli schemi XDM. Questa guida fornisce una panoramica su come creare, modificare e gestire gruppi di campi personalizzati per la tua organizzazione nell’interfaccia utente di Platform.

## Prerequisiti {#prerequisites}

Questa guida richiede una buona conoscenza del sistema XDM. Consulta la [panoramica di XDM](../../home.md) per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema Experience Platform e le [nozioni di base sulla composizione dello schema](../../schema/composition.md) per informazioni sul modo in cui i gruppi di campi contribuiscono agli schemi XDM.

Sebbene non sia necessario per questa guida, è consigliabile seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità di [!DNL Schema Editor].

## Crea un nuovo gruppo di campi {#create}

Per creare un nuovo gruppo di campi, devi innanzitutto selezionare uno schema a cui aggiungere il gruppo di campi. Puoi scegliere di [creare un nuovo schema](./schemas.md#create) o [selezionare uno schema esistente da modificare](./schemas.md#edit).

Dopo aver aperto lo schema in [!DNL Schema Editor], seleziona **[!UICONTROL Aggiungi]** accanto alla sezione [!UICONTROL Gruppi di campi] nella barra a sinistra.

![](../../images/ui/resources/field-groups/add-field-group.png)

Nella finestra di dialogo visualizzata, seleziona **[!UICONTROL Crea nuovo gruppo di campi]**. Qui puoi fornire **[!UICONTROL Nome visualizzato]** e **[!UICONTROL Descrizione]** per il gruppo di campi. Al termine, selezionare **[!UICONTROL Aggiungi gruppi di campi]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

[!DNL Schema Editor] viene nuovamente visualizzato, con il nuovo gruppo di campi elencato nella barra a sinistra. Poiché si tratta di un gruppo di campi nuovo di zecca, al momento non fornisce alcun campo allo schema, e pertanto l’area di lavoro rimane invariata. Ora puoi iniziare ad aggiungere [campi al gruppo di campi](#add-fields).

![](../../images/ui/resources/field-groups/field-group-added.png)

## Filtra gruppi di campi {#filter}

L’elenco dei gruppi di campi disponibili viene prefiltrato in base alla modalità di creazione. Per impostazione predefinita vengono visualizzati i gruppi di campi definiti dall&#39;Adobe. Tuttavia, puoi anche filtrare l’elenco per mostrare quelli creati dalla tua organizzazione. Selezionare il pulsante di opzione per scegliere tra le opzioni [!UICONTROL Standard] e [!UICONTROL Personalizzato]. L&#39;opzione [!UICONTROL Standard] mostra le entità create da Adobe e l&#39;opzione [!UICONTROL Custom] mostra le entità create all&#39;interno dell&#39;organizzazione.

![Scheda [!UICONTROL Gruppi di campi] dell&#39;area di lavoro [!UICONTROL Schemi] con [!UICONTROL Standard] e [!UICONTROL Personalizzato] evidenziati.](../../images/ui/resources/field-groups/standard-and-custom-field-groups.png)

## Modificare un gruppo di campi esistente {#edit}

>[!NOTE]
>
>Solo i gruppi di campi personalizzati definiti dall’organizzazione possono essere completamente modificati e personalizzati. Per i gruppi di campi principali definiti da Adobe, è possibile modificare solo i nomi visualizzati dei relativi campi nel contesto dei singoli schemi. Nell&#39;Editor schema sono indicati da un&#39;icona lucchetto (![Un&#39;icona lucchetto.](../../images/ui/explore/padlock-icon.png)). Per ulteriori informazioni, consulta la sezione sulla [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names).
>
>Dopo aver salvato e utilizzato un gruppo di campi personalizzato in uno schema per l’acquisizione dei dati, è possibile apportare al gruppo di campi solo modifiche aggiuntive. Per ulteriori informazioni, consulta le [regole dell&#39;evoluzione dello schema](../../schema/composition.md#evolution).

Per modificare un gruppo di campi esistente, è innanzitutto necessario aprire uno schema che utilizza il gruppo di campi all&#39;interno di [!DNL Schema Editor]. È possibile [selezionare uno schema esistente da modificare](./schemas.md#edit) oppure [creare un nuovo schema](./schemas.md#create) e aggiungere il gruppo di campi in questione.

Dopo aver aperto lo schema nell&#39;editor, puoi iniziare ad [aggiungere campi al gruppo di campi](#add-fields).

## Aggiungere campi a un gruppo di campi {#add-fields}

>[!NOTE]
>
>Questa sezione si concentra sull’aggiunta di campi ai gruppi di campi personalizzati. Per informazioni su come aggiungere campi personalizzati ai gruppi di campi standard, consulta la [guida dell&#39;interfaccia utente degli schemi](./schemas.md#custom-fields-for-standard-groups).

Per aggiungere campi a un gruppo di campi personalizzato, inizia selezionando l&#39;icona **più (+)** accanto al nome dello schema nell&#39;area di lavoro.

![](../../images/ui/resources/field-groups/add-field.png)

Nell&#39;area di lavoro viene visualizzato un segnaposto per **[!UICONTROL Campo senza titolo]** e la barra a destra si aggiorna per mostrare i controlli per configurare le proprietà del campo. Consulta la guida su [definizione dei campi nell&#39;interfaccia utente](../fields/overview.md#define) per i passaggi specifici su come configurare diversi tipi di campi.

In **[!UICONTROL Assegna a]**, seleziona l&#39;opzione **[!UICONTROL Gruppo di campi]**, quindi utilizza il menu a discesa per selezionare il gruppo di campi desiderato dall&#39;elenco. Per limitare i risultati, puoi iniziare a digitare il nome del gruppo di campi.

![](../../images/ui/resources/field-groups/select-field-group.png)

In **[!UICONTROL Assegna a]**, seleziona l&#39;opzione **[!UICONTROL Gruppo di campi]**, quindi utilizza il menu a discesa per selezionare il gruppo di campi desiderato dall&#39;elenco. Per limitare i risultati, puoi iniziare a digitare il nome del gruppo di campi.

![](../../images/ui/resources/field-groups/select-field-group.png)

Una volta aggiunto allo schema, il campo viene assegnato al gruppo di campi selezionato. Continua ad aggiungere al gruppo di campi tutti i campi necessari. Al termine, selezionare **[!UICONTROL Salva]** per salvare sia lo schema che il gruppo di campi.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Se lo stesso gruppo di campi è già utilizzato in altri schemi, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Passaggi successivi {#next-steps}

Questa guida illustra come creare e modificare i gruppi di campi utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemi], vedere la panoramica dell&#39;area di lavoro [[!UICONTROL Schemi]](../overview.md).

Per informazioni su come gestire i gruppi di campi utilizzando l&#39;API [!DNL Schema Registry], consulta la [guida dell&#39;endpoint dei gruppi di campi](../../api/field-groups.md).
