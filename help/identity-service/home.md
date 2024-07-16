---
keywords: Experience Platform;home;argomenti popolari;identità;identità;grafi XDM;servizio identità;servizio identità
solution: Experience Platform
title: Panoramica del servizio Identity
description: Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore del cliente e del suo comportamento, collegando le identità tra dispositivi e sistemi diversi e consentendo di fornire esperienze digitali personali e di impatto in tempo reale.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 16e49628df73d5ce97ef890dbc0a6f2c8e7de346
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 2%

---

# Adobe Experience Platform Identity Service

Per offrire esperienze digitali rilevanti, devi disporre di una rappresentazione completa e accurata delle entità del mondo reale che compongono la tua base di clienti.

Le organizzazioni e le aziende si trovano oggi ad affrontare un grande volume di set di dati diversi: i singoli clienti sono rappresentati da una varietà di identificatori diversi. Il cliente può essere collegato a diversi browser web (Safari, Google Chrome), dispositivi hardware (telefoni, notebook) e altri identificatori di persona (ID CRM, account e-mail). Questo crea una visione disgiunta del cliente.

Il servizio Adobe Experience Platform Identity e le relative funzionalità consentono di risolvere questi problemi:

* Genera un **grafo di identità** che collega identità diverse, fornendo in tal modo una rappresentazione visiva di come un cliente interagisce con il tuo marchio su canali diversi.
* Crea un grafico per Real-Time Customer Profile, che viene quindi utilizzato per creare una visualizzazione completa del cliente mediante l’unione di attributi e comportamenti.
* Eseguire la convalida e il debug utilizzando i vari strumenti.

Questo documento fornisce una panoramica del servizio Identity e spiega come utilizzarne le funzionalità nel contesto di Experience Platform.

## Terminologia {#terminology}

Prima di immergerti nei dettagli del servizio Identity, leggi la tabella seguente per un riepilogo dei termini chiave:

| Termine | Definizione |
| --- | --- |
| Identità | Un’identità è un dato univoco di un’entità. In genere si tratta di un oggetto reale, ad esempio una singola persona, un dispositivo hardware o un browser web (rappresentato da un cookie). Un&#39;identità completa è costituita da due elementi: uno spazio dei nomi **identity** e un **identity value**. |
| Spazio dei nomi identità | Uno spazio dei nomi dell’identità è il contesto di una determinata identità. Ad esempio, uno spazio dei nomi di `Email` potrebbe corrispondere al valore di identità: **julien<span>@acme.com**. Analogamente, uno spazio dei nomi di `Phone` potrebbe corrispondere al valore di identità: `555-555-1234`. Per ulteriori informazioni, leggere la [panoramica dello spazio dei nomi delle identità](./features/namespaces.md). |
| Valore identità | Un valore di identità è una stringa che rappresenta un’entità reale ed è categorizzata all’interno di Identity Service tramite uno spazio dei nomi. Ad esempio, il valore di identità (stringa) **julien<span>@acme.com** potrebbe essere classificato come uno spazio dei nomi `Email`. |
| Tipo di identità | Un tipo di identità è un componente di uno spazio dei nomi di identità. Il tipo di identità indica se i dati di identità sono collegati o meno in un grafico delle identità. |
| Collegamento | Un collegamento o un collegamento è un metodo per stabilire che due identità diverse rappresentano la stessa entità. Ad esempio, un collegamento tra &quot;`Email` = julien<span>@acme.com&quot; e &quot;`Phone` = 555-555-1234&quot; indica che entrambe le identità rappresentano la stessa entità. Ciò suggerisce che il cliente che ha interagito con il tuo marchio sia con l&#39;indirizzo e-mail di julien<span>@acme.com che con il numero di telefono di 555-555-1234 è lo stesso. |
| Identity Service | Identity Service è un servizio all’interno di Experience Platform che collega (o scollega) le identità per mantenere i grafici delle identità. |
| Grafico delle identità | Il grafo delle identità è una raccolta di identità che rappresentano un singolo cliente. Per ulteriori informazioni, leggere la guida in [utilizzo del visualizzatore del grafico delle identità](./features/identity-graph-viewer.md). |
| Profilo cliente in tempo reale | Real-Time Customer Profile è un servizio all’interno di Adobe Experience Platform che: <ul><li>Unisce i frammenti di profili per creare un profilo, in base a un grafico delle identità.</li><li>Segmenta i profili in modo che possano essere inviati alla destinazione per le attivazioni.</li></ul> |
| Profilo | Un profilo è una rappresentazione di un soggetto, un’organizzazione o un individuo. Un profilo è composto da quattro elementi: <ul><li>Attributi: gli attributi forniscono informazioni quali nome, età o genere.</li><li>Comportamento: i comportamenti forniscono informazioni sulle attività di un determinato profilo. Ad esempio, un comportamento di profilo può indicare se un determinato profilo è &quot;alla ricerca di sandali&quot; o &quot;in ordine di t-shirt&quot;.</li><li>Identità: per un profilo unito, fornisce informazioni su tutte le identità associate alla persona. Le identità possono essere classificate in tre categorie: Persona (CRMID, e-mail, telefono), dispositivo (IDFA, GAID) e cookie (ECID, AAID).</li><li>Appartenenze al pubblico: i gruppi a cui appartiene il profilo (utenti fedeli, utenti che vivono in California, ecc.)</li></ul> |

{style="table-layout:auto"}

## Cos’è il servizio Identity?

![Unione identità in Platform](./images/identity-service-stitching.png)

In un contesto Business-To-Customer (B2C), i clienti interagiscono con la tua azienda e stabiliscono una relazione con il tuo marchio. Un cliente tipico può essere attivo in qualsiasi numero di sistemi all’interno dell’infrastruttura dati della tua organizzazione. Qualsiasi cliente può essere attivo all’interno dei sistemi di e-commerce, fedeltà e help desk. Lo stesso cliente può anche utilizzare sia in modo anonimo che tramite mezzi autenticati su qualsiasi numero di dispositivi diversi.

Prendi in considerazione il seguente percorso di clienti:

* Julien ha creato un account sul tuo sito web di e-commerce e ha ordinato alcuni elementi in passato. Di solito Julien usa il suo portatile per fare acquisti e accedere al suo account con ogni tempo di utilizzo.
* Tuttavia, durante una delle sue visite al tuo sito, utilizza una tavoletta per cercare i sandali. Durante questa sessione, poiché ha utilizzato un dispositivo diverso, non effettua l’accesso né effettua un ordine.
* A questo punto, le attività di Julien sono rappresentate in due profili separati:
   * Il suo primo profilo è il suo ID di accesso e-commerce. Questo profilo viene utilizzato quando utilizza una combinazione di nome utente e password per autenticare la sessione sul sito di e-commerce. Questo profilo è identificato da un identificatore cross-device.
   * Il suo secondo profilo è il suo dispositivo tablet. Questo profilo è stato creato dopo che ha navigato nel tuo sito di e-commerce in modo anonimo utilizzando un tablet senza accedere al suo account. Questo profilo è identificato da un identificatore di cookie.
* Successivamente, Julien riprende la sessione con il tablet. Tuttavia, questa volta accede al suo account. Di conseguenza, il servizio Identity mette ora in relazione l’attività di Julien sul tablet con il suo ID di accesso all’e-commerce.
* In futuro, il contenuto mirato potrebbe riflettere il profilo completo di Julien, la cronologia degli acquisti e l&#39;attività di navigazione anonima.

>[!IMPORTANT]
>
>Puoi utilizzare il servizio Identity per collegare le identità e creare un’immagine completa del cliente, che altrimenti potrebbe essere dispersa nei diversi sistemi.

## Quali operazioni vengono eseguite dal servizio Identity?

Il servizio Identity fornisce le seguenti operazioni per raggiungere la sua missione:

* Crea spazi dei nomi personalizzati in base alle esigenze della tua organizzazione.
* Crea, aggiorna e visualizza i grafici delle identità.
* Elimina le identità in base ai set di dati.
* Elimina le identità per garantire la conformità alle normative.

## Collegamento delle identità tramite il servizio Identity

Quando lo spazio dei nomi dell’identità e i valori dell’identità corrispondono, viene stabilito un collegamento tra due identità.

Un tipico evento di accesso **invia due identità** in Experience Platform:

* L’identificatore della persona (ad esempio un ID del sistema di gestione delle relazioni con i clienti) che rappresenta un utente autenticato.
* L’identificatore del browser (ad esempio un ECID) che rappresenta il browser web.

Prendi in considerazione l&#39;esempio seguente:

* Accedi con la combinazione di nome utente e password a un sito Web di e-commerce utilizzando il tuo laptop. Questo evento ti qualifica come utente autenticato, pertanto il servizio Identity riconosce il tuo ID CRM.
* Anche l’utilizzo di un browser per accedere al sito web di e-commerce viene riconosciuto da Identity Service come evento. Questo evento è rappresentato in Identity Service tramite un ECID.
* Dietro le quinte, Identity Service elabora i due eventi come: `CRM_ID:ABC, ECID:123`.
   * ID CRM: ABC è lo spazio dei nomi e il valore che ti rappresenta, come utente autenticato.
   * ECID: 123 è lo spazio dei nomi e il valore che rappresenta l’utilizzo del browser web sul laptop.
* Quindi, se accedi con le stesse credenziali allo stesso sito web di e-commerce, ma utilizzi il browser web sul telefono invece del browser web sul laptop, viene registrato un nuovo ECID in Identity Service.
* Dietro le quinte, Identity Service elabora questo nuovo evento come `{CRM_ID:ABC, ECID:456}`, dove CRM_ID: ABC rappresenta l’ID cliente autenticato e ECID:456 rappresenta il browser Web sul dispositivo mobile.

Considerando gli scenari di cui sopra, il servizio Identity stabilisce un collegamento tra `{CRM_ID:ABC, ECID:123}` e `{CRM_ID:ABC, ECID:456}`. Questo determina un grafico delle identità in cui &quot;possiedi&quot; tre identità: una per l’identificatore della persona (ID del sistema di gestione delle relazioni con i clienti) e due per gli identificatori dei cookie (ECID).

Per ulteriori informazioni, consulta la guida su [come Identity Service collega le identità](./features/identity-linking-logic.md).

## Grafici delle identità

Un grafo di identità è una mappa di relazioni tra diversi spazi dei nomi di identità, che ti consente di visualizzare e comprendere meglio quali identità dei clienti sono unite tra loro e come. Per ulteriori informazioni, leggi l&#39;esercitazione su [utilizzo del visualizzatore del grafico delle identità](./features/identity-graph-viewer.md).

Il video seguente ha lo scopo di aiutarti a comprendere le identità e i grafici di identità.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Comprensione del ruolo del servizio Identity nell’infrastruttura Experience Platform

Il servizio Identity svolge un ruolo fondamentale all’interno di Experience Platform. Alcune di queste integrazioni chiave includono:

* [Schemi](../xdm/home.md): all&#39;interno di uno schema specifico, i campi dello schema contrassegnati come identità consentono la creazione di grafici delle identità.
* [Set di dati](../catalog/datasets/overview.md): quando un set di dati è abilitato per l&#39;acquisizione in Real-Time Customer Profile, i grafici delle identità vengono generati dal set di dati, dato che il set di dati contiene almeno due campi contrassegnati come identità.
* [Web SDK](../web-sdk/home.md): Web SDK invia eventi di esperienza a Adobe Experience Platform e Identity Service genera un grafico quando esistono due o più identità nell&#39;evento.
* [Profilo cliente in tempo reale](../profile/home.md): prima dell&#39;unione degli attributi e degli eventi per un determinato profilo, il profilo cliente in tempo reale può fare riferimento al grafico delle identità. Per ulteriori informazioni, consulta la guida su [informazioni sulla relazione tra Identity Service e Real-Time Customer Profile](./identity-and-profile.md).
* [Destinazioni](../destinations/home.md): le destinazioni possono inviare informazioni sul profilo ad altri sistemi in base a uno spazio dei nomi di identità, ad esempio e-mail con hash.
* [Corrispondenza segmento](../segmentation/ui/segment-match/overview.md): la corrispondenza del segmento corrisponde a due profili in due sandbox diverse che hanno lo stesso spazio dei nomi e lo stesso valore di identità.
* [Privacy Service](../privacy-service/home.md): se la richiesta di eliminazione include `identity`, è possibile eliminare da Identity Service la combinazione di spazio dei nomi e valore di identità specificata utilizzando la funzionalità di elaborazione delle richieste di privacy in Privacy Service.

