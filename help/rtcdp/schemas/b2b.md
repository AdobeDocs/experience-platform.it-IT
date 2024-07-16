---
title: Schemi in Real-time Customer Data Platform B2B Edition
description: Panoramica del ruolo degli schemi Experience Data Model (XDM) in Adobe Real-time Customer Data Platform B2B Edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="Edizione B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 13%

---

# Schemi in Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B Edition fornisce diverse [classi XDM (Experience Data Model) standard](../../xdm/schema/composition.md#class) che acquisiscono dettagli sulle entità di dati B2B essenziali, come account, opportunità, campagne e altro ancora. Inoltre, Real-Time CDP B2B Edition consente di definire relazioni molti-a-uno tra questi schemi in modo che possano partecipare a casi d’uso di segmentazione avanzata.

>[!IMPORTANT]
>
>Per consentire agli schemi B2B di partecipare a [Profilo cliente in tempo reale](../../profile/home.md), è necessario avere accesso a Real-Time CDP B2B Edition.

In Real-Time CDP B2B Edition sono disponibili le seguenti classi standard:

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
