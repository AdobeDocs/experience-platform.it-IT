---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketing da coinvolgere;marketo
solution: Experience Platform
title: Connettore Marketo Engage
topic-legacy: overview
description: Questo documento fornisce una panoramica del connettore di origine del Marketo Engage, con informazioni sull’autenticazione, la mappatura e la latenza dei dati.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 2844ffd7270ffcc2fba4da08dda1aea238cf6c9f
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# [!DNL Marketo Engage] connettore

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (in seguito denominato &quot;[!DNL Marketo]&quot;) è una soluzione completa per i responsabili della gestione dei lead e per gli esperti di marketing B2B che desiderano trasformare le esperienze dei clienti impegnandosi in ogni fase dei percorsi di acquisto complessi.

Con il connettore di origine [!DNL Marketo], puoi portare i dati B2B da [!DNL Marketo] a Platform e tenerli aggiornati utilizzando le applicazioni connesse a Platform.

Questo documento fornisce una panoramica del connettore di origine [!DNL Marketo], con informazioni su come autenticare il connettore, come mappare i campi [!DNL Marketo] a Experience Data Model (XDM) e sulla latenza dei dati del connettore.

## Autentica il connettore [!DNL Marketo]

Per connettersi a [!DNL Marketo] Platform, è innanzitutto necessario recuperare i valori per `munchkinId`, `clientId` e `clientSecret`.

Per recuperare le credenziali, consulta i passaggi descritti nel documento [Autentica il connettore di origine Marketo](./marketo-auth.md) .

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni che ti consentono di acquisire dati da fonti di terze parti da utilizzare nei servizi della piattaforma a valle.

Il rispetto degli standard XDM consente l’integrazione uniforme dei dati nell’ecosistema della piattaforma, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM e il suo ruolo in Platform, consulta la [Panoramica del sistema XDM](../../../../xdm/home.md).

## Mappatura dei campi da [!DNL Marketo] a XDM

Per stabilire una connessione di origine tra [!DNL Marketo] e Platform, i campi dei dati di origine Marketo devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra i set di dati [!DNL Marketo] e la piattaforma, consulta quanto segue:

* [Attività](../mapping/marketo.md#activities)
* [Programmi](../mapping/marketo.md#programs)
* [Partecipazioni al programma](../mapping/marketo.md#program-memberships)
* [Aziende](../mapping/marketo.md#companies)
* [Elenchi statici](../mapping/marketo.md#static-lists)
* [appartenenze a elenchi statici](../mapping/marketo.md#static-list-memberships)
* [Account denominati](../mapping/marketo.md#named-accounts)
* [Opportunità](../mapping/marketo.md#opportunities)
* [Ruoli di contatto opportunità](../mapping/marketo.md#opportunity-contact-roles)
* [Persone](../mapping/marketo.md#persons)

## Latenza prevista dei dati [!DNL Marketo] su Platform

La tabella seguente illustra la latenza prevista per l’inserimento di dati [!DNL Marketo] in Platform, in base alla natura dell’acquisizione e alla destinazione desiderata:

| Destinazione | Latenza prevista |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minuto |
| Lago dati | &lt; 60 minuti |

## Passaggi successivi e risorse aggiuntive

La seguente documentazione fornisce ulteriori informazioni sulla creazione di una connessione sorgente [!DNL Marketo]:

* Per informazioni su come collegare i dati [!DNL Marketo] a Platform, consulta l’esercitazione su [creazione di un connettore sorgente Marketo nell’interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Per informazioni sulla configurazione sottostante per i namespace e gli schemi B2B utilizzati con [!DNL Marketo], consulta la documentazione relativa a [namespace e schemi B2B](./marketo-namespaces.md).
* Per informazioni su come trovare il tuo [!DNL Marketo] munchkin ID e generare le tue credenziali, consulta la [[!DNL Marketo] guida all&#39;autenticazione](./marketo-auth.md).
* Per informazioni sulle regole di mappatura specifiche applicabili ai set di dati [!DNL Marketo], consulta la documentazione sulle mappature dei campi [[!DNL Marketo] a2/>.](../mapping/marketo.md)
* Per informazioni generali su [!DNL Real-time Customer Data Platform B2B Edition] e sulle relative funzioni, consulta la documentazione su [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
