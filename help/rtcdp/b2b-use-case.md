---
keywords: RTCDP;CDP;Real-time Customer Data Platform;piattaforma dati cliente in tempo reale;cdp in tempo reale;cdp;rtcdp
title: Esempio di utilizzo per Real-time Customer Data Platform B2B Edition
description: Questo scenario di esempio fornisce un esempio per la configurazione dell’implementazione di Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 15505980-ac33-44b2-8989-c08cbabd212b
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# Esempio di utilizzo per Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition amplia le offerte Real-Time CDP e Adobe Experience Platform esistenti per supportare dati e flussi di lavoro B2B. Questo documento fornisce un esempio di caso d&#39;uso che dimostra i vantaggi aggiuntivi forniti da B2B Edition. Sono le seguenti:

- Combina i dati relativi a persone e account provenienti da diverse origini dati in silos per produrre una visualizzazione completa che consenta una migliore comprensione dei clienti e una segmentazione più accurata. Consulta la documentazione su [creazione di relazioni dello schema XDM](./schemas/b2b.md) da utilizzare con varie fonti B2B per ulteriori informazioni.
- Segmenta un pubblico in base agli attributi delle entità correlate. Sono inclusi account, opportunità, campagne ed elenchi di marketing. I segmenti non sono più limitati agli attributi Persona ed Eventi di esperienza. Consulta la sezione [Documentazione sulla segmentazione B2B](./segmentation/b2b.md) per ulteriori esempi sulla creazione di tipi di pubblico specifici per B2B.
- Supporta in modo nativo il caso d’uso di una persona relativa a più account.

## Caso d’uso

Bodea, un&#39;azienda tecnologica, ha un nuovo prodotto e desidera indirizzare simultaneamente i clienti con un&#39;e-mail e una campagna pubblicitaria LinkedIn. Al fine di massimizzare l&#39;efficienza della campagna di marketing, Bodea vuole anche rivolgersi alle persone associate a quell&#39;account esistente che hanno speso più di un milione di dollari per i suoi prodotti in precedenza, E ha visitato la nuova pagina di prodotto nell&#39;ultimo mese.

Tuttavia, Bodea ha due linee di business diverse. La prima linea di business &quot;Line 1&quot; di Bodea crea software per l&#39;industria automobilistica. La sua seconda linea di business &quot;Line 2&quot; vende stampanti 3D che creano parti di automobile. A causa delle due linee di business di Bodea, i dati sui ricavi generati dai conti clienti di Bodea non sono unificati in un’unica vista.

Ogni linea di business ha un proprio sistema di vendita: &quot;CRM 1&quot; e &quot;CRM 2&quot;. Entrambi questi sistemi di vendita CRM sono collegati alla propria piattaforma di automazione marketing &quot;Marketo 1&quot; e &quot;Marketo 2&quot;. I dati da CRM 1 vengono sincronizzati solo in Marketo 1 e i dati da CRM2 vengono sincronizzati solo in Marketo 2. In ultima analisi, i loro dati vengono conservati in diversi silos di informazioni aziendali.

## Situazione attuale dei dati

Poiché entrambe le linee di attività di Bodea vendono alla società Townsend, i dati aziendali di Townsend sono registrati come due conti separati in ciascun sistema di vendita.

In Marketo 1, Townsend è registrato come Account 1. Ha due persone correlate (p1@townsend.com e p2@townsend.com) e un&#39;opportunità di $200k chiusa (&quot;Opportunity 1&quot;) in CRM 1. Tali dati vengono sincronizzati da CRM 1 in Marketo 1.

In Marketo 2, Townsend è registrato come Account 2. L&#39;account 2 ha anche due persone collegate (p2@townsend.com e p3@townsend.com) e un&#39;opportunità di $900k chiusa (&quot;Opportunity 2&quot;) in CRM 2. Tali dati vengono sincronizzati da CRM 2 a Marketo 2.

Per scopi di integrazione e di controllo aziendale aggiuntivi, Bodea dispone anche di un sistema Master Data Management (MDM) in cui mantiene un record che indica che l&#39;account 1 in Marketo 1 (e CRM 1) e l&#39;account 2 in Marketo 2 (e CRM 2) sono la stessa azienda.

Nell&#39;ultimo mese, `p2@townsend.com` ha visitato la nuova pagina del prodotto e la visita web è stata registrata da Marketo 1.

![diagramma informazioni account](./assets/account-info.png)

## Il problema

La Linea 1 ha appena rilasciato un nuovo prodotto software e desidera venderlo all’attuale base di clienti di livello superiore di Bodea. Bodea lancia una campagna di marketing pensando a quel pubblico specifico.

Poiché le informazioni relative a Townsend sono registrate come Account 1 in Marketo 1 e Account 2 in Marketo 2, il team marketing di Bodea non è in grado di utilizzare in modo efficiente le informazioni silurate.

Questo impedisce al team marketing di Bodea di indirizzare in modo efficiente specifici contatti commerciali a queste aziende con questa nuova opportunità.

Ad oggi, Townsend ha speso cumulativamente più di un milione di dollari sui prodotti Bodea in tutti i loro conti. Tuttavia, un segmento creato utilizzando il loro vecchio sistema non includerebbe nessuno di Townsend a meno che il totale speso all&#39;interno di un singolo sistema di vendita non sia superiore a 1 milione di dollari. Questo perché i dati sui ricavi vengono memorizzati in account in diversi sistemi di vendita.

Poiché la spesa di Townsend è suddivisa in diversi sistemi di vendita e non è un totale individuale più di un milione, il segmento non troverebbe nessuno qualificato in Marketo 1 o Marketo 2.

### Come Real-Time CDP B2B Edition risolve il problema

Con Real-Time CDP B2B Edition, il team marketing di Bodea può:

- Combina i dati di tutte le origini diverse (più istanze Marketo e CRM e la Gestione dati principale) in Real-Time CDP B2B Edition.

Con RT-CDP B2B Edition, Bodea può utilizzare il connettore sorgente di Marketo Engage per inserire in Experience Platform i dati B2B da Marketo 1 e Marketo 2 e mantenere aggiornati i dati utilizzando le applicazioni connesse a Platform. Consulta la sezione [Connettore sorgente Marketo](../sources/connectors/adobe-applications/marketo/marketo.md) documentazione per ulteriori informazioni.

I dati B2B (persone, account, opportunità e attività ) provenienti da CRM1 vengono sincronizzati in Marketo 1. Analogamente, tutti i dati B2B di CRM 2 sono sincronizzati in Marketo 2. Vengono sincronizzati in Adobe Experience Platform tramite il connettore sorgente Marketo. Tuttavia, se Bodea desidera inserire in Experience Platform dati aggiuntivi da un sistema di gestione delle relazioni con i clienti, può utilizzare i connettori di gestione delle relazioni con i clienti esistenti.

Per il bene della semplicità e lo scopo di questo esempio, le persone vengono identificate dalle loro e-mail. I dati di conto combinati per questo esempio sono i seguenti:

| People |
|---|
| p1@townsend.com |
| p2@townsend.com (che ha visitato la pagina del nuovo prodotto nell’ultimo mese) |
| p3@townsend.com |

| Opportunità (chiuse) |
|---|
| Opportunità 1, $200.000 |
| Opportunità 2, $900.000 |

- Crea segmenti univoci utilizzando questi dati aggregati per iniziative di marketing diverse. In questo esempio, il segmento trova tutte le persone che:

   - Avere opportunità associate (in TUTTI gli account) superiore a $1 milione di valore
   - AND
   - Ho visitato la pagina del prodotto nell’ultimo mese

- Crea un pubblico che sia i destinatari più efficienti della nuova campagna di marketing di Bodea. In questo esempio, RT-CDP, B2B Edition aiuterà l’addetto al marketing a identificare `p2@townsend.com` come target corretto per questa campagna di marketing.

Utilizzando il Marketo Engage e le destinazioni LinkedIn, Bodea dispone di una soluzione end-to-end per la gestione dell’esperienza dei clienti (CXM) per il proprio team di marketing. Il pubblico creato in Experience Platform viene inviato alla destinazione Marketo dove viene visualizzato come elenco statico. Questo pubblico viene quindi aggiunto automaticamente a una campagna di marketing Marketo. Allo stesso tempo, il pubblico può anche essere inviato a una campagna di marketing LinkedIn dalla RT-CDP B2B Edition.

## Passaggi successivi

Leggendo questo documento, ti sono stati presentati i tipi di obiettivi e problemi che possono essere risolti utilizzando Real-Time CDP B2B Edition.

Per migliorare la comprensione delle funzioni specifiche di B2B, si consiglia di consultare la seguente documentazione:

- [Esercitazione end-to-end su Real-time Customer Data Platform B2B Edition](./b2b-tutorial.md)
- [Fonti in Real-time Customer Data Platform B2B Edition](./sources/b2b.md)
- [Schemi in Real-time Customer Data Platform B2B Edition](./schemas/b2b.md)
- [Esempi di segmentazione B2B](./segmentation/b2b.md)
- [Panoramica dei profili account](./accounts/account-profile-overview.md)
- [Destinazioni in Real-time Customer Data Platform B2B Edition](./destinations/b2b.md)
- [Configurare una destinazione LinkedIn Matched Audiences](../destinations/catalog/social/linkedin.md)
