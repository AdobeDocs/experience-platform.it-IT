---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Apache HDFS nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---


# Creare un connettore sorgente [!DNL Apache] HDFS nell’interfaccia utente

>[!NOTE]
>Il connettore [!DNL Apache] HDFS è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in [!DNL Adobe Experience Platform] consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce passaggi per l&#39;autenticazione di un connettore sorgente [!DNL Apache Hadoop Distributed File System] (in seguito denominato &quot;HDFS&quot;) tramite l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di [!DNL Platform]:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione HDFS, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore di origine HDFS, è necessario specificare i valori per la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | L’URL definisce i parametri di autenticazione necessari per la connessione ad HDFS in modo anonimo. Per ulteriori informazioni su come ottenere questo valore, fare riferimento al seguente documento sull&#39;autenticazione [HTTPS per HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Collegamento dell&#39;account HDFS

Dopo aver raccolto le credenziali necessarie, è possibile seguire i passaggi descritti di seguito per creare un nuovo account HDFS a cui connettersi [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare un account in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Cloud storage]* categoria, selezionare **[!UICONTROL Apache HDFS]** seguito **[!UICONTROL Add data]** da per creare un nuovo connettore HDFS.

![catalogo](../../../../images/tutorials/create/hdfs/catalog.png)

Viene *[!UICONTROL Connect to HDFS]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali di archiviazione file. Al termine, selezionate **[!UICONTROL Connect to source]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account HDFS con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/hdfs/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account HDFS. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud alla piattaforma](../../dataflow/batch/cloud-storage.md).