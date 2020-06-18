---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Google AdWords nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: b9e9207741044f118d53ab8eb3d3d6cd7451132d
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Creare un connettore sorgente Google AdWords nell’interfaccia utente

>[!NOTE]
>Il connettore Google AdWords è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in  Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente Google AdWords tramite l&#39;interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una conoscenza approfondita dei seguenti componenti del  Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione Google AdWords, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli credenziali richieste

Per accedere all&#39;account Platform di Google AdWords, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientCustomerId` | L&#39;ID cliente client dell&#39;account AdWords. |
| `developerToken` | Token sviluppatore associato all&#39;account manager. |
| `refreshToken` | Token di aggiornamento ottenuto da Google per autorizzare l&#39;accesso ad AdWords. |
| `clientId` | L&#39;ID client dell&#39;applicazione Google utilizzata per acquisire il token di aggiornamento. |
| `clientSecret` | Il segreto client dell’applicazione Google utilizzata per acquisire il token di aggiornamento. |

Per ulteriori informazioni su come iniziare, consulta questo documento [](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

## Connetti il tuo account Google AdWords

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in ingresso per collegare il tuo account Google AdWords ad Platform.

Accedete a [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *Pubblicità* , selezionate **Google AdWords** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionate l&#39;origine **** Connect.

![catalogo](../../../../images/tutorials/create/ads/catalog.png)

Viene visualizzata la pagina *Connetti a Google AdWords* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, specifica la connessione di base con un nome, una descrizione facoltativa e le tue credenziali Google AdWords. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per stabilire la nuova connessione di base.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Account esistente

Per collegare un account esistente, seleziona l&#39;account Google AdWords con cui vuoi connetterti, quindi seleziona **Avanti** per continuare.

![esistenti](../../../../images/tutorials/create/ads/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione di base al tuo account Google AdWords. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per l&#39;inserimento di dati pubblicitari in Platform](../../dataflow/advertising.md).