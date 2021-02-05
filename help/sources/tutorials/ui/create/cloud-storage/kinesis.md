---
keywords: ' Experience Platform;home;argomenti popolari; Amazon Kinesis;amazon kinesis;Kinesis;kinesis'
solution: Experience Platform
title: Creare una connessione  Amazon Kinesis Source nell'interfaccia utente
topic: overview
type: Tutorial
description: Scoprite come creare una connessione sorgente Amazon  Kinesis utilizzando l'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Amazon Kinesis] nell&#39;interfaccia utente

>[!NOTE]
>
>Il connettore [!DNL Amazon Kinesis] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce passaggi per l&#39;autenticazione di un connettore di origine [!DNL Amazon Kinesis] (in seguito denominato [!DNL "Kinesis"]) mediante l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione [!DNL Kinesis] valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage-streaming.md).

### Raccogli credenziali richieste

Per autenticare il connettore di origine [!DNL Kinesis], è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | ID chiave di accesso per l&#39;account [!DNL Kinesis]. |
| `Secret access key` | La chiave di accesso segreta per l&#39;account [!DNL Kinesis]. |
| `region` | La regione del server AWS. |

Per ulteriori informazioni su questi valori, fare riferimento a [this [!DNL Kinesis] document](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Collegare l&#39;account [!DNL Kinesis]

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account [!DNL Kinesis] a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL Cloud Storage]**, selezionare **[!UICONTROL Amazon Kinesis]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Kinesis].

![](../../../../images/tutorials/create/kinesis/catalog.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Connect to Amazon Kinesis]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New Account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Kinesis]. Al termine, selezionare **[!UICONTROL Connect]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/kinesis/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account [!DNL Kinesis] con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, ti sei connesso al tuo account [!DNL Kinesis] in [!DNL Platform]. È ora possibile continuare l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in  [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).