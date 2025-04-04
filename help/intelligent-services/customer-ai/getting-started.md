---
keywords: Experience Platform;guida introduttiva;ia cliente;argomenti più comuni
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Guida introduttiva di Customer AI
description: Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente.
exl-id: 90c9a83a-8e66-4239-b2d6-2049a6319b25
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 8%

---

# Guida introduttiva di Customer AI

Le guide per IA per l’analisi dei clienti richiedono una buona conoscenza dei vari servizi di Experience Platform coinvolti nell’utilizzo di IA per l’analisi dei clienti. Prima di iniziare, consulta i seguenti documenti:

- [Panoramica del sistema Experience Data Model (XDM)](../../xdm/home.md): XDM è il framework fondamentale che consente a [!DNL Adobe Experience Cloud], con tecnologia Experience Platform, di inviare il messaggio giusto alla persona giusta, sul canale giusto, nel momento esatto. La metodologia su cui è basato Experience Platform, il sistema XDM, rende operativi gli schemi Experience Data Model per l’utilizzo da parte dei servizi Experience Platform.
- [Nozioni di base sulla composizione dello schema](../../xdm/schema/composition.md): questo documento fornisce un&#39;introduzione agli schemi Experience Data Model (XDM) e ai blocchi predefiniti, ai principi e alle best practice per la composizione degli schemi da utilizzare in [!DNL Adobe Experience Platform].
- [Creazione di schemi](../../xdm/tutorials/create-schema-ui.md): questo tutorial illustra i passaggi necessari per la creazione di uno schema tramite l&#39;Editor di schema in Experience Platform.
- [Panoramica del profilo cliente in tempo reale](../../rtcdp/overview.md): basata su [!DNL Adobe Experience Platform], Adobe Real-Time Customer Data Platform (Real-Time CDP) consente alle aziende di unire dati noti e sconosciuti per attivare i profili dei clienti con decisioni intelligenti in tutto il percorso di clienti. Real-Time CDP combina più origini dati aziendali per creare profili unificati in tempo reale che possono essere utilizzati per fornire ai clienti esperienze personalizzate uno a uno su tutti i canali e i dispositivi.
- [Panoramica del servizio di segmentazione](../../segmentation/home.md): la segmentazione è il processo di definizione di attributi o comportamenti specifici condivisi da un sottoinsieme di profili dall&#39;archivio profili per distinguere un gruppo commerciabile di persone dalla base clienti. Ad esempio, in una campagna e-mail denominata &quot;Hai dimenticato di acquistare le tue scarpe da ginnastica?&quot;, potresti desiderare un pubblico di tutti gli utenti che hanno cercato scarpe da corsa negli ultimi 30 giorni, ma che non hanno completato un acquisto. Utilizzando segmenti diversi, puoi concentrarti sui vari tipi di pubblico, offrendo un’esperienza di marketing più personalizzata.
- [Guida utente di Segment Builder](../../segmentation/tutorials/create-a-segment.md): Experience Platform ti consente di creare e accedere facilmente ai segmenti e di utilizzare blocchi predefiniti diversi per caratterizzare ulteriormente i segmenti.

## Download dei punteggi di Customer AI

>[!NOTE]
>
>Se non è necessario scaricare i punteggi non elaborati, puoi saltare questo passaggio e passare alla [guida alla configurazione](./user-guide/configure.md).

Il download dei punteggi di Customer AI viene eseguito tramite una combinazione di chiamate API. Per effettuare chiamate alle API di Experience Platform, devi prima completare l&#39;[esercitazione di autenticazione](https://www.adobe.com/go/platform-api-authentication-en). Il completamento del tutorial di autenticazione fornisce i valori per ciascuna delle intestazioni richieste in tutte le chiamate API di Experience Platform, come mostrato di seguito:

- Autorizzazione: Bearer `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Tutte le risorse in Experience Platform sono isolate in specifiche sandbox virtuali. Tutte le richieste alle API di Experience Platform richiedono un’intestazione che specifichi il nome della sandbox in cui verrà eseguita l’operazione:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Per ulteriori informazioni sulle sandbox in Experience Platform, consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

### Lettura delle chiamate API di esempio

Questa guida fornisce esempi di chiamate API per illustrare come formattare le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un codice JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere chiamate API di esempio](../../landing/troubleshooting.md) nella guida alla risoluzione dei problemi di Experience Platform.

## Passaggi successivi

Dopo aver completato i passaggi descritti nel documento precedente, visita la documentazione [Input e Output](./data-requirements.md). Questo documento fornisce una breve panoramica sui tipi di dati utilizzati e prodotti in Customer AI.
