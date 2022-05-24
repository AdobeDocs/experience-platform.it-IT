---
keywords: Experience Platform;home;argomenti popolari;controllo accessi;controllo accessi basato su attributi;
title: Panoramica sul controllo dell'accesso basato su attributi
description: Questo documento fornisce informazioni sul controllo degli accessi basato sugli attributi in Adobe Experience Platform
hide: true
hidefromtoc: true
exl-id: 5495c55f-b808-40c1-8896-e03eace0ca4d
source-git-commit: 4ac69f614d878cd3c3b9f47e41dedbc6f09288ac
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 1%

---

# Panoramica sul controllo dell&#39;accesso basato su attributi

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile in una versione limitata. Questa funzionalità sarà disponibile per tutti i clienti Real-time Customer Data Platform una volta rilasciata.

Il controllo dell&#39;accesso basato su attributi consente agli amministratori di controllare l&#39;accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere un valore esistente, ad esempio la geolocalizzazione o il reparto di una persona. Gli attributi possono anche essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema.

Questa funzionalità ti consente di etichettare i campi dello schema Experience Data Model (XDM) con etichette che definiscono gli ambiti di utilizzo organizzativi o dei dati. In parallelo, gli amministratori possono utilizzare l’interfaccia utente e l’interfaccia di amministrazione dei ruoli per definire i criteri di accesso ai campi dello schema XDM e gestire meglio l’accesso dato a utenti o gruppi di utenti (utenti interni, esterni o di terze parti). Inoltre, il controllo degli accessi basato sugli attributi consente agli amministratori di gestire l’accesso a segmenti specifici.

Grazie al controllo degli accessi basato sugli attributi, gli amministratori dell’organizzazione possono controllare l’accesso degli utenti ai dati personali sensibili (SPD) e alle informazioni personali (PII) in tutti i flussi di lavoro e le risorse di Platform. Gli amministratori possono definire ruoli utente specifici con accesso solo a campi specifici e solo a dati specifici corrispondenti a tali campi.

## Terminologia di controllo degli accessi basata su attributi

Il controllo dell&#39;accesso basato su attributi include i seguenti componenti:

| Terminologia | Definizione |
| --- | --- |
| Attributi | Gli attributi sono gli identificatori che indicano la correlazione tra un utente e le risorse di Platform a cui hanno accesso. Gli attributi possono essere un valore esistente, ad esempio la geolocalizzazione o il reparto di una persona. Gli attributi possono anche essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. |
| Etichette | Le etichette consentono di classificare set di dati e campi in base ai criteri di utilizzo applicati a tali dati. Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti in Platform o non appena i dati diventano disponibili per l’utilizzo in Platform. |
| Autorizzazioni | Le autorizzazioni includono la possibilità di visualizzare e/o utilizzare le funzioni di Platform, ad esempio la creazione di sandbox, la definizione di schemi e la gestione dei set di dati. |
| Set di autorizzazioni | I set di autorizzazioni rappresentano un gruppo di autorizzazioni che un amministratore può assegnare a un ruolo. Un amministratore può assegnare set di autorizzazioni a un ruolo, anziché assegnare singole autorizzazioni. Ciò ti consente di creare ruoli personalizzati da un ruolo predefinito che contiene un gruppo di autorizzazioni. |
| Criteri | Le politiche sono dichiarazioni che riuniscono gli attributi per stabilire azioni ammissibili e non ammissibili. I criteri possono essere locali o globali e possono sostituire altri criteri. |
| Risorsa | Una risorsa è la risorsa o l’oggetto a cui un soggetto può o non può accedere. Le risorse possono essere file, applicazioni, server o anche API. |
| Ruoli | I ruoli definiscono l’accesso che un amministratore, uno specialista o un utente finale ha alle risorse dell’organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente viene raggruppato attraverso responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario. |
| Oggetto | Un oggetto è l’utente che richiede l’accesso a una risorsa per eseguire un’azione. |
| Gruppi utente | I gruppi di utenti sono più utenti che sono stati raggruppati insieme e hanno l&#39;accesso per eseguire le stesse funzioni. |

## Autorizzazioni

>[!IMPORTANT]
>
>Una volta che l’organizzazione è abilitata per il controllo degli accessi basato su attributi, puoi iniziare a utilizzare Autorizzazioni su Adobe Experience Cloud, invece dei profili di prodotto in Adobe Admin Console, per gestire le autorizzazioni per utenti, funzionalità, etichette e altre risorse dell’organizzazione.

Le autorizzazioni sono l’area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri di accesso per gestire le autorizzazioni di accesso per funzioni, funzionalità e oggetti all’interno di un’applicazione di prodotto. Tramite le Autorizzazioni puoi creare e gestire i ruoli e assegnare le autorizzazioni di risorse desiderate per questi ruoli. Le autorizzazioni ti consentono inoltre di gestire le etichette, le sandbox e gli utenti associati a un ruolo specifico. Per ulteriori informazioni, consulta la guida alle autorizzazioni .

## API di controllo dell&#39;accesso basato su attributi

L’API per il controllo degli accessi basata sugli attributi consente di gestire in modo programmatico ruoli, criteri e prodotti all’interno di Platform utilizzando le API.

## Controllo degli accessi basato su attributi in Adobe Experience Platform

Le sezioni seguenti forniscono informazioni su come il controllo degli accessi basato sugli attributi viene integrato in altri componenti di Platform:

### Controllo degli accessi

Utilizzo della piattaforma [Adobe Admin Console](https://adminconsole.adobe.com) profili di prodotto per collegare gli utenti con autorizzazioni e sandbox. Le autorizzazioni controllano l’accesso a una varietà di funzionalità di Platform, tra cui la modellazione dei dati, la gestione dei profili e l’amministrazione di sandbox. Una volta che l’organizzazione è abilitata per il controllo degli accessi basato su attributi, puoi iniziare a utilizzare Autorizzazioni su Adobe Experience Cloud, invece dei profili di prodotto in Adobe Admin Console, per gestire le autorizzazioni per utenti, funzionalità, etichette e altre risorse dell’organizzazione.

Per ulteriori informazioni sul controllo degli accessi, consulta la sezione [panoramica sul controllo degli accessi](../home.md).

### Destinazioni

[!DNL Destinations] sono integrazioni predefinite con piattaforme di destinazione che consentono l’attivazione senza soluzione di continuità dei dati da Platform. Puoi utilizzare le destinazioni per attivare i dati noti e sconosciuti per le campagne di marketing cross-channel, le campagne e-mail, la pubblicità mirata e molti altri casi d’uso.

In qualità di amministratore, puoi utilizzare funzionalità di controllo accessi basate su attributi per:

* Configura l’accesso utente per visualizzare segmenti specifici nel processo di attivazione in base a ruolo, autorizzazioni ed etichette;
   * Nel processo di attivazione, potrebbe essere richiesto agli utenti di selezionare i segmenti che desiderano attivare in una destinazione. In qualità di amministratore, puoi assegnare agli utenti della tua organizzazione il provisioning per visualizzare solo i segmenti etichettati con etichette a cui gli utenti hanno accesso e i segmenti a cui non sono associate etichette.
* Configura l’accesso utente per visualizzare campi specifici nel processo di attivazione in base a ruolo, autorizzazioni ed etichette;
   * Nel processo di attivazione, potrebbe essere richiesto agli utenti di selezionare i campi che desiderano attivare in una destinazione. In qualità di amministratore, puoi assegnare agli utenti dell’organizzazione il provisioning per visualizzare solo i campi etichettati con le etichette a cui gli utenti hanno accesso e i campi che non contengono etichette.

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

* Applicare attributi a gruppi di campi e o classi. Ciò consente a più schemi con gli stessi gruppi di campi o classi, di assegnare ai campi i tag con gli stessi attributi, a seconda delle configurazioni a livello di gruppo di campi o di classe;
* Configura l&#39;accesso dell&#39;utente a specifici campi dello schema XDM in base ai set di autorizzazioni applicati ai ruoli assegnati agli utenti.

Per ulteriori informazioni su XDM, consulta la sezione [Panoramica di XDM](../../xdm/home.md).