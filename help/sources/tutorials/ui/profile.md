---
keywords: ' Experience Platform;home;argomenti popolari;attivare i dati in entrata;compilare il profilo;popolare rtcp;popolato profilo unificato'
solution: Experience Platform
title: Attivare i dati di origine in entrata per compilare i profili cliente nell’interfaccia utente
topic: overview
type: Tutorial
description: I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e compilare i dati del profilo cliente in tempo reale.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Attivare i dati di origine in entrata per compilare i profili cliente

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e compilare i dati [!DNL Real-time Customer Profile].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che sia già stato creato e configurato un connettore di origine.  Un elenco di esercitazioni per la creazione di diversi connettori nell&#39;interfaccia utente è disponibile nella [panoramica dei connettori sorgente](../../home.md).

## Compilare i dati [!DNL Real-time Customer Profile]

Per arricchire i profili dei clienti, lo schema di origine del dataset di destinazione deve essere compatibile per l&#39;utilizzo in [!DNL Real-time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

- Lo schema ha almeno un attributo specificato come proprietà identity.
- Lo schema presenta una proprietà identity definita come identità primaria.
- Esiste una mappatura all&#39;interno del flusso di dati in cui l&#39;identità primaria è un attributo di destinazione.

Nell&#39;area di lavoro Origini, fare clic sulla scheda **[!UICONTROL Browse]** per elencare le connessioni di base. Nell’elenco visualizzato, individuate la connessione che contiene il flusso di dati con cui desiderate compilare i profili. Fate clic sul nome della connessione per accedere ai relativi dettagli.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Viene visualizzata la schermata **[!UICONTROL Source activity]** della connessione, che mostra i set di dati in cui la connessione sta trasferendo i dati di origine. Fare clic sul nome del set di dati che si desidera abilitare per [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Viene visualizzata la schermata **[!UICONTROL Dataset activity]**. La colonna **[!UICONTROL Properties]** sul lato destro dello schermo visualizza i dettagli del dataset, include uno switch **[!UICONTROL Profile]** e un collegamento allo schema a cui il dataset aderisce. Fate clic sul nome dello schema per visualizzarne la composizione.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Viene visualizzata la **[!UICONTROL Schema Editor]** che mostra la struttura dello schema nel quadro centrale. All&#39;interno del quadro, selezionare il campo da impostare come identità principale. Sotto la scheda **[!UICONTROL Field properties]** visualizzata, selezionare la casella di controllo **[!UICONTROL Identity]**, quindi **[!UICONTROL Primary identity]**. Infine, selezionare un **[!UICONTROL Identity namespace]** appropriato, quindi fare clic su **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Fare clic sull&#39;oggetto di primo livello della struttura dello schema e viene visualizzata la colonna **[!UICONTROL Schema properties]**. Abilitare lo schema per [!DNL Profile] attivando l&#39;interruttore **[!UICONTROL Profile]**. Fate clic su **[!UICONTROL Save]** per finalizzare le modifiche.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ora che lo schema è abilitato per [!DNL Profile], tornare alla schermata **[!UICONTROL Dataset activity]** e abilitare il dataset per [!DNL Profile] facendo clic sull&#39;interruttore **[!UICONTROL Profile]** all&#39;interno della colonna **[!UICONTROL Properties]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con lo schema e il set di dati abilitati per [!DNL Profile], i dati inseriti in tale set di dati ora popoleranno anche i profili cliente.

>[!NOTE]
>
>I dati esistenti in un dataset abilitato di recente non vengono utilizzati da [!DNL Profile].

## Passaggi successivi

Seguendo questa esercitazione, i dati in entrata sono stati attivati correttamente per la popolazione [!DNL Profile]. Per ulteriori informazioni, vedere la [[!DNL Real-time Customer Profile] panoramica](../../../profile/home.md).