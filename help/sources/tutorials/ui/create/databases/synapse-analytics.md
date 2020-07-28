---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Analytics  sintonizzazione di Azure nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---


# Creare un connettore [!DNL Azure Synapse Analytics] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL Azure Synapse Analytics] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL Azure Synapse Analytics] (in seguito denominato &quot;[!DNL Synapse]&quot;) sorgente utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione di [!DNL Synapse] base, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Synapse] account su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione associata all&#39; [!DNL Synapse] autenticazione. Il pattern della stringa di [!DNL Synapse] connessione è `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`. |

Per ulteriori informazioni su questo valore, consultare [questo documento](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse)di sintesi.

## Collegamento dell&#39; [!DNL Synapse] account

Dopo aver raccolto le credenziali richieste, è possibile seguire i passaggi descritti di seguito per creare una nuova connessione di base in entrata a cui collegare l&#39; [!DNL Synapse] account [!DNL Platform].

Accedete a <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. La *[!UICONTROL Catalog]* schermata mostra una serie di origini con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Sotto la *[!UICONTROL Databases]* categoria, selezionate **[!UICONTROL Azure Synapse Analytics]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionare **[!UICONTROL Connect source]**.

![](../../../../images/tutorials/create/azure-synapse-analytics/catalog.png)

Viene *[!UICONTROL Connect to Azure Synapse Analytics]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input che viene visualizzato, fornire alla connessione di base un nome, una descrizione facoltativa e [!DNL Synapse] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione di base.

![](../../../../images/tutorials/create/azure-synapse-analytics/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Synapse] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/azure-synapse-analytics/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione di base all&#39; [!DNL Synapse] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati in Platform](../../dataflow/databases.md).