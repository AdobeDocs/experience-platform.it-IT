---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Microsoft SQL Server nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 75ba0bce7ce070af851bbf7e220dbf08febc4c20
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---


# Creare un connettore di origine Microsoft SQL Server nell&#39;interfaccia utente

> [!NOTE]
> Il connettore di Microsoft SQL Server è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore di origine Microsoft SQL Server (di seguito &quot;SQL Server&quot;) tramite l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione di base di SQL Server, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per connettersi a SQL Server sulla piattaforma, è necessario specificare la seguente proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione associata all&#39;account SQL Server. Il pattern della stringa di connessione di SQL Server è: `Data Source={SERVER_NAME}\\<{INSTANCE_NAME} if using named instance>;Initial Catalog={DATABASE};Integrated Security=False;User ID={USERNAME};Password={PASSWORD};`. |

Per ulteriori informazioni sull&#39;utilizzo di SQL Server, consultate [questo documento](https://docs.microsoft.com/en-us/dotnet/framework/data/adonet/sql/authentication-in-sql-server) .

## Connessione dell&#39;account SQL Server

Dopo aver raccolto le credenziali richieste, è possibile seguire i passaggi descritti di seguito per creare una nuova connessione di base in entrata per collegare l&#39;account SQL Server alla piattaforma.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *Database* , selezionare **Microsoft SQL Server** per visualizzare una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionate l&#39;origine **** Connect.

![](../../../../images/tutorials/create/microsoft-sql-server/catalog.png)

Viene visualizzata la pagina *Connetti a Microsoft SQL Server* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, fornite alla connessione di base un nome, una descrizione facoltativa e le credenziali di SQL Server. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione di base.

![](../../../../images/tutorials/create/microsoft-sql-server/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account SQL Server con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![](../../../../images/tutorials/create/microsoft-sql-server/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione di base all&#39;account SQL Server. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/databases.md).