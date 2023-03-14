---
title: Schemi in Real-time Customer Data Platform B2B Edition
description: Panoramica del ruolo degli schemi Experience Data Model (XDM) in Adobe Real-time Customer Data Platform B2B Edition.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Schemi in Real-time Customer Data Platform B2B Edition

Adobe Real-time Customer Data Platform B2B Edition fornisce diversi standard [Classi Experience Data Model (XDM)](../../xdm/schema/composition.md#class) che acquisiscono dettagli sulle entità di dati B2B essenziali, come account, opportunità, campagne e altro ancora. Inoltre, Real-Time CDP B2B Edition consente di definire relazioni molti-a-uno tra questi schemi in modo che possano partecipare a casi d’uso di segmentazione avanzata.

>[!IMPORTANT]
>
>Per poter partecipare agli schemi B2B, è necessario avere accesso a Real-Time CDP B2B Edition [Profilo cliente in tempo reale](../../profile/home.md).

In Real-Time CDP B2B Edition sono disponibili le seguenti classi standard:

* [Account aziendale XDM](../../xdm/classes/b2b/business-account.md)
* [Relazione della persona dell’account aziendale XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campagna aziendale XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membri della campagna aziendale XDM](../../xdm/classes/b2b/business-campaign-members.md)
* [Opportunità di business XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relazione della persona dell’opportunità di business XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Elenco di marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list.md)
* [Membri dell’elenco di marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list-members.md)

Per informazioni su come gli schemi si adattano al flusso di lavoro B2B, consulta [tutorial end-to-end](../b2b-tutorial.md).

Per i passaggi su come creare una relazione molti-a-uno tra due schemi, consulta l’esercitazione su [definizione delle relazioni tra schemi B2B](../../xdm/tutorials/relationship-b2b.md).

Se utilizzi una connessione di origine B2B, puoi utilizzare uno strumento per generare automaticamente gli schemi richiesti e le relazioni tra di essi. Consulta la guida su [Spazi dei nomi B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) per ulteriori informazioni, consulta la documentazione sulle sorgenti.
