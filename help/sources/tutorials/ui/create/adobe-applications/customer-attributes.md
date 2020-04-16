---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine attributi cliente nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creare un connettore di origine attributi cliente nell&#39;interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un connettore di origine nell&#39;interfaccia utente per la raccolta dei dati di profilo degli attributi del cliente in Adobe Experience Platform. Per ulteriori informazioni sugli attributi del cliente, consultate il documento [](https://docs.adobe.com/content/help/it-IT/core-services/interface/customer-attributes/attributes.html)della panoramica.

## Creazione di una connessione di origine

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro delle origini. Nella schermata *Catalogo* sono visualizzate le sorgenti disponibili con cui creare connessioni in ingresso e ogni origine mostra il numero di connessioni esistenti ad esse associate. Selezionate l&#39;opzione per Attributi **** cliente, quindi fate clic su Origine **** Connect. Se la connessione viene stabilita, l&#39;utente verrà reindirizzato se la connessione viene stabilita correttamente.

>[!NOTE] Se hai già stabilito un connettore di origine per i dati di profilo degli attributi del cliente, l&#39;opzione per connettersi all&#39;origine verrà disabilitata.

![](../../../../images/tutorials/create/customer-attributes/CA-sources_catalog.png)

Nella schermata Attività *di* origine sono elencate tutte le connessioni precedentemente stabilite per i dati di profilo degli attributi cliente. È possibile creare una nuova connessione facendo clic su **Seleziona dati**.

>[!NOTE] È possibile creare più connessioni in entrata a un&#39;origine per inserire dati diversi.

![](../../../../images/tutorials/create/customer-attributes/CA-source_activity.png)

Dall&#39;elenco dei set di dati di profilo di attributi cliente disponibili, selezionate quello da importare in Piattaforma e fate clic su **Avanti**.

>[!NOTE] È possibile selezionare un solo set di dati per connessione di origine attributi cliente.

![](../../../../images/tutorials/create/customer-attributes/CA-select_data.png)

Viene visualizzato il passaggio *Revisione* , che consente di controllare la nuova connessione in ingresso prima della creazione. I dettagli della connessione sono raggruppati per categorie, tra cui:

* *Dettagli* origine: Mostra il tipo di connessione di origine e i dati di origine selezionati.
* *Dettagli* di destinazione: Quando si creano altri connettori di origine, questo contenitore mostra in quale set di dati di origine vengono acquisiti i dati, incluso lo schema a cui il dataset aderisce. I dati del profilo degli attributi del cliente vengono mappati automaticamente e assimilati in profili cliente in tempo reale.

![](../../../../images/tutorials/create/customer-attributes/CA-review.png)

## Passaggi successivi

Una volta creata la connessione, viene automaticamente creato uno schema di destinazione e un dataset che contiene i dati in arrivo. Al termine dell&#39;assimilazione iniziale, i dati del profilo degli attributi del cliente possono essere utilizzati dai servizi della piattaforma a valle, come Profilo cliente in tempo reale e Servizio di segmentazione. Per ulteriori informazioni, consulta i documenti seguenti:

* [Panoramica del profilo cliente in tempo reale](../../../../../profile/home.md)
* [Panoramica del servizio di segmentazione](../../../../../segmentation/home.md)
