---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;personalizzazione;dettagli profilo;dettagli profilo;dettagli
title: Personalizzazione dei dettagli del profilo nell’interfaccia utente
description: Questa guida fornisce istruzioni dettagliate per personalizzare il modo in cui i dati Real-Time Customer Profile vengono visualizzati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] personalizzazione dettagli {#profile-detail-customization}

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare e interagire con [!DNL Real-Time Customer Profile] sotto forma di profili cliente. Le informazioni di profilo visualizzate nell’interfaccia utente di sono state unite da più frammenti di profilo per formare un’unica vista per ogni singolo cliente. Ciò include dettagli quali attributi di base, identità collegate e preferenze di canale. I campi predefiniti visualizzati nei profili possono anche essere modificati a livello organizzativo per visualizzare i campi preferiti [!DNL Profile] attributi. Questa guida fornisce istruzioni dettagliate per personalizzare il modo in cui [!DNL Profile] I dati di vengono visualizzati nell’interfaccia di Platform.

Per una guida completa all’interfaccia utente Profili, visita [Guida all’interfaccia utente del profilo](user-guide.md).

## Riordinare e ridimensionare le schede {#reorder-and-resize-cards}

Dalla sezione **[!UICONTROL Dettaglio]** del profilo cliente, puoi selezionare **[!UICONTROL Personalizza dettagli profilo]** per ridimensionare e riordinare le schede esistenti.

![Il pulsante Personalizza dettagli profilo è evidenziato nella dashboard Profilo.](../images/profile-customization/customize-profile-details.png)

Dopo aver scelto di modificare il dashboard, puoi riordinare le schede selezionando il titolo e trascinandole e rilasciandole nell’ordine desiderato. È inoltre possibile ridimensionare una scheda selezionando il simbolo dell&#39;angolo nell&#39;angolo inferiore destro della scheda (`⌟`) e trascinando la scheda alle dimensioni desiderate. In questo esempio, la proprietà **[!UICONTROL Attributi di base]** è in corso il ridimensionamento della scheda.

![Il pulsante di ridimensionamento è evidenziato nella scheda Attributi di base.](../images/profile-customization/resize.png)

La scheda selezionata si adatta alle dimensioni desiderate e le schede circostanti vengono riposizionate in modo dinamico. Questo può causare lo spostamento di alcune schede in righe aggiuntive, che richiedono lo scorrimento verso il basso per visualizzare tutte le schede. Ad esempio, quando &quot;[!UICONTROL Attributi di base]&quot; è ridimensionata dalla scheda &quot;[!UICONTROL Identità collegate]La scheda &quot; non è più visibile nella riga superiore e ora viene visualizzata su una nuova seconda riga all’interno del profilo (non visualizzata). Per restituire il &quot;[!UICONTROL Identità collegate]&quot; nella riga superiore, puoi trascinarla e rilasciarla nella posizione corrente della &quot;[!UICONTROL Preferenze canale]&quot;.

![Viene evidenziata una scheda ridimensionata.](../images/profile-customization/resized.png)

## Modificare e rimuovere schede

Oltre a ridimensionare e riordinare le schede, puoi modificare il contenuto di alcune schede e rimuoverle completamente dal dashboard. Seleziona i puntini di sospensione (`...`) nell’angolo in alto a destra della scheda per modificarla o rimuoverla. Si apre un menu a discesa con le opzioni per modificare o rimuovere la scheda, a seconda delle proprietà della scheda selezionata.

>[!NOTE]
>
>Non tutte le schede possono essere modificate o rimosse. Questo perché alcune schede contengono informazioni di sola lettura o obbligatorie. Se nell&#39;angolo superiore destro di una scheda non è presente un&#39;ellisse, la scheda contiene le informazioni richieste AND di sola lettura e non può essere modificata né rimossa. Se una scheda presenta dei puntini di sospensione nell’angolo e se la selezioni, viene visualizzata solo un’opzione per rimuoverla, le informazioni sulla scheda sono di sola lettura e non possono essere modificate.

![Viene evidenziato il menu a discesa della scheda di modifica. Sono incluse le opzioni per modificare o rimuovere la scheda.](../images/profile-customization/edit-card.png)

Seleziona **[!UICONTROL Modifica]** nel menu a discesa per aprire **[!UICONTROL Modifica widget]** area di lavoro, che consente di aggiornare il titolo della scheda, riordinare o rimuovere gli attributi visibili o aggiungere altri attributi utilizzando **[!UICONTROL Aggiungi attributi]** pulsante.

![Viene visualizzata la scheda Attributi di base.](../images/profile-customization/basic-attributes.png)

## Aggiungi attributi {#add-attributes}

Dalla sezione **[!UICONTROL Modifica widget]** schermata, seleziona **[!UICONTROL Aggiungi attributi]** nell’angolo in alto a destra della scheda per iniziare ad aggiungere attributi a essa.

![Il pulsante Aggiungi attributi nella scheda Attributi di base è evidenziato.](../images/profile-customization/add-attributes.png)

Quando **[!UICONTROL Seleziona campo schema di unione]** viene visualizzata, il lato sinistro della finestra di dialogo mostra il [!UICONTROL Profilo individuale XDM] schema di unione, con campi nidificati al di sotto. Per ulteriori informazioni sugli schemi di unione, consulta [sezione schemi unione della sezione [!DNL Profile] guida utente](user-guide.md#union-schema).

Il **[!UICONTROL Attributi selezionati]** sezione sul lato destro della finestra di dialogo mostra gli attributi attualmente inclusi nella scheda che stai modificando. Puoi rimuovere e riordinare gli attributi anche qui. Vengono visualizzati il numero totale di attributi selezionati e il numero massimo di attributi (20) che è possibile aggiungere a una singola scheda.

![Vengono evidenziati gli attributi che attualmente compongono gli attributi della scheda.](../images/profile-customization/select-before.png)

Puoi selezionare uno qualsiasi dei campi schema di unione disponibili per personalizzare gli attributi della scheda che stai modificando. I campi selezionati vengono visualizzati con un segno di spunta accanto e vengono aggiunti automaticamente all&#39;elenco degli attributi selezionati. Dopo aver aggiunto tutti gli attributi che desideri visualizzare sulla scheda, scegli **[!UICONTROL Seleziona]** per tornare al **[!UICONTROL Modifica widget]** schermo.

![Vengono evidenziati i nuovi attributi aggiunti.](../images/profile-customization/select-after.png)

Quando ritorni al **[!UICONTROL Modifica widget]** , l’elenco degli attributi sulla scheda deve ora essere aggiornato per riflettere le scelte effettuate. Puoi comunque rimuovere o riordinare gli attributi della scheda o modificarne il titolo in base alle esigenze. Una volta completate le modifiche, seleziona **[!UICONTROL Salva]** per salvare le modifiche.

![I nuovi attributi aggiunti vengono visualizzati sulla scheda modificata.](../images/profile-customization/new-attributes.png)

Dopo il salvataggio, si ritorna al **[!UICONTROL Dettaglio]** in cui sono visibili la scheda e gli attributi aggiornati.

![I nuovi attributi aggiunti vengono visualizzati sulla scheda nel dashboard Profilo.](../images/profile-customization/added-attributes.png)

## Aggiungi una nuova scheda {#add-a-new-card}

Per personalizzare ulteriormente l’aspetto dei profili in Experience Platform, puoi scegliere di aggiungere nuove schede al dashboard e selezionare gli attributi che desideri visualizzare su tali schede. Per iniziare, seleziona **[!UICONTROL Modifica dashboard]** il **[!UICONTROL Dettaglio]** scheda.

![Viene evidenziato il pulsante Personalizza dettagli profilo.](../images/profile-customization/customize-profile-details.png)

Quindi, seleziona **[!UICONTROL Aggiungi widget]** nell&#39;angolo in alto a sinistra del dashboard.

![Viene evidenziato il pulsante Aggiungi widget.](../images/profile-customization/add-widget.png)

Se si sceglie di aggiungere una nuova scheda, viene aperto il **[!UICONTROL Modifica widget]** in cui è possibile fornire un titolo per la nuova scheda e scegliere gli attributi che si desidera visualizzare. Per iniziare ad aggiungere attributi alla scheda, seleziona **[!UICONTROL Aggiungi attributi]**.

![Nella schermata Modifica widget viene visualizzata una nuova scheda widget vuota.](../images/profile-customization/edit-widget.png)

Quando **[!UICONTROL Seleziona campo schema di unione]** viene visualizzata, il lato sinistro della finestra di dialogo mostra il [!UICONTROL Profilo individuale XDM] schema di unione e **[!UICONTROL Attributi selezionati]** sezione sul lato destro della finestra di dialogo mostra gli attributi selezionati per la scheda. Per ulteriori informazioni sull&#39;aggiunta di attributi, vedere [sezione sull’aggiunta di attributi](#add-attributes) visualizzata in precedenza in questo documento.

Vengono visualizzati il numero totale di attributi selezionati e il numero massimo di attributi (20) che è possibile aggiungere a una singola scheda. Puoi anche rimuovere e riordinare gli attributi selezionati da questa schermata. Dopo aver aggiunto tutti gli attributi da visualizzare sulla scheda, scegli **[!UICONTROL Seleziona]** per tornare al **[!UICONTROL Modifica widget]** schermo.

![I campi che stai aggiungendo alla scheda vengono evidenziati.](../images/profile-customization/add-widget-attributes.png)

Quando ritorni al **[!UICONTROL Modifica widget]** , l’elenco degli attributi sulla scheda deve riflettere le scelte effettuate nella schermata precedente. Puoi anche riordinare e rimuovere gli attributi della scheda in base alle esigenze.

Per salvare la nuova carta devi prima fornire un **[!UICONTROL Titolo carta]**, sarà possibile selezionare **[!UICONTROL Salva]** e completare il processo di creazione della scheda.

![Il nuovo widget viene visualizzato in anteprima nella schermata Modifica widget.](../images/profile-customization/new-widget.png)

Dopo il salvataggio, si ritorna al **[!UICONTROL Dettaglio]** in cui sono visibili la nuova scheda e gli attributi.

![Il nuovo widget viene aggiunto alla dashboard Profilo.](../images/profile-customization/added-widget.png)

## Ripristina schede predefinite

Se in qualsiasi momento decidi di ripristinare le schede predefinite che sono state rimosse in seguito, puoi farlo in modo rapido e semplice. Seleziona innanzitutto **[!UICONTROL Modifica dashboard]**, quindi seleziona **[!UICONTROL Ripristina schede predefinite]**. Una volta che le schede predefinite sono visibili, puoi selezionare **[!UICONTROL Salva]** per salvare le modifiche o selezionare **[!UICONTROL Annulla]** se non si desidera ripristinare le schede predefinite.

![Il pulsante Ripristina schede predefinite è evidenziato nel dashboard Profilo.](../images/profile-customization/restore-default.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di aggiornare la vista profilo per la tua organizzazione, tra cui l’aggiunta e la rimozione di schede, la modifica dei dettagli e degli attributi delle schede e il riordinamento e ridimensionamento delle schede. Per ulteriori informazioni sull&#39;utilizzo di [!DNL Profile] nell’interfaccia utente di Experience Platform, consulta la sezione [[!DNL Profile] guida utente](user-guide.md).
