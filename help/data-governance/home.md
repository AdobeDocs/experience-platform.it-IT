---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Panoramica sulla governance dei dati
description: La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 1a050cfb41a28053606f07931c7c97d15989ac3e
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 9%

---

# Panoramica sulla governance dei dati {#data-governance-overview}

>[!CONTEXTUALHELP]
>id="platform_datagovernance_framework"
>title="Obbligo di governance dei dati"
>abstract="Ricorda che è tua esclusiva responsabilità rispettare i criteri di governance dei dati della tua organizzazione e soddisfare i requisiti normativi. Experience Platform fornisce strumenti di governance dei dati per aiutarti a gestire gli obblighi in materia di utilizzo dei dati. Applica le etichette di utilizzo dei dati appropriate prima di eseguire query o elaborare dati. Consulta la documentazione per scoprire gli strumenti di governance dei dati e le best practice."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it" text="Panoramica sulla governance dei dati"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=it" text="Panoramica delle etichette per la governance dei dati"

Una delle funzionalità principali di Adobe Experience Platform è quella di unire i dati provenienti da più sistemi aziendali per consentire agli addetti al marketing di identificare, comprendere e coinvolgere i clienti. Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. È quindi importante assicurarsi che le operazioni sui dati in [!DNL Platform] siano conformi ai criteri di utilizzo dei dati.

Gestisci i dati dei clienti e assicurati la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati con la governance dei dati di Adobe Experience Platform. La governance dei dati svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.

>[!NOTE]
>
>Ad Experience Platform, la governance dei dati riguarda solo il modo in cui i dati vengono utilizzati o attivati, indipendentemente dall’utente che esegue l’azione. Per informazioni su come controllare l&#39;accesso a campi dati specifici per alcuni utenti di Platform all&#39;interno della tua organizzazione, consulta invece la documentazione sul [controllo dell&#39;accesso basato su attributi](../access-control/abac/overview.md).

## Ruoli di governance dei dati {#data-governance-roles}

Il concetto di governance dei dati non è automatico, né si verifica nel vuoto. Quello che era iniziato come un ruolo per un singolo individuo, generalmente riconosciuto come un amministratore dei dati, è cresciuto considerevolmente con l’espansione dell’ecosistema di governance dei dati. Oggi, per avere successo, la governance dei dati richiede una gestione e un monitoraggio continui. Un’efficace governance dei dati si basa sulla disponibilità, da parte degli amministratori di dati, di strumenti con cui etichettare correttamente i dati, creare criteri di utilizzo e garantirne la conformità.

Mentre la governance dei dati dovrebbe essere responsabilità di ogni individuo nell’organizzazione, ecco alcuni dei ruoli essenziali all’interno del ciclo di governance dei dati:

![Grafico per trasmettere i quattro ruoli di governance dei dati, con virgolette sui compiti di ogni ruolo.](./images/overview/roles.png)

### Amministratore dati {#data-steward}

Gli amministratori dei dati sono il cuore della governance dei dati. Questo ruolo è responsabile dell’interpretazione di regolamenti, restrizioni contrattuali e politiche e della loro applicazione diretta ai dati. Sulla base della loro comprensione di tali regolamenti, restrizioni e politiche, il ruolo di un amministratore dei dati include:

* Revisione di dati, set di dati ed esempi di dati per applicare e gestire l’etichettatura di utilizzo dei metadati.
* Creazione di criteri per i dati e loro applicazione a set di dati e campi.
* Comunicazione dei criteri dei dati all’organizzazione.

### Addetto marketing {#marketer}

Gli addetti al marketing rappresentano il punto finale della governance dei dati. Richiedono dati dall’infrastruttura di governance dei dati creata da amministratori di dati, scienziati e ingegneri. Gli addetti al marketing comprendono una serie di specialità diverse sotto l&#39;ombrello della commercializzazione, tra cui:

* Gli analisti di marketing richiedono dati per consentire la comprensione dei clienti, sia singolarmente che in gruppo (noti anche come segmenti).
* Gli esperti di marketing e i designer di esperienza utilizzano i dati per progettare nuove esperienze per i clienti.

## Framework di governance dei dati {#data-governance-framework}

Il framework per la governance dei dati semplifica e snellisce il processo di categorizzazione dei dati e di creazione di policy di utilizzo dei dati. Una volta applicate le etichette dei dati e applicati i criteri di utilizzo, è possibile valutare le azioni di marketing per garantire il corretto utilizzo dei dati.

Il framework per la governance dei dati include tre elementi chiave: Etichette, Criteri e Applicazione.

1. **Etichette:** Classifica i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e ai criteri organizzativi.
1. **Criteri:** Descrivi i tipi di azioni di marketing consentite o meno per dati specifici.
1. **Applicazione:** utilizza il framework dei criteri per consigliare e applicare i criteri in diversi modelli di accesso ai dati.

## Etichette di utilizzo dei dati {#data-usage-labels}

La governance dei dati consente agli amministratori dei dati di applicare etichette di utilizzo a livello di campo schema per categorizzare i dati in base al tipo di criteri applicati.

Il framework per la governance dei dati include etichette di utilizzo dei dati predefinite che possono essere utilizzate per categorizzare i dati in tre modi:

![Le tre categorie di etichette di utilizzo dei dati.](./images/overview/label-categories.png)

* **Etichette per i dati del contratto &quot;C&quot;:** Etichetta e categorizza i dati che hanno obblighi contrattuali o sono relativi ai criteri di governance dei dati del cliente.
* **Etichette dati di identità &quot;I&quot;:** Etichetta e categorizza i dati che possono identificare o contattare una persona specifica.
* **Etichette dati sensibili &quot;S&quot;:** Etichetta e categorizza i dati relativi ai dati sensibili, ad esempio i dati geografici.

>[!NOTE]
>
>Per un elenco completo delle etichette disponibili e delle definizioni per ogni tipo di etichetta, consulta la guida su [etichette di utilizzo dati supportate](labels/reference.md).

Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. La best practice incoraggia l&#39;assegnazione di etichette ai dati quando vengono acquisiti in Experience Platform o non appena i dati diventano disponibili in [!DNL Platform].

Per ulteriori informazioni su come utilizzare le etichette di utilizzo dei dati per applicare la conformità alla governance dei dati, consulta la panoramica sulle [etichette di utilizzo dei dati](./labels/overview.md).

## Criteri di utilizzo dei dati {#data-usage-policies}

Affinché le etichette di utilizzo dei dati supportino in modo efficace la conformità, è necessario implementare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati di Experience Platform.

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se è in vigore un criterio che dichiara che non è possibile esportare informazioni personali (PII, Personally Identifiable Information) ed è stata applicata un’etichetta &quot;I&quot; (dati di identità) al livello di campo dal relativo schema. Policy Service impedisce quindi qualsiasi azione che potrebbe esportare questo set di dati in una destinazione di terze parti. Se si verifica uno di questi tentativi di azione, Policy Service invia un messaggio per informarti che un criterio di utilizzo dei dati è stato violato.


Sono disponibili due tipi di criteri:

* **[!UICONTROL Criteri di governance dei dati]**: limita l&#39;attivazione dei dati in base all&#39;azione di marketing in esecuzione e alle etichette di utilizzo dei dati presenti nei dati in questione.
* **[!UICONTROL Criteri di consenso]**: filtra i profili che possono essere attivati in [destinazioni](../destinations/home.md) in base al consenso o alle preferenze dei tuoi clienti.

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono creare criteri utilizzando l’API del servizio criteri o l’interfaccia utente di Experience Platform. Per ulteriori informazioni sui criteri di utilizzo dei dati e sulle azioni di marketing, consulta la [panoramica dei criteri](./policies/overview.md).

>[!IMPORTANT]
>
>Tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, è necessario abilitarlo manualmente.

## Passaggi successivi

Questo documento fornisce un’introduzione di alto livello alla governance dei dati e al framework per la governance dei dati. Ora puoi continuare a consultare la [guida utente delle etichette di utilizzo dei dati](labels/user-guide.md) e iniziare ad aggiungere etichette di utilizzo ai dati dell&#39;esperienza.

## Appendice

La sezione seguente fornisce ulteriori informazioni sulla governance dei dati.

### Terminologia per la governance dei dati {#data-governance-terminology}

La tabella seguente illustra i termini chiave relativi alla governance dei dati e al framework per la governance dei dati.

| Termine | Definizione |
|---|---|
| **Etichette contratto** | Le etichette &quot;C&quot; del contratto vengono utilizzate per categorizzare i dati che hanno obblighi contrattuali o sono relativi ai criteri di governance dei dati della tua organizzazione. |
| **Dati intersito** | I dati cross-site rappresentano la combinazione di dati provenienti da più siti. I dati intersito includono sia i dati nel sito che quelli esterni al sito, oppure una combinazione di dati provenienti da diverse origini esterne al sito. |
| **Governance dei dati** | La governance dei dati include le strategie e le tecnologie utilizzate per garantire la conformità dei dati alle normative e alle politiche aziendali in relazione all’utilizzo dei dati. |
| **Data Steward** | L’amministratore dei dati è la persona responsabile della gestione, della supervisione e dell’applicazione delle risorse di dati di un’organizzazione. Un data steward assicura inoltre che i criteri di governance dei dati siano salvaguardati e mantenuti in modo da essere conformi alle normative governative e ai criteri organizzativi. |
| **Etichette di utilizzo dati** | Le etichette di utilizzo dei dati consentono agli utenti di categorizzare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e alle politiche aziendali. |
| **Etichette set di dati** | È possibile aggiungere etichette a uno schema. Tutti i campi all’interno di un set di dati ereditano le etichette dello schema. |
| **Etichette campo** | Le etichette dei campi sono etichette di governance dei dati ereditate da uno schema o applicate direttamente a un campo. Le etichette di governance dei dati applicate a un campo non vengono ereditate fino al livello dello schema. |
| **Recinto geografico** | Un recinto geografico è un confine geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da una determinata area. |
| **Etichette di identità** | Le etichette di identità “I” vengono utilizzate per categorizzare i dati che possono identificare o contattare una persona specifica. |
| **Destinazione basata su interessi** | Il targeting basato su interessi, noto anche come personalizzazione, si verifica se vengono soddisfatte le tre condizioni seguenti:<br>I dati raccolti nel sito sono,<br><ul><li>Utilizzato per trarre conclusioni sull’interesse di un utente,</li><li>Utilizzato in un altro contesto, ad esempio in un altro sito o in un’altra app (fuori sito)</li><li>Utilizzato per selezionare quali contenuti o annunci vengono distribuiti in base a tali inferenze.</li></ul> |
| **Azione di marketing** | Un’azione di marketing, nel contesto del framework di governance dei dati, è un’azione intrapresa da un consumatore di dati Experience Platform, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati |
| **Criterio** | Nel framework di governance dei dati, un criterio è una regola che descrive quali tipi di azioni di marketing sono consentiti o meno per essere eseguiti su dati specifici. |
| **Etichette schema** | Gestisci le etichette per la governance dei dati, il consenso e il controllo degli accessi a livello di schema. In questo modo le etichette vengono propagate a ogni set di dati che utilizza tale schema. |
| **Etichette sensibili** | Le etichette sensibili &quot;S&quot; vengono utilizzate per categorizzare i dati considerati sensibili dall’utente e dall’organizzazione. |

## Risorse aggiuntive

Il video seguente ha lo scopo di aiutarti a comprendere il framework di governance dei dati.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

Il video seguente fornisce indicazioni su come applicare le etichette di utilizzo dei dati agli schemi o all’intero set di dati in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29709/?learn=on)
