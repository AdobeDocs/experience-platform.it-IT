---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketo;marketo;home;popular topic;system;marketo engagement;marketo
solution: Experience Platform
title: Connettore Marketo Engage
description: Questo documento fornisce una panoramica del connettore di origine del Marketo Engage, incluse informazioni sull’autenticazione, la mappatura e la latenza dei dati.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 1%

---

# Connettore [!DNL Marketo Engage]

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) è una soluzione completa per chi si occupa di lead management e B2B e intende trasformare le esperienze dei clienti coinvolgendoli in ogni fase di percorsi di acquisto complessi.

Con il connettore di origine [!DNL Marketo Engage], puoi portare dati B2B da [!DNL Marketo Engage] a Platform e tenerli aggiornati utilizzando applicazioni connesse a Platform.

>[!IMPORTANT]
>
>Devi avere accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) per utilizzare tutti i set di dati di Marketo per la segmentazione con [Real-Time Customer Profile](../../../../profile/home.md). Senza Real-Time CDP B2B Edition, è ancora possibile utilizzare l’origine Marketo per portare i dati dai set di dati di persone e attività al Profilo cliente in tempo reale per la segmentazione.

Questo documento fornisce una panoramica del connettore di origine [!DNL Marketo Engage], incluse informazioni su come autenticare il connettore, come mappare i campi [!DNL Marketo Engage] su Experience Data Model (XDM) e sulla latenza dei dati del connettore.

## Imposta mapping organizzazione Adobe

Prima di poter stabilire i set di mappatura per [!DNL Marketo Engage], è necessario impostare Adobe Organization Mapping. Per i passaggi dettagliati su come completare questa procedura, consulta la guida su [configurazione di Adobe Organization Mapping per [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Autentica il connettore [!DNL Marketo Engage]

Per connettere [!DNL Marketo Engage] a Platform, devi prima recuperare i valori per `munchkinId`, `clientId` e `clientSecret`.

Consulta i passaggi descritti nel documento [Autentica il connettore di origine di Marketo](./marketo-auth.md) per recuperare le credenziali.

## Configurare gli spazi dei nomi B2B e l’utility di generazione automatica dello schema

Quindi, utilizza lo spazio dei nomi B2B e l’utility di generazione automatica dello schema per configurare la Platform Developer Console e l’ambiente Postman. Questo consente di popolare automaticamente gli spazi dei nomi e gli schemi B2B. Per istruzioni dettagliate, consulta la guida su [configurazione degli spazi dei nomi B2B e dell&#39;utilità di generazione automatica dello schema](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni che consentono di acquisire dati da origini di terze parti da utilizzare nei servizi Platform a valle.

Il rispetto degli standard XDM consente di incorporare i dati in modo uniforme nell’ecosistema della piattaforma, semplificando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM e sul suo ruolo in Platform, consulta la [panoramica del sistema XDM](../../../../xdm/home.md).

## Mappatura campo da [!DNL Marketo Engage] a XDM

Per stabilire una connessione di origine tra [!DNL Marketo Engage] e Platform, i campi dati di origine di Marketo devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Marketo Engage] set di dati e Platform, consulta:

* [Attività](../mapping/marketo.md#activities)
* [Programmi](../mapping/marketo.md#programs)
* [Iscrizioni al programma](../mapping/marketo.md#program-memberships)
* [Aziende](../mapping/marketo.md#companies)
* [Elenchi statici](../mapping/marketo.md#static-lists)
* [Appartenenze a elenchi statici](../mapping/marketo.md#static-list-memberships)
* [Account denominati](../mapping/marketo.md#named-accounts)
* [Opportunità](../mapping/marketo.md#opportunities)
* [Ruoli di contatto opportunità](../mapping/marketo.md#opportunity-contact-roles)
* [Persone](../mapping/marketo.md#persons)

## Latenza prevista di [!DNL Marketo Engage] dati su Platform

La tabella seguente illustra la latenza prevista per l&#39;importazione di dati [!DNL Marketo Engage] in Platform, in base alla natura dell&#39;acquisizione e alla destinazione desiderata:

| Destinazione | Latenza prevista |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 10 minuti |
| Data lake | &lt; 60 minuti |

>[!NOTE]
>
>Le cifre relative alla latenza sopra indicate rappresentano aspettative con un livello di affidabilità del 95%. Le latenze effettive variano e, in rari casi, possono superare di oltre il 50% tali cifre.

## Passaggi successivi e risorse aggiuntive

Nella documentazione seguente vengono fornite ulteriori informazioni sulla creazione di una connessione di origine [!DNL Marketo Engage]:

* Per informazioni su come collegare i dati di [!DNL Marketo Engage] a Platform, leggere l&#39;esercitazione sulla [creazione di una connessione di origine [!DNL Marketo Engage] nell&#39;interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Per informazioni su come configurare gli schemi e acquisire dati di attività personalizzati, leggi l&#39;esercitazione su [creazione di una connessione di origine e di un flusso di dati per [!DNL Marketo Engage] dati di attività personalizzati](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Per informazioni su come migrare il mapping ECID dal set di dati [!DNL Person] al set di dati [!DNL Activity], leggere la [guida alla migrazione della mappatura ECID](./migration.md).
* Per informazioni sulla configurazione sottostante degli spazi dei nomi e degli schemi B2B utilizzati con [!DNL Marketo Engage], leggere la documentazione relativa a [spazi dei nomi B2B e schemi](./marketo-namespaces.md).
* Per informazioni su come trovare il tuo ID munchkin [!DNL Marketo Engage] e generare le tue credenziali, consulta la [[!DNL Marketo Engage] guida all&#39;autenticazione](./marketo-auth.md).
* Per informazioni sulle regole di mappatura specifiche applicabili ai set di dati [!DNL Marketo Engage], consulta la documentazione sulle [[!DNL Marketo Engage] mappature dei campi](../mapping/marketo.md).
* Per informazioni generali su [!DNL Real-Time Customer Data Platform B2B Edition] e sulle relative funzionalità, consultare la documentazione in [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
