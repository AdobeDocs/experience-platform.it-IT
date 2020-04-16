---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Microsoft Dynamics o Salesforce nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# Creare un connettore sorgente Microsoft Dynamics o Salesforce nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di acquisire dati CRM di origine esterna su base programmata. Questa esercitazione fornisce passaggi per la creazione di un connettore di origine Microsoft Dynamics (di seguito denominato &quot;Dynamics&quot;) o Salesforce tramite l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base di Microsoft Dynamics o Salesforce, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

Per accedere al tuo account Dynamics sulla piattaforma, devi fornire un URI **** Service, un **nome utente** e una **password**.

Allo stesso modo, per accedere al tuo account Salesforce sulla piattaforma è necessario fornire un URL **** ambiente, **nome utente**, **password** e token **di** sicurezza.

## Collegamento dell&#39;account Dynamics o Salesforce

Con le credenziali del sistema CRM in uso, puoi seguire i passaggi descritti di seguito per creare una nuova connessione di base in ingresso per collegare il tuo account Dynamics o Salesforce alla piattaforma.

Accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> , quindi seleziona **Origini** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro delle origini. Nella schermata *Catalogo* sono visualizzate diverse sorgenti con cui è possibile creare connessioni di base in entrata e ogni origine mostra il numero di connessioni di base esistenti ad esse associate.

Nella categoria *CRM* , seleziona **Microsoft Dynamics** o **Salesforce** per esporre una barra delle informazioni sul lato destro dello schermo. La barra delle informazioni fornisce una breve descrizione dell’origine selezionata e delle opzioni per visualizzarne la documentazione o per collegarsi all’origine. Per creare una nuova connessione di base in entrata, fate clic su **Connetti sorgente**.

![](../../../../images/tutorials/create/salesforce/sf_sources_catalog.png)

Nel modulo di input, fornisci alla connessione di base un nome, una descrizione facoltativa e le tue credenziali Dynamics o Salesforce. Infine, fate clic su **Connect** , quindi lasciate che sia possibile stabilire una nuova connessione di base.

![](../../../../images/tutorials/create/salesforce/sf_credentials.png)

Una volta stabilita una connessione di base con il sistema CRM, puoi continuare con la sezione successiva e configurare un flusso di dati per l&#39;inserimento di dati CRM in Platform.

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione di base all&#39;account Dynamics o Salesforce. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/crm.md).