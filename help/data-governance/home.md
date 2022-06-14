---
keywords: Experience Platform;home;argomenti popolari;DULE;dule
solution: Experience Platform
title: Panoramica sulla governance dei dati
topic-legacy: overview
description: La governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno dell’Experience Platform a vari livelli, tra cui catalogazione, derivazione dei dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing
exl-id: 00ca6bc2-1c58-4ea2-8bb5-30fd3fa5944a
source-git-commit: 0c78b5dc420a1346c92bf9ed7864fa1733422a83
workflow-type: tm+mt
source-wordcount: '1431'
ht-degree: 0%

---

# Panoramica sulla governance dei dati

Una delle funzionalità principali di Adobe Experience Platform è quella di unire i dati provenienti da più sistemi aziendali per consentire agli addetti al marketing di identificare, comprendere e coinvolgere meglio i clienti. Questi dati possono essere soggetti a restrizioni di utilizzo definite dalla tua organizzazione o da normative legali. È quindi importante assicurarsi che i dati operino entro [!DNL Platform] sono conformi ai criteri di utilizzo dei dati.

La governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. svolge un ruolo chiave all&#39;interno di [!DNL Experience Platform] a vari livelli, compresi catalogazione, derivazione dati, etichettatura dell’utilizzo dei dati, criteri di utilizzo dei dati e controllo dell’utilizzo dei dati per le azioni di marketing.

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

Gli addetti al marketing sono il punto finale della governance dei dati. Richiedono i dati dall&#39;infrastruttura di governance dei dati creata da amministratori di dati, scienziati e ingegneri. Gli addetti al marketing comprendono diverse specialità nell’ambito del marketing, tra cui:

* Gli analisti di marketing richiedono i dati per consentire la comprensione dei clienti, sia come individui che in gruppi (noti anche come segmenti).
* Gli esperti marketing e i designer di esperienze utilizzano i dati per progettare nuove esperienze cliente.


## Quadro di riferimento per la governance dei dati

Il framework per la governance dei dati semplifica e semplifica il processo di categorizzazione dei dati e creazione di criteri di utilizzo dei dati. Una volta applicate le etichette dei dati e stabiliti i criteri di utilizzo dei dati, è possibile valutare le azioni di marketing per garantire l’uso corretto dei dati.

Il framework per la governance dei dati presenta tre elementi chiave: Etichette, criteri e applicazione.

1. **Etichette:** Classificare i dati che riflettono considerazioni relative alla privacy e condizioni contrattuali conformi alle normative e ai criteri aziendali.
1. **Criteri:** Descrivi il tipo o i tipi di azioni di marketing consentiti o non consentiti per dati specifici.
1. **Applicazione:** Utilizza il framework dei criteri per consigliare e applicare le politiche in diversi schemi di accesso ai dati.

## Etichette di utilizzo dati

La governance dei dati consente agli amministratori dei dati di applicare etichette di utilizzo a livello di set di dati e di campi per classificare i dati in base al tipo di criteri applicabili.

Il framework per la governance dei dati include etichette di utilizzo dei dati predefinite che possono essere utilizzate per classificare i dati in tre modi:

![Categorie delle etichette per l&#39;utilizzo dei dati](./images/overview/label-categories.png)

* **Etichette dati &quot;C&quot; del contratto:** Etichettare e classificare i dati che hanno obblighi contrattuali o sono correlati ai criteri di governance dei dati dei clienti.
* **Etichette per i dati di identità &quot;I&quot;:** Etichettare e classificare i dati che possono identificare o contattare una persona specifica.
* **Etichette per i dati sensibili &quot;S&quot;:** Etichettare e classificare i dati relativi a dati sensibili, come i dati geografici.

>[!NOTE]
>
>Consulta la guida su [etichette di utilizzo dei dati supportate](labels/reference.md) per un elenco completo delle etichette disponibili, nonché delle definizioni per ciascun tipo di etichetta.

Le etichette possono essere applicate in qualsiasi momento, fornendo flessibilità nella scelta della modalità di gestione dei dati. Le best practice incoraggiano l’etichettatura dei dati non appena vengono acquisiti [!DNL Experience Platform], o non appena i dati diventano disponibili in [!DNL Platform].

Vedi la panoramica su [etichette di utilizzo dei dati](./labels/overview.md) per ulteriori informazioni.

## Criteri di utilizzo dei dati

Affinché le etichette per l’utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare i criteri per l’utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che ti sono consentite o a cui ti è impedito di eseguire sui dati all’interno di [!DNL Experience Platform].

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se esiste una politica che indica che le informazioni personali (PII) non possono essere esportate e un&#39;etichetta &quot;I&quot; (dati di identità) è stata applicata al set di dati, [!DNL Policy Service] impedisce qualsiasi azione che possa esportare il set di dati in una destinazione di terze parti. Se si verifica uno di questi tentativi di azione, il servizio criteri invia un messaggio che indica che è stato violato un criterio di utilizzo dei dati.

Sono disponibili due tipi di criteri:

* **[!UICONTROL Criteri di governance dei dati]**: Limita l’attivazione dei dati in base all’azione di marketing in corso e alle etichette di utilizzo dei dati in base ai dati in questione.
* **[!UICONTROL Criterio di consenso]**: Filtrare i profili a cui è possibile attivare [destinazioni](../destinations/home.md) in base al consenso o alle preferenze dei clienti.

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono creare i criteri utilizzando [!DNL Policy Service] o [!DNL Experience Platform] interfaccia utente. Per ulteriori informazioni sui criteri di utilizzo dei dati e sulle azioni di marketing, consulta la sezione [panoramica dei criteri](./policies/overview.md).

>[!IMPORTANT]
>
>Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l&#39;applicazione, è necessario abilitare manualmente tale criterio.

## Passaggi successivi

Questo documento fornisce un’introduzione di alto livello alla governance dei dati e al framework per la governance dei dati. Ora puoi continuare con la [guida utente delle etichette per l’utilizzo dei dati](labels/user-guide.md) e inizia ad aggiungere etichette di utilizzo ai dati dell’esperienza.

## Appendice

La sezione seguente fornisce ulteriori informazioni sulla governance dei dati.

### Terminologia sulla governance dei dati

La tabella seguente delinea i termini chiave relativi alla governance dei dati e al framework per la governance dei dati.

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
| **Azione di marketing** | Un’azione di marketing, nel contesto del framework di governance dei dati, è un’azione che [!DNL Experience Platform] dati acquisiti dal consumatore, per i quali è necessario verificare la presenza di violazioni dei criteri di utilizzo dei dati |
| **Criterio** | Nel framework di governance dei dati, una policy è una regola che descrive il tipo di azioni di marketing consentite o non consentite su dati specifici. |
| **Etichette sensibili** | Le etichette &quot;S&quot; sensibili vengono utilizzate per classificare i dati che tu e la tua organizzazione consideri sensibili. |

## Risorse aggiuntive

Il seguente video è pensato per aiutarti a comprendere il framework per la governance dei dati.

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&enable10seconds=on&speedcontrol=on)

Il video seguente fornisce un’introduzione alle varie funzioni di governance dei dati di Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&enable10seconds=on&speedcontrol=on)
