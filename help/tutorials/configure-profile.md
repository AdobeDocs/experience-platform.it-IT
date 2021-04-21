---
keywords: Experience Platform;home;argomenti popolari;Profilo cliente in tempo reale;servizio Identity;
solution: Experience Platform
title: Esercitazioni sul profilo cliente in tempo reale
topic-legacy: tutorial
type: Tutorial
description: Questo documento illustra i passaggi necessari e fornisce collegamenti alle esercitazioni per il completamento di ogni singolo flusso di lavoro.
exl-id: cda6e7a7-9498-454c-94df-c6271a5a4fd4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# Configurare gli [!DNL Real-time Customer Profile]

Per configurare [!DNL Real-time Customer Profile] per la tua organizzazione, devi completare più flussi di lavoro separati. Questo documento illustra i passaggi necessari e fornisce collegamenti alle esercitazioni per il completamento di ogni singolo flusso di lavoro.

Per ulteriori informazioni su [!DNL Real-time Customer Profile], inizia leggendo la [Panoramica profilo](../profile/home.md).

## Panoramica dell’interfaccia utente del profilo cliente in tempo reale

Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi singoli clienti, combinando dati provenienti da più canali tra cui online, offline, CRM e dati di terze parti.

**Questa guida ti aiuterà a:**
- Comprendere l’ [!UICONTROL Profiles] interfaccia utente e le funzioni disponibili.
- Visualizza e gestisci i dati del tuo profilo.

Per ulteriori informazioni, visita la [guida utente Profilo cliente in tempo reale](../profile/ui/user-guide.md)

## API del profilo cliente in tempo reale

L’API del profilo cliente in tempo reale include più endpoint. Per ulteriori informazioni su ciascuno degli endpoint disponibili e sui relativi casi d’uso, consulta la [Panoramica API del profilo cliente in tempo reale](../profile/api/overview.md) .

Per ulteriori informazioni e ottenere i valori richiesti per l&#39;esecuzione delle operazioni CRUD con l&#39;API Profilo cliente in tempo reale, visita la [guida introduttiva](../profile/api/getting-started.md).

## Abilitare uno schema per il servizio [!DNL Profile] e [!DNL Identity]

Prima di poter acquisire i dati in Adobe Experience Platform e utilizzarli nella creazione di [!DNL Real-time Customer Profiles], è necessario creare uno schema per fornire la struttura dei dati che verranno acquisiti e tale schema deve essere abilitato per l’utilizzo in [!DNL Profile] e Adobe Experience Platform [!DNL Identity Service].

**Questa guida ti aiuterà a:**
- Sfoglia gli schemi esistenti.
- Creare e denominare uno schema.
- Aggiungi e definisci i mixin XDM.
- Imposta i campi dello schema come campi di identità.
- Abilita profilo per il tuo schema.

Per istruzioni dettagliate sulla creazione di uno schema abilitato sia per [!DNL Profile] che per [!DNL Identity Service], consulta le esercitazioni per [creazione di uno schema tramite l’API del Registro di sistema dello schema](../xdm/tutorials/create-schema-api.md) o [creazione di uno schema tramite l’interfaccia utente del Generatore di schema](../xdm/tutorials/create-schema-ui.md).

## Configura un set di dati per [!DNL Profile] e [!DNL Identity]

Per iniziare ad acquisire i dati in [!DNL Profile], devi disporre di un set di dati configurato correttamente per l’utilizzo con [!DNL Real-time Customer Profile] e [!DNL Identity Service].

**Questa guida ti aiuterà a:**
- Crea un set di dati abilitato per Profilo.
- Configura i set di dati esistenti.
- Inserire dati nel set di dati.
- Conferma che il set di dati sia abilitato per il profilo e utilizzi il servizio Identity.

Per iniziare, segui l’esercitazione API per [configurare un set di dati per Profilo e identità](../profile/tutorials/dataset-configuration.md).

## Configurare i criteri di unione

Adobe Experience Platform consente di unire dati provenienti da più sorgenti e combinarli per visualizzare una visione completa di ciascuno dei singoli clienti. Quando si riuniscono questi dati, i criteri di unione sono le regole utilizzate da [!DNL Platform] per determinare in che modo i dati verranno definiti come prioritari e quali dati verranno combinati per creare tale visualizzazione unificata.

**Questa guida ti aiuterà a:**
- Creare nuovi criteri di unione.
- Gestire i criteri di unione esistenti.
- Impostare un criterio di unione predefinito per l&#39;organizzazione.
- Comprendere le violazioni dei criteri di unione.

Per utilizzare i criteri di unione nell&#39;interfaccia utente [!DNL Platform], visita la [guida utente dei criteri di unione](../profile/ui/merge-policies.md). Per utilizzare i criteri di unione utilizzando l&#39;API Profilo cliente in tempo reale, consulta la [guida per gli sviluppatori dei criteri di unione](../profile/api/merge-policies.md).

## Configurare le proiezioni edge

Al fine di promuovere in tempo reale esperienze coordinate, coerenti e personalizzate per i clienti su più canali, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano cambiamenti. L’Adobe [!DNL Experience Platform] consente l’accesso in tempo reale ai dati tramite l’utilizzo di elementi noti come edge. Un server perimetrale è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui i dati saranno inviati, e una configurazione di proiezione che definisce le informazioni specifiche che saranno rese disponibili sul bordo.

**Questa guida ti aiuterà a:**
- Elencare, creare, visualizzare, aggiornare ed eliminare una destinazione di proiezione Edge.
- Elenca e crea una configurazione di proiezione edge.
- Comprendere i selettori.

Per ulteriori informazioni e per iniziare a lavorare con i bordi, consulta la guida secondaria [!DNL Real-time Customer Profile] API [sulle proiezioni edge](../profile/api/edge-projections.md).

## Personalizzare la visualizzazione dei dati del profilo nell’interfaccia utente

Nell’interfaccia utente di Experience Platform, puoi visualizzare e interagire con i dati del profilo cliente in tempo reale sotto forma di profili cliente. Le informazioni di profilo visualizzate nell’interfaccia utente sono state unite da più frammenti di profilo per formare una singola visualizzazione per ogni singolo cliente. Ciò include dettagli quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti visualizzati nei profili possono essere modificati anche a livello organizzativo per visualizzare gli attributi di profilo preferiti.

**Questa guida ti aiuterà a:**
- Riordinare, ridimensionare, modificare e rimuovere le schede.
- Aggiungi attributi.
- Aggiungi una nuova scheda.
- Ripristina valori predefiniti.

Per ulteriori informazioni sulla personalizzazione dei dati del profilo, visita la [documentazione sulla personalizzazione del profilo](../profile/ui/profile-customization.md)

## Passaggi successivi

Dopo aver configurato [!DNL Real-time Customer Profile] per la tua organizzazione, puoi iniziare ad aggiungere dati ai profili dei singoli clienti e a creare segmenti di pubblico in base a attributi cliente specifici. Per iniziare, vedi le seguenti esercitazioni:

- [Aggiungere dati al profilo cliente in tempo reale](../profile/tutorials/add-profile-data.md)
- [Creare un segmento](../segmentation/tutorials/create-a-segment.md)
