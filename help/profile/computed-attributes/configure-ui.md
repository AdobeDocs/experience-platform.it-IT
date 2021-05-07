---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Come configurare un campo attributo calcolato
topic-legacy: guide
type: Documentation
description: Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Per configurare un attributo calcolato, devi innanzitutto identificare il campo che conterrà il valore dell’attributo calcolato. È possibile creare il campo utilizzando un gruppo di campi dello schema per aggiungere il campo a uno schema esistente oppure selezionando un campo già definito in uno schema.
translation-type: tm+mt
source-git-commit: 6e0f7578d0818f88e13b963f64cb2de6729f0574
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---


# (Alfa) Configura un campo attributo calcolato nell’interfaccia utente

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per configurare un attributo calcolato, devi innanzitutto identificare il campo che conterrà il valore dell’attributo calcolato. È possibile creare il campo utilizzando un gruppo di campi dello schema per aggiungere il campo a uno schema esistente oppure selezionando un campo già definito in uno schema.

>[!NOTE]
>
>Gli attributi calcolati non possono essere aggiunti ai campi all’interno di gruppi di campi definiti da Adobe. Il campo deve trovarsi all’interno dello spazio dei nomi `tenant` , ovvero deve essere un campo definito e aggiunto a uno schema.

Per definire con successo un campo attributo calcolato, lo schema deve essere abilitato per [!DNL Profile] e deve essere visualizzato come parte dello schema di unione per la classe su cui si basa lo schema. Per ulteriori informazioni sugli schemi e le unioni abilitati [!DNL Profile], consulta la sezione della [!DNL Schema Registry] guida per gli sviluppatori in [abilitazione di uno schema per Profilo e visualizzazione degli schemi di unione](../../xdm/api/getting-started.md). È inoltre consigliabile consultare la sezione [sui sindacati](../../xdm/schema/composition.md) nella documentazione di base sulla composizione dello schema.

Il flusso di lavoro in questa esercitazione utilizza uno schema abilitato [!DNL Profile] e segue i passaggi per definire un nuovo gruppo di campi contenente il campo dell’attributo calcolato e assicurarsi che sia lo spazio dei nomi corretto. Se disponi già di un campo nello spazio dei nomi corretto all’interno di uno schema abilitato per il profilo, puoi procedere direttamente al passaggio [creazione di un attributo calcolato](#create-a-computed-attribute).

## Visualizzare uno schema

I passaggi seguenti utilizzano l’interfaccia utente di Adobe Experience Platform per individuare uno schema, aggiungere un gruppo di campi e definire un campo. Se preferisci utilizzare l&#39;API [!DNL Schema Registry], fai riferimento alla [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md) per i passaggi su come creare un gruppo di campi, aggiungere un gruppo di campi a uno schema e abilitare uno schema da utilizzare con [!DNL Real-time Customer Profile].

Nell’interfaccia utente, fai clic su **[!UICONTROL Schemas]** nella barra a sinistra e utilizza la barra di ricerca nella scheda **[!UICONTROL Browse]** per trovare rapidamente lo schema da aggiornare.

![](../images/computed-attributes/Schemas-Browse.png)

Una volta individuato lo schema, fai clic sul suo nome per aprire [!DNL Schema Editor] in cui puoi apportare modifiche allo schema.

![](../images/computed-attributes/Schema-Editor.png)

## Creare un gruppo di campi

Per creare un nuovo gruppo di campi, fai clic su **[!UICONTROL Add]** accanto a **[!UICONTROL Field groups]** nella sezione **[!UICONTROL Composition]** a sinistra dell’editor. Viene visualizzata la finestra di dialogo **[!UICONTROL Add field group]** in cui sono disponibili i gruppi di campi esistenti. Fai clic sul pulsante di scelta per **[!UICONTROL Create new field group]** per definire il nuovo gruppo di campi.

Assegna un nome e una descrizione al gruppo di campi e fai clic su **[!UICONTROL Add field group]** al termine.

![](../images/computed-attributes/Add-field-group.png)

## Aggiungi un campo attributo calcolato allo schema

Il nuovo gruppo di campi deve ora essere visualizzato nella sezione &quot;[!UICONTROL Field groups]&quot; in &quot;[!UICONTROL Composition]&quot;. Fai clic sul nome del gruppo di campi e nella sezione **[!UICONTROL Structure]** dell’editor vengono visualizzati più pulsanti **[!UICONTROL Add field]** .

Selezionare **[!UICONTROL Add field]** accanto al nome dello schema per aggiungere un campo di livello superiore, oppure è possibile aggiungere il campo in un punto qualsiasi dello schema desiderato.

Dopo aver fatto clic su **[!UICONTROL Add field]** viene aperto un nuovo oggetto denominato ID tenant, che mostra che il campo si trova nello spazio dei nomi corretto. All&#39;interno dell&#39;oggetto viene visualizzato un **[!UICONTROL New field]**. Questo se il campo in cui verrà definito l&#39;attributo calcolato.

![](../images/computed-attributes/New-field.png)

## Configura il campo

Utilizzando la sezione **[!UICONTROL Field properties]** sul lato destro dell’editor, fornisci le informazioni necessarie per il nuovo campo, compreso il nome, il nome visualizzato e il tipo.

>[!NOTE]
>
>Il tipo del campo deve essere lo stesso tipo del valore dell&#39;attributo calcolato. Ad esempio, se il valore dell’attributo calcolato è una stringa, il campo definito nello schema deve essere una stringa.

Al termine, fai clic su **[!UICONTROL Apply]** e il nome del campo e il relativo tipo verranno visualizzati nella sezione **[!UICONTROL Structure]** dell’editor.

![](../images/computed-attributes/Apply.png)

## Abilita schema per [!DNL Profile]

Prima di continuare, assicurati che lo schema sia stato abilitato per [!DNL Profile]. Fai clic sul nome dello schema nella sezione **[!UICONTROL Structure]** dell’editor in modo che venga visualizzata la scheda **[!UICONTROL Schema Properties]** . Se il cursore **[!UICONTROL Profile]** è blu, lo schema è stato abilitato per [!DNL Profile].

>[!NOTE]
>
>Impossibile annullare l&#39;abilitazione di uno schema per [!DNL Profile]. Se si fa clic sul dispositivo di scorrimento una volta abilitato, non è necessario rischiare di disattivarlo.

![](../images/computed-attributes/Profile.png)

Ora puoi fare clic su **[!UICONTROL Save]** per salvare lo schema aggiornato e continuare con il resto dell’esercitazione utilizzando l’API.

## Passaggi successivi

Ora che hai creato un campo in cui verrà memorizzato il valore dell’attributo calcolato, puoi creare l’attributo calcolato utilizzando l’endpoint API `/computedattributes`. Per passaggi dettagliati per la creazione di un attributo calcolato nell&#39;API, segui i passaggi descritti nella [guida all&#39;endpoint API degli attributi calcolati](ca-api.md) .