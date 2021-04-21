---
keywords: Experience Platform;modello di apprendimento automatico;Data Science Workspace;Profilo cliente in tempo reale;argomenti popolari;informazioni sull'apprendimento automatico
solution: Experience Platform
title: Arricchire il profilo del cliente in tempo reale con informazioni sull’apprendimento automatico
topic-legacy: tutorial
type: Tutorial
description: Questo documento fornisce una guida su come arricchire il profilo cliente in tempo reale con informazioni sull’apprendimento automatico.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Arricchisci [!DNL Real-time Customer Profile] con informazioni sull&#39;apprendimento automatico

Adobe Experience Platform [!DNL Data Science Workspace] fornisce gli strumenti e le risorse necessari per creare, valutare e utilizzare modelli di apprendimento automatico per generare previsioni e informazioni sui dati. Quando le informazioni sull’apprendimento automatico vengono acquisite in un set di dati abilitato [!DNL Profile], gli stessi dati vengono acquisiti anche come record [!DNL Profile] che possono essere segmentati utilizzando [!DNL Adobe Experience Platform Segmentation Service]. Man mano che i dati di profilo e serie temporali vengono acquisiti, Profilo cliente in tempo reale decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente i calcoli e prendere decisioni per fornire ai clienti esperienze ottimizzate e personalizzate mentre interagiscono con il tuo marchio.

Questo documento fornisce collegamenti alle esercitazioni che ti consentono di arricchire [!DNL Real-time Customer Profile] con le informazioni sull’apprendimento automatico.

## Introduzione

Per completare le esercitazioni riportate di seguito, è necessario avere una buona conoscenza dell’acquisizione dei dati [!DNL Profile] e della creazione dei segmenti. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce una rappresentazione completa e unificata di ogni singolo cliente basata su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): Consente  [!DNL Real-time Customer Profile] di collegare identità da diverse origini dati che vengono acquisite in Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale Platform organizza i dati sulla customer experience.

Oltre ai documenti di cui sopra, è consigliabile consultare anche le seguenti guide sugli schemi e sull’Editor di schema:

- [Nozioni di base sulla composizione](../../xdm/schema/composition.md) dello schema: Descrive gli schemi XDM, i blocchi predefiniti, i principi e le best practice per la composizione degli schemi da utilizzare in  [!DNL Experience Platform].
- [Esercitazione](../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Fornisce istruzioni dettagliate per la creazione di schemi utilizzando l’Editor di schema in  [!DNL Experience Platform].

## Creare e configurare uno schema e un set di dati di output {#create-an-output-schema-and-dataset}

Il primo passo verso l&#39;arricchimento di [!DNL Real-time Customer Profile] con informazioni di punteggio è sapere quale oggetto reale (come una persona) definisce i tuoi dati. La comprensione dei dati consente di descrivere e progettare una struttura per aggiungere significato, proprio come la progettazione di un database relazionale.

La composizione di uno schema inizia con l’assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Per iniziare a creare schemi personalizzati, segui i passaggi dell&#39;esercitazione su [creazione di uno schema utilizzando l&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md). Tieni presente che prima di poter abilitare un set di dati per [!DNL Profile], devi configurare lo schema del set di dati in modo che abbia un campo di identità principale e quindi abilitare lo schema per [!DNL Profile]. Quando i dati vengono acquisiti in un set di dati abilitato [!DNL Profile], gli stessi vengono acquisiti anche come record [!DNL Profile].

Se invece preferisci comporre uno schema utilizzando l&#39;API [!DNL Schema Registry], inizia leggendo la [[!DNL Schema Registry] guida per gli sviluppatori](../../xdm/api/getting-started.md) prima di provare l&#39;esercitazione su [creazione di uno schema utilizzando l&#39;API](../../xdm/tutorials/create-schema-api.md).

Una volta preparati lo schema e il set di dati, puoi generare e inserire i dati del punteggio nel set di dati eseguendo le esecuzioni del punteggio utilizzando un modello appropriato.

## Crea segmenti utilizzando [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Dopo aver generato e acquisito le informazioni sui dati di punteggio nel set di dati abilitato [!DNL Profile], puoi creare segmenti dinamici utilizzando [!DNL Segment Builder].

L’ [!DNL Segment Builder] offre un’area di lavoro ricca che consente di interagire con gli elementi dati [!DNL Profile]. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio riquadri drag-and-drop utilizzati per rappresentare le proprietà dei dati. Segui la [[!DNL Segment Builder] guida utente](../../segmentation/ui/segment-builder.md) per informazioni su:

- Creazione di definizioni di segmenti utilizzando una combinazione di attributi, eventi e tipi di pubblico esistenti come blocchi predefiniti.
- Utilizzo dell’area di lavoro e dei contenitori del generatore di regole per controllare l’ordine in cui vengono eseguite le regole del segmento.
- Visualizzazione delle stime del pubblico potenziale, che consentono di regolare le definizioni dei segmenti in base alle esigenze.
- Abilitazione di tutte le definizioni di segmento per la segmentazione pianificata.
- Abilitazione di definizioni di segmenti specifiche per la segmentazione in streaming.

## Passaggi successivi {#next-steps}

Per ulteriori informazioni sui segmenti e sul [!DNL Segment Builder], consulta la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

Per ulteriori informazioni su [!DNL Real-time Customer Profile], consulta la [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
