---
title: Utilizzare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati di destinazione
description: Scopri come utilizzare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati di destinazione in modo che solo un sottoinsieme di utenti dell’organizzazione possa accedere a flussi di dati di destinazione specifici.
badgePrivateBeta: label="Versione beta privata" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
source-git-commit: 5e5dc2f755be0f396dec1d3f19c166bae3bc9575
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---


# Utilizzare le etichette di accesso per gestire l’accesso degli utenti ai flussi di dati di destinazione

Nell&#39;ambito del [!UICONTROL Controllo degli accessi basato su attributi] funzionalità di Real-Time CDP, ora puoi applicare etichette di accesso ai flussi di dati di destinazione. In questo modo, puoi garantire che solo un sottoinsieme di utenti dell’organizzazione abbia accesso a flussi di dati di destinazione specifici.

Quando aggiungi un’etichetta di accesso a una particolare destinazione, solo gli utenti che hanno accesso a un ruolo a cui è assegnata tale etichetta possono visualizzare e modificare tale flusso di dati di destinazione. Se un flusso di dati di destinazione non è contrassegnato con alcuna etichetta, è visibile a tutti gli utenti appartenenti alla tua organizzazione.

Leggi questa pagina per comprendere alcuni casi d’uso di esempio, i prerequisiti prima di poter applicare le etichette di accesso ai flussi di dati di destinazione e altri callout importanti quando utilizzi questa funzionalità.

## Prerequisiti {#prerequisites}

Prima di iniziare a utilizzare questa funzionalità, tieni presente i seguenti prerequisiti da completare. Per acquisire familiarità con [!UICONTROL Controllo degli accessi basato su attributi] Adobe consiglia inoltre di leggere i seguenti articoli:

* [Panoramica sul controllo degli accessi basato su attributi](/help/access-control/abac/overview.md)
* [Guida end-to-end al controllo degli accessi basato su attributi](/help/access-control/abac/end-to-end-guide.md)

### Accesso all’interfaccia utente delle autorizzazioni {#access-permissions-ui}

[!UICONTROL Autorizzazioni] è l’area di Experience Cloud in cui gli amministratori possono definire ruoli utente e criteri per gestire le autorizzazioni per funzioni e oggetti all’interno di un’applicazione di prodotto. Leggi le [sezione autorizzazioni](/help/access-control/abac/end-to-end-guide.md#permissions) per iniziare.

### Creare ruoli, etichette e assegnare utenti {#create-roles-labels-assign-users}

Dopo aver ottenuto l’accesso a [!UICONTROL autorizzazioni] Nell’interfaccia utente, è necessario impostare i ruoli e aggiungere le etichette richieste a tali ruoli. Infine, è necessario aggiungere al ruolo gli utenti che devono accedere alle risorse etichettate con le etichette specifiche. Consulta le seguenti sezioni della documentazione:

* [Creare un nuovo ruolo](/help/access-control/abac/ui/roles.md)
* [Aggiungere etichette a un ruolo](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Aggiungere utenti a un ruolo](/help/access-control/ui/users.md)

### Creare flussi di dati di destinazione {#create-dataflow}

Prima di poter applicare le etichette di accesso al flusso di dati, è innanzitutto necessario connettersi alla destinazione desiderata e creare un flusso di dati per esportare i dati.

Leggi le guide su [connessione a una destinazione](/help/destinations/ui/connect-destination.md) e [attivazione dei dati nella destinazione](/help/destinations/ui/activation-overview.md). Quindi, seleziona la destinazione desiderata da [catalogo dei connettori disponibili](/help/destinations/catalog/overview.md).

## Già disponibile: Applica etichette di accesso ad altre risorse Experienci Platform {#apply-labels-other-resources}

Questa versione di consente di concedere agli utenti l’accesso a livello di oggetto a flussi di dati di destinazione specifici; tuttavia, la funzionalità per concedere il controllo di accesso a livello di oggetto è già generalmente disponibile per altre risorse di Experience Platform, come [audience](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Esempio di caso d’uso {#use-case-example}

Con il controllo dell’accesso a livello di oggetto per le destinazioni, limita i team specifici di addetti al marketing ad accedere solo alle loro destinazioni specifiche. Ad esempio, se la tua organizzazione dispone di dati dei clienti in diverse posizioni geografiche, come Stati Uniti e Regno Unito, puoi limitare un team di marketing a visualizzare e modificare i flussi di dati solo per la posizione negli Stati Uniti e un altro team di marketing a visualizzare e modificare i flussi di dati per la posizione nel Regno Unito.

## Applicare le etichette di accesso ai flussi di dati di destinazione {#apply-labels-to-destination-dataflow}

Per applicare le etichette di accesso a un flusso di dati specifico:

1. Accedi a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** e individua il flusso di dati di destinazione a cui desideri limitare l’accesso degli utenti.
1. Seleziona i puntini di sospensione (`...`) in [!UICONTROL Nome] e utilizza la ![Modifica controllo dettagli](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL Applica etichette di accesso]** per aggiungere nuove etichette e gestire le etichette esistenti per il flusso di dati.
   ![Seleziona Applica etichette di accesso nella vista Sfoglia dell’area di lavoro delle destinazioni.](/help/access-control/images/olac/apply-access-labels.png)
1. Seleziona le etichette da aggiungere al flusso di dati di destinazione e seleziona **[!UICONTROL Salva]**.
   ![Seleziona le etichette di accesso in che devono essere applicate al flusso di dati di destinazione.](/help/access-control/images/olac/view-access-labels.png)
1. Osserva come ora il flusso di dati presenta un’etichetta di accesso nell’interfaccia utente.
   ![Visualizzazione di diversi flussi di dati di destinazione con il flusso di dati selezionato e visualizzazione di un’etichetta di accesso.](/help/access-control/images/olac/dataflow-with-access-label.png)

Se un flusso di dati di destinazione non è contrassegnato con alcuna etichetta, verrà visualizzato per tutti gli utenti. Se il flusso di dati è contrassegnato con una o più etichette di accesso, verrà visualizzato solo per gli utenti appartenenti a un ruolo con la stessa etichetta o combinazione di etichette.

Puoi aggiungere etichette standard e personalizzate ai flussi di dati di destinazione. Dopo aver aggiunto un’etichetta ai flussi di dati di destinazione:

* Gli utenti assegnati a ruoli con accesso alla stessa etichetta possono visualizzare il flusso di dati con la nuova etichetta nell’interfaccia utente. Possono visualizzare e modificare il flusso di dati di destinazione nell’interfaccia utente o tramite API.

* Utenti che sono *non* i ruoli assegnati a con accesso alla stessa etichetta non hanno accesso al flusso di dati di destinazione per visualizzarlo o modificarlo nell’interfaccia utente o tramite API.

## Callout importanti ed elementi da conoscere {#important-callouts}

Attualmente, le etichette di accesso possono essere applicate solo ai flussi di dati esistenti. Ciò significa che è necessario creare il flusso di dati nella destinazione prima di poter applicare le etichette di accesso.

Non puoi applicare un’etichetta di accesso a un flusso di dati di destinazione se non hai accesso a tale etichetta.

Quando si aggiungono più etichette a un flusso di dati di destinazione, gli utenti che devono essere in grado di visualizzare e modificare il flusso di dati devono essere aggiunti a un ruolo con almeno la stessa combinazione di etichette. Ad esempio, se applichi le etichette C1, I2 e un’altra etichetta personalizzata a un flusso di dati di destinazione, solo gli utenti aggiunti ai ruoli con accesso alla combinazione di queste tre etichette possono visualizzare e modificare questo flusso di dati di destinazione specifico.

![Diagramma di Venn che mostra come solo alcuni utenti hanno accesso a destinazioni con più etichette applicate.](/help/access-control/images/olac/multiple-labels-venn.png)

## Passaggi successivi {#next-steps}

Seguendo i passaggi descritti in questo documento, ora sai come applicare le etichette di accesso ai flussi di dati di destinazione in modo che solo un sottoinsieme di utenti dell’organizzazione possa accedere a flussi di dati di destinazione specifici.

Ulteriori informazioni sulle altre funzionalità supportate da [!UICONTROL Controllo degli accessi basato su attributi] quando si attivano i dati nelle destinazioni. Ad esempio, puoi limitare l’accesso degli utenti a [visualizza e attiva solo campi specifici](/help/access-control/abac/overview.md#destinations).