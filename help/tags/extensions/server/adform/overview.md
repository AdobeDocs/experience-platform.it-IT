---
keywords: integrazione adform; adform;
title: Integrazione di Adform per il retargeting non autenticato
description: Questa integrazione di Adobe Experience Platform consente di eseguire il retargeting degli utenti in base a ECID.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: 37eb9453-fc3c-481e-94ea-54d9b1545631
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# Panoramica dell&#39;estensione [!DNL Adform]

L&#39;estensione [[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud) abilita l&#39;inoltro degli eventi lato server in Adobe Experience Platform, consentendo agli inserzionisti, alle agenzie multimediali e agli editori di sincronizzare i dati direttamente con il sistema Fusion di Adobe ID. Questa integrazione consente alle aziende di coinvolgere il pubblico su più canali, migliorando le prestazioni delle campagne e fornendo soluzioni personalizzate per perfezionare le strategie pubblicitarie digitali e massimizzare l’efficacia degli annunci.

A differenza del tracciamento lato client tradizionale, questa estensione elimina la necessità di cookie di terze parti sfruttando gli ID di prime parti, in particolare l’ECID (Experience Cloud ID) sincronizzato con Adform. Questo consente un retargeting del pubblico senza soluzione di continuità senza richiedere l’implementazione lato client di JavaScript.

Questa guida illustra come installare, configurare e implementare l’estensione per inoltrare gli eventi dalle proprietà digitali di un brand tramite Adobe Edge Network to Adform per consentire il retargeting fluido dei visitatori.

## Retargeting fuori sede

Tramite il retargeting fuori sede, puoi coinvolgere nuovamente i potenziali clienti che hanno visitato il tuo sito web ma non hanno convertito. Adform consente di raggiungere questi tipi di pubblico su varie piattaforme, rafforzando la presenza del brand e aumentando le opportunità di conversione. Utilizza questa integrazione per:

* Rivolgiti a visitatori sconosciuti senza l’utilizzo di cookie di terze parti.
* Attiva i tipi di pubblico direttamente sugli ECID senza utilizzare identificatori alternativi ai cookie di terze parti o tag aggiuntivi sulle proprietà digitali.

Adform consente di:

* Trasforma facilmente i tipi di pubblico di prima parte identificati negli ECID in ID indirizzabili per le campagne pubblicitarie digitali.
* Collega gli ECID a più di 40 soluzioni ID disponibili per ottimizzare portata, frequenza e prestazioni rispetto al pubblico di destinazione.

### Attivazione del pubblico lato server con [!DNL Adform] {#server-side-activation}

A differenza delle implementazioni ID lato client tradizionali, questa integrazione non richiede la distribuzione di una soluzione del fornitore ID sulle proprietà digitali. Al contrario, abilita l’attivazione del pubblico lato server sfruttando gli ECID già sincronizzati con Adform. I vantaggi principali includono:

* **Nessuna distribuzione JavaScript lato client**: non è necessario gestire la logica di riconoscimento dei visitatori lato client o decrittografare gli ID lato client in versioni stabili di durata maggiore.
* **Sincronizzazione perfetta del pubblico**: gli ECID sono mappati sul grafo ID interno di Adform per consentire un retargeting efficiente tra le piattaforme.
* **Maggiore portata e deduplicazione**: il grafo di Fusion ID connette gli ECID a più identificatori garantendo una corrispondenza di pubblico di alta qualità.

## Prerequisiti {#prerequisites}

Prima di integrare Adform con Adobe, assicurati di soddisfare i seguenti prerequisiti:

1. **Installazione di Adobe Web SDK**: è necessario implementare Adobe Web SDK per facilitare la raccolta dei dati e l&#39;inoltro degli eventi.

2. **CDP o SKU connessione**: è necessario disporre dello SKU di Adobe Customer Data Platform (CDP) Prime o Ultimate oppure dello SKU connessione per consentire una comunicazione lato client e lato server senza interruzioni.

3. **Configurazione Adobe Experience Platform Edge Network**:
   * Assicurati che Edge Network sia configurato per supportare l’inoltro di eventi in tempo reale per il retargeting fuori sede. Per ulteriori informazioni, consulta la [Guida introduttiva all&#39;inoltro degli eventi](https://experienceleague.adobe.com/it/docs/experience-platform/tags/event-forwarding/getting-started) di Adobe.
   * Questo passaggio è fondamentale per trasmettere i dati all’endpoint lato server di Adform in modo efficiente.

Una volta stabiliti questi prerequisiti, è possibile continuare a configurare e distribuire l&#39;estensione [!DNL Adform].

## Configura l&#39;estensione [!DNL Adform] {#configure-adform-extension}

Per configurare l&#39;estensione [!DNL Adform], eseguire i passaggi descritti nelle sezioni seguenti.

### Installare e configurare l’estensione

Passa a [!DNL Adform extension] nell&#39;interfaccia utente di inoltro degli eventi e immetti i valori richiesti:

| Input | Descrizione |
| --- | --- |
| ID configurazione tracciamento | Identificatore univoco fornito da Adform per il tracciamento degli eventi. |
| Dominio globale | Utilizza `a1.adform.net` per ottimizzare le prestazioni ed evitare problemi di latenza regionali. |

Salva la configurazione dopo aver inserito questi dettagli.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### Definire i parametri di tracciamento

L’azione &quot;track&quot; è la regola dell’evento principale. Si attiva in base ad azioni predefinite, in genere `page load.` Includi i seguenti parametri:

**Parametri richiesti:**

| Parametri | Descrizione |
| --- | --- |
| `Page Name` | Identifica la pagina o l’azione dell’utente. |
| `User Agent` | Acquisisce informazioni per la corrispondenza del pubblico. |
| `IP Address` | Fondamentale per il targeting e il retargeting accurati. |

**Parametri consigliati:**

| Parametri | Descrizione |
| --- | --- |
| `Page URL` | Identifica la pagina o l’azione dell’utente. |
| `Referral URL` | Acquisisce informazioni per la corrispondenza del pubblico. |
| `ECID` | Fondamentale per il targeting e il retargeting accurati. |
| `Source Domain` | Fondamentale per il targeting e il retargeting accurati. |

<!-- ![Tracking parameters for Adform]() -->

### Allega regola

L&#39;estensione deve essere associata a una regola per funzionare correttamente. Se non vengono impostate condizioni, crea una regola globale per assicurarti che venga sempre eseguita.

>[!NOTE]
>
>Se l&#39;estensione non viene attivata, verifica che sia associata a una regola valida in Raccolta dati di Adobe Experience Platform.

<!-- ![Attach a rule to the Adform extension]() -->

## Convalidare e distribuire

Assicurati che l&#39;estensione sia installata e configurata correttamente e che tutti gli elementi dati richiesti siano mappati, tra cui:

* [ECID](/help/identity-service/features/ecid.md)
* Nome pagina
* URL di riferimento
* Agente utente
* Indirizzo IP

Dopo aver inserito tutti i campi obbligatori e completato il test, seleziona **build** per distribuire l&#39;estensione.

## Passaggi successivi

È ora necessario comprendere in che modo Adform si integra con le funzionalità lato server di Adobe e può valutare la fattibilità dell’integrazione all’interno dell’infrastruttura esistente. Per ulteriori informazioni, consultare la [documentazione ufficiale di Adform](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud).
