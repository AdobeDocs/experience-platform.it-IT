---
title: Crittografia dei dati in Adobe Experience Platform
topic-legacy: data protection
description: Scopri come i dati vengono crittografati in transito e nel resto in Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 0a01dd2b0d8a1039178e3593475f9a87639ccdcd
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 5%

---

# Crittografia dei dati in Adobe Experience Platform

Adobe Experience Platform è un sistema potente ed estensibile che centralizza e standardizza i dati sulla customer experience tra le soluzioni aziendali. Tutti i dati utilizzati da Platform sono crittografati durante il transito e a riposo per proteggere i tuoi dati. Questo documento descrive i processi di crittografia di Platform ad alto livello.

Il diagramma di flusso del processo seguente illustra il modo in cui i dati vengono acquisiti, crittografati e mantenuti da [!DNL Experience Platform]:

![](../images/governance-privacy-security/encryption/flow.png)

## Dati in transito {#in-transit}

Tutti i dati in transito tra Platform e qualsiasi componente esterno vengono eseguiti tramite connessioni protette e crittografate tramite HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

In generale, i dati vengono inseriti in Platform in tre modi:

* [Raccolta dati](../../rtcdp-connections/home.md) Le funzionalità consentono a siti web e applicazioni mobili di inviare dati a Platform Edge Network per la gestione temporanea e la preparazione all’acquisizione.
* [Connettori sorgente](../../sources/home.md) i dati vengono inviati direttamente a Platform dalle applicazioni Adobe Experience Cloud e da altre origini dati aziendali.
* Gli strumenti ETL non di Adobe (estrazione, trasformazione, caricamento) inviano i dati al [API di acquisizione batch](../../ingestion/batch-ingestion/overview.md) per il consumo.

Una volta inseriti i dati nel sistema e [criptato a riposo](#at-rest), può quindi essere arricchito dai servizi Platform e portato fuori dal sistema nei seguenti modi:

* [Destinazioni](../../destinations/home.md) consente di attivare i dati nelle applicazioni Adobe e nelle applicazioni partner.
* Applicazioni native per la piattaforma come [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it) può anche utilizzare i dati.

## Dati a riposo {#at-rest}

I dati acquisiti e utilizzati da Platform vengono memorizzati nel data lake, un archivio dati altamente granulare contenente tutti i dati gestiti dal sistema, indipendentemente dall’origine o dal formato del file. Tutti i dati persistenti nel data lake sono crittografati, memorizzati e gestiti in un [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) istanza univoca per la tua organizzazione.

Per informazioni dettagliate sul modo in cui i dati a riposo vengono crittografati nel database Azure Data Lake Storage e Cosmos, consulta la sezione [documentazione ufficiale di Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello del modo in cui i dati vengono crittografati in Platform. Per ulteriori informazioni sulle procedure di sicurezza in Platform, consulta la panoramica su [governance, privacy e sicurezza](./overview.md) ad Experience League, oppure dai un&#39;occhiata al [Whitepaper sulla sicurezza della piattaforma](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
