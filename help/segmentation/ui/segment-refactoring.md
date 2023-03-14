---
keywords: Experience Platform;home;argomenti popolari;segmentazione;segmentazione;segmentation;segment builder;Segment builder
solution: Experience Platform
title: Guida dell’interfaccia utente per i vincoli di tempo di segmentazione con refactoring
description: Segment Builder offre un’area di lavoro avanzata che consente di interagire con gli elementi dati del profilo. L’area di lavoro fornisce controlli intuitivi per la creazione e la modifica di regole, ad esempio le tessere trascinate utilizzate per rappresentare le proprietà dei dati.
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Refactorizzazione dei vincoli di tempo

La versione di ottobre 2020 per Adobe Experience Platform ha introdotto modifiche delle prestazioni nel servizio di segmentazione di Adobe Experience Platform, che aggiungono nuove restrizioni all’utilizzo degli operatori logici OR e AND. Queste modifiche interesseranno i segmenti appena creati o modificati tramite l’interfaccia utente di Segment Builder (Generatore di segmenti). Questa guida spiega come mitigare queste modifiche.

Prima del rilascio della versione di ottobre 2020, tutti i vincoli di tempo a livello di regola, di gruppo e di evento facevano riferimento in modo ridondante alla stessa marca temporale. Per chiarire l’utilizzo dei vincoli di tempo, sono stati rimossi i vincoli di tempo a livello di regola e di gruppo. Per adattarsi a questa modifica, tutti i vincoli temporali devono essere riscritti come vincoli temporali a livello di evento.

In precedenza, a un singolo evento potevano essere associate più regole di vincoli di tempo.

![Lo stile precedente dei vincoli di tempo è evidenziato nel Generatore di segmenti.](../images/ui/segment-refactoring/former-time-constraint.png)

Come puoi vedere, questo segmento ha due vincoli a livello di regola: uno per &quot;[!UICONTROL Oggi]&quot; e l’altro per &quot;[!UICONTROL Ieri]&quot;.

Il segmento precedente è equivalente al segmento seguente: entrambi i vincoli di tempo a livello di evento sono stati collegati utilizzando un operatore AND. Il primo vincolo di tempo a livello di evento fa riferimento a un evento di clic il cui nome è uguale a &quot;Training&quot; (Formazione) e si verifica oggi, mentre il secondo vincolo di tempo a livello di evento fa riferimento a un evento di clic il cui nome è uguale a &quot;Pets&quot; e si è verificato ieri.

![Il nuovo stile di restrizioni temporali viene evidenziato nel Generatore di segmenti.](../images/ui/segment-refactoring/time-constraint-1.png) ![Il nuovo stile di restrizioni temporali viene evidenziato nel Generatore di segmenti.](../images/ui/segment-refactoring/time-constraint-2.png)

Questo refactoring dei vincoli di tempo influisce anche sui vincoli di tempo connessi mediante un operatore OR.
