---
title: Priorità dello spazio dei nomi
description: Scopri la priorità dello spazio dei nomi in Identity Service.
exl-id: bb04f02e-3826-45af-b935-752ea7e6ed7c
source-git-commit: 8157eaf3d79523995fd50d02234e7873cffcea14
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 3%

---

# Priorità dello spazio dei nomi {#namespace-priority}

>[!CONTEXTUALHELP]
>id="platform_identities_namespacepriority"
>title="Priorità dello spazio dei nomi"
>abstract="La priorità dello spazio dei nomi determina il modo in cui i collegamenti vengono rimossi dal grafico delle identità."

>[!AVAILABILITY]
>
>Le regole di collegamento del grafo delle identità sono attualmente a disponibilità limitata. Contatta il team del tuo account Adobe per informazioni su come accedere alla funzione nelle sandbox di sviluppo.

Ogni implementazione del cliente è unica e personalizzata per soddisfare gli obiettivi di una particolare organizzazione e, come tale, l’importanza di un dato spazio dei nomi varia da cliente a cliente. Esempi reali includono:

* La tua azienda potrebbe considerare ogni indirizzo e-mail come un&#39;entità a persona singola e quindi utilizzare [le impostazioni di identità](./identity-settings-ui.md) per configurare lo spazio dei nomi e-mail come univoco. Un’altra società, tuttavia, potrebbe voler rappresentare entità a persona singola come se avessero più indirizzi e-mail e quindi configurare lo spazio dei nomi e-mail come non univoco. Queste aziende dovrebbero utilizzare un altro namespace identità come univoco, ad esempio uno spazio dei nomi CRMID, in modo che possa esserci un identificatore di una singola persona collegato a più indirizzi e-mail.
* Puoi raccogliere il comportamento online utilizzando uno spazio dei nomi &quot;ID accesso&quot;. Questo ID di accesso potrebbe avere una relazione 1:1 con il CRMID, che quindi memorizza gli attributi da un sistema CRM e può essere considerato il namespace più importante. In questo caso, si determina che lo spazio dei nomi CRMID è una rappresentazione più accurata di una persona, mentre lo spazio dei nomi ID di accesso è il secondo più importante.

È necessario creare configurazioni in Identity Service che riflettano l&#39;importanza degli spazi dei nomi, in quanto ciò influenza il modo in cui i profili e i relativi grafici di identità vengono formati e suddivisi.

## Stabilisci le tue priorità

La determinazione della priorità dello spazio dei nomi si basa sui seguenti fattori:

### Struttura del grafico di identità

Se la struttura del grafico dell&#39;organizzazione è stratificata, la priorità dello spazio dei nomi dovrebbe riflettere questo aspetto in modo che i collegamenti corretti vengano rimossi in caso di compressione del grafico.

>[!TIP]
>
>* &quot;Compressione del grafico&quot; si riferisce a scenari in cui più profili disparati vengono inavvertitamente fusi insieme in un unico grafico di identità.
>
>* Un grafico a più livelli si riferisce a grafici di identità che hanno più livelli di collegamenti. Visualizza l&#39;immagine seguente per un esempio di grafico con tre livelli.

![Un diagramma dei livelli del grafico](../images/namespace-priority/graph-layers.png)

### Significato semantico dello spazio dei nomi

Un&#39;identità rappresenta un oggetto del mondo reale. Il grafico dell&#39;identità rappresenta tre oggetti. In ordine di importanza, sono:

* Persone (Cross-dispositivo, Email, Numero di telefono)
* Hardware dispositivo
* Browser web (cookie)

Gli spazi dei nomi delle persone sono relativamente immutabili rispetto ai dispositivi hardware (come IDFA, GAID), che sono relativamente immutabili rispetto ai browser web. In sostanza, tu (persona) sarà sempre un’unica entità, che può avere più dispositivi hardware (telefono, laptop, tablet, ecc.) e utilizzare più browser (Google Chrome, Safari, FireFox, ecc.)

Un altro modo per affrontare questo argomento è attraverso la cardinalità. Per una determinata entità persona, quante identità verranno create? Nella maggior parte dei casi, una persona avrà un CRMID, una manciata di identificatori di dispositivi hardware (i ripristini IDFA/GAID non dovrebbero accadere spesso) e ancora più cookie (un individuo potrebbe ragionevolmente navigare su più dispositivi, utilizzare la modalità in incognito, o reimpostare i cookie in qualsiasi momento). In genere, **la cardinalità inferiore indica uno spazio dei nomi con un valore superiore**.

## Convalidare le impostazioni di priorità dello spazio dei nomi

Una volta che si ha un&#39;idea di come assegnare la priorità agli spazi dei nomi, è possibile utilizzare il strumento Simulazione grafico nella interfaccia per testare vari scenari di compressione del grafico e assicurarsi che le configurazioni prioritarie restituiscano i risultati del grafico previsti. Per ulteriori informazioni, leggi la guida all&#39;utilizzo di [Graph Simulation strumento](./graph-simulation.md).

## Configurare la priorità dello spazio dei nomi

La priorità dello spazio dei nomi può essere configurata utilizzando l&#39;[interfaccia utente delle impostazioni delle identità](./identity-settings-ui.md). Nell’interfaccia delle impostazioni di identità, puoi trascinare e rilasciare uno spazio dei nomi per determinarne l’importanza relativa.

>[!IMPORTANT]
>
>Non è possibile dare priorità agli spazi dei nomi dispositivo/cookie rispetto ai namespace delle persone. Questa restrizione evita il verificarsi di configurazioni errate.

## Utilizzo della priorità dello spazio dei nomi

Attualmente, la priorità dello spazio dei nomi influenza il comportamento del sistema del profilo cliente in tempo reale. Il diagramma seguente illustra questo concetto. Per ulteriori informazioni, leggi la guida ai [diagrammi](https://experienceleague.adobe.com/en/docs/blueprints-learn/architecture/architecture-overview/platform-applications) dell&#39;architettura di Adobe Experience Platform e delle applicazioni.

![Diagramma della priorità dello spazio dei nomi applicazione ambito](../images/namespace-priority/application-scope.png)

## Servizio Identity: algoritmo di ottimizzazione dell&#39;identità

For relatively complex graph structures, namespace priority plays an important role in ensuring that the correct links are removed when graph collapse scenarios happen. For more information read the [identity optimization algorithm overview](../identity-graph-linking-rules/identity-optimization-algorithm.md).

## Profilo cliente in tempo reale: determinazione dell&#39;identità primaria per gli eventi di esperienza

* Dopo aver configurato le impostazioni di identità per una determinata sandbox, l&#39;identità primaria per gli eventi di esperienza sarà determinata dalla priorità dello spazio dei nomi più alta nella configurazione.
   * Questo perché gli eventi dell&#39;esperienza sono di natura dinamica. Una mappa identità può contenere tre o più identità e la priorità dello spazio dei nomi garantisce che lo spazio dei nomi più importante sia associato all&#39;evento esperienza.
* Di conseguenza, le **seguenti configurazioni non saranno più utilizzate da Real-Time Customer Profile**:
   * La configurazione dell&#39;identità primaria (`primary=true`) quando si inviano identità in identityMap tramite Web SDK, Mobile SDK o API Edge Network Server (lo spazio dei nomi dell&#39;identità e il valore dell&#39;identità continueranno a essere utilizzati in Profilo). **Nota**: i servizi esterni al profilo cliente in tempo reale like l&#39;archiviazione o Adobe Target del data lake continueranno a utilizzare la configurazione dell&#39;identità primaria (`primary=true`).
   * Tutti i campi contrassegnati come identità primaria in uno schema XDM Experience Event Class.
   * Impostazioni di identità primaria predefinite nel connettore di origine Adobe Analytics (ECID o AAID).
* D&#39;altra parte, la priorità dello spazio dei nomi **non determina l&#39;identità primaria per i record di profilo**.
   * Per i record di profilo, devi continuare a definire i campi di identità nello schema, inclusa l’identità primaria. Per ulteriori informazioni, leggere la guida alla [definizione dei campi di identità nell&#39;interfaccia](../../xdm/ui/fields/identity.md) .

>[!TIP]
>
>* La priorità dello spazio dei nomi è **una proprietà di un namespace**. È un valore numerico assegnato a uno spazio dei nomi per indicarne l&#39;importanza relativa.
>
>* L&#39;identità primaria è l&#39;identità in cui viene memorizzato un frammento di profilo. Un frammento di profilo è un record di dati in cui sono memorizzate informazioni su un determinato utente: attributi (ad esempio, record CRM) o eventi (ad esempio, l&#39;esplorazione di siti Web).

### Scenario di esempio

In questa sezione viene fornito un esempio di come la configurazione delle priorità può influire sui dati.

Supponiamo che per una determinata sandbox siano stabilite le seguenti configurazioni:

| Namespace | Applicazione reale dello spazio dei nomi | Priorità |
| --- | --- | --- |
| CRMID | Utente | 1 |
| IDFA | Apple hardware device (iPhone, IPad, etc.) | 2 |
| GAID | dispositivo hardware Google (Google Pixel, Pixelbook, ecc.) | 3 |
| ECID | browser web (Firefox, Safari, Google Effetto cromatura, ecc.) | 4 |
| AAID · | Browser web | 5 |

{style="table-layout:auto"}

Date le configurazioni sopra delineate, le azioni utente e la determinazione dell&#39;identità primaria, saranno risolte come tali:

| Azione dell&#39;utente (evento esperienza) | Stato Authentication | Origine dati | Namespace nell&#39;evento | Spazio dei nomi dell&#39;identità primaria |
| --- | --- | --- | --- | --- |
| Visualizza pagina dell&#39;offerta scheda di credito | Non autenticato (anonimo) | Web SDK | `{ECID}` | ECID |
| Visualizza pagina della guida | Non autenticato | SDK mobile | `{ECID, IDFA}` | IDFA |
| Visualizza il controllo account saldo | autenticato | Web SDK | `{CRMID, ECID}` | CRMID |
| Iscriviti al prestito per la casa | autenticato | Analytics connettore sorgente | `{CRMID, ECID, AAID}` | CRMID |
| Trasferisci $ 1.000 dall&#39;assegno al risparmio | autenticato | SDK mobile | `{CRMID, GAID, ECID}` | CRMID |

{style="table-layout:auto"}

## Servizio di segmentazione: archiviazione dei metadati di iscrizione al segmento

![Diagramma dell&#39;archivio di appartenenza ai segmenti](../images/namespace-priority/segment-membership-storage.png)

Per un determinato profilo unito, le appartenenze al segmento verranno memorizzate in base all’identità con la priorità più elevata dello spazio dei nomi.

Ad esempio, si supponga che siano presenti due profili:

* Il profilo 1 rappresenta John.
   * Il profilo di John si qualifica per S1 (segmento iscrizione 1). Ad esempio, S1 potrebbe riferirsi a un segmento di clienti che si identificano come maschi.
   * Anche il profilo di John si qualifica per S2 (segmento iscrizione 2). Potrebbe riferirsi a un segmento di clienti il cui stato di fedeltà è oro.
* Il profilo 2 rappresenta Jane.
   * Il profilo di Jane è idoneo per S3 (appartenenza al segmento 3). Questo potrebbe riferirsi a un segmento di clienti che si identificano come donne.
   * Anche il profilo di Jane si qualifica per S4 (segmento iscrizione 4). Questo potrebbe riferirsi a un segmento di clienti il cui stato di fedeltà è platino.

Se John e Jane condividono un dispositivo, l&#39;ECID (web browser) si trasferisce da una persona all&#39;altra. Tuttavia, ciò non influenza il segmento iscrizione le informazioni memorizzate su John e Jane.

Se i criteri di qualificazione del segmento fossero basati esclusivamente su eventi anonimi memorizzati nell&#39;ECID, Jane si qualificherebbe per quel segmento.

## Implicazioni su altri servizi Experience Platform {#implications}

This section outlines how namespace priority can affect other Experience Platform services.

### Gestione avanzata del ciclo di vita dei dati

Il record di igiene dei dati elimina le richieste nel modo seguente, per una determinata identità:

* Profilo cliente in tempo reale: elimina qualsiasi frammento di profilo con identità specificata come identità principale. **L&#39;identità principale nel profilo verrà ora determinata in base alla priorità dello spazio dei nomi.**
* Data lake: elimina qualsiasi record con l&#39;identità specificata come identità primaria. A differenza di Real-Time Customer Profile, l&#39;identità primaria nel data lake si basa sull&#39;identità primaria specificata in WebSDK (`primary=true`) o su un campo contrassegnato come identità primaria

Per ulteriori informazioni, leggere la [panoramica sulla gestione avanzata del ciclo di vita](../../hygiene/home.md).

### Attributi calcolati

If identity settings is enabled, then computed attributes will use namespace priority to store the computed attribute value. Per un dato evento, l’identità con la priorità più elevata dello spazio dei nomi avrà il valore dell’attributo calcolato scritto in base a essa. For more information, read the [computed attributes UI guide](../../profile/computed-attributes/ui.md).

### Data lake

L&#39;inserimento dei dati nel data lake continuerà a rispettare le impostazioni di identità primarie configurate negli [schemi e negli SDK](../../tags/extensions/client/web-sdk/data-element-types.md#identity-map) Web.

Il data lake non determina l&#39;identità primaria in base alla priorità dello spazio dei nomi. Ad esempio, Adobe Systems Customer Journey Analytics continuerà a utilizzare valori nella mappa identità lineare dopo l&#39;abilitazione della priorità dello spazio dei nomi (ad esempio, l&#39;aggiunta di un set di dati a una nuova connessione), perché Customer Journey Analytics utilizza i propri dati dal data lake.

### Schemi XDM (Experience Data Model)

Qualsiasi schema che non sia un evento esperienza XDM, ad esempio Profili individuali XDM, continuerà a rispettare tutti i [campi contrassegnati come identità](../../xdm/ui/fields/identity.md).

Per ulteriori informazioni sugli schemi XDM, leggi la [panoramica](../../xdm/home.md) degli schemi.

### Servizi intelligenti

Quando si selezionano i dati, è necessario specificare uno spazio dei nomi, che verrà utilizzato per determinare gli eventi che calcolano i punteggi e gli eventi che store i punteggi calcolati. Si consiglia di selezionare lo spazio dei nomi che rappresenta una persona.

* Se si raccolgono dati sul comportamento Web utilizzando WebSDk, si consiglia di scegliere lo spazio dei nomi CRMID all&#39;interno della mappa identità.
* Se si raccolgono dati sul comportamento Web utilizzando il connettore di origine Analytics, è necessario selezionare il descrittore di identità (CRMID).

Questa configurazione determina il calcolo dei punteggi utilizzando solo eventi autenticati.

Per ulteriori informazioni, leggere i documenti in [IA per l&#39;attribuzione](../../intelligent-services/attribution-ai/overview.md) e [IA per l&#39;analisi dei clienti](../../intelligent-services/customer-ai/overview.md).

### Destinazioni create dai partner

I risultati aggiornati della squalifica del pubblico per i profili associati a un dispositivo condiviso potrebbero non essere inviati a destinazioni downstream. Ciò può accadere in alcuni rari casi in cui:

* La qualifica dell&#39;audience si basa solo sull&#39;attività anonima.
* Gli accessi su più profili avvengono in un breve periodo di tempo.

Per ulteriori informazioni sulle destinazioni create dai partner, consulta la [panoramica sulle destinazioni](../../destinations/home.md#adobe-built-and-partner-built-destinations).

### Privacy Service

[Privacy Service richieste](../privacy.md) di eliminazione funzionano nel modo seguente, per una determinata identità:

* Profilo cliente in tempo reale: elimina qualsiasi frammento di profilo con valore di identità specificato come identità primaria. **L&#39;identità principale nel profilo verrà ora determinata in base alla priorità dello spazio dei nomi.**
* Data lake: elimina qualsiasi record con l&#39;identità specificata come identità primaria o secondaria.

Per maggiori informazioni, leggi l&#39;informativa](../../privacy-service/home.md) sul [servizio Privacy.

### Adobe Target

Adobe Target possono produrre targeting utente imprevisti per scenari di dispositivo condivisi quando si utilizzano Segmentazione perimetrali.