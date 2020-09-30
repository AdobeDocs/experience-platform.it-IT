---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Esercitazioni sul profilo cliente in tempo reale
topic: tutorial
type: Tutorial
description: Questo documento illustra i passaggi da seguire e fornisce collegamenti alle esercitazioni per completare ogni singolo flusso di lavoro.
translation-type: tm+mt
source-git-commit: 844ef4a0131e41d3a7a3da319ccf7f8d5cf1f40d
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---


# Configura [!DNL Real-time Customer Profile] e [!DNL Identity Service]

Per configurare [!DNL Real-time Customer Profile] la tua organizzazione, devi completare più flussi di lavoro separati. Questo documento illustra i passaggi da seguire e fornisce collegamenti alle esercitazioni per completare ogni singolo flusso di lavoro.

Per saperne di più, [!DNL Real-time Customer Profile]iniziare leggendo la panoramica [del](../profile/home.md)profilo.

## Panoramica dell’interfaccia utente del profilo cliente in tempo reale

Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi clienti, combinando dati da più canali tra cui dati online, offline, CRM e di terze parti.

**Questa guida è utile per:**
- Comprendere l’ [!UICONTROL Profiles] interfaccia utente e le funzioni disponibili.
- Visualizza e gestisci i dati del tuo profilo.

Per saperne di più, consulta la guida utente del profilo cliente [in tempo reale](../profile/ui/user-guide.md)

## API profilo cliente in tempo reale

L&#39;API del profilo cliente in tempo reale include più endpoint. Il profilo consente di consolidare diversi dati dei clienti da più canali, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente. Per ulteriori informazioni su ciascuno degli endpoint disponibili e sui relativi casi di utilizzo, consulta la panoramica [dell&#39;API del profilo cliente in tempo](../profile/api/overview.md) reale.

**Sono disponibili le seguenti guide per gli sviluppatori API:**
- [Attributi calcolati (alfa) ](../profile/api/computed-attributes.md) - Informazioni sui casi di utilizzo per gli attributi calcolati e su come configurare, accedere, aggiornare ed eliminare un attributo calcolato.
- [Proiezioni](../profile/api/edge-projections.md) Edge - Scopri come creare, visualizzare, aggiornare, eliminare ed elencare le destinazioni di proiezione. Inoltre, questo documento contiene informazioni sull&#39;elencazione e sulla creazione di configurazioni di proiezione e fornisce esempi per l&#39;utilizzo di Selettori.
- [Entità (accesso profilo)](../profile/api/entities.md) - Informazioni su come accedere ai dati del profilo in base all&#39;identità o a un elenco di identità. Inoltre, scopri come accedere agli eventi delle serie temporali per più profili utilizzando identità, un singolo profilo per identità e accedere a più entità dello schema.
- [Processi di esportazione (esportazione profilo)](../profile/api/export-jobs.md) - Informazioni su come creare, visualizzare, monitorare e annullare i processi di esportazione.
- [Unisci criteri](../profile/api/merge-policies.md) : informazioni sui componenti dei criteri di unione e su come accedere, creare, aggiornare ed eliminare un criterio di unione.
- [Anteprima dello stato del campione (Anteprima profilo)](../profile/api/preview-sample-status.md) - Informazioni su come visualizzare lo stato dell’ultimo esempio, la distribuzione del profilo di elenco per set di dati e la distribuzione del profilo di elenco per namespace.
- [Processi di sistema del profilo (richieste di eliminazione)](../profile/api/profile-system-jobs.md) - Informazioni su come visualizzare, creare e rimuovere una richiesta di eliminazione per un set di dati o un batch nell&#39;archivio profili.

Per saperne di più e ottenere i valori richiesti per eseguire le operazioni CRUD con l&#39;API del profilo cliente in tempo reale, visita la guida [](../profile/api/getting-started.md)introduttiva.

## Abilita uno schema per [!DNL Profile] e [!DNL Identity] Servizio

Per poter acquisire i dati in Adobe Experience Platform e utilizzarli per la creazione di [!DNL Real-time Customer Profiles], è necessario creare uno schema che fornisca la struttura dei dati che verranno acquisiti e che tale schema debba essere abilitato per l&#39;uso in [!DNL Profile] e Adobe Experience Platform [!DNL Identity Service].

**Questa guida è utile per:**
- Sfogliate gli schemi esistenti.
- Creare e assegnare un nome a uno schema.
- Aggiungete e definite i mixin XDM.
- Impostare i campi dello schema come campi di identità.
- Abilita profilo per lo schema.

Per istruzioni dettagliate sulla creazione di uno schema abilitato per entrambi [!DNL Profile] e [!DNL Identity Service], fare riferimento alle esercitazioni per la [creazione di uno schema mediante l&#39;API](../xdm/tutorials/create-schema-api.md) del Registro di sistema dello schema o [la creazione di uno schema mediante l&#39;interfaccia](../xdm/tutorials/create-schema-ui.md)del Generatore di schemi.

## Configurare un dataset per [!DNL Profile] e [!DNL Identity]

Per iniziare l&#39;assimilazione dei dati in [!DNL Profile], è necessario disporre di un set di dati configurato correttamente per l&#39;utilizzo con [!DNL Real-time Customer Profile] e [!DNL Identity Service].

**Questa guida è utile per:**
- Crea un set di dati abilitato per il profilo.
- Configurare i set di dati esistenti.
- Inserite i dati nel dataset.
- Confermate che il set di dati sia abilitato per il profilo e che utilizzi il servizio identità.

Per iniziare, segui l&#39;esercitazione API per [configurare un dataset per Profilo e Identità](../profile/tutorials/dataset-configuration.md).

## Configurare i criteri di unione

Adobe Experience Platform consente di unire dati provenienti da più origini e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole che [!DNL Platform] utilizzano per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare tale visualizzazione unificata.

**Questa guida è utile per:**
- Creare nuovi criteri di unione.
- Gestire i criteri di unione esistenti.
- Impostare un criterio di unione predefinito per l&#39;organizzazione.
- Comprendere le violazioni dei criteri di unione.

Per utilizzare i criteri di unione nell&#39; [!DNL Platform] interfaccia utente, consultare la guida [utente dei criteri di](../profile/ui/merge-policies.md)unione. Per lavorare con i criteri di unione utilizzando l&#39;API Profilo cliente in tempo reale, consulta la guida [per gli sviluppatori dei criteri di](../profile/api/merge-policies.md)unione.

## Configurare le proiezioni dei bordi

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche.  Adobe [!DNL Experience Platform] consente l&#39;accesso in tempo reale ai dati attraverso l&#39;uso di ciò che sono noti come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo.

**Questa guida è utile per:**
- Elenca, crea, visualizza, aggiorna ed elimina una destinazione di proiezione edge.
- Elenca e crea una configurazione di proiezione Edge.
- Comprendere i selettori.

Per ulteriori informazioni e per iniziare a lavorare con i bordi, fate riferimento alla [!DNL Real-time Customer Profile] guida [secondaria API sulle proiezioni](../profile/api/edge-projections.md)edge.

## Personalizzare la modalità di visualizzazione dei dati del profilo nell’interfaccia utente

Nell&#39;interfaccia utente del Experience Platform , puoi visualizzare e interagire con i dati del profilo cliente in tempo reale sotto forma di profili cliente. Le informazioni di profilo visualizzate nell’interfaccia sono state unite da più frammenti di profilo per formare una singola vista di ciascun cliente. Ciò include dettagli quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti mostrati nei profili possono essere modificati anche a livello organizzativo per visualizzare gli attributi di profilo preferiti.

**Questa guida è utile per:**
- Riordinare, ridimensionare, modificare e rimuovere le schede.
- Aggiungete gli attributi.
- Aggiungete una nuova scheda.
- Ripristina valori predefiniti.

Per ulteriori informazioni sulla personalizzazione dei dati del profilo, consulta la documentazione sulla personalizzazione del [profilo](../profile/ui/profile-customization.md)

## Passaggi successivi

Dopo aver configurato [!DNL Real-time Customer Profile] la propria organizzazione, puoi iniziare ad aggiungere dati ai profili dei clienti individuali e a creare segmenti di pubblico in base a attributi specifici del cliente. Per iniziare, consulta le seguenti esercitazioni:

- [Aggiungere dati al profilo cliente in tempo reale](../profile/tutorials/add-profile-data.md)
- [Creazione di un segmento](../segmentation/tutorials/create-a-segment.md)