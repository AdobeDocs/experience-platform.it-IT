---
keywords: ' Experience Platform;home;argomenti più comuni;governance dei dati;etichetta di utilizzo dei dati;servizio criteri;etichetta di utilizzo dei dati Guida utente'
solution: Experience Platform
title: Guida utente etichette di utilizzo dati
topic: labels
description: Questa guida utente descrive i passaggi necessari per utilizzare le etichette di utilizzo dei dati nell'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 0%

---


# Guida utente etichette di utilizzo dati

Questa guida utente descrive i passaggi necessari per utilizzare le etichette di utilizzo dei dati nell&#39;interfaccia utente [!DNL Experience Platform]. Prima di utilizzare la guida, vedere la [[!DNL Data Governance] panoramica](../home.md) per un&#39;introduzione più affidabile al framework [!DNL Data Governance].

## Gestione delle etichette di utilizzo dei dati a livello di dataset

Per gestire le etichette di utilizzo dei dati a livello di dataset, è necessario selezionare un dataset esistente o crearne uno nuovo. Dopo aver effettuato l&#39;accesso ad Adobe Experience Platform, selezionare **[!UICONTROL Datasets]** nella barra di navigazione a sinistra per aprire l&#39;area di lavoro **[!UICONTROL Datasets]**. In questa pagina sono elencati tutti i set di dati creati appartenenti alla propria organizzazione, insieme a utili dettagli relativi a ciascun set di dati.

![Scheda Set di dati in Area di lavoro dati](../images/labels/datasets.png)

La sezione successiva contiene i passaggi necessari per creare un nuovo dataset a cui applicare le etichette. Se si desidera modificare le etichette per un dataset esistente, selezionare il dataset dall&#39;elenco e passare a [aggiungere etichette di utilizzo dei dati al dataset](#add-labels).

### Creare un nuovo dataset

>[!NOTE]
>
>In questo esempio, un dataset viene creato utilizzando uno schema [!DNL Experience Data Model] (XDM) preconfigurato. Per ulteriori informazioni sugli schemi XDM, vedere [Panoramica del sistema XDM](../../xdm/home.md) e [nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md).

Per creare un nuovo dataset, selezionare **[!UICONTROL Create Dataset]** nell&#39;angolo superiore destro dell&#39;area di lavoro **[!UICONTROL Datasets]**.

![](../images/labels/create_dataset.png)

Viene visualizzata la schermata **[!UICONTROL Create Dataset]**. Da qui, selezionare **[!UICONTROL Create Dataset from Schema]**.

![Crea set di dati da schema](../images/labels/dataset_create.png)

Viene visualizzata la schermata **[!UICONTROL Select Schema]**, in cui sono elencati tutti gli schemi disponibili che è possibile utilizzare per creare un set di dati. Selezionare il pulsante di scelta accanto a uno schema per selezionarlo. Nella sezione **[!UICONTROL Schemas]** a destra sono visualizzati ulteriori dettagli sullo schema selezionato. Dopo aver selezionato uno schema, selezionare **[!UICONTROL Next]**.

![Seleziona schema dati](../images/labels/dataset_schema.png)

Viene visualizzata la schermata **[!UICONTROL Configure Dataset]**. Immettete un nome (obbligatorio) e una descrizione (facoltativo, ma consigliato) per il nuovo set di dati, quindi selezionate **[!UICONTROL Finish]**.

![Configura set di dati con nome e descrizione](../images/labels/dataset_configure.png)

Viene visualizzata la pagina **[!UICONTROL Dataset Activity]** in cui sono visualizzate informazioni sul set di dati appena creato. In questo esempio, il set di dati è denominato &quot;Fedeltà Membri&quot;, pertanto la navigazione superiore mostra **Set di dati > Fedeltà Membri**.

![DataSet Activity, pagina](../images/labels/dataset_activity.png)

### Aggiungere etichette di utilizzo dei dati al set di dati {#add-labels}

Dopo aver creato un nuovo dataset o aver selezionato un dataset esistente dall&#39;elenco nell&#39;area di lavoro **[!UICONTROL Datasets]**, selezionare **[!UICONTROL Data Governance]** per aprire l&#39;area di lavoro **[!UICONTROL Data Governance]**. L&#39;area di lavoro consente di gestire le etichette di utilizzo dei dati a livello di dataset e di campo.

![Scheda Governance dei dati del set di dati](../images/labels/dataset_data_governance.png)

Per modificare le etichette di utilizzo dei dati a livello di dataset, selezionare l&#39;icona matita accanto al nome del dataset.

![Modificare le etichette a livello di set di dati](../images/labels/dataset_labels_edit_button.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Edit Governance Labels]**. Nella finestra di dialogo, selezionare le caselle accanto alle etichette che si desidera applicare al set di dati. Ricordate che queste etichette saranno ereditate da tutti i campi all&#39;interno del dataset. L&#39;intestazione **[!UICONTROL Applied Labels]** viene aggiornata durante la verifica di ogni casella, mostrando le etichette scelte. Dopo aver selezionato le etichette desiderate, selezionare **[!UICONTROL Save Changes]**.

<img alt="Applica etichette di governance a livello di set di dati" src="../images/labels/apply-labels-dataset.png" width="700"><br>

L&#39;area di lavoro **[!UICONTROL Data Governance]** viene visualizzata di nuovo, mostrando le etichette applicate a livello di set di dati. È inoltre possibile vedere che le etichette vengono ereditate fino a ciascuno dei campi all&#39;interno del set di dati.

![Etichette di set di dati ereditate dai campi](../images/labels/dataset_inherited_labels.png)

Si noti che accanto alle etichette a livello di set di dati viene visualizzata una &quot;x&quot; che consente di rimuovere le etichette. Le etichette ereditate accanto a ciascun campo non dispongono di una &quot;x&quot; accanto a esse e vengono visualizzate in grigio senza la possibilità di rimuovere o modificare. Questo perché i campi ereditati **sono di sola lettura**, il che significa che non possono essere rimossi a livello di campo.

L&#39;opzione **[!UICONTROL Show Inherited Labels]** è attivata per impostazione predefinita, per visualizzare tutte le etichette ereditate dal set di dati ai relativi campi. Se si cambia l&#39;opzione Disattiva, vengono nascoste tutte le etichette ereditate all&#39;interno del dataset.

![Nascondi etichette ereditate](../images/labels/hide_inherited_labels.png)

## Gestione delle etichette di utilizzo dei dati a livello di campo dataset

Continuando il flusso di lavoro per l&#39; [aggiunta e modifica delle etichette di utilizzo dei dati a livello di dataset](#add-labels), è anche possibile gestire le etichette a livello di campo all&#39;interno dell&#39;area di lavoro **[!UICONTROL Data Governance]** per tale dataset.

Per applicare le etichette di utilizzo dei dati a un singolo campo, selezionare la casella di controllo accanto al nome del campo, quindi selezionare **[!UICONTROL Edit Governance Labels]**.

![Modifica etichette campo](../images/labels/fields_single_field.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Edit Governance Labels]**. Nella finestra di dialogo sono visualizzate intestazioni contenenti campi selezionati, etichette applicate ed etichette ereditate. Le etichette ereditate (C2 e C5) sono disabilitate nella finestra di dialogo. Sono etichette di sola lettura ereditate dal livello del set di dati e sono pertanto modificabili solo a livello del set di dati.

<img alt="Modifica delle etichette governance per un singolo campo" src="../images/labels/field-label-inheritance.png" width="700"><br>

Selezionare le etichette a livello di campo selezionando la casella di controllo accanto a ciascuna etichetta da utilizzare. Quando si selezionano le etichette, l&#39;intestazione **[!UICONTROL Applied Labels]** viene aggiornata per mostrare le etichette applicate ai campi mostrati nell&#39;intestazione **[!UICONTROL Selected Fields]**. Dopo aver selezionato le etichette a livello di campo, selezionare **[!UICONTROL Save Changes]**.

<img alt="Applicare etichette a livello di campo" src="../images/labels/apply-labels-field.png" width="700"><br>

L&#39;area di lavoro **[!UICONTROL Data Governance]** viene visualizzata di nuovo, in cui vengono visualizzate le etichette a livello di campo selezionate nella riga accanto al nome del campo. L&#39;etichetta a livello di campo è dotata di una &quot;x&quot; che consente di rimuovere l&#39;etichetta.

![Campo che mostra le etichette a livello di campo](../images/labels/fields_show_field_level_labels.png)

È possibile ripetere questi passaggi per continuare ad aggiungere e modificare etichette a livello di campo per altri campi, compresa la selezione di più campi per applicare etichette a livello di campo contemporaneamente.

![Selezionare più campi per applicare etichette a livello di campo contemporaneamente.](../images/labels/fields_select_multiple.png)

È importante ricordare che l&#39;ereditarietà si sposta solo dal livello superiore verso il basso (dataset → campi), il che significa che le etichette applicate a livello di campo non vengono propagate ad altri campi o set di dati.

## Gestione delle etichette personalizzate

È possibile creare etichette di utilizzo personalizzate all&#39;interno dell&#39;area di lavoro **[!UICONTROL Policies]** nell&#39;interfaccia di [!DNL Experience Platform]. Selezionare **[!UICONTROL Policies]** nella navigazione a sinistra, quindi selezionare **[!UICONTROL Labels]** per visualizzare un elenco delle etichette esistenti. Da qui, selezionare **[!UICONTROL Create label]**.

![](../images/labels/create-label-btn.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create label]**. Da qui, fornire le seguenti informazioni per la nuova etichetta:

* **[!UICONTROL Identifier]**: Un identificatore univoco per l&#39;etichetta. Questo valore viene utilizzato a scopo di ricerca e deve pertanto essere breve e conciso.
* **[!UICONTROL Name]**: Un nome visualizzato intuitivo per l&#39;etichetta.
* **[!UICONTROL Description]**: (Facoltativo) Descrizione dell&#39;etichetta per fornire ulteriore contesto.

Al termine, selezionare **[!UICONTROL Create]**.

![](../images/labels/create-label.png)

La finestra di dialogo si chiude e l&#39;etichetta personalizzata appena creata viene visualizzata nell&#39;elenco sotto la scheda **[!UICONTROL Labels]**.

![](../images/labels/label-created.png)

È ora possibile selezionare l&#39;etichetta in **[!UICONTROL Custom Labels]** quando si modificano le etichette di utilizzo per set di dati e campi oppure quando si creano criteri di utilizzo dei dati.

<img src="../images/labels/add-custom-label.png" width="600" /><br>

## Passaggi successivi

Dopo aver aggiunto le etichette di utilizzo dei dati a livello di set di dati e di campo, è possibile iniziare a assimilare i dati in [!DNL Experience Platform]. Per saperne di più, leggere la [documentazione di inserimento dei dati](../../ingestion/home.md).

È inoltre possibile definire criteri di utilizzo dei dati in base alle etichette applicate. Per ulteriori informazioni, vedere la [panoramica dei criteri di utilizzo dei dati](../policies/overview.md).

## Risorse aggiuntive

Il seguente video è pensato per consentire agli utenti di comprendere meglio [!DNL Data Governance] e illustra come applicare etichette a un set di dati e a singoli campi.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
