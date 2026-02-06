---
keywords: RTCDP;CDP;Real-Time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Caso di utilizzo di esempio per Real-Time Customer Data Platform B2B edition
description: Questo scenario fornisce un esempio per la configurazione dell’implementazione di Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Use Cases, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# Caso di utilizzo di esempio per Real-Time Customer Data Platform B2B edition

Real-Time Customer Data Platform B2B edition amplia le offerte Real-Time CDP e Adobe Experience Platform esistenti per supportare i dati e i flussi di lavoro B2B. Questo documento fornisce un esempio di caso d’uso che illustra i vantaggi aggiuntivi offerti da B2B edition. Sono le seguenti:

- Combina i dati di persone e account provenienti da diverse origini dati in silos per produrre una visualizzazione completa che consenta una migliore comprensione dei clienti e una segmentazione più accurata. Per ulteriori informazioni, consulta la documentazione su [creazione di relazioni tra schemi XDM](./schemas/b2b.md) da utilizzare con origini B2B diverse.
- Segmentare un pubblico in base agli attributi delle entità correlate. Ciò include account, opportunità, campagne ed elenchi di marketing. I tipi di pubblico non sono più limitati solo agli attributi della persona e agli eventi esperienza. Per ulteriori esempi sulla creazione di tipi di pubblico specifici per B2B, consulta la [documentazione sulla segmentazione B2B](./segmentation/b2b.md).
- Supporta in modo nativo il caso di utilizzo di una persona correlata a più account.

## Caso d’uso

Bodea, un’azienda tecnologica, ha un nuovo prodotto e desidera eseguire il targeting dei clienti simultaneamente con un’e-mail e una campagna pubblicitaria LinkedIn. Al fine di massimizzare l’efficienza della loro campagna di marketing, Bodea vuole anche rivolgersi alle persone associate a tale account esistente che in precedenza hanno speso oltre un milione di dollari per i suoi prodotti e che hanno visitato la nuova pagina di prodotto nell’ultimo mese.

Tuttavia, Bodea ha due linee di business diverse. La prima linea di business di Bodea, la &quot;Linea 1&quot;, crea software per l&#39;industria automobilistica. La seconda linea di business &quot;Line 2&quot; vende stampanti 3D che creano parti di automobili. Come risultato delle due linee di business di Bodea, i dati dei ricavi generati dai conti clienti di Bodea non sono unificati in un’unica vista.

Ogni linea di business ha un proprio sistema di vendita: &quot;CRM 1&quot; e &quot;CRM 2&quot;. Entrambi questi sistemi di vendita CRM sono collegati alla propria piattaforma di automazione marketing &quot;Marketo 1&quot; e &quot;Marketo 2&quot;. I dati da CRM 1 vengono sincronizzati solo in Marketo 1 e i dati da CRM2 vengono sincronizzati solo in Marketo 2. In ultima analisi, i dati vengono conservati in diversi silos di informazioni aziendali.

## Situazione attuale dei dati

Poiché entrambe le linee di attività di Bodea vendono alla società Townsend, i dati commerciali di Townsend sono registrati come due conti separati in ciascun sistema di vendita.

In Marketo 1, Townsend viene registrato come Account 1. Ha due persone correlate (p1@townsend.com e p2@townsend.com) e un&#39;opportunità chiusa di $200k (&quot;Opportunità 1&quot;) in CRM 1. Tali dati vengono sincronizzati da CRM 1 a Marketo 1.

In Marketo 2, Townsend viene registrato come Account 2. L’account 2 dispone anche di due persone correlate (p2@townsend.com e p3@townsend.com) e di un’opportunità chiusa di 900.000 dollari (&quot;opportunità 2&quot;) in CRM 2. Tali dati vengono sincronizzati da CRM 2 a Marketo 2.

Ai fini dell’integrazione e di un ulteriore controllo aziendale, Bodea dispone anche di un sistema di gestione dei dati master (MDM) in cui è conservato un record indicante che l’account 1 in Marketo 1 (e CRM 1) e l’account 2 in Marketo 2 (e CRM 2) sono la stessa società.

Nell&#39;ultimo mese, `p2@townsend.com` ha visitato la nuova pagina del prodotto e la visita Web è stata registrata da Marketo 1.

![diagramma informazioni account](./assets/account-info.png)

## Il problema

La linea 1 ha appena rilasciato un nuovo prodotto software e vorrebbe vendere l’up-sell alla base clienti di alto livello di Bodea. Bodea lancia una campagna di marketing pensando a quel pubblico specifico.

Poiché le informazioni Townsend pertinenti vengono registrate come Account 1 in Marketo 1 e Account 2 in Marketo 2, il team di marketing di Bodea non è in grado di utilizzare in modo efficiente le informazioni silos.

Questo impedisce al team di marketing di Bodea di indirizzare in modo efficiente specifici contatti di business presso queste aziende con questa nuova opportunità.

Ad oggi, Townsend ha speso più di un milione di dollari cumulativamente per i prodotti Bodea in tutti i loro account. Tuttavia, un pubblico creato utilizzando il loro vecchio sistema non includerebbe nessuno di Townsend a meno che il totale speso all&#39;interno di un singolo sistema di vendita non ammontasse a più di 1 milione di dollari. Questo perché i dati dei ricavi vengono inseriti in un silos nei conti in sistemi di vendita diversi.

Poiché la spesa di Townsend è suddivisa tra diversi sistemi di vendita e non supera singolarmente un milione di unità, la definizione del segmento non troverebbe nessuno qualificato né in Marketo 1 né in Marketo 2.

### Come Real-Time CDP B2B edition risolve il problema

Con Real-Time CDP B2B edition, il team marketing di Bodea può:

- Combina i dati di tutte le diverse origini (più istanze di Marketo e CRM e la Gestione dati master) in Real-Time CDP B2B edition.

Con RT-CDP B2B edition, Bodea può utilizzare il connettore Marketo Engage Source per inserire in Experience Platform i dati B2B da Marketo 1 e Marketo 2 e mantenerli aggiornati utilizzando le applicazioni connesse ad Experience Platform. Per ulteriori informazioni, consulta la documentazione del [connettore di origine Marketo](../sources/connectors/adobe-applications/marketo/marketo.md).

I dati B2B (Persone, Account, Opportunità e attività ) da CRM1 vengono sincronizzati in Marketo 1. Analogamente, tutti i dati B2B da CRM 2 vengono sincronizzati in Marketo 2. Vengono sincronizzati in Adobe Experience Platform tramite il connettore di origine Marketo. Tuttavia, se Bodea desidera inserire in Experience Platform dati aggiuntivi provenienti da un sistema di gestione delle relazioni con i clienti, può utilizzare i connettori CRM esistenti.

Per semplicità e per lo scopo di questo esempio, le persone vengono identificate dalle loro e-mail. L&#39;aspetto dei dati di conto combinati per questo esempio è il seguente:

| People |
|---|
| p1@townsend.com |
| p2@townsend.com (che ha visitato la nuova pagina del prodotto nell’ultimo mese) |
| p3@townsend.com |

| Opportunità (chiuse) |
|---|
| Opportunità 1, 200.000 dollari |
| Opportunità 2, 900.000 dollari |

- Crea tipi di pubblico univoci utilizzando i dati aggregati per varie iniziative di marketing. In questo esempio, la definizione del segmento trova tutte le persone che:

   - Avere opportunità associate (su TUTTI gli account) superiori a 1 milione di dollari in valore
   - E
   - Hai visitato la pagina del prodotto nell’ultimo mese

- Crea un pubblico che sia il destinatario più efficiente della nuova campagna di marketing di Bodea. In questo esempio, RT-CDP, B2B edition aiuterà l&#39;addetto al marketing a identificare `p2@townsend.com` come destinazione corretta per questa campagna di marketing.

Utilizzando le destinazioni Marketo Engage e LinkedIn, Bodea dispone di una soluzione CXM (Customer Experience Management) end-to-end per il proprio team di marketing. Il pubblico creato in Experience Platform viene inviato alla destinazione Marketo dove viene visualizzato come elenco statico. Questo pubblico viene quindi aggiunto automaticamente a una campagna di marketing Marketo. Contemporaneamente, il pubblico può anche essere inviato a una campagna di marketing LinkedIn dal B2B edition RT-CDP.

## Passaggi successivi

Dopo aver letto questo documento, ti verranno presentati i tipi di obiettivi e problemi che è possibile risolvere con Real-Time CDP B2B edition.

Per comprendere meglio le funzioni specifiche di B2B, si consiglia di consultare la seguente documentazione:

- [Tutorial end-to-end su Real-Time Customer Data Platform B2B edition](./b2b-tutorial.md)
- [Origini in Real-Time Customer Data Platform B2B edition](./sources/b2b.md)
- [Schemi in Real-Time Customer Data Platform B2B edition](./schemas/b2b.md)
- [Esempi di segmentazione B2B](./segmentation/b2b.md)
- [Panoramica dei profili account](./accounts/account-profile-overview.md)
- [Destinazioni in Real-Time Customer Data Platform B2B edition](./destinations/b2b.md)
- [Configurare una destinazione LinkedIn Matched Audiences](../destinations/catalog/social/linkedin.md)
