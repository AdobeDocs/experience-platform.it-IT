---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente OData generico nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# Creare un connettore [!DNL Generic OData] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL Generic OData] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente generico Open Data Protocol (in seguito denominato &quot;OData&quot;) tramite l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione OData valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dataset di protocolli](../../dataflow/protocols.md)

### Raccogli credenziali richieste

Per accedere al tuo [!DNL OData] account in [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | URL principale del [!DNL OData] servizio. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://www.odata.org/getting-started/basic-tutorial/)OData.

## Collegamento dell&#39; [!DNL OData] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per creare un nuovo [!DNL OData] account a cui collegarvi [!DNL Platform].

Accedete a <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse sorgenti per le quali è possibile creare un account in ingresso. Ciascuna origine mostra il numero di conti e flussi di dati esistenti ad essi associati.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Protocols]* categoria, selezionate **[!UICONTROL Generic OData]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione in entrata, selezionare **[!UICONTROL Connect source]**.

![catalogo](../../../../images/tutorials/create/odata/catalog.png)

Viene *[!UICONTROL Connect to Generic OData]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL OData] le credenziali per la connessione. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL OData] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/odata/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL OData] account. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dataset per portare i dati dei protocolli in Platform](../../dataflow/protocols.md).