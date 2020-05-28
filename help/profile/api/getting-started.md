---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida per lo sviluppatore di API profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: 8449681a7fd0fc5dccf4837a1e8e512f1e2f2601
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---


# Guida per lo sviluppatore di API profilo cliente in tempo reale

Il profilo cliente in tempo reale ti permette di vedere una visione olistica di ogni singolo cliente all&#39;interno di Adobe Experience Platform. Il profilo consente di consolidare diversi dati dei clienti da più canali, come online, offline, CRM e dati di terze parti, in una visualizzazione unificata che offre un account con marca temporale utilizzabile per ogni interazione con il cliente.

## Introduzione {#getting-started}

Utilizzando l&#39;API Profilo cliente in tempo reale, potete eseguire operazioni CRUD di base rispetto alle risorse Profilo, come la configurazione di attributi calcolati, l&#39;accesso alle entità, l&#39;esportazione di dati Profilo ed eliminazione di set di dati o batch non necessari.

L’utilizzo di questa guida per gli sviluppatori richiede una buona conoscenza dei vari servizi Adobe Experience Platform coinvolti nell’utilizzo dei dati di profilo. Prima di iniziare a lavorare con l&#39;API del profilo cliente in tempo reale, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../home.md)cliente in tempo reale: Fornisce un profilo cliente unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Ottieni una visione migliore del tuo cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi.
* [Servizio](../../segmentation/home.md)di segmentazione della piattaforma Adobe Experience: Consente di creare segmenti di pubblico dai dati del profilo cliente in tempo reale.
* [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.
* [Sandbox](../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che dividono una singola istanza della piattaforma in ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.

Le sezioni seguenti forniscono informazioni aggiuntive che sarà necessario conoscere per effettuare correttamente le chiamate agli endpoint API di profilo.

### Lettura di chiamate API di esempio

La documentazione API del profilo cliente in tempo reale fornisce esempi di chiamate API per dimostrare come formattare correttamente le richieste. Questi includono percorsi, intestazioni richieste e payload di richieste formattati correttamente. Viene inoltre fornito un JSON di esempio restituito nelle risposte API. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione [come leggere le chiamate](../../landing/troubleshooting.md#how-do-i-format-an-api-request) API di esempio nella guida alla risoluzione dei problemi della piattaforma Experience.

### Intestazioni necessarie

La documentazione API richiede inoltre di aver completato l&#39;esercitazione [di](../../tutorials/authentication.md) autenticazione per effettuare correttamente le chiamate agli endpoint piattaforma. Completando l&#39;esercitazione sull&#39;autenticazione, vengono forniti i valori per ciascuna delle intestazioni richieste nelle chiamate API di Experience Platform, come illustrato di seguito:

* Autorizzazione: Portatore `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Tutte le risorse in Experience Platform sono isolate in sandbox virtuali specifiche. Le richieste alle API della piattaforma richiedono un&#39;intestazione che specifica il nome della sandbox in cui si svolgerà l&#39;operazione:

* x-sandbox-name: `{SANDBOX_NAME}`

Per ulteriori informazioni sulle sandbox in Piattaforma, consultate la documentazione [sulla panoramica della](../../sandboxes/home.md)sandbox.

Tutte le richieste con un payload nel corpo della richiesta (come le chiamate POST, PUT e PATCH) devono includere un&#39; `Content-Type` intestazione. I valori accettati specifici per ogni chiamata vengono forniti nei parametri delle chiamate.

## (Alfa) Attributi calcolati

>[!IMPORTANT]
>La funzionalità dell&#39;attributo calcolato è in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati consentono di calcolare automaticamente il valore dei campi in base ad altri valori, calcoli ed espressioni. Gli attributi calcolati operano a livello di profilo, il che significa che puoi aggregare i valori per tutti i record ed eventi.

Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo o in un evento. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie.

Potete creare, visualizzare, modificare ed eliminare gli attributi calcolati utilizzando i `config/computedAttributes` punti finali. Per informazioni sull&#39;utilizzo di questi endpoint, consultare la guida secondaria degli attributi [calcolati](computed-attributes.md).

## Proiezioni Edge

Adobe Experience Platform consente la personalizzazione in tempo reale delle esperienze dei clienti, rendendo i dati facilmente accessibili su server situati strategicamente denominati &quot;edge&quot;. L&#39;API del profilo cliente in tempo reale fornisce gli endpoint per l&#39;utilizzo dei bordi tramite componenti denominati &quot;proiezioni&quot;. Ciò include configurazioni di proiezione per determinare quali dati proiettare su ciascun bordo, nonché destinazioni di proiezione per definire dove indirizzare una proiezione.

Per informazioni dettagliate sull’utilizzo delle proiezioni dei bordi, visitare la [guida](edge-projections.md)secondaria Proiezioni dei bordi.

## Entità

Tramite Adobe Experience Platform puoi accedere ai dati del profilo cliente in tempo reale utilizzando le RESTful API o l&#39;interfaccia utente. Per informazioni su come accedere alle entità, più comunemente note come &quot;profili&quot;, mediante l&#39;API, segui i passaggi descritti nella guida secondaria [delle entità](entities.md).

## Unisci criteri

Quando si uniscono dati da più origini in Experience Platform, i criteri di unione sono le regole utilizzate dalla Piattaforma per determinare in che modo i dati verranno classificati in ordine di priorità e quali dati verranno combinati per creare singoli profili cliente.

Utilizzando l&#39;API Profilo cliente in tempo reale, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API, consultare la guida secondaria [Criteri di unione](merge-policies.md).

Per una guida all&#39;utilizzo dei criteri di unione tramite l&#39;interfaccia utente della piattaforma, consultate la guida [utente](../ui/merge-policies.md)Unisci criteri.

## Processi del sistema di profili

I dati acquisiti in Piattaforma vengono memorizzati nel Data Lake e nell&#39;archivio dati del profilo cliente in tempo reale. Talvolta potrebbe essere necessario eliminare un set di dati o un batch dall&#39;archivio dei profili per rimuovere i dati che non sono più necessari o che sono stati aggiunti per errore. Ciò richiede l’utilizzo dell’API per creare un processo di sistema dei profili, noto come &quot;richiesta di eliminazione&quot;, che può anche essere, modificato, monitorato o eliminato se necessario.

Per informazioni su come gestire le richieste di eliminazione tramite gli `/system/jobs` endpoint nell’API Profilo cliente in tempo reale, segui i passaggi descritti nella guida secondaria [ai processi del sistema di](profile-system-jobs.md)profilo.

## Passaggi successivi

Per iniziare a effettuare chiamate tramite l’API Profilo cliente in tempo reale, seleziona una delle guide secondarie per scoprire come utilizzare endpoint specifici correlati al profilo. Per ulteriori informazioni sull’utilizzo dei dati di profilo nell’interfaccia utente della piattaforma, consulta la guida [utente Profilo cliente](../ui/user-guide.md)in tempo reale.