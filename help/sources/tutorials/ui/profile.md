---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Attivare i dati di origine in entrata per compilare i profili cliente
topic: overview
translation-type: tm+mt
source-git-commit: 6bd5dc5a68fb2814ab99d43b34f90aa7e50aa463
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Attivare i dati di origine in entrata per compilare i profili cliente

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e compilare [!DNL Real-time Customer Profile] i dati.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Profilo cliente in tempo reale]](../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che sia già stato creato e configurato un connettore di origine.  Un elenco di esercitazioni per la creazione di diversi connettori nell’interfaccia utente è disponibile nella panoramica [dei connettori](../../home.md)sorgente.

## Compilazione dei [!DNL Real-time Customer Profile] dati

Per arricchire i profili dei clienti, lo schema di origine del dataset di destinazione deve essere compatibile per l&#39;uso in [!DNL Real-time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

- Lo schema ha almeno un attributo specificato come proprietà identity.
- Lo schema presenta una proprietà identity definita come identità primaria.
- Esiste una mappatura all&#39;interno del flusso di dati in cui l&#39;identità primaria è un attributo di destinazione.

Nell&#39;area di lavoro Origini, fare clic sulla **[!UICONTROL Browse]** scheda per elencare le connessioni di base. Nell’elenco visualizzato, individuate la connessione che contiene il flusso di dati con cui desiderate compilare i profili. Fate clic sul nome della connessione per accedere ai relativi dettagli.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Viene visualizzata la **[!UICONTROL Source activity]** schermata della connessione, in cui sono visualizzati i set di dati in cui la connessione sta trasferendo i dati di origine. Fare clic sul nome del set di dati per il quale si desidera abilitare [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Viene **[!UICONTROL Dataset activity]** visualizzata la schermata. La **[!UICONTROL Properties]** colonna a destra della schermata mostra i dettagli del dataset, include un **[!UICONTROL Profile]** interruttore e un collegamento allo schema a cui il dataset aderisce. Fate clic sul nome dello schema per visualizzarne la composizione.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Viene **[!UICONTROL Schema Editor]** visualizzata la struttura dello schema nel quadro centrale. All&#39;interno del quadro, selezionare il campo da impostare come identità principale. Sotto la *[!UICONTROL Field properties]* scheda visualizzata, selezionare la **[!UICONTROL Identity]** casella di controllo, quindi **[!UICONTROL Primary identity]**. Infine, selezionate un elemento appropriato **[!UICONTROL Identity namespace]**, quindi fate clic su **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Fare clic sull&#39;oggetto di primo livello della struttura dello schema e viene visualizzata la **[!UICONTROL Schema properties]** colonna. Abilitare lo schema per [!DNL Profile] attivando l&#39; **[!UICONTROL Profile]** interruttore. Fate clic **[!UICONTROL Save]** per finalizzare le modifiche.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ora che lo schema è abilitato, [!DNL Profile]tornare alla **[!UICONTROL Dataset activity]** schermata e abilitare il dataset [!DNL Profile] facendo clic sull&#39; **[!UICONTROL Profile]** interruttore all&#39;interno della **[!UICONTROL Properties]** colonna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con lo schema e il set di dati abilitati per [!DNL Profile], i dati inseriti in tale set di dati ora popoleranno anche i profili dei clienti.

>[!NOTE]
>
>I dati esistenti all&#39;interno di un dataset abilitato di recente non vengono utilizzati da [!DNL Profile].

## Passaggi successivi

Seguendo questa esercitazione, i dati in entrata sono stati attivati correttamente per la [!DNL Profile] popolazione. For more information, see the [[!DNL Real-time Customer Profile] overview](../../../profile/home.md).