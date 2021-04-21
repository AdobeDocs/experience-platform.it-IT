---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Panoramica sulla governance dei dati
topic-legacy: overview
description: La governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno dell’Experience Platform a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 0%

---

# Panoramica sulla governance dei dati

Una delle funzionalità principali di Adobe Experience Platform è quella di unire i dati provenienti da più sistemi aziendali per consentire agli addetti al marketing di identificare, comprendere e coinvolgere meglio i clienti. Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. È quindi importante assicurarsi che le operazioni sui dati all’interno di [!DNL Platform] siano conformi ai criteri di utilizzo dei dati.

Adobe Experience Platform [!DNL Data Governance] ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all’interno di [!DNL Experience Platform] a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.

## Ruoli di governance dei dati

Come concetto, la governance dei dati non è automatica, né si verifica nel vuoto. Ciò che è iniziato come ruolo per un singolo individuo, generalmente riconosciuto come amministratore dei dati, è cresciuto notevolmente con l&#39;espansione dell&#39;ecosistema di governance dei dati. Oggi, la governance dei dati richiede una gestione e un monitoraggio continui per avere successo e si basa sul fatto che i responsabili della gestione dei dati dispongano di strumenti con i quali i dati possono essere correttamente etichettati, possono essere creati criteri di utilizzo e la conformità a tali criteri può essere applicata.

Mentre la governance dei dati dovrebbe essere responsabilità di ogni individuo dell’organizzazione, ecco alcuni dei ruoli essenziali all’interno del ciclo di governance dei dati:

![Ruoli di governance dei dati](./images/overview/roles.png)

### Data steward

Gli amministratori dei dati sono il cuore della governance dei dati. Questo ruolo è responsabile dell&#39;interpretazione delle normative, delle restrizioni contrattuali e delle politiche e della loro applicazione diretta ai dati. In base alla loro comprensione di tali regolamenti, restrizioni e politiche, il ruolo di un responsabile del trattamento dei dati include:

* Analisi di dati, set di dati ed esempi di dati per applicare e gestire l’etichettatura dell’utilizzo dei metadati.
* Creazione di criteri per i dati e loro applicazione a set di dati e campi.
* Comunicazione dei criteri dei dati all&#39;organizzazione.

### Addetto marketing

Gli addetti al marketing sono il punto finale della governance dei dati. Richiedono i dati dall&#39;infrastruttura di governance dei dati creata da amministratori di dati, scienziati e ingegneri. Gli addetti al marketing includono diverse specialità nell’ambito del marketing, tra cui:

* Gli analisti di marketing richiedono i dati per consentire la comprensione dei clienti, sia come individui che in gruppi (noti anche come segmenti).
* Gli esperti marketing e i designer di esperienze utilizzano i dati per progettare nuove esperienze cliente.


## [!DNL Data Governance] quadro

Il framework [!DNL Data Governance] semplifica e semplifica il processo di categorizzazione dei dati e creazione di criteri di utilizzo dei dati. Una volta applicate le etichette dei dati e stabiliti i criteri di utilizzo dei dati, è possibile valutare le azioni di marketing per garantire l’uso corretto dei dati.

Il framework [!DNL Data Governance] presenta tre elementi chiave: Etichette, criteri e applicazione.

1. **Etichette:** classifica i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e ai criteri aziendali.
1. **Criteri:** descrive i tipi di azioni di marketing consentite o non consentite per dati specifici.
1. **Applicazione:** utilizza il framework dei criteri per consigliare e applicare le politiche in diversi modelli di accesso ai dati.

## Etichette di utilizzo dati

[!DNL Data Governance] consente agli amministratori di dati di applicare etichette di utilizzo a livello di set di dati e di campo per classificare i dati in base al tipo di criteri applicabili.

Il framework [!DNL Data Governance] include etichette di utilizzo dati predefinite che possono essere utilizzate per classificare i dati in tre modi:

![Categorie delle etichette per l&#39;utilizzo dei dati](./images/overview/label-categories.png)

* **Etichette per i dati &quot;C&quot; del contratto:** Etichettare e categorizzare i dati che hanno obblighi contrattuali o sono relativi alle politiche di governance dei dati del cliente.
* **Etichette per i dati di identità &quot;I&quot;:** etichettare e classificare i dati che possono identificare o contattare una persona specifica.
* **Etichette per i dati sensibili &quot;S&quot;:** etichetta e categorizza i dati relativi a dati sensibili, come i dati geografici.

>[!NOTE]
>
>Per un elenco completo delle etichette disponibili e delle definizioni per ogni tipo di etichetta, consulta la guida sulle [etichette di utilizzo dei dati supportate](labels/reference.md) .

Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. La best practice incoraggia l’etichettatura dei dati non appena vengono acquisiti in [!DNL Experience Platform] o non appena i dati diventano disponibili in [!DNL Platform].

Per ulteriori informazioni, consulta la panoramica sulle [etichette di utilizzo dei dati](./labels/overview.md) .

## Criteri di utilizzo dei dati

Affinché le etichette per l’utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare i criteri per l’utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o a cui è stata limitata l’esecuzione di dati all’interno di [!DNL Experience Platform].

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se esiste un criterio che indica che tipi specifici di dati, come Informazioni personali (PII, Personally Identifiable Information), non possono essere esportati e che è stata applicata un’etichetta &quot;I&quot; (Dati identità) al set di dati, riceverai una risposta da [!DNL Policy Service] che informa che è stata violata una policy di utilizzo dei dati.

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono creare criteri utilizzando l’ [!DNL Policy Service] API o l’ interfaccia utente [!DNL Experience Platform].

>[!IMPORTANT]
>
>Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l&#39;applicazione, è necessario abilitare manualmente tale criterio.

Per ulteriori informazioni sui criteri di utilizzo dei dati e sulle azioni di marketing, consulta la [panoramica dei criteri](./policies/overview.md).

## Passaggi successivi

Questo documento fornisce un&#39;introduzione di alto livello al framework [!DNL Data Governance] e[!DNL Data Governance]. Ora puoi continuare con la [guida utente delle etichette per l’utilizzo dei dati](labels/user-guide.md) e iniziare ad aggiungere etichette di utilizzo ai dati dell’esperienza.

## Appendice

La sezione seguente fornisce ulteriori informazioni su [!DNL Data Governance].

### [!DNL Data Governance] terminologia

La tabella seguente illustra i termini chiave relativi al framework [!DNL Data Governance] e[!DNL Data Governance] .

| Termine | Definizione |
|---|---|
| **Etichette per i contratti** | Le etichette &quot;C&quot; del contratto vengono utilizzate per classificare i dati che hanno obblighi contrattuali o sono correlati alle politiche di governance dei dati della tua organizzazione. |
| **Dati intersito** | I dati intersito sono la combinazione di dati provenienti da diversi siti, inclusa una combinazione di dati sul sito e dati fuori sito o una combinazione di dati provenienti da più fonti esterne al sito. |
| **Governance dei dati** | La governance dei dati include le strategie e le tecnologie utilizzate per garantire che i dati siano conformi alle normative e alle politiche aziendali in materia di utilizzo dei dati. |
| **Data steward** | Il responsabile del trattamento dei dati è la persona responsabile della gestione, della sorveglianza e dell&#39;applicazione delle risorse di dati di un&#39;organizzazione. Un amministratore dei dati garantisce inoltre che le politiche di governance dei dati siano salvaguardate e mantenute in conformità con le normative e le politiche di organizzazione governative. |
| **Etichette di utilizzo dati** | Le etichette per l’utilizzo dei dati consentono agli utenti di categorizzare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e ai criteri aziendali. |
| **Etichette set di dati** | Le etichette possono essere aggiunte a un set di dati. Tutti i campi all’interno di un set di dati ereditano le etichette del set di dati. |
| **Etichette per i campi** | Le etichette dei campi sono etichette di governance dei dati ereditate da un set di dati o applicate direttamente a un campo.  Le etichette di governance dei dati applicate a un campo non vengono ereditate fino a un set di dati. |
| **Geofence** | Un recinto geografico è un limite geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da una determinata area. |
| **Etichette di identità** | Le etichette di identità &quot;I&quot; vengono utilizzate per classificare i dati che possono identificare o contattare una persona specifica. |
| **Targeting basato su interessi** | Il targeting basato sugli interessi, noto anche come personalizzazione, si verifica se sono soddisfatte le tre condizioni seguenti: i dati raccolti sul sito vengono utilizzati per fare deduzioni sull’interesse degli utenti, vengono utilizzati in un altro contesto, ad esempio su un altro sito o un’app (fuori sito), e vengono utilizzati per selezionare quali contenuti o annunci vengono serviti in base a tali deduzioni. |
| **Azione di marketing** | Un’azione di marketing, nel contesto del framework di governance dei dati, è un’azione eseguita da un consumatore di dati [!DNL Experience Platform] per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati |
| **Criterio** | Nel framework di governance dei dati, una policy è una regola che descrive il tipo di azioni di marketing consentite o non consentite su dati specifici. |
| **Etichette sensibili** | Le etichette &quot;S&quot; sensibili vengono utilizzate per classificare i dati che tu e la tua organizzazione consideri sensibili. |

## Risorse aggiuntive

Il video seguente è pensato per comprendere meglio il framework [!DNL Data Governance] .

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

Il video seguente fornisce un’introduzione alle varie funzioni di [!DNL Data Governance] in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
