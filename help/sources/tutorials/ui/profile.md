---
keywords: Experience Platform;home;argomenti popolari;attivare dati in entrata;compilare profilo;popolare rtcp;profilo unificato popolato
solution: Experience Platform
title: Attivare i dati di origine in entrata per popolare i profili dei clienti nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati del profilo cliente in tempo reale.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Attivare i dati di origine in entrata per popolare i profili dei clienti

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare il tuo [!DNL Real-Time Customer Profile] dati.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questa esercitazione richiede che sia già stato creato e configurato un connettore di origine.  Un elenco di esercitazioni per la creazione di diversi connettori nell’interfaccia utente è disponibile nella sezione [panoramica dei connettori sorgente](../../home.md).

## Popolare il tuo [!DNL Real-Time Customer Profile] dati

Per arricchire i profili dei clienti, lo schema di origine del set di dati di destinazione deve essere compatibile per l’utilizzo in [!DNL Real-Time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

- Lo schema ha almeno un attributo specificato come proprietà Identity.
- Lo schema presenta una proprietà Identity definita come identità principale.
- Esiste una mappatura all’interno del flusso di dati in cui l’identità principale è un attributo di destinazione.

Nell&#39;area di lavoro Origini, fai clic sul pulsante **[!UICONTROL Sfoglia]** scheda per elencare le connessioni di base. Nell’elenco visualizzato, individua la connessione contenente il flusso di dati con cui desideri compilare i profili. Fare clic sul nome della connessione per accedere ai relativi dettagli.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

La connessione è **[!UICONTROL Attività di origine]** viene visualizzata una schermata in cui sono visualizzati i set di dati in cui la connessione sta acquisendo i dati di origine. Fai clic sul nome del set di dati per il quale desideri abilitare [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

La **[!UICONTROL Attività set di dati]** viene visualizzata la schermata . La **[!UICONTROL Proprietà]** la colonna a destra dello schermo visualizza i dettagli del set di dati e include un **[!UICONTROL Profilo]** passa a e a un collegamento allo schema a cui aderisce il set di dati. Fare clic sul nome dello schema per visualizzarne la composizione.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

La **[!UICONTROL Editor di schema]** viene visualizzata la struttura dello schema nell&#39;area di lavoro centrale. Nell’area di lavoro, seleziona il campo da impostare come identità principale. Sotto la **[!UICONTROL Proprietà campo]** seleziona la scheda visualizzata **[!UICONTROL Identità]** casella di controllo, quindi **[!UICONTROL Identità principale]**. Infine, seleziona un **[!UICONTROL Spazio dei nomi identità]**, quindi fai clic su **[!UICONTROL Applica]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Fai clic sull’oggetto di primo livello della struttura dello schema e sul pulsante **[!UICONTROL Proprietà dello schema]** viene visualizzata la colonna . Abilita lo schema per [!DNL Profile] attivando **[!UICONTROL Profilo]** interruttore. Fai clic su **[!UICONTROL Salva]** per finalizzare le modifiche.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ora che lo schema è abilitato per [!DNL Profile], torna alla sezione **[!UICONTROL Attività set di dati]** scherma e abilita il set di dati per [!DNL Profile] facendo clic sul pulsante **[!UICONTROL Profilo]** all&#39;interno di **[!UICONTROL Proprietà]** colonna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con lo schema e il set di dati abilitati per [!DNL Profile], i dati acquisiti in quel set di dati ora popolano anche i profili dei clienti.

>[!NOTE]
>
>I dati esistenti in un set di dati abilitato di recente non vengono utilizzati da [!DNL Profile].

## Passaggi successivi

Seguendo questa esercitazione, hai attivato correttamente i dati in entrata per [!DNL Profile] popolazione. Per ulteriori informazioni, consulta la sezione [[!DNL Real-Time Customer Profile] panoramica](../../../profile/home.md).
