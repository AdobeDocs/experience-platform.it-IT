---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;segment builder;Segment builder
solution: Experience Platform
title: Guida alle modifiche al Generatore di segmenti di servizio di segmentazione
topic: ui guide
description: 'Segment Builder (Generatore di segmenti) fornisce un’area di lavoro completa che consente di interagire con gli elementi dati del profilo. L’area di lavoro offre controlli intuitivi per la creazione e la modifica di regole, come le sezioni di trascinamento utilizzate per rappresentare le proprietà dei dati. '
translation-type: tm+mt
source-git-commit: beacce03136e1620ff57fb549f335d2199bb6001
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Refactorizzazione dei vincoli temporali

La release di ottobre 2020 per Adobe Experience Platform ha introdotto modifiche alle prestazioni di Adobe Experience Platform Segmentation Service che aggiungono nuove restrizioni all&#39;uso degli operatori OR e AND logici. Queste modifiche interesseranno i segmenti appena creati o modificati creati utilizzando l’interfaccia utente di Generatore di segmenti. Questa guida spiega come attenuare tali modifiche.

Prima della release di ottobre 2020, tutti i vincoli temporali a livello di regola, gruppo e a livello di evento si riferivano in modo ridondante alla stessa marca temporale. Per chiarire l&#39;uso dei vincoli temporali, i vincoli temporali a livello di regola e a livello di gruppo sono stati rimossi. Per tenere conto di questa modifica, tutti i vincoli temporali devono essere riscritti come vincoli temporali a livello di evento.

In precedenza, un singolo evento poteva presentare più regole di vincolo temporale associate.

![](../images/ui/segment-refactoring/former-time-constraint.png)

Come potete vedere, questo segmento ha due vincoli a livello di regola: Uno per &quot;[!UICONTROL Today]&quot; e l&#39;altro per &quot;[!UICONTROL Yesterday]&quot;.

Il segmento precedente è equivalente al segmento seguente — entrambi i vincoli temporali a livello di evento sono stati collegati tramite un operatore AND. Il primo vincolo temporale a livello di evento fa riferimento a un evento click il cui nome è uguale a &quot;Formazione&quot; e si verifica oggi, mentre il secondo vincolo temporale a livello di evento fa riferimento a un evento click il cui nome è uguale a &quot;Animali domestici&quot; e si è verificato ieri.

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

Questo refactoring dei vincoli di tempo influisce anche sui vincoli di tempo che vengono collegati tramite un operatore OR.