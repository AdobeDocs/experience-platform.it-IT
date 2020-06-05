---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine ServiceNow nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 75ba0bce7ce070af851bbf7e220dbf08febc4c20
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---


# Creare un connettore di origine ServiceNow nell&#39;interfaccia utente

>[!NOTE]
>Il connettore ServiceNow è in versione beta. Le funzioni e la documentazione sono soggette a modifiche.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore di origine ServiceNow utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione ServiceNow, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/customer-success.md)

### Raccogli credenziali richieste

Per accedere al tuo account ServiceNow su Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `endpoint` | Endpoint del server ServiceNow. |
| `username` | Il nome utente utilizzato per connettersi al server ServiceNow per l&#39;autenticazione. |
| `password` | La password per connettersi al server ServiceNow per l&#39;autenticazione. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)ServiceNow.

## Connessione dell&#39;account ServiceNow

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per creare un nuovo account ServiceNow da connettere alla piattaforma.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro *Origini* . Nella schermata *Catalogo* sono visualizzate diverse origini per le quali è possibile creare un account e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Nella categoria *Customer Success* (Successo **cliente), selezionate** ServiceNowper esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione della sorgente selezionata e le opzioni per collegarsi alla sorgente o visualizzare la documentazione. Per creare un nuovo account, selezionate l&#39;origine **** Connect.

![](../../../../images/tutorials/create/servicenow/catalog.png)

Viene visualizzata la pagina *Connetti a ServiceNow* . In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **Nuovo account**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali di ServiceNow. Al termine, selezionate **Connect** , quindi concedete un po&#39; di tempo per la creazione del nuovo account.

![](../../../../images/tutorials/create/servicenow/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account ServiceNow con cui desiderate connettervi, quindi selezionate **Avanti** per continuare.

![](../../../../images/tutorials/create/servicenow/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account ServiceNow. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/customer-success.md).
