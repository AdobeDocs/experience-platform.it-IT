---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente GreenPlum nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---


# Creare un connettore sorgente GreenPlum nell’interfaccia utente

> [!NOTE]
> Il connettore GreenPlum è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente GreenPlum utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione GreenPlum valida, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per collegarsi con successo a GreenPlum tramite l&#39;API del servizio di flusso.

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per connettersi all&#39;istanza GreenPlum. Il pattern della stringa di connessione per GreenPlum è `HOST=<server>;PORT=<port>;DB=<database>;UID=<user name>;PWD=<password>` |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)GreenPlum.

## Collegamento dell&#39;account GreenPlum

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare un nuovo account GreenPlum per la connessione alla piattaforma.

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare un account in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, selezionare **[!UICONTROL GreenPlum]** fare clic **sull&#39;icona + (+)** per creare un nuovo connettore GreenPlum.

![catalogo](../../../../images/tutorials/create/greenplum/catalog.png)

Viene *[!UICONTROL Connect to GreenPlum]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali di GreenPlum. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account GreenPlum con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo superiore destro per proseguire.

![esistenti](../../../../images/tutorials/create/greenplum/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account GreenPlum. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/databases.md).