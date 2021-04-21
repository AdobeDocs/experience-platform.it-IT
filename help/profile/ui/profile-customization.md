---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dettagli profilo;dettagli
title: Personalizzazione dei dettagli del profilo nell’interfaccia utente
description: 'Questa guida fornisce istruzioni passo per personalizzare il modo in cui i dati del profilo cliente in tempo reale vengono visualizzati nell’interfaccia utente di Adobe Experience Platform. '
topic-legacy: guide
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] personalizzazione dei dettagli  {#profile-detail-customization}

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare e interagire con i dati [!DNL Real-time Customer Profile] sotto forma di profili cliente. Le informazioni di profilo visualizzate nell’interfaccia utente sono state unite da più frammenti di profilo per formare una singola visualizzazione per ogni singolo cliente. Ciò include dettagli quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti mostrati nei profili possono anche essere modificati a livello organizzativo per visualizzare gli attributi preferiti [!DNL Profile]. Questa guida fornisce istruzioni passo passo per personalizzare il modo in cui i dati [!DNL Profile] vengono visualizzati nell’interfaccia utente di Platform.

Per una guida completa all&#39;interfaccia utente dei profili, visita la [guida all&#39;interfaccia utente dei profili](user-guide.md).

## Riordinare e ridimensionare le schede {#reorder-and-resize-cards}

Dalla scheda **[!UICONTROL Detail]** del profilo cliente, puoi selezionare **[!UICONTROL Modify dashboard]** per ridimensionare e riordinare le schede esistenti.

![](../images/profile-customization/profiles-modify-dashboard.png)

Dopo aver scelto di modificare il dashboard, è possibile riordinare le schede selezionando il titolo e trascinando e rilasciando le schede nell&#39;ordine desiderato. Potete anche ridimensionare una scheda selezionando il simbolo dell&#39;angolo nell&#39;angolo in basso a destra della scheda (`⌟`) e trascinando la scheda nella dimensione desiderata. In questo esempio, la scheda **[!UICONTROL Basic attributes]** viene ridimensionata.

![](../images/profile-customization/profiles-resize-cards.png)

La scheda selezionata si adatta alle dimensioni desiderate e le schede circostanti vengono riposizionate dinamicamente. Questo può causare lo spostamento di alcune schede in righe aggiuntive, che richiedono lo scorrimento verso il basso per visualizzare tutte le schede. Ad esempio, quando la scheda &quot;[!UICONTROL Basic attributes]&quot; viene ridimensionata, la scheda &quot;[!UICONTROL Linked identities]&quot; non è più visibile sulla riga superiore e ora viene visualizzata su una nuova seconda riga all&#39;interno del profilo (non visualizzata). Per restituire la scheda &quot;[!UICONTROL Linked identities]&quot; alla riga superiore, puoi trascinarla e rilasciarla nella posizione corrente della scheda &quot;[!UICONTROL Channel preferences]&quot;.

![](../images/profile-customization/profiles-card-resized.png)

## Modificare e rimuovere le schede

Oltre a ridimensionare e riordinare le schede, è possibile modificare il contenuto di alcune schede e rimuovere alcune schede dal dashboard completamente. Seleziona i puntini di sospensione (`...`) nell&#39;angolo in alto a destra della scheda per modificarla o rimuoverla. Viene visualizzato un menu a discesa con le opzioni per modificare o rimuovere la scheda, a seconda delle proprietà della scheda selezionata.

>[!NOTE]
>
>Non tutte le schede possono essere modificate o rimosse. Questo perché alcune schede contengono informazioni di sola lettura o richieste. Se una scheda non ha un puntino di sospensione nell&#39;angolo in alto a destra, contiene le informazioni necessarie in sola lettura e non può essere modificata né rimossa. Se una scheda ha dei puntini di sospensione nell&#39;angolo e la sua selezione mostra solo un&#39;opzione per rimuovere la scheda, le informazioni sulla scheda sono di sola lettura e non possono essere modificate.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Seleziona **[!UICONTROL Edit]** nel menu a discesa per aprire l&#39;area di lavoro **[!UICONTROL Edit widget]**, in cui puoi aggiornare il titolo della scheda, riordinare o rimuovere gli attributi visibili, oppure aggiungere altri attributi utilizzando il pulsante **[!UICONTROL Add attributes]** .

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Aggiungi attributi {#add-attributes}

Dalla schermata **[!UICONTROL Edit widget]** , seleziona **[!UICONTROL Add attributes]** nell’angolo in alto a destra della scheda per iniziare ad aggiungere attributi a tale scheda.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Quando si apre la finestra di dialogo **[!UICONTROL Select union schema field]** , il lato sinistro della finestra di dialogo mostra lo schema di unione completo [!UICONTROL XDM Individual Profile], con i campi nidificati sotto di essa. Per ulteriori informazioni sugli schemi di unione, consulta la sezione [schemi di unione della [!DNL Profile] guida utente](user-guide.md#union-schema).

La sezione **[!UICONTROL Selected Attributes]** a destra della finestra di dialogo mostra gli attributi attualmente inclusi nella scheda che si sta modificando. Puoi rimuovere e riordinare gli attributi anche qui. Vengono visualizzati il numero totale di attributi selezionati, nonché il numero massimo di attributi (20) che possono essere aggiunti a una singola scheda.

![](../images/profile-customization/profiles-select-field-before.png)

Puoi selezionare uno dei campi dello schema unione disponibili per personalizzare gli attributi nella scheda che stai modificando. I campi selezionati sono contrassegnati da un segno di spunta accanto a essi e vengono aggiunti automaticamente all’elenco degli attributi selezionati. Dopo aver aggiunto tutti gli attributi che desideri visualizzare sulla scheda, scegli **[!UICONTROL Select]** per tornare alla schermata **[!UICONTROL Edit widget]**.

![](../images/profile-customization/profiles-select-field-after.png)

Quando torni alla schermata **[!UICONTROL Edit widget]** , l’elenco degli attributi nella scheda deve ora essere aggiornato per riflettere le tue scelte. Potete comunque rimuovere o riordinare gli attributi della scheda o modificarne il titolo in base alle necessità. Una volta completate le modifiche, seleziona **[!UICONTROL Save]** per salvarle.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Dopo il salvataggio, vieni riportato alla scheda **[!UICONTROL Detail]** in cui sono visibili la scheda e gli attributi aggiornati.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Aggiungi una nuova scheda {#add-a-new-card}

Per personalizzare ulteriormente l’aspetto dei profili all’interno di Experience Platform, puoi scegliere di aggiungere nuove schede al dashboard e selezionare gli attributi da visualizzare su tali schede. Per iniziare, seleziona **[!UICONTROL Modify dashboard]** nella scheda **[!UICONTROL Detail]** .

![](../images/profile-customization/profiles-modify-dashboard.png)

Quindi, seleziona **[!UICONTROL Add widget]** nell’angolo in alto a sinistra del dashboard.

![](../images/profile-customization/profiles-add-widget.png)

Scegliendo di aggiungere una nuova scheda si apre la schermata **[!UICONTROL Edit widget]** in cui è possibile fornire un titolo alla nuova scheda e scegliere gli attributi che si desidera visualizzare nella scheda. Per iniziare ad aggiungere attributi alla scheda, seleziona **[!UICONTROL Add attributes]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Quando si apre la finestra di dialogo **[!UICONTROL Select union schema field]** , il lato sinistro della finestra di dialogo mostra lo schema di unione completo [!UICONTROL XDM Individual Profile] e la sezione **[!UICONTROL Selected Attributes]** sul lato destro della finestra di dialogo mostra gli attributi selezionati per la scheda. Per ulteriori informazioni sull&#39;aggiunta di attributi, consulta la sezione [sull&#39;aggiunta di attributi](#add-attributes) che viene visualizzata in precedenza in questo documento.

Vengono visualizzati il numero totale di attributi selezionati, nonché il numero massimo di attributi (20) che possono essere aggiunti a una singola scheda. Puoi anche rimuovere e riordinare gli attributi selezionati da questa schermata. Dopo aver aggiunto tutti gli attributi che desideri visualizzare sulla scheda, scegli **[!UICONTROL Select]** per tornare alla schermata **[!UICONTROL Edit widget]**.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Quando ritorni alla schermata **[!UICONTROL Edit widget]** , l’elenco degli attributi nella scheda deve riflettere le scelte della schermata precedente. Potete inoltre riordinare e rimuovere gli attributi della scheda in base alle esigenze.

Per salvare la nuova scheda è innanzitutto necessario fornire un **[!UICONTROL Card title]**, quindi sarà possibile selezionare **[!UICONTROL Save]** e completare il processo di creazione della scheda.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Dopo il salvataggio, vieni riportato alla scheda **[!UICONTROL Detail]** in cui sono visibili la nuova scheda e i nuovi attributi.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Ripristina schede predefinite

Se in qualsiasi momento decidi di voler ripristinare le schede predefinite che sono state rimosse, puoi farlo in modo rapido e semplice. Innanzitutto, seleziona **[!UICONTROL Modify dashboard]**, quindi seleziona **[!UICONTROL Restore default cards]**. Una volta visualizzate le schede predefinite, è possibile selezionare **[!UICONTROL Save]** per salvare le modifiche oppure selezionare **[!UICONTROL Cancel]** se non si desidera ripristinare le schede predefinite.

![](../images/profile-customization/profiles-restore-default.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di aggiornare la visualizzazione del profilo per la tua organizzazione, tra cui l’aggiunta e la rimozione di schede, la modifica di dettagli e attributi della scheda e il riordinamento e il ridimensionamento delle schede. Per ulteriori informazioni sull&#39;utilizzo dei dati [!DNL Profile] nell&#39;interfaccia utente di Experience Platform, consulta la [[!DNL Profile] guida utente](user-guide.md).
