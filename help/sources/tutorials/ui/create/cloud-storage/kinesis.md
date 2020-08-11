---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Amazon  Kinesis nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---


# Creare un connettore [!DNL Amazon Kinesis] sorgente nell’interfaccia utente

>[!NOTE]
>Il [!DNL Amazon Kinesis] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un connettore [!DNL Amazon Kinesis] (in seguito denominato [!DNL "Kinesis"]) sorgente mediante l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di un [!DNL Kinesis] account, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore [!DNL Kinesis] di origine, è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `accessKeyId` | ID chiave di accesso per il tuo [!DNL Kinesis] account. |
| `Secret access key` | La chiave di accesso segreta per il tuo [!DNL Kinesis] account. |
| `region` | La regione del server AWS. |

Per ulteriori informazioni su questi valori, consultare [questo documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)Kinesis.

## Collegamento dell&#39; [!DNL Kinesis] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare il vostro [!DNL Kinesis] account a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella scheda *Catalogo* sono visualizzate diverse sorgenti alle quali è possibile connettersi [!DNL Platform]. Ogni origine mostra il numero di account esistenti ad essi associati.

Sotto la *[!UICONTROL Cloud Storage]* categoria, selezionare **[!UICONTROL Amazon Kinesis]** seguito **[!UICONTROL Add data]** da per creare un nuovo [!DNL Kinesis] connettore.

![](../../../../images/tutorials/create/kinesis/catalog.png)

Viene visualizzata *[!UICONTROL Connect to Amazon Kinesis]* la finestra di dialogo. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New Account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Kinesis] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/kinesis/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Kinesis] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, ti sei collegato al tuo [!DNL Kinesis] account a [!DNL Platform]. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud alla piattaforma](../../dataflow/streaming/cloud-storage.md).