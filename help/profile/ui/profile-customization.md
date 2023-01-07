---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;interfaccia utente;interfaccia utente;personalizzazione;dettagli profilo;dettagli
title: Personalizzazione dei dettagli del profilo nell’interfaccia utente
description: Questa guida fornisce istruzioni passo per personalizzare il modo in cui i dati del profilo cliente in tempo reale vengono visualizzati nell’interfaccia utente di Adobe Experience Platform.
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] personalizzazione dei dettagli {#profile-detail-customization}

Nell’interfaccia utente di Adobe Experience Platform, puoi visualizzare e interagire con [!DNL Real-Time Customer Profile] sotto forma di profili cliente. Le informazioni di profilo visualizzate nell’interfaccia utente sono state unite da più frammenti di profilo per formare una singola visualizzazione per ogni singolo cliente. Ciò include dettagli quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti visualizzati nei profili possono essere modificati anche a livello organizzativo per visualizzare i campi preferiti [!DNL Profile] attributi. Questa guida fornisce istruzioni passo per personalizzare il modo in cui [!DNL Profile] i dati vengono visualizzati nell’interfaccia utente di Platform.

Per una guida completa all’interfaccia utente dei profili, visita il [Guida all’interfaccia utente del profilo](user-guide.md).

## Riordinare e ridimensionare le schede {#reorder-and-resize-cards}

Da **[!UICONTROL Dettaglio]** scheda del profilo cliente, puoi selezionare **[!UICONTROL Personalizzare i dettagli del profilo]** per ridimensionare e riordinare le schede esistenti.

![Il pulsante Personalizza dettagli profilo è evidenziato nel dashboard Profilo.](../images/profile-customization/customize-profile-details.png)

Dopo aver scelto di modificare il dashboard, è possibile riordinare le schede selezionando il titolo e trascinando e rilasciando le schede nell&#39;ordine desiderato. Potete anche ridimensionare una scheda selezionando il simbolo dell&#39;angolo nell&#39;angolo in basso a destra della scheda (`⌟`) e trascinare la scheda nella dimensione desiderata. In questo esempio, la **[!UICONTROL Attributi di base]** la scheda viene ridimensionata.

![Il pulsante ridimensiona viene evidenziato nella scheda Attributi di base.](../images/profile-customization/resize.png)

La scheda selezionata si adatta alle dimensioni desiderate e le schede circostanti vengono riposizionate dinamicamente. Questo può causare lo spostamento di alcune schede in righe aggiuntive, che richiedono lo scorrimento verso il basso per visualizzare tutte le schede. Ad esempio, quando &quot;[!UICONTROL Attributi di base]&quot; la scheda viene ridimensionata[!UICONTROL Identità collegate]&quot;la scheda non è più visibile nella riga superiore e ora viene visualizzata in una nuova seconda riga all’interno del profilo (non visualizzata). Per restituire &quot;[!UICONTROL Identità collegate]&quot; scheda nella riga superiore, puoi trascinarla e rilasciarla nella posizione corrente del &quot;[!UICONTROL Preferenze del canale]&quot; scheda.

![Viene evidenziata una scheda ridimensionata.](../images/profile-customization/resized.png)

## Modificare e rimuovere le schede

Oltre a ridimensionare e riordinare le schede, è possibile modificare il contenuto di alcune schede e rimuovere alcune schede dal dashboard completamente. Seleziona i puntini di sospensione (`...`) nell’angolo in alto a destra della scheda per modificarla o rimuoverla. Viene visualizzato un menu a discesa con le opzioni per modificare o rimuovere la scheda, a seconda delle proprietà della scheda selezionata.

>[!NOTE]
>
>Non tutte le schede possono essere modificate o rimosse. Questo perché alcune schede contengono informazioni di sola lettura o richieste. Se una scheda non ha un puntino di sospensione nell&#39;angolo in alto a destra, contiene le informazioni necessarie in sola lettura e non può essere modificata né rimossa. Se una scheda ha dei puntini di sospensione nell&#39;angolo e la sua selezione mostra solo un&#39;opzione per rimuovere la scheda, le informazioni sulla scheda sono di sola lettura e non possono essere modificate.

![Il menu a discesa della scheda di modifica è evidenziato. Ciò include opzioni per modificare o rimuovere la scheda.](../images/profile-customization/edit-card.png)

Seleziona **[!UICONTROL Modifica]** nel menu a discesa per aprire **[!UICONTROL Widget di modifica]** Area di lavoro, in cui puoi aggiornare il titolo della scheda, riordinare o rimuovere gli attributi visibili o aggiungere altri attributi utilizzando **[!UICONTROL Aggiungi attributi]** pulsante .

![Viene visualizzata la scheda Attributi di base .](../images/profile-customization/basic-attributes.png)

## Aggiungi attributi {#add-attributes}

Da **[!UICONTROL Widget di modifica]** schermata, seleziona **[!UICONTROL Aggiungi attributi]** nell’angolo in alto a destra della scheda per iniziare ad aggiungere attributi a tale scheda.

![Viene evidenziato il pulsante Aggiungi attributi nella scheda Attributi di base.](../images/profile-customization/add-attributes.png)

Quando il **[!UICONTROL Selezionare il campo schema unione]** si apre la finestra di dialogo, il lato sinistro della finestra di dialogo mostra l’intero [!UICONTROL Profilo individuale XDM] schema di unione, con campi nidificati sotto. Per ulteriori informazioni sugli schemi di unione, consulta [sezione schemi unione [!DNL Profile] guida utente](user-guide.md#union-schema).

La **[!UICONTROL Attributi selezionati]** nella sezione a destra della finestra di dialogo vengono visualizzati gli attributi attualmente inclusi nella scheda che si sta modificando. Puoi rimuovere e riordinare gli attributi anche qui. Viene visualizzato il numero totale di attributi selezionati, nonché il numero massimo di attributi (20) che possono essere aggiunti a una singola scheda.

![Vengono evidenziati gli attributi che attualmente compongono gli attributi sulla scheda.](../images/profile-customization/select-before.png)

Puoi selezionare uno dei campi dello schema unione disponibili per personalizzare gli attributi nella scheda che stai modificando. I campi selezionati sono contrassegnati da un segno di spunta accanto a essi e vengono aggiunti automaticamente all’elenco degli attributi selezionati. Dopo aver aggiunto tutti gli attributi che desiderate visualizzare sulla scheda, scegliete **[!UICONTROL Seleziona]** per tornare al **[!UICONTROL Widget di modifica]** schermo.

![I nuovi attributi aggiunti vengono evidenziati.](../images/profile-customization/select-after.png)

Quando ritorni a **[!UICONTROL Widget di modifica]** , l’elenco degli attributi nella scheda deve ora essere aggiornato per riflettere le scelte effettuate. Potete comunque rimuovere o riordinare gli attributi della scheda o modificarne il titolo in base alle necessità. Al termine delle modifiche, seleziona **[!UICONTROL Salva]** per salvare le modifiche.

![I nuovi attributi aggiunti vengono visualizzati sulla scheda modificata.](../images/profile-customization/new-attributes.png)

Dopo il salvataggio, viene visualizzata nuovamente la **[!UICONTROL Dettaglio]** scheda in cui sono visibili la scheda e gli attributi aggiornati.

![I nuovi attributi aggiunti vengono visualizzati sulla scheda all’interno del dashboard Profilo.](../images/profile-customization/added-attributes.png)

## Aggiungi una nuova scheda {#add-a-new-card}

Per personalizzare ulteriormente l’aspetto dei profili all’interno di Experience Platform, puoi scegliere di aggiungere nuove schede al dashboard e selezionare gli attributi da visualizzare su tali schede. Per iniziare, seleziona **[!UICONTROL Modifica dashboard]** sulla **[!UICONTROL Dettaglio]** scheda .

![Il pulsante Personalizza dettagli profilo è evidenziato.](../images/profile-customization/customize-profile-details.png)

Quindi, seleziona **[!UICONTROL Aggiungi widget]** nell’angolo in alto a sinistra del dashboard.

![Il pulsante Aggiungi widget viene evidenziato.](../images/profile-customization/add-widget.png)

Scegliendo di aggiungere una nuova scheda si apre la **[!UICONTROL Widget di modifica]** schermata in cui potete specificare un titolo per la nuova scheda e scegliere gli attributi che desiderate visualizzare nella scheda. Per iniziare ad aggiungere attributi alla scheda, seleziona **[!UICONTROL Aggiungi attributi]**.

![Nella schermata Modifica widget viene visualizzata una nuova scheda widget vuota.](../images/profile-customization/edit-widget.png)

Quando il **[!UICONTROL Selezionare il campo schema unione]** si apre la finestra di dialogo, il lato sinistro della finestra di dialogo mostra l’intero [!UICONTROL Profilo individuale XDM] schema dell&#39;unione e **[!UICONTROL Attributi selezionati]** la sezione a destra della finestra di dialogo mostra gli attributi selezionati per la scheda. Per ulteriori informazioni sull’aggiunta degli attributi, consulta la sezione [sezione sull’aggiunta di attributi](#add-attributes) che viene visualizzato in precedenza in questo documento.

Viene visualizzato il numero totale di attributi selezionati, nonché il numero massimo di attributi (20) che possono essere aggiunti a una singola scheda. Puoi anche rimuovere e riordinare gli attributi selezionati da questa schermata. Dopo aver aggiunto tutti gli attributi che desiderate visualizzare sulla scheda, scegliete **[!UICONTROL Seleziona]** per tornare al **[!UICONTROL Widget di modifica]** schermo.

![I campi che aggiungi alla scheda vengono evidenziati.](../images/profile-customization/add-widget-attributes.png)

Quando ritorni a **[!UICONTROL Widget di modifica]** L&#39;elenco degli attributi sulla scheda deve riflettere le scelte della schermata precedente. Potete inoltre riordinare e rimuovere gli attributi della scheda in base alle esigenze.

Per salvare la nuova scheda è necessario fornire prima un **[!UICONTROL Titolo della scheda]**, potrai quindi selezionare **[!UICONTROL Salva]** e completare il processo di creazione della scheda.

![Il nuovo widget viene visualizzato in anteprima nella schermata Modifica widget.](../images/profile-customization/new-widget.png)

Dopo il salvataggio, viene visualizzata nuovamente la **[!UICONTROL Dettaglio]** scheda in cui sono visibili la nuova scheda e i nuovi attributi.

![Il nuovo widget viene aggiunto al dashboard Profilo.](../images/profile-customization/added-widget.png)

## Ripristina schede predefinite

Se in qualsiasi momento decidi di voler ripristinare le schede predefinite che sono state rimosse, puoi farlo in modo rapido e semplice. Per prima cosa, seleziona **[!UICONTROL Modifica dashboard]**, quindi seleziona **[!UICONTROL Ripristina schede predefinite]**. Una volta visualizzate le schede predefinite, potete selezionare **[!UICONTROL Salva]** per salvare le modifiche o selezionare **[!UICONTROL Annulla]** se non si desidera ripristinare le schede predefinite.

![Il pulsante Ripristina schede predefinite è evidenziato nel dashboard Profilo .](../images/profile-customization/restore-default.png)

## Passaggi successivi

Seguendo questo documento, ora dovresti essere in grado di aggiornare la visualizzazione del profilo per la tua organizzazione, tra cui l’aggiunta e la rimozione di schede, la modifica di dettagli e attributi della scheda e il riordinamento e il ridimensionamento delle schede. Per ulteriori informazioni sull’utilizzo di [!DNL Profile] nell’interfaccia utente di Experience Platform, fai riferimento alla [[!DNL Profile] guida utente](user-guide.md).
