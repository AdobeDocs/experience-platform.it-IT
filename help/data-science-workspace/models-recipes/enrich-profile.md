---
keywords: Experience Platform;machine learning model;Data Science Workspace;Real-time Customer Profile;popular topics
solution: Experience Platform
title: Arricchisci il profilo cliente in tempo reale con informazioni approfondite sull'apprendimento automatico
topic: Tutorial
translation-type: tm+mt
source-git-commit: 34fff508f49327ce314a517d77efabb286ef055c

---


# Arricchisci il profilo cliente in tempo reale con informazioni approfondite sull&#39;apprendimento automatico

Adobe Experience Platform Data Science Workspace offre gli strumenti e le risorse per creare, valutare e utilizzare modelli di machine learning per generare previsioni e approfondimenti sui dati. Quando le informazioni di machine learning vengono inserite in un dataset abilitato per il profilo, gli stessi dati vengono anche assimilati come record di profilo che possono essere poi segmentati in sottoinsiemi di elementi correlati utilizzando Experience Platform Segmentation Service.

Questo documento fornisce un&#39;esercitazione dettagliata per arricchire il profilo cliente in tempo reale con informazioni approfondite sull&#39;apprendimento automatico. I passaggi sono suddivisi nelle seguenti sezioni:

1. [Creare uno schema di output e un dataset](#create-an-output-schema-and-dataset)
2. [Configurare uno schema di output e un dataset](#configure-an-output-schema-and-dataset)
3. [Creazione di segmenti con Segment Builder (Generatore di segmenti)](#create-segments-using-the-segment-builder)

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei vari aspetti di Adobe Experience Platform coinvolti nell&#39;acquisizione dei dati del profilo e nella creazione di segmenti. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../../rtcdp/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../identity-service/home.md)identità: Abilita il profilo cliente in tempo reale collegando identità da origini dati diverse che vengono caricate nella piattaforma.
* [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.

Oltre ai documenti di cui sopra, si consiglia di consultare anche le seguenti guide sugli schemi e sull&#39;Editor di schema:

* [Nozioni di base sulla composizione](../../xdm/schema/composition.md)dello schema: Descrive gli schemi XDM, i blocchi costitutivi, i principi e le procedure ottimali per la composizione degli schemi da utilizzare in Experience Platform.
* [Esercitazione](../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Fornisce istruzioni dettagliate per la creazione di schemi utilizzando l&#39;Editor di schema in Experience Platform.

## Creare uno schema di output e un dataset

Il primo passo verso l&#39;arricchimento del profilo cliente in tempo reale con informazioni di punteggio è sapere quale oggetto reale (come una persona) definisce i tuoi dati. La comprensione dei dati consente di descrivere e progettare una struttura che ha un significato per i dati, come la progettazione di un database relazionale.

La composizione di uno schema inizia con l&#39;assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Questa sezione fornisce istruzioni di base per creare uno schema utilizzando il generatore di schemi. Per un&#39;esercitazione più dettagliata, fare riferimento all&#39;esercitazione sulla [creazione di uno schema con l&#39;Editor](../../xdm/tutorials/create-schema-ui.md)di schema.

1. In Adobe Experience Platform, fai clic sulla scheda **Schema** per accedere al browser dello schema. Fare clic su **Crea schema** per accedere all&#39;Editor **schema, dove è possibile creare e creare schemi in modo interattivo.
   ![](../images/models-recipes/enrich-rtcdp/schema_browser.png)

2. Nella finestra *Composizione* , fate clic su **Assegna** per esplorare le classi disponibili.
   * Per assegnare una classe esistente, fare clic sulla classe desiderata ed evidenziarla, quindi fare clic su **Assegna classe**.
      ![](../images/models-recipes/enrich-rtcdp/existing_class.png)

   * Per creare una classe personalizzata, fate clic su **Crea nuova classe** disponibile accanto al centro nella parte superiore della finestra del browser. Immettete un nome di classe, una descrizione e scegliete il comportamento della classe. Al termine, fate clic su **Assegna classe** .
      ![](../images/models-recipes/enrich-rtcdp/create_new_class.png)
   A questo punto, la struttura dello schema deve contenere alcuni campi di classe ed è possibile assegnare i mixin. Un mixin è un gruppo di uno o più campi che descrivono un concetto particolare.

3. Nella finestra *Composizione* , fate clic su **Aggiungi** nella sottosezione *Mixins* .
   * Per assegnare un mixin esistente, fate clic ed evidenziate il mixin desiderato, quindi fate clic su **Aggiungi mixin**. A differenza delle classi, è possibile assegnare più mixin a un singolo schema, purché sia appropriato.
      ![](../images/models-recipes/enrich-rtcdp/existing_mixin.png)

   * Per creare un nuovo mixin, fate clic su **Create New Mixin (Crea nuovo mixin** ) vicino al centro nella parte superiore della finestra del browser. Al termine, specificate un nome e una descrizione per il mixin, quindi fate clic su **Assegna mixin** .
      ![](../images/models-recipes/enrich-rtcdp/create_new_mixin.png)

   * Per aggiungere campi mixin, fate clic sul nome del mixin nella finestra *Composizione* . Verrà quindi fornita l&#39;opzione per aggiungere campi mixin facendo clic su **Aggiungi campo** nella finestra *Struttura* . Assicurarsi di fornire le proprietà di mixin di conseguenza.
      ![](../images/models-recipes/enrich-rtcdp/mixin_properties.png)

4. Dopo aver creato lo schema, fare clic sul campo di livello superiore dello schema all&#39;interno della finestra *Struttura* per visualizzare le proprietà dello schema nella finestra delle proprietà a destra. Immettete un nome e una descrizione, quindi fate clic su **Salva** per creare lo schema.
   ![](../images/models-recipes/enrich-rtcdp/save_schema.png)

5. Crea un set di dati di output utilizzando lo schema appena creato facendo clic su **Set** di dati dalla colonna di navigazione a sinistra, quindi fai clic su **Crea set di dati**. Nella schermata successiva, scegliete **Crea set di dati dallo schema**.
   ![](../images/models-recipes/enrich-rtcdp/dataset_overview.png)

6. Utilizzando il browser dello schema, individuare e selezionare lo schema appena creato, quindi fare clic su **Avanti**.
   ![](../images/models-recipes/enrich-rtcdp/choose_schema.png)

7. Immettete un nome e una descrizione facoltativa, quindi fate clic su **Fine** per creare il set di dati.
   ![](../images/models-recipes/enrich-rtcdp/configure_dataset.png)

Ora che è stato creato un set di dati dello schema di output, è possibile continuare fino alla sezione successiva per configurarlo e abilitarlo per l&#39;arricchimento del profilo.

## Configurare uno schema di output e un dataset

Prima di abilitare un dataset per il profilo, è necessario configurare lo schema del dataset in modo che abbia un campo identità principale e quindi attivare lo schema per il profilo. Se si desidera creare e abilitare un nuovo schema, è possibile fare riferimento all&#39;esercitazione sulla [creazione di uno schema utilizzando l&#39;Editor](../../xdm/tutorials/create-schema-ui.md)di schema. In caso contrario, seguire le istruzioni riportate di seguito per abilitare uno schema e un dataset esistenti.

1. In Adobe Experience Platform, usate il browser dello schema per trovare lo schema di output su cui desiderate abilitare il profilo e fate clic sul suo nome per visualizzarne la composizione.
   ![](../images/models-recipes/enrich-rtcdp/schemas.png)

2. Espandere la struttura dello schema e trovare un campo appropriato da impostare come identificatore principale. Fate clic sul campo desiderato per visualizzarne le proprietà.
   ![](../images/models-recipes/enrich-rtcdp/schema_structure.png)

3. Impostare il campo come identità principale abilitando la proprietà **Identità** del campo, la proprietà Identità **** principale, quindi selezionando uno spazio dei nomi **** identità appropriato. Fate clic su **Applica** dopo aver apportato le modifiche.
   ![](../images/models-recipes/enrich-rtcdp/set_identity.png)

4. Fare clic sull&#39;oggetto di primo livello della struttura dello schema per visualizzare le proprietà dello schema e attivare lo schema per Profilo attivando lo switch **Profilo** . Fai clic su **Salva** per finalizzare le modifiche. È ora possibile abilitare per il profilo il set di dati creato con questo schema.
   ![](../images/models-recipes/enrich-rtcdp/enable_schema.png)

5. Utilizzate il browser del set di dati per trovare il set di dati su cui desiderate abilitare il profilo e fate clic sul suo nome per accedere ai relativi dettagli.
   ![](../images/models-recipes/enrich-rtcdp/datasets.png)

6. Attivate il set di dati per il profilo attivando lo switch **Profilo** presente nella colonna delle informazioni corrette.
   ![](../images/models-recipes/enrich-rtcdp/enable_dataset.png)

Quando i dati vengono trasferiti in un dataset abilitato per il profilo, gli stessi dati vengono anche assimilati come record di profilo. Ora che lo schema e il set di dati sono preparati, genera alcuni dati nel dataset eseguendo l&#39;esecuzione del punteggio utilizzando un modello appropriato, quindi continua con questa esercitazione per creare segmenti di approfondimento utilizzando Segment Builder (Generatore di segmenti).

## Creazione di segmenti con Segment Builder (Generatore di segmenti)

Ora che hai generato e acquisito informazioni approfondite nel set di dati abilitato per il profilo, puoi gestire tali dati identificando sottoinsiemi di elementi correlati tramite Segment Builder (Generatore di segmenti). Segui i passaggi indicati di seguito per creare i tuoi segmenti.

1. In Adobe Experience Platform, fai clic sulla scheda **Segmenti** , seguita da **Crea segmento** per accedere al Generatore di segmenti.
   ![](../images/models-recipes/enrich-rtcdp/segments_overview.png)

2. In Segment Builder (Generatore di segmenti), la barra a sinistra consente di accedere ai blocchi di generazione principali dei segmenti: attributi, eventi e segmenti esistenti. Ciascun blocco predefinito viene visualizzato nella relativa scheda. Seleziona la classe alla quale si estende lo schema abilitato per il profilo, quindi individua e individua i blocchi di generazione per il segmento.
   ![](../images/models-recipes/enrich-rtcdp/segment_builder.png)

3. Trascinare e rilasciare i blocchi di generazione nell&#39;area di lavoro del generatore di regole, per completarli fornendo istruzioni comparative.
   ![](../images/models-recipes/enrich-rtcdp/drag_fill.gif)

4. Durante la creazione del segmento potete visualizzare in anteprima i risultati stimati del segmento osservando il pannello Proprietà ** segmento.
   ![](../images/models-recipes/enrich-rtcdp/preview_segment.gif)

5. Seleziona un criterio **di** unione appropriato, specifica un nome e una descrizione facoltativa, quindi fai clic su **Salva** per completare il nuovo segmento.
   ![](../images/models-recipes/enrich-rtcdp/save_segment.png)


## Passaggi successivi

Questo documento illustra i passaggi necessari per abilitare uno schema e un set di dati per il profilo e illustra brevemente il flusso di lavoro per la creazione di segmenti di approfondimento mediante il Generatore di segmenti. Per ulteriori informazioni sui segmenti e sul Generatore di segmenti, consulta la panoramica [del servizio](../../segmentation/home.md)Segmentazione.