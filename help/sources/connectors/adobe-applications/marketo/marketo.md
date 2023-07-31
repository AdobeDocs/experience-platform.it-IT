---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketo;marketo;home;popular topic;system;marketo engagement;marketo
solution: Experience Platform
title: Connettore Marketo Engage
description: Questo documento fornisce una panoramica del connettore di origine del Marketo Engage, incluse informazioni sull’autenticazione, la mappatura e la latenza dei dati.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: f0a3486fc7df7b08a11ec7bfb041841bc2c1c9a3
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 5%

---

# [!DNL Marketo Engage] connettore

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) è una soluzione completa per i responsabili della gestione dei lead e per gli esperti di marketing B2B che desiderano trasformare l’esperienza dei clienti seguendo tutte le fasi dei processi di acquisto più complessi.

Con il [!DNL Marketo Engage] connettore di origine, puoi importare dati B2B da [!DNL Marketo Engage] su Platform e di tenerli aggiornati utilizzando le applicazioni connesse a Platform.

>[!IMPORTANT]
>
>Devi avere accesso a [Adobe Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) per utilizzare tutti i set di dati di Marketo per la segmentazione con [Profilo cliente in tempo reale](../../../../profile/home.md). Senza Real-Time CDP B2B Edition, è ancora possibile utilizzare l’origine Marketo per portare i dati dai set di dati di persone e attività al Profilo cliente in tempo reale per la segmentazione.

Questo documento fornisce una panoramica della [!DNL Marketo Engage] connettore di origine, incluse informazioni su come autenticare il connettore, come mappare [!DNL Marketo Engage] campi in Experience Data Model (XDM) e la latenza dei dati del connettore.

## Imposta mapping organizzazione Adobe

Prima di poter stabilire i set di mappatura per [!DNL Marketo Engage], devi prima impostare Adobe Organization Mapping. Per i passaggi dettagliati su come completare questa procedura, consulta la guida su [impostazione di Adobe Organization Mapping per [!DNL Marketo Engage]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Autentica il tuo [!DNL Marketo Engage] connettore

Per connettersi [!DNL Marketo Engage] in Platform, devi prima recuperare i valori per `munchkinId`, `clientId`, e `clientSecret`.

Consulta i passaggi descritti in [Autentica il connettore di origine Marketo](./marketo-auth.md) per recuperare le credenziali.

## Configurare gli spazi dei nomi B2B e l’utility di generazione automatica dello schema

Quindi, utilizza lo spazio dei nomi B2B e l’utility di generazione automatica dello schema per configurare la Platform Developer Console e l’ambiente Postman. Questo consente di popolare automaticamente gli spazi dei nomi e gli schemi B2B. Per istruzioni dettagliate, consulta la guida [configurazione degli spazi dei nomi B2B e dell’utility di generazione automatica dello schema](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni che consentono di acquisire dati da origini di terze parti da utilizzare nei servizi Platform a valle.

Il rispetto degli standard XDM consente di incorporare i dati in modo uniforme nell’ecosistema della piattaforma, semplificando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM e sul suo ruolo in Platform, consulta la sezione [Panoramica del sistema XDM](../../../../xdm/home.md).

## Mappatura campi da [!DNL Marketo Engage] a XDM

Per stabilire una connessione di origine tra [!DNL Marketo Engage] e Platform, i campi dei dati di origine di Marketo devono essere mappati sui rispettivi campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Marketo Engage] Set di dati e Platform:

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

La tabella seguente illustra la latenza prevista per l&#39;introduzione di [!DNL Marketo Engage] dati in Platform, in base alla natura dell’acquisizione e alla destinazione desiderata:

| Destinazione | Latenza prevista |
| ----------- | ---------------- |
| [!DNL Real-Time Customer Profile] | &lt; 1 minuto |
| Data lake | &lt; 60 minuti |

## Passaggi successivi e risorse aggiuntive

La documentazione seguente fornisce ulteriori informazioni sulla creazione di un’ [!DNL Marketo Engage] connessione di origine:

* Per informazioni su come collegare [!DNL Marketo Engage] su Platform, leggi l’esercitazione su [creazione di [!DNL Marketo Engage] connessione sorgente nell’interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
   * Per informazioni su come impostare gli schemi e acquisire dati di attività personalizzati, leggi l’esercitazione su [creazione di una connessione sorgente e di un flusso di dati per [!DNL Marketo Engage] dati attività personalizzati](../../../tutorials/ui/create/adobe-applications/marketo-custom-activities.md)
* Per informazioni sulla configurazione sottostante degli spazi dei nomi B2B e degli schemi utilizzati con [!DNL Marketo Engage], leggi la documentazione di [Spazi dei nomi e schemi B2B](./marketo-namespaces.md).
* Per informazioni su come trovare [!DNL Marketo Engage] ID munchkin e generazione delle credenziali, leggi la [[!DNL Marketo Engage] guida all’autenticazione](./marketo-auth.md).
* Per informazioni sulle regole di mappatura specifiche applicabili a [!DNL Marketo Engage] set di dati, consulta la documentazione su [[!DNL Marketo Engage] mappature campi](../mapping/marketo.md).
* Per informazioni generali su [!DNL Real-Time Customer Data Platform B2B Edition] e le relative funzioni, consulta la documentazione su [[!DNL Real-Time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
