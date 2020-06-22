---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Governance dei dati  Adobe Experience Platform
topic: overview
translation-type: tm+mt
source-git-commit: 42d4fe7eecf1f64fab1c9554cfdc4bfeb42ffdeb
workflow-type: tm+mt
source-wordcount: '1462'
ht-degree: 0%

---


# Panoramica sulla governance dei dati

Una delle funzionalità principali di  Adobe Experience Platform consiste nel mettere insieme i dati provenienti da più sistemi aziendali per consentire ai professionisti del marketing di identificare, comprendere e coinvolgere meglio i clienti. Questi dati possono essere soggetti a restrizioni d&#39;uso definite dalla tua organizzazione o dalle normative legali. È pertanto importante garantire che le operazioni relative ai dati in Platform siano conformi ai criteri di utilizzo dei dati.

 Adobe Experience Platform Data Governance consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. Esso svolge un ruolo chiave all&#39;interno  Experience Platform a vari livelli, tra cui catalogazione, linea di dati, etichettatura dell&#39;uso dei dati, criteri di utilizzo dei dati e controllo dell&#39;utilizzo dei dati per le azioni di marketing.

## Ruoli di governance dei dati

Come concetto, la governance dei dati non è automatica, né avviene nel vuoto. Ciò che è iniziato come un ruolo per un singolo individuo, generalmente riconosciuto come amministratore dei **dati**, è cresciuto considerevolmente con l&#39;espansione dell&#39;ecosistema di governance dei dati. Oggi, la governance dei dati richiede una gestione e un monitoraggio continui per avere successo e si affida agli amministratori dei dati che dispongono di strumenti con cui i dati possono essere correttamente etichettati, è possibile creare criteri di utilizzo e applicare la conformità a tali criteri.

Mentre la governance dei dati dovrebbe essere responsabilità di ogni individuo nell&#39;organizzazione, ecco alcuni dei ruoli essenziali all&#39;interno del ciclo di governance dei dati:

![Ruoli di governance dei dati](./images/overview/roles.png)

### Amministratori dati

Gli amministratori dei dati sono il cuore della governance dei dati. Questo ruolo è responsabile dell&#39;interpretazione di regolamenti, restrizioni contrattuali e politiche, e della loro applicazione diretta ai dati. In base alla loro comprensione di tali regolamenti, restrizioni e politiche, il ruolo di amministratore dei dati include:

* Analisi di dati, set di dati ed esempi di dati per applicare e gestire l’etichettatura dell’utilizzo dei metadati.
* Creazione di criteri di dati e loro applicazione a set di dati e campi.
* Comunicazione dei criteri dati all&#39;organizzazione.

### Marketer

Gli esperti di marketing sono il punto finale della governance dei dati. Richiedono dati dall&#39;infrastruttura di governance dei dati creata da amministratori di dati, scienziati e ingegneri. Gli esperti di marketing includono diverse specialità diverse sotto l&#39;ombrello marketing, tra cui:

* Gli analisti del marketing richiedono i dati per consentire la comprensione dei clienti, sia come individui che in gruppi (noti anche come segmenti).
* Gli esperti di marketing e i progettisti di esperienze utilizzano i dati per progettare nuove esperienze cliente.


## DULE Framework

L&#39;etichettatura e l&#39;applicazione dell&#39;uso dei dati (DULE) è il framework di base per  gestione dei dati Experience Platform. DULE semplifica e semplifica il processo di classificazione dei dati e creazione di criteri di utilizzo dei dati. Una volta applicate le etichette dati e applicate le policy di utilizzo dei dati, è possibile valutare le azioni di marketing per garantire l&#39;uso corretto dei dati.

Il quadro DULE contiene tre elementi chiave: Etichette, politiche e applicazione.

1. **Etichette:** Classificare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali in modo che siano conformi alle normative e alle politiche aziendali.
1. **Criteri:** Descrivere i tipi di azioni di marketing consentite o non consentite per dati specifici.
1. **Esecuzione:** Utilizza il framework del criterio per consigliare e applicare criteri tra diversi pattern di accesso ai dati.

## Etichette di utilizzo dati

La governance dei dati consente agli amministratori dei dati di applicare etichette di utilizzo a livello di set di dati e di campi per classificare i dati in base al tipo di criteri applicabili.

Il framework DULE include etichette di utilizzo dei dati predefinite che possono essere utilizzate per classificare i dati in tre modi:

![Categorie delle etichette di utilizzo dei dati](./images/overview/label-categories.png)

* **Etichette dati contratto &quot;C&quot;:** Etichettare e classificare i dati che hanno obblighi contrattuali o che sono correlati a criteri di governance dei dati dei clienti.
* **Etichette Dati Identità &quot;I&quot;:** Etichettare e classificare i dati in grado di identificare o contattare una persona specifica.
* **Etichette dati sensibili &quot;S&quot;:** Etichettare e classificare i dati relativi a dati sensibili, ad esempio dati geografici.

>[!NOTE] Per un elenco completo delle etichette disponibili e per le definizioni per ciascun tipo di etichetta, consultare la guida sulle etichette [di utilizzo dei dati](labels/reference.md) supportate.

Le etichette possono essere applicate in qualsiasi momento, fornendo la flessibilità nella modalità di gestione dei dati. Le best practice incoraggiano l&#39;etichettatura dei dati non appena vengono trasferiti  Experience Platform, o non appena i dati diventano disponibili in Platform.

Per ulteriori informazioni, vedere la panoramica sulle etichette [di utilizzo dei](./labels/overview.md) dati.

## Criteri di utilizzo dei dati

Affinché le etichette di utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare dei criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o da cui è consentito eseguire attività sui dati all&#39;interno  Experience Platform.

Un esempio di un&#39;azione di marketing potrebbe essere il desiderio di esportare un dataset in un servizio di terze parti. Se è presente un criterio che indica che tipi specifici di dati, come Informazioni personali (PII), non possono essere esportati e che al set di dati è stata applicata un&#39;etichetta &quot;I&quot; (Dati identità), riceverete una risposta dal Servizio criteri in cui viene indicato che è stata violata una policy di utilizzo dei dati.

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono creare criteri utilizzando l&#39;API DULE Policy Service o l&#39;interfaccia utente  Experience Platform.

>[!IMPORTANT] Tutti i criteri di utilizzo dei dati (inclusi i criteri di base forniti da Adobe) sono disattivati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l&#39;applicazione, è necessario abilitare manualmente tale criterio.

Per ulteriori informazioni sui criteri di utilizzo dei dati e sulle azioni di marketing, consulta la panoramica [dei](./policies/overview.md)criteri.

## Versioni future

La governance dei dati supporta attualmente l&#39;etichettatura DULE a due livelli (dataset e campo). La governance dei dati supporta anche la creazione e la gestione di criteri di utilizzo dei dati e azioni di marketing tramite l&#39;API di DULE Policy Service.

Le versioni successive forniranno le seguenti funzionalità:

* Etichette di utilizzo dati personalizzate: Crea nuove etichette e definizioni in base alle esigenze aziendali.
* Applicazione delle regole: Utilizza il framework del criterio per consigliare e applicare criteri tra diversi pattern di accesso ai dati.
* Verifica: Monitora le attività di accesso ai dati e individua e segnala i problemi di conformità.

## Passaggi successivi

Questo documento ha fornito un&#39;introduzione di alto livello alla governance dei dati e al quadro DULE. Potete ora continuare a visualizzare la guida [utente delle etichette di utilizzo dei](labels/user-guide.md) dati e iniziare ad aggiungere etichette di utilizzo ai dati dell&#39;esperienza.

## Appendice

La sezione seguente fornisce ulteriori informazioni sulla governance dei dati.

### Terminologia di governance dei dati

La tabella seguente delinea i termini chiave relativi alla governance dei dati e al quadro DULE.

| Termine | Definizione |
|---|---|
| **Etichette contratto** | Le etichette &quot;C&quot; del contratto sono utilizzate per classificare i dati che hanno obblighi contrattuali o che sono correlati alle politiche di governance dei dati della tua organizzazione. |
| **Dati intersito** | I dati intersito sono la combinazione di dati provenienti da diversi siti, tra cui una combinazione di dati on-site e dati off-site o una combinazione di dati provenienti da diverse fonti off-site. |
| **Governance dei dati** | La governance dei dati comprende le strategie e le tecnologie utilizzate per garantire che i dati siano conformi alle normative e alle politiche aziendali in materia di utilizzo dei dati. |
| **Amministratori dati** | L&#39;amministratore dei dati è la persona responsabile della gestione, della sorveglianza e dell&#39;esecuzione delle risorse di dati di un&#39;organizzazione. Un amministratore dei dati garantisce inoltre che le politiche di governance dei dati siano salvaguardate e mantenute in conformità con le normative e le politiche di organizzazione governative. |
| **Etichette di utilizzo dati** | Le etichette di utilizzo dei dati consentono agli utenti di classificare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali in modo da essere conformi alle normative e alle politiche aziendali. |
| **Etichette set di dati** | Le etichette possono essere aggiunte a un set di dati. Tutti i campi all&#39;interno di un dataset ereditano le etichette del dataset. |
| **DULE** | DULE è un acronimo di &quot;Etichettatura e applicazione dell&#39;uso dei dati&quot;. Una parte chiave della governance dei dati, DULE è una raccolta di funzioni che consente l&#39;etichettatura dell&#39;uso dei dati e l&#39;applicazione di criteri di accesso ai dati per esigenze di governance all&#39;interno di un&#39;organizzazione. |
| **Etichette dei campi** | Le etichette dei campi sono etichette di governance dei dati ereditate da un set di dati o applicate direttamente a un campo.  Le etichette di governance dei dati applicate a un campo non vengono ereditate fino a un dataset. |
| **Geofence** | Una geofence è un limite geografico virtuale, definito dalla tecnologia GPS o RFID, che consente al software di attivare una risposta quando un dispositivo mobile entra o esce da un&#39;area particolare. |
| **Etichette identità** | Le etichette di identità &quot;I&quot; vengono utilizzate per classificare i dati in grado di identificare o contattare una persona specifica. |
| **Targeting basato su interessi** | Il targeting basato sugli interessi, noto anche come personalizzazione, si verifica se sono soddisfatte tre condizioni: i dati raccolti sul sito vengono utilizzati per ricavare deduzioni sull&#39;interesse degli utenti, in un altro contesto, ad esempio in un altro sito o in un&#39;altra app (fuori sito), e vengono utilizzati per selezionare il contenuto o gli annunci che vengono serviti in base a tali inferenze. |
| **Azione marketing** | Un&#39;azione di marketing, nel contesto del framework di governance dei dati, è un&#39;azione che un consumatore di dati Experience Platform  esegue, per la quale è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati |
| **Criterio** | Nel framework di governance dei dati, un criterio è una regola che descrive il tipo di azioni di marketing consentite o non consentite per dati specifici. |
| **Etichette sensibili** | Le etichette &quot;S&quot; sensibili vengono utilizzate per classificare i dati che voi e la vostra organizzazione considerate sensibili. |

## Risorse aggiuntive

Il seguente video è stato realizzato per illustrare la governance dei dati e illustrare gli aspetti chiave del framework DUE (Data Usage Labelling and Enforcement, Etichettatura e applicazione dell’uso dei dati).

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)
