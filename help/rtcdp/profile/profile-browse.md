---
keywords: visualizzare profili rtcdp;rtcdp visualizzazione profilo;rtcdp profili
title: Sfogliare i profili in Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform consente di sfogliare i dati Real-Time Customer Profile tramite l’interfaccia utente di Adobe Experience Platform.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: ea785ffa1dfa0f7c684fe536796a4b7409882159
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# Sfogliare i profili in Real-time Customer Data Platform

Real-Time Customer Profile crea una visualizzazione olistica di ciascuno dei singoli clienti, combinando dati provenienti da più canali tra cui dati online, offline, del sistema CRM e di terze parti. Poiché i singoli profili vengono aggregati in base ai dati inseriti nel sistema da varie sorgenti, ogni profilo diventa un account actionable con marca temporale di ogni interazione del cliente con il brand.

Nell’interfaccia utente di Adobe Experience Platform, puoi visualizzare questi profili di sola lettura e informazioni importanti su ciascuno dei singoli clienti, incluse le preferenze, gli eventi passati, le interazioni e i tipi di pubblico a cui appartengono i singoli utenti.

Adobe Real-time Customer Data Platform è basato su Adobe Experience Platform ed è quindi in grado di utilizzare le funzionalità di visualizzazione del profilo nell’interfaccia utente di Experience Platform. Per una guida dettagliata alla visualizzazione dei profili cliente nell&#39;interfaccia utente di Platform, consulta la [guida utente Profilo cliente in tempo reale](../../profile/ui/user-guide.md).

## Miglioramenti del profilo per Real-Time CDP, edizione B2B

Oltre alle funzionalità di esplorazione del profilo supportate da Adobe Experience Platform, gli utenti di Real-Time CDP e dell&#39;edizione B2B possono accedere agli attributi e agli eventi B2B all&#39;interno del profilo del cliente, rispettivamente nelle schede [!UICONTROL Attributi] e [!UICONTROL Eventi]. I dati B2B possono essere utilizzati anche per eseguire la segmentazione, con i tipi di pubblico visualizzati nella scheda [!UICONTROL Appartenenza al pubblico] del cliente insieme a tipi di pubblico non B2B.

Real-Time CDP, B2B Edition consente inoltre di sfogliare [!UICONTROL Account], [!UICONTROL Opportunità] e [!UICONTROL Record Source] dalle origini aziendali associate a un singolo cliente.

Per esplorare questi miglioramenti, iniziare seguendo i passaggi descritti nella [Guida utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md) per sfogliare un profilo in base a un criterio di unione o a uno spazio dei nomi delle identità.

![](images/b2b-browse-profile.png)

I dettagli del profilo includono l&#39;accesso alle schede [!UICONTROL Account], [!UICONTROL Opportunità] e [!UICONTROL Record di Source] oltre alle informazioni standard fornite nel profilo cliente, migliorate anche con eventi e attributi B2B.

![](images/b2b-profile-detail.png)

Per ulteriori informazioni sui dettagli del profilo forniti nell&#39;interfaccia utente di Platform, consulta la sezione [dettagli della documentazione del dashboard Profili](../../dashboards/guides/profiles.md#browse-profiles).

### Scheda Account

Seleziona **[!UICONTROL Account]** per visualizzare un elenco di account correlati al profilo. Questo elenco include informazioni di base dal profilo dell’account, come il nome, il sito web e il settore dell’account, nonché un collegamento al profilo dell’account.

Per ulteriori informazioni sulla visualizzazione e l&#39;esplorazione dei profili dell&#39;account, leggere la [panoramica dei profili dell&#39;account](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Scheda Opportunità

La scheda **[!UICONTROL Opportunità]** fornisce i dettagli relativi alle opportunità aperte e chiuse correlate all&#39;account. Queste opportunità possono essere acquisite in Experience Platform da più origini, tuttavia Real-Time CDP, B2B Edition consente agli esperti di marketing di vedere tutte queste opportunità insieme in un’unica posizione.

Ogni opportunità include informazioni quali il nome, l&#39;importo, la fase e se l&#39;opportunità è aperta, chiusa, vinta o persa.

![](images/b2b-profile-opportunities.png)

### Scheda Record di Source

La scheda **[!UICONTROL Record Source]** consente di visualizzare facilmente più record di origine provenienti dalle origini aziendali che contribuiscono al singolo profilo cliente. Oltre alla [!UICONTROL chiave di origine della persona] e all&#39;indirizzo di posta elettronica, ogni record di origine fornisce anche il tipo di record, ad esempio un record &quot;contatto&quot; o &quot;lead&quot;, e l&#39;origine.

![](images/b2b-profile-source-records.png)
