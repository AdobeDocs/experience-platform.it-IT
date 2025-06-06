---
title: Crittografia dei dati in Adobe Experience Platform
description: Scopri come i dati vengono crittografati in transito e a riposo in Adobe Experience Platform.
exl-id: 184b2b2d-8cd7-4299-83f8-f992f585c336
source-git-commit: f6eaba4c0622318ba713c562ba0a4c20bba02338
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Crittografia dei dati in Adobe Experience Platform

Adobe Experience Platform è un sistema potente ed estensibile che centralizza e standardizza i dati sull’esperienza del cliente nelle soluzioni aziendali. Tutti i dati utilizzati da Experience Platform sono crittografati in transito e inattivi per proteggerli. Questo documento descrive i processi di crittografia di Experience Platform ad alto livello.

Il seguente diagramma di flusso del processo illustra come Experience Platform acquisisce, crittografa e salva in modo permanente i dati:

![Diagramma che illustra il modo in cui Experience Platform acquisisce, crittografa e mantiene i dati.](../images/governance-privacy-security/encryption/flow.png)

## Dati in transito {#in-transit}

Tutti i dati in transito tra Experience Platform e qualsiasi componente esterno vengono condotti su connessioni sicure e crittografate utilizzando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

In generale, i dati vengono inseriti in Experience Platform in tre modi:

- Le funzionalità di [Raccolta dati](../../collection/home.md) consentono a siti Web e applicazioni mobili di inviare dati ad Experience Platform Edge Network per la gestione temporanea e la preparazione per l&#39;acquisizione.
- [I connettori Source](../../sources/home.md) inviano dati in streaming direttamente ad Experience Platform dalle applicazioni Adobe Experience Cloud e da altre origini dati aziendali.
- Gli strumenti ETL (Extract, Transform, Load, cioè Estrai, Trasforma, Carica) non Adobe inviano i dati all&#39;[API di acquisizione batch](../../ingestion/batch-ingestion/overview.md) per l&#39;utilizzo.

Dopo che i dati sono stati introdotti nel sistema e [crittografati all&#39;arresto](#at-rest), i servizi Experience Platform arricchiscono ed esportano i dati nei modi seguenti:

- [Le destinazioni](../../destinations/home.md) ti consentono di attivare i dati nelle applicazioni Adobe e nelle applicazioni partner.
- Anche le applicazioni Experience Platform native come [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it) e [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home) possono utilizzare i dati.

### Supporto del protocollo mTLS {#mtls-protocol-support}

È ora possibile utilizzare Mutual Transport Layer Security (mTLS) per garantire una maggiore sicurezza nelle connessioni in uscita alla [destinazione API HTTP](../../destinations/catalog/streaming/http-destination.md) e alle [azioni personalizzate](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/orchestrate-journeys/about-journey-building/using-custom-actions) di Adobe Journey Optimizer. mTLS è un metodo di sicurezza end-to-end per l’autenticazione reciproca che garantisce che entrambe le parti che condividono le informazioni siano chi affermano di essere prima che i dati vengano condivisi. mTLS include un ulteriore passaggio rispetto a TLS, in cui il server richiede anche il certificato del client e lo verifica alla loro fine.

Se desideri [utilizzare mTLS con le azioni personalizzate di Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/configuration/configure-journeys/action-journeys/about-custom-action-configuration) e i flussi di lavoro di destinazione delle API HTTP di Experience Platform, l&#39;indirizzo del server inserito nell&#39;interfaccia utente delle azioni dei clienti di Adobe Journey Optimizer o nell&#39;interfaccia utente delle destinazioni deve avere i protocolli TLS disabilitati e solo mTLS abilitato. Se il protocollo TLS 1.2 è ancora abilitato su tale endpoint, non viene inviato alcun certificato per l’autenticazione client. Ciò significa che per utilizzare mTLS con questi flussi di lavoro, l&#39;endpoint del server &quot;ricevente&quot; deve essere un endpoint di connessione abilitato per mTLS **only**.

>[!IMPORTANT]
>
>Per attivare mTLS non è necessaria alcuna configurazione aggiuntiva nella destinazione Adobe Journey Optimizer custom action o HTTP API. Questo processo si verifica automaticamente quando viene rilevato un endpoint abilitato per mTLS. Il Nome comune (CN) e i Nomi alternativi dei soggetti (SAN) per ciascun certificato sono disponibili nella documentazione come parte del certificato e possono essere utilizzati come livello aggiuntivo di convalida della proprietà, se lo si desidera.
>
>La RFC 2818, pubblicata nel maggio 2000, depreca l&#39;uso del campo Common Name (CN) nei certificati HTTPS per la verifica del nome del soggetto. Consiglia invece di utilizzare l’estensione &quot;Subject Alternative Name&quot; (SAN) del tipo &quot;dns name&quot;.

### Scarica certificati {#download-certificates}

>[!NOTE]
>
>È tua responsabilità verificare che i sistemi utilizzino un certificato pubblico valido. Esamina regolarmente i certificati, soprattutto in base all’approssimarsi della data di scadenza. Utilizza l’API per recuperare e aggiornare i certificati prima della loro scadenza.

Non vengono più forniti collegamenti diretti per il download dei certificati mTLS pubblici. Utilizzare invece l&#39;[endpoint certificato pubblico](../../data-governance/mtls-api/public-certificate-endpoint.md) per recuperare i certificati. Questo è l&#39;unico metodo supportato per accedere ai certificati pubblici correnti. In questo modo puoi ricevere sempre certificati validi e aggiornati per le integrazioni.

Le integrazioni che si basano sulla crittografia basata su certificati devono aggiornare i propri flussi di lavoro per supportare il recupero automatico dei certificati tramite l’API. L’utilizzo di collegamenti statici o aggiornamenti manuali può causare l’utilizzo di certificati scaduti o revocati, con conseguenti integrazioni non riuscite.

#### Automazione del ciclo di vita dei certificati {#certificate-lifecycle-automation}

Adobe ora automatizza il ciclo di vita dei certificati per le integrazioni mTLS per migliorare l’affidabilità e prevenire interruzioni del servizio. I certificati pubblici sono:

- Rilasciato 60 giorni prima della scadenza.
- Revocato 30 giorni prima della scadenza.

Questi intervalli continueranno a essere ridotti in linea con le [linee guida in evoluzione per il forum CA/B](https://www.digicert.com/blog/tls-certificate-lifetimes-will-officially-reduce-to-47-days), che mirano a ridurre la durata dei certificati a un massimo di 47 giorni.

Se in precedenza hai utilizzato collegamenti in questa pagina per scaricare certificati, aggiorna il processo per recuperarli esclusivamente tramite l’API.

## Dati a riposo {#at-rest}

I dati acquisiti e utilizzati da Experience Platform vengono memorizzati nel data lake, un archivio di dati altamente granulare contenente tutti i dati gestiti dal sistema, indipendentemente dall’origine o dal formato del file. Tutti i dati persistenti nel data lake vengono crittografati, archiviati e gestiti in un&#39;istanza [[!DNL Microsoft Azure Data Lake] Storage](https://docs.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction) isolata, univoca per la tua organizzazione.

Per informazioni dettagliate sulla modalità di crittografia dei dati inattivi nell&#39;archiviazione di Azure Data Lake, vedere la [documentazione ufficiale di Azure](https://learn.microsoft.com/en-us/azure/storage/common/storage-service-encryption).

## Passaggi successivi

Questo documento fornisce una panoramica di alto livello sul modo in cui i dati vengono crittografati in Experience Platform. Per ulteriori informazioni sulle procedure di sicurezza in Experience Platform, consulta la panoramica su [governance, privacy e sicurezza](./overview.md) in Experience League oppure consulta il [white paper sulla sicurezza in Experience Platform](https://www.adobe.com/content/dam/cc/en/security/pdfs/AEP_SecurityOverview.pdf).
