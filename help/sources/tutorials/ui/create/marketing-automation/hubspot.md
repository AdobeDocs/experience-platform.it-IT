---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente HubSpot nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# Creare un connettore sorgente HubSpot nell’interfaccia utente

> [!NOTE]
> Il connettore HubSpot è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore di origine HubSpot utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base HubSpot, potete ignorare il resto del documento e passare all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/marketing-automation.md)di automazione marketing.

### Raccogli credenziali richieste

Per accedere al tuo account HubSpot sulla piattaforma, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientId` | L&#39;ID client associato all&#39;applicazione HubSpot. |
| `clientSecret` | Il segreto client associato all’applicazione HubSpot. |
| `accessToken` | Token di accesso ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |
| `refreshToken` | Token di aggiornamento ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |

Per ulteriori informazioni su come iniziare, consulta questo documento [](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)HubSpot.

## Collegare l&#39;account HubSpot

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in ingresso per collegare il tuo account HubSpot alla piattaforma.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *Automazione* marketing, selezionate **HubSpot** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionate l&#39;origine **** Connect.

![catalogo](../../../../images/tutorials/create/hubspot/catalog.png)

Viene visualizzata la pagina *Connetti a HubSpot* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, fornite alla connessione di base un nome, una descrizione facoltativa e le credenziali HubSpot. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione di base.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account HubSpot con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![esistenti](../../../../images/tutorials/create/hubspot/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione di base al tuo account HubSpot. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati del sistema di automazione di marketing nella piattaforma](../../dataflow/marketing-automation.md).