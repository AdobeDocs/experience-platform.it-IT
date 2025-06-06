---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;
title: Panoramica sul controllo degli accessi basato su attributi
description: Questo documento fornisce informazioni sul controllo degli accessi basato su attributi in Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 13%

---

# Panoramica sul controllo degli accessi basato su attributi {#attribute-based-access-control-overview}

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti.

Utilizza questa funzionalità per etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. Parallelamente, gli amministratori possono utilizzare l’interfaccia di amministrazione di utenti e ruoli per definire i criteri di accesso relativi ai campi dello schema XDM e gestire in modo migliore l’accesso concesso a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo dell’accesso basato su attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

>[!IMPORTANT]
>
>Il controllo dell’accesso basato sugli attributi non deve essere confuso con le funzionalità di governance dei dati di Experience Platform, che consentono di utilizzare etichette e criteri per controllare il modo in cui i dati vengono utilizzati in Experience Platform anziché gli utenti dell’organizzazione che vi hanno accesso. Per ulteriori informazioni, consulta la [panoramica sulla governance dei dati](../../data-governance/home.md).

Tramite il controllo dell’accesso basato su attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti ai dati personali sensibili (SPD), alle informazioni personali (PII) e ai tipi di dati personalizzati in tutti i flussi di lavoro e le risorse di Experience Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici che corrispondono a tali campi.

Il video seguente ha lo scopo di illustrare il controllo degli accessi basato su attributi e illustra come configurare ruoli, risorse e criteri.

>[!VIDEO](https://video.tv.adobe.com/v/3451846?learn=on&captions=ita)

## Terminologia per il controllo degli accessi basato su attributi

Il controllo dell’accesso basato su attributi include i seguenti componenti:

| Terminologia | Definizione |
| --- | --- |
| Attributi | Gli attributi sono gli identificatori che indicano la correlazione tra un utente e le risorse Experience Platform a cui ha accesso. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti. |
| Etichette | Le etichette consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Le best practice incoraggiano i dati di etichettatura non appena vengono acquisiti in Experience Platform o non appena i dati diventano disponibili per l’utilizzo in Experience Platform. |
| Autorizzazioni | Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare le funzioni di Experience Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione di set di dati. |
| Set di autorizzazioni | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può applicare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, invece di assegnare singole autorizzazioni. In questo modo è possibile creare ruoli personalizzati da un ruolo predefinito contenente un gruppo di autorizzazioni. |
| Criteri | I criteri sono dichiarazioni che riuniscono alcuni attributi al fine di definire azioni ammissibili e non ammissibili. I criteri possono essere locali o globali e possono ignorare altri criteri. |
| Risorsa | Una risorsa è la risorsa o l&#39;oggetto a cui un soggetto può o non può accedere. Le risorse possono essere segmenti o campi schema. |
| Ruoli | I ruoli sono modi per categorizzare i tipi di utenti che interagiscono con l’istanza Experience Platform e sono blocchi predefiniti delle policy di controllo degli accessi. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente è raggruppato in base a responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario. |
| Argomento | Un oggetto è l’utente che richiede l’accesso a una risorsa per eseguire un’azione. |
| Gruppi di utenti | I gruppi di utenti sono utenti multipli che sono stati raggruppati e hanno l’accesso per eseguire le stesse funzioni. |

## Autorizzazioni

>[!IMPORTANT]
>
>Una volta che l’organizzazione è abilitata per il controllo degli accessi basato su attributi, puoi iniziare a utilizzare Autorizzazioni su Adobe Experience Cloud, anziché Ruoli in Adobe Admin Console, per gestire le autorizzazioni per gli utenti, le funzionalità, le etichette e altre risorse dell’organizzazione.

Autorizzazioni è l’area di Experience Cloud in cui gli amministratori possono definire i ruoli utente e i criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto.

Tramite le Autorizzazioni, puoi creare e gestire i ruoli, nonché assegnare le autorizzazioni per le risorse desiderate per tali ruoli. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico. Per ulteriori informazioni, vedere la [Guida alle autorizzazioni](ui/browse.md).

## API di controllo dell’accesso basata su attributi

L’API di controllo degli accessi basata su attributi consente di gestire in modo programmatico ruoli, criteri e prodotti all’interno di Experience Platform utilizzando le API. Per ulteriori informazioni, consulta la guida su [utilizzo dell&#39;API per gestire le configurazioni di controllo dell&#39;accesso basate su attributi](api/overview.md).

## Controllo degli accessi basato su attributi in Adobe Experience Platform

Le sezioni seguenti forniscono informazioni su come il controllo degli accessi basato su attributi viene integrato con altri componenti di Experience Platform:

### Controllo degli accessi

Experience Platform sfrutta i ruoli [Adobe Admin Console](https://adminconsole.adobe.com) per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a diverse funzionalità di Experience Platform, tra cui la modellazione di dati, la gestione dei profili e l’amministrazione della sandbox. Una volta che l’organizzazione è abilitata per il controllo degli accessi basato su attributi, puoi iniziare a utilizzare Autorizzazioni su Adobe Experience Cloud, anziché Ruoli in Adobe Admin Console, per gestire le autorizzazioni per gli utenti, le funzionalità, le etichette e altre risorse dell’organizzazione.

La disponibilità del controllo degli accessi basato su attributi per i clienti che acquistano prodotti sanitari e/o scudi per la privacy è limitata. Le caratteristiche di questa funzionalità includono:

* Interfaccia autorizzazioni: fornisce un’interfaccia che consente di definire ruoli utente, autorizzazioni e criteri per il controllo degli accessi basato su attributi.

* Etichette: aggiungi, modifica e rimuovi etichette ai ruoli utente, ai campi dello schema, ai segmenti e ad altri oggetti supportati per sfruttare i criteri di controllo di accesso. **Nota:** Qualsiasi segmento che utilizza un attributo con etichetta deve essere etichettato allo stesso modo se desideri che ad esso vengano applicate le stesse restrizioni di accesso.

I flussi di lavoro di amministrazione per tutte le applicazioni basate su Experience Platform da Admin Console alla nuova interfaccia Autorizzazioni sono in fase di commutazione.

>[!IMPORTANT]
>
>Quando l’organizzazione è abilitata, i ruoli vengono migrati automaticamente all’interfaccia Autorizzazioni. I ruoli in Admin Console rimarranno invariati per il momento. **non** modificare i ruoli dopo l&#39;abilitazione dell&#39;organizzazione.

Per ulteriori informazioni sul controllo degli accessi, vedere la [panoramica sul controllo degli accessi](../home.md).

### Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l&#39;attivazione diretta dei dati da Experience Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e molti altri casi d’uso.

In qualità di amministratore, puoi utilizzare funzionalità di controllo dell’accesso basate su attributi per:

* Configurare l&#39;accesso utente per visualizzare segmenti specifici nel processo di attivazione, in base a ruolo, autorizzazioni ed etichette;
   * Nel processo di attivazione, gli utenti potrebbero dover selezionare i segmenti da attivare su una destinazione. In qualità di amministratore, puoi assegnare ruoli agli utenti dell’organizzazione per visualizzare solo i segmenti etichettati con etichette a cui gli utenti hanno accesso e i segmenti che non contengono etichette.
* Configurare l&#39;accesso utente per visualizzare campi specifici nel processo di attivazione, in base a ruolo, autorizzazioni ed etichette;
   * Nel processo di attivazione, gli utenti potrebbero dover selezionare i campi da attivare su una destinazione. In qualità di amministratore, è possibile assegnare ruoli agli utenti dell&#39;organizzazione per visualizzare solo i campi con etichette a cui gli utenti hanno accesso e i campi che non contengono etichette.

>[!IMPORTANT]
>
>In sintesi, considera le seguenti implicazioni quando utilizzi le destinazioni e il controllo degli accessi basato su attributi:
>
>* Puoi attivare solo i tipi di pubblico per i quali disponi dell&#39;autorizzazione di accesso e visualizzazione in [Audience Portal](/help/segmentation/ui/audience-portal.md#browse) e [seleziona il passaggio del segmento](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) del flusso di lavoro di attivazione.
>* Nel [passaggio di mappatura del flusso di lavoro di attivazione](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), puoi visualizzare e selezionare per l&#39;attivazione solo i campi per i quali disponi dell&#39;autorizzazione di accesso.
>* Quando desideri attivare altri segmenti in una destinazione esistente in cui non hai accesso a tutti i campi mappati per l’esportazione, il flusso di lavoro di attivazione viene bloccato automaticamente.

Per ulteriori informazioni su [!DNL Destinations], consulta la [[!DNL Destinations] panoramica](../../destinations/home.md).

### Identity Service

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una migliore visualizzazione dei clienti e del loro comportamento collegando le identità tra dispositivi e sistemi, consentendo di fornire esperienze digitali personali e di impatto in tempo reale.

Come parte del controllo degli accessi basato su attributi, l&#39;autorizzazione `view-identity-graph` consente di determinare quali utenti dell&#39;organizzazione possono accedere al grafo delle identità tramite l&#39;interfaccia utente o le API. Per ulteriori informazioni, consulta la guida su [utilizzo del visualizzatore del grafico delle identità](../../identity-service/features/identity-graph-viewer.md).

Per ulteriori informazioni su [!DNL Identity Service], consulta la [[!DNL Identity Service] panoramica](../../identity-service/home.md).

### Profilo cliente in tempo reale

Experience Platform ti consente di promuovere esperienze coordinate, coerenti e rilevanti per i tuoi clienti, indipendentemente da dove o quando interagiscono con il tuo marchio. Con il Profilo cliente in tempo reale puoi avere una visione completa di ogni singolo cliente combinando dati provenienti da più canali, inclusi online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i diversi dati dei clienti in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

In qualità di amministratore, puoi utilizzare funzionalità di controllo dell’accesso basate su attributi per:

* Configurare l’accesso degli utenti a specifici attributi di profilo in base a ruoli, autorizzazioni ed etichette;
   * In qualità di amministratore, puoi assegnare agli utenti della tua organizzazione il provisioning necessario per visualizzare solo gli attributi del profilo con etichette a cui gli utenti hanno accesso e gli attributi del profilo che non contengono alcuna etichetta;
   * In qualità di amministratore, puoi assegnare agli utenti della tua organizzazione il provisioning necessario per visualizzare solo gli attributi del profilo etichettati con etichette a cui gli utenti hanno accesso durante la creazione di segmenti;
* Configura l’accesso utente all’anteprima dei dati etichettando campi di dati specifici utilizzati nello schema XDM del modello di dati.

Per ulteriori informazioni sul profilo, consulta la [Panoramica profilo](../../profile/home.md).

### Servizio di segmentazione

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabile all’interno della tua clientela. I segmenti possono essere basati su dati dei record (ad esempio informazioni demografiche) o su eventi della serie temporale che rappresentano le interazioni della clientela con il tuo marchio.

In qualità di amministratore, puoi utilizzare funzionalità di controllo dell’accesso basate su attributi per:

* Configurare l’accesso degli utenti per visualizzare e gestire segmenti specifici in base a ruoli, autorizzazioni ed etichette;
   * In qualità di amministratore, puoi assegnare ruoli agli utenti dell’organizzazione per visualizzare solo i segmenti etichettati con etichette a cui gli utenti hanno accesso e i segmenti che non contengono etichette quando utilizzi l’interfaccia utente Segmentazione.

Per ulteriori informazioni su [!DNL Segmentation Service], consulta la [[!DNL Segmentation Service] panoramica](../../segmentation/home.md).

### XDM

Experience Data Model (XDM) è una specifica open-source progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Experience Platform. Aderendo agli standard XDM, tutti i dati sull’esperienza cliente possono essere incorporati in una rappresentazione comune per fornire approfondimenti in modo più rapido e integrato. Puoi ottenere approfondimenti importanti dalle azioni della clientela, definire i tipi di pubblico della clientela attraverso i segmenti e utilizzare gli attributi della clientela a scopo di personalizzazione.

Il controllo degli accessi basato su attributi consente di:

* [Applica etichette di utilizzo dati a gruppi di campi e classi](../../xdm/tutorials/labels.md). Ciò consente a più schemi con gli stessi gruppi di campi o classi di avere campi contrassegnati con gli stessi attributi, a seconda delle configurazioni a livello di gruppo di campi o di classe;
* Configura l’accesso degli utenti a campi di schema XDM specifici in base ai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

Per ulteriori informazioni su XDM, consulta la [panoramica XDM](../../xdm/home.md).