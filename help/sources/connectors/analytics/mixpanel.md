---
keywords: Experience Platform;home;argomenti popolari;
title: Panoramica Del Connettore Di Origine Mixpanel (Beta)
description: Scopri come collegare Mixpanel a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# (Beta) [!DNL Mixpanel]

>[!NOTE]
>
>Il [!DNL Mixpanel] sorgente in versione beta. Consulta la [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un’applicazione di analisi di terze parti. Il supporto per i provider di analisi include [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) è uno strumento di analisi dei prodotti che consente di acquisire dati sul modo in cui gli utenti interagiscono con un prodotto digitale. Mixpanel consente di analizzare questi dati di prodotto con rapporti semplici e interattivi che consentono di eseguire query e visualizzare i dati con pochi clic.

Le origini sfruttano [API di esportazione eventi Mixpanel > Scarica](https://developer.mixpanel.com/reference/raw-event-export) per scaricare i dati dell’evento così come vengono ricevuti e memorizzati in [!DNL Mixpanel], insieme a tutte le proprietà evento (tra cui `distinct_id`) e la marca temporale esatta in cui l&#39;evento è stato inviato all&#39;Experience Platform. Mixpanel utilizza token bearer come meccanismo di autenticazione per comunicare con l’API di esportazione degli eventi Mixpanel.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Autentica il tuo [!DNL Mixpanel] account

Questa sezione descrive i passaggi prerequisiti da completare per autenticare il tuo account e portare [!DNL Mixpanel] su Platform.

Per creare un [!DNL Mixpanel] connessione di origine e flusso di dati, devi prima disporre di un [!DNL Mixpanel] account. Se non disponi di un [!DNL Mixpanel] account, consulta [Registro mixpanel](https://mixpanel.com/register/) per creare il tuo account.

Dopo aver creato correttamente un [!DNL Mixpanel] account, passa a [!DNL Project Details] scheda in [!DNL Project Seettings] pagina di [!DNL Mixpanel] Interfaccia utente per recuperare l’ID del progetto e configurare il fuso orario.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Quindi, passa a [!DNL Service Accounts] scheda in [!DNL Project Settings] pagina in [!DNL Mixpanel] Interfaccia utente per recuperare le credenziali dell’account del servizio.

>[!TIP]
>
>Come best practice, seleziona un account di servizio che [non scade](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Account del servizio Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Infine, crea una piattaforma [schema](../../../xdm/schema/composition.md) richiesto per [!DNL Mixpanel Event Export API]. Per ulteriori informazioni sulle mappature richieste per lo schema, consulta la guida su [creazione di [!DNL Mixpanel] connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Crea schema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connetti [!DNL Mixpanel] alla piattaforma utilizzando le API

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Mixpanel] in Platform tramite API o l’interfaccia utente:

* [Creare una connessione di origine e un flusso di dati per [!DNL Mixpanel] utilizzo dell’API del servizio Flusso](../../tutorials/api/create/analytics/mixpanel.md)

## Connetti [!DNL Mixpanel] a Platform tramite l’interfaccia utente

* [Creare un [!DNL Mixpanel] connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/analytics/mixpanel.md)
* [Creare un flusso di dati per una connessione sorgente di successo del cliente nell’interfaccia utente](../../tutorials/ui/dataflow/analytics.md)
