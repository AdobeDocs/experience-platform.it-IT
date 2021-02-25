---
keywords: ' Experience Platform;home;argomenti popolari;Real-time Customer Profile;Identity Service;'
solution: Experience Platform
title: Esercitazioni sul profilo cliente in tempo reale
topic: esercitazione
type: Esercitazione
description: Questo documento illustra i passaggi da seguire e fornisce collegamenti alle esercitazioni per completare ogni singolo flusso di lavoro.
translation-type: tm+mt
source-git-commit: 0aa59a5375757f81d63ac43d778ff2c7179d449b
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---


# Configurare gli [!DNL Real-time Customer Profile]

Per configurare [!DNL Real-time Customer Profile] per l&#39;organizzazione, è necessario completare più flussi di lavoro separati. Questo documento illustra i passaggi da seguire e fornisce collegamenti alle esercitazioni per completare ogni singolo flusso di lavoro.

Per saperne di più su [!DNL Real-time Customer Profile], iniziare leggendo la [Panoramica profilo](../profile/home.md).

## Panoramica dell’interfaccia utente del profilo cliente in tempo reale

Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi clienti, combinando dati da più canali tra cui dati online, offline, CRM e di terze parti.

**Questa guida è utile per:**
- Comprendere l&#39;interfaccia [!UICONTROL Profiles] e le funzioni disponibili.
- Visualizza e gestisci i dati del tuo profilo.

Per saperne di più, visita la [Guida utente del profilo cliente in tempo reale](../profile/ui/user-guide.md)

## API profilo cliente in tempo reale

L&#39;API del profilo cliente in tempo reale include più endpoint. Leggi la [Panoramica API profilo cliente in tempo reale](../profile/api/overview.md) per ulteriori informazioni su ciascuno degli endpoint disponibili e sui relativi casi di utilizzo.

Per saperne di più e ottenere i valori richiesti per eseguire le operazioni CRUD con l&#39;API Real-time Customer Profile, visita la [guida introduttiva](../profile/api/getting-started.md).

## Abilita uno schema per il servizio [!DNL Profile] e [!DNL Identity]

Prima di poter trasferire i dati in Adobe Experience Platform e utilizzarli per la creazione di [!DNL Real-time Customer Profiles], è necessario creare uno schema che fornisca la struttura dei dati che verranno acquisiti e che tale schema debba essere abilitato per l&#39;uso in [!DNL Profile] e Adobe Experience Platform [!DNL Identity Service].

**Questa guida è utile per:**
- Sfogliate gli schemi esistenti.
- Creare e assegnare un nome a uno schema.
- Aggiungete e definite i mixin XDM.
- Impostare i campi dello schema come campi di identità.
- Abilita profilo per lo schema.

Per istruzioni dettagliate sulla creazione di uno schema abilitato sia per [!DNL Profile] che per [!DNL Identity Service], fare riferimento alle esercitazioni per [creazione di uno schema mediante l&#39;API del Registro di sistema dello schema](../xdm/tutorials/create-schema-api.md) o [creazione di uno schema mediante l&#39;interfaccia utente di Generatore di schema](../xdm/tutorials/create-schema-ui.md).

## Configurare un dataset per [!DNL Profile] e [!DNL Identity]

Per iniziare l&#39;assimilazione dei dati in [!DNL Profile], è necessario disporre di un set di dati configurato correttamente per l&#39;uso con [!DNL Real-time Customer Profile] e [!DNL Identity Service].

**Questa guida è utile per:**
- Crea un set di dati abilitato per il profilo.
- Configurare i set di dati esistenti.
- Inserite i dati nel dataset.
- Confermate che il set di dati sia abilitato per il profilo e che utilizzi il servizio identità.

Per iniziare, segui l&#39;esercitazione API per [configurare un dataset per Profile and Identity](../profile/tutorials/dataset-configuration.md).

## Configurare i criteri di unione

Adobe Experience Platform consente di unire dati provenienti da più origini e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare tale visualizzazione unificata.

**Questa guida è utile per:**
- Creare nuovi criteri di unione.
- Gestire i criteri di unione esistenti.
- Impostare un criterio di unione predefinito per l&#39;organizzazione.
- Comprendere le violazioni dei criteri di unione.

Per utilizzare i criteri di unione nell&#39;interfaccia di [!DNL Platform], visitare la [guida utente dei criteri di unione](../profile/ui/merge-policies.md). Per utilizzare i criteri di unione utilizzando l&#39;API Profilo cliente in tempo reale, consultare la [guida per lo sviluppo dei criteri di unione](../profile/api/merge-policies.md).

## Configurare le proiezioni dei bordi

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche.  Adobe [!DNL Experience Platform] consente l&#39;accesso in tempo reale ai dati attraverso l&#39;uso di ciò che sono noti come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo.

**Questa guida è utile per:**
- Elenca, crea, visualizza, aggiorna ed elimina una destinazione di proiezione edge.
- Elenca e crea una configurazione di proiezione Edge.
- Comprendere i selettori.

Per ulteriori informazioni e per iniziare a lavorare con i bordi, fare riferimento alla [!DNL Real-time Customer Profile] Guida secondaria [sulle proiezioni dei bordi](../profile/api/edge-projections.md).

## Personalizzare la modalità di visualizzazione dei dati del profilo nell’interfaccia utente

Nell&#39;interfaccia utente del Experience Platform , puoi visualizzare e interagire con i dati del profilo cliente in tempo reale sotto forma di profili cliente. Le informazioni di profilo visualizzate nell’interfaccia sono state unite da più frammenti di profilo per formare una singola vista di ciascun cliente. Ciò include dettagli quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti mostrati nei profili possono essere modificati anche a livello organizzativo per visualizzare gli attributi di profilo preferiti.

**Questa guida è utile per:**
- Riordinare, ridimensionare, modificare e rimuovere le schede.
- Aggiungete gli attributi.
- Aggiungete una nuova scheda.
- Ripristina valori predefiniti.

Per ulteriori informazioni sulla personalizzazione dei dati del profilo, consultare la [Documentazione sulla personalizzazione del profilo](../profile/ui/profile-customization.md)

## Passaggi successivi

Dopo aver configurato [!DNL Real-time Customer Profile] per la propria organizzazione, potete iniziare ad aggiungere dati ai profili dei singoli clienti e a creare segmenti di pubblico in base ad attributi specifici del cliente. Per iniziare, consulta le seguenti esercitazioni:

- [Aggiungere dati al profilo cliente in tempo reale](../profile/tutorials/add-profile-data.md)
- [Creazione di un segmento](../segmentation/tutorials/create-a-segment.md)