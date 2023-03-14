---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;class;classes;
solution: Experience Platform
title: Creare e modificare le classi nell’interfaccia utente
description: Scopri come creare e modificare le classi nell’interfaccia utente di Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 3a9b97b25980d88e0fff3d71e43407b641e6454d
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Creare e modificare le classi nell’interfaccia utente

In Adobe Experience Platform, la classe di uno schema definisce gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Inoltre, le classi descrivono il minor numero di proprietà comuni che tutti gli schemi basati su tale classe dovrebbero includere e forniscono un modo per unire più set di dati compatibili.

Adobe fornisce diverse classi standard (&quot;core&quot;) di Experience Data Model (XDM), tra cui [!DNL XDM Individual Profile] e [!DNL XDM ExperienceEvent]. Oltre a queste classi principali, puoi anche creare classi personalizzate per descrivere casi d’uso più specifici per la tua organizzazione.

Questo documento fornisce una panoramica su come creare, modificare e gestire le classi personalizzate nell’interfaccia utente di Experience Platform.

## Prerequisiti

Questa guida richiede una buona conoscenza del sistema XDM. Consulta la sezione [Panoramica di XDM](../../home.md) per un’introduzione al ruolo di XDM nell’ecosistema Experience Platform e [nozioni di base sulla composizione dello schema](../../schema/composition.md) per scoprire come le classi contribuiscono agli schemi XDM.

Sebbene non sia necessario per questa guida, si consiglia di seguire l’esercitazione anche su [composizione di uno schema nell’interfaccia utente](../../tutorials/create-schema-ui.md) per acquisire familiarità con le varie funzionalità del [!DNL Schema Editor].

## Crea una nuova classe {#create}

In **[!UICONTROL Schemi]** workspace, seleziona **[!UICONTROL Crea schema]**, quindi seleziona **[!UICONTROL Sfoglia]** dal menu a discesa.

![](../../images/ui/resources/classes/browse-classes.png)

Viene visualizzata una finestra di dialogo che consente di selezionare da un elenco di classi disponibili. Nella parte superiore della finestra di dialogo, seleziona **[!UICONTROL Crea nuova classe]**. È quindi possibile assegnare alla nuova classe un nome visualizzato (breve, descrittivo, univoco e descrittivo per la classe), una descrizione e un comportamento per i dati definiti dallo schema (**[!UICONTROL Registra]** o **[!UICONTROL Serie temporali]**).

Al termine, seleziona **[!UICONTROL Assegna classe]**.

![](../../images/ui/resources/classes/class-details.png)

Il [!DNL Schema Editor] viene visualizzato un nuovo schema nell’area di lavoro basato sulla classe personalizzata appena creata. Poiché non sono ancora stati aggiunti campi alla classe, lo schema contiene solo un `_id` , che rappresenta l&#39;identificatore univoco generato dal sistema e applicato automaticamente a tutte le risorse nel [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Quando crei uno schema che implementa una classe definita dall’organizzazione, ricorda che i gruppi di campi di schema sono disponibili per l’utilizzo solo con classi compatibili. Poiché la classe definita è nuova, non sono elencati gruppi di campi compatibili in **[!UICONTROL Aggiungi gruppo di campi]** . Sarà invece necessario [creare nuovi gruppi di campi](./field-groups.md#create) da utilizzare con tale classe. La prossima volta che componi uno schema che implementa la nuova classe, i gruppi di campi definiti verranno elencati e saranno disponibili per l’uso.

Ora puoi iniziare [aggiunta di campi alla classe](#add-fields), che verrà condiviso da tutti gli schemi che utilizzano la classe.

## Modificare una classe esistente {#edit}

>[!NOTE]
>
>Solo le classi personalizzate definite dall&#39;organizzazione possono essere completamente modificate e personalizzate. Per le classi principali definite da Adobe, è possibile modificare solo i nomi visualizzati dei relativi campi nel contesto dei singoli schemi. Consulta la sezione su [modifica dei nomi visualizzati per i campi schema](./schemas.md#display-names) per i dettagli.
>
>Dopo aver salvato e utilizzato una classe personalizzata nell’acquisizione dei dati, è possibile apportarvi solo modifiche aggiuntive. Consulta la [regole di evoluzione dello schema](../../schema/composition.md#evolution) per ulteriori informazioni.

Per modificare una classe esistente, selezionare **[!UICONTROL Sfoglia]** e quindi selezionare il nome di uno schema che utilizza la classe che si desidera modificare.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Puoi utilizzare le funzionalità di ricerca e filtro dell’area di lavoro per trovare più facilmente lo schema. Consulta la guida su [esplorazione delle risorse XDM](../explore.md) per ulteriori informazioni.

Il [!DNL Schema Editor] viene visualizzata, con la struttura dello schema visualizzata nell’area di lavoro. Ora puoi iniziare [aggiunta di campi alla classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Aggiungere campi a una classe {#add-fields}

Una volta che si dispone di uno schema che utilizza una classe personalizzata aperta in [!UICONTROL Editor schema], puoi iniziare ad aggiungere campi alla classe. Per aggiungere un nuovo campo, selezionare **più (+)** accanto al nome dello schema.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Tenere presente che tutti i campi aggiunti a una classe verranno utilizzati in tutti gli schemi che utilizzano tale classe. Pertanto, è necessario considerare attentamente quali campi saranno utili in tutti i casi di utilizzo degli schemi. Se stai pensando di aggiungere un campo che potrebbe essere utilizzato solo in alcuni schemi di questa classe, puoi provare ad aggiungerlo a tali schemi [creazione di un gruppo di campi](./field-groups.md#create) invece.

Un **[!UICONTROL Campo senza titolo]** il segnaposto viene visualizzato nell’area di lavoro e la barra a destra si aggiorna per mostrare i controlli per configurare le proprietà del campo. Sotto **[!UICONTROL Assegna a]**, seleziona **[!UICONTROL Classe]**.

![](../../images/ui/resources/classes/assign-to-class.png)

![](../../images/ui/resources/classes/assign-to-class.png)

Consulta la guida su [definizione dei campi nell’interfaccia utente](../fields/overview.md#define) per passaggi specifici su come configurare e aggiungere il campo alla classe. Continua ad aggiungere alla classe tutti i campi necessari. Al termine, seleziona **[!UICONTROL Salva]** per salvare sia lo schema che la classe.

![](../../images/ui/resources/classes/save.png)

Se in precedenza sono stati creati schemi che utilizzano questa classe, i campi appena aggiunti verranno visualizzati automaticamente in tali schemi.

## Modificare la classe di uno schema {#schema}

È possibile modificare la classe dello schema in qualsiasi momento durante il processo di creazione iniziale prima che sia stato salvato. Consulta la guida su [creazione e modifica di schemi](./schemas.md#change-class) per ulteriori informazioni.

## Passaggi successivi

Questo documento illustra come creare e modificare le classi utilizzando l’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità di [!UICONTROL Schemi] Workspace, consulta la sezione [[!UICONTROL Schemi] panoramica di workspace](../overview.md).

Per informazioni su come gestire le classi utilizzando [!DNL Schema Registry] API, consulta [guida dell’endpoint &quot;classes&quot;](../../api/classes.md).
