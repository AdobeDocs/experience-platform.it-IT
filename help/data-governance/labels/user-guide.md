---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guida utente etichette di utilizzo dati
topic: labels
translation-type: tm+mt
source-git-commit: 4a60956ade2d742ac83e138a2921a6a4893e06ef

---


# Guida utente etichette di utilizzo dati

Questa guida utente descrive i passaggi per l’utilizzo delle etichette di utilizzo dei dati (dette anche etichette DULE) nell’interfaccia utente della piattaforma Experience. Prima di utilizzare la guida, consulta la panoramica [sulla governance dei](../home.md) dati per un&#39;introduzione più efficace al framework DULE.

## Gestione delle etichette di utilizzo dei dati a livello di dataset

Per gestire le etichette di utilizzo dei dati a livello di dataset, è necessario selezionare un dataset esistente o crearne uno nuovo. Dopo aver effettuato l&#39;accesso ad Adobe Experience Platform, seleziona **Set** di dati nella barra di navigazione a sinistra per aprire l&#39;area di lavoro _Set_ di dati. In questa pagina sono elencati tutti i set di dati creati appartenenti alla propria organizzazione, insieme a utili dettagli relativi a ciascun set di dati.

![Scheda Set di dati in Area di lavoro dati](../images/labels/datasets.png)

La sezione successiva contiene i passaggi necessari per creare un nuovo dataset a cui applicare le etichette. Se si desidera modificare le etichette per un set di dati esistente, selezionare il set di dati dall&#39;elenco e passare all&#39; [aggiunta di etichette di utilizzo dei dati al set di dati](#add-labels).

### Creare un nuovo dataset

>[!NOTE] In questo esempio, viene creato un dataset utilizzando uno schema XDM (Experience Data Model) preconfigurato. Per ulteriori informazioni sugli schemi XDM, vedere la panoramica [del sistema](../../xdm/home.md) XDM e le [nozioni di base della composizione](../../xdm/schema/composition.md)dello schema.

Per creare un nuovo set di dati, fai clic su **Crea set** di dati nell&#39;angolo superiore destro dell&#39;area di lavoro _Set_ dati.

![](../images/labels/create_dataset.png)

Viene visualizzata la schermata _Crea set di dati_ . Da qui, fare clic su **Crea set di dati dallo schema**.

![Crea set di dati da schema](../images/labels/dataset_create.png)

Viene visualizzata la schermata _Seleziona schema_ , in cui sono elencati tutti gli schemi disponibili utilizzabili per creare un set di dati. Fare clic sul pulsante di scelta accanto a uno schema per selezionarlo. Nella sezione _Schemi_ a destra sono visualizzati ulteriori dettagli sullo schema selezionato. Dopo aver selezionato uno schema, fare clic su **Avanti**.

![Seleziona schema dati](../images/labels/dataset_schema.png)

Viene visualizzata la schermata _Configura set di dati_ . Immettete un **nome** (obbligatorio) e una **descrizione** (facoltativo, ma consigliato) per il nuovo set di dati, quindi fate clic su **Fine**.

![Configura set di dati con nome e descrizione](../images/labels/dataset_configure.png)

Viene visualizzata la pagina Attività __ DataSet, in cui sono visualizzate informazioni sul set di dati appena creato. In questo esempio, il set di dati è denominato &quot;Membri fedeltà&quot;, pertanto nella parte superiore della navigazione sono visualizzati _Set di dati > Membri_ fedeltà.

![DataSet Activity, pagina](../images/labels/dataset_activity.png)

### Aggiungere etichette di utilizzo dei dati al dataset {#add-labels}

Dopo aver creato un nuovo dataset o aver selezionato un dataset esistente dall&#39;elenco nell&#39;area di lavoro _Set_ dati, fare clic su **Governance** dati per aprire l&#39;area di lavoro _Governance_ dati. L&#39;area di lavoro consente di gestire le etichette di utilizzo dei dati a livello di dataset e di campo.

![Scheda Governance dei dati del set di dati](../images/labels/dataset_data_governance.png)

Per modificare le etichette di utilizzo dei dati a livello di dataset, fare clic sull&#39;icona matita accanto al nome del dataset.

![Modificare le etichette a livello di set di dati](../images/labels/dataset_labels_edit_button.png)

Viene visualizzata la finestra di dialogo _Modifica etichette_ di governance. Nella finestra di dialogo, selezionare le caselle accanto alle etichette che si desidera applicare al set di dati. Ricordate che queste etichette saranno ereditate da tutti i campi all&#39;interno del dataset. L&#39;intestazione Etichette __ applicate si aggiorna quando si seleziona ogni casella, mostrando le etichette scelte. Dopo aver selezionato le etichette desiderate, fate clic su **Salva modifiche**.

<img alt="Applica etichette di governance a livello di set di dati" src="../images/labels/dataset_apply_labels.png" width="450"><br>

L&#39;area di lavoro _Governance_ dei dati viene visualizzata di nuovo, con le etichette applicate a livello di set di dati. È inoltre possibile vedere che le etichette vengono ereditate fino a ciascuno dei campi all&#39;interno del set di dati.

![Etichette di set di dati ereditate dai campi](../images/labels/dataset_inherited_labels.png)

Si noti che accanto alle etichette a livello di set di dati viene visualizzata una &quot;x&quot; che consente di rimuovere le etichette. Le etichette ereditate accanto a ciascun campo non dispongono di una &quot;x&quot; accanto a esse e vengono visualizzate in grigio senza la possibilità di rimuovere o modificare. Questo perché i campi **ereditati sono di sola** lettura e non possono quindi essere rimossi a livello di campo.

Per impostazione predefinita, l’opzione **Mostra etichette** ereditate è attivata e consente di visualizzare tutte le etichette ereditate dal set di dati ai relativi campi. Se si cambia l&#39;opzione Disattiva, vengono nascoste tutte le etichette ereditate all&#39;interno del dataset.

![Nascondi etichette ereditate](../images/labels/hide_inherited_labels.png)

## Gestione delle etichette di utilizzo dei dati a livello di campo dataset

Continuando il flusso di lavoro per l&#39; [aggiunta e la modifica delle etichette di utilizzo dei dati a livello](#add-labels)di dataset, puoi anche gestire le etichette a livello di campo all&#39;interno dell&#39;area di lavoro _Governance_ dei dati per quel set di dati.

Per applicare le etichette di utilizzo dei dati a un singolo campo, selezionare la casella di controllo accanto al nome del campo, quindi fare clic su **Modifica etichette** di governance.

![Modifica etichette campo](../images/labels/fields_single_field.png)

Viene visualizzata la finestra di dialogo _Modifica etichette_ di governance. Nella finestra di dialogo sono visualizzate intestazioni contenenti campi selezionati, etichette applicate ed etichette ereditate. Le etichette ereditate (C2 e C5) sono disabilitate nella finestra di dialogo. Sono etichette di sola lettura ereditate dal livello del set di dati e sono pertanto modificabili solo a livello del set di dati.

<img alt="Modifica delle etichette governance per un singolo campo" src="../images/labels/fields_inherited_labels.png" width="450"><br>

Selezionare le etichette a livello di campo facendo clic sulla casella di controllo accanto a ciascuna etichetta da utilizzare. Quando si selezionano le etichette, l&#39;intestazione Etichette __ applicate si aggiorna e mostra le etichette applicate ai campi visualizzati nell&#39;intestazione Campi __ selezionati. Dopo aver selezionato le etichette a livello di campo, fare clic su **Salva modifiche**.

<img alt="Applicare etichette a livello di campo" src="../images/labels/fields_field_level_label.png" width="450"><br>

L&#39;area di lavoro _Governance_ dei dati viene visualizzata nuovamente, con le etichette a livello di campo selezionate nella riga accanto al nome del campo. L&#39;etichetta a livello di campo è dotata di una &quot;x&quot; che consente di rimuovere l&#39;etichetta.

![Campo che mostra le etichette a livello di campo](../images/labels/fields_show_field_level_labels.png)

È possibile ripetere questi passaggi per continuare ad aggiungere e modificare etichette a livello di campo per altri campi, compresa la selezione di più campi per applicare etichette a livello di campo contemporaneamente.

![Selezionare più campi per applicare etichette a livello di campo contemporaneamente.](../images/labels/fields_select_multiple.png)

È importante ricordare che l&#39;ereditarietà si sposta solo dal livello superiore verso il basso (dataset → campi), il che significa che le etichette applicate a livello di campo non vengono propagate ad altri campi o set di dati.

## Passaggi successivi

Dopo aver aggiunto etichette di utilizzo dei dati a livello di set di dati e di campo, puoi iniziare a assimilare i dati in Experience Platform. Per saperne di più, leggi la documentazione [sull’inserimento dei](../../ingestion/home.md)dati.

## Risorse aggiuntive

Il seguente video è stato realizzato per illustrare la governance dei dati e illustrare come applicare le etichette a un set di dati e a singoli campi.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)
