---
keywords: Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics;Dynamics
solution: Experience Platform
title: Panoramica del connettore Source di Microsoft Dynamics
description: Scopri come connettere Microsoft Dynamics a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 6ca162ce-2016-4270-b741-301cf4230233
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 3%

---

# Connettore Microsoft Dynamics

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform]. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

[!DNL Experience Platform] fornisce supporto per l&#39;acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL Microsoft Dynamics].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Mappatura campo da [!DNL Microsoft Dynamics] a XDM

Per stabilire una connessione di origine tra [!DNL Microsoft Dynamics] e Platform, i campi dati di origine [!DNL Microsoft Dynamics] devono essere mappati sui campi XDM di destinazione appropriati prima di essere acquisiti in Platform.

Per informazioni dettagliate sulle regole di mappatura dei campi tra [!DNL Microsoft Dynamics] set di dati e Platform, consulta:

- [Contatti](../adobe-applications/mapping/dynamics.md#contacts)
- [Lead](../adobe-applications/mapping/dynamics.md#leads)
- [Account](../adobe-applications/mapping/dynamics.md#accounts)
- [Opportunità](../adobe-applications/mapping/dynamics.md#opportunities)
- [Ruoli di contatto opportunità](../adobe-applications/mapping/dynamics.md#opportunity-contact-roles)
- [Campagne](../adobe-applications/mapping/dynamics.md#campaigns)
- [Elenco marketing](../adobe-applications/mapping/dynamics.md#marketing-list)
- [Membri elenco di marketing](../adobe-applications/mapping/dynamics.md#marketing-list-members)

La documentazione seguente fornisce informazioni su come connettere [!DNL Microsoft Dynamics] a [!DNL Platform] tramite API o l&#39;interfaccia utente:

## Connetti [!DNL Microsoft Dynamics] a [!DNL Platform] tramite API

- [Creare una connessione di base Microsoft Dynamics utilizzando l’API del servizio Flusso](../../tutorials/api/create/crm/ms-dynamics.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Microsoft Dynamics] a [!DNL Platform] tramite l&#39;interfaccia utente

- [Creare una connessione di origine Microsoft Dynamics nell’interfaccia utente](../../tutorials/ui/create/crm/dynamics.md)
- [Creare un flusso di dati per una connessione CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
