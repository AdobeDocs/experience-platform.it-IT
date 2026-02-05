---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketo;;home;popular topic;;marketo engagement;marketo
solution: Experience Platform
title: Connettore Marketo Engage
description: Questo documento fornisce una panoramica del connettore di origine di Marketo Engage, incluse informazioni sull’autenticazione, la mappatura e la latenza dei dati.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 659e873f9bccdbc0e52a1943a924dc70d3170e96
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 5%

---

# Connettore [!DNL Marketo Engage]

>[!IMPORTANT]
>
>È ora possibile utilizzare l&#39;origine [!DNL Marketo Engage] quando si esegue Adobe Experience Platform su Amazon Web Services (AWS). Experience Platform in esecuzione su AWS è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, consulta la [Panoramica multi-cloud di Experience Platform](../../../../landing/multi-cloud.md).

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. Puoi acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) è una soluzione completa per chi si occupa di lead management e B2B e intende trasformare le esperienze dei clienti coinvolgendoli in ogni fase di percorsi di acquisto complessi.

Con il connettore di origine [!DNL Marketo Engage], puoi portare dati B2B da [!DNL Marketo Engage] ad Experience Platform e tenerli aggiornati utilizzando applicazioni connesse ad Experience Platform.

>[!IMPORTANT]
>
>Devi avere accesso a [Adobe Real-Time Customer Data Platform B2B edition](../../../../rtcdp/b2b-overview.md) per utilizzare tutti i set di dati Marketo per la segmentazione con [Real-Time Customer Profile](../../../../profile/home.md). Senza Real-Time CDP B2B edition, puoi comunque utilizzare l’origine Marketo per portare i dati dai set di dati di persone e attività al Profilo cliente in tempo reale per la segmentazione.

Questo documento fornisce una panoramica del connettore di origine [!DNL Marketo Engage], incluse informazioni su come autenticare il connettore, come mappare i campi [!DNL Marketo Engage] su Experience Data Model (XDM) e sulla latenza dei dati del connettore.

## Impostare Adobe Organization Mapping

Prima di poter stabilire i set di mappatura per [!DNL Marketo Engage], è necessario configurare Adobe Organization Mapping. Per i passaggi dettagliati su come completare questa procedura, consulta la guida su [configurazione di Adobe Organization Mapping per [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Autentica il connettore [!DNL Marketo Engage]

Per connettere [!DNL Marketo Engage] ad Experience Platform, devi prima recuperare i valori per `munchkinId`, `clientId` e `clientSecret`.

Consulta i passaggi descritti nel documento [Autentica il connettore di origine di Marketo](./marketo-auth.md) per recuperare le credenziali.

## Configurare gli spazi dei nomi B2B e l’utility di generazione automatica dello schema

Quindi, utilizza lo spazio dei nomi B2B e l’utility di generazione automatica dello schema per configurare la Experience Platform Developer Console e l’ambiente Postman. Questo consente di popolare automaticamente gli spazi dei nomi e gli schemi B2B. Per istruzioni dettagliate, consulta la guida su [configurazione degli spazi dei nomi B2B e dell&#39;utilità di generazione automatica dello schema](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni che consentono di acquisire dati da origini di terze parti da utilizzare nei servizi Experience Platform a valle.

Il rispetto degli standard XDM consente di incorporare i dati in modo uniforme nell’ecosistema Experience Platform, semplificando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM e sul suo ruolo in Experience Platform, consulta la [Panoramica del sistema XDM](../../../../xdm/home.md).

## Mappatura campo da [!DNL Marketo Engage] a XDM

Per stabilire una connessione di origine tra [!DNL Marketo Engage] e Experience Platform, i campi dei dati di origine di Marketo devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Experience Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Marketo Engage] set di dati e Experience Platform, consulta:

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

## Latenza prevista di [!DNL Marketo Engage] dati su Experience Platform

La tabella seguente illustra la latenza prevista per l&#39;importazione di dati [!DNL Marketo Engage] in Experience Platform, in base alla natura dell&#39;acquisizione e alla destinazione desiderata:

| Destinazione | Latenza prevista |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 20 minuti |
| Data lake | &lt; 60 minuti |

>[!NOTE]
>
>Le cifre relative alla latenza sopra indicate rappresentano aspettative con un livello di affidabilità del 95%. Le latenze effettive variano e in alcuni casi si estendono oltre tali cifre.

## Passaggi successivi e risorse aggiuntive

Nella documentazione seguente vengono fornite ulteriori informazioni sulla creazione di una connessione di origine [!DNL Marketo Engage]:

* Per informazioni su come collegare i dati di [!DNL Marketo Engage] ad Experience Platform, leggere l&#39;esercitazione sulla [creazione di una connessione di origine [!DNL Marketo Engage] nell&#39;interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Per informazioni su come configurare gli schemi e acquisire dati di attività personalizzati, leggi l&#39;esercitazione su [creazione di una connessione di origine e di un flusso di dati per [!DNL Marketo Engage] dati di attività personalizzati](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
   * Per informazioni su come migrare il mapping ECID dal set di dati [!DNL Person] al set di dati [!DNL Activity], leggere la [guida alla migrazione della mappatura ECID](./migration.md).
* Per informazioni sulla configurazione sottostante degli spazi dei nomi e degli schemi B2B utilizzati con [!DNL Marketo Engage], leggere la documentazione relativa a [spazi dei nomi B2B e schemi](./marketo-namespaces.md).
* Per informazioni su come trovare il tuo ID munchkin [!DNL Marketo Engage] e generare le tue credenziali, consulta la [[!DNL Marketo Engage] guida all&#39;autenticazione](./marketo-auth.md).
* Per informazioni sulle regole di mappatura specifiche applicabili ai set di dati [!DNL Marketo Engage], consulta la documentazione sulle [[!DNL Marketo Engage] mappature dei campi](../mapping/marketo.md).
* Per informazioni generali su [!DNL Real-Time Customer Data Platform B2B Edition] e sulle relative funzionalità, consultare la documentazione in [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
