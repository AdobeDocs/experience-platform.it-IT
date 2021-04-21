---
keywords: Experience Platform;home;argomenti popolari;attivare dati in entrata;compilare profilo;popolare rtcp;profilo unificato popolato
solution: Experience Platform
title: Attivare i dati di origine in entrata per popolare i profili dei clienti nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati del profilo cliente in tempo reale.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Attivare i dati di origine in entrata per popolare i profili dei clienti

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati [!DNL Real-time Customer Profile].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che sia già stato creato e configurato un connettore di origine.  Un elenco di esercitazioni per la creazione di diversi connettori nell&#39;interfaccia utente è disponibile nella [panoramica dei connettori sorgente](../../home.md).

## Compilare i dati [!DNL Real-time Customer Profile]

Per arricchire i profili dei clienti, lo schema di origine del set di dati di destinazione deve essere compatibile per l’utilizzo in [!DNL Real-time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

- Lo schema ha almeno un attributo specificato come proprietà Identity.
- Lo schema presenta una proprietà Identity definita come identità principale.
- Esiste una mappatura all’interno del flusso di dati in cui l’identità principale è un attributo di destinazione.

Nell&#39;area di lavoro Origini fare clic sulla scheda **[!UICONTROL Browse]** per elencare le connessioni di base. Nell’elenco visualizzato, individua la connessione contenente il flusso di dati con cui desideri compilare i profili. Fare clic sul nome della connessione per accedere ai relativi dettagli.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Viene visualizzata la schermata **[!UICONTROL Source activity]** della connessione, che mostra i set di dati in cui la connessione sta acquisendo i dati di origine. Fai clic sul nome del set di dati da abilitare per [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Viene visualizzata la schermata **[!UICONTROL Dataset activity]**. La colonna **[!UICONTROL Properties]** sul lato destro dello schermo visualizza i dettagli del set di dati e include uno switch **[!UICONTROL Profile]** e un collegamento allo schema a cui il set di dati aderisce. Fare clic sul nome dello schema per visualizzarne la composizione.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Viene visualizzata la sezione **[!UICONTROL Schema Editor]** che mostra la struttura dello schema nell&#39;area di lavoro centrale. Nell’area di lavoro, seleziona il campo da impostare come identità principale. Sotto la scheda **[!UICONTROL Field properties]** visualizzata, seleziona la casella di controllo **[!UICONTROL Identity]** , quindi **[!UICONTROL Primary identity]**. Infine, seleziona un **[!UICONTROL Identity namespace]** appropriato, quindi fai clic su **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Fai clic sull’oggetto di livello superiore della struttura dello schema e viene visualizzata la colonna **[!UICONTROL Schema properties]** . Abilita lo schema per [!DNL Profile] attivando il parametro **[!UICONTROL Profile]**. Fai clic su **[!UICONTROL Save]** per finalizzare le modifiche.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ora che lo schema è abilitato per [!DNL Profile], torna alla schermata **[!UICONTROL Dataset activity]** e attiva il set di dati per [!DNL Profile] facendo clic sull&#39;interruttore **[!UICONTROL Profile]** all&#39;interno della colonna **[!UICONTROL Properties]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con lo schema e il set di dati abilitati per [!DNL Profile], i dati acquisiti in quel set di dati compileranno anche i profili dei clienti.

>[!NOTE]
>
>I dati esistenti all’interno di un set di dati abilitato di recente non vengono utilizzati da [!DNL Profile].

## Passaggi successivi

Seguendo questa esercitazione, hai attivato correttamente i dati in entrata per la popolazione [!DNL Profile] . Per ulteriori informazioni, consulta la sezione [[!DNL Real-time Customer Profile] panoramica](../../../profile/home.md).
