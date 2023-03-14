---
title: Crittografia dei dati in Adobe Experience Platform
description: Scopri come i dati vengono crittografati in transito e a riposo in Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 5%

---

# Crittografia dei dati in Adobe Experience Platform

Adobe Experience Platform è un sistema potente ed estensibile che centralizza e standardizza i dati sull’esperienza del cliente nelle soluzioni aziendali. Tutti i dati utilizzati da Platform sono crittografati in transito e inattivi per proteggerli. Questo documento descrive i processi di crittografia di Platform ad alto livello.

Il seguente diagramma di flusso del processo illustra come i dati vengono acquisiti, crittografati e memorizzati da [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Dati in transito {#in-transit}

Tutti i dati in transito tra Platform e qualsiasi componente esterno vengono condotti tramite connessioni sicure e crittografate tramite HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

In generale, i dati vengono inseriti in Platform in tre modi:

* [Raccolta dati](../../collection/home.md) Le funzionalità consentono a siti web e applicazioni mobili di inviare dati alla rete Edge di Platform per la gestione temporanea e la preparazione per l’acquisizione.
* [Connettori sorgente](../../sources/home.md) trasmettono i dati direttamente a Platform da applicazioni Adobe Experience Cloud e altre origini dati aziendali.
* Gli strumenti ETL (Extract, Transform, Load, cioè Estrai, Trasforma, Carica) non di Adobe inviano i dati al [API di acquisizione batch](../../ingestion/batch-ingestion/overview.md) per il consumo.

Dopo che i dati sono stati inseriti nel sistema e [crittografato a riposo](#at-rest), può quindi essere arricchito dai servizi di Platform e portato fuori dal sistema nei seguenti modi:

* [Destinazioni](../../destinations/home.md) consente di attivare i dati per applicazioni Adobe e applicazioni partner.
* Applicazioni della piattaforma nativa come [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it) può anche utilizzare i dati.

## Dati a riposo {#at-rest}

I dati acquisiti e utilizzati da Platform vengono memorizzati nel data lake, un archivio di dati altamente granulare contenente tutti i dati gestiti dal sistema, indipendentemente dall’origine o dal formato del file. Tutti i dati persistenti nel data lake vengono crittografati, archiviati e gestiti in un unico [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) un’istanza univoca per la tua organizzazione.

Per informazioni dettagliate sulla modalità di crittografia dei dati inattivi nell&#39;archiviazione di Azure Data Lake, vedere [documentazione ufficiale di Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello sul modo in cui i dati vengono crittografati in Platform. Per ulteriori informazioni sulle procedure di sicurezza in Platform, consulta la panoramica su [governance, privacy e sicurezza](./overview.md) ad Experience League, o dai un&#39;occhiata al [White paper sulla sicurezza della piattaforma](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
