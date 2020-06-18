---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine PayPal nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Creare un connettore di origine PayPal nell&#39;interfaccia utente

> [!NOTE]
> Il connettore PayPal è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per creare un connettore di origine PayPal utilizzando l&#39;interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base PayPal, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli credenziali richieste

Per accedere al tuo account PayPal Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | L&#39;URL dell&#39;istanza PayPal. |
| `clientID` | L&#39;ID cliente associato all&#39;applicazione PayPal. |
| `clientSecret` | Il segreto cliente associato all&#39;applicazione PayPal. |

Per ulteriori informazioni su come iniziare, consulta questo documento [PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Connessione dell&#39;account PayPal

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in entrata per collegare il tuo account PayPal ad Platform.

Accedete a <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi selezionate **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *CRM* , seleziona **PayPal** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionate l&#39;origine **** Connect.

![catalogo](../../../../images/tutorials/create/paypal/catalog.png)

Viene visualizzata la pagina *Connetti a PayPal* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, fornite alla connessione di base un nome, una descrizione facoltativa e le credenziali PayPal. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione di base.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account PayPal con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![esistenti](../../../../images/tutorials/create/paypal/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione di base al tuo account PayPal. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per l&#39;immissione di dati CRM in Platform](../../dataflow/payments.md).