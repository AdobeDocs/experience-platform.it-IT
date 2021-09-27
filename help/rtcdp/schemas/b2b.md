---
title: Schemi in Real-time Customer Data Platform B2B Edition
description: Panoramica del ruolo degli schemi Experience Data Model (XDM) in Real-time Customer Data Platform B2B Edition.
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Schemi in Real-time Customer Data Platform B2B Edition (Beta)

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Real-time Customer Data Platform B2B Edition fornisce diverse classi [Experience Data Model (XDM) ](../../xdm/schema/composition.md#class) che acquisiscono dettagli sulle entità dati B2B essenziali, come account, opportunità, campagne e altro ancora. Inoltre, Real-time CDP B2B Edition ti consente di definire relazioni molti-a-uno tra questi schemi in modo che possano partecipare a casi di utilizzo di segmentazione avanzati.

Le seguenti classi standard sono fornite in Real-time CDP B2B Edition:

* [Account aziendale XDM](../../xdm/classes/b2b/business-account.md)
* [Relazione personale account aziendale XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campagna aziendale XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membri di una campagna aziendale XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Opportunità aziendali XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relazione personale opportunità di business XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Elenco di marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membri elenco marketing commerciale XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Per i passaggi su come creare una relazione molti-a-uno tra due schemi, consulta l’esercitazione su [definizione delle relazioni dello schema B2B](../../xdm/tutorials/relationship-b2b.md).

Se utilizzi una connessione sorgente B2B, puoi utilizzare uno strumento per generare automaticamente gli schemi richiesti e le relazioni tra di essi. Per ulteriori informazioni, consulta la guida sugli [spazi dei nomi B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) nella documentazione sulle sorgenti.
