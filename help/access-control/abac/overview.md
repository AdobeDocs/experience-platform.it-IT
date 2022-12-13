---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;controllo accessi basato su attributi;
title: Panoramica sul controllo dell'accesso basato su attributi
description: Questo documento fornisce informazioni sul controllo degli accessi basato sugli attributi in Adobe Experience Platform
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 3%

---

# Panoramica sul controllo dell&#39;accesso basato su attributi

Il controllo dell&#39;accesso basato su attributi è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l&#39;accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono gli attributi per gestire le autorizzazioni di accesso degli utenti.

Questa funzionalità ti consente di etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. In parallelo, gli amministratori possono utilizzare l’interfaccia utente e l’interfaccia di amministrazione dei ruoli per definire i criteri di accesso ai campi dello schema XDM e gestire meglio l’accesso dato a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo degli accessi basato sugli attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

>[!IMPORTANT]
>
>Il controllo dell’accesso basato su attributi non va confuso con le funzionalità di governance dei dati di Experience Platform, che ti consentono di utilizzare etichette e criteri per controllare il modo in cui i dati vengono utilizzati in Platform, anziché a quali utenti dell’organizzazione possono accedervi. Consulta la sezione [panoramica sulla governance dei dati](../../data-governance/home.md) per ulteriori informazioni.

Grazie al controllo degli accessi basato sugli attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti a dati personali sensibili (SPD), informazioni personali (PII) e tipi personalizzati di dati in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente con accesso solo a campi e dati specifici corrispondenti a tali campi.

## Terminologia di controllo degli accessi basata su attributi

Il controllo dell&#39;accesso basato su attributi include i seguenti componenti:

| Terminologia | Definizione |
| --- | --- |
| Attributi | Gli attributi sono gli identificatori che indicano la correlazione tra un utente e le risorse di Platform a cui hanno accesso. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono gli attributi per gestire le autorizzazioni di accesso degli utenti. |
| Etichette | Le etichette consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti in Platform o non appena i dati diventano disponibili per l’utilizzo in Platform. |
| Autorizzazioni | Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare le funzioni di Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione dei set di dati. |
| Set di autorizzazioni | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| Criteri | Le politiche sono dichiarazioni che riuniscono gli attributi per stabilire azioni ammissibili e non ammissibili. I criteri possono essere locali o globali e possono sostituire altri criteri. |
| Risorsa | Una risorsa è la risorsa o l’oggetto a cui un soggetto può o non può accedere. Le risorse possono essere segmenti o campi di schema. |
| Ruoli | I ruoli sono modi per classificare i tipi di utenti che interagiscono con l’istanza Platform e costituiscono blocchi costitutivi dei criteri di controllo degli accessi. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente viene raggruppato attraverso responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario. |
| Oggetto | Un oggetto è l’utente che richiede l’accesso a una risorsa per eseguire un’azione. |
| Gruppi utente | I gruppi di utenti sono più utenti che sono stati raggruppati insieme e hanno l&#39;accesso per eseguire le stesse funzioni. |

## Autorizzazioni

>[!IMPORTANT]
>
>Una volta che l’organizzazione è abilitata per il controllo degli accessi basato su attributi, puoi iniziare a utilizzare Autorizzazioni su Adobe Experience Cloud, invece dei profili di prodotto in Adobe Admin Console, per gestire le autorizzazioni per utenti, funzionalità, etichette e altre risorse dell’organizzazione.

Le autorizzazioni sono l’area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri di accesso per gestire le autorizzazioni di accesso per funzioni e oggetti all’interno di un’applicazione di prodotto.

Mediante le Autorizzazioni di , , puoi creare e gestire i ruoli, nonché assegnare le autorizzazioni per le risorse desiderate per tali ruoli. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico. Per ulteriori informazioni, consulta la sezione [Guida alle autorizzazioni](ui/browse.md).

## API di controllo dell&#39;accesso basato su attributi

L’API per il controllo degli accessi basata sugli attributi consente di gestire in modo programmatico ruoli, criteri e prodotti all’interno di Platform utilizzando le API. Per ulteriori informazioni, consulta la guida su [utilizzo dell’API per gestire le configurazioni di controllo accessi basate su attributi](api/overview.md).

## Controllo degli accessi basato su attributi in Adobe Experience Platform

Le sezioni seguenti forniscono informazioni su come il controllo degli accessi basato sugli attributi viene integrato in altri componenti di Platform:

### Controllo degli accessi

Utilizzo della piattaforma [Adobe Admin Console](https://adminconsole.adobe.com) profili di prodotto per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a una varietà di funzionalità di Platform, tra cui la modellazione dei dati, la gestione dei profili e l’amministrazione di sandbox. Una volta che l’organizzazione è abilitata per il controllo degli accessi basato su attributi, puoi iniziare a utilizzare Autorizzazioni su Adobe Experience Cloud, invece dei profili di prodotto in Adobe Admin Console, per gestire le autorizzazioni per utenti, funzionalità, etichette e altre risorse dell’organizzazione.

La disponibilità per il controllo degli accessi basato sugli attributi è limitata ai clienti che acquistano scudi sanitari e/o privacy. Le funzioni di questa funzionalità includono:

* Interfaccia delle autorizzazioni: Fornisce un&#39;interfaccia per definire ruoli utente, autorizzazioni e criteri per il controllo degli accessi basato su attributi.

* Etichettatura: Aggiungi, modifica, rimuovi le etichette ai ruoli utente, ai campi dello schema, ai segmenti e ad altri oggetti supportati al fine di sfruttare i criteri di controllo degli accessi.

I flussi di lavoro di amministrazione per tutte le applicazioni basate su Experience Platform, dall’Admin Console alla nuova interfaccia Autorizzazioni, sono in corso di commutazione.

>[!IMPORTANT]
>
>Quando l’organizzazione è abilitata, i profili di prodotto vengono migrati automaticamente nell’interfaccia Autorizzazioni . I profili di prodotto in Admin Console rimarranno invariati al momento. Per favore **non** modifica i profili di prodotto dopo che l’organizzazione è stata abilitata.

Per ulteriori informazioni sul controllo degli accessi, consulta la sezione [panoramica sul controllo degli accessi](../home.md).

### Destinazioni {#destinations}

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

In qualità di amministratore, puoi utilizzare funzionalità di controllo accessi basate su attributi per:

* Configura l’accesso utente per visualizzare segmenti specifici nel processo di attivazione in base a ruolo, autorizzazioni ed etichette;
   * Nel processo di attivazione, potrebbe essere richiesto agli utenti di selezionare i segmenti che desiderano attivare in una destinazione. In qualità di amministratore, puoi assegnare agli utenti della tua organizzazione il provisioning per visualizzare solo i segmenti etichettati con etichette a cui gli utenti hanno accesso e i segmenti a cui non sono associate etichette.
* Configura l’accesso utente per visualizzare campi specifici nel processo di attivazione in base a ruolo, autorizzazioni ed etichette;
   * Nel processo di attivazione, potrebbe essere richiesto agli utenti di selezionare i campi che desiderano attivare in una destinazione. In qualità di amministratore, puoi assegnare agli utenti dell’organizzazione il provisioning per visualizzare solo i campi etichettati con le etichette a cui gli utenti hanno accesso e i campi che non contengono etichette.

>[!IMPORTANT]
>
>In sintesi, tieni presente le seguenti implicazioni quando lavori con le destinazioni e con il controllo degli accessi basato sugli attributi:
>
>* Puoi attivare solo i segmenti a cui hai le autorizzazioni di accesso e visualizzazione nel [visualizzazione di ricerca dei segmenti](/help/segmentation/ui/overview.md#browse) e [seleziona il passaggio del segmento](/help/destinations/ui/activate-batch-profile-destinations.md#select-segments) del flusso di lavoro di attivazione.
>* In [fase di mappatura del flusso di lavoro di attivazione](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), puoi visualizzare e selezionare per l’attivazione solo i campi a cui disponi dell’autorizzazione di accesso.
>* Quando desideri attivare ulteriori segmenti in una destinazione esistente in cui non hai accesso a tutti i campi mappati per l’esportazione, il flusso di lavoro di attivazione verrà bloccato automaticamente.


Per ulteriori informazioni su [!DNL Destinations], fare riferimento alla [[!DNL Destinations] panoramica](../../destinations/home.md).

### Servizio Identity

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento delle identità tra dispositivi e sistemi, per offrire in tempo reale esperienze digitali personali di impatto.

Come parte del controllo dell&#39;accesso basato sugli attributi, il `view-identity-graph` Le autorizzazioni ti consentono di determinare quali utenti della tua organizzazione possono accedere al grafico delle identità tramite l’interfaccia utente o le API. Per ulteriori informazioni, consulta la guida su [utilizzo del visualizzatore grafico delle identità](../../identity-service/ui/identity-graph-viewer.md).

Per ulteriori informazioni su [!DNL Identity Service], fare riferimento alla [[!DNL Identity Service] panoramica](../../identity-service/home.md).

### Real-time Customer Profile

Platform ti consente di distribuire esperienze coordinate, coerenti e rilevanti per i clienti, indipendentemente da dove e quando interagiscono con il tuo marchio. Con Profilo cliente in tempo reale puoi vedere una visualizzazione olistica di ogni singolo cliente che combina dati provenienti da più canali, inclusi dati online, offline, CRM e di terze parti. Il profilo ti consente di consolidare i dati dei tuoi clienti diversi in una visualizzazione unificata che offre un account utilizzabile e con marca temporale per ogni interazione con il cliente.

In qualità di amministratore, puoi utilizzare funzionalità di controllo accessi basate su attributi per:

* Configurare l’accesso dell’utente ad attributi di profilo specifici in base a ruoli, autorizzazioni ed etichette;
   * In qualità di amministratore, puoi assegnare agli utenti della tua organizzazione il provisioning per visualizzare solo gli attributi di profilo etichettati con etichette a cui gli utenti hanno accesso e gli attributi di profilo che non contengono alcuna etichetta;
   * In qualità di amministratore, puoi assegnare agli utenti della tua organizzazione il provisioning per visualizzare solo gli attributi di profilo etichettati con le etichette a cui gli utenti hanno accesso durante la creazione dei segmenti;
* Configura l’accesso dell’utente all’anteprima dei dati etichettando campi di dati specifici utilizzati nello schema XDM del modello dati.

Per ulteriori informazioni su Profilo, consulta la sezione [Panoramica del profilo](../../profile/home.md).

### Servizio di segmentazione

[!DNL Segmentation Service] definisce un particolare sottoinsieme di profili descrivendo i criteri che distinguono un gruppo di persone commerciabili all’interno della base cliente. I segmenti possono essere basati su dati di record (come informazioni demografiche) o su eventi di serie temporali che rappresentano le interazioni dei clienti con il tuo marchio.

In qualità di amministratore, puoi utilizzare funzionalità di controllo accessi basate su attributi per:

* Configura l’accesso utente per visualizzare e gestire segmenti specifici, in base a ruoli, autorizzazioni ed etichette;
   * In qualità di amministratore, puoi assegnare agli utenti della tua organizzazione il provisioning per visualizzare solo i segmenti etichettati con etichette a cui gli utenti hanno accesso e i segmenti a cui non sono associate etichette quando utilizzi l’interfaccia utente Segmentazione.

Per ulteriori informazioni su [!DNL Segmentation Service], fare riferimento alla [[!DNL Segmentation Service] panoramica](../../segmentation/home.md).

### XDM

Experience Data Model (XDM) è una specifica open-source progettata per migliorare la potenza delle esperienze digitali. Fornisce strutture e definizioni comuni per qualsiasi applicazione per comunicare con i servizi su Platform. Aderendo agli standard XDM, tutti i dati sulla customer experience possono essere incorporati in una rappresentazione comune per fornire informazioni in modo più rapido e integrato. Puoi ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti e utilizzare gli attributi del cliente a scopo di personalizzazione.

Con il controllo dell&#39;accesso basato su attributi, puoi:

* [Applicare etichette di utilizzo dati a gruppi di campi e classi](../../xdm/tutorials/labels.md). Ciò consente a più schemi con gli stessi gruppi di campi o classi, di assegnare ai campi i tag con gli stessi attributi, a seconda delle configurazioni a livello di gruppo di campi o di classe;
* Configura l&#39;accesso dell&#39;utente a specifici campi dello schema XDM in base ai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

Per ulteriori informazioni su XDM, consulta la sezione [Panoramica di XDM](../../xdm/home.md).