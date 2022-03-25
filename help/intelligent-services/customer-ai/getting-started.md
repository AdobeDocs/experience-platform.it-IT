---
keywords: Experience Platform;guida introduttiva;ai clienti;argomenti comuni
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Guida introduttiva di Customer AI
topic-legacy: Getting started
description: Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Guida introduttiva a Customer AI

Le guide per Customer AI richiedono una comprensione approfondita dei vari servizi Platform coinvolti nell’utilizzo di Customer AI. Prima di iniziare, controlla i seguenti documenti:

- [Panoramica del sistema Experience Data Model (XDM)](../../xdm/home.md): XDM è il framework fondamentale che consente [!DNL Adobe Experience Cloud], grazie all&#39;Experience Platform, per inviare il messaggio giusto alla persona giusta, sul canale giusto, al momento giusto. La metodologia su cui viene generato l’Experience Platform, sistema XDM, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi Platform.
- [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): Questo documento fornisce un’introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): Questa esercitazione descrive i passaggi per la creazione di uno schema utilizzando l’Editor di schema in Experience Platform.
- [Panoramica del profilo cliente in tempo reale](../../rtcdp/overview.md): Incorporato [!DNL Adobe Experience Platform], Real-time Customer Data Platform (Real-time CDP) consente alle aziende di unire dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti in tutto il percorso di clienti. Real-time CDP combina più origini dati aziendali per creare in tempo reale profili unificati che possono essere utilizzati per fornire esperienze cliente personalizzate uno-a-uno su tutti i canali e dispositivi.
- [Panoramica del servizio di segmentazione](../../segmentation/home.md): La segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall’archivio dei profili per distinguere un gruppo commerciabile di persone dalla base dei clienti. Ad esempio, in una campagna e-mail intitolata &quot;Ti sei dimenticato di comprare le scarpe da ginnastica?&quot;, potresti volere un pubblico di tutti gli utenti che hanno cercato di correre scarpe negli ultimi 30 giorni, ma che non hanno completato un acquisto. Utilizzando segmenti diversi, puoi concentrarti sui vari tipi di pubblico, offrendo un’esperienza di marketing più personalizzata.
- [Guida utente di Segment Builder](../../segmentation/tutorials/create-a-segment.md): Platform consente di creare e accedere facilmente ai segmenti e di utilizzare diversi blocchi predefiniti per caratterizzare ulteriormente i segmenti.

## Download dei punteggi di Customer AI

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e passare alla [guida alla configurazione](./user-guide/configure.md).

Il download dei punteggi di Customer AI viene effettuato tramite una combinazione di chiamate API. Per effettuare chiamate alle API di Platform, devi prima completare l’ [esercitazione sull&#39;autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento dell’esercitazione di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: Portatore `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Tutte le richieste alle API di Platform richiedono un’intestazione che specifichi il nome della sandbox in cui avrà luogo l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Platform, consulta la sezione [documentazione panoramica su sandbox](../../sandboxes/home.md).

### Lettura di chiamate API di esempio

Questa guida fornisce esempi di chiamate API per dimostrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richiesta formattati correttamente. Viene inoltre fornito un esempio di codice JSON restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi

Una volta completati i passaggi descritti nel documento precedente, visita il [Ingresso e uscita](./input-output.md) documentazione. Questo documento fornisce una breve panoramica dei tipi di dati utilizzati e prodotti in Customer AI.
