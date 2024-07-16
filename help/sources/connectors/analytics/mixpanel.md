---
title: Panoramica del connettore Source Mixpanel
description: Scopri come collegare Mixpanel a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 7eb605f6-8580-40b7-a9b3-96b9c3444f5d
source-git-commit: 6f8abca8f0db8a559fe62e6c143f2d0506d3b886
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# [!DNL Mixpanel]

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un’applicazione di analisi di terze parti. Il supporto per i provider di analisi include [!DNL Mixpanel].

[[!DNL Mixpanel]](https://www.mixpanel.com) è uno strumento di analisi del prodotto che consente di acquisire dati sul modo in cui gli utenti interagiscono con un prodotto digitale. Mixpanel consente di analizzare questi dati di prodotto con rapporti semplici e interattivi che consentono di eseguire query e visualizzare i dati con pochi clic.

Le origini sfruttano [Mixpanel Event Export API > Download](https://developer.mixpanel.com/reference/raw-event-export) per scaricare i dati dell&#39;evento così come vengono ricevuti e memorizzati in [!DNL Mixpanel], insieme a tutte le proprietà dell&#39;evento (incluso `distinct_id`) e la marca temporale esatta dell&#39;invio dell&#39;evento all&#39;Experience Platform. Mixpanel utilizza token bearer come meccanismo di autenticazione per comunicare con l’API di esportazione degli eventi Mixpanel.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Autentica il tuo account [!DNL Mixpanel]

Questa sezione descrive i passaggi preliminari da completare per autenticare il tuo account e portare i tuoi dati di [!DNL Mixpanel] in Platform.

Per creare una connessione e un flusso di dati di origine [!DNL Mixpanel], è necessario disporre di un account [!DNL Mixpanel] valido. Se non disponi di un account [!DNL Mixpanel] valido, consulta la pagina del [registro Mixpanel](https://mixpanel.com/register/) per creare il tuo account.

Dopo aver creato correttamente un account [!DNL Mixpanel], passa alla scheda [!DNL Project Details] nella pagina [!DNL Project Seettings] dell&#39;interfaccia utente [!DNL Mixpanel] per recuperare l&#39;ID del progetto e configurare il fuso orario.

![mixpanel-project-settings](../../images/tutorials/create/mixpanel-export-events/mixpanel-project-settings.png)

Passare quindi alla scheda [!DNL Service Accounts] nella pagina [!DNL Project Settings] dell&#39;interfaccia utente [!DNL Mixpanel] per recuperare le credenziali dell&#39;account del servizio.

>[!TIP]
>
>Per best practice, selezionare un account di servizio [non scaduto](https://developer.mixpanel.com/reference/service-accounts#service-account-expiration).

![Account del servizio Mixpanel](../../images/tutorials/create/mixpanel-export-events/mixpanel-service-account.png)

Infine, crea uno [schema](../../../xdm/schema/composition.md) della piattaforma richiesto per [!DNL Mixpanel Event Export API]. Per ulteriori informazioni sui mapping richiesti per lo schema, vedere la guida alla [creazione di una connessione di origine [!DNL Mixpanel] nell&#39;interfaccia utente](../../tutorials/ui/create/analytics/mixpanel.md#additional-resources).

![Crea schema](../../images/tutorials/create/mixpanel-export-events/schema.png)

## Connetti [!DNL Mixpanel] a Platform tramite API

La documentazione seguente fornisce informazioni su come connettere [!DNL Mixpanel] a Platform tramite API o tramite l&#39;interfaccia utente:

* [Crea una connessione di origine e un flusso di dati per  [!DNL Mixpanel]  utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/analytics/mixpanel.md)

## Connetti [!DNL Mixpanel] a Platform tramite l&#39;interfaccia utente

* [Crea una connessione di origine  [!DNL Mixpanel]  nell&#39;interfaccia utente](../../tutorials/ui/create/analytics/mixpanel.md)
* [Creare un flusso di dati per una connessione sorgente di successo del cliente nell’interfaccia utente](../../tutorials/ui/dataflow/analytics.md)
