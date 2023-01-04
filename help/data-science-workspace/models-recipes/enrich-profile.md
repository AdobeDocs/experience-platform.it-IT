---
keywords: Experience Platform;modello di apprendimento automatico;Data Science Workspace;Profilo cliente in tempo reale;argomenti popolari;informazioni sull'apprendimento automatico
solution: Experience Platform
title: Arricchire il profilo del cliente in tempo reale con informazioni sull’apprendimento automatico
topic-legacy: tutorial
type: Tutorial
description: Questo documento fornisce una guida su come arricchire il profilo cliente in tempo reale con informazioni sull’apprendimento automatico.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Arricchire [!DNL Real-Time Customer Profile] con informazioni sull’apprendimento automatico

Adobe Experience Platform [!DNL Data Science Workspace] fornisce gli strumenti e le risorse per creare, valutare e utilizzare modelli di apprendimento automatico per generare previsioni e insights sui dati. Quando le informazioni sull’apprendimento automatico vengono acquisite in un [!DNL Profile]set di dati abilitati, gli stessi dati vengono acquisiti anche come [!DNL Profile] record che possono quindi essere segmentati utilizzando [!DNL Adobe Experience Platform Segmentation Service].

Questo documento fornisce collegamenti alle esercitazioni che consentono di arricchire [!DNL Real-Time Customer Profile] con le informazioni sull&#39;apprendimento automatico.

## Introduzione

Per completare le esercitazioni riportate di seguito, è necessario avere una buona conoscenza dell’acquisizione [!DNL Profile] e creazione di segmenti. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornisce una rappresentazione completa e unificata di ogni singolo cliente basata su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): Abilita [!DNL Real-Time Customer Profile] collegando identità provenienti da diverse fonti di dati che vengono acquisite in Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.

Oltre ai documenti di cui sopra, è consigliabile consultare anche le seguenti guide sugli schemi e sull’Editor di schema:

- [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): Descrive gli schemi XDM, i blocchi predefiniti, i principi e le best practice per la composizione degli schemi da utilizzare in [!DNL Experience Platform].
- [Esercitazione sull’Editor di schema](../../xdm/tutorials/create-schema-ui.md): Fornisce istruzioni dettagliate per la creazione di schemi utilizzando l’Editor di schema in [!DNL Experience Platform].

## Creare e configurare uno schema e un set di dati di output {#create-an-output-schema-and-dataset}

Il primo passo verso l&#39;arricchimento [!DNL Real-Time Customer Profile] per &quot;scoring insights&quot; si intende sapere quale oggetto reale (come una persona) definisce i tuoi dati. La comprensione dei dati consente di descrivere e progettare una struttura per aggiungere significato, proprio come la progettazione di un database relazionale.

La composizione di uno schema inizia con l’assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Per iniziare a creare i tuoi schemi, segui i passaggi dell’esercitazione su [creazione di uno schema tramite l’Editor di schema](../../xdm/tutorials/create-schema-ui.md). Tieni presente che prima di poter abilitare un set di dati per [!DNL Profile], devi configurare lo schema del set di dati in modo che abbia un campo di identità principale e quindi abilitare lo schema per [!DNL Profile]. Quando i dati vengono acquisiti in un [!DNL Profile]set di dati abilitati, gli stessi dati vengono acquisiti anche come [!DNL Profile] registrazioni.

Se preferisci comporre uno schema utilizzando [!DNL Schema Registry] API, invece, inizia leggendo il [[!DNL Schema Registry] guida per sviluppatori](../../xdm/api/getting-started.md) prima di provare l&#39;esercitazione su [creazione di uno schema tramite API](../../xdm/tutorials/create-schema-api.md).

Una volta preparati lo schema e il set di dati, puoi generare e inserire i dati del punteggio nel set di dati eseguendo le esecuzioni del punteggio utilizzando un modello appropriato.

## Crea segmenti utilizzando [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Dopo aver generato e acquisito le informazioni sui dati di valutazione nel tuo [!DNL Profile]Set di dati abilitato, puoi creare segmenti dinamici utilizzando [!DNL Segment Builder].

La [!DNL Segment Builder] offre un’area di lavoro ricca che consente di interagire con [!DNL Profile] elementi dati. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio riquadri drag-and-drop utilizzati per rappresentare le proprietà dei dati. Segui [[!DNL Segment Builder] guida utente](../../segmentation/ui/segment-builder.md) per ulteriori informazioni:

- Creazione di definizioni di segmenti utilizzando una combinazione di attributi, eventi e tipi di pubblico esistenti come blocchi predefiniti.
- Utilizzo dell’area di lavoro e dei contenitori del generatore di regole per controllare l’ordine in cui vengono eseguite le regole del segmento.
- Visualizzazione delle stime del pubblico potenziale, che consentono di regolare le definizioni dei segmenti in base alle esigenze.
- Abilitazione di tutte le definizioni di segmento per la segmentazione pianificata.
- Abilitazione di definizioni di segmenti specifiche per la segmentazione in streaming.

## Passaggi successivi {#next-steps}

Per ulteriori informazioni sui segmenti e sui [!DNL Segment Builder], leggi [Panoramica del servizio di segmentazione](../../segmentation/home.md).

Per ulteriori informazioni [!DNL Real-Time Customer Profile], leggi [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
