---
title: Visualizzazione consegna Edge
description: Questa guida contiene informazioni dettagliate sulla vista Consegna Edge in Adobe Experience Platform Assurance.
source-git-commit: d6b5894a5c5ba3907a8e6dd0d1864f773dd6325c
workflow-type: tm+mt
source-wordcount: '962'
ht-degree: 1%

---

# Visualizzazione consegna Edge in Assurance

Il **[!UICONTROL Consegna Edge]** visualizza all&#39;interno **[!UICONTROL Adobe Experience Platform Assurance]** consente di verificare e convalidare [!UICONTROL AJO in entrata] recapito edge di messaggi alle app web e mobili. Questa visualizzazione è particolarmente utile per risolvere i problemi relativi alla distribuzione di [!UICONTROL AJO in entrata] campagne e percorsi web e mobili.

## Introduzione

Prima di continuare, assicurati di avere accesso ai seguenti servizi:

- L’[interfaccia utente Raccolta dati di Adobe Experience Platform](https://experience.adobe.com/it#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/it/assurance)

Per scoprire come installare **[!UICONTROL Assurance]** nell&#39;applicazione, leggere le [guida all’implementazione di Assurance](../tutorials/implement-assurance.md).

## Utilizzare Assurance con Edge Delivery

Una volta aperto un’ **[!UICONTROL Assurance]** , è possibile aggiungere la **[!UICONTROL Consegna Edge]** visualizza a **[!UICONTROL Assurance]**. Nella parte inferiore del pannello sinistro, seleziona **[!UICONTROL Configura]** per aggiungere **[!UICONTROL Consegna Edge]** visualizza e **Salva** ...

![Aggiungi il plug-in selezionando Configura in basso a sinistra](./images/edge-delivery/add-plugin.png)

Una volta aggiunto, seleziona il **[!UICONTROL Consegna Edge]** visualizzare in **[!UICONTROL Adobe Journey Optimizer]** sezione per convalidare la consegna Edge in entrata.

![È possibile accedere a Edge Delivery nel gruppo di visualizzazione Adobe Journey Optimizer](./images/edge-delivery/ajo-plugins.png)

## Elenco richieste

Nel riquadro principale della visualizzazione viene visualizzato l’elenco delle richieste di consegna Edge. Questo elenco mostra tutti [!UICONTROL AJO in entrata] richieste effettuate a Experience Edge ed elaborate da **[!UICONTROL Servizio di consegna in entrata]**, incluse le richieste di recupero di decisioni sulla personalizzazione e il tracciamento delle interazioni delle proposte di personalizzazione (come visualizzazione, clic, attivazione o esclusione).

Le richieste sono ordinate per marca temporale, con le richieste più recenti in alto. Oltre alla marca temporale, l’elenco include anche una colonna ID richiesta e un tipo di richiesta, che possono essere uno dei seguenti:

- **[!UICONTROL Consegna delle esperienze]**: richiesta per recuperare le decisioni di personalizzazione
- **[!UICONTROL Interazioni con le esperienze]**: richiesta per tenere traccia delle interazioni delle proposte di personalizzazione
- **[!UICONTROL Consegna delle esperienze e interazioni]**: richiesta per recuperare le decisioni di personalizzazione, incluse anche le interazioni della proposta di personalizzazione
- **[!UICONTROL Anteprima consegna]**: richiesta per recuperare le decisioni di personalizzazione dell’anteprima

Le richieste possono essere filtrate anche inserendo un termine di ricerca nella barra di ricerca nella parte superiore dell’elenco. Questo è utile quando si filtrano valori specifici, come gli ID.

![L’elenco delle richieste in entrata viene visualizzato nella vista principale](./images/edge-delivery/request-list.png)

## Visualizzazioni richieste dettagliate

Una volta selezionata una richiesta nella vista principale, a destra vengono visualizzate informazioni dettagliate sulla richiesta selezionata. Questa visualizzazione include le sezioni seguenti:

### Panoramica della richiesta

Questa sezione fornisce una panoramica di alto livello della richiesta selezionata, tra cui [!UICONTROL ID organizzazione], [!UICONTROL Cluster perimetrale], [!UICONTROL ID richiesta] e [!UICONTROL Tipo di richiesta], [!UICONTROL ID sandbox], [!UICONTROL Nome sandbox], [!UICONTROL ID flusso di dati], nonché l&#39;elenco delle superfici di richiesta in caso di [!UICONTROL Consegna delle esperienze] richieste.

![La sezione Panoramica delle richieste fornisce dettagli sulle richieste di alto livello](./images/edge-delivery/request-overview.png)

### Profilo

Questa sezione fornisce informazioni sui dati del profilo utilizzati durante l’elaborazione della richiesta, tra cui la mappa di identità, l’iscrizione al segmento e le impostazioni di consenso.\
Il [!UICONTROL Profilo] Questa sezione è molto utile per la risoluzione di problemi come il mancato funzionamento della consegna come previsto a causa della mancata o ritardata iscrizione al segmento o delle impostazioni di consenso per la rinuncia.

![La sezione Profilo include la mappa di identità, l’iscrizione al segmento e le impostazioni di consenso](./images/edge-delivery/profile.png)

### Attività qualificate

Questa sezione fornisce un elenco delle attività qualificate per la richiesta selezionata, inclusi il tipo di attività, gli ID, lo spazio dei nomi delle identità, le superfici, la pianificazione e i tipi di pubblico. Informazioni più dettagliate sull’attività sono disponibili nella sezione [sezione traccia esecuzione non elaborata](#execution).

![La sezione Attività qualificate contiene i dettagli delle attività qualificate](./images/edge-delivery/qualified-activities.png)

### Attività non qualificate

Questa sezione fornisce un elenco delle attività che non sono state qualificate. Oltre al tipo di attività, agli ID, agli spazi dei nomi delle identità, alle superfici, alle pianificazioni e ai tipi di pubblico, questa sezione include anche un elenco dei motivi per cui l’attività non è stata qualificata.

![La sezione Attività non qualificate contiene dettagli sull’attività non qualificati e motivi di esclusione](./images/edge-delivery/unqualified-activities.png)

### Dettagli messaggio

Questa sezione fornisce informazioni dettagliate sui messaggi consegnati per la richiesta selezionata. Include ID messaggio, frammenti, criteri di decisione, [!UICONTROL Offer decisioning] e il contesto di selezione dei messaggi.

![Sezione contenente i dettagli dei messaggi consegnati come ID messaggio e contesto di selezione, frammenti, criteri di decisione e parametri di decisione](./images/edge-delivery/message-details.png)

### Interazioni

Questa sezione fornisce informazioni dettagliate sulle interazioni tracciate nella richiesta selezionata. Include il tipo di interazione (in `propositionEventType`), nonché i metadati della proposta associati, come i metadati dell&#39;attività (in `scopeDetails.activity`) e token di evento della proposta (in `scopeDetails.characteristics.eventToken`).

![Le interazioni vengono tracciate tramite token di proposta e metadati di attività associati](./images/edge-delivery/interactions.png)

### Tracce non elaborate

Questa sezione fornisce le tracce non elaborate della richiesta selezionata. Include la traccia completa della richiesta, inclusa la richiesta effettiva ricevuta in **[!UICONTROL Servizio di consegna in entrata]**, traccia di esecuzione e traccia di risposta. Ciò è utile per la risoluzione avanzata di problemi come il mancato funzionamento della consegna come previsto a causa della non disponibilità del servizio di consegna, di dati mancanti o errati o per comprendere il flusso completo dell’elaborazione delle richieste.

#### Richiesta

La traccia della richiesta include la richiesta completa così come è stata ricevuta da **[!UICONTROL Servizio di consegna in entrata]** **[!UICONTROL Konduttore]** a monte. Include le intestazioni della richiesta, il corpo e altri metadati. Ad esempio, il payload XDM della richiesta può essere ispezionato in `event.body.xdm` campo.

![Informazioni dettagliate sulla richiesta, compresi intestazioni e corpo, sono disponibili nella traccia della richiesta](./images/edge-delivery/request.png)

#### Esecuzione

La traccia di esecuzione include la traccia completa della richiesta così come è stata elaborata dal **[!UICONTROL Servizio di consegna in entrata]**. Mostra il contesto di esecuzione, la qualifica dell’attività, la selezione dei messaggi e altri passaggi di elaborazione. Eventuali errori o avvisi che si verificavano durante l’elaborazione della richiesta sono reperibili in `context.messages` e `context.exceptions` campi. Informazioni dettagliate sulla qualifica dell’attività sono disponibili nella `context.qualifiedActivitiesDetailed` e `context.unqualifiedActivitiesDetailed` campi.

![La traccia di esecuzione include il contesto di esecuzione, la qualifica dell’attività, la selezione dei messaggi e altri dettagli di elaborazione.](./images/edge-delivery/execution.png)

#### Risposta

La traccia di risposta include la risposta completa restituita da **[!UICONTROL Servizio di consegna in entrata]** a valle di **[!UICONTROL Konduttore]**. Include le intestazioni di risposta, il corpo e altri metadati. Il corpo completo della risposta può essere ispezionato copiando il messaggio con l’ID `1` negli Appunti utilizzando **[!UICONTROL Copia valore]** e incollarlo in un visualizzatore JSON.

![La traccia di risposta contiene il corpo di risposta completo restituito a valle](./images/edge-delivery/response.png)
