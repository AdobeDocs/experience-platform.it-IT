---
keywords: Experience Platform;modello di apprendimento automatico;Data Science Workspace;Profilo cliente in tempo reale;argomenti popolari;machine learning insights
solution: Experience Platform
title: Arricchire il profilo cliente in tempo reale con Approfondimenti apprendimento automatico
type: Tutorial
description: Questo documento fornisce una guida su come arricchire Real-Time Customer Profile con informazioni sull’apprendimento automatico.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Arricchisci [!DNL Real-Time Customer Profile] con le informazioni di apprendimento automatico

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

[!DNL Data Science Workspace] Adobe Experience Platform fornisce gli strumenti e le risorse per creare, valutare e utilizzare modelli di Machine Learning per generare previsioni e approfondimenti sui dati. Quando le informazioni dettagliate di Machine Learning vengono inserite in un [!DNL Profile]set di dati abilitato, gli stessi dati vengono acquisiti anche come [!DNL Profile] record che possono quindi essere segmentati utilizzando [!DNL Adobe Experience Platform Segmentation Service].

Il processo di Segmentazione dipende dal metodo di valutazione per il pubblico. Se un pubblico è configurato come **streaming**, elaborerà tutti i nuovi aggiornamenti scritti dal modello nel profilo in tempo reale. Tuttavia, se un pubblico è configurato per **la valutazione batch** , i nuovi valori verranno valutati nel batch successivo.

Questo documento fornisce collegamenti a esercitazioni che ti consentono di arricchire [!DNL Real-Time Customer Profile] le tue informazioni dettagliate su Machine Learning.

## Introduzione

Per completare le esercitazioni riportate di seguito, è necessario avere una conoscenza pratica dell&#39;inserimento [!DNL Profile] dei dati e della creazione di tipi di pubblico. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce una rappresentazione completa e unificata di ogni singolo cliente basata su dati aggregati provenienti da più origini.
- [[!DNL Identity Service]](../../identity-service/home.md): abilita [!DNL Real-Time Customer Profile] collegando identità da diverse origini dati acquisite in Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato in base al quale Platform organizza i dati sull’esperienza del cliente.

Oltre ai documenti sopra menzionati, si consiglia vivamente di rivedere anche le seguenti guide sugli schemi e sull&#39;Editor schema:

- [Nozioni di base sulla composizione](../../xdm/schema/composition.md) dello schema: descrive gli schemi XDM, i blocchi predefiniti, i principi e le procedure consigliate per la composizione di schemi da utilizzare in [!DNL Experience Platform].
- [Editor di schemi esercitazione](../../xdm/tutorials/create-schema-ui.md): fornisce istruzioni dettagliate per la creazione di schemi utilizzando l&#39;Editor di schemi all&#39;interno [!DNL Experience Platform]di .

## Crea e configurare uno schema di output e un set di dati {#create-an-output-schema-and-dataset}

Il primo passo per arricchire [!DNL Real-Time Customer Profile] con le informazioni dettagliate sul punteggio è sapere quale oggetto del mondo reale (come una persona) definiscono i tuoi dati. Avere una comprensione dei dati consente di descrivere e progettare una struttura per aggiungere significato, molto like la progettazione di un database relazionale.

La composizione di uno schema inizia con l&#39;assegnazione di una classe. Le classi definiscono gli aspetti comportamentali dei dati che lo schema conterrà (record o serie temporali). Per iniziare a creare schemi personalizzati, seguire i passaggi della esercitazione per [creare uno schema utilizzando l&#39;Editor](../../xdm/tutorials/create-schema-ui.md) schema. Prima di poter abilitare un set di dati per [!DNL Profile], è necessario configurare lo schema del set di dati in modo che abbia un campo di identità principale e quindi abilitare lo schema per [!DNL Profile]. Quando i dati vengono acquisiti in un set di dati abilitato per [!DNL Profile], gli stessi dati vengono acquisiti anche come [!DNL Profile] record.

Se invece preferisci comporre uno schema utilizzando l&#39;API [!DNL Schema Registry], inizia leggendo la [[!DNL Schema Registry] guida per sviluppatori](../../xdm/api/getting-started.md) prima di tentare l&#39;esercitazione [creazione di uno schema utilizzando l&#39;API](../../xdm/tutorials/create-schema-api.md).

Una volta preparati lo schema e il set di dati, puoi generare e acquisire i dati di punteggio nel set di dati eseguendo le esecuzioni di punteggio utilizzando un modello appropriato.

## Crea pubblico utilizzando il [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Dopo aver generato e inserito le informazioni dettagliate sui dati di punteggio nel [!DNL Profile]set di dati abilitato, puoi creare tipi di pubblico dinamici utilizzando .[!DNL Segment Builder]

Offre un&#39;area [!DNL Segment Builder] di lavoro avanzata che consente di interagire con [!DNL Profile] gli elementi dati. L&#39;area di lavoro fornisce controlli intuitivi per la creazione e la modifica delle regole, ad esempio i riquadri con trascinamento della selezione utilizzati per rappresentare le proprietà dei dati. Segui la [[!DNL Segment Builder] guida](../../segmentation/ui/segment-builder.md) utente per ulteriori informazioni su:

- Creazione di definizioni di segmenti utilizzando una combinazione di attributi, eventi e tipi di pubblico esistenti come blocchi predefiniti.
- Uso dell&#39;area di disegno e dei contenitori per la creazione di regola per controllare l&#39;ordine di esecuzione delle regole per i tipi di pubblico.
- Visualizzazione delle stime del pubblico potenziale, che consente di modificare le definizioni dei segmenti in base alle esigenze.
- Abilitazione di tutte le definizioni di segmento per la segmentazione pianificata.
- Abilitazione di definizioni di segmenti specificate per la segmentazione in streaming.

## Passaggi successivi {#next-steps}

Per ulteriori informazioni sui tipi di pubblico e su [!DNL Segment Builder], consulta la [Panoramica del servizio di segmentazione](../../segmentation/home.md).

Per saperne di più su [!DNL Real-Time Customer Profile], leggi la panoramica del [profilo cliente in tempo reale](../../profile/home.md)
