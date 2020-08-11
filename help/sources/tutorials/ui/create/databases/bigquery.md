---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Google Big Query nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 598b29f681ac930a4e1781f7f298608c8344d807
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---


# Creare un connettore [!DNL Google Big Query] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL Google BigQuery] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore sorgente [!DNL Google Big Query] (in seguito denominato &quot;GBQ&quot;) utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base GBQ, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account GBQ su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `project` | L&#39;ID progetto del [!DNL BigQuery] progetto predefinito su cui eseguire la query. |
| `clientID` | Il valore ID utilizzato per generare il token di aggiornamento. |
| `clientSecret` | Il valore segreto utilizzato per generare il token di aggiornamento. |
| `refreshToken` | Token di aggiornamento ottenuto da [!DNL Google] utilizzato per autorizzare l&#39;accesso a [!DNL BigQuery]. |

Per ulteriori informazioni su questi valori, consulta [questo documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing)GBQ.

## Collegamento dell’account GBQ

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in ingresso per collegare il tuo account GBQ a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. La *[!UICONTROL Catalog]* schermata mostra una serie di origini con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Sotto la *[!UICONTROL Databases]* categoria, selezionate **[!UICONTROL Google Big Query]** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare una nuova connessione di base in entrata, selezionare **[!UICONTROL Add data]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

Viene *[!UICONTROL Connect to Google Big Query]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, fornite alla connessione di base un nome, una descrizione facoltativa e le credenziali GBQ. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione di base.

![](../../../../images/tutorials/create/google-big-query/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account GBQ con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/google-big-query/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione di base al tuo account GBQ. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/databases.md).