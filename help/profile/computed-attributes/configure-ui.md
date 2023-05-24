---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Come configurare un campo attributo calcolato
type: Documentation
description: Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Per configurare un attributo calcolato, devi innanzitutto identificare il campo che conterrà il valore dell’attributo calcolato. Questo campo può essere creato utilizzando un gruppo di campi schema per aggiungere il campo a uno schema esistente oppure selezionando un campo già definito all’interno di uno schema.
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alfa) Configurare un campo attributo calcolato nell’interfaccia utente di

>[!IMPORTANT]
>
>La funzionalità degli attributi calcolati è attualmente in formato alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per configurare un attributo calcolato, devi innanzitutto identificare il campo che conterrà il valore dell’attributo calcolato. Questo campo può essere creato utilizzando un gruppo di campi schema per aggiungere il campo a uno schema esistente oppure selezionando un campo già definito all’interno di uno schema.

>[!NOTE]
>
>Non è possibile aggiungere attributi calcolati a campi all’interno di gruppi di campi definiti da Adobe. Il campo deve trovarsi all’interno del `tenant` spazio dei nomi, ovvero deve essere un campo definito e aggiunto a uno schema.

Per definire correttamente un campo attributo calcolato, lo schema deve essere abilitato per [!DNL Profile] e vengono visualizzati come parte dello schema di unione per la classe su cui si basa lo schema. Per ulteriori informazioni su [!DNL Profile]- abilitati, consulta la sezione della sezione [!DNL Schema Registry] sezione della guida per sviluppatori su [abilitazione di uno schema per il profilo e visualizzazione degli schemi di unione](../../xdm/api/getting-started.md). Si consiglia inoltre di rivedere [sezione sulle unioni](../../xdm/schema/composition.md) nella documentazione di base sulla composizione dello schema.

Il flusso di lavoro di questa esercitazione utilizza [!DNL Profile]dello schema abilitato e segue i passaggi per definire un nuovo gruppo di campi contenente il campo attributo calcolato e per verificare che sia lo spazio dei nomi corretto. Se disponi già di un campo nello spazio dei nomi corretto all’interno di uno schema abilitato per il profilo, puoi procedere direttamente al passaggio per [creazione di un attributo calcolato](#create-a-computed-attribute).

## Visualizzare uno schema

I passaggi seguenti utilizzano l’interfaccia utente di Adobe Experience Platform per individuare uno schema, aggiungere un gruppo di campi e definire un campo. Se preferisce utilizzare il [!DNL Schema Registry] API, fare riferimento al [Guida per gli sviluppatori del registro dello schema](../../xdm/api/getting-started.md) per i passaggi su come creare un gruppo di campi, aggiungi un gruppo di campi a uno schema e abilita uno schema da utilizzare con [!DNL Real-Time Customer Profile].

Nell’interfaccia utente di, fai clic su **[!UICONTROL Schemi]** nella barra a sinistra e utilizza la barra di ricerca nella **[!UICONTROL Sfoglia]** per trovare rapidamente lo schema da aggiornare.

![](../images/computed-attributes/Schemas-Browse.png)

Dopo aver individuato lo schema, fai clic sul nome per aprire [!DNL Schema Editor] dove è possibile apportare modifiche allo schema.

![](../images/computed-attributes/Schema-Editor.png)

## Crea un gruppo di campi

Per creare un nuovo gruppo di campi, fare clic su **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]** nel **[!UICONTROL Composizione]** a sinistra dell’editor. Verrà aperto il **[!UICONTROL Aggiungi gruppo di campi]** in cui è possibile visualizzare i gruppi di campi esistenti. Fai clic sul pulsante di opzione per **[!UICONTROL Crea nuovo gruppo di campi]** per definire il nuovo gruppo di campi.

Assegna un nome e una descrizione al gruppo di campi, quindi fai clic su **[!UICONTROL Aggiungi gruppo di campi]** al termine.

![](../images/computed-attributes/Add-field-group.png)

## Aggiungere un campo attributo calcolato allo schema

Il nuovo gruppo di campi deve ora essere visualizzato in &quot;[!UICONTROL Gruppi di campi]&quot; sezione in &quot;[!UICONTROL Composizione]&quot;. Fai clic sul nome del gruppo di campi e su più **[!UICONTROL Aggiungi campo]** verranno visualizzati nel **[!UICONTROL Struttura]** sezione dell’editor.

Seleziona **[!UICONTROL Aggiungi campo]** accanto al nome dello schema per aggiungere un campo di livello principale, oppure puoi selezionare di aggiungere il campo in qualsiasi punto dello schema desiderato.

Dopo aver fatto clic su **[!UICONTROL Aggiungi campo]** viene aperto un nuovo oggetto, denominato in base all’ID tenant, che indica che il campo si trova nello spazio dei nomi corretto. All’interno di tale oggetto, un **[!UICONTROL Nuovo campo]** viene visualizzato. Ciò si verifica se il campo in cui viene definito l’attributo calcolato.

![](../images/computed-attributes/New-field.png)

## Configurare il campo

Utilizzo di **[!UICONTROL Proprietà campo]** sul lato destro dell’editor, fornisci le informazioni necessarie per il nuovo campo, tra cui nome, nome visualizzato e tipo.

>[!NOTE]
>
>Il tipo del campo deve corrispondere al valore dell&#39;attributo calcolato. Ad esempio, se il valore dell’attributo calcolato è una stringa, il campo definito nello schema deve essere una stringa.

Al termine, fai clic su **[!UICONTROL Applica]** e il nome del campo, così come il relativo tipo, verranno visualizzati nel **[!UICONTROL Struttura]** sezione dell’editor.

![](../images/computed-attributes/Apply.png)

## Abilita schema per [!DNL Profile]

Prima di continuare, assicurati che lo schema sia stato abilitato per [!DNL Profile]. Fai clic sul nome dello schema in **[!UICONTROL Struttura]** dell&#39;editor in modo che il **[!UICONTROL Proprietà schema]** viene visualizzata la scheda. Se il **[!UICONTROL Profilo]** il cursore è blu, lo schema è stato abilitato per [!DNL Profile].

>[!NOTE]
>
>Abilitazione di uno schema per [!DNL Profile] non può essere annullato, quindi se si fa clic sul dispositivo di scorrimento una volta attivato, non è necessario rischiare di disabilitarlo.

![](../images/computed-attributes/Profile.png)

Ora puoi fare clic su **[!UICONTROL Salva]** per salvare lo schema aggiornato e continuare con il resto dell’esercitazione utilizzando l’API.

## Passaggi successivi

Dopo aver creato un campo in cui memorizzare il valore dell&#39;attributo calcolato, è possibile creare l&#39;attributo calcolato utilizzando `/computedattributes` Endpoint API Per i passaggi dettagliati della creazione di un attributo calcolato nell’API, segui i passaggi descritti in [guida dell’endpoint API per attributi calcolati](ca-api.md).