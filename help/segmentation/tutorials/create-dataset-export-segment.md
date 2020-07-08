---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un dataset per l'esportazione di un segmento di pubblico
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---


# Creare un dataset per l&#39;esportazione di un segmento di pubblico

 Adobe Experience Platform consente di segmentare facilmente i profili dei clienti in audience in base a attributi specifici. Una volta creati i segmenti, puoi esportare il pubblico in un dataset dal quale è possibile accedervi e agire. Affinché l&#39;esportazione abbia esito positivo, il dataset deve essere configurato correttamente.

Questa esercitazione descrive i passaggi necessari per creare un dataset che può essere utilizzato per esportare un segmento di pubblico utilizzando l&#39;interfaccia  di Experience Platform.

Questa esercitazione è direttamente correlata ai passaggi descritti nell&#39;esercitazione per la [valutazione e l&#39;accesso ai risultati](./evaluate-a-segment.md)del segmento. L&#39;esercitazione di valutazione di un segmento fornisce i passaggi per la creazione di un set di dati mediante l&#39;API Catalog, mentre questa esercitazione descrive i passaggi per creare un set di dati utilizzando l&#39;interfaccia  di Experience Platform.

## Introduzione

Per esportare un segmento, il set di dati deve essere basato sullo schema unionale profilo singolo XDM. Uno schema unione è uno schema di sola lettura generato dal sistema che aggrega i campi di tutti gli schemi che condividono la stessa classe, in questo caso si tratta della classe Profilo singolo XDM. Per ulteriori informazioni sugli schemi di visualizzazione dell&#39;unione, vedere la sezione Profilo cliente in tempo [reale della guida](../../xdm/schema/composition.md#union)per gli sviluppatori del Registro di sistema dello schema.

Per visualizzare gli schemi di unione nell&#39;interfaccia utente, fai clic su **Profili** nella navigazione a sinistra, quindi fai clic sulla scheda Schema ** unione come mostrato di seguito.

![Scheda Schema unione nell&#39;interfaccia  Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Area di lavoro DataSet

L&#39;area di lavoro dei set di dati nell&#39;interfaccia  di Experience Platform consente di visualizzare e gestire tutti i set di dati creati dall&#39;organizzazione IMS e di crearne di nuovi.

Per visualizzare l&#39;area di lavoro dei set di dati, fai clic su **Set** di dati nella barra di navigazione a sinistra, quindi fai clic sulla scheda *Sfoglia* . L&#39;area di lavoro dei set di dati contiene un elenco di set di dati, tra cui colonne con *Nome*, *Creato* (data e ora), *Origine*, *Schema* e Stato **** ultimo batch, nonché la data e l&#39;ora dell&#39;ultimo aggiornamento del set di dati. A seconda della larghezza di ciascuna colonna, potrebbe essere necessario scorrere verso sinistra o verso destra per visualizzare tutte le colonne.

>[!NOTE]
>
>Fate clic sull&#39;icona del filtro accanto alla barra di ricerca per utilizzare le funzionalità di filtro per visualizzare solo i set di dati abilitati per il profilo cliente in tempo reale.

![Visualizza tutti i set di dati](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Creare un dataset

Per creare un set di dati, fare clic su **Crea set** di dati nell&#39;angolo superiore destro dell&#39;area di lavoro Set di dati.

![Fate clic su Crea set di dati](../images/tutorials/segment-export-dataset/dataset-click-create.png)

Nella schermata *Crea set di dati* , fare clic su **Crea set di dati dallo schema** per continuare.

![Seleziona origine dati](../images/tutorials/segment-export-dataset/create-dataset.png)

## Seleziona schema unione profilo singolo XDM

Per selezionare lo schema dell&#39;unione del profilo singolo XDM da utilizzare nel dataset, individuare lo schema &quot;Profilo singolo XDM&quot; con un tipo di &quot;Unione&quot; nella schermata *Seleziona schema* .

Selezionato il pulsante di scelta accanto a Profilo **singolo** XDM, quindi fate clic su **Avanti** nell&#39;angolo superiore destro.

![Seleziona schema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configura set di dati

Nella schermata **Configura set** di dati, verrà richiesto di assegnare al set di dati un *nome* e anche una *descrizione* del set di dati.

**Note sui nomi dei set di dati:**
- I nomi dei set di dati devono essere brevi e descrittivi in modo che il set di dati possa essere facilmente trovato nella libreria in un secondo momento.
- I nomi dei set di dati devono essere univoci, il che significa che devono essere sufficientemente specifici da non essere riutilizzati in futuro.
- È consigliabile fornire informazioni aggiuntive sul set di dati utilizzando il campo di descrizione, in quanto potrebbe aiutare altri utenti a distinguere tra set di dati in futuro.

Una volta che il dataset ha un nome e una descrizione, fare clic su **Fine**.

![Configura set di dati](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Attività DataSet

È stato creato un set di dati vuoto e l&#39;utente è stato riportato nella scheda Attività ** DataSet nell&#39;area di lavoro Set di dati. Il nome del set di dati deve essere visualizzato nell’angolo in alto a sinistra dell’area di lavoro, insieme alla notifica che &quot;Non sono stati aggiunti batch&quot;. Questo è previsto perché non avete ancora aggiunto alcun batch a questo set di dati.

Sul lato destro dell&#39;area di lavoro Set di dati viene visualizzata la scheda **Informazioni** contenente informazioni relative al nuovo set di dati, quali ID *set di dati,* Nome *,* Descrizione *, Nome**tabella, NomeSchema*******, , Streaminge Sorgente. La scheda Informazioni include anche informazioni su quando il set di dati è stato *creato* e sulla data dell&#39; *ultima modifica* .

Prendete nota dell&#39;ID **** set di dati, in quanto questo valore è richiesto per completare il flusso di lavoro di esportazione del segmento di pubblico.

![Attività DataSet](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Passaggi successivi

Dopo aver creato un set di dati basato sullo schema unionale profilo singolo XDM, è possibile utilizzare l&#39;ID **** set di dati per continuare l&#39;esercitazione [di valutazione e accesso ai risultati](./evaluate-a-segment.md) del segmento.

Al momento, tornate all’esercitazione sui risultati del segmento di valutazione e fate clic sul passaggio [Genera profili individuali XDM per i membri](./evaluate-a-segment.md#generate-profiles-for-audience-members) del pubblico nel flusso di lavoro di [esportazione di un segmento](./evaluate-a-segment.md#export-a-segment) .
