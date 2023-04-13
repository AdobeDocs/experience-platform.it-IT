---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilita profilo;abilita profilo
title: Guida all’API del profilo cliente in tempo reale
description: L’API Profilo cliente in tempo reale consente agli sviluppatori di esplorare e lavorare con i dati del profilo, tra cui visualizzare i profili, creare e aggiornare criteri di unione, esportare o dati del profilo di esempio ed eliminare i dati del profilo che non sono più necessari o che sono stati aggiunti per errore. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 8f61840ad60b7d24c980b218b6f742485f5ebfdd
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 2%

---

# Guida dell’API di [!DNL Real-Time Customer Profile]

[!DNL Real-Time Customer Profile] ti consente di visualizzare una visualizzazione olistica di ciascuno dei tuoi clienti in Adobe Experience Platform. [!DNL Profile] consente di consolidare dati cliente diversi da più canali, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account actionable e timestamp di ogni interazione con il cliente.

La [!DNL Real-Time Customer Profile] L’API include più endpoint, descritti di seguito. Per informazioni dettagliate, visita le singole guide dell’endpoint e fai riferimento alla sezione [guida introduttiva](getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

Per visualizzare tutti gli endpoint disponibili e le operazioni CRUD, visita il [Swagger di riferimento API del profilo cliente in tempo reale](https://www.adobe.com/go/profile-apis-en).

Per una guida sull’utilizzo di [!DNL Real-Time Customer Profile] i dati [!DNL Experience Platform] Interfaccia utente, fai riferimento al [Guida utente profilo](../ui/user-guide.md).

<!-- ## (Alpha) Computed attributes {#computed-attributes}

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha and is not available to all users. Documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization.

Each computed attribute contains an expression, or "rule", that evaluates incoming data and stores the resulting value in a profile attribute. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. These computed attribute values can then be viewed in a profile, used to create a segment, or accessed through a number of different access patterns.

You can create, view, edit, and delete computed attributes using the `config/computedAttributes` endpoint. To learn how to use computed attributes, refer to the [computed attributes overview](../computed-attributes/overview.md). For API operations, visit the [computed attributes API endpoint guide](../computed-attributes/ca-api.md). -->

## Proiezioni del bordo {#edge-projections}

Adobe Experience Platform consente la personalizzazione in tempo reale delle esperienze dei clienti rendendo i dati facilmente accessibili su server situati in posizioni strategiche denominati &quot;edge&quot;. La [!DNL Real-Time Customer Profile] L’API fornisce gli endpoint per l’utilizzo dei bordi tramite componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati proiettare su ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione. Per informazioni dettagliate sulle operazioni con le proiezioni dei bordi, visitare il [guida alle configurazioni di proiezione e agli endpoint di destinazione](edge-projections.md).

## Entità ([!DNL Profile] accesso) {#entities}

Tramite Adobe Experience Platform puoi accedere a [!DNL Real-Time Customer Profile] i dati che utilizzano le API RESTful o l’interfaccia utente. Per scoprire come accedere alle entità, più comunemente note come &quot;profili&quot;, utilizzando l’API, segui i passaggi descritti in [guida all’endpoint entità](entities.md). Per accedere ai profili utilizzando [!DNL Platform] Interfaccia utente, fai riferimento alla [Guida utente profilo](../ui/user-guide.md).

## Processi di esportazione ([!DNL Profile] esportazione) {#profile-export}

[!DNL Real-Time Customer Profile] i dati possono essere esportati in un set di dati per un’ulteriore elaborazione, ad esempio per esportare segmenti di pubblico per l’attivazione o gli attributi di profilo per il reporting. I processi di esportazione per i segmenti di pubblico fanno parte del [!DNL Adobe Experience Platform Segmentation Service] API, leggi [guida all’endpoint dei processi di esportazione per segmentazione](../../profile/api/export-jobs.md) per saperne di più. Per istruzioni dettagliate su come creare e gestire i processi di esportazione per gli attributi di profilo, visita il [guida all’endpoint dei processi di esportazione](export-jobs.md).

## Unisci criteri {#merge-policies}

Quando si riuniscono dati provenienti da più origini in [!DNL Experience Platform], i criteri di unione sono le regole che [!DNL Platform] utilizza per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare profili cliente individuali. Utilizzo della [!DNL Real-Time Customer Profile] È possibile creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la propria organizzazione. Per utilizzare i criteri di unione utilizzando l’API, visita [guida all’endpoint dei criteri di unione](merge-policies.md).

Per ulteriori informazioni sui criteri di unione e sul loro ruolo all’interno di Platform, consulta la sezione [panoramica dei criteri di unione](../merge-policies/overview.md).

## Stato del campione di anteprima ([!DNL Profile] anteprima) {#profile-preview}

Man mano che i dati vengono acquisiti in Platform, viene eseguito un processo di esempio per aggiornare il conteggio dei profili e altre metriche relative ai dati del profilo cliente in tempo reale. I risultati di questo processo di esempio possono essere visualizzati utilizzando `/previewsamplestatus` endpoint , parte dell’API del profilo cliente in tempo reale. Questo endpoint può essere utilizzato anche per elencare le distribuzioni dei profili per set di dati e namespace di identità, nonché per generare più rapporti al fine di acquisire visibilità nella composizione dell’archivio profili della tua organizzazione.  Per iniziare a utilizzare `/profilepreviewstatus` punto finale, fare riferimento alla [guida all’anteprima di un endpoint di stato di esempio](preview-sample-status.md).

## Processi del sistema di profili {#profile-system-jobs}

Dati abilitati per il profilo acquisiti in [!DNL Platform] è memorizzato in [!DNL Data Lake] nonché [!DNL Real-Time Customer Profile] archivio dati. Talvolta può essere necessario eliminare un set di dati o un batch [!DNL Profile] per rimuovere i dati che non sono più necessari o che sono stati aggiunti per errore. È necessario utilizzare l’API per creare un [!DNL Profile System Job], noto anche come &quot;[!DNL delete request]&quot;, che può essere modificato, monitorato o cancellato se necessario. Per scoprire come utilizzare le richieste di cancellazione utilizzando `/system/jobs` punto finale [!DNL Real-Time Customer Profile] API, segui i passaggi descritti in [guida all’endpoint dei processi del sistema di profilo](profile-system-jobs.md).

## Aggiornare gli attributi dei profili {#update-profile}

A volte può essere necessario aggiornare i dati nell’archivio profili della tua organizzazione. Ad esempio, potrebbe essere necessario correggere i record o modificare un valore di attributo. Questo può essere fatto tramite l’acquisizione batch e richiede un set di dati abilitato per il profilo configurato con un tag upsert. Per ulteriori informazioni su come configurare un set di dati per gli aggiornamenti degli attributi, consulta l’esercitazione per [abilitazione di un set di dati per profilo e aggiornamento](../../catalog/datasets/enable-upsert.md).

## Passaggi successivi {#next-steps}

Per iniziare a effettuare chiamate utilizzando [!DNL Real-Time Customer Profile] API, leggi [guida introduttiva](getting-started.md) quindi selezionare una delle guide dell&#39;endpoint per imparare a utilizzare specifiche [!DNL Profile]Endpoint correlati a . Per lavorare con [!DNL Profile] i dati che utilizzano [!DNL Experience Platform] Interfaccia utente, fai riferimento al [Guida utente al profilo cliente in tempo reale](../ui/user-guide.md).
