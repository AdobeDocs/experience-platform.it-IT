---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;classe;classi;
solution: Experience Platform
title: Creare e modificare le classi nell’interfaccia utente
description: Scopri come creare e modificare le classi nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# Creare e modificare le classi nell’interfaccia utente

In Experience Data Model (XDM), le classi definiscono gli aspetti comportamentali dei dati che uno schema conterrà (record o serie temporali). Inoltre, le classi descrivono il numero più piccolo di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per unire più set di dati compatibili.

Adobe fornisce diverse classi XDM standard (&quot;core&quot;), tra cui [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Oltre a queste classi principali, puoi anche creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione.

Questo documento fornisce una panoramica su come creare, modificare e gestire classi personalizzate nell’interfaccia utente di Adobe Experience Platform.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Per un&#39;introduzione al ruolo di XDM all&#39;interno dell&#39;ecosistema Experience Platform, fai riferimento alla [panoramica XDM](../../home.md) e alle [nozioni di base sulla composizione dello schema](../../schema/composition.md) per scoprire come le classi contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, si consiglia anche di seguire l&#39;esercitazione su [composizione di uno schema nell&#39;interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità di [!DNL Schema Editor].

## Crea una nuova classe {#create}

Nell’area di lavoro **[!UICONTROL Schemas]**, seleziona **[!UICONTROL Create schema]**, quindi seleziona **[!UICONTROL Browse]** dal menu a discesa.

![](../../images/ui/resources/classes/browse-classes.png)

Viene visualizzata una finestra di dialogo che consente di selezionare da un elenco di classi disponibili. Nella parte superiore della finestra di dialogo, seleziona **[!UICONTROL Create new class]**. È quindi possibile assegnare alla nuova classe un nome visualizzato (un nome breve, descrittivo, univoco e descrittivo per la classe), una descrizione e un comportamento per i dati che lo schema definirà (&quot;[!UICONTROL Record]&quot; o &quot;[!UICONTROL Time-series]&quot;).

Al termine, seleziona **[!UICONTROL Assign class]**.

![](../../images/ui/resources/classes/class-details.png)

Viene visualizzato [!DNL Schema Editor], che mostra un nuovo schema nell’area di lavoro basato sulla classe personalizzata appena creata. Poiché non è ancora stato aggiunto alcun campo alla classe, lo schema contiene solo un campo `_id` che rappresenta l’identificatore univoco generato dal sistema che viene applicato automaticamente a tutte le risorse nel [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Quando si crea uno schema che implementa una classe definita dall&#39;organizzazione, tenere presente che i gruppi di campi dello schema sono disponibili per l&#39;utilizzo solo con classi compatibili. Poiché la classe definita è nuova, nella finestra di dialogo **[!UICONTROL Add field group]** non sono presenti gruppi di campi compatibili. Sarà invece necessario [creare nuovi gruppi di campi](./field-groups.md#create) da utilizzare con tale classe. La prossima volta che si compone uno schema che implementa la nuova classe, i gruppi di campi definiti verranno elencati e disponibili per l&#39;uso.

Ora puoi iniziare [aggiungendo campi alla classe](#add-fields), che verrà condivisa da tutti gli schemi che utilizzano la classe.

## Modifica una classe esistente {#edit}

>[!NOTE]
>
>Solo le classi personalizzate definite dall&#39;organizzazione possono essere modificate e personalizzate completamente. Per le classi principali definite dall’Adobe, solo i nomi visualizzati dei relativi campi possono essere modificati nel contesto dei singoli schemi. Per ulteriori informazioni, consulta la sezione sulla [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names) .
>
>Una volta salvata e utilizzata una classe personalizzata nell’inserimento dei dati, è possibile apportare solo modifiche aggiuntive in seguito. Per ulteriori informazioni, consulta le [regole di evoluzione dello schema](../../schema/composition.md#evolution) .

Per modificare una classe esistente, selezionare la scheda **[!UICONTROL Browse]**, quindi selezionare il nome di uno schema che utilizza la classe da modificare.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>È possibile utilizzare le funzionalità di ricerca e filtro dell&#39;area di lavoro per facilitare lo schema. Per ulteriori informazioni, consulta la guida sull’ [esplorazione delle risorse XDM](../explore.md) .

Viene visualizzato il simbolo [!DNL Schema Editor], con la struttura dello schema visualizzata nell&#39;area di lavoro. Ora puoi iniziare [aggiungendo campi alla classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Aggiungi campi a una classe {#add-fields}

Una volta che si dispone di uno schema che utilizza una classe personalizzata aperta in [!UICONTROL Schema Editor], è possibile iniziare ad aggiungere campi alla classe. Per aggiungere un nuovo campo, seleziona l’icona **più (+)** accanto al nome dello schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Tenere presente che tutti i campi aggiunti a una classe verranno utilizzati in tutti gli schemi che utilizzano tale classe. È quindi necessario considerare attentamente quali campi saranno utili in tutti i casi di utilizzo dello schema. Se si sta pensando di aggiungere un campo che può essere utilizzato solo in alcuni schemi di questa classe, è consigliabile aggiungerlo a tali schemi creando un gruppo di campi](./field-groups.md#create).[

Nell’area di lavoro viene visualizzato un **[!UICONTROL New field]** e la barra a destra viene aggiornata per mostrare i controlli necessari per configurare le proprietà del campo. Per passaggi specifici su come configurare e aggiungere il campo alla classe, consulta la guida [Definizione dei campi nell’interfaccia utente](../fields/overview.md#define) .

Continua ad aggiungere tutti i campi necessari alla classe. Al termine, selezionare **[!UICONTROL Save]** per salvare sia lo schema che la classe.

![](../../images/ui/resources/classes/save.png)

Se in precedenza sono stati creati schemi che utilizzano questa classe, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Modificare la classe di uno schema {#schema}

È possibile modificare la classe dello schema in qualsiasi momento durante il processo di creazione iniziale prima che sia stato salvato. Per ulteriori informazioni, consulta la guida sulla [creazione e modifica di schemi](./schemas.md#change-class) .

## Passaggi successivi

Questo documento illustra come creare e modificare le classi utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità dell&#39;area di lavoro [!UICONTROL Schemas], consulta la [[!UICONTROL Schemas] panoramica dell&#39;area di lavoro](../overview.md).

Per informazioni su come gestire le classi utilizzando l&#39;API [!DNL Schema Registry], consulta la [guida all&#39;endpoint delle classi](../../api/classes.md).
