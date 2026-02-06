---
title: Schemi in Real-Time Customer Data Platform B2B edition
description: Panoramica del ruolo degli schemi Experience Data Model (XDM) in Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 8%

---

# Schemi in Real-Time Customer Data Platform B2B edition

Adobe Real-Time Customer Data Platform B2B edition fornisce diverse [classi XDM (Experience Data Model) standard](../../xdm/schema/composition.md#class) che acquisiscono dettagli sulle entità di dati B2B essenziali, come account, opportunità, campagne e altro ancora. Inoltre, Real-Time CDP B2B edition consente di definire relazioni molti-a-uno tra questi schemi in modo che possano partecipare a casi di utilizzo di segmentazione avanzata.

>[!IMPORTANT]
>
>Gli schemi B2B sono disponibili per l&#39;utilizzo nelle applicazioni Experience Platform, ad esempio in [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition). <br/>È tuttavia necessario avere accesso a Real-Time CDP B2B edition per consentire agli schemi B2B (profili in) di partecipare a [Profilo cliente in tempo reale](../../profile/home.md).

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


La tabella seguente contiene informazioni sulla configurazione sottostante degli schemi B2B.

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Nome dello schema | Classe base | Gruppi di campi | [!DNL Profile] nello schema | Identità primaria | Spazio dei nomi identità primaria | Identità secondaria | Spazio dei nomi dell’identità secondaria | Relazione | Note |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Account B2B | [Account aziendale XDM](../../xdm/classes/b2b/business-account.md) | Dettagli dell’account aziendale XDM | Abilitata | `accountKey.sourceKey` nella classe base | Account B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Account B2B | <ul><li>`accountParentKey.sourceKey` nel gruppo di campi Dettagli account aziendale XDM</li><li>Proprietà di destinazione: `/accountKey/sourceKey`</li><li>Tipo: uno a uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li></ul> |  |
| Persona B2B | [Profilo individuale XDM](../../xdm/classes/individual-profile.md) | <ul><li>Dettagli persona aziendale XDM</li><li>Componenti della persona aziendale XDM</li><li>IdentityMap</li><li>Dettagli su consenso e preferenze</li></ul> | Abilitata | `b2b.personKey.sourceKey` nel gruppo di campi Dettagli persona aziendale XDM | Persona B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` del gruppo di campi Dettagli persona aziendale XDM</li><li>`workEmail.address` del gruppo di campi Dettagli persona aziendale XDM</ol></li> | <ol><li>Persona B2B</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` del gruppo di campi Componenti persona aziendale XDM</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: accountKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |  |
| Opportunità B2B | [Opportunità di business XDM](../../xdm/classes/b2b/business-opportunity.md) | Dettagli sull’opportunità di business XDM | Abilitata | `opportunityKey.sourceKey` nella classe base | Opportunità B2B | `extSourceSystemAudit.externalKey.sourceKey` nella classe base | Opportunità B2B | <ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione da schema di riferimento: opportunità</li></ul> |  |
| Relazione persona opportunità B2B | [Relazione della persona dell&#39;opportunità di business XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md) | Nessuna | Abilitata | `opportunityPersonKey.sourceKey` nella classe base | Relazione persona opportunità B2B | | | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: b2b.personKey.sourceKey</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione da schema di riferimento: opportunità</li></ul>**Seconda relazione**<ul><li>`opportunityKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: opportunità B2B </li><li>Namespace: Opportunità B2B </li><li>Proprietà di destinazione: `opportunityKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: opportunità</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |  |
| Campagna B2B | [Campagna aziendale XDM](../../xdm/classes/b2b/business-campaign.md) | Dettagli della campagna aziendale XDM | Abilitata | `campaignKey.sourceKey` nella classe base | Campagna B2B | | | | |
| Iscritto campagna B2B | [Membri della campagna aziendale XDM](../../xdm/classes/b2b/business-campaign-members.md) | Dettagli del membro della campagna aziendale XDM | Abilitata | `ccampaignMemberKey.sourceKey` nella classe base | Iscritto campagna B2B | | | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione dallo schema di riferimento: Campagne</li></ul>**Seconda relazione**<ul><li>`campaignKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: campagna B2B</li><li>Spazio dei nomi: campagna B2B</li><li>Proprietà di destinazione: `campaignKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Campaign</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |  |
| Elenco di marketing B2B | [Elenco marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list.md) | Nessuna | Abilitata | `marketingListKey.sourceKey` nella classe base | Elenco di marketing B2B | Nessuna | Nessuna | Nessuna | L&#39;elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un&#39;identità secondaria. |
| Iscritto elenco di marketing B2B | [Membri dell&#39;elenco di marketing aziendale XDM](../../xdm/classes/b2b/business-marketing-list-members.md) | Nessuna | Abilitata | `marketingListMemberKey.sourceKey` nella classe base | Iscritto elenco di marketing B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`PersonKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Persona</li><li>Nome di relazione da schema di riferimento: elenchi di marketing</li></ul>**Seconda relazione**<ul><li>`marketingListKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: elenco di marketing B2B</li><li>Spazio dei nomi: Elenco di marketing B2B</li><li>Proprietà di destinazione: `marketingListKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Elenco marketing</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> | Il membro dell&#39;elenco statico non è sincronizzato da [!DNL Salesforce] e pertanto non dispone di un&#39;identità secondaria. |
| Relazione della persona dell’account B2B | [Relazione della persona dell&#39;account aziendale XDM](../../xdm/classes/b2b/business-account-person-relation.md) | Mappa delle identità | Abilitata | `accountPersonKey.sourceKey` nella classe base | Relazione della persona dell’account B2B | Nessuna | Nessuna | **Prima relazione**<ul><li>`personKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: persona B2B</li><li>Spazio dei nomi: Persona B2B</li><li>Proprietà di destinazione: `b2b.personKey.SourceKey`</li><li>Nome di relazione dallo schema corrente: Persone</li><li>Nome di relazione da schema di riferimento: Account</li></ul>**Seconda relazione**<ul><li>`accountKey.sourceKey` nella classe base</li><li>Tipo: molti-a-uno</li><li>Schema di riferimento: account B2B</li><li>Spazio dei nomi: Account B2B</li><li>Proprietà di destinazione: `accountKey.sourceKey`</li><li>Nome di relazione dallo schema corrente: Account</li><li>Nome di relazione dallo schema di riferimento: Persone</li></ul> |  |

{style="table-layout:auto"}

