---
title: Priorità dello spazio dei nomi
description: Scopri la priorità dello spazio dei nomi in Identity Service.
badge: Beta
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 5674309e4e8f17ad4c951ec4a5cb0cbc0a15ab03
workflow-type: tm+mt
source-wordcount: '1519'
ht-degree: 1%

---

# Priorità dello spazio dei nomi

>[!AVAILABILITY]
>
>Questa funzione non è ancora disponibile; il programma beta per le regole di collegamento del grafo delle identità dovrebbe iniziare a luglio per le sandbox di sviluppo. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione.

Ogni implementazione del cliente è unica e personalizzata per soddisfare gli obiettivi di una particolare organizzazione e, come tale, l’importanza di un dato spazio dei nomi varia da cliente a cliente. Esempi reali includono:

* Da un lato, lo spazio dei nomi E-mail potrebbe rappresentare un’entità persona e quindi essere univoco per persona. D’altra parte, un altro cliente potrebbe considerare lo spazio dei nomi E-mail come un identificatore non affidabile e, pertanto, potrebbe consentire l’associazione di un singolo ID del sistema di gestione delle relazioni con i clienti a più identità con lo spazio dei nomi E-mail.
* È possibile raccogliere il comportamento in linea utilizzando uno spazio dei nomi &quot;ID accesso&quot;. Questo ID di accesso potrebbe avere una relazione 1:1 con l’ID del sistema di gestione delle relazioni con i clienti, che memorizza quindi gli attributi da un sistema di gestione delle relazioni con i clienti e può essere considerato lo spazio dei nomi più importante. In questo caso, stai quindi determinando che lo spazio dei nomi dell’ID del sistema di gestione delle relazioni con i clienti è una rappresentazione più accurata di una persona, mentre lo spazio dei nomi dell’ID di accesso è il secondo più importante.

Devi effettuare configurazioni in Identity Service che riflettano l’importanza degli spazi dei nomi, in quanto questo influisce sul modo in cui i profili vengono formati e segmentati.

## Determinare le priorità

La determinazione della priorità dello spazio dei nomi si basa sui seguenti fattori:

### Struttura del grafico delle identità

Se il grafico strutturato della tua organizzazione è a livelli, la priorità dello spazio dei nomi deve riflettere questo in modo che i collegamenti corretti vengano rimossi in caso di compressione del grafico.

>[!TIP]
>
>* Per &quot;compressione di un grafico&quot; si intendono gli scenari in cui più profili diversi vengono inavvertitamente uniti in un singolo grafico di identità.
>
>* Un grafico a livelli si riferisce a grafici di identità con più livelli di collegamenti. Visualizza l’immagine seguente per un esempio di grafico con tre livelli.

![Diagramma dei livelli del grafico](../images/namespace-priority/graph-layers.png)

### Significato semantico dello spazio dei nomi

Un’identità rappresenta un oggetto del mondo reale. Tre oggetti sono rappresentati nel grafico delle identità. In ordine di importanza, sono:

* Persone (multidispositivo, e-mail, numero di telefono)
* Dispositivo hardware
* Browser web (cookie)

Gli spazi dei nomi delle persone sono relativamente immutabili rispetto ai dispositivi hardware (come IDFA, GAID), che sono relativamente immutabili rispetto ai browser web. In sostanza, tu (persona) sarà sempre un’unica entità, che può avere più dispositivi hardware (telefono, laptop, tablet, ecc.) e utilizzare più browser (Google Chrome, Safari, FireFox, ecc.)

Un altro modo per affrontare questo argomento è attraverso la cardinalità. Per una determinata entità persona, quante identità verranno create? Nella maggior parte dei casi, una persona avrà un ID CRM, una manciata di identificatori di dispositivi hardware (i ripristini IDFA/GAID non dovrebbero accadere spesso) e ancora più cookie (un individuo potrebbe immaginabilmente lanciare su più dispositivi, utilizzare la modalità in incognito, o reimpostare i cookie in qualsiasi momento). Generalmente, **la cardinalità inferiore indica uno spazio dei nomi con un valore più alto**.

## Convalidare le impostazioni di priorità dello spazio dei nomi

Una volta acquisita un’idea di come assegnare la priorità agli spazi dei nomi, puoi utilizzare lo strumento Simulazione grafico per verificare vari scenari di compressione dei grafici e assicurarti che le configurazioni di priorità restituiscano i risultati attesi. Per ulteriori informazioni, consulta la guida sull’utilizzo di [Strumento Simulazione grafico](./graph-simulation.md).

## Configurare la priorità dello spazio dei nomi

La priorità dello spazio dei nomi può essere configurata utilizzando [!UICONTROL Impostazioni identità]. In [!UICONTROL Impostazioni identità] , è possibile trascinare e rilasciare uno spazio dei nomi per determinarne l&#39;importanza relativa.

>[!IMPORTANT]
>
>Non è possibile assegnare priorità agli spazi dei nomi dei dispositivi/cookie rispetto agli spazi dei nomi delle persone. Questa restrizione evita il verificarsi di configurazioni errate.

## Utilizzo priorità dello spazio dei nomi

Attualmente, la priorità dello spazio dei nomi influenza il comportamento del sistema di Real-Time Customer Profile. Il diagramma seguente illustra questo concetto. Per ulteriori informazioni, consulta la guida su [Diagrammi di architettura di Adobe Experience Platform e applicazioni](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications).

![Diagramma dell&#39;ambito applicazione prioritario dello spazio dei nomi](../images/namespace-priority/application-scope.png)

### Servizio Identity: algoritmo di ottimizzazione delle identità

Per strutture di grafo relativamente complesse, la priorità dello spazio dei nomi svolge un ruolo importante nel garantire che i collegamenti corretti vengano rimossi quando si verificano scenari di collasso del grafo. Per ulteriori informazioni, consulta [[!DNL Identity Optimization Algorithm] panoramica](../identity-graph-linking-rules/identity-optimization-algorithm.md).

### Real-Time Customer Profile: determinazione dell’identità primaria per gli eventi esperienza

* Per gli eventi esperienza, una volta configurate le impostazioni di identità per una determinata sandbox, l’identità primaria sarà determinata dalla priorità più elevata dello spazio dei nomi.
   * Questo perché gli eventi di esperienza sono di natura dinamica. Una mappa di identità può contenere tre o più identità e la priorità dello spazio dei nomi assicura che lo spazio dei nomi più importante sia associato all’evento esperienza.
* Di conseguenza, le seguenti configurazioni **non sarà più utilizzato da Real-Time Customer Profile**:
   * Casella di controllo &quot;Primary&quot; sul tipo di elemento dati in WebSDK.
   * Eventuali campi contrassegnati come identità primaria in uno schema XDM Experience Event Class.
   * Impostazioni di identità primaria predefinite nel connettore di origine di Adobe Analytics (ECID o AAID).
* D&#39;altro canto, **la priorità dello spazio dei nomi non determina l’identità primaria per i record del profilo**.
   * Per i record di profilo, puoi utilizzare l’area di lavoro schemi nell’interfaccia utente di Experienci Platform per definire i campi di identità, inclusa l’identità primaria. Leggi la guida su [definizione dei campi di identità nell’interfaccia utente](../../xdm/ui/fields/identity.md) per ulteriori informazioni.

>[!NOTE]
>
>* La priorità dello spazio dei nomi è **proprietà di uno spazio dei nomi**. Si tratta di un valore numerico assegnato a uno spazio dei nomi per indicarne l’importanza relativa.
>
>* L’identità primaria è l’identità in cui è memorizzato un frammento di profilo in base a. Un frammento di profilo è un record di dati che memorizza informazioni su un determinato utente: attributi (di solito acquisiti tramite record di gestione delle relazioni con i clienti) o eventi (di solito acquisiti da eventi di esperienza o dati online).

### Scenario con grafico di esempio

Questa sezione fornisce un esempio di come la configurazione della priorità può influenzare i dati.

Supponiamo che per una determinata sandbox siano stabilite le seguenti configurazioni:

| Namespace | Applicazione reale dello spazio dei nomi | Priorità |
| --- | --- | --- |
| CRMID | Utente | 1 |
| IDFA | Dispositivo hardware Apple (iPhone, IPad, ecc.) | 2 |
| GAID | Dispositivo hardware Google (Google Pixel, Pixelbook, ecc.) | 3 |
| ECID | Browser web (Firefox, Safari, Google Chrome, ecc.) | 4 |
| AAID | Browser web | 5 |

{style="table-layout:auto"}

Date le configurazioni sopra descritte, le azioni degli utenti e la determinazione dell’identità primaria saranno risolte come tali:

| Azione utente (evento esperienza) | Stato di autenticazione | Origine dati | Mappa identità | Identità primaria (chiave primaria del frammento di profilo) |
| --- | --- | --- | --- | --- |
| Visualizza pagina offerta carta di credito | Non autenticato (anonimo) | SDK per web | {ECID} | ECID |
| Visualizza pagina della guida | Non autenticato | Mobile SDK | {ECID, IDFA} | IDFA |
| Visualizza saldo conto corrente | autenticato | SDK per web | {ID CRM, ECID} | ID CRM |
| Iscriviti al prestito per la casa | autenticato | Connettore di origine di Analytics | {ID CRM, ECID, AAID} | ID CRM |
| Trasferisci $1.000 dal controllo al risparmio | autenticato | Mobile SDK | {ID CRM, GAID, ECID} | ID CRM |

{style="table-layout:auto"}

### Servizio di segmentazione: archiviazione dei metadati di iscrizione al segmento

![Un diagramma dell’archiviazione dell’appartenenza ai segmenti](../images/namespace-priority/segment-membership-storage.png)

Per un determinato profilo unito, le appartenenze ai segmenti verranno memorizzate in base all’identità con lo spazio dei nomi con priorità più elevata.

Ad esempio, si supponga che siano presenti due profili:

* Il primo profilo rappresenta John.
* Il secondo profilo rappresenta Jane.

Se John e Jane condividono un dispositivo, allora l’ECID (browser web) si trasferisce da una persona all’altra. Tuttavia, questo non influenza le informazioni sull’iscrizione al segmento memorizzate per John e Jane.

Se i criteri di qualificazione del segmento si basassero esclusivamente su eventi anonimi memorizzati in base all’ECID, Jane si qualificherebbe per quel segmento

## Implicazioni su altri servizi Experienci Platform {#implications}

Questa sezione illustra come la priorità dello spazio dei nomi può influenzare altri servizi Experienci Platform.

### Gestione avanzata del ciclo di vita dei dati

Il record di igiene dei dati elimina le richieste nel modo seguente, per una determinata identità:

* Profilo cliente in tempo reale: elimina qualsiasi frammento di profilo con identità specificata come identità principale. **L’identità primaria nel profilo verrà ora determinata in base alla priorità dello spazio dei nomi.**
* Data lake: elimina qualsiasi record con l’identità specificata come identità primaria.

Per ulteriori informazioni, leggere [panoramica sulla gestione avanzata del ciclo di vita](../../hygiene/home.md).

### Data lake

L’acquisizione dei dati nel data lake continuerà a rispettare le impostazioni di identità primaria configurate in [SDK per web](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) e gli schemi.

Il data lake non determinerà l’identità primaria in base alla priorità dello spazio dei nomi. Ad esempio, Adobe Customer Journey Analytics continuerà a utilizzare i valori nella mappa delle identità anche dopo l’abilitazione della priorità dello spazio dei nomi (ad esempio, l’aggiunta di un set di dati a una nuova connessione), perché il Customer Journey Analytics utilizza i propri dati dal data lake.

### Schemi Experience Data Model (XDM)

Qualsiasi schema che non sia un evento esperienza XDM, come ad esempio Profili individuali XDM, continuerà a rispettare qualsiasi [campi contrassegnati come identità](../../xdm/ui/fields/identity.md).

Per ulteriori informazioni sugli schemi XDM, consulta [panoramica degli schemi](../../xdm/home.md).

### Servizi intelligenti

Quando selezioni i dati, dovrai specificare uno spazio dei nomi, che verrà utilizzato per determinare gli eventi che calcolano i punteggi e gli eventi che memorizzano i punteggi calcolati. Si consiglia di selezionare lo spazio dei nomi che rappresenta una persona.

* Se raccogli dati di comportamento web utilizzando WebSDk, ti consigliamo di scegliere lo spazio dei nomi ID CRM all’interno della mappa di identità.
* Se raccogli dati sul comportamento web utilizzando il connettore di origine di Analytics, seleziona il descrittore di identità (ID del sistema di gestione delle relazioni con i clienti).

Questa configurazione consente di calcolare i punteggi solo utilizzando eventi autenticati.

Per ulteriori informazioni su, consulta i documenti su [Attribution AI](../../intelligent-services/attribution-ai/overview.md) e [IA per l’analisi dei clienti](../../intelligent-services/customer-ai/overview.md).

### Privacy Service

[Richieste di eliminazione Privacy Service](../privacy.md) funziona nel modo seguente, per una determinata identità:

* Profilo cliente in tempo reale: elimina qualsiasi frammento di profilo con valore di identità specificato come identità primaria. **L’identità primaria nel profilo verrà ora determinata in base alla priorità dello spazio dei nomi.**
* Data lake: elimina qualsiasi record con l’identità specificata come identità primaria o secondaria.

Per ulteriori informazioni, leggere [Panoramica di Privacy Service](../../privacy-service/home.md).
