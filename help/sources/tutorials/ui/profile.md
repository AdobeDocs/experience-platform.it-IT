---
keywords: Experience Platform;home;argomenti popolari;attivare dati in entrata;popolare profilo;popolare rtcp;popolato profilo unificato
solution: Experience Platform
title: Attivare i dati di origine in entrata per popolare i profili dei clienti nell’interfaccia utente
type: Tutorial
description: I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati del Profilo cliente in tempo reale.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Attiva i dati di origine in entrata per popolare i profili cliente

I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare il [!DNL Real-Time Customer Profile] dati.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’editor di schemi](../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questo tutorial richiede che tu abbia già creato e configurato un connettore di origine.  Un elenco di esercitazioni per la creazione di diversi connettori nell’interfaccia utente è disponibile nella sezione [panoramica dei connettori di origini](../../home.md).

## Popola il tuo [!DNL Real-Time Customer Profile] dati

Per arricchire i profili dei clienti, lo schema di origine del set di dati di destinazione deve essere compatibile per l’utilizzo in [!DNL Real-Time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

- Lo schema ha almeno un attributo specificato come proprietà di identità.
- Lo schema ha una proprietà di identità definita come identità primaria.
- Esiste una mappatura all’interno del flusso di dati in cui l’identità primaria è un attributo di destinazione.

Nell’area di lavoro Origini, fai clic su **[!UICONTROL Sfoglia]** per elencare le connessioni di base. Nell’elenco visualizzato, individua la connessione contenente il flusso di dati con cui desideri popolare i profili. Fai clic sul nome della connessione per accedere ai relativi dettagli.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

La connessione è **[!UICONTROL Attività sorgente]** viene visualizzata la schermata che mostra i set di dati in cui la connessione sta acquisendo i dati di origine. Fai clic sul nome del set di dati che desideri abilitare per [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Il **[!UICONTROL Attività set di dati]** viene visualizzata la schermata. Il **[!UICONTROL Proprietà]** sul lato destro dello schermo mostra i dettagli del set di dati e include una **[!UICONTROL Profilo]** e un collegamento allo schema a cui aderisce il set di dati. Fare clic sul nome dello schema per visualizzarne la composizione.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Il **[!UICONTROL Editor schema]** viene visualizzata, mostrando la struttura dello schema nell&#39;area di lavoro centrale. Nell’area di lavoro, seleziona il campo da impostare come identità primaria. Sotto **[!UICONTROL Proprietà campo]** che viene visualizzata, seleziona la scheda **[!UICONTROL Identità]** casella di controllo, quindi **[!UICONTROL Identità primaria]**. Infine, seleziona un **[!UICONTROL Spazio dei nomi dell’identità]**, quindi fai clic su **[!UICONTROL Applica]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Fare clic sull&#39;oggetto di primo livello della struttura dello schema e sul **[!UICONTROL Proprietà dello schema]** viene visualizzata. Abilita lo schema per [!DNL Profile] attivando/disattivando **[!UICONTROL Profilo]** switch. Clic **[!UICONTROL Salva]** per finalizzare le modifiche.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ora che lo schema è abilitato per [!DNL Profile], torna a **[!UICONTROL Attività set di dati]** e abilita il set di dati per [!DNL Profile] facendo clic su **[!UICONTROL Profilo]** attivare/disattivare all&#39;interno di **[!UICONTROL Proprietà]** colonna.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con schema e set di dati abilitati per [!DNL Profile]Ora anche i dati acquisiti in tale set di dati popolano i profili dei clienti.

>[!NOTE]
>
>I dati esistenti all’interno di un set di dati abilitato di recente non vengono utilizzati da [!DNL Profile].

## Passaggi successivi

Seguendo questa esercitazione, hai attivato correttamente i dati in entrata per [!DNL Profile] popolazione. Per ulteriori informazioni, vedere [[!DNL Real-Time Customer Profile] panoramica](../../../profile/home.md).
