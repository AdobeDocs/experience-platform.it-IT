---
solution: Experience Platform
title: Panoramica dei modelli di dati di settore
topic-legacy: overview
description: Scopri i modelli di dati standardizzati per vari settori verticali che possono essere costruiti utilizzando componenti XDM (Experience Data Model) standard.
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# Panoramica dei modelli di dati di settore

Experience Data Model (XDM) consente di creare schemi altamente personalizzabili per acquisire dati di esperienza del cliente chiave relativi alla tua attività. Per semplificare il processo di modellazione dei dati per renderli conformi a XDM, Adobe Experience Platform fornisce una suite versatile di componenti XDM standard, che acquisiscono concetti comunemente utilizzati in diversi settori.

>[!NOTE]
>
>I nuovi componenti XDM standard vengono continuamente rilasciati per soddisfare le migliori esigenze dei consumatori. Per un elenco dei componenti più aggiornati, è possibile [esplorare le risorse esistenti nell&#39;interfaccia utente](../../ui/explore.md) o fare riferimento all&#39; [archivio XDM ufficiale](https://github.com/adobe/xdm/tree/master/components) su GitHub.

A seconda del settore in cui opera la tua azienda, alcuni componenti XDM saranno più pertinenti alle tue esigenze rispetto ad altri. Inoltre, le relazioni stabilite tra gli schemi XDM variano a seconda del settore.

Per guidare la strategia di modellazione dei dati in base al settore specifico, questa guida fornisce un riferimento di diagrammi di relazione delle entità (ERD) per diversi settori verticali supportati.

## Prerequisiti

Per leggere gli ERD a cui si fa riferimento in questa guida, è necessario avere una conoscenza approfondita del modo in cui i componenti XDM interagiscono con gli schemi dei moduli e del funzionamento degli schemi XDM nell’Experience Platform nel suo complesso. Prima di continuare, leggi la seguente documentazione di panoramica:

* [Panoramica](../../home.md) del sistema XDM: Scopri come funziona XDM nell’ecosistema Platform.
* [Nozioni di base sulla composizione](../../schema/composition.md) dello schema: Scopri in che modo i componenti XDM (come gruppi di campi di schema, classi e tipi di dati) contribuiscono alla struttura di uno schema e al ruolo dei campi di identità.

È inoltre consigliabile consultare la [guida alle best practice per la modellazione dei dati](../../schema/best-practices.md) per le linee guida generali su come mappare i dati in XDM.

## ERD dei modelli di dati di settore {#erds}

I modelli verticali del settore rappresentati dalle ERD di seguito sono intenzionalmente creati in modo denormalizzato e tenendo conto del modo in cui i dati vengono memorizzati in Platform.

Per un dato ERD, ogni entità mostrata in si basa su una classe XDM sottostante. Per una determinata entità, ogni riga contrassegnata in **grassetto** rappresenta un gruppo di campi o un tipo di dati, con i campi pertinenti che fornisce elencati di seguito nel testo senza bolli. I campi più importanti per una determinata entità sono evidenziati in rosso.

>[!NOTE]
>
>Alcune entità possono includere un campo &quot;_ID&quot;. Rappresenta l’identificatore univoco (`_id`) che Platform assegna automaticamente alle entità evento o profilo al momento dell’acquisizione. Tuttavia, se lo desideri, puoi scegliere di utilizzare i tuoi valori ID univoci per questo campo.

Tutte le proprietà che possono essere utilizzate per identificare i singoli clienti sono contrassegnate come &quot;identità&quot;, con una di queste proprietà contrassegnata come &quot;identità principale&quot;.

Le relazioni di entità sono contrassegnate come non dipendenti, poiché gli eventi basati su cookie spesso non possono determinare la persona o la persona che ha eseguito la transazione.

Le ERD sono fornite per i seguenti settori verticali:

* [[!UICONTROL Retail]](./retail.md)
* [[!UICONTROL Financial services]](./financial.md)
* [[!UICONTROL Travel and hospitality]](./travel-hospitality.md)

## Passaggi successivi

Questo documento ha fornito una panoramica dei modelli di dati ERD del settore e di come interpretarli. Per visualizzare un ERD, selezionane uno dall’elenco precedente.
