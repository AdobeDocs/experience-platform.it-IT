---
keywords: visualizzare profili rtcdp;visualizzazione profilo rtcdp;profili rtcdp
title: Cercare profili in Real-time Customer Data Platform
description: Real-time Customer Data Platform consente di sfogliare i dati Profilo cliente in tempo reale utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 6579e371a8729e926b7061418c786150a27d4876
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Cercare profili in Real-time Customer Data Platform

Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi singoli clienti, combinando dati provenienti da più canali tra cui online, offline, CRM e dati di terze parti. Poiché i singoli profili vengono aggregati in base ai dati inseriti nel sistema da varie fonti, ogni profilo diventa un account utilizzabile e con marca temporale per ogni interazione del cliente con il tuo marchio.

Nell’interfaccia utente di Adobe Experience Platform puoi visualizzare questi profili di sola lettura e visualizzare informazioni importanti relative a ciascuno dei tuoi clienti, incluse le loro preferenze, gli eventi passati, le interazioni e i segmenti a cui appartiene l’individuo.

Real-time Customer Data Platform è basato su Adobe Experience Platform ed è quindi in grado di utilizzare le funzionalità di visualizzazione del profilo nell’interfaccia utente di Experience Platform. Per una guida dettagliata alla visualizzazione dei profili dei clienti all’interno dell’interfaccia utente di Platform, consulta la [Guida utente al profilo cliente in tempo reale](../../profile/ui/user-guide.md) .

## Miglioramenti al profilo per Real-time CDP, B2B Edition

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Oltre alle funzionalità di ricerca dei profili supportate da Adobe Experience Platform, gli utenti di Real-time CDP e B2B Edition possono accedere agli attributi e agli eventi B2B all’interno del profilo del cliente, rispettivamente nelle schede [!UICONTROL Attributi] e [!UICONTROL Eventi] . I dati B2B possono anche essere utilizzati per eseguire la segmentazione, con i segmenti che compaiono sotto la scheda [!UICONTROL Iscrizione al segmento] del cliente insieme ai segmenti non B2B.

Real-time CDP, B2B Edition consente inoltre di sfogliare [!UICONTROL Account], [!UICONTROL Opportunità] e [!UICONTROL Record di origine] tra le origini aziendali associate a un singolo cliente.

Per esplorare questi miglioramenti, inizia seguendo i passaggi descritti nella [Guida utente al profilo cliente in tempo reale](../../profile/ui/user-guide.md) per sfogliare un profilo in base a criteri di unione o namespace di identità.

![](images/b2b-browse-profile.png)

I dettagli del profilo includono l&#39;accesso alle schede [!UICONTROL Account], [!UICONTROL Opportunità] e [!UICONTROL Record di origine] oltre alle informazioni standard fornite nel profilo del cliente, che sono state migliorate anche con gli eventi e gli attributi B2B.

![](images/b2b-profile-detail.png)

### Scheda Account

Seleziona **[!UICONTROL Account]** per visualizzare un elenco di account relativi al profilo. Questo elenco include informazioni di base dal profilo dell’account come il nome, il sito web e il settore dell’account, nonché un collegamento al profilo dell’account.

Per ulteriori informazioni sulla visualizzazione e l&#39;esplorazione dei profili account, inizia leggendo la [panoramica dei profili account](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Scheda Opportunità

La scheda **[!UICONTROL Opportunità]** fornisce dettagli relativi alle opportunità aperte e chiuse relative all’account. Queste opportunità possono essere acquisite in Experience Platform da più sorgenti, tuttavia Real-time CDP, B2B Edition rende facile per gli esperti di marketing vedere tutte queste opportunità insieme in un&#39;unica posizione.

Ogni opportunità include informazioni quali il nome dell’opportunità, la sua quantità, lo stadio e se l’opportunità è aperta, chiusa, vinta o persa.

![](images/b2b-profile-opportunities.png)

### Scheda Record di origine

La scheda **[!UICONTROL Record sorgente]** ti consente di vedere facilmente i record sorgente multipli provenienti dalle origini aziendali che contribuiscono al singolo profilo cliente. Oltre alla [!UICONTROL Chiave sorgente persona] e all&#39;indirizzo e-mail, ogni record sorgente fornisce anche il tipo di record (ad esempio, un record &quot;contatto&quot; o &quot;lead&quot;), nonché l&#39;origine.

![](images/b2b-profile-source-records.png)
