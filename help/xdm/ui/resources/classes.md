---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;classe;classi;
solution: Experience Platform
title: Creare e modificare le classi nell’interfaccia utente
description: Scopri come creare e modificare le classi nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c83b5616f46f6f7d752979fa66a66fad16f16102
workflow-type: tm+mt
source-wordcount: '999'
ht-degree: 0%

---

# Creare e modificare le classi nell’interfaccia utente

In Experience Data Model (XDM), le classi definiscono gli aspetti comportamentali dei dati che uno schema conterrà (record o serie temporali). Inoltre, le classi descrivono il numero più piccolo di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per unire più set di dati compatibili.

Adobe fornisce diverse classi XDM standard (&quot;core&quot;), tra cui [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Oltre a queste classi principali, puoi anche creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione.

Questo documento fornisce una panoramica su come creare, modificare e gestire classi personalizzate nell’interfaccia utente di Adobe Experience Platform.

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Fai riferimento a [Panoramica di XDM](../../home.md) introduzione al ruolo di XDM nell&#39;ecosistema Experience Platform e [nozioni di base sulla composizione dello schema](../../schema/composition.md) per scoprire come le classi contribuiscono agli schemi XDM.

Sebbene non sia richiesto per questa guida, è consigliabile seguire anche l’esercitazione su [composizione di uno schema nell’interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità del [!DNL Schema Editor].

## Crea una nuova classe {#create}

In **[!UICONTROL Schemi]** area di lavoro, seleziona **[!UICONTROL Creare uno schema]**, quindi seleziona **[!UICONTROL Sfoglia]** dal menu a discesa .

![](../../images/ui/resources/classes/browse-classes.png)

Viene visualizzata una finestra di dialogo che consente di selezionare da un elenco di classi disponibili. Nella parte superiore della finestra di dialogo, seleziona **[!UICONTROL Crea nuova classe]**. È quindi possibile assegnare alla nuova classe un nome visualizzato (un nome breve, descrittivo, univoco e descrittivo per la classe), una descrizione e un comportamento per i dati che lo schema definirà (&quot;[!UICONTROL Record]&quot; o &quot;[!UICONTROL Serie temporali]&quot;).

Al termine, seleziona **[!UICONTROL Assegna classe]**.

![](../../images/ui/resources/classes/class-details.png)

La [!DNL Schema Editor] viene visualizzato un nuovo schema nell&#39;area di lavoro basato sulla classe personalizzata appena creata. Poiché non è ancora stato aggiunto alcun campo alla classe, lo schema contiene solo un `_id` , che rappresenta l’identificatore univoco generato dal sistema applicato automaticamente a tutte le risorse nel [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Quando si crea uno schema che implementa una classe definita dall&#39;organizzazione, tenere presente che i gruppi di campi dello schema sono disponibili per l&#39;utilizzo solo con classi compatibili. Poiché la classe definita è nuova, non sono presenti gruppi di campi compatibili elencati nella **[!UICONTROL Aggiungi gruppo di campi]** finestra di dialogo. Invece, dovrai [creare nuovi gruppi di campi](./field-groups.md#create) da utilizzare con quella classe. La prossima volta che si compone uno schema che implementa la nuova classe, i gruppi di campi definiti verranno elencati e disponibili per l&#39;uso.

Ora puoi iniziare [aggiunta di campi alla classe](#add-fields), che verrà condiviso da tutti gli schemi che utilizzano la classe .

## Modificare una classe esistente {#edit}

>[!IMPORTANT]
>
>Le classi personalizzate create dopo il 30 aprile 2022 non possono essere modificate direttamente e una correzione è attualmente in fase di sviluppo. Come soluzione alternativa, è possibile [creare un gruppo di campi personalizzato](./field-groups.md) e riutilizzarlo per ogni schema che utilizza la classe personalizzata che si desidera estendere. Questa limitazione non riguarda le classi personalizzate create prima del 30 aprile 2022.

>[!NOTE]
>
>Solo le classi personalizzate definite dall&#39;organizzazione possono essere modificate e personalizzate completamente. Per le classi principali definite dall’Adobe, solo i nomi visualizzati dei relativi campi possono essere modificati nel contesto dei singoli schemi. Vedi la sezione su [modifica dei nomi visualizzati per i campi dello schema](./schemas.md#display-names) per i dettagli.
>
>Una volta salvata e utilizzata una classe personalizzata nell’inserimento dei dati, è possibile apportare solo modifiche aggiuntive in seguito. Consulta la sezione [regole di evoluzione dello schema](../../schema/composition.md#evolution) per ulteriori informazioni.

Per modificare una classe esistente, seleziona la **[!UICONTROL Sfoglia]** quindi selezionare il nome di uno schema che utilizza la classe da modificare.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>È possibile utilizzare le funzionalità di ricerca e filtro dell&#39;area di lavoro per facilitare lo schema. Consulta la guida su [esplorazione delle risorse XDM](../explore.md) per ulteriori informazioni.

La [!DNL Schema Editor] , con la struttura dello schema mostrata nell&#39;area di lavoro. Ora puoi iniziare [aggiunta di campi alla classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Aggiungere campi a una classe {#add-fields}

>[!IMPORTANT]
>
>Le classi personalizzate create dopo il 30 aprile 2022 non possono essere modificate direttamente e una correzione è attualmente in fase di sviluppo. Come soluzione alternativa, è possibile [creare un gruppo di campi personalizzato](./field-groups.md) e riutilizzarlo per ogni schema che utilizza la classe personalizzata che si desidera estendere. Questa limitazione non riguarda le classi personalizzate create prima del 30 aprile 2022.

Una volta che si dispone di uno schema che utilizza una classe personalizzata aperta nel [!UICONTROL Editor di schema], puoi iniziare ad aggiungere campi alla classe . Per aggiungere un nuovo campo, seleziona la **più (+)** accanto al nome dello schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Tenere presente che tutti i campi aggiunti a una classe verranno utilizzati in tutti gli schemi che utilizzano tale classe. È quindi necessario considerare attentamente quali campi saranno utili in tutti i casi di utilizzo dello schema. Se si sta pensando di aggiungere un campo che può essere utilizzato solo in alcuni schemi di questa classe, è consigliabile aggiungerlo a tali schemi tramite [creazione di un gruppo di campi](./field-groups.md#create) invece.

A **[!UICONTROL Nuovo campo]** nell’area di lavoro e nella barra a destra vengono visualizzati i controlli per configurare le proprietà del campo. Consulta la guida su [definizione dei campi nell’interfaccia utente](../fields/overview.md#define) per passaggi specifici su come configurare e aggiungere il campo alla classe .

Continua ad aggiungere tutti i campi necessari alla classe. Al termine, seleziona **[!UICONTROL Salva]** per salvare lo schema e la classe.

![](../../images/ui/resources/classes/save.png)

Se in precedenza sono stati creati schemi che utilizzano questa classe, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Modificare la classe di uno schema {#schema}

È possibile modificare la classe dello schema in qualsiasi momento durante il processo di creazione iniziale prima che sia stato salvato. Consulta la guida su [creazione e modifica degli schemi](./schemas.md#change-class) per ulteriori informazioni.

## Passaggi successivi

Questo documento illustra come creare e modificare le classi utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità del [!UICONTROL Schemi] area di lavoro, vedi [[!UICONTROL Schemi] panoramica dell&#39;area di lavoro](../overview.md).

Per informazioni su come gestire le classi utilizzando [!DNL Schema Registry] API, vedi [guida all&#39;endpoint delle classi](../../api/classes.md).
