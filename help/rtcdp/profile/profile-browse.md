---
keywords: visualizzare profili rtcdp;visualizzazione profilo rtcdp;profili rtcdp
title: Cercare profili in Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform consente di sfogliare i dati del profilo cliente in tempo reale utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Cercare profili in Real-time Customer Data Platform

Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi singoli clienti, combinando dati provenienti da più canali tra cui online, offline, CRM e dati di terze parti. Poiché i singoli profili vengono aggregati in base ai dati inseriti nel sistema da varie fonti, ogni profilo diventa un account utilizzabile e con marca temporale per ogni interazione del cliente con il tuo marchio.

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare questi profili di sola lettura e visualizzare informazioni importanti relative a ciascuno dei tuoi clienti, incluse le loro preferenze, gli eventi passati, le interazioni e i segmenti a cui appartiene l’individuo.

Adobe Real-time Customer Data Platform è basato su Adobe Experience Platform ed è quindi in grado di utilizzare le funzionalità di visualizzazione del profilo nell’interfaccia utente di Experience Platform. Per una guida dettagliata alla visualizzazione dei profili dei clienti all’interno dell’interfaccia utente di Platform, consulta [Guida utente al profilo cliente in tempo reale](../../profile/ui/user-guide.md).

## Miglioramenti al profilo per Real-Time CDP, B2B Edition

Oltre alle funzionalità di ricerca dei profili supportate da Adobe Experience Platform, gli utenti Real-Time CDP e B2B Edition possono accedere agli attributi e agli eventi B2B all’interno del profilo del cliente nel [!UICONTROL Attributi] e [!UICONTROL Eventi] rispettivamente. I dati B2B possono essere utilizzati anche per eseguire la segmentazione, con i segmenti che compaiono sotto il [!UICONTROL Iscrizione al segmento] accanto ai segmenti non B2B.

Real-Time CDP, B2B Edition consente anche di sfogliare [!UICONTROL Account], [!UICONTROL Opportunità]e [!UICONTROL Record sorgente] da diverse origini aziendali associate a un singolo cliente.

Per esplorare questi miglioramenti, inizia seguendo i passaggi descritti in [Guida utente al profilo cliente in tempo reale](../../profile/ui/user-guide.md) per sfogliare un profilo in base a criteri di unione o namespace di identità.

![](images/b2b-browse-profile.png)

I dettagli del profilo includono l’accesso a [!UICONTROL Account], [!UICONTROL Opportunità]e [!UICONTROL Record sorgente] oltre alle informazioni standard fornite nel profilo del cliente, che sono state migliorate con eventi e attributi B2B.

![](images/b2b-profile-detail.png)

### Scheda Account

Seleziona **[!UICONTROL Account]** per visualizzare un elenco degli account relativi al profilo. Questo elenco include informazioni di base dal profilo dell’account come il nome, il sito web e il settore dell’account, nonché un collegamento al profilo dell’account.

Per ulteriori informazioni sulla visualizzazione e l’esplorazione dei profili dell’account, inizia leggendo il [panoramica dei profili account](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Scheda Opportunità

La **[!UICONTROL Opportunità]** tab fornisce i dettagli relativi alle opportunità aperte e chiuse relative all’account. Queste opportunità possono essere acquisite in Experienci Platform da più sorgenti, tuttavia Real-Time CDP, B2B Edition rende facile per gli esperti di marketing vedere tutte queste opportunità insieme in un’unica posizione.

Ogni opportunità include informazioni quali il nome dell’opportunità, la sua quantità, lo stadio e se l’opportunità è aperta, chiusa, vinta o persa.

![](images/b2b-profile-opportunities.png)

### Scheda Record di origine

La **[!UICONTROL Record sorgente]** La scheda ti consente di visualizzare facilmente i record sorgente multipli provenienti dalle origini aziendali che contribuiscono al singolo profilo cliente. Oltre al [!UICONTROL Chiave di origine della persona] e l&#39;indirizzo e-mail, ogni record sorgente fornisce anche il tipo di record (ad esempio, un record &quot;contatto&quot; o &quot;lead&quot;), nonché l&#39;origine.

![](images/b2b-profile-source-records.png)
