---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Connettore Audience Manager '
topic: overview
translation-type: tm+mt
source-git-commit: a1b09f3e88e489f1b0ec0c1fcb72a2a5a4356d87
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---


# Connettore Audience Manager 

Il connettore dati Adobe Audience Manager trasferisce in Adobe Experience Platform i dati di prime parti raccolti in Adobe Audience Manager. Il connettore del Audience Manager  acquisisce tre categorie di dati sulla piattaforma:

- **Dati in tempo reale:** Dati acquisiti in tempo reale  server  raccolta dati. Questi dati vengono utilizzati in  Audience Manager per popolare caratteristiche basate su regole e verranno visualizzati in Piattaforma nel tempo di latenza più breve.
- **Dati profilo:**  Audience Manager utilizza dati in tempo reale e caricati per derivare i profili dei clienti. Questi profili vengono utilizzati per compilare grafici identità e caratteristiche sulle realizzazioni dei segmenti.

Il connettore  Audience Manager mappa queste categorie di dati sullo schema Experience Data Model (XDM) e le invia alla piattaforma. I dati in tempo reale vengono inviati come dati XDM ExperienceEvent, mentre i dati del profilo vengono inviati come profili XDM singoli.

Per istruzioni su come creare una connessione con Adobe Audience Manager utilizzando l&#39;interfaccia utente della piattaforma, vedere l&#39;esercitazione [sui connettori di Audience Manager](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Cos&#39;è Experience Data Model (XDM)?

XDM è una specifica documentata pubblicamente che fornisce un framework standardizzato tramite il quale la piattaforma organizza i dati relativi all&#39;esperienza cliente.

Il rispetto degli standard XDM consente di incorporare uniformemente i dati sull&#39;esperienza dei clienti, semplificando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni sull&#39;utilizzo di XDM in  Experience Platform, vedere la panoramica [del sistema](../../../xdm/home.md)XDM. Per ulteriori informazioni sulla struttura degli schemi XDM come Profile e ExperienceEvent, consulta le [nozioni di base della composizione](../../../xdm/schema/composition.md)dello schema.

## Esempi di schemi XDM

Di seguito sono riportati alcuni esempi della struttura del Audience Manager  mappato su XDM ExperienceEvent e XDM Individuale Profile in Platform (Profilo singolo XDM).

### ExperienceEvent - per dati in tempo reale e dati caricati

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Profilo singolo XDM - per i dati di profilo

![](images/aam-profile-xdm-for-profile-data.png)

## Come vengono mappati i campi da Adobe Audience Manager a XDM?

Per ulteriori informazioni, consulta la documentazione relativa ai campi [di mappatura](./mapping/audience-manager.md) Audience Manager.

## Gestione dei dati sulla piattaforma

### Set di dati

I set di dati sono un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene schema (colonne) e campi (righe) ed è resa disponibile da una connessione dati.  dati di Audience Manager sono costituiti da dati in tempo reale, dati in entrata e dati di profilo. Per individuare i set di dati  Audience Manager, utilizzate la funzione di ricerca nell’interfaccia utente con le convenzioni di denominazione fornite per ciascun tipo di dati.

 set di dati di Audience Manager sono disattivati per impostazione predefinita per il profilo e gli utenti possono attivare o disattivare i set di dati in base ai casi di utilizzo. Non è consigliabile disabilitare i set di dati che verranno utilizzati per l&#39;appartenenza al segmento in Profile.

| Nome set di dati | Descrizione |
| ------------ | ----------- |
|  Audience Manager | Questo set di dati contiene i dati raccolti dagli hit diretti sugli endpoint DCS  Audience Manager e le mappe di identità per i profili  Audience Manager. Mantieni questo set di dati abilitato per l’assimilazione del profilo. |
|  Audience Manager Aggiornamenti dei profili in tempo reale | Questo set di dati consente il targeting in tempo reale di caratteristiche e segmenti  Audience Manager. Include informazioni per l’instradamento, la caratteristica e l’appartenenza al segmento regionale Edge. Mantieni questo set di dati abilitato per l’assimilazione del profilo. |
| Dati sui dispositivi  Audience Manager | Dati dispositivo con ECID e corrispondenti realizzazioni segmenti aggregate in  Audience Manager. |
| Dati profilo dispositivo Audience Manager  | Utilizzato per  diagnostica connettore Audience Manager. |
| Profili di autenticazione Audience Manager  | Questo set di dati contiene  profili autenticati di Audience Manager. |
|  Audience Manager Metadati Profili autenticati | Utilizzato per  diagnostica del connettore Audience Manager. |

### Connessioni

Adobe Audience Manager crea una connessione in Catalog: **connessione** Audience Manager. Catalog è il sistema dei record per la posizione dei dati e la linea di dati in Adobe Experience Platform. Una connessione è un oggetto Catalog che è un&#39;istanza specifica del cliente dei connettori. Per ulteriori informazioni su Catalogo, connessioni e connettori, consultate la panoramica [Servizio](../../../catalog/home.md) catalogo.

## Qual è la latenza prevista per i dati  Audience Manager sulla piattaforma?

| Dati Audience Manager  | Latenza | Note |
| --- | --- | --- |
| Dati in tempo reale | &lt; 35 minuti. | Tempo di acquisizione al nodo Realtime per la visualizzazione sul lago di dati della piattaforma. |
| Dati in entrata | &lt; 13 ore | Il tempo da essere catturato ai secchi S3 a comparire su Platform Data Lake. |
| Dati profilo | &lt; 2 giorni | Tempo di acquisizione dai dati in tempo reale/in ingresso per l&#39;aggiunta a un profilo utente e infine la visualizzazione sul lago di dati della piattaforma. |