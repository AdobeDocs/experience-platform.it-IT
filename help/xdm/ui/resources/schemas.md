---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;schema;schemi;
solution: Experience Platform
title: Creare e modificare schemi nell’interfaccia utente
description: Scopri le nozioni di base su come creare e modificare schemi nell’interfaccia utente di Experience Platform.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 49a54b78d1e3745694352e779fb2226acd99d663
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Creare e modificare schemi nell’interfaccia utente

Questa guida fornisce una panoramica su come creare, modificare e gestire gli schemi Experience Data Model (XDM) per la tua organizzazione nell’interfaccia utente di Adobe Experience Platform.

>[!IMPORTANT]
>
>Gli schemi XDM sono estremamente personalizzabili e pertanto i passaggi necessari per creare uno schema possono variare a seconda del tipo di dati che si desidera acquisire dallo schema. Di conseguenza, questo documento copre solo le interazioni di base che è possibile eseguire con gli schemi nell’interfaccia utente ed esclude i passaggi correlati come la personalizzazione di classi, gruppi di campi dello schema, tipi di dati e campi.
>
>Per una panoramica completa del processo di creazione dello schema, segui insieme alla [esercitazione sulla creazione dello schema](../../tutorials/create-schema-ui.md) per creare uno schema di esempio completo e acquisire familiarità con le numerose funzionalità di [!DNL Schema Editor].

## Prerequisiti

Questa guida richiede una buona comprensione del sistema XDM. Fai riferimento a [Panoramica di XDM](../../home.md) introduzione al ruolo di XDM nell&#39;ecosistema Experience Platform e [nozioni di base sulla composizione dello schema](../../schema/composition.md) per una panoramica della creazione degli schemi.

## Creare un nuovo schema {#create}

In [!UICONTROL Schemi] area di lavoro, seleziona **[!UICONTROL Creare uno schema]** nell&#39;angolo in alto a destra. Nel menu a discesa visualizzato, puoi scegliere tra **[!UICONTROL Profilo individuale XDM]** e **[!UICONTROL ExperienceEvent XDM]** come classe base per lo schema. In alternativa, è possibile selezionare **[!UICONTROL Sfoglia]** per selezionare dall’elenco completo delle classi disponibili, oppure [creare una nuova classe personalizzata](./classes.md#create) invece.

![](../../images/ui/resources/schemas/create-schema.png)

Dopo aver selezionato una classe, la [!DNL Schema Editor] e la struttura di base dello schema (fornita dalla classe) viene visualizzata nell&#39;area di lavoro. Da qui, puoi utilizzare la barra a destra per aggiungere un **[!UICONTROL Nome visualizzato]** e **[!UICONTROL Descrizione]** per lo schema.

![](../../images/ui/resources/schemas/schema-details.png)

Ora puoi iniziare a creare la struttura dello schema tramite [aggiunta di gruppi di campi schema](#add-field-groups).

## Modificare uno schema esistente {#edit}

>[!NOTE]
>
>Una volta salvato e utilizzato lo schema nell’inserimento dei dati, è possibile apportare solo modifiche aggiuntive. Consulta la sezione [regole di evoluzione dello schema](../../schema/composition.md#evolution) per ulteriori informazioni.

Per modificare uno schema esistente, seleziona **[!UICONTROL Sfoglia]** quindi selezionare il nome dello schema da modificare.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>È possibile utilizzare le funzionalità di ricerca e filtro dell&#39;area di lavoro per facilitare lo schema. Consulta la guida su [esplorazione delle risorse XDM](../explore.md) per ulteriori informazioni.

Una volta selezionato uno schema, la [!DNL Schema Editor] viene visualizzata con la struttura dello schema mostrata nell&#39;area di lavoro. Ora puoi [aggiungere gruppi di campi](#add-field-groups) allo schema, [modificare i nomi visualizzati dei campi](#display-names)oppure [modifica gruppi di campi personalizzati esistenti](./field-groups.md#edit) se lo schema ne utilizza uno.

## Aggiunta di gruppi di campi a uno schema {#add-field-groups}

>[!NOTE]
>
>Questa sezione illustra come aggiungere gruppi di campi esistenti a uno schema. Per creare un nuovo gruppo di campi personalizzato, consulta la guida [creazione e modifica di gruppi di campi](./field-groups.md#create) invece.

Una volta aperto uno schema all&#39;interno di [!DNL Schema Editor], è possibile aggiungere campi allo schema utilizzando gruppi di campi. Per iniziare, seleziona **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]** nella barra a sinistra.

![](../../images/ui/resources/schemas/add-field-group-button.png)

Viene visualizzata una finestra di dialogo in cui viene visualizzato un elenco di gruppi di campi selezionabili per lo schema. Poiché i gruppi di campi sono compatibili solo con una classe, verranno elencati solo i gruppi di campi associati alla classe selezionata dello schema. Per impostazione predefinita, i gruppi di campi elencati sono ordinati in base alla loro popolarità d’uso all’interno dell’organizzazione.

![](../../images/ui/resources/schemas/field-group-popularity.png)

Se si conosce l’attività o l’area business generale dei campi che si desidera aggiungere, selezionare una o più categorie verticali del settore nella barra a sinistra per filtrare l’elenco visualizzato dei gruppi di campi.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Per ulteriori informazioni sulle best practice per la modellazione di dati specifici per il settore in XDM, consulta la documentazione su [modelli di dati del settore](../../schema/industries/overview.md).

Puoi anche utilizzare la barra di ricerca per individuare il gruppo di campi desiderato. I gruppi di campi il cui nome corrisponde alla query vengono visualizzati nella parte superiore dell’elenco. Sotto **[!UICONTROL Campi standard]**, vengono visualizzati i gruppi di campi contenenti i campi che descrivono gli attributi di dati desiderati.

![](../../images/ui/resources/schemas/field-group-search.png)

Selezionare la casella di controllo accanto al nome del gruppo di campi che si desidera aggiungere allo schema. È possibile selezionare più gruppi di campi dall’elenco, ciascuno dei quali è visualizzato nella barra a destra.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Per qualsiasi gruppo di campi elencato, puoi passare il cursore sull’icona delle informazioni (![](../../images/ui/resources/schemas/info-icon.png)) per visualizzare una breve descrizione del tipo di dati acquisiti dal gruppo di campi. Puoi anche selezionare l’icona di anteprima (![](../../images/ui/resources/schemas/preview-icon.png)) per visualizzare la struttura dei campi forniti dal gruppo di campi prima di decidere di aggiungerlo allo schema.

Dopo aver selezionato i gruppi di campi, seleziona **[!UICONTROL Aggiungi gruppi di campi]** per aggiungerli allo schema.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

La [!DNL Schema Editor] viene visualizzata nuovamente con i campi forniti dal gruppo di campi rappresentati nell’area di lavoro.

![](../../images/ui/resources/schemas/field-groups-added.png)

## Abilitare uno schema per il profilo cliente in tempo reale {#profile}

[Profilo cliente in tempo reale](../../../profile/home.md) unisce i dati provenienti da fonti diverse per creare una visione completa di ogni singolo cliente. Se si desidera che i dati acquisiti da uno schema partecipino a questo processo, è necessario abilitare lo schema da utilizzare in [!DNL Profile].

>[!IMPORTANT]
>
>Per abilitare uno schema per [!DNL Profile], deve avere un campo di identità principale definito. Consulta la guida su [definizione dei campi di identità](../fields/identity.md) per ulteriori informazioni.

Per abilitare lo schema, inizia selezionando il nome dello schema nella barra a sinistra, quindi seleziona la **[!UICONTROL Profilo]** attiva la barra a destra.

![](../../images/ui/resources/schemas/profile-toggle.png)

Viene visualizzato un puntatore che avvisa che, una volta abilitato e salvato uno schema, non può essere disabilitato. Seleziona **[!UICONTROL Abilita]** per continuare.

![](../../images/ui/resources/schemas/profile-confirm.png)

L&#39;area di lavoro viene visualizzata nuovamente con la [!UICONTROL Profilo] attiva/disattiva.

>[!IMPORTANT]
>
>Poiché lo schema non è ancora stato salvato, questo è il punto di non ritorno se cambi idea di consentire allo schema di partecipare al Profilo cliente in tempo reale: una volta salvato uno schema abilitato, non è più possibile disattivarlo. Seleziona la **[!UICONTROL Profilo]** per disattivare lo schema, seleziona di nuovo l’opzione .

Per completare il processo, seleziona **[!UICONTROL Salva]** per salvare lo schema.

![](../../images/ui/resources/schemas/profile-enabled.png)

Lo schema è ora abilitato per l’utilizzo in Profilo cliente in tempo reale. Quando Platform acquisisce dati in set di dati basati su questo schema, questi verranno incorporati nei dati del profilo amalgamato.

## Modifica dei nomi visualizzati per i campi dello schema {#display-names}

Dopo aver assegnato una classe e aggiunto gruppi di campi a uno schema, è possibile modificare i nomi visualizzati di qualsiasi campo dello schema, indipendentemente dal fatto che tali campi siano stati forniti da risorse XDM standard o personalizzate.

>[!NOTE]
>
>Tenere presente che i nomi visualizzati dei campi appartenenti a classi o gruppi di campi standard possono essere modificati solo nel contesto di uno schema specifico. In altre parole, la modifica del nome visualizzato di un campo standard in uno schema non influisce su altri schemi che utilizzano la stessa classe o gruppo di campi associati.
>
>Una volta apportate le modifiche ai nomi visualizzati dei campi di uno schema, tali modifiche vengono immediatamente applicate a tutti i set di dati esistenti in base a tale schema.

Per modificare il nome visualizzato di un campo schema, selezionare il campo nell’area di lavoro. Nella barra a destra, inserisci il nuovo nome in **[!UICONTROL Nome visualizzato]**.

![](../../images/ui/resources/schemas/display-name.png)

Seleziona **[!UICONTROL Applica]** nella barra a destra e l’area di lavoro viene aggiornata per mostrare il nuovo nome visualizzato del campo. Seleziona **[!UICONTROL Salva]** per applicare le modifiche allo schema.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Modificare la classe di uno schema {#change-class}

È possibile modificare la classe di uno schema in qualsiasi punto durante il processo di composizione iniziale prima che lo schema sia stato salvato.

>[!WARNING]
>
>La riassegnazione della classe per uno schema deve essere eseguita con estrema cautela. I gruppi di campi sono compatibili solo con determinate classi e pertanto la modifica della classe reimposterà l’area di lavoro e gli eventuali campi aggiunti.

Per riassegnare una classe, selezionare **[!UICONTROL Assegna]** sul lato sinistro del quadro.

![](../../images/ui/resources/schemas/assign-class-button.png)

Viene visualizzata una finestra di dialogo in cui viene visualizzato l’elenco di tutte le classi disponibili, incluse quelle definite dall’organizzazione (il proprietario è &quot;[!UICONTROL Cliente]&quot;) nonché le classi standard definite dall&#39;Adobe.

Selezionare una classe dall’elenco per visualizzarne la descrizione sul lato destro della finestra di dialogo. Puoi anche selezionare **[!UICONTROL Struttura della classe di anteprima]** per visualizzare i campi e i metadati associati alla classe. Seleziona **[!UICONTROL Assegna classe]** per continuare.

![](../../images/ui/resources/schemas/assign-class.png)

Viene visualizzata una nuova finestra di dialogo in cui viene richiesto di confermare l’assegnazione di una nuova classe. Seleziona **[!UICONTROL Assegna]** per confermare.

![](../../images/ui/resources/schemas/assign-confirm.png)

Dopo aver confermato la modifica della classe, l&#39;area di lavoro verrà reimpostata e tutti i progressi della composizione andranno persi.

## Passaggi successivi

Questo documento illustra le nozioni di base per la creazione e la modifica degli schemi nell’interfaccia utente di Platform. Si consiglia vivamente di rivedere il [esercitazione sulla creazione dello schema](../../tutorials/create-schema-ui.md) per un flusso di lavoro completo per la creazione di uno schema completo nell’interfaccia utente, inclusa la creazione di gruppi di campi personalizzati e tipi di dati per casi d’uso univoci.

Per ulteriori informazioni sulle funzionalità del [!UICONTROL Schemi] area di lavoro, vedi [[!UICONTROL Schemi] panoramica dell&#39;area di lavoro](../overview.md).

Per scoprire come gestire gli schemi nella [!DNL Schema Registry] API, vedi [guida all’endpoint degli schemi](../../api/schemas.md).
