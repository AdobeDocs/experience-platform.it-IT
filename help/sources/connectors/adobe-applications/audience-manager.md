---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: 75c446aed75100bd2b5b4a3d365c090cb01dcc69

---


# Connettore Audience Manager

Il connettore dati di Adobe Audience Manager trasferisce i dati di prime parti raccolti in Adobe Audience Manager in Adobe Experience Platform. Il connettore di Audience Manager consente di acquisire tre categorie di dati sulla piattaforma:

- **Dati in tempo reale:** Dati acquisiti in tempo reale sul server di raccolta dati di Audience Manager. Questi dati vengono utilizzati in Audience Manager per popolare caratteristiche basate su regole e verranno visualizzati in Piattaforma nel tempo di latenza più breve.
- **Dati caricati (in entrata):** Si tratta dei file caricati da un utente in una posizione Amazon S3 ospitata da Audience Manager. Audience Manager utilizza questi dati per compilare i tratti caricati utilizzando il metodo file in entrata e avrà una certa latenza.
- **Dati profilo:** Audience Manager utilizza dati in tempo reale e caricati per derivare i profili dei clienti. Questi profili vengono utilizzati per compilare grafici identità e caratteristiche sulle realizzazioni dei segmenti.

Il connettore di Audience Manager mappa queste categorie di dati sullo schema Experience Data Model (XDM) e le invia alla piattaforma. I dati in tempo reale e quelli caricati vengono inviati come dati XDM ExperienceEvent, mentre i dati di profilo vengono inviati come profili XDM singoli.

Per istruzioni su come creare una connessione con Adobe Audience Manager utilizzando l&#39;interfaccia utente della piattaforma, consulta l&#39;esercitazione [sui connettori di](../../tutorials/ui/create/adobe-applications/audience-manager.md)Audience Manager.

## Cos&#39;è Experience Data Model (XDM)?

XDM è una specifica documentata pubblicamente che fornisce un framework standardizzato tramite il quale la piattaforma organizza i dati relativi all&#39;esperienza cliente.

Il rispetto degli standard XDM consente di incorporare uniformemente i dati sull&#39;esperienza dei clienti, semplificando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni sull&#39;utilizzo di XDM in Experience Platform, consultate la panoramica [di sistema](../../../xdm/home.md)XDM. Per ulteriori informazioni sulla struttura degli schemi XDM come Profile e ExperienceEvent, consulta le [nozioni di base della composizione](../../../xdm/schema/composition.md)dello schema.

## Esempi di schemi XDM

Di seguito sono riportati alcuni esempi della struttura di Audience Manager mappata su XDM ExperienceEvent e XDM Singolo profilo nella piattaforma.

### ExperienceEvent - per dati in tempo reale e dati caricati

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Profilo singolo XDM - per i dati di profilo

![](images/aam-profile-xdm-for-profile-data.png)

## Come vengono mappati i campi da Adobe Audience Manager a XDM?

Per ulteriori informazioni, consulta la documentazione relativa ai campi [di mappatura di](./mapping/audience-manager.md) Audience Manager.

## Gestione dei dati sulla piattaforma

### Set di dati

I set di dati sono un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene schema (colonne) e campi (righe) ed è resa disponibile da una connessione dati. I dati di Audience Manager sono costituiti da dati in tempo reale, dati in entrata e dati di profilo. Per individuare i set di dati di Audience Manager, utilizzate la funzione di ricerca nell’interfaccia utente con le convenzioni di denominazione fornite per ciascun tipo di dati.

Sebbene gli utenti siano in grado di disabilitare i set di dati, non è consigliabile disabilitare i set di dati che verranno utilizzati per l&#39;appartenenza al segmento in Profile.

| Nome set di dati | Descrizione |
| ------------ | ----------- |
| Tempo reale di Audience Manager | Questo set di dati contiene i dati raccolti dagli hit diretti sugli endpoint DCS di Audience Manager e le mappe di identità per i profili Audience Manager. Mantieni questo set di dati abilitato per l’assimilazione del profilo. |
| Aggiornamenti dei profili in tempo reale di Audience Manager | Questo set di dati consente il targeting in tempo reale di caratteristiche e segmenti di Audience Manager. Include informazioni per l’instradamento, la caratteristica e l’appartenenza al segmento regionale Edge. Mantieni questo set di dati abilitato per l’assimilazione del profilo. |
| Dati dispositivi Audience Manager | Dati dispositivo con ECID e corrispondenti realizzazioni di segmenti aggregate in Audience Manager. |
| Dati profilo dispositivo Audience Manager | Utilizzata per la diagnostica dei connettori di Audience Manager. |
| Profili autenticati di Audience Manager | Questo set di dati contiene i profili autenticati di Audience Manager. |
| Metadati profili autenticati di Audience Manager | Utilizzata per la diagnostica del connettore Audience Manager. |
| ID origine dati {DataSource} in ingresso di Audience Manager **(obsoleto)** | Questo set di dati rappresenta i record caricati in Audience Manager tramite il metodo file in ingresso. Questo flusso di dati è obsoleto e verrà rimosso in una versione successiva. |
| Metadati In Entrata Di Audience Manager **(Obsoleto)** | Utilizzata per la diagnostica dei connettori di Audience Manager. Questo flusso di dati è obsoleto e verrà rimosso in una versione successiva. |

### Connessioni

Adobe Audience Manager crea una connessione in Catalog: **Audience Manager Connection**. Catalog è il sistema di record per la posizione dei dati e la linea di demarcazione all&#39;interno di Adobe Experience Platform. Una connessione è un oggetto Catalog che è un&#39;istanza specifica del cliente dei connettori. Per ulteriori informazioni su Catalogo, connessioni e connettori, consultate la panoramica [Servizio](../../../catalog/home.md) catalogo.

## Qual è la latenza prevista per i dati di Audience Manager sulla piattaforma?

| Dati Audience Manager | Latenza | Note |
| --- | --- | --- |
| Dati in tempo reale | &lt; 35 minuti. | Tempo di acquisizione al nodo Realtime per la visualizzazione sul lago di dati della piattaforma. |
| Dati in entrata | &lt; 13 ore | Il tempo da essere catturato ai secchi S3 a comparire su Platform Data Lake. |
| Dati profilo | &lt; 2 giorni | Tempo di acquisizione dai dati in tempo reale/in ingresso per l&#39;aggiunta a un profilo utente e infine la visualizzazione sul lago di dati della piattaforma. |