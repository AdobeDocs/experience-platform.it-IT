---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida utente etichette di utilizzo dati
topic: labels
translation-type: tm+mt
source-git-commit: 0534fe8dcc11741ddc74749d231e732163adf5b0
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 0%

---


# Guida utente etichette di utilizzo dati

Questa guida utente descrive i passaggi necessari per utilizzare le etichette di utilizzo dei dati (dette anche etichette DULE) all&#39;interno dell&#39;interfaccia [!DNL Experience Platform] utente. Prima di utilizzare la guida, consulta la panoramica [sulla governance dei](../home.md) dati per un&#39;introduzione più efficace al framework DULE.

## Gestione delle etichette di utilizzo dei dati a livello di dataset

Per gestire le etichette di utilizzo dei dati a livello di dataset, è necessario selezionare un dataset esistente o crearne uno nuovo. Dopo aver effettuato l&#39;accesso  Adobe Experience Platform, selezionate **[!UICONTROL Datasets]** nella navigazione a sinistra per aprire l&#39;area di lavoro _Set_ dati. In questa pagina sono elencati tutti i set di dati creati appartenenti alla propria organizzazione, insieme a utili dettagli relativi a ciascun set di dati.

![Scheda Set di dati in Area di lavoro dati](../images/labels/datasets.png)

La sezione successiva contiene i passaggi necessari per creare un nuovo dataset a cui applicare le etichette. Se si desidera modificare le etichette per un set di dati esistente, selezionare il set di dati dall&#39;elenco e passare all&#39; [aggiunta di etichette di utilizzo dei dati al set di dati](#add-labels).

### Creare un nuovo dataset

>[!NOTE]
>
>In questo esempio, un dataset viene creato utilizzando uno schema [!DNL Experience Data Model] (XDM) preconfigurato. Per ulteriori informazioni sugli schemi XDM, vedere la panoramica [del sistema](../../xdm/home.md) XDM e le [nozioni di base della composizione](../../xdm/schema/composition.md)dello schema.

Per creare un nuovo set di dati, fate clic **[!UICONTROL Create Dataset]** nell’angolo superiore destro dell’ _[!UICONTROL Datasets]_area di lavoro.

![](../images/labels/create_dataset.png)

Viene _[!UICONTROL Create Dataset]_visualizzata la schermata. Da qui, clicca **[!UICONTROL Create Dataset from Schema]**.

![Crea set di dati da schema](../images/labels/dataset_create.png)

Viene visualizzata _[!UICONTROL Select Schema]_la schermata, in cui sono elencati tutti gli schemi disponibili utilizzabili per creare un set di dati. Fare clic sul pulsante di scelta accanto a uno schema per selezionarlo. Nella_[!UICONTROL Schemas]_ sezione a destra sono visualizzati ulteriori dettagli sullo schema selezionato. Dopo aver selezionato uno schema, fare clic su **[!UICONTROL Next]**.

![Seleziona schema dati](../images/labels/dataset_schema.png)

Viene visualizzata la schermata _Configura set di dati_ . Immettete un **nome** (obbligatorio) e una **descrizione** (facoltativo, ma consigliato) per il nuovo set di dati, quindi fate clic **[!UICONTROL Finish]**.

![Configura set di dati con nome e descrizione](../images/labels/dataset_configure.png)

Viene visualizzata la _[!UICONTROL Dataset Activity]_pagina con informazioni sul set di dati appena creato. In questo esempio, il set di dati è denominato &quot;Membri fedeltà&quot;, pertanto nella parte superiore della navigazione sono visualizzati_ Set di dati > Membri _fedeltà.

![DataSet Activity, pagina](../images/labels/dataset_activity.png)

### Aggiungere etichette di utilizzo dei dati al dataset {#add-labels}

Dopo aver creato un nuovo dataset o aver selezionato un dataset esistente dall&#39;elenco nell&#39; _[!UICONTROL Datasets]_area di lavoro, fare clic **[!UICONTROL Data Governance]**per aprire l&#39;_[!UICONTROL Data Governance]_ area di lavoro. L&#39;area di lavoro consente di gestire le etichette di utilizzo dei dati a livello di dataset e di campo.

![Scheda Governance dei dati del set di dati](../images/labels/dataset_data_governance.png)

Per modificare le etichette di utilizzo dei dati a livello di dataset, fare clic sull&#39;icona matita accanto al nome del dataset.

![Modificare le etichette a livello di set di dati](../images/labels/dataset_labels_edit_button.png)

Viene visualizzata _[!UICONTROL Edit Governance Labels]_la finestra di dialogo. Nella finestra di dialogo, selezionare le caselle accanto alle etichette che si desidera applicare al set di dati. Ricordate che queste etichette saranno ereditate da tutti i campi all&#39;interno del dataset. L’_[!UICONTROL Applied Labels]_ intestazione viene aggiornata mentre selezionate ogni casella, mostrando le etichette selezionate. Dopo aver selezionato le etichette desiderate, fate clic su **[!UICONTROL Save Changes]**.

<img alt="Applica etichette di governance a livello di set di dati" src="../images/labels/apply-labels-dataset.png" width="700"><br>

L&#39; _[!UICONTROL Data Governance]_area di lavoro viene visualizzata di nuovo, con le etichette applicate a livello di set di dati. È inoltre possibile vedere che le etichette vengono ereditate fino a ciascuno dei campi all&#39;interno del set di dati.

![Etichette di set di dati ereditate dai campi](../images/labels/dataset_inherited_labels.png)

Si noti che accanto alle etichette a livello di set di dati viene visualizzata una &quot;x&quot; che consente di rimuovere le etichette. Le etichette ereditate accanto a ciascun campo non dispongono di una &quot;x&quot; accanto a esse e vengono visualizzate in grigio senza la possibilità di rimuovere o modificare. Questo perché i campi **ereditati sono di sola** lettura e non possono quindi essere rimossi a livello di campo.

Per impostazione predefinita, l’ **[!UICONTROL Show Inherited Labels]** interruttore è attivato e consente di visualizzare tutte le etichette ereditate dal set di dati ai relativi campi. Se si cambia l&#39;opzione Disattiva, vengono nascoste tutte le etichette ereditate all&#39;interno del dataset.

![Nascondi etichette ereditate](../images/labels/hide_inherited_labels.png)

## Gestione delle etichette di utilizzo dei dati a livello di campo dataset

Continuando il flusso di lavoro per l&#39; [aggiunta e la modifica delle etichette di utilizzo dei dati a livello](#add-labels)_[!UICONTROL Data Governance]_di dataset, potete anche gestire le etichette a livello di campo all&#39;interno dell&#39;area di lavoro per tale set di dati.

Per applicare le etichette di utilizzo dei dati a un singolo campo, selezionare la casella di controllo accanto al nome del campo, quindi fare clic **[!UICONTROL Edit Governance Labels]**.

![Modifica etichette campo](../images/labels/fields_single_field.png)

Viene visualizzata _[!UICONTROL Edit Governance Labels]_la finestra di dialogo. Nella finestra di dialogo sono visualizzate intestazioni contenenti campi selezionati, etichette applicate ed etichette ereditate. Le etichette ereditate (C2 e C5) sono disabilitate nella finestra di dialogo. Sono etichette di sola lettura ereditate dal livello del set di dati e sono pertanto modificabili solo a livello del set di dati.

<img alt="Modifica delle etichette governance per un singolo campo" src="../images/labels/field-label-inheritance.png" width="700"><br>

Selezionare le etichette a livello di campo facendo clic sulla casella di controllo accanto a ciascuna etichetta da utilizzare. Quando si selezionano le etichette, l&#39; _[!UICONTROL Applied Labels]_intestazione viene aggiornata per mostrare le etichette applicate ai campi visualizzati nell&#39;_[!UICONTROL Selected Fields]_ intestazione. Dopo aver selezionato le etichette a livello di campo, fare clic su **[!UICONTROL Save Changes]**.

<img alt="Applicare etichette a livello di campo" src="../images/labels/apply-labels-field.png" width="700"><br>

L&#39; _[!UICONTROL Data Governance]_area di lavoro viene visualizzata nuovamente, con le etichette a livello di campo selezionate nella riga accanto al nome del campo. L&#39;etichetta a livello di campo è dotata di una &quot;x&quot; che consente di rimuovere l&#39;etichetta.

![Campo che mostra le etichette a livello di campo](../images/labels/fields_show_field_level_labels.png)

È possibile ripetere questi passaggi per continuare ad aggiungere e modificare etichette a livello di campo per altri campi, compresa la selezione di più campi per applicare etichette a livello di campo contemporaneamente.

![Selezionare più campi per applicare etichette a livello di campo contemporaneamente.](../images/labels/fields_select_multiple.png)

È importante ricordare che l&#39;ereditarietà si sposta solo dal livello superiore verso il basso (dataset → campi), il che significa che le etichette applicate a livello di campo non vengono propagate ad altri campi o set di dati.

## Gestione delle etichette personalizzate

Potete creare etichette di utilizzo personalizzate all’interno dell’ *[!UICONTROL Policies]* area di lavoro nell’ [!DNL Experience Platform] interfaccia utente. Fare clic **[!UICONTROL Policies]** nel menu di navigazione a sinistra, quindi fare clic **[!UICONTROL Labels]** per visualizzare un elenco delle etichette esistenti. Da qui, clicca **[!UICONTROL Create label]**.

![](../images/labels/create-label-btn.png)

Viene visualizzata *[!UICONTROL Create label]* la finestra di dialogo. Da qui, fornire le seguenti informazioni per la nuova etichetta:

* **[!UICONTROL Identifier]**: Un identificatore univoco per l&#39;etichetta. Questo valore viene utilizzato a scopo di ricerca e deve pertanto essere breve e conciso.
* **[!UICONTROL Name]**: Un nome visualizzato intuitivo per l&#39;etichetta.
* **[!UICONTROL Description]**: (Facoltativo) Descrizione dell&#39;etichetta per fornire ulteriore contesto.

Al termine, fate clic **[!UICONTROL Create]**.

![](../images/labels/create-label.png)

La finestra di dialogo si chiude e l&#39;etichetta personalizzata appena creata viene visualizzata nell&#39;elenco sotto la *[!UICONTROL Labels]* scheda.

![](../images/labels/label-created.png)

È ora possibile selezionare l&#39;etichetta in *[!UICONTROL Custom Labels]* quando si modificano le etichette di utilizzo per set di dati e campi o quando si creano criteri di utilizzo dei dati.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Passaggi successivi

Ora che sono state aggiunte etichette di utilizzo dei dati a livello di set di dati e di campo, è possibile iniziare a assimilare i dati in [!DNL Experience Platform]. Per saperne di più, leggi la documentazione [sull’inserimento dei](../../ingestion/home.md)dati.

È inoltre possibile definire criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere la panoramica [dei criteri di utilizzo dei](../policies/overview.md)dati.

## Risorse aggiuntive

Il seguente video è pensato per illustrare [!DNL Data Governance]e illustrare come applicare etichette a un set di dati e a singoli campi.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
