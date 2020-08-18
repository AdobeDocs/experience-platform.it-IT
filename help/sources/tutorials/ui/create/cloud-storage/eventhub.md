---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Event Hubs nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: dd036cf4df5d772206d2b73292c60f2d866ba0de
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# Creare un connettore [!DNL Azure Event Hubs] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL Azure Event Hubs] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un connettore [!DNL Azure Event Hubs] (in seguito denominato &quot;[!DNL Event Hubs]&quot;) sorgente mediante l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Profilo cliente in tempo reale]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una [!DNL Event Hubs] connessione valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore [!DNL Event Hubs] di origine, è necessario specificare i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La firma di accesso condiviso generata. |
| `namespace` | Lo spazio dei nomi del [!DNL Event Hubs] sito a cui si accede. |

Per ulteriori informazioni su questi valori, fare riferimento a [ [!DNL Event Hubs] questo documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).

## Collegamento dell&#39; [!DNL Event Hubs] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare il vostro [!DNL Event Hubs] account a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** scheda sono visualizzate diverse origini con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Cloud Storage]** categoria, selezionare **[!UICONTROL Azure Event Hubs]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionate **[!UICONTROL Add data]** per creare un nuovo connettore per hub eventi.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Viene visualizzata **[!UICONTROL Connect to Azure Event Hubs]** la finestra di dialogo. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New Account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Event Hubs] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/eventhub/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Event Hubs] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai collegato il tuo [!DNL Event Hubs] account a [!DNL Platform]. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud [!DNL Platform]](../../dataflow/streaming/cloud-storage.md).