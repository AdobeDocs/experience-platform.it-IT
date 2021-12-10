---
title: Schemi in Real-time Customer Data Platform B2B Edition
description: Panoramica del ruolo degli schemi Experience Data Model (XDM) in Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 1a104d26b920082ee73178dd0ad7234ad43dec1a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Schemi in Real-time Customer Data Platform B2B Edition

Real-time Customer Data Platform B2B Edition fornisce diversi standard [Classi Experience Data Model (XDM)](../../xdm/schema/composition.md#class) che acquisiscono dettagli sulle entità dati B2B essenziali, come account, opportunità, campagne e altro ancora. Inoltre, Real-time CDP B2B Edition ti consente di definire relazioni molti-a-uno tra questi schemi in modo che possano partecipare a casi di utilizzo di segmentazione avanzati.

>[!IMPORTANT]
>
>È necessario avere accesso a Real-time CDP B2B Edition per consentire agli schemi B2B di partecipare [Profilo cliente in tempo reale](../../profile/home.md).

Le seguenti classi standard sono fornite in Real-time CDP B2B Edition:

* [Account aziendale XDM](../../xdm/classes/b2b/business-account.md)
* [Relazione personale account aziendale XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campagna aziendale XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membri di una campagna aziendale XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Opportunità aziendali XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relazione personale opportunità di business XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Elenco di marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membri elenco marketing commerciale XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Per capire come gli schemi si adattano al tuo flusso di lavoro B2B, consulta [esercitazione end-to-end](../b2b-tutorial.md).

Per i passaggi necessari per creare una relazione molti-a-uno tra due schemi, consulta l’esercitazione su [definizione delle relazioni dello schema B2B](../../xdm/tutorials/relationship-b2b.md).

Se utilizzi una connessione sorgente B2B, puoi utilizzare uno strumento per generare automaticamente gli schemi richiesti e le relazioni tra di essi. Consulta la guida su [namespace B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) nella documentazione di origine per ulteriori informazioni.
