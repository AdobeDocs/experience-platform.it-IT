---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Panoramica del connettore di origine di Microsoft Dynamics
description: Scopri come connettere Microsoft Dynamics a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 2%

---

# Connettore Microsoft Dynamics

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[!DNL Experience Platform] fornisce supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider CRM include [!DNL Microsoft Dynamics].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Mappatura campi da [!DNL Microsoft Dynamics] a XDM

Per stabilire una connessione di origine tra [!DNL Microsoft Dynamics] e Platform, [!DNL Microsoft Dynamics] i campi dati di origine devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Microsoft Dynamics] Set di dati e Platform:

- [Contatti](../adobe-applications/mapping/dynamics.md#contacts)
- [Lead](../adobe-applications/mapping/dynamics.md#leads)
- [Account](../adobe-applications/mapping/dynamics.md#accounts)
- [Opportunità](../adobe-applications/mapping/dynamics.md#opportunities)
- [Ruoli di contatto opportunità](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campagne](../adobe-applications/mapping/dynamics.md#campaigns)
- [Elenco marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Membri di elenco marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Microsoft Dynamics] a [!DNL Platform] utilizzando le API o l’interfaccia utente:

## Connetti [!DNL Microsoft Dynamics] a [!DNL Platform] utilizzo delle API

- [Creare una connessione di base Microsoft Dynamics utilizzando l’API del servizio Flusso](../../tutorials/api/create/crm/ms-dynamics.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Microsoft Dynamics] a [!DNL Platform] utilizzo dell’interfaccia utente

- [Creare una connessione di origine Microsoft Dynamics nell’interfaccia utente](../../tutorials/ui/create/crm/dynamics.md)
- [Creare un flusso di dati per una connessione CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
