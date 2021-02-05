---
keywords: ' Experience Platform;home;argomenti popolari;Azure Table Storage;azol table storage;ats;ATS'
solution: Experience Platform
title: Creazione di una connessione di Azure Table Storage Source nell'interfaccia utente
topic: overview
type: Tutorial
description: Informazioni su come creare una connessione di origine Azure Table Storage utilizzando l'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Azure Table Storage] nell&#39;interfaccia utente

>[!NOTE]
>
>Il connettore [!DNL Azure Table Storage] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce passaggi per la creazione di un connettore sorgente [!DNL Azure Table Storage] (in seguito denominato &quot;ATS&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione ATS valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account ATS su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione per la connessione all&#39;istanza [!DNL Azure Table Storage]. Stringa di connessione per la connessione all&#39;istanza ATS. Il pattern della stringa di connessione per ATS è `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |

Per ulteriori informazioni su come iniziare, fare riferimento a [this [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

## Collegare l&#39;account [!DNL Azure Table Storage]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per collegare il tuo account ATS a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Azure Table Storage]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore ATS.

![catalogo](../../../../images/tutorials/create/ats/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Azure Table Storage]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali ATS. Al termine, selezionare **[!UICONTROL Connect]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ats/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account ATS con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/ats/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account ATS. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per l&#39;inserimento di dati in [!DNL Platform]](../../dataflow/databases.md).