---
keywords: visualizzare profili rtcdp;rtcdp visualizzazione profilo;rtcdp profili
title: Sfogliare i profili in Real-Time Customer Data Platform
description: Adobe Real-Time Customer Data Platform consente di sfogliare i dati Real-Time Customer Profile tramite l’interfaccia utente di Adobe Experience Platform.
feature: Get Started, Profiles
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it#rtcdp-editions" newtab=true
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Sfogliare i profili in Real-Time Customer Data Platform

Real-Time Customer Profile crea una visualizzazione olistica di ciascuno dei singoli clienti, combinando dati provenienti da più canali tra cui dati online, offline, del sistema CRM e di terze parti. Poiché i singoli profili vengono aggregati in base ai dati inseriti nel sistema da varie sorgenti, ogni profilo diventa un account actionable con marca temporale di ogni interazione del cliente con il brand.

Nell’interfaccia utente di Adobe Experience Platform, puoi visualizzare questi profili di sola lettura e informazioni importanti su ciascuno dei singoli clienti, incluse le preferenze, gli eventi passati, le interazioni e i tipi di pubblico a cui appartengono i singoli utenti.

Adobe Real-Time Customer Data Platform è basato su Adobe Experience Platform ed è quindi in grado di utilizzare le funzionalità di visualizzazione dei profili nell’interfaccia utente di Experience Platform. Per una guida dettagliata alla visualizzazione dei profili dei clienti nell&#39;interfaccia utente di Experience Platform, consulta la [guida utente Profilo cliente in tempo reale](../../profile/ui/user-guide.md).

## Miglioramenti del profilo per Real-Time CDP, B2B edition

Oltre alle funzionalità di esplorazione del profilo supportate da Adobe Experience Platform, Real-Time CDP, gli utenti di B2B edition possono accedere agli attributi B2B e agli eventi all&#39;interno del profilo del cliente, rispettivamente nelle schede [!UICONTROL Attributes] e [!UICONTROL Events]. I dati B2B possono essere utilizzati anche per eseguire la segmentazione, con quei tipi di pubblico visualizzati nella scheda [!UICONTROL Audience membership] del cliente insieme a tipi di pubblico non B2B.

Real-Time CDP, B2B edition consente inoltre di sfogliare [!UICONTROL Accounts], [!UICONTROL Opportunities] e [!UICONTROL Source records] dalle origini aziendali associate a un singolo cliente.

Per esplorare questi miglioramenti, iniziare seguendo i passaggi descritti nella [Guida utente del profilo cliente in tempo reale](../../profile/ui/user-guide.md) per sfogliare un profilo in base a un criterio di unione o a uno spazio dei nomi delle identità.

![](images/b2b-browse-profile.png)

I dettagli del profilo includono l&#39;accesso alle schede [!UICONTROL Accounts], [!UICONTROL Opportunities] e [!UICONTROL Source records] oltre alle informazioni standard fornite nel profilo cliente, migliorate anche con eventi e attributi B2B.

![](images/b2b-profile-detail.png)

Per ulteriori informazioni sui dettagli del profilo forniti nell&#39;interfaccia utente di Experience Platform, consulta la sezione [dettagli della documentazione della dashboard dei profili](../../dashboards/guides/profiles.md#browse-profiles).

### Scheda Account

Selezionare **[!UICONTROL Accounts]** per visualizzare un elenco di account correlati al profilo. Questo elenco include informazioni di base dal profilo dell’account, come il nome, il sito web e il settore dell’account, nonché un collegamento al profilo dell’account.

Per ulteriori informazioni sulla visualizzazione e l&#39;esplorazione dei profili dell&#39;account, leggere la [panoramica dei profili dell&#39;account](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Scheda Opportunità

La scheda **[!UICONTROL Opportunities]** fornisce i dettagli relativi alle opportunità aperte e chiuse correlate all&#39;account. Queste opportunità possono essere acquisite in Experience Platform da più origini, tuttavia Real-Time CDP, B2B edition consente agli esperti di marketing di vedere tutte queste opportunità insieme in un’unica posizione.

Ogni opportunità include informazioni quali il nome, l&#39;importo, la fase e se l&#39;opportunità è aperta, chiusa, vinta o persa.

![](images/b2b-profile-opportunities.png)

### Scheda Record di Source

La scheda **[!UICONTROL Source records]** consente di visualizzare facilmente più record di origine provenienti dalle origini aziendali che contribuiscono al singolo profilo cliente. Oltre a [!UICONTROL Person source key] e all&#39;indirizzo di posta elettronica, ogni record di origine fornisce anche il tipo di record, ad esempio un record &quot;contatto&quot; o &quot;lead&quot;, e l&#39;origine.

![](images/b2b-profile-source-records.png)
