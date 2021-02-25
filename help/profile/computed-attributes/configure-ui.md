---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Come configurare un campo attributo calcolato
topic: guida
type: Documentazione
description: Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Per configurare un attributo calcolato, è innanzitutto necessario identificare il campo che includerà il valore dell'attributo calcolato. Questo campo può essere creato utilizzando un mixin per aggiungere il campo a uno schema esistente, oppure selezionando un campo già definito all'interno di uno schema.
translation-type: tm+mt
source-git-commit: 92533f732cc14b57d2a0a34ce9afe99554f9af04
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 1%

---


# (Alfa) Configura un campo attributo calcolato nell’interfaccia utente

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per configurare un attributo calcolato, è innanzitutto necessario identificare il campo che includerà il valore dell&#39;attributo calcolato. Questo campo può essere creato utilizzando un mixin per aggiungere il campo a uno schema esistente, oppure selezionando un campo già definito all&#39;interno di uno schema.

>[!NOTE]
>
>Gli attributi calcolati non possono essere aggiunti ai campi all&#39;interno  mixin definiti dal Adobe. Il campo deve essere all&#39;interno dello spazio dei nomi `tenant`, ovvero deve essere un campo definito e aggiunto a uno schema.

Per definire con successo un campo attributo calcolato, lo schema deve essere abilitato per [!DNL Profile] e deve essere visualizzato come parte dello schema unione per la classe su cui si basa lo schema. Per ulteriori informazioni sugli schemi e sulle unioni [!DNL Profile] abilitati, consultare la sezione della [!DNL Schema Registry] guida per gli sviluppatori in [abilitazione di uno schema per il profilo e visualizzazione degli schemi di unione](../../xdm/api/getting-started.md). Si consiglia inoltre di consultare la sezione [sui sindacati](../../xdm/schema/composition.md) nella documentazione di base sulla composizione dello schema.

Il flusso di lavoro di questa esercitazione utilizza uno schema abilitato per [!DNL Profile] e segue i passaggi per definire un nuovo mixin contenente il campo dell&#39;attributo calcolato e assicurarsi che sia lo spazio dei nomi corretto. Se si dispone già di un campo che si trova nello spazio dei nomi corretto all&#39;interno di uno schema abilitato per il profilo, è possibile procedere direttamente al passaggio [creazione di un attributo calcolato](#create-a-computed-attribute).

## Visualizzare uno schema

I passaggi successivi utilizzano l&#39;interfaccia utente di Adobe Experience Platform per individuare uno schema, aggiungere un mixin e definire un campo. Se si preferisce utilizzare l&#39;API [!DNL Schema Registry], fare riferimento alla [Guida per gli sviluppatori del Registro di sistema dello schema](../../xdm/api/getting-started.md) per istruzioni su come creare un mixin, aggiungere un mixin a uno schema e attivare uno schema da utilizzare con [!DNL Real-time Customer Profile].

Nell&#39;interfaccia utente, fare clic su **[!UICONTROL Schemas]** nella barra a sinistra e utilizzare la barra di ricerca nella scheda **[!UICONTROL Browse]** per trovare rapidamente lo schema da aggiornare.

![](../images/computed-attributes/Schemas-Browse.png)

Una volta individuato lo schema, fare clic sul suo nome per aprire il [!DNL Schema Editor] in cui è possibile apportare modifiche allo schema.

![](../images/computed-attributes/Schema-Editor.png)

## Creare un mixin

Per creare un nuovo mixin, fate clic su **[!UICONTROL Add]** accanto a **[!UICONTROL Mixins]** nella sezione **[!UICONTROL Composition]** a sinistra dell&#39;editor. Viene visualizzata la finestra di dialogo **[!UICONTROL Add mixin]** in cui sono disponibili i mixin esistenti. Fare clic sul pulsante di scelta **[!UICONTROL Create new mixin]** per definire il nuovo mixin.

Assegna al mixin un nome e una descrizione, quindi fai clic su **[!UICONTROL Add mixin]** al termine.

![](../images/computed-attributes/Add-mixin.png)

## Aggiunta di un campo attributo calcolato allo schema

Il nuovo mixin dovrebbe ora essere visualizzato nella sezione &quot;[!UICONTROL Mixins]&quot; in &quot;[!UICONTROL Composition]&quot;. Fare clic sul nome del mixin e più **[!UICONTROL Add field]** pulsanti appariranno nella sezione **[!UICONTROL Structure]** dell&#39;editor.

Selezionare **[!UICONTROL Add field]** accanto al nome dello schema per aggiungere un campo di primo livello oppure è possibile aggiungere il campo in qualsiasi punto dello schema desiderato.

Dopo aver fatto clic su **[!UICONTROL Add field]** si apre un nuovo oggetto, denominato per l&#39;ID tenant, che mostra che il campo è nello spazio dei nomi corretto. All&#39;interno dell&#39;oggetto viene visualizzato un **[!UICONTROL New field]**. Questo se il campo in cui si definisce l&#39;attributo calcolato.

![](../images/computed-attributes/New-field.png)

## Configurare il campo

Utilizzando la sezione **[!UICONTROL Field properties]** a destra dell&#39;editor, fornite le informazioni necessarie per il nuovo campo, incluso nome, nome visualizzato e tipo.

>[!NOTE]
>
>Il tipo del campo deve essere lo stesso tipo del valore dell&#39;attributo calcolato. Ad esempio, se il valore dell&#39;attributo calcolato è una stringa, il campo definito nello schema deve essere una stringa.

Al termine, fare clic su **[!UICONTROL Apply]**, il nome del campo e il relativo tipo verranno visualizzati nella sezione **[!UICONTROL Structure]** dell&#39;editor.

![](../images/computed-attributes/Apply.png)

## Abilita schema per [!DNL Profile]

Prima di continuare, assicurarsi che lo schema sia stato abilitato per [!DNL Profile]. Fare clic sul nome dello schema nella sezione **[!UICONTROL Structure]** dell&#39;editor in modo che venga visualizzata la scheda **[!UICONTROL Schema Properties]**. Se il cursore **[!UICONTROL Profile]** è blu, lo schema è stato abilitato per [!DNL Profile].

>[!NOTE]
>
>L&#39;abilitazione di uno schema per [!DNL Profile] non può essere annullata, quindi se si fa clic sul dispositivo di scorrimento dopo che è stato abilitato, non è necessario rischiare di disattivarlo.

![](../images/computed-attributes/Profile.png)

Ora è possibile fare clic su **[!UICONTROL Save]** per salvare lo schema aggiornato e continuare con il resto dell&#39;esercitazione utilizzando l&#39;API.

## Passaggi successivi

Ora che avete creato un campo in cui memorizzare il valore dell&#39;attributo calcolato, potete creare l&#39;attributo calcolato utilizzando l&#39;endpoint `/computedattributes` API. Per la procedura dettagliata per la creazione di un attributo calcolato nell&#39;API, segui i passaggi forniti nella [guida dell&#39;endpoint API degli attributi calcolati](ca-api.md).