---
keywords: Experience Platform;home;argomenti popolari;RGPD;RGPD;CCPA;CCPA;PDPA;PDPA;LGPD;LGPD;lgpd;faq;FAQ;regolamento;regolamenti;regolamenti;privacy;privacy;
solution: Experience Platform
title: Domande frequenti sulle normative sulla privacy
description: Questo documento fornisce le risposte alle domande più frequenti sulle normative legali sulla privacy supportate e sulla loro implementazione in Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# Domande frequenti sulle normative sulla privacy

Questo documento fornisce le risposte alle domande più frequenti sulle normative legali sulla privacy supportate e sulla loro implementazione in Adobe Experience Cloud.

>[!NOTE]
>
>Le definizioni dei vari termini utilizzati in questo documento sono disponibili nella [terminologia normativa sulla privacy](terminology.md) guida.

## Domande generali

Le seguenti domande riguardano tutte le normative sulla privacy supportate dall&#39;Experience Cloud.

### Quali sono gli effetti delle normative sulla privacy supportate?

La [normative sulla privacy supportate dall&#39;Experience Cloud](./overview.md) si applica a tutte le organizzazioni che memorizzano e trattano i dati personali dei cittadini nelle rispettive giurisdizioni, indipendentemente dalla posizione geografica dell&#39;organizzazione.

### Cosa si intende per dati personali?

Per dati personali si intendono tutte le informazioni relative a una persona fisica o a una persona interessata che possono essere utilizzate per identificare direttamente o indirettamente la persona. Può essere qualsiasi cosa da un nome, una foto, un indirizzo e-mail, dettagli bancari, post su siti di social networking, informazioni mediche o un indirizzo IP del computer.

I seguenti identificatori sono comunemente utilizzati nelle applicazioni di Experience Cloud e potrebbero essere soggetti ai requisiti della normativa sulla privacy:

* Nome
* Indirizzo postale
* Identificatore personale univoco
* Identificatore online
* Indirizzo IP
* Indirizzo e-mail
* Nome account

Le informazioni personali possono includere anche informazioni su Internet o altre informazioni di attività della rete elettronica. Ciò include, tra l&#39;altro:

* Cronologia esplorazioni
* Cronologia ricerche
* Informazioni relative all&#39;interazione di un consumatore con un sito web, un&#39;applicazione o un annuncio

Anche se le normative sulla privacy coprono un ampio insieme di informazioni personali, le condizioni contrattuali standard dell&#39;Adobe stabiliscono che le informazioni personali sensibili (come SSN, le informazioni sulla patente di guida, le informazioni finanziarie e i dati biometrici) sono generalmente vietate dall&#39;importazione e dall&#39;uso nelle applicazioni di Experience Cloud.

### Qual è la differenza tra un titolare del trattamento e un responsabile del trattamento dei dati?

A **titolare dei dati** è l&#39;entità che determina le finalità, le condizioni e i mezzi del trattamento dei dati personali, mentre **elaboratore dati** è un’entità che tratta dati personali per conto del titolare del trattamento.

A **titolare dei dati** è la persona o l&#39;organizzazione che ha il potere e la responsabilità di prendere decisioni in merito alla raccolta, all&#39;uso o alla divulgazione dei dati personali. A **elaboratore dati** è la persona o l’organizzazione che opera in relazione alla raccolta, all’uso o alla divulgazione dei dati personali e alla direzione del titolare del trattamento.

### Qual è la differenza tra il consenso esplicito e non ambiguo delle persone interessate?

**Consenso esplicito** si riferisce a uno standard di consenso che comporta un&#39;indicazione specifica, informata e inequivocabile della volontà della persona interessata in forma orale o scritta. In parole povere, la persona interessata deve dire letteralmente ed esplicitamente &quot;Io acconsento&quot; o &quot;Io sono d&#39;accordo&quot; affinché il consenso sia considerato esplicito. Inoltre, il ritiro del consenso deve essere altrettanto semplice di quello che lo è.

**Consenso univoco (implicito)** si riferisce al consenso che non è stato dato esplicitamente dalla persona interessata, ma che è comunque di natura inequivocabile. Ad esempio, durante il processo di registrazione per un sito web aziendale, viene comunicato che, fornendo un indirizzo e-mail, l’interessato acconsente a ricevere e-mail su offerte speciali. Se l’interessato legge l’avviso, l’azione positiva di inserire l’e-mail è sufficiente per essere considerato un consenso non ambiguo.

Per molti regolamenti come il RGPD, è necessario un consenso esplicito per il trattamento dei dati personali sensibili, dove basta solo il &quot;consenso&quot;. Per i dati non sensibili, tuttavia, il consenso esplicito (implicito) è accettabile.

### I soggetti interessati sotto una certa età possono dare il loro consenso?

Molte normative sulla privacy stabiliscono che se una persona interessata è al di sotto di una certa età, non può fornire legalmente il consenso per la raccolta dei propri dati personali. Alcuni regolamenti consentono il consenso del titolare della responsabilità genitoriale per la persona interessata in questi casi, ma non tutti. La tabella seguente elenca l&#39;età minima per le persone interessate per fornire il proprio consenso per ogni regolamento, con note per ulteriori informazioni:

| Regolamento | Età del consenso | Note |
| --- | --- | --- |
| CCPA (California) | 16 | <ul><li>Il consenso dei genitori può essere fornito solo per i soggetti di età uguale o superiore a 13 anni.</li><li>La raccolta di dati personali da soggetti di età inferiore ai 13 anni è severamente vietata.</li></ul> |
| RGPD (Unione europea) | 16 | <ul><li>A tal fine, alcuni Stati membri dell&#39;UE possono prevedere una legge per un&#39;età INFERIORE, MA non INFERIORE A 13 ANNI.</li><li>Il consenso dei genitori deve essere fornito per tutte le persone interessate al di sotto del limite di età.</li></ul> |
| LGPD (Brasile) | 13 | <ul><li>Il consenso dei genitori deve essere fornito per tutte le persone interessate al di sotto del limite di età.</li><li>Il consenso può essere concesso da una persona fisica di età compresa tra i 13 e i 18 anni, a condizione che il trattamento dei loro dati personali sia trattato nel loro interesse superiore.</li></ul> |
| PDPA (Thailandia) | 10 | <ul><li>Il consenso dei genitori deve essere fornito per tutte le persone interessate al di sotto del limite di età.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Quanti giorni un&#39;azienda deve rispondere a una richiesta del consumatore per accedere o cancellare informazioni personali?

Presupponendo che l&#39;azienda abbia raccolto informazioni personali e possa autenticare o verificare l&#39;identità di un particolare consumatore, le normative sulla privacy consentono di rispettare un intervallo di tempo specifico per una richiesta del consumatore. La tabella seguente riassume i periodi di tempo applicabili per ciascun regolamento, con note su alcune eccezioni:

| Regolamento | Finestra di conformità | Note |
| --- | --- | --- |
| CCPA (California) | 45 giorni |  |
| RGPD (Unione europea) | 30 giorni | Se la richiesta è complessa o se numerose richieste sono state effettuate dalla stessa persona interessata, la richiesta può essere estesa a 60 giorni. |
| LGPD (Brasile) | 15 giorni |  |
| PDPA (Thailandia) | 30 giorni | Se un&#39;azienda non è in grado di rispondere alla richiesta dell&#39;interessato entro il periodo di conformità, l&#39;azienda avrà un ulteriore periodo di 30 giorni dalla data in cui non è stata in grado di soddisfare la richiesta di risposta scritta all&#39;interessato. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### La mia azienda deve nominare un responsabile della protezione dei dati?

Se le operazioni relative ai dati della tua organizzazione rientrano nelle giurisdizioni legali del RGPD, LGPD o PDPA, devi nominare un responsabile della protezione dei dati (DPO) nei seguenti casi:

* La tua organizzazione è un&#39;autorità pubblica
* La tua organizzazione effettua un monitoraggio sistematico su larga scala
* La tua organizzazione si impegna in un trattamento su larga scala di dati personali sensibili.

>[!IMPORTANT]
>
>A differenza di altri regolamenti, il CCPA lo definisce come un requisito. Tuttavia, si raccomanda generalmente che, per mantenere la conformità alla privacy, un&#39;azienda debba disporre di attività di monitoraggio individuale qualificate per la raccolta dei dati e l&#39;archiviazione dei dati dei consumatori, nonché rispondere alle richieste dei clienti.

### Come posso supportare le richieste sulla privacy dei consumatori se mantengo i dati coperti dalle normative sulla privacy?

Una volta effettuati i passaggi necessari per autenticare i consumatori che rientrano nelle giurisdizioni legali appropriate, Adobe Experience Platform Privacy Service ti consente di inviare le richieste sulla privacy dei consumatori ad applicazioni Experience Cloud compatibili. Consulta la sezione [[!DNL Privacy Service] panoramica](../home.md) per ulteriori informazioni. Per informazioni su come le applicazioni di Experience Cloud possono soddisfare le richieste sulla privacy, consulta la guida su [Applicazioni Privacy Service e Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>Sono ancora disponibili ulteriori orientamenti da parte dell&#39;autorità di regolamentazione della California in merito a quali tipi di dati sono idonei per le richieste sulla privacy dei consumatori.

## Domande CCPA

Le seguenti domande riguardano specificamente il CCPA.

### Come si applicano ad Experience Cloud i diversi ruoli e responsabilità del CCPA?

Come definito dal CCPA, i seguenti ruoli si applicano ad Adobe e ai suoi clienti:

* I clienti Adobi (la parte che richiede la raccolta e l&#39;uso di informazioni personali da parte dei residenti della California) saranno considerati come **Business**.
* L&#39;Adobe, nel suo ruolo di prestazione del servizio, sarebbe considerato un **Provider di servizi**.

In qualità di fornitore di servizi, Adobe raccoglie ed elabora le informazioni personali per conto dell&#39;Azienda ed è contrattualmente obbligato ad utilizzare tali informazioni solo per gli scopi specifici stabiliti nel contratto.

Considerata questa relazione e il linguaggio contrattuale Adobe, le informazioni all&#39;Adobe probabilmente non sarebbero considerate una &quot;vendita&quot; per la quale le imprese dovrebbero fornire un avviso e richiedere il consenso.

Tuttavia, i servizi Adobe possono essere utilizzati per consentire la condivisione e il trasferimento di determinati dati a terzi. Questi trasferimenti di terzi potrebbero essere considerati una &quot;vendita&quot; e richiedono legalmente la divulgazione e il consenso. I clienti devono collaborare con il proprio consulente legale per valutare casi d’uso specifici al fine di valutare i requisiti applicabili.

### L’Adobe offre altri strumenti utili per soddisfare i requisiti CCPA?

Le applicazioni Adobe Experience Cloud forniscono funzioni di gestione e governance dei dati che possono essere utili per le esigenze di privacy delle aziende. Tra questi strumenti ci sono l’etichettatura dell’utilizzo dei dati, i controlli dell’accesso basati su ruolo, l’offuscamento dell’IP e le funzionalità di hashing.

Adobe ha ricevuto diverse certificazioni sulle sue pratiche di privacy e sicurezza, come una certificazione ISO 27001 e una convalida RGPD TrustArc.

## Domande sul RGPD

Le seguenti domande riguardano specificamente il RGPD.

### Qual è la differenza tra un regolamento e una direttiva?

A **regolamento** è un atto legislativo vincolante e deve essere applicato nella sua interezza in tutta l&#39;UE. A **direttiva** è un atto legislativo che stabilisce un obiettivo che tutti i paesi dell&#39;UE devono raggiungere, ma spetta ai singoli paesi decidere come.

È importante notare che il RGPD è un regolamento, a differenza della precedente legislazione (la direttiva sulla protezione dei dati), che è una direttiva.

### In che modo il RGPD influisce sulla politica relativa alle violazioni dei dati?

Le proposte di regolamento relative alle violazioni dei dati riguardano principalmente le politiche di notifica delle imprese che sono state violate. Le violazioni dei dati che possono comportare rischi per le persone fisiche devono essere notificate all&#39;autorità preposta alla protezione dei dati entro 72 ore e alle persone interessate senza indebito ritardo.

## Domande sul PDPA

Le seguenti domande riguardano specificamente il PDPA.

### Cosa costituisce un dato personale sensibile?

Il PDPA prevede requisiti rigorosi per la raccolta e la conservazione di dati personali sensibili, compresi i dati personali relativi a: origine razziale o etnica, opinioni politiche, credenze religiose o filosofiche, casellari giudiziari, appartenenze sindacali, dati genetici, dati biometrici, cartelle cliniche e orientamento o preferenze sessuali.
