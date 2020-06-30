---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Event Hubs nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 1%

---


# Creare un connettore [!DNL Azure Event Hubs] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL Azure Event Hubs] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un connettore [!DNL Azure Event Hubs] (in seguito denominato &quot;[!DNL Event Hubs]&quot;) sorgente mediante l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di un [!DNL Event Hubs] account, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore [!DNL Event Hubs] di origine, è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La firma di accesso condiviso generata. |
| `namespace` | Lo spazio dei nomi del [!DNL Event Hubs] sito a cui si accede. |

Per ulteriori informazioni su questi valori, consultate [questo documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)sugli hub eventi.

## Collegamento dell&#39; [!DNL Event Hubs] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare il vostro [!DNL Event Hubs] account a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella *[!UICONTROL Catalog]* scheda sono visualizzate diverse sorgenti alle quali è possibile connettersi [!DNL Platform]. Ogni origine mostra il numero di account esistenti ad essi associati.

Sotto la *[!UICONTROL Cloud Storage]* categoria, selezionate **[!UICONTROL Azure Event Hubs]** e fate clic **sull&#39;icona + (+)** per creare un nuovo connettore per hub eventi.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Viene visualizzata *[!UICONTROL Connect to Azure Event Hubs]* la finestra di dialogo. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New Account]**. Nel modulo di input visualizzato, fornite un nome, una descrizione facoltativa e le credenziali per gli hub eventi. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/eventhub/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account Hubs evento con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, avete collegato il vostro account Hubs evento a [!DNL Platform]. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud ad Platform](../../dataflow/streaming/cloud-storage.md).