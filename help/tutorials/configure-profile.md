---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esercitazioni sul profilo cliente in tempo reale
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Configurare il profilo cliente e il servizio identità in tempo reale

Per configurare il profilo cliente in tempo reale per la tua organizzazione, devi completare più flussi di lavoro separati. Questo documento illustra i passaggi da seguire e fornisce collegamenti alle esercitazioni per completare ogni singolo flusso di lavoro. Per saperne di più sul profilo cliente in tempo reale, leggete la panoramica [del](../profile/home.md)profilo.

## Abilita schema per profilo e identità

Prima di poter trasferire i dati in Adobe Experience Platform e utilizzarli per la creazione di profili cliente in tempo reale, è necessario creare uno schema che fornisca la struttura dei dati che verranno acquisiti e che tale schema debba essere abilitato per l&#39;uso in Profile e Adobe Experience Platform Identity Service. Per istruzioni dettagliate sulla creazione di uno schema abilitato sia per il servizio Profilo che per il servizio identità, fare riferimento alle esercitazioni per la [creazione di uno schema tramite l&#39;API](../xdm/tutorials/create-schema-api.md) del Registro di sistema dello schema o per la [creazione di uno schema tramite l&#39;interfaccia utente](../xdm/tutorials/create-schema-ui.md)di Generatore di schemi.

## Configurare un dataset per Profilo e Identità

Per iniziare a assimilare i dati in Profile, devi disporre di un set di dati configurato per l’uso con Real-time Customer Profile and Identity Service (Profilo cliente e Servizio identità in tempo reale). Per iniziare, segui l’esercitazione [](../profile/tutorials/dataset-configuration.md)Configura un dataset per Profilo e Identità.

## Configurare i criteri di unione

Adobe Experience Platform consente di unire dati provenienti da più origini e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole utilizzate dalla Piattaforma per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare tale visualizzazione unificata. Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per utilizzare i criteri di unione nell&#39;interfaccia utente della piattaforma, consultare la guida [utente relativa ai criteri di](../profile/ui/merge-policies.md)unione. Per lavorare con i criteri di unione utilizzando l&#39;API Profilo cliente in tempo reale, consulta la guida [per gli sviluppatori dei criteri di](../profile/api/merge-policies.md)unione.

## Configurare le proiezioni dei bordi

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche. Adobe Experience Platform consente l&#39;accesso in tempo reale ai dati tramite l&#39;utilizzo di ciò che sono noti come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo. Per ulteriori informazioni e per iniziare a lavorare con i bordi, consulta la [guida secondaria API Profilo cliente in tempo reale sulle proiezioni](../profile/api/edge-projections.md)edge.

## Passaggi successivi

Dopo aver configurato il profilo cliente in tempo reale per la tua organizzazione, puoi iniziare ad aggiungere dati ai profili cliente individuali e creare segmenti di pubblico in base a attributi cliente specifici. Per iniziare, consulta le seguenti esercitazioni:

* [Aggiungere dati al profilo cliente in tempo reale](../profile/tutorials/add-profile-data.md)
* [Creazione di un segmento](../segmentation/tutorials/create-a-segment.md)