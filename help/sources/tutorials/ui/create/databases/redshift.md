---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Amazon Redshift nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---


# Creare un connettore [!DNL Amazon Redshift] sorgente nell’interfaccia utente

>Le selezioni del menu [!NOTE]
>Il [!DNL Amazon Redshift] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL Amazon Redshift] (in seguito denominato &quot;[!DNL Redshift]&quot;) sorgente utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione di [!DNL Redshift] base, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Redshift] account su [!DNL Platform], devi fornire i seguenti valori:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Server associato al tuo [!DNL Redshift] account. |
| `username` | Nome utente associato al tuo [!DNL Redshift] account. |
| `password` | La password associata al tuo [!DNL Redshift] account. |
| `database` | Il [!DNL Redshift] database a cui si accede. |

Per ulteriori informazioni su come iniziare, consultare [questo documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html)Redshift.

## Collegamento dell&#39; [!DNL Redshift] account

Dopo aver raccolto le credenziali richieste, è possibile seguire i passaggi descritti di seguito per creare una nuova connessione di base in entrata a cui collegare l&#39; [!DNL Redshift] account [!DNL Platform].

Accedete a <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. La *[!UICONTROL Catalog]* schermata mostra una serie di origini con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Sotto la *[!UICONTROL Databases]* categoria, selezionate **[!UICONTROL Amazon Redshift]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionare **[!UICONTROL Connect source]**.

![](../../../../images/tutorials/create/redshift/catalog.png)

Viene *[!UICONTROL Connect to Amazon Redshift]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input che viene visualizzato, fornire alla connessione di base un nome, una descrizione facoltativa e [!DNL Redshift] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione di base.

![](../../../../images/tutorials/create/redshift/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Redshift] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/redshift/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione di base all&#39; [!DNL Redshift] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati in Platform](../../dataflow/databases.md).