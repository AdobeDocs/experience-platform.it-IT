---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Panoramica sulla governance dei dati
description: La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di Experience Platform a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: d45c813cf660d9bf738d09101536f1dfb41a1505
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 5%

---

# Panoramica sulla governance dei dati

Una delle funzionalità principali di Adobe Experience Platform è quella di unire i dati provenienti da più sistemi aziendali per consentire agli addetti al marketing di identificare, comprendere e coinvolgere i clienti. Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. È quindi importante garantire che le operazioni sui dati in [!DNL Platform] sono conformi ai criteri di utilizzo dei dati.

La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave in [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.

>[!NOTE]
>
>Ad Experience Platform, la governance dei dati riguarda solo il modo in cui i dati vengono utilizzati o attivati, indipendentemente dall’utente che esegue l’azione. Per informazioni su come controllare l’accesso a campi dati specifici per alcuni utenti di Platform all’interno della tua organizzazione, consulta la documentazione su [controllo degli accessi basato su attributi](../access-control/abac/overview.md) invece.

## Ruoli di governance dei dati

Il concetto di governance dei dati non è automatico, né si verifica nel vuoto. Quello che era iniziato come un ruolo per un singolo individuo, generalmente riconosciuto come un amministratore dei dati, è cresciuto considerevolmente con l’espansione dell’ecosistema di governance dei dati. Oggi, per avere successo, la governance dei dati richiede una gestione e un monitoraggio continui e si basa sulla disponibilità, da parte degli amministratori dei dati, di strumenti con cui etichettare correttamente i dati, creare criteri di utilizzo e garantirne la conformità.

Mentre la governance dei dati dovrebbe essere responsabilità di ogni individuo nell’organizzazione, ecco alcuni dei ruoli essenziali all’interno del ciclo di governance dei dati:

![Ruoli di governance dei dati](./images/overview/roles.png)

### Amministratore dati

Gli amministratori dei dati sono il cuore della governance dei dati. Questo ruolo è responsabile dell’interpretazione di regolamenti, restrizioni contrattuali e politiche e della loro applicazione diretta ai dati. Sulla base della loro comprensione di tali regolamenti, restrizioni e politiche, il ruolo di un amministratore dei dati include:

* Revisione di dati, set di dati ed esempi di dati per applicare e gestire l’etichettatura di utilizzo dei metadati.
* Creazione di criteri per i dati e loro applicazione a set di dati e campi.
* Comunicazione dei criteri dei dati all’organizzazione.

### Addetto marketing

Gli addetti al marketing rappresentano il punto finale della governance dei dati. Richiedono dati dall’infrastruttura di governance dei dati creata da amministratori di dati, scienziati e ingegneri. Gli addetti al marketing comprendono una serie di specialità diverse sotto l&#39;ombrello della commercializzazione, tra cui:

* Gli analisti di marketing richiedono dati per consentire la comprensione dei clienti, sia singolarmente che in gruppo (noti anche come segmenti).
* Gli esperti di marketing e i designer di esperienza utilizzano i dati per progettare nuove esperienze per i clienti.


## Framework di governance dei dati

Il framework per la governance dei dati semplifica e snellisce il processo di categorizzazione dei dati e di creazione di policy di utilizzo dei dati. Una volta applicate le etichette dei dati e applicati i criteri di utilizzo, è possibile valutare le azioni di marketing per garantire il corretto utilizzo dei dati.

Il framework per la governance dei dati include tre elementi chiave: Etichette, Criteri e Applicazione.

1. **Etichette** Classifica i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali in modo da essere conformi alle normative e alle politiche aziendali.
1. **Criteri:** Descrivi i tipi di azioni di marketing consentite o non consentite per l’esecuzione su dati specifici.
1. **Applicazione:** Utilizza il framework delle politiche per consigliare e applicare le politiche in diversi modelli di accesso ai dati.

## Etichette di utilizzo dati

La governance dei dati consente agli amministratori dei dati di applicare etichette di utilizzo a livello di campo schema e di set di dati per categorizzare i dati in base al tipo di criteri applicati.

Il framework per la governance dei dati include etichette di utilizzo dei dati predefinite che possono essere utilizzate per categorizzare i dati in tre modi:

![Categorie etichette utilizzo dati](./images/overview/label-categories.png)

* **Etichette dati contratto &quot;C&quot;:** Etichetta e categorizza i dati che hanno obblighi contrattuali o sono relativi alle politiche di governance dei dati dei clienti.
* **Etichette dati di identità &quot;I&quot;:** Etichettare e classificare i dati che possono identificare o contattare una persona specifica.
* **Etichette dati sensibili &quot;S&quot;:** Etichettare e classificare i dati relativi ai dati sensibili, ad esempio i dati geografici.

>[!NOTE]
>
>Consulta la guida su [etichette di utilizzo dei dati supportate](labels/reference.md) per un elenco completo delle etichette disponibili, nonché le definizioni per ciascun tipo di etichetta.

Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. La best practice incoraggia i dati di etichettatura non appena vengono acquisiti in [!DNL Experience Platform]o non appena i dati diventano disponibili in [!DNL Platform].

Consulta la panoramica su [etichette di utilizzo dei dati](./labels/overview.md) per ulteriori informazioni.

## Criteri di utilizzo dei dati {#data-usage-policies}

Affinché le etichette di utilizzo dei dati supportino in modo efficace la conformità, è necessario implementare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform].

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se è in vigore una politica che dichiara che non è possibile esportare informazioni personali (PII, Personally Identifiable Information) ed è stata applicata un’etichetta &quot;I&quot; (dati di identità) al livello di campo o al set di dati, [!DNL Policy Service] impedisce qualsiasi azione che potrebbe esportare questo set di dati in una destinazione di terze parti. Se si verifica uno di questi tentativi di azione, Policy Service invia un messaggio per informarti che un criterio di utilizzo dei dati è stato violato.

Sono disponibili due tipi di criteri:

* **[!UICONTROL Criteri di governance dei dati]**: limita l’attivazione dei dati in base all’azione di marketing che viene eseguita e alle etichette di utilizzo dei dati presenti nei dati in questione.
* **[!UICONTROL Criterio di consenso]**: filtra i profili che possono essere attivati in [destinazioni](../destinations/home.md) in base al consenso o alle preferenze dei clienti.

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono creare criteri utilizzando [!DNL Policy Service] API o [!DNL Experience Platform] dell&#39;utente. Per ulteriori informazioni sui criteri di utilizzo dei dati e sulle azioni di marketing, consulta [panoramica dei criteri](./policies/overview.md).

>[!IMPORTANT]
>
>Tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, è necessario abilitarlo manualmente.

## Passaggi successivi

Questo documento fornisce un’introduzione di alto livello alla governance dei dati e al framework per la governance dei dati. Ora puoi passare alla sezione [guida utente delle etichette di utilizzo dati](labels/user-guide.md) e inizia ad aggiungere etichette di utilizzo ai dati dell’esperienza.

## Appendice

La sezione seguente fornisce ulteriori informazioni sulla governance dei dati.

### Terminologia per la governance dei dati {#data-governance-terminology}

La tabella seguente illustra i termini chiave relativi alla governance dei dati e al framework per la governance dei dati.

| Termine | Definizione |
|---|---|
| **Etichette contratto** | Le etichette &quot;C&quot; del contratto vengono utilizzate per categorizzare i dati che hanno obblighi contrattuali o sono relativi ai criteri di governance dei dati della tua organizzazione. |
| **Dati intersito** | I dati intersito sono la combinazione di dati provenienti da diversi siti, inclusa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse origini esterne al sito. |
| **Governance dei dati** | La governance dei dati include le strategie e le tecnologie utilizzate per garantire la conformità dei dati alle normative e alle politiche aziendali in relazione all’utilizzo dei dati. |
| **Amministratore dati** | L’amministratore dei dati è la persona responsabile della gestione, della supervisione e dell’applicazione delle risorse di dati di un’organizzazione. Un data steward garantisce inoltre che i criteri di governance dei dati siano salvaguardati e mantenuti in modo da essere conformi alle normative governative e ai criteri organizzativi. |
| **Etichette di utilizzo dati** | Le etichette di utilizzo dei dati consentono agli utenti di categorizzare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e alle politiche aziendali. |
| **Etichette set di dati** | È possibile aggiungere etichette a uno schema. Tutti i campi all’interno di un set di dati ereditano le etichette dello schema. |
| **Etichette campo** | Le etichette dei campi sono etichette di governance dei dati ereditate da uno schema o applicate direttamente a un campo. Le etichette di governance dei dati applicate a un campo non vengono ereditate fino al livello dello schema. |
| **Recinto geografico** | Un recinto geografico è un confine geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da una determinata area. |
| **Etichette di identità** | Le etichette di identità &quot;I&quot; vengono utilizzate per categorizzare i dati che possono identificare o contattare una persona specifica. |
| **Targeting basato sugli interessi** | Il targeting basato sugli interessi, noto anche come personalizzazione, si verifica se sono soddisfatte le tre condizioni seguenti: i dati raccolti sul sito sono utilizzati per trarre conclusioni sull’interesse di un utente, sono utilizzati in un altro contesto, ad esempio su un altro sito o un’altra app (fuori sito) e vengono utilizzati per selezionare quali contenuti o annunci vengono distribuiti in base a tali conclusioni. |
| **Azione di marketing** | Un’azione di marketing, nel contesto del framework di governance dei dati, è un’azione che [!DNL Experience Platform] dati richiesti dal consumatore, per i quali è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati |
| **Criterio** | Nel framework di governance dei dati, un criterio è una regola che descrive il tipo di azioni di marketing consentite o meno da intraprendere su dati specifici. |
| **Etichette schema** | Gestisci le etichette per la governance dei dati, il consenso e il controllo degli accessi a livello di schema. In questo modo le etichette vengono propagate a ogni set di dati che utilizza tale schema. |
| **Etichette sensibili** | Le etichette sensibili &quot;S&quot; vengono utilizzate per categorizzare i dati considerati sensibili dall’utente e dall’organizzazione. |

## Risorse aggiuntive

Il video seguente ha lo scopo di aiutarti a comprendere il framework di governance dei dati.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

<!-- A key section of the video is now outdated due to the deprecation of the dataset field level labelling feature.

The following video provides an introduction to various Data Governance features in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on) -->
