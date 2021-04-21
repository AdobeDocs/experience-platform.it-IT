---
keywords: Experience Platform;home;argomenti popolari;abilitare set di dati;set di dati;set di dati
solution: Experience Platform
title: Guida all’interfaccia utente dei set di dati
topic-legacy: datasets
description: Scopri come eseguire azioni comuni quando si utilizzano i set di dati nell’interfaccia utente di Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Guida all’interfaccia utente dei set di dati

Questa guida utente fornisce istruzioni sull’esecuzione delle azioni comuni quando si lavora con i set di dati all’interno dell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida utente richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Set di dati](overview.md): Il costrutto di archiviazione e gestione per la persistenza dei dati in  [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Editor](../../xdm/tutorials/create-schema-ui.md) schema: Scopri come creare schemi XDM personalizzati utilizzando l’ [!DNL Schema Editor] interfaccia  [!DNL Platform] utente di .
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Assicurati la conformità a normative, restrizioni e criteri sull&#39;utilizzo dei dati dei clienti.

## Visualizzare i set di dati

Nell’interfaccia utente di [!DNL Experience Platform], fai clic su **[!UICONTROL Datasets]** nel menu di navigazione a sinistra per aprire il dashboard **[!UICONTROL Datasets]**. Il dashboard elenca tutti i set di dati disponibili per l’organizzazione. Vengono visualizzati i dettagli di ciascun set di dati elencato, compreso il nome, lo schema a cui il set di dati aderisce e lo stato dell’esecuzione di acquisizione più recente.

![](../images/datasets/user-guide/browse_datasets.png)

Fai clic sul nome di un set di dati per accedere alla relativa schermata **[!UICONTROL Dataset activity]** e visualizzare i dettagli del set di dati selezionato. La scheda Attività include un grafico che mostra il tasso di utilizzo dei messaggi e un elenco di batch con esito positivo o negativo.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Anteprima di un set di dati

Dalla schermata **[!UICONTROL Dataset activity]**, fai clic su **[!UICONTROL Preview dataset]** nell’angolo in alto a destra dello schermo per visualizzare in anteprima fino a 100 righe di dati. Se il set di dati è vuoto, il collegamento di anteprima verrà disattivato e verrà invece indicato che l’anteprima non è disponibile.

![](../images/datasets/user-guide/click_to_preview.png)

Nella finestra di anteprima, la visualizzazione gerarchica dello schema per il set di dati viene visualizzata a destra.

![](../images/datasets/user-guide/preview_dataset.png)

Per metodi più affidabili per accedere ai dati, [!DNL Experience Platform] fornisce servizi a valle, ad esempio [!DNL Query Service] e [!DNL JupyterLab], per esplorare e analizzare i dati. Per ulteriori informazioni, consulta i seguenti documenti:

* [Panoramica del servizio query](../../query-service/home.md)
* [Guida utente di JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Creare un set di dati {#create}

Per creare un nuovo set di dati, inizia facendo clic su **[!UICONTROL Create dataset]** nel dashboard **[!UICONTROL Datasets]**.

![](../images/datasets/user-guide/click_to_create.png)

Nella schermata successiva, sono disponibili le due opzioni seguenti per la creazione di un nuovo set di dati:

* [Creare un set di dati dallo schema](#schema)
* [Creare un set di dati da file CSV](#csv)

### Creare un set di dati con uno schema esistente {#schema}

Nella schermata **[!UICONTROL Create dataset]** , fai clic su **[!UICONTROL Create dataset from schema]** per creare un nuovo set di dati vuoto.

![](../images/datasets/user-guide/create_dataset_schema.png)

Viene visualizzato il passaggio **[!UICONTROL Select schema]** . Sfoglia l’elenco degli schemi e seleziona lo schema a cui si conformerà il set di dati prima di fare clic su **[!UICONTROL Next]**.

![](../images/datasets/user-guide/select_schema.png)

Viene visualizzato il passaggio **[!UICONTROL Configure dataset]** . Fornisci al set di dati un nome e una descrizione facoltativa, quindi fai clic su **[!UICONTROL Finish]** per creare il set di dati.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Creare un set di dati con un file CSV {#csv}

Quando un set di dati viene creato utilizzando un file CSV, viene creato uno schema ad hoc per fornire al set di dati una struttura corrispondente al file CSV fornito. Nella schermata **[!UICONTROL Create dataset]**, fai clic sulla casella che indica **[!UICONTROL Create dataset from CSV file]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

Viene visualizzato il passaggio **[!UICONTROL Configure]** . Fornisci il set di dati con un nome e una descrizione facoltativa, quindi fai clic su **[!UICONTROL Next]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

Viene visualizzato il passaggio **[!UICONTROL Add data]** . Carica il file CSV trascinandolo e rilasciandolo al centro dello schermo oppure fai clic su **[!UICONTROL Browse]** per esplorare la directory dei file. Le dimensioni del file possono essere fino a dieci gigabyte. Una volta caricato il file CSV, fai clic su **[!UICONTROL Save]** per creare il set di dati.

>[!NOTE]
>
>I nomi delle colonne CSV devono iniziare con caratteri alfanumerici e possono contenere solo lettere, numeri e caratteri di sottolineatura.

![](../images/datasets/user-guide/add_csv_data.png)

## Abilita un set di dati per il profilo cliente in tempo reale {#enable-profile}

Ogni set di dati è in grado di arricchire i profili dei clienti con i relativi dati acquisiti. A tal fine, lo schema a cui aderisce il set di dati deve essere compatibile per l’utilizzo in [!DNL Real-time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

* Lo schema ha almeno un attributo specificato come proprietà Identity.
* Lo schema presenta una proprietà Identity definita come identità principale.

Per ulteriori informazioni sull&#39;abilitazione di uno schema per [!DNL Profile], consulta la [guida utente dell&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md).

Per abilitare un set di dati per Profilo, accedi alla relativa schermata **[!UICONTROL Dataset activity]** e fai clic sull’interruttore **[!UICONTROL Profile]** all’interno della colonna **[!UICONTROL Properties]** . Una volta attivato, i dati acquisiti nel set di dati verranno utilizzati anche per popolare i profili dei clienti.

>[!NOTE]
>
>Se un set di dati contiene già dati e viene quindi abilitato per [!DNL Profile], i dati esistenti non vengono utilizzati automaticamente da [!DNL Profile]. Dopo che un set di dati è abilitato per [!DNL Profile], ti consigliamo di inserire nuovamente tutti i dati esistenti per contribuire ai profili dei clienti.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## Gestire e applicare la governance dei dati su un set di dati

Le etichette di utilizzo dei dati ti consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Per ulteriori informazioni sulle etichette, consulta la [Panoramica sulla governance dei dati](../../data-governance/home.md) oppure fai riferimento alla [guida utente delle etichette per l’utilizzo dei dati](../../data-governance/labels/overview.md) per istruzioni su come applicare le etichette ai set di dati.

## Eliminare un set di dati

È possibile eliminare un set di dati accedendo prima alla relativa schermata **[!UICONTROL Dataset activity]**. Quindi, fai clic su **[!UICONTROL Delete dataset]** per eliminarlo.

>[!NOTE]
>
>I set di dati creati e utilizzati da applicazioni e servizi di Adobe (ad esempio Adobe Analytics, Adobe Audience Manager o [!DNL Offer Decisioning]) non possono essere eliminati.

![](../images/datasets/user-guide/delete_dataset.png)

Viene visualizzata una casella di conferma. Fai clic su **[!UICONTROL Delete]** per confermare l’eliminazione del set di dati.

![](../images/datasets/user-guide/confirm_delete.png)

## Eliminare un set di dati abilitato per il profilo

Se un set di dati è abilitato per [!DNL Profile], l’eliminazione di tale set di dati tramite l’interfaccia utente lo elimina sia dal Data Lake che dall’archivio dei profili all’interno di Platform.

Puoi eliminare un set di dati solo dall’ [!DNL Profile] archivio (lasciando i dati nel Data Lake) utilizzando l’API Profilo cliente in tempo reale. Per ulteriori informazioni, consulta la [guida all&#39;endpoint API dei processi di sistema del profilo](../../profile/api/profile-system-jobs.md).

## Monitorare l’acquisizione di dati

Nell’interfaccia utente di [!DNL Experience Platform], fai clic su **[!UICONTROL Monitoring]** nel menu di navigazione a sinistra. Il dashboard **[!UICONTROL Monitoring]** ti consente di visualizzare gli stati dei dati in entrata da un’acquisizione batch o in streaming. Per visualizzare gli stati dei singoli batch, fai clic su **[!UICONTROL Batch end-to-end]** o **[!UICONTROL Streaming end-to-end]**. Nelle dashboard sono elencate tutte le esecuzioni di batch o streaming ingestion, comprese quelle che hanno esito positivo, non sono riuscite o sono ancora in corso. Ogni elenco fornisce i dettagli del batch, compreso l’ID batch, il nome del set di dati di destinazione e il numero di record acquisiti. Se il set di dati di destinazione è abilitato per [!DNL Profile], viene visualizzato anche il numero di record di identità e profilo acquisiti.

![](../images/datasets/user-guide/batch_listing.png)

Puoi fare clic su un singolo **[!UICONTROL Batch ID]** per accedere al dashboard **[!UICONTROL Batch overview]** e visualizzare i dettagli del batch, compresi i registri di errore in caso di errore durante l&#39;inserimento del batch.

![](../images/datasets/user-guide/batch_overview.png)

Per eliminare il batch, fai clic su **[!UICONTROL Delete batch]** in alto a destra nel dashboard. In questo modo verranno rimossi anche i record dal set di dati a cui è stato originariamente acquisito il batch.

![](../images/datasets/user-guide/delete_batch.png)

## Passaggi successivi

Questa guida utente fornisce istruzioni per l’esecuzione delle azioni comuni quando si utilizzano i set di dati nell’interfaccia utente [!DNL Experience Platform] . Per i passaggi relativi all’esecuzione di flussi di lavoro comuni [!DNL Platform] che coinvolgono set di dati, consulta le seguenti esercitazioni:

* [Creare un set di dati utilizzando le API](create.md)
* [Dati del set di dati di query tramite API di accesso ai dati](../../data-access/home.md)
* [Configurare un set di dati per il profilo cliente in tempo reale e il servizio Identity utilizzando le API](../../profile/tutorials/dataset-configuration.md)
