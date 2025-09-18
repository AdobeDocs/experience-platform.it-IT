---
title: Ciclo di vita del pubblico in Experience Platform e nelle destinazioni di streaming
description: Scopri come i nomi del pubblico e le mappature di Experience Platform si riflettono nelle piattaforme di destinazione di streaming.
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---


# Ciclo di vita del pubblico nelle destinazioni di streaming

Questa pagina descrive come gli aggiornamenti e le mappature dei nomi del pubblico in Experience Platform vengono sincronizzati con le piattaforme di destinazione di streaming. Quando modifichi i nomi dei tipi di pubblico o rimuovi le mappature dei tipi di pubblico in Experience Platform, il comportamento varia a seconda delle funzionalità della piattaforma di destinazione.

Comprendere queste differenze è importante per gestire le operazioni del ciclo di vita del pubblico e garantire che le piattaforme di destinazione riflettano lo stato attuale dei tipi di pubblico in Experience Platform.

## Comportamento di propagazione del nome del pubblico {#audience-name-propagation}

Quando attivi un pubblico in una destinazione di streaming, il nome del pubblico viene inviato alla destinazione durante l’attivazione iniziale. Tuttavia, il comportamento di aggiornamento del nome del pubblico varia in base alla destinazione:

* **[Destinazioni che supportano gli aggiornamenti dei nomi di pubblico](#name-update-supported)**: se modifichi il nome di un pubblico in Experience Platform, il nome aggiornato si propagherà automaticamente a queste destinazioni.
* **[Destinazioni che non supportano gli aggiornamenti dei nomi di pubblico](#name-update-not-supported)**: se modifichi il nome di un pubblico in Experience Platform, la destinazione continuerà a utilizzare il nome originale dall&#39;attivazione iniziale.

### Destinazioni che supportano gli aggiornamenti dei nomi dei tipi di pubblico {#name-update-supported}

Le seguenti destinazioni di streaming supportano gli aggiornamenti automatici dei nomi del pubblico quando si modificano i nomi del pubblico in Experience Platform:

* [Acxiom Audience Connection](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Persone Demandbase](../catalog/advertising/demandbase-people.md)
* [Experience Cloud Audiences](../catalog/adobe/experience-cloud-audiences.md)
* [Pubblico personalizzato Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [(Aziende) LinkedIn Pubblico Corrispondente](../catalog/social/linkedin-b2b.md)
* [Pubblico di LinkedIn corrispondente](../catalog/social/linkedin.md)
* [(Legacy) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Connessione PubMatic](../catalog/advertising/pubmatic.md)
* [InviaGriglia](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Tipi di pubblico personalizzati di Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinazioni che non supportano gli aggiornamenti dei nomi del pubblico {#name-update-not-supported}

Per le destinazioni non elencate in precedenza, i nomi del pubblico rimangono statici dopo l’attivazione iniziale. Se devi aggiornare il nome di un pubblico per queste destinazioni, devi:

1. Creare un nuovo pubblico in Experience Platform con il nome desiderato
2. Attiva il nuovo pubblico nella destinazione

>[!TIP]
>
>Per evitare confusione, utilizza nomi di pubblico descrittivi dalla prima attivazione, soprattutto quando si attiva in destinazioni che non supportano gli aggiornamenti dei nomi di pubblico.

## Destinazioni che supportano la rimozione dei tipi di pubblico {#support-removal}

Quando rimuovi (annulla mappatura) un pubblico da una destinazione di streaming, Experience Platform tenta di rimuovere il pubblico corrispondente dalla piattaforma di destinazione. Tuttavia, non tutte le destinazioni supportano questa funzionalità.

Le seguenti destinazioni di streaming supportano la rimozione automatica del pubblico quando si annulla la mappatura di un pubblico dalla destinazione:

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [(Aziende) LinkedIn Pubblico Corrispondente](../catalog/social/linkedin-b2b.md)
* [(Legacy) (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Pubblico dell&#39;account Bombora](../catalog/advertising/bombora.md)
* [Criteo](../catalog/advertising/criteo.md)
* [Experience Cloud Audiences](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [LinkedIn - Tipi di pubblico corrispondenti](../catalog/social/linkedin.md)
* [LiveRamp - Distribuzione](../catalog/advertising/liveramp-distribution.md)
* [Categorie di interesse Mailchimp](../catalog/email-marketing/mailchimp-interest-categories.md)
* [Connessione PubMatic](../catalog/advertising/pubmatic.md)
* [Salesforce Marketing Cloud - Coinvolgimento dell&#39;account](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [InviaGriglia](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Tipi di pubblico personalizzati di Twitter](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### Destinazioni che non supportano la rimozione di un pubblico

Per le destinazioni non elencate in precedenza, quando annulli la mappatura di un pubblico dalla destinazione, Experience Platform rimuove solo la mappatura. Il pubblico nella piattaforma di destinazione rimane attivo finché non lo elimini manualmente nella piattaforma partner.
