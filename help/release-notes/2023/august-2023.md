---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di agosto 2023 per Adobe Experience Platform.
source-git-commit: 384faa13154386ef2578da4c20ab47f171aefeda
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 38%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 23 agosto 2023**

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Real-Time Customer Data Platform](#rtcdp)
- [Controllo degli accessi basato su attributi](#abac)
- [Dashboard](#dashboards)
- [Raccolta dati](#data-collection)
- [Acquisizione dei dati](#data-ingestion)
- [Preparazione dei dati](#data-prep)
- [Destinazioni](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Servizio di segmentazione](#segmentation)
- [Origini](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Basato su Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) consente alle aziende di unire dati noti e sconosciuti per attivare i profili cliente con decisioni intelligenti in tutto il percorso del cliente.

[!DNL Real-Time CDP] combina più origini dati aziendali per creare profili cliente in tempo reale. I segmenti generati da questi profili possono quindi essere inviati alle destinazioni a valle per fornire esperienze cliente personalizzate individuali su tutti i canali e i dispositivi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Guida all’esempio di ricoinvolgimento intelligente | Il [Nuovo coinvolgimento intelligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) la guida del caso d’uso fornisce dettagli su come coinvolgere nuovamente i clienti che hanno abbandonato una conversione prima di completarla in modo intelligente e responsabile. Questa guida utilizza i seguenti percorsi di esempio per coinvolgere nuovamente i clienti: <ul><li>Percorso di ricoinvolgimento: esegui il targeting dei clienti che hanno abbandonato la navigazione dei prodotti.</li><li>Percorso carrello abbandonato: il targeting dei clienti che hanno inserito prodotti nel carrello ma non hanno ancora completato l’acquisto.</li><li>Percorso di conferma dell’ordine: concentrarsi sugli acquisti di prodotti</li></ul> Utilizza il collegamento dettagliato delle opzioni di feedback nella parte inferiore della sezione [Guida all’esempio di ricoinvolgimento intelligente](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) per fornire un feedback. |
| Supporto dati partner | Esegui il marketing upper funnel in Real-Time CDP, con profili prospect originati dai partner e ID partner, per raggiungere nuovi clienti e arricchire i dati di prime parti: <ul><li>Acquisizione da parte del cliente e indirizzabilità: sfrutta identificatori senza cookie e PII con hash provenienti da partner di dati scelti per raggiungere nuovi clienti e ridurre la dipendenza da cookie di terze parti.</li><li>Marketing full funnel in un unico sistema: segmentazione self-service, cura del pubblico e attivazione nativa per clienti potenziali e noti in un unico sistema.</li><li>Foundation of trust: governa i dati e i profili dei partner con l’utilizzo di dati brevettati, l’etichettatura, i controlli di accesso e altro ancora in modo responsabile per il mercato. Per ulteriori informazioni, consulta le seguenti guide dei casi d’uso: Sono ora disponibili le guide dei casi d’uso per la ricerca di potenziali clienti. Leggi le guide dei casi d’uso per la ricerca di potenziali clienti per scoprire come coinvolgere e acquisire nuovi clienti attraverso i casi d’uso per la ricerca di potenziali clienti:<ul><li>[Prospezione](../../rtcdp/partner-data/prospecting.md)</li><li>[Personalizzazione nel sito](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Integrare i profili di prime parti](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Attiva i tipi di pubblico potenziali](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere [Panoramica di Real-Time CDP](../../rtcdp/overview.md).

## Controllo degli accessi basato su attributi {#abac}

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che offre ai brand attenti alla privacy una maggiore flessibilità per gestire l’accesso degli utenti. È possibile assegnare singoli oggetti, come campi e segmenti dello schema, ai ruoli utente. Questa funzione ti consente di concedere o revocare l’accesso a singoli oggetti per specifici utenti di Platform nella tua organizzazione.

Tramite il controllo dell’accesso basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti a, dati personali sensibili (SPD), informazioni personali (PII) e altri tipi di dati personalizzati in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Configurazione sandbox dei criteri di autorizzazione | Il nuovo [configurazione sandbox dei criteri di autorizzazione](../../access-control/abac/ui/policies.md) Questa funzione ti consente di applicare un criterio di controllo dell’accesso basato su attributi su tutte le sandbox o su un numero selezionato di sandbox, a seconda delle tue esigenze e dei tuoi requisiti. |

{style="table-layout:auto"}

Per ulteriori informazioni sul controllo degli accessi basato su attributi, vedere [panoramica sul controllo degli accessi basato su attributi](../../access-control/abac/overview.md). Per una guida completa sul flusso di lavoro di controllo degli accessi basato su attributi, leggi [guida end-to-end per il controllo degli accessi basato su attributi](../../access-control/abac/end-to-end-guide.md).

## Dashboard {#dashboards}

Adobe Experience Platform fornisce più dashboard attraverso le quali è possibile visualizzare approfondimenti importanti sui dati della tua organizzazione, acquisiti durante le istantanee giornaliere.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Caso di utilizzo: analisi del consenso e tracciamento | Scopri come creare una dashboard del consenso per vari casi d’uso di marketing per i dati di Real-Time CDP con [analisi del consenso e documento di tracciamento](../../dashboards/insights-use-cases/consent-analysis.md). Descrive come creare un pubblico con gli attributi appropriati per le tue esigenze aziendali e quindi utilizzare le informazioni tramite l’utilizzo di widget preconfigurati nell’interfaccia utente di Adobe Experience Platform. Fornisce inoltre istruzioni su come creare widget personalizzati con la funzione delle dashboard definite dall’utente. Il documento illustra la tendenza del consenso e i casi di utilizzo di sovrapposizione del consenso. |

{style="table-layout:auto"}

Per ulteriori informazioni sulle dashboard, tra cui come concedere le autorizzazioni di accesso e creare widget personalizzati, consulta la [panoramica sulle dashboard](../../dashboards/home.md).

## Raccolta dati {#data-collection}

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente lato client e inviarli alla rete Edge di Adobe Experience Platform, per arricchirli, trasformarli e distribuirli a destinazioni Adobe o non Adobe.

**Funzioni nuove o aggiornate**

| Tipo | Funzione | Descrizione |
| --- | --- | --- |
| Tag e inoltro eventi | [Tag Experience Platform (Cina)](/help/tags/ui/publishing/premium-cdn.md) | La nuova funzione Tag di Experience Platform (Cina) migliora l’affidabilità e la latenza del sito web, consentendo tempi di risposta più rapidi per i clienti che distribuiscono i tag sui siti web in Cina. I clienti ora possono utilizzare il codice JavaScript nella libreria Tag durante l’implementazione di siti web in Cina. Questa funzione è stata aggiunta anche al protocollo UPP (Unified Provisioning Protocol), per consentire l’implementazione automatica del prodotto dopo l’acquisto. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere [panoramica delle raccolte dati](../../tags/home.md).

## Acquisizione dei dati {#data-ingestion}

Adobe Experience Platform offre un set completo di funzioni per acquisire qualsiasi tipo e latenza di dati. Puoi acquisire utilizzando le API Batch o Streaming, le origini create da Adobe, i partner di integrazione dei dati o l’interfaccia utente di Adobe Experience Platform.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modifiche ai flussi di lavoro di acquisizione dati | Le righe di dati contenenti valori superiori al tipo di dati specificato (ad esempio, dati lunghi passati come tipo di dati integer) verranno ora rifiutate e verranno segnalati messaggi di errore. In precedenza, queste righe venivano rifiutate senza preavviso. |

Per ulteriori informazioni, leggere [panoramica sull’acquisizione dei dati](../../ingestion/home.md).

## Preparazione dei dati {#data-prep}

La preparazione dei dati consente ai data engineer di mappare, trasformare e convalidare i dati da e per Experience Data Model (XDM).

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Supporto per il filtraggio di identità secondarie | Ora puoi utilizzare la preparazione dati per filtrare le identità provenienti da Adobe Analytics, come AAID e AACUSTOMID. Se escluse, queste identità non vengono acquisite nel Profilo cliente in tempo reale. I dati non filtrati continueranno a essere acquisiti nel data lake. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere [Panoramica sulla preparazione dati](../../data-prep/home.md).

## Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione diretta dei dati da Adobe Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

**Funzionalità nuove o aggiornate** {#destinations-new-updated-functionality}

- Ora puoi [attivare i tipi di pubblico potenziali](../../destinations/ui/activate-prospect-audiences.md) nelle destinazioni di archiviazione cloud.
- Il generale [guardrail di attivazione](../../destinations/guardrails.md#general-activation-guardrails) di un massimo di 100 destinazioni per sandbox è stato aggiornato a _limite rigido_.

Per informazioni più generali sulle destinazioni, consulta la [panoramica sulle destinazioni](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM è una specifica open-source che fornisce strutture e definizioni comuni (schemi) per i dati inseriti in Adobe Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

**Nuovi componenti XDM**

| Tipo di componente | Nome | Descrizione |
| --- | --- | --- |
| Classe | [[!UICONTROL Profilo individuale potenziale cliente XDM]](https://github.com/adobe/xdm/pull/1758/files) | Utilizza questa classe per inserire profili di potenziali clienti provenienti dai casi d’uso più complessi dei fornitori di dati per l’acquisizione clienti. Consulta la sezione [[!UICONTROL Profilo potenziale individuale XDM]](../../xdm/classes/prospect.md) per visualizzare esempi e ulteriori informazioni. |

{style="table-layout:auto"}

**Componenti XDM aggiornati**

| Tipo di componente | Nome | Descrizione aggiornamento |
| --- | --- | --- |
| Estensione ([!UICONTROL Estensione completa Adobe Analytics ExperienceEvent]) | [[!UICONTROL Dati contestuali]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL Dati contestuali] oggetto mappa aggiunto a [!UICONTROL Estensione completa Adobe Analytics ExperienceEvent] per fornire dati contestuali per Adobe Analytics. |
| Gruppo di campi | Multiplo | Vari campi aggiunti a [[!UICONTROL Dettagli segmento evento arricchito]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere [Panoramica del sistema XDM](../../xdm/home.md).

## Identity Service {#identity-service}

Adobe Experience Platform Identity Service offre una panoramica completa della clientela e del relativo comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali ed efficaci in tempo reale.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Modifiche ai limiti del grafo delle identità | Entro la fine di settembre, il grafo delle identità passerà a 50 identità per grafo, e verrà acquisita l’identità più recente. Di conseguenza, l’identità meno recente verrà eliminata in base alla marca temporale e al tipo di identità dell’acquisizione, e i tipi di identità dei cookie verranno eliminati per primi. Oggi, i grafici delle identità hanno un limite di 150 identità per grafico e, una volta raggiunto questo limite, i grafici non vengono più aggiornati. Contatta il rappresentante del tuo account per richiedere una modifica del tipo di identità se la sandbox di produzione contiene: <ul><li>uno spazio dei nomi personalizzato in cui gli identificatori della persona (come gli ID del sistema di gestione delle relazioni con i clienti) sono configurati come tipo di identità cookie/dispositivo.</li><li>uno spazio dei nomi personalizzato in cui gli identificatori cookie/dispositivo sono configurati come tipo di identità tra dispositivi.</li></ul> Queste richieste verranno elaborate manualmente da Adobe Engineering. Per ulteriori informazioni, leggere [guardrail per i dati del servizio Identity](../../identity-service/guardrails.md). |

Per ulteriori informazioni, leggere [Panoramica del servizio Identity](../../identity-service/home.md).

## Servizio di segmentazione {#segmentation}

[!DNL Segmentation Service] consente di segmentare i dati memorizzati in [!DNL Experience Platform] che si riferiscono ai singoli utenti (come clienti, potenziali clienti, utenti o organizzazioni) in tipi di pubblico. Puoi creare tipi di pubblico tramite definizioni di segmenti o altre origini dai tuoi dati di [!DNL Real-Time Customer Profile]. Questi tipi di pubblico sono configurati e gestiti centralmente in [!DNL Platform] e sono facilmente accessibili da qualsiasi soluzione Adobe.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Tipi di pubblico simili (disponibilità limitata) | I tipi di pubblico simili forniscono informazioni intelligenti su ciascun pubblico, sfruttando informazioni basate sull’apprendimento automatico per identificare e indirizzare i clienti di alto valore con le campagne di marketing. Con i tipi di pubblico simili, puoi creare tipi di pubblico espansi per rivolgerti a clienti con prestazioni simili a quelle dei tuoi tipi di pubblico con prestazioni migliori, oppure rivolgerti a clienti simili ai tipi di pubblico convertiti in precedenza. Per ulteriori informazioni sui tipi di pubblico simili, consulta [Panoramica sui tipi di pubblico simili](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere [Panoramica sulla segmentazione](../../segmentation/home.md).

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Disponibilità generale di [!DNL SugarCRM] | [!DNL SugarCRM] Le origini sono ora disponibili. Utilizza le origini [!DNL SugarCRM Accounts & Contacts] e [!DNL SugarCRM Events] per importare i dati dal tuo account [!DNL SugarCRM] su Experience Platform. Per ulteriori informazioni, consulta la [[!DNL SugarCRM] panoramica](../../sources/connectors/crm/sugarcrm.md). |
| Supporto per l’acquisizione su richiesta di flussi di dati di origini nell’interfaccia utente | Ora puoi creare un flusso eseguito su richiesta per un flusso di dati di origini esistenti nell’interfaccia utente. Per ulteriori informazioni, consulta la guida su [creazione di un’esecuzione del flusso su richiesta per le origini utilizzando l’interfaccia utente](../../sources/tutorials/ui/on-demand-ingestion.md). |
| Supporto per nuovi `correlationID` campo per Adobe Analytics | Il `_experience.decisioning.propositions.scopeDetails.correlationID` è ora disponibile nello schema del connettore di origine di Adobe Analytics. Questo campo viene utilizzato a supporto delle classificazioni A4T e verrà popolato a partire da settembre 2023. |

{style="table-layout:auto"}

Per ulteriori informazioni, leggere [panoramica sulle origini](../../sources/home.md).
