---
keywords: Experience Platform;modello di apprendimento automatico;Data Science Workspace;Profilo cliente in tempo reale;argomenti popolari;machine learning insights
solution: Experience Platform
title: Arricchire il profilo cliente in tempo reale con Approfondimenti apprendimento automatico
type: Tutorial
description: Questo documento fornisce una guida su come arricchire Real-Time Customer Profile con informazioni sull’apprendimento automatico.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Arricchisci [!DNL Real-Time Customer Profile] con le informazioni di apprendimento automatico

Adobe Experience Platform [!DNL Data Science Workspace] fornisce gli strumenti e le risorse per creare, valutare e utilizzare modelli di apprendimento automatico per generare previsioni e informazioni sui dati. Quando le informazioni di apprendimento automatico vengono acquisite in un set di dati abilitato per [!DNL Profile], gli stessi dati vengono acquisiti anche come [!DNL Profile] record che possono quindi essere segmentati utilizzando [!DNL Adobe Experience Platform Segmentation Service].

In questo documento sono disponibili collegamenti a tutorial che consentono di arricchire [!DNL Real-Time Customer Profile] con le tue informazioni di machine learning.

## Introduzione

Per completare le esercitazioni seguenti, è necessario avere una buona conoscenza dell&#39;acquisizione dei dati [!DNL Profile] e della creazione di segmenti. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce una rappresentazione completa e unificata di ogni singolo cliente basata su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): abilita [!DNL Real-Time Customer Profile] collegando identità da diverse origini dati acquisite in Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull’esperienza del cliente.

Oltre ai documenti sopra indicati, si consiglia vivamente di consultare anche le seguenti guide sugli schemi e sull’Editor di schema:

- [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): descrive schemi XDM, blocchi predefiniti, principi e best practice per la composizione di schemi da utilizzare in [!DNL Experience Platform].
- [Esercitazione sull&#39;editor di schemi](../../xdm/tutorials/create-schema-ui.md): fornisce istruzioni dettagliate per la creazione di schemi tramite l&#39;editor di schemi in [!DNL Experience Platform].

## Creare e configurare uno schema di output e un set di dati {#create-an-output-schema-and-dataset}

Il primo passo per arricchire [!DNL Real-Time Customer Profile] con informazioni sul punteggio è sapere quale oggetto reale (ad esempio una persona) definisce i tuoi dati. Conoscere i dati consente di descrivere e progettare una struttura per aggiungere un significato, in modo analogo alla progettazione di un database relazionale.

La composizione di uno schema inizia assegnando una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Per iniziare a creare schemi personalizzati, segui i passaggi descritti nell&#39;esercitazione su [creazione di uno schema tramite l&#39;Editor di schema](../../xdm/tutorials/create-schema-ui.md). Prima di poter abilitare un set di dati per [!DNL Profile], è necessario configurare lo schema del set di dati in modo che abbia un campo di identità principale e quindi abilitare lo schema per [!DNL Profile]. Quando i dati vengono acquisiti in un set di dati abilitato per [!DNL Profile], gli stessi dati vengono acquisiti anche come [!DNL Profile] record.

Se invece preferisci comporre uno schema utilizzando l&#39;API [!DNL Schema Registry], inizia leggendo la [[!DNL Schema Registry] guida per sviluppatori](../../xdm/api/getting-started.md) prima di tentare l&#39;esercitazione [creazione di uno schema utilizzando l&#39;API](../../xdm/tutorials/create-schema-api.md).

Una volta preparati lo schema e il set di dati, puoi generare e acquisire i dati di punteggio nel set di dati eseguendo le esecuzioni di punteggio utilizzando un modello appropriato.

## Crea segmenti utilizzando [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Dopo aver generato e acquisito le informazioni sul punteggio per il set di dati abilitato per [!DNL Profile], puoi creare segmenti dinamici utilizzando [!DNL Segment Builder].

[!DNL Segment Builder] fornisce un&#39;area di lavoro avanzata che consente di interagire con gli elementi dati [!DNL Profile]. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio le tessere trascinate utilizzate per rappresentare le proprietà dei dati. Segui la [[!DNL Segment Builder] guida utente](../../segmentation/ui/segment-builder.md) per scoprire:

- Creazione di definizioni di segmenti utilizzando una combinazione di attributi, eventi e tipi di pubblico esistenti come blocchi predefiniti.
- Utilizzo dell’area di lavoro e dei contenitori del generatore di regole per controllare l’ordine di esecuzione delle regole dei segmenti.
- Visualizzazione di stime del pubblico potenziale, per regolare le definizioni dei segmenti in base alle esigenze.
- Abilitazione di tutte le definizioni di segmento per la segmentazione pianificata.
- Abilitazione di definizioni di segmenti specificate per la segmentazione in streaming.

## Passaggi successivi {#next-steps}

Per ulteriori informazioni sui segmenti e su [!DNL Segment Builder], consulta la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

Per ulteriori informazioni su [!DNL Real-Time Customer Profile], leggere la [Panoramica del profilo cliente in tempo reale](../../profile/home.md)
