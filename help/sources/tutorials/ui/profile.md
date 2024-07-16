---
keywords: Experience Platform;home;argomenti popolari;attivare dati in entrata;popolare profilo;popolare rtcp;popolato profilo unificato
solution: Experience Platform
title: Attivare i dati Source in entrata per popolare i profili cliente nell’interfaccia utente
type: Tutorial
description: I dati in entrata provenienti dal connettore di origine possono essere utilizzati per arricchire e popolare i dati del Profilo cliente in tempo reale.
exl-id: ddd3766a-3f55-4bbc-8358-c578eae2c629
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Attiva i dati di origine in entrata per popolare i profili cliente

I dati in entrata dal connettore di origine possono essere utilizzati per arricchire e popolare i dati [!DNL Real-Time Customer Profile].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull&#39;editor di schemi](../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Inoltre, questo tutorial richiede che tu abbia già creato e configurato un connettore di origine.  Un elenco di esercitazioni per la creazione di diversi connettori nell&#39;interfaccia utente è disponibile nella [panoramica dei connettori di origine](../../home.md).

## Popola i tuoi dati di [!DNL Real-Time Customer Profile]

Per arricchire i profili dei clienti, lo schema di origine del set di dati di destinazione deve essere compatibile per l&#39;utilizzo in [!DNL Real-Time Customer Profile]. Uno schema compatibile soddisfa i seguenti requisiti:

- Lo schema ha almeno un attributo specificato come proprietà di identità.
- Lo schema ha una proprietà di identità definita come identità primaria.
- Esiste una mappatura all’interno del flusso di dati in cui l’identità primaria è un attributo di destinazione.

Nell&#39;area di lavoro Origini fare clic sulla scheda **[!UICONTROL Sfoglia]** per elencare le connessioni di base. Nell’elenco visualizzato, individua la connessione contenente il flusso di dati con cui desideri popolare i profili. Fai clic sul nome della connessione per accedere ai relativi dettagli.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

Viene visualizzata la schermata dell&#39;**[!UICONTROL attività Source]** della connessione, in cui sono visualizzati i set di dati in cui la connessione acquisisce i dati di origine. Fare clic sul nome del set di dati che si desidera abilitare per [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

Viene visualizzata la schermata **[!UICONTROL Attività set di dati]**. La colonna **[!UICONTROL Proprietà]** sul lato destro dello schermo visualizza i dettagli del set di dati e include un&#39;opzione **[!UICONTROL Profilo]** e un collegamento allo schema a cui il set di dati aderisce. Fare clic sul nome dello schema per visualizzarne la composizione.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

Viene visualizzato l&#39;**[!UICONTROL Editor schema]**, che mostra la struttura dello schema nell&#39;area di lavoro centrale. Nell’area di lavoro, seleziona il campo da impostare come identità primaria. Nella scheda **[!UICONTROL Proprietà campo]** visualizzata, selezionare la casella di controllo **[!UICONTROL Identità]**, quindi **[!UICONTROL Identità primaria]**. Infine, selezionare uno spazio dei nomi **[!UICONTROL Identity]** appropriato, quindi fare clic su **[!UICONTROL Apply]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Fare clic sull&#39;oggetto di primo livello della struttura dello schema per visualizzare la colonna **[!UICONTROL Proprietà schema]**. Abilitare lo schema per [!DNL Profile] attivando l&#39;opzione **[!UICONTROL Profilo]**. Fai clic su **[!UICONTROL Salva]** per finalizzare le modifiche.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Ora che lo schema è abilitato per [!DNL Profile], tornare alla schermata **[!UICONTROL Attività set di dati]** e abilitare il set di dati per [!DNL Profile] facendo clic sull&#39;interruttore **[!UICONTROL Profilo]** nella colonna **[!UICONTROL Proprietà]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Con lo schema e il set di dati abilitati per [!DNL Profile], anche i dati acquisiti in tale set di dati popoleranno i profili cliente.

>[!NOTE]
>
>I dati esistenti in un set di dati abilitato di recente non vengono utilizzati da [!DNL Profile].

## Passaggi successivi

Seguendo questa esercitazione, i dati in entrata sono stati attivati correttamente per la popolazione [!DNL Profile]. Per ulteriori informazioni, vedere la [[!DNL Real-Time Customer Profile] panoramica](../../../profile/home.md).
