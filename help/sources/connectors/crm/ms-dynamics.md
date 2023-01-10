---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Panoramica del connettore di origine Microsoft Dynamics
description: Scopri come collegare Microsoft Dynamics a Adobe Experience Platform utilizzando API o l’interfaccia utente.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 2%

---

# Connettore Microsoft Dynamics

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

[!DNL Experience Platform] fornisce il supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL Microsoft Dynamics].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Mappatura del campo da [!DNL Microsoft Dynamics] a XDM

Per stabilire una connessione sorgente tra [!DNL Microsoft Dynamics] e la piattaforma [!DNL Microsoft Dynamics] i campi dei dati di origine devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Microsoft Dynamics] set di dati e piattaforma:

- [Contatti](../adobe-applications/mapping/dynamics.md#contacts)
- [Lead](../adobe-applications/mapping/dynamics.md#leads)
- [Account](../adobe-applications/mapping/dynamics.md#accounts)
- [Opportunità](../adobe-applications/mapping/dynamics.md#opportunities)
- [Ruoli di contatto opportunità](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campagne](../adobe-applications/mapping/dynamics.md#campaigns)
- [Marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Membri dell’elenco di marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

La documentazione seguente fornisce informazioni su come connettersi [!DNL Microsoft Dynamics] a [!DNL Platform] utilizzando le API o l’interfaccia utente:

## Connetti [!DNL Microsoft Dynamics] a [!DNL Platform] utilizzo delle API

- [Creare una connessione base Microsoft Dynamics utilizzando l’API del servizio di flusso](../../tutorials/api/create/crm/ms-dynamics.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio di flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio di flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Microsoft Dynamics] a [!DNL Platform] utilizzo dell’interfaccia

- [Creare una connessione sorgente Microsoft Dynamics nell’interfaccia utente](../../tutorials/ui/create/crm/dynamics.md)
- [Creare un flusso di dati per una connessione CRM nell&#39;interfaccia utente](../../tutorials/ui/dataflow/crm.md)
