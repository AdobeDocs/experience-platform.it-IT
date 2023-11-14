---
keywords: visualizzare profili rtcdp;rtcdp visualizzazione profilo;rtcdp profili
title: Sfogliare i profili in Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform consente di sfogliare i dati Real-Time Customer Profile tramite l’interfaccia utente di Adobe Experience Platform.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Sfogliare i profili in Real-time Customer Data Platform

Real-Time Customer Profile crea una visualizzazione olistica di ciascuno dei singoli clienti, combinando dati provenienti da più canali tra cui dati online, offline, del sistema CRM e di terze parti. Poiché i singoli profili vengono aggregati in base ai dati inseriti nel sistema da varie sorgenti, ogni profilo diventa un account actionable con marca temporale di ogni interazione del cliente con il brand.

Nell’interfaccia utente di Adobe Experience Platform, puoi visualizzare questi profili di sola lettura e informazioni importanti su ciascuno dei singoli clienti, incluse le preferenze, gli eventi passati, le interazioni e i tipi di pubblico a cui appartengono i singoli utenti.

Adobe Real-time Customer Data Platform è basato su Adobe Experience Platform ed è quindi in grado di utilizzare le funzionalità di visualizzazione del profilo nell’interfaccia utente di Experienci Platform. Per una guida dettagliata alla visualizzazione dei profili dei clienti nell’interfaccia utente di Platform, consulta [Guida utente di Real-Time Customer Profile](../../profile/ui/user-guide.md).

## Miglioramenti del profilo per Real-Time CDP, edizione B2B

Oltre alle funzionalità di navigazione del profilo supportate da Adobe Experience Platform, gli utenti di Real-Time CDP e della versione B2B possono accedere agli attributi e agli eventi B2B all’interno del profilo del cliente su [!UICONTROL Attributi] e [!UICONTROL Eventi] rispettivamente. I dati B2B possono essere utilizzati anche per eseguire la segmentazione, con quei tipi di pubblico che appaiono sotto il [!UICONTROL Iscrizione al pubblico] insieme ai tipi di pubblico non B2B.

Real-Time CDP, B2B Edition consente inoltre di esplorare [!UICONTROL Account], [!UICONTROL Opportunità], e [!UICONTROL Record di origine] da diverse origini aziendali associate a un singolo cliente.

Per esplorare questi miglioramenti, inizia seguendo i passaggi descritti in [Guida utente di Real-Time Customer Profile](../../profile/ui/user-guide.md) per sfogliare un profilo in base a un criterio di unione o a uno spazio dei nomi di identità.

![](images/b2b-browse-profile.png)

I dettagli del profilo includono l’accesso a [!UICONTROL Account], [!UICONTROL Opportunità], e [!UICONTROL Record di origine] oltre alle informazioni standard fornite nel profilo cliente, migliorate anche con eventi e attributi B2B.

![](images/b2b-profile-detail.png)

### Scheda Account

Seleziona **[!UICONTROL Account]** per visualizzare un elenco di account correlati al profilo. Questo elenco include informazioni di base dal profilo dell’account, come il nome, il sito web e il settore dell’account, nonché un collegamento al profilo dell’account.

Per ulteriori informazioni sulla visualizzazione e l’esplorazione dei profili dell’account, consulta la sezione [panoramica dei profili account](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Scheda Opportunità

Il **[!UICONTROL Opportunità]** fornisce dettagli relativi alle opportunità aperte e chiuse correlate all’account. Queste opportunità possono essere acquisite in Experienci Platform da più origini, tuttavia Real-Time CDP, B2B Edition consente agli esperti di marketing di vedere tutte queste opportunità insieme in un’unica posizione.

Ogni opportunità include informazioni quali il nome, l&#39;importo, la fase e se l&#39;opportunità è aperta, chiusa, vinta o persa.

![](images/b2b-profile-opportunities.png)

### Scheda Record di origine

Il **[!UICONTROL Record di origine]** Questa scheda consente di visualizzare facilmente i diversi record di origine provenienti dalle origini aziendali che contribuiscono al singolo profilo cliente. Oltre al [!UICONTROL Chiave sorgente della persona] e indirizzo e-mail, ogni record di origine fornisce anche il tipo di record (ad esempio, un record &quot;contatto&quot; o &quot;lead&quot;), nonché l’origine.

![](images/b2b-profile-source-records.png)
