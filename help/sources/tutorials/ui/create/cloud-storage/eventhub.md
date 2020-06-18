---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Event Hubs nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 855f543a1cef394d121502f03471a60b97eae256
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---


# Creare un connettore di origine Azure Event Hubs nell&#39;interfaccia utente

>[!NOTE]
> Il connettore Azure Event Hubs è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un connettore di origine di Azure Event Hubs (in seguito denominato &quot;Event Hubs&quot;) tramite l&#39;interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di un account Hubs evento, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore di origine di Event Hubs, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La firma di accesso condiviso generata. |
| `namespace` | Lo spazio dei nomi degli hub eventi a cui si accede. |

Per ulteriori informazioni su questi valori, consultate [questo documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)sugli hub eventi.

## Collegamento dell’account Hubs dell’evento

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare l’account Hubs all’Platform.

Accedete a [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella scheda *Catalogo* sono visualizzate diverse origini per le quali è possibile connettersi ad Platform. Ogni origine mostra il numero di account esistenti ad essi associati.

Nella categoria Archiviazione ** cloud, selezionate Hubs **evento di** Azure e fate clic **sull&#39;icona + (+)** per creare un nuovo connettore Hubs evento.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Viene visualizzata la finestra di dialogo *Connetti agli hub* eventi di Azure. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se state utilizzando nuove credenziali, selezionate **Nuovo account**. Nel modulo di input visualizzato, fornite un nome, una descrizione facoltativa e le credenziali per gli hub eventi. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/eventhub/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account Hubs evento con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, avete collegato il vostro account Hubs evento ad Platform. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud ad Platform](../../dataflow/streaming/cloud-storage.md).