---
title: Retargeting fuori sede dei visitatori non autenticati
description: Scopri come effettuare il retargeting degli utenti non autenticati utilizzando gli ECID
feature: Use Cases, Customer Acquisition
source-git-commit: 672b15b0c36efbf3b7d62ec616f254fffe3dbb81
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Retargeting non autenticato {#unauthenticated-retargeting}

Poiché i cookie di terze parti perdono efficacia, le aziende stanno passando a soluzioni senza cookie per il coinvolgimento e il retargeting personalizzati. Il retargeting fuori sede consente alle aziende di raggiungere gli utenti ad alto intento in base alle loro interazioni precedenti, senza affidarsi a JavaScript lato client.

## Perché considerare il retargeting dei visitatori non autenticati {#why-use-case}

Integrando il Web SDK di Adobe Experience Platform e l’inoltro di eventi lato server, puoi semplificare lo streaming di eventi e l’inoltro di dati. Questo consente il retargeting integrato degli utenti non autenticati tramite gli ECID (Experience Cloud ID), garantendo un coinvolgimento coerente tra le piattaforme. Con questa soluzione, puoi aumentare le opportunità di conversione eseguendo il retargeting efficace degli utenti non autenticati in base alle loro interazioni passate.

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Prima di procedere con la distribuzione del Web SDK e la configurazione di Inoltro eventi, verificare quanto segue:

1. **Installazione di Adobe con Web SDK**: è necessario implementare Adobe Web SDK per facilitare la raccolta degli eventi e l&#39;inoltro dei dati.

2. **Configurazione di Adobe Experience Platform Edge Network**: assicurati che Edge Network sia configurato per supportare l&#39;inoltro di eventi in tempo reale per il retargeting fuori sede.

3. **Sincronizzazione ECID**: assicurati che gli ECID siano sincronizzati tra le piattaforme per consentire una corrispondenza perfetta del pubblico.

## Come ottenere il retargeting fuori sede {#achieve-offsite-retargeting}

1. **Distribuisci Web SDK**: implementa Adobe Web SDK sul tuo sito Web per acquisire dati evento in tempo reale, incluse le interazioni dell&#39;utente come visualizzazioni di pagina, clic e altri comportamenti.

2. **Abilita Inoltro eventi**: configura l&#39;inoltro eventi in Platform per inviare i dati utente raccolti, garantendo un trasferimento efficiente dei dati per l&#39;attivazione del pubblico.

3. **Configura attivazione lato server**: utilizza le funzionalità lato server di Adobe per attivare il retargeting dei tipi di pubblico in base agli ECID, garantendo un targeting accurato del pubblico tra le piattaforme.

4. **Crea tipi di pubblico mirati**: utilizza gli strumenti di segmentazione del pubblico di Platform per definire tipi di pubblico mirati in base al comportamento dell&#39;utente, ad esempio visualizzazioni, interazioni o carrelli abbandonati.

5. **Attiva tipi di pubblico**: una volta creati i tipi di pubblico di cui hai effettuato il retargeting, attivali per distribuire contenuti personalizzati, assicurando che gli utenti vengano nuovamente coinvolti in base alle loro precedenti interazioni con il sito.

## Creare un pubblico utilizzando l’attributo calcolato {#create-audience}

Per eseguire il retargeting in modo efficace degli utenti ad alto intento, crea tipi di pubblico in base alle loro interazioni passate con il sito web. Utilizza Platform per segmentare gli utenti utilizzando attributi calcolati.

1. **Identifica i comportamenti chiave**: seleziona le azioni dell&#39;utente da monitorare, ad esempio le visualizzazioni di pagina o i clic.

2. **Crea tipi di pubblico**: utilizza gli strumenti di segmentazione del pubblico per raggruppare gli utenti in base ai comportamenti.

3. **Sincronizza ECID**: assicurati che gli ECID siano sincronizzati tra le piattaforme per una corrispondenza accurata del pubblico.

## Attiva il pubblico {#activate-audience}

Dopo aver creato il pubblico, attivalo su più piattaforme per coinvolgere gli utenti.

1. **Rivedi tipi di pubblico**: assicurati che i segmenti di pubblico riflettano i comportamenti corretti.

2. **Crea regole di attivazione**: imposta le condizioni per quando e come gli utenti vengono coinvolti in base alle azioni.

3. **Invia a Platform**: attiva il pubblico.

4. **Monitoraggio delle prestazioni**: tieni traccia delle prestazioni del pubblico e apporta le modifiche necessarie.

## Configurare l’estensione di retargeting per l’offsite {#configure-extension}

### Distribuire il Web SDK

Assicurati che Adobe Web SDK sia correttamente integrato nel tuo sito web. Questo SDK consente di raccogliere dati di eventi in tempo reale, fondamentale per un retargeting efficiente.

### Abilitare l’inoltro degli eventi

Imposta l’inoltro di eventi in Platform per inviare i dati sul comportamento degli utenti raccolti alle piattaforme di retargeting. L’inoltro degli eventi garantisce una trasmissione efficiente dei dati, consentendo alle aziende di eseguire il targeting di utenti ad alte intenzioni senza affidarsi ai cookie.

### Allega a regola di retargeting

Assicurati che l’estensione per il retargeting fuori sede sia associata a una regola evento valida in Raccolta dati di Adobe Experience Platform. In genere, è necessario creare una regola globale per attivare azioni chiave, ad esempio `page load` o interazioni utente specifiche.

Per ulteriori informazioni sulla configurazione dell&#39;estensione, consulta la documentazione di [Inoltro eventi](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started).

## Altri casi d’uso {#other-use-cases}

Questo documento fornisce una panoramica dei casi d’uso chiave e delle considerazioni tecniche per sviluppare e utilizzare correttamente la configurazione di Web SDK e Inoltro eventi. Seguendo le procedure descritte e assicurandoti che i prerequisiti necessari siano soddisfatti, puoi migliorare in modo significativo le loro funzionalità di tracciamento e analisi dei dati.

Puoi esplorare altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

- [Coinvolgi e acquisisci nuovi clienti](./prospecting.md) utilizzando i dati dei partner.
- [Personalizza le esperienze nel sito](./offsite-retargeting.md) con il riconoscimento dei visitatori supportato dai partner.
- [Integrare i profili di prime parti](./supplement-first-party-profiles.md) con gli attributi forniti dai partner.