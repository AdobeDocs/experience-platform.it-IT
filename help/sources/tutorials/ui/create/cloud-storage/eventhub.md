---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Azure Event Hubs nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 1eb6883ec9b78e5d4398bb762bba05a61c0f8308
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---


# Creare un connettore di origine Azure Event Hubs nell&#39;interfaccia utente

>[!NOTE]
> Il connettore Azure Event Hubs è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per l&#39;autenticazione di un connettore di origine di Azure Event Hubs (in seguito denominato &quot;EventHub&quot;) tramite l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di un account EventHub, potete ignorare il resto del documento e passare all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/streaming/cloud-storage.md).

### Raccogli credenziali richieste

Per autenticare il connettore di origine EventHub, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `sasKeyName` | Nome della regola di autorizzazione, noto anche come nome della chiave SAS. |
| `sasKey` | La firma di accesso condiviso generata. |
| `namespace` | Spazio dei nomi dell’EventHub a cui si accede. |

Per ulteriori informazioni su questi valori, consultate [questo documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)EventHub.

## Connessione dell’account EventHub

Dopo aver raccolto le credenziali richieste, potete seguire i passaggi descritti di seguito per collegare l&#39;account EventHub alla piattaforma.

Accedi ad [Adobe Experience Platform](https://platform.adobe.com) , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella scheda *Catalogo* sono visualizzate diverse origini per le quali è possibile connettersi a Piattaforma. Ogni origine mostra il numero di account esistenti ad essi associati.

Nella categoria Archiviazione ** cloud, selezionate Hubs **evento di** Azure e fate clic **sull&#39;icona + (+)** per creare un nuovo connettore EventHub.

![](../../../../images/tutorials/create/eventhub/catalog.png)

Viene visualizzata la finestra di dialogo *Connetti agli hub* eventi di Azure. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se state utilizzando nuove credenziali, selezionate **Nuovo account**. Nel modulo di input visualizzato, fornite un nome, una descrizione facoltativa e le credenziali EventHub. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/eventhub/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account EventHub con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai collegato il tuo account EventHub a Platform. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud alla piattaforma](../../dataflow/streaming/cloud-storage.md).