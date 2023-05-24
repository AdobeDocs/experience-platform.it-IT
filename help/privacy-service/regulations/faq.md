---
keywords: Experience Platform;home;argomenti popolari;RGPD;RGPD;CCPA;PDPA;pdpa;LGPD;lgpd;faq;FAQ;regulation;regulation;regulations;Regulations;privacy;Privacy;
solution: Experience Platform
title: Domande frequenti sulle normative sulla privacy
description: Questo documento fornisce le risposte alle domande più frequenti sulle normative legali sulla privacy supportate e sulla loro implementazione in Adobe Experience Cloud.
exl-id: ec553e53-664b-4e18-abb1-4e4063fdd2c9
source-git-commit: 7e86721f6dd6fd280ae7e7e67aca21b4258ffb66
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 0%

---

# Domande frequenti sulle normative sulla privacy

Questo documento fornisce le risposte alle domande più frequenti sulle normative legali sulla privacy supportate e sulla loro implementazione in Adobe Experience Cloud.

>[!NOTE]
>
>Le definizioni dei vari termini utilizzati nel presente documento sono reperibili nella [terminologia delle normative sulla privacy](terminology.md) guida.

## Domande generali

Le seguenti domande si riferiscono a tutte le normative sulla privacy supportate dall’Experience Cloud.

### Quali sono gli effetti delle normative sulla privacy supportate?

Il [normative sulla privacy supportate dall’Experience Cloud](./overview.md) si applica a tutte le organizzazioni che memorizzano ed elaborano i dati personali dei cittadini all&#39;interno delle rispettive giurisdizioni, indipendentemente dalla posizione geografica dell&#39;organizzazione.

### Cosa costituiscono i dati personali?

Per dati personali si intende qualsiasi informazione correlata a una persona fisica o a una persona interessata che può essere usata per identificare direttamente o indirettamente la persona. Può essere qualsiasi cosa, da un nome, una foto, un indirizzo e-mail, dati bancari, post su siti di social networking, informazioni mediche, o un indirizzo IP del computer.

I seguenti identificatori sono comunemente utilizzati nelle applicazioni Experience Cloud e potrebbero essere soggetti ai requisiti della normativa sulla privacy:

* Nome
* Indirizzo postale
* Identificatore personale univoco
* Identificatore online
* Indirizzo IP
* Indirizzo e-mail
* Nome account

Le informazioni personali possono includere anche informazioni su Internet o su altre reti elettroniche. Ciò include, ma non è limitato a:

* Cronologia esplorazioni
* Cronologia ricerche
* Informazioni relative all’interazione di un consumatore con un sito web, un’applicazione o un annuncio pubblicitario

Anche se le normative sulla privacy coprono un&#39;ampia serie di informazioni personali, i termini contrattuali standard di Adobe impongono che le informazioni personali sensibili (come SSN, informazioni sulla patente di guida, informazioni finanziarie sul conto e dati biometrici) siano generalmente vietate dall&#39;importazione e dall&#39;uso in applicazioni di Experience Cloud.

### Qual è la differenza tra un titolare del trattamento e un responsabile del trattamento dei dati?

A **titolare del trattamento** è l&#39;entità che determina le finalità, le condizioni e i mezzi del trattamento dei dati personali, mentre **elaboratore dati** è un’entità che tratta dati personali per conto del titolare del trattamento.

A **titolare del trattamento** è la persona o l’organizzazione che ha il potere e la responsabilità di prendere decisioni in merito alla raccolta, all’utilizzo o alla divulgazione di dati personali. A **elaboratore dati** è la persona o l’organizzazione che opera in relazione alla raccolta, all’utilizzo o alla divulgazione dei dati personali e alla direzione del titolare del trattamento.

### Qual è la differenza tra consenso esplicito e non ambiguo dell’interessato?

**Consenso esplicito** si riferisce a uno standard di consenso che implica un&#39;indicazione specifica, informata e inequivocabile, orale o scritta, dei desideri dell&#39;interessato. In parole povere, la persona interessata deve letteralmente ed esplicitamente dire &quot;Io consenso&quot; o &quot;Io accetto&quot; affinché il consenso possa essere considerato esplicito. Inoltre, la revoca del consenso deve essere tanto facile quanto la sua concessione.

**Consenso univoco (implicito)** si riferisce al consenso che non è stato dato esplicitamente dalla persona interessata, ma è comunque di natura inequivocabile. Ad esempio, durante il processo di iscrizione al sito web di un’azienda, viene comunicato che fornendo un indirizzo e-mail, l’interessato acconsente alla ricezione di e-mail su offerte speciali. Se l’interessato legge l’avviso, l’azione positiva consistente nell’inserire l’e-mail è sufficiente per essere considerata un consenso inequivocabile.

Per molte normative come il RGPD è necessario il consenso esplicito per il trattamento dei dati personali sensibili, dove è sufficiente il solo consenso esplicito. Per i dati non sensibili, tuttavia, è accettabile un consenso inequivocabile (implicito).

### Le persone interessate al di sotto di una certa età possono dare il consenso?

Molte normative sulla privacy stabiliscono che se una persona interessata ha meno di una certa età, non può legalmente fornire il consenso per la raccolta dei suoi dati personali. In questi casi alcune normative consentono al titolare della responsabilità genitoriale di fornire il consenso per la persona interessata, ma non tutte. Nella tabella seguente è indicata l’età minima entro la quale le persone interessate devono fornire il proprio consenso per ciascun regolamento, con note per ulteriori informazioni:

| Regolamento | Età del consenso | Note |
| --- | --- | --- |
| CCPA (California) | 16 | <ul><li>Il consenso dei genitori può essere fornito solo per le persone interessate di almeno 13 anni di età.</li><li>La raccolta di dati personali da soggetti di età inferiore a 13 anni è severamente vietata.</li></ul> |
| RGPD (Unione europea) | 16 | <ul><li>Alcuni Stati membri dell&#39;UE possono prevedere a tal fine una legge per un&#39;età inferiore, ma non inferiore a 13 anni.</li><li>Il consenso dei genitori deve essere fornito a tutte le persone interessate al di sotto del limite di età.</li></ul> |
| LGPD (Brasile) | 13 | <ul><li>Il consenso dei genitori deve essere fornito a tutte le persone interessate al di sotto del limite di età.</li><li>Il consenso può essere dato da una persona fisica di età compresa tra i 13 e i 18 anni, purché il trattamento dei suoi dati personali sia effettuato nel loro interesse superiore.</li></ul> |
| PDPA (Thailandia) | 10 | <ul><li>Il consenso dei genitori deve essere fornito a tutte le persone interessate al di sotto del limite di età.</li></ul> |

<!-- | New Zealand [!DNL Privacy Act] | 16 | <ul><li>Parental consent must be provided for all data subjects below the age limit in cases where consent is required.</li></ul> | -->

### Quanti giorni deve un&#39;azienda rispondere a una richiesta del consumatore di accedere o cancellare informazioni personali?

Supponendo che l’azienda abbia raccolto informazioni personali e che possa autenticare o verificare l’identità di un particolare consumatore, le normative sulla privacy consentono di rispettare una finestra temporale specifica per una richiesta del consumatore. La tabella che segue riassume gli intervalli di tempo applicabili a ciascun regolamento, con le note su alcune eccezioni:

>[!NOTE]
>
>I tempi di risposta in &quot;giorni&quot; riflettono i termini stabiliti da ciascuna normativa di regolamentazione per completare una richiesta dei consumatori.

| Regolamento | Intervallo temporale per la risposta | Note |
| --- | --- | --- |
| CCPA (California) | 45 giorni |  |
| RGPD (Unione europea) | 30 giorni | Se la richiesta è complessa o se la stessa persona interessata ha presentato numerose richieste, la richiesta può essere estesa a 60 giorni. |
| LGPD (Brasile) | 15 giorni |  |
| PDPA (Thailandia) | 30 giorni | Se una società non è in grado di rispondere alla richiesta di una persona interessata entro il periodo di conformità, essa disporrà di ulteriori 30 giorni dalla data in cui non è stata in grado di soddisfare la richiesta per rispondere per iscritto alla persona interessata. |

<!-- | New Zealand [!DNL Privacy Act] | 20 working days | | -->

### La mia azienda deve nominare un responsabile della protezione dei dati?

Se le operazioni sui dati dell’organizzazione rientrano nelle giurisdizioni legali del RGPD, LGPD o PDPA, devi nominare un responsabile della protezione dei dati (DPO) nei seguenti casi:

* La tua organizzazione è un&#39;autorità pubblica
* La tua organizzazione si impegna nel monitoraggio sistematico su larga scala
* La tua organizzazione si occupa dell’elaborazione su larga scala di dati personali sensibili.

>[!IMPORTANT]
>
>A differenza di altri regolamenti, il CCPA lo prevede come requisito. Tuttavia, si consiglia in genere che per mantenere la conformità in materia di privacy, un’azienda debba disporre di attività di monitoraggio dei dati individuali qualificate e l’archiviazione dei dati dei consumatori, nonché rispondere alle richieste dei clienti.

### Come posso supportare le richieste sulla privacy dei consumatori se mantengo i dati coperti dalle normative sulla privacy?

Dopo aver adottato le misure necessarie per autenticare i consumatori che rientrano nelle giurisdizioni legali appropriate, Adobe Experience Platform Privacy Service ti consente di inviare richieste sulla privacy dei consumatori ad applicazioni Experienci Cloud compatibili. Consulta la [[!DNL Privacy Service] panoramica](../home.md) per ulteriori informazioni. Per informazioni su come le tue applicazioni per Experienci Cloud possono soddisfare le richieste relative alla privacy, consulta la guida su [Applicazioni Privacy Service e Experience Cloud](../experience-cloud-apps.md).

>[!NOTE]
>
>Ulteriori indicazioni da parte dell’autorità di regolamentazione della California sono ancora disponibili per quanto riguarda i tipi di dati che possono essere richiesti ai consumatori in materia di privacy.

## Domande sul CCPA

Le seguenti domande riguardano specificamente il CCPA.

### In che modo i diversi ruoli e responsabilità del CCPA si applicano agli Experienci Cloud?

Secondo la definizione del CCPA, i seguenti ruoli si applicano ad Adobe e ai suoi clienti:

* I clienti Adobi (la parte che richiede la raccolta e l&#39;utilizzo delle informazioni personali dei residenti della California) sarebbero considerati **Aziende**.
* Adobe, nel suo ruolo di fornitura del servizio, sarebbe considerato **Provider di servizi**.

In qualità di fornitore di servizi, Adobe raccoglie ed elabora informazioni personali per conto dell&#39;azienda ed è contrattualmente vincolato a utilizzare tali informazioni solo per le finalità specifiche stabilite nell&#39;accordo.

Data questa relazione e il linguaggio contrattuale dell&#39;Adobe, la divulgazione all&#39;Adobe probabilmente non sarebbe considerata una &quot;vendita&quot; per la quale le aziende dovrebbero dare preavviso e richiedere il consenso.

Tuttavia, i servizi Adobe possono essere utilizzati per consentire alcuni trasferimenti di dati e di condivisione a terze parti. Questi trasferimenti di terze parti potrebbero essere considerati una &quot;vendita&quot; e per legge richiedono la divulgazione e il consenso. I clienti devono collaborare con il proprio consulente legale per valutare casi d’uso specifici e valutare i requisiti applicabili.

### Adobe offre altri strumenti che potrebbero essere utili per soddisfare i requisiti del CCPA?

Le applicazioni Adobe Experience Cloud forniscono funzioni di gestione e governance dei dati che possono essere utili per le esigenze di privacy delle aziende. Tra questi strumenti ci sono l’etichettatura dell’utilizzo dei dati, i controlli dell’accesso basati sui ruoli, l’offuscamento dell’IP e le funzionalità di hashing.

Adobe ha ricevuto diverse certificazioni relative alla propria privacy e alle pratiche di sicurezza, ad esempio una certificazione ISO 27001 e una convalida RGPD TrustArc.

## Domande sul RGPD

Le seguenti domande si riferiscono specificamente al RGPD.

### Qual è la differenza tra un regolamento e una direttiva?

A **regolamento** è un atto legislativo vincolante e deve essere applicato nella sua interezza in tutta l&#39;UE. A **direttiva** è un atto legislativo che stabilisce un obiettivo che tutti i paesi dell&#39;UE devono raggiungere, ma spetta ai singoli paesi decidere come farlo.

È importante notare che il RGPD è un regolamento, a differenza della legislazione precedente (la direttiva sulla protezione dei dati), che è una direttiva.

### In che modo il RGPD influisce sui criteri relativi alle violazioni dei dati?

Le normative proposte in materia di violazioni dei dati si riferiscono principalmente alle politiche di notifica delle aziende che sono state violate. Le violazioni dei dati che possono rappresentare un rischio per le persone devono essere notificate all&#39;autorità di protezione dei dati entro 72 ore e alle persone interessate senza indebito ritardo.

## Domande PDPA

Le seguenti domande riguardano specificamente il PDPA.

### Cosa costituiscono i dati personali sensibili?

Il PDPA prevede requisiti rigorosi per la raccolta e l&#39;archiviazione di dati personali sensibili che includono dati personali relativi a: origine razziale o etnica, opinioni politiche, credenze religiose o filosofiche, casellari giudiziari, appartenenze a sindacati, dati genetici, dati biometrici, cartelle cliniche, orientamento sessuale o preferenze.
