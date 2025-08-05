---
title: Schemi in Real-Time Customer Data Platform B2B edition
description: Panoramica del ruolo degli schemi Experience Data Model (XDM) in Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 09f671af0d04251ab7b0a71528cb4b9745594b1c
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 12%

---

# Schemi in Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition fornisce diverse [classi XDM (Experience Data Model) standard](../../xdm/schema/composition.md#class) che acquisiscono dettagli sulle entità di dati B2B essenziali, come account, opportunità, campagne e altro ancora. Inoltre, Real-Time CDP B2B edition consente di definire relazioni molti-a-uno tra questi schemi in modo che possano partecipare a casi di utilizzo di segmentazione avanzata.

>[!IMPORTANT]
>
>Gli schemi B2B sono disponibili per l&#39;utilizzo nelle applicazioni Experience Platform, ad esempio in [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/it/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition). <br/>È tuttavia necessario avere accesso a Real-Time CDP B2B edition per consentire agli schemi B2B (profili in) di partecipare a [Profilo cliente in tempo reale](../../profile/home.md).

In Real-Time CDP B2B edition sono disponibili le seguenti classi standard:

* [Account aziendale XDM](../../xdm/classes/b2b/business-account.md)
* [Relazione della persona dell’account aziendale XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campagna aziendale XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membri della campagna aziendale XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Opportunità di business XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relazione della persona dell’opportunità di business XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Elenco di marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membri dell’elenco di marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Per capire come gli schemi si adattano al flusso di lavoro B2B, consulta l&#39;[esercitazione end-to-end](../b2b-tutorial.md).

Per i passaggi su come creare una relazione molti-a-uno tra due schemi, consulta l&#39;esercitazione su [definizione delle relazioni tra schemi B2B](../../xdm/tutorials/relationship-b2b.md).

Se utilizzi una connessione di origine B2B, puoi utilizzare uno strumento per generare automaticamente gli schemi richiesti e le relazioni tra di essi. Per ulteriori informazioni, consulta la guida sugli [spazi dei nomi B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) nella documentazione delle origini.
