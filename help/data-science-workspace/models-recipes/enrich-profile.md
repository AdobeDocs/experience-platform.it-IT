---
keywords: ' Experience Platform;modello di apprendimento automatico;Area di lavoro dati;Profilo cliente in tempo reale;argomenti più comuni;informazioni sull''apprendimento automatico'
solution: Experience Platform
title: Ottimizzazione del profilo cliente in tempo reale con informazioni approfondite sull'apprendimento automatico
topic: tutorial
type: Tutorial
description: Questo documento fornisce una guida su come arricchire il profilo cliente in tempo reale con informazioni approfondite sull'apprendimento automatico.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Arricchisci [!DNL Real-time Customer Profile] con approfondimenti di machine learning

Adobe Experience Platform [!DNL Data Science Workspace] fornisce gli strumenti e le risorse per creare, valutare e utilizzare modelli di machine learning per generare previsioni e approfondimenti sui dati. Quando le informazioni sull&#39;apprendimento automatico vengono inserite in un dataset [!DNL Profile] abilitato, gli stessi dati vengono anche assimilati a record [!DNL Profile] che possono essere segmentati utilizzando [!DNL Adobe Experience Platform Segmentation Service]. Con l&#39;acquisizione dei dati di profilo e serie temporali, il profilo cliente in tempo reale decide automaticamente di includere o escludere tali dati dai segmenti attraverso un processo continuo denominato segmentazione in streaming, prima di unirli ai dati esistenti e di aggiornare la visualizzazione unione. Di conseguenza, puoi eseguire istantaneamente dei calcoli e prendere decisioni per offrire esperienze personalizzate e avanzate ai clienti mentre interagiscono con il tuo marchio.

Questo documento contiene collegamenti alle esercitazioni che consentono di arricchire [!DNL Real-time Customer Profile] le informazioni sull&#39;apprendimento delle computer.

## Introduzione

Per completare le esercitazioni riportate di seguito, è necessario avere una buona conoscenza dell&#39;assimilazione dei dati [!DNL Profile] e della creazione dei segmenti. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce una rappresentazione completa e unificata di ogni singolo cliente basata su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): Consente  [!DNL Real-time Customer Profile] di collegare identità da origini dati diverse che vengono caricate in Piattaforma.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.

Oltre ai documenti di cui sopra, si consiglia di consultare anche le seguenti guide sugli schemi e sull&#39;Editor di schema:

- [Nozioni di base sulla composizione](../../xdm/schema/composition.md) dello schema: Descrive gli schemi XDM, i blocchi costitutivi, i principi e le procedure ottimali per la composizione degli schemi in cui  [!DNL Experience Platform]utilizzarli.
- [Esercitazione](../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Fornisce istruzioni dettagliate per la creazione di schemi utilizzando l&#39;Editor di schema all&#39;interno  [!DNL Experience Platform].

## Creare e configurare uno schema di output e un dataset {#create-an-output-schema-and-dataset}

Il primo passo verso l&#39;arricchimento di [!DNL Real-time Customer Profile] con informazioni di punteggio è sapere quale oggetto reale (come una persona) definisce i dati. La comprensione dei dati consente di descrivere e progettare una struttura per aggiungere significato, come la progettazione di un database relazionale.

La composizione di uno schema inizia con l&#39;assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Per iniziare a creare i tuoi schemi, segui i passaggi dell&#39;esercitazione su [creazione di uno schema utilizzando l&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md). Prima di abilitare un dataset per [!DNL Profile], è necessario configurare lo schema del dataset in modo che abbia un campo identità principale e quindi attivare lo schema per [!DNL Profile]. Quando i dati vengono trasferiti in un dataset abilitato [!DNL Profile], gli stessi dati vengono anche inseriti come record [!DNL Profile].

Se invece si preferisce comporre uno schema utilizzando l&#39;API [!DNL Schema Registry], iniziare leggendo la [[!DNL Schema Registry] guida allo sviluppatore](../../xdm/api/getting-started.md) prima di provare l&#39;esercitazione su [creazione di uno schema mediante l&#39;API](../../xdm/tutorials/create-schema-api.md).

Una volta preparati lo schema e il set di dati, è possibile generare e assimilare i dati del punteggio al dataset eseguendo le esecuzioni del punteggio utilizzando un modello appropriato.

## Creare segmenti utilizzando [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Dopo aver generato e assimilato le informazioni sui dati di punteggio al dataset [!DNL Profile] abilitato, puoi creare segmenti dinamici utilizzando [!DNL Segment Builder].

[!DNL Segment Builder] offre un&#39;area di lavoro ricca che consente di interagire con gli elementi di dati [!DNL Profile]. L’area di lavoro offre controlli intuitivi per la creazione e la modifica di regole, come le sezioni di trascinamento utilizzate per rappresentare le proprietà dei dati. Seguite la [[!DNL Segment Builder] guida utente](../../segmentation/ui/segment-builder.md) per saperne di più:

- Creazione di definizioni di segmento tramite una combinazione di attributi, eventi e audience esistenti come elementi costitutivi.
- Utilizzo del quadro e dei contenitori del generatore di regole per controllare l&#39;ordine in cui vengono eseguite le regole del segmento.
- Visualizzazione delle stime del pubblico potenziale, per regolare le definizioni dei segmenti in base alle esigenze.
- Abilitazione di tutte le definizioni di segmento per la segmentazione pianificata.
- Abilitazione delle definizioni di segmento specificate per la segmentazione in streaming.

## Passaggi successivi {#next-steps}

Per ulteriori informazioni sui segmenti e sull&#39; [!DNL Segment Builder], leggere la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

Per ulteriori informazioni su [!DNL Real-time Customer Profile], leggere la [Panoramica sul profilo cliente in tempo reale](../../profile/home.md)