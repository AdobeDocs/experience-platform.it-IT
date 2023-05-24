---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Segment Match;segment match;home;popular topic;segmentation;Segmentation;Segment Match;segment match
solution: Experience Platform
title: Domande frequenti sulla corrispondenza dei segmenti
description: Segment Match è un servizio di condivisione dei segmenti in Adobe Experience Platform che consente a due o più utenti di Platform di scambiarsi i dati dei segmenti in modo sicuro, gestito e rispettoso della privacy.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# [!DNL Segment Match] domande frequenti

Questa guida fornisce le risposte alle domande legali e sulla privacy spesso poste in merito a Adobe Experience Platform Segment Match.

## Quali dati vengono condivisi durante la sovrapposizione delle stime e come può Adobe garantire che queste metriche vengano ottenute in modo sicuro?

![overlap-report.png](./images/overlap-report.png)

Per ottenere queste metriche di stima di sovrapposizione, i dati dei clienti o dei segmenti non vengono spostati tra le sandbox. Le identità applicabili preselezionate dal cliente in una data sandbox vengono aggiunte a una struttura di dati probabilistica in cui gli ID stessi sono rappresentati in un formato con hash.

Si tratta di un processo unidirezionale, il che significa che gli identificatori pre-hash originali non sono esposti e non possono essere decodificati.

Queste strutture di dati hanno proprietà univoche che consentono agli ingegneri di eseguire operazioni di unione e intersezione tra di esse, anche se le informazioni codificate sono fortemente compresse o sottoposte a hashing. Queste operazioni consentono [!DNL Segment Match] ottenere l’intersezione stimata di due strutture di dati composte da ID provenienti da due sandbox diverse senza dover confrontare i valori effettivi. Da [!DNL Segment Match] utilizza solo le strutture di dati, gli ID non lasciano mai le archivi profilo delle rispettive organizzazioni a scopo di stima. Questo consente ad Adobe di soddisfare i requisiti di privacy e sicurezza dei clienti offrendo al contempo strumenti di stima altamente accurati per guidare gli accordi di collaborazione sui dati.

## Qual è il processo alla base della designazione delle identità che ricevono gli ID del segmento condiviso?

[!DNL Segment Match] offre ai clienti un’opzione per configurare gli spazi dei nomi da utilizzare nel servizio. Questa selezione viene applicata sia al processo di stima descritto nella domanda precedente che al processo di trasferimento dei dati, nel caso in cui il cliente decida di pubblicare il feed in una sandbox partner.

Il processo di trasferimento dei dati tra le identità crittografate di due organizzazioni diverse viene eseguito in un ambiente di elaborazione neutro. Il processo di trasferimento dei dati è di proprietà di Adobe e le organizzazioni coinvolte nella partnership non hanno accesso a questo ambiente, né a qualsiasi registro che possa essere un risultato del processo di trasferimento dei dati.

Solo l’appartenenza a un segmento viene acquisita nei frammenti di profilo sovrapposti di un’organizzazione ricevente e non viene trasferita alcuna identità aggiuntiva dall’organizzazione mittente all’organizzazione ricevente. Il processo di trasferimento dei dati non legge informazioni personali identificabili (PII) in formato testo normale perché [!DNL Segment Match] consente sovrapposizioni solo sugli spazi dei nomi crittografati SHA256 (e-mail/telefono) ogni volta che i dati sono PII. I risultati non vengono mai memorizzati nell&#39;ambiente di elaborazione.
