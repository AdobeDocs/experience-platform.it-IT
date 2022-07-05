---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketing da coinvolgere;marketo
solution: Experience Platform
title: Connettore Marketo Engage
topic-legacy: overview
description: Questo documento fornisce una panoramica del connettore di origine del Marketo Engage, con informazioni sull’autenticazione, la mappatura e la latenza dei dati.
exl-id: 063ec5d9-d643-4141-bf6d-878273f22b33
source-git-commit: 8b8e08adb5ff3498169c1702680ea44f3bebf5c5
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# [!DNL Marketo Engage] connettore

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[[!DNL Marketo Engage]](https://www.marketo.com/software/) (in appresso denominato &quot;[!DNL Marketo]&quot;) è una soluzione completa per i responsabili della gestione dei lead e per gli esperti di marketing B2B che desiderano trasformare le esperienze dei clienti impegnandosi in ogni fase dei percorsi di acquisto complessi.

Con la [!DNL Marketo] connettore di origine, puoi portare dati B2B da [!DNL Marketo] su Platform e aggiorna tali dati utilizzando le applicazioni connesse a Platform.

>[!IMPORTANT]
>
>Devi avere accesso a [Real-time Customer Data Platform B2B Edition](../../../../rtcdp/b2b-overview.md) affinché il Marketo Engage partecipi [Profilo cliente in tempo reale](../../../../profile/home.md).

Questo documento fornisce una panoramica del [!DNL Marketo] connettore di origine, comprese informazioni su come autenticare il connettore e su come eseguire la mappatura [!DNL Marketo] in Experience Data Model (XDM) e la latenza dati del connettore.

## Autentica il tuo [!DNL Marketo] connettore

Per connettersi [!DNL Marketo] su Platform, devi prima recuperare i valori per la `munchkinId`, `clientId`e `clientSecret`.

Vedi i passaggi descritti nel [Autenticazione del connettore sorgente Marketo](./marketo-auth.md) per recuperare le credenziali.

## Configurare la mappatura dell&#39;organizzazione Adobe

Prima di poter stabilire set di mappature per [!DNL Marketo], devi prima impostare Adobe Organization Mapping. Per i passaggi dettagliati su come completare questa procedura, consulta la guida su [configurazione di Adobe Organization Mapping per [!DNL Marketo]](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html).

## Imposta spazi dei nomi B2B e utilità di generazione automatica dello schema

Quindi, utilizza lo spazio dei nomi B2B e l’utility di generazione automatica dello schema per configurare la console per sviluppatori Platform e l’ambiente Postman. Questo ti consente di compilare automaticamente i namespace e gli schemi B2B. Per istruzioni dettagliate, consulta la guida su [configurazione dei namespace B2B e dell&#39;utility di generazione automatica dello schema](./marketo-namespaces.md)

## Experience Data Model (XDM)

XDM è una specifica documentata pubblicamente che fornisce strutture e definizioni comuni che ti consentono di acquisire dati da fonti di terze parti da utilizzare nei servizi della piattaforma a valle.

Il rispetto degli standard XDM consente l’integrazione uniforme dei dati nell’ecosistema della piattaforma, facilitando la distribuzione dei dati e la raccolta delle informazioni.

Per ulteriori informazioni su XDM e il suo ruolo in Platform, consulta la sezione [Panoramica del sistema XDM](../../../../xdm/home.md).

## Mappatura del campo da [!DNL Marketo] a XDM

Per stabilire una connessione sorgente tra [!DNL Marketo] e Platform, i campi dei dati di origine Marketo devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Marketo] set di dati e piattaforma:

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

## Latenza prevista di [!DNL Marketo] dati su Platform

La tabella seguente illustra la latenza prevista per il [!DNL Marketo] in Platform, in base alla natura dell’acquisizione e alla destinazione desiderata:

| Destinazione | Latenza prevista |
| ----------- | ---------------- |
| [!DNL Real-time Customer Profile] | &lt; 1 minuto |
| Lago dati | &lt; 60 minuti |

## Passaggi successivi e risorse aggiuntive

La seguente documentazione fornisce ulteriori informazioni sulla creazione di un [!DNL Marketo] connessione di origine:

* Per informazioni su come collegare le [!DNL Marketo] dati a Platform, consulta l’esercitazione su [creazione di un connettore sorgente Marketo nell’interfaccia utente](../../../tutorials/ui/create/adobe-applications/marketo.md).
* Per informazioni sulla configurazione sottostante per i namespace e gli schemi B2B utilizzati con [!DNL Marketo], consulta la documentazione di [namespace e schemi B2B](./marketo-namespaces.md).
* Per informazioni su come trovare le [!DNL Marketo] munchkin ID e la generazione delle tue credenziali, vedi [[!DNL Marketo] guida all’autenticazione](./marketo-auth.md).
* Per informazioni sulle regole di mappatura specifiche applicabili a [!DNL Marketo] set di dati, consulta la documentazione su [[!DNL Marketo] mappature dei campi](../mapping/marketo.md).
* Per informazioni generali su [!DNL Real-time Customer Data Platform B2B Edition] e le relative funzioni, consulta la documentazione [[!DNL Real-time Customer Data Platform B2B Edition]](../../../../rtcdp/b2b-overview.md).
