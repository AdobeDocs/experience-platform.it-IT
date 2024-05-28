---
title: Crittografia dei dati in Adobe Experience Platform
description: Scopri come i dati vengono crittografati in transito e a riposo in Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: 4f67df5d3667218c79504535534de57f871b0650
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# Crittografia dei dati in Adobe Experience Platform

Adobe Experience Platform è un sistema potente ed estensibile che centralizza e standardizza i dati sull’esperienza del cliente nelle soluzioni aziendali. Tutti i dati utilizzati da Platform sono crittografati in transito e inattivi per proteggerli. Questo documento descrive i processi di crittografia di Platform ad alto livello.

Il diagramma di flusso seguente illustra il modo in cui Experienci Platform acquisisce, crittografa e salva i dati in modo permanente:

![Un diagramma che illustra il modo in cui i dati vengono acquisiti, crittografati e mantenuti per Experience Platform.](../images/governance-privacy-security/encryption/flow.png)

## Dati in transito {#in-transit}

Tutti i dati in transito tra Platform e qualsiasi componente esterno vengono condotti tramite connessioni sicure e crittografate tramite HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

In generale, i dati vengono inseriti in Platform in tre modi:

- [Raccolta dati](../../collection/home.md) Le funzionalità consentono a siti web e applicazioni mobili di inviare dati all’Edge Network di Platform per la gestione temporanea e la preparazione per l’acquisizione.
- [Connettori sorgente](../../sources/home.md) trasmettono i dati direttamente a Platform da applicazioni Adobe Experience Cloud e altre origini dati aziendali.
- Gli strumenti ETL (Extract, Transform, Load, cioè Estrai, Trasforma, Carica) non di Adobe inviano i dati al [API di acquisizione batch](../../ingestion/batch-ingestion/overview.md) per il consumo.

Dopo che i dati sono stati inseriti nel sistema e [crittografato a riposo](#at-rest), i servizi Platform arricchiscono ed esportano i dati nei modi seguenti:

- [Destinazioni](../../destinations/home.md) consente di attivare i dati per applicazioni Adobe e applicazioni partner.
- Applicazioni della piattaforma nativa come [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home) può anche utilizzare i dati.

### Supporto del protocollo mTLS {#mtls-protocol-support}

È ora possibile utilizzare Mutual Transport Layer Security (mTLS) per garantire una maggiore sicurezza nelle connessioni in uscita al [Destinazione API HTTP](../../destinations/catalog/streaming/http-destination.md) e ADOBE JOURNEY OPTIMIZER [azioni personalizzate](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions). mTLS è un metodo di sicurezza end-to-end per l’autenticazione reciproca che garantisce che entrambe le parti che condividono le informazioni siano chi affermano di essere prima che i dati vengano condivisi. mTLS include un ulteriore passaggio rispetto a TLS, in cui il server richiede anche il certificato del client e lo verifica alla loro fine.

Se vuoi [utilizzare mTLS con le azioni personalizzate di Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) Ad Experience Platform, nei flussi di lavoro di destinazione delle API HTTP, l’indirizzo del server inserito nell’interfaccia utente Azioni cliente di Adobe Journey Optimizer o nell’interfaccia utente Destinazioni deve essere disabilitato per i protocolli TLS e abilitato solo per mTLS. Se il protocollo TLS 1.2 è ancora abilitato su tale endpoint, non viene inviato alcun certificato per l’autenticazione client. Ciò significa che per utilizzare mTLS con questi flussi di lavoro, l’endpoint del server &quot;ricevente&quot; deve essere un mTLS **solo** endpoint di connessione abilitato.

>[!IMPORTANT]
>
>Per attivare mTLS non è necessaria alcuna configurazione aggiuntiva nella destinazione Adobe Journey Optimizer custom action o HTTP API. Questo processo si verifica automaticamente quando viene rilevato un endpoint abilitato per mTLS. Il Nome comune (CN) e i Nomi alternativi dei soggetti (SAN) per ciascun certificato sono disponibili nella documentazione come parte del certificato e possono essere utilizzati come livello aggiuntivo di convalida della proprietà, se lo si desidera.
>
>La RFC 2818, pubblicata nel maggio 2000, depreca l&#39;uso del campo Common Name (CN) nei certificati HTTPS per la verifica del nome del soggetto. Consiglia invece di utilizzare l’estensione &quot;Subject Alternative Name&quot; (SAN) del tipo &quot;dns name&quot;.

### Scarica certificati {#download-certificates}

>[!NOTE]
>
>È tua responsabilità mantenere il certificato pubblico aggiornato. Assicurati di rivedere regolarmente il certificato, in particolare con l’approssimarsi della data di scadenza. Applica un segnalibro a questa pagina per mantenere la copia più recente nell’ambiente.

Se desideri verificare il CN o la SAN per eseguire un’ulteriore convalida di terze parti, puoi scaricare i certificati pertinenti qui:

- [Il certificato pubblico Adobe Journey Optimizer](../images/governance-privacy-security/encryption/AJO-public-certificate.pem)
- [Il certificato pubblico del servizio Destinazioni](../images/governance-privacy-security/encryption/destinations-public-cert.pem).

## Dati a riposo {#at-rest}

I dati acquisiti e utilizzati da Platform vengono memorizzati nel data lake, un archivio di dati altamente granulare contenente tutti i dati gestiti dal sistema, indipendentemente dall’origine o dal formato del file. Tutti i dati persistenti nel data lake vengono crittografati, archiviati e gestiti in un unico [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) un’istanza univoca per la tua organizzazione.

Per informazioni dettagliate sulla modalità di crittografia dei dati inattivi nell&#39;archiviazione di Azure Data Lake, vedere [documentazione ufficiale di Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello sul modo in cui i dati vengono crittografati in Platform. Per ulteriori informazioni sulle procedure di sicurezza in Platform, consulta la panoramica su [governance, privacy e sicurezza](./overview.md) ad Experience League, o dai un&#39;occhiata al [White paper sulla sicurezza della piattaforma](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
