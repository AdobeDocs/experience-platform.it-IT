---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Domande frequenti su CCPA
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 0%

---


# Domande frequenti su CCPA

Questo documento contiene le risposte alle domande frequenti sull&#39; [!DNL California Consumer Protection Act] (CCPA) e sulla sua implementazione in Adobe Experience Cloud.

## Cos&#39;è l&#39;CCPA?

La [!DNL California Consumer Privacy Act] (CCPA) è la nuova legge sulla privacy californiana che conferisce ai propri residenti nuovi diritti in merito alle proprie informazioni personali e impone responsabilità in materia di protezione dei dati a determinate entità che svolgono attività commerciali in California.

>[!NOTE]
>
>Anche se tecnicamente efficace nel gennaio 2020, l&#39;CCPA è ancora messa a punto dai legislatori. Inoltre, importanti dettagli di attuazione e altri orientamenti sono disponibili nelle norme che devono ancora essere scritte dall&#39;autorità di regolamentazione della California.

Sebbene l’APP condivida alcuni concetti forniti dal Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) dell’Unione europea, come il diritto di accesso ed eliminazione dei dati personali, esistono diversi modi chiave in cui l’APP differisce dal GDPR. Ad esempio, l&#39;APP offre ai consumatori il diritto di non partecipare a determinate attività di condivisione dei dati che possono essere considerate come &quot;vendita&quot; di informazioni personali a terzi, piuttosto che richiedere il consenso preventivo.

## Qual è la definizione di informazioni personali nell&#39;ambito dell&#39;APP?

Le informazioni personali sono informazioni &quot;che identificano, si riferiscono, descrive, possono essere associate o ragionevolmente collegate, direttamente o indirettamente, con un consumatore o una famiglia&quot;.

## Quali tipi di informazioni personali o identificatori utilizzati in Adobe Experience Cloud sono soggetti a questi nuovi requisiti?

I seguenti identificatori sono comunemente utilizzati nelle [!DNL Experience Cloud] applicazioni e possono essere soggetti ai requisiti CCPA:

- Nome
- Indirizzo postale
- Identificatore personale univoco
- Identificatore online
- Indirizzo IP
- Indirizzo e-mail
- Nome account

Le informazioni personali possono anche includere informazioni su Internet o altre informazioni sulle attività della rete elettronica. Ciò include, ma non solo:

- Cronologia esplorazioni
- Cronologia ricerche
- Informazioni relative all&#39;interazione di un consumatore con un sito Web, un&#39;applicazione o un annuncio pubblicitario

Anche se l&#39;APP copre un&#39;ampia gamma di informazioni personali, le condizioni contrattuali standard di Adobe stabiliscono che le informazioni personali riservate (come SSN, informazioni sulla licenza del conducente, informazioni finanziarie e dati biometrici) sono generalmente vietate dall&#39;importazione e dall&#39;uso nelle [!DNL Experience Cloud] applicazioni.

## In che modo si applicano i diversi ruoli e responsabilità dell&#39;APP [!DNL Experience Cloud]?

Come definito da CCPA, i seguenti ruoli si applicano ad Adobe e ai suoi clienti:

- I clienti Adobe (la parte che richiede la raccolta e l&#39;uso di informazioni personali da parte di residenti della California) sarebbero considerati **Business**.
- Adobe, nel suo ruolo di fornitore del servizio, sarebbe considerato un **fornitore** di servizi.

Considerata questa relazione e la lingua del contratto di Adobe, le comunicazioni ad Adobe probabilmente non sarebbero considerate una &quot;vendita&quot; per la quale le aziende dovrebbero fornire un avviso e offrire una rinuncia.

Tuttavia, i servizi Adobe possono essere utilizzati per consentire la condivisione e il trasferimento di alcuni dati a terzi. Questi trasferimenti di terzi potrebbero essere considerati una &quot;vendita&quot; e legalmente richiedono la divulgazione e l&#39;opt-out.  I clienti devono collaborare con il proprio consulente legale per valutare casi di utilizzo specifici al fine di valutare i requisiti applicabili.

## Quanti giorni ha un&#39;azienda per rispondere a una richiesta del consumatore di accedere o cancellare informazioni personali?

Presupponendo che l&#39;azienda abbia raccolto informazioni personali e che possa autenticare o verificare l&#39;identità di un particolare consumatore californiano, l&#39;APP consente di soddisfare le richieste dei consumatori entro 45 giorni (con alcune eccezioni).

## Qual è il ruolo di Adobe nell&#39;ambito dell&#39;APP?

In qualità di fornitore di servizi, Adobe raccoglie ed elabora informazioni personali per conto dell&#39;Azienda ed è contrattualmente tenuta a utilizzarle solo per gli scopi specifici stabiliti nel contratto.

Considerata questa relazione e la lingua del contratto di Adobe, le comunicazioni ad Adobe rientrano nelle disposizioni della legge per i provider di servizi e probabilmente non saranno considerate una &quot;vendita&quot; per la quale le aziende dovrebbero fornire un avviso e offrire un&#39;opzione di rifiuto.

I servizi Adobe possono essere utilizzati per consentire la condivisione e il trasferimento di alcuni dati a terzi. Questi trasferimenti di terzi potrebbero essere considerati una &quot;vendita&quot; e legalmente richiedono la divulgazione e l&#39;opt-out.  I clienti devono collaborare con il proprio consulente legale per valutare casi di utilizzo specifici al fine di valutare i requisiti applicabili.

## Come posso supportare i requisiti sulla privacy dei consumatori in base all&#39;APP se mantengo certi tipi di dati coperti dai requisiti?

Una volta che avete adottato le misure necessarie per autenticare i consumatori CA,  Adobe Experience Platform [!DNL Privacy Service] consente di inviare le richieste di privacy dei consumatori alle [!DNL Experience Cloud] applicazioni compatibili. Per ulteriori informazioni, consultate la panoramica [di](../home.md) Privacy Service. Per informazioni su come [!DNL Experience Cloud] le applicazioni specifiche possono soddisfare le richieste di privacy, consultare la guida sulle applicazioni [](../experience-cloud-apps.md)Privacy Service e  Experience Cloud.

>[!NOTE]
>
>Ulteriori indicazioni da parte dell&#39;autorità di regolamentazione californiana sono ancora disponibili in merito a quali tipi di dati sono ammissibili per le richieste di privacy dei consumatori.

## Adobe offre altri strumenti utili per soddisfare i requisiti CCPA?

Le applicazioni Adobe Experience Cloud forniscono funzioni di gestione e governance dei dati utili per le esigenze di privacy delle aziende. Tra questi strumenti figurano l’etichettatura dell’utilizzo dei dati, i controlli di accesso basati su ruoli, l’offuscamento IP e le funzionalità di hashing.

Adobe ha ricevuto diverse certificazioni sulle pratiche relative alla privacy e alla sicurezza, come ad esempio una certificazione ISO 27001 e una convalida GDPR TrustArc.