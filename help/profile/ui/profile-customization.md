---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Personalizzazione dei dettagli del profilo
description: 'Questa guida fornisce istruzioni dettagliate per personalizzare il modo in cui i dati del profilo cliente in tempo reale vengono visualizzati nell’interfaccia utente di Adobe Experience Platform. '
topic: guide
translation-type: tm+mt
source-git-commit: b08644102e6455d4c4c8b03e747411d3c05c7deb
workflow-type: tm+mt
source-wordcount: '1151'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] personalizzazione dei dettagli {#profile-detail-customization}

All&#39;interno dell&#39;interfaccia utente di Adobe Experience Platform, è possibile visualizzare e interagire con [!DNL Real-time Customer Profile] i dati sotto forma di profili cliente. Le informazioni di profilo visualizzate nell’interfaccia sono state unite da più frammenti di profilo per formare una singola vista di ciascun cliente. Ciò include dettagli quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti mostrati nei profili possono essere modificati anche a livello organizzativo per visualizzare [!DNL Profile] gli attributi preferiti. Questa guida fornisce istruzioni dettagliate per personalizzare il modo in cui [!DNL Profile] i dati vengono visualizzati nell’interfaccia utente della piattaforma.

Per una guida completa all’ [!UICONTROL Profiles] interfaccia utente, visita la guida [utente](user-guide.md)Profilo.

## Riordinare e ridimensionare le schede {#reorder-and-resize-cards}

Dalla [!UICONTROL Detail] scheda del profilo cliente, potete selezionare **[!UICONTROL Modify dashboard]** per ridimensionare e riordinare le schede esistenti.

![](../images/profile-customization/profiles-modify-dashboard.png)

Dopo aver scelto di modificare il dashboard, potete riordinare le schede selezionando il titolo della scheda e trascinando e rilasciando le schede nell&#39;ordine desiderato. Potete anche ridimensionare una scheda selezionando il simbolo dell&#39;angolo nell&#39;angolo inferiore destro della scheda (`⌟`) e trascinando la scheda nella dimensione desiderata. In questo esempio, la **[!UICONTROL Basic attributes]** scheda viene ridimensionata.

![](../images/profile-customization/profiles-resize-cards.png)

La scheda selezionata si adatta alle dimensioni desiderate e le schede circostanti vengono riposizionate in modo dinamico. Ciò potrebbe causare lo spostamento di alcune schede in righe aggiuntive, che richiedono lo scorrimento verso il basso per visualizzare tutte le schede. Ad esempio, quando la [!UICONTROL Basic attributes] scheda viene ridimensionata, la [!UICONTROL Linked identities] scheda non è più visibile sulla riga superiore e ora viene visualizzata su una nuova riga all&#39;interno del profilo (non visualizzata). Per riportare la [!UICONTROL Linked identities] scheda nella riga superiore, potete trascinarla e rilasciarla nella posizione corrente della [!UICONTROL Channel preferences] scheda.

![](../images/profile-customization/profiles-card-resized.png)

## Modificare e rimuovere le schede

Oltre a ridimensionare e riordinare le schede, potete modificare il contenuto di alcune schede e rimuovere alcune schede dal dashboard completamente. Selezionate le ellissi (`...`) nell&#39;angolo superiore destro della scheda per modificarla o rimuoverla. Si apre un menu a discesa con opzioni per modificare o rimuovere la scheda, a seconda delle proprietà della scheda selezionata.

>[!NOTE]
>
>Non tutte le schede possono essere modificate o rimosse. Questo perché alcune schede contengono informazioni di sola lettura o obbligatorie. Se una scheda non ha un&#39;ellissi nell&#39;angolo superiore destro, contiene le informazioni di sola lettura E richieste e non può essere modificata né rimossa. Se una scheda ha delle ellissi nell&#39;angolo e la sua selezione mostra solo un&#39;opzione per rimuovere la scheda, le informazioni sulla scheda sono di sola lettura e non possono essere modificate.

![](../images/profile-customization/profiles-edit-remove-resized.png)

Selezionate **[!UICONTROL Edit]** nel menu a discesa per aprire l&#39; **[!UICONTROL Edit widget]** area di lavoro, in cui potete aggiornare il titolo della scheda, riordinare o rimuovere gli attributi visibili, oppure aggiungere altri attributi utilizzando il [!UICONTROL Add attributes] pulsante.

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## Aggiungi attributi {#add-attributes}

Dalla [!UICONTROL Edit widget] schermata, selezionate **[!UICONTROL Add attributes]** nell&#39;angolo superiore destro della scheda per iniziare ad aggiungere attributi alla scheda.

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

Quando si apre la [!UICONTROL Select union schema field] finestra di dialogo, sul lato sinistro viene visualizzato lo schema di [!UICONTROL XDM Individual Profile] unione completo, con campi nidificati al di sotto. Per ulteriori informazioni sugli schemi di unione, fare riferimento alla sezione [schemi di unione della [!DNL Profile] guida](user-guide.md#union-schema)utente.

La **[!UICONTROL Selected Attributes]** sezione a destra della finestra di dialogo mostra gli attributi attualmente inclusi nella scheda che si sta modificando. Potete anche rimuovere e riordinare gli attributi. Viene visualizzato il numero totale di attributi selezionati, nonché il numero massimo di attributi (20) che possono essere aggiunti a una singola scheda.

![](../images/profile-customization/profiles-select-field-before.png)

Potete selezionare uno qualsiasi dei campi dello schema unione disponibili per personalizzare gli attributi della scheda che state modificando. I campi selezionati sono contrassegnati da un segno di spunta e vengono automaticamente aggiunti all’elenco degli attributi selezionati. Dopo aver aggiunto tutti gli attributi che desiderate visualizzare sulla scheda, scegliete **[!UICONTROL Select]** di tornare alla [!UICONTROL Edit widget] schermata.

![](../images/profile-customization/profiles-select-field-after.png)

Quando tornate alla [!UICONTROL Edit widget] schermata, l&#39;elenco degli attributi sulla scheda dovrebbe ora essere aggiornato per riflettere le scelte. Potete comunque rimuovere o riordinare gli attributi della scheda o modificare il titolo della scheda in base alle esigenze. Una volta completate le modifiche, selezionate **[!UICONTROL Save]** per salvarle.

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

Dopo il salvataggio, viene nuovamente visualizzata la [!UICONTROL Detail] scheda in cui sono visibili la scheda e gli attributi aggiornati.

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Add a new card {#add-a-new-card}

Per personalizzare ulteriormente l&#39;aspetto dei profili all&#39;interno  Experience Platform, potete scegliere di aggiungere nuove schede al dashboard e selezionare gli attributi che desiderate visualizzare su tali schede. Per iniziare, selezionate **[!UICONTROL Modify dashboard]** sulla [!UICONTROL Detail] scheda.

![](../images/profile-customization/profiles-modify-dashboard.png)

Quindi, selezionate **[!UICONTROL Add widget]** nell&#39;angolo superiore sinistro del dashboard.

![](../images/profile-customization/profiles-add-widget.png)

Scegliendo di aggiungere una nuova scheda si apre la [!UICONTROL Edit widget] schermata in cui potete fornire un titolo alla nuova scheda e scegliere gli attributi che desiderate vengano visualizzati. Per iniziare ad aggiungere attributi alla scheda, selezionate **[!UICONTROL Add attributes]**.

![](../images/profile-customization/profiles-edit-new-widget.png)

Quando si apre la **[!UICONTROL Select union schema field]** finestra di dialogo, il lato sinistro della finestra di dialogo mostra lo schema [!UICONTROL XDM Individual Profile] dell&#39;unione completo e la **[!UICONTROL Selected Attributes]** sezione sul lato destro della finestra di dialogo mostra gli attributi selezionati per la scheda. Per ulteriori informazioni sull&#39;aggiunta di attributi, consultate la [sezione sull&#39;aggiunta di attributi](#add-attributes) che viene visualizzata in precedenza in questo documento.

Viene visualizzato il numero totale di attributi selezionati, nonché il numero massimo di attributi (20) che possono essere aggiunti a una singola scheda. Potete inoltre rimuovere e riordinare gli attributi selezionati da questa schermata. Dopo aver aggiunto tutti gli attributi che desiderate visualizzare sulla scheda, scegliete **[!UICONTROL Select]** di tornare alla [!UICONTROL Edit widget] schermata.

![](../images/profile-customization/profiles-add-fields-new-widget.png)

Quando tornate alla [!UICONTROL Edit widget] schermata, l&#39;elenco degli attributi sulla scheda dovrebbe riflettere le scelte effettuate dalla schermata precedente. Potete anche riordinare e rimuovere gli attributi della scheda in base alle esigenze.

Per salvare la nuova scheda è prima necessario fornire un **[!UICONTROL Card title]**, quindi sarà possibile selezionare **[!UICONTROL Save]** e completare il processo di creazione della scheda.

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

Dopo il salvataggio, tornate alla [!UICONTROL Detail] scheda in cui sono visibili la nuova scheda e i nuovi attributi.

![](../images/profile-customization/profiles-detail-new-widget.png)

## Ripristina schede predefinite

Se in qualsiasi momento decidete di rimuovere le modifiche e tornare alla visualizzazione predefinita, potete ripristinare rapidamente e facilmente tutte le schede e gli attributi predefiniti. A questo scopo, selezionate **[!UICONTROL Modify dashboard]**, quindi selezionate **[!UICONTROL Restore default cards]**. In questo modo verranno rimosse tutte le personalizzazioni (incluso il ridimensionamento) effettuate. Potete quindi selezionare **[!UICONTROL Save]** di salvare le modifiche o, se non desiderate ripristinare le modifiche predefinite, selezionare **[!UICONTROL Cancel]** per mantenere le modifiche apportate.

>[!NOTE]
>
>Fate attenzione quando ripristinate le schede e gli attributi predefiniti. Una volta ripristinato e salvato il valore predefinito, l&#39;unico modo per tornare alle personalizzazioni della vista è crearle nuovamente utilizzando i passaggi descritti in questo documento.

![](../images/profile-customization/profiles-restore-default.png)

## Passaggi successivi

Seguendo questo documento dovreste essere in grado di aggiornare la visualizzazione profilo per la vostra organizzazione, inclusa l&#39;aggiunta e la rimozione di schede, la modifica dei dettagli e degli attributi della scheda e il riordinamento e ridimensionamento delle schede. Per ulteriori informazioni sull&#39;utilizzo [!DNL Profile] dei dati nell&#39;interfaccia utente del Experience Platform , fare riferimento alla guida [[!DNL Profile] ](user-guide.md)utente.