---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine PayPal nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 1%

---


# Creare un connettore [!DNL PayPal] sorgente nell’interfaccia utente

> [!NOTE]
> Il [!DNL PayPal] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL PayPal] sorgente utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione di [!DNL PayPal] base, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli credenziali richieste

Per accedere al tuo [!DNL PayPal] account [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | L’URL dell’ [!DNL PayPal] istanza. |
| `clientID` | L&#39;ID client associato all&#39; [!DNL PayPal] applicazione. |
| `clientSecret` | Il segreto client associato all&#39; [!DNL PayPal] applicazione. |

Per ulteriori informazioni su come iniziare, consulta questo documento [PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Collegamento dell&#39; [!DNL PayPal] account

Dopo aver raccolto le credenziali richieste, è possibile seguire i passaggi descritti di seguito per creare una nuova connessione di base in entrata a cui collegare l&#39; [!DNL PayPal] account [!DNL Platform].

Accedete a <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. La *[!UICONTROL Catalog]* schermata mostra una serie di origini con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Sotto la *[!UICONTROL CRM]* categoria, selezionate **[!UICONTROL PayPal]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionare **[!UICONTROL Connect source]**.

![catalogo](../../../../images/tutorials/create/paypal/catalog.png)

Viene *[!UICONTROL Connect to PayPal]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input che viene visualizzato, fornire alla connessione di base un nome, una descrizione facoltativa e [!DNL PayPal] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione di base.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL PayPal] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/paypal/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione di base all&#39; [!DNL PayPal] account. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per l&#39;immissione di dati CRM in Platform](../../dataflow/payments.md).