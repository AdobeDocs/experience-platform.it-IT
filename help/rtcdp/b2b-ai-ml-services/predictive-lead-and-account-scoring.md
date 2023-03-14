---
title: Punteggio predittivo di lead e account in Real-Time CDP B2B
type: Documentation
description: Panoramica e ulteriori informazioni sulla funzione di punteggio predittivo di lead e account in Experience Platform CDP B2B.
exl-id: d3afbabb-005d-4537-831a-857c88043759
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# Punteggio predittivo di lead e account in Real-Time CDP B2B

Gli esperti di marketing B2B si trovano ad affrontare diverse sfide nella parte superiore del funnel di marketing. Per essere efficaci, gli esperti di marketing B2B hanno bisogno di un modo automatizzato per qualificare un numero elevato di persone in modo che possano concentrarsi sui target di alto valore. La qualifica deve essere allineata con il risultato finale delle vendite, non solo con la conversione marketing.

I conti sono le entità finali che acquistano prodotti e servizi B2B. Per commercializzare e vendere in modo efficace, gli addetti al marketing B2B devono conoscere non solo la probabilità di acquistare dell’individuo, ma anche quella dell’account.

Il marketing basato sull’account, in particolare, definisce gli account come obiettivi di marketing. I punteggi relativi alla propensione all’acquisto dell’account aiutano notevolmente gli esperti di marketing B2B a stabilire la priorità tra gli account in modo da massimizzare il ritorno sull’investimento.

Il servizio di predictive lead and account scoring affronta le sfide di cui sopra apprendendo e prevedendo gli eventi di conversione della fase dell’opportunità e aggregando le attività delle persone a livello di account per produrre i punteggi dell’account. I punteggi sono prontamente disponibili come campi personalizzati sui profili delle persone e degli account e possono essere facilmente inclusi come criteri di segmento per perfezionare il pubblico. I principali fattori influenti sono disponibili anche a livello aggregato e di unità per aiutare gli esperti di marketing B2B a comprendere meglio quali elementi hanno guidato i punteggi.

## Informazioni sul punteggio predittivo di lead e account {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] l’origine dati è attualmente richiesta in quanto è l’unica origine dati in grado di fornire gli eventi di conversione a livello di profilo della persona.

Il punteggio predittivo di lead e account utilizza un metodo di apprendimento automatico basato su albero (aumento casuale di foresta/gradiente) per creare il modello di punteggio predittivo di lead.

Gli amministratori possono configurare più obiettivi di punteggio di profilo, o modelli, uno per ogni evento di conversione configurato, consentendo la generazione di punteggi separati per ogni obiettivo configurato.

Il punteggio predittivo di lead e account supporta i seguenti tipi e campi di obiettivo di conversione:

| Tipo di obiettivo | Campi |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Esempio: `opportunityEvent.dataValueChanges.attributeName` è uguale a `Stage` e `opportunityEvent.dataValueChanges.newValue` è uguale a `Contract`</ul> |

L’algoritmo prende in considerazione i seguenti attributi e dati di input:

* Profilo della persona

| Campo XDM | Obbligatorio/facoltativo |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Obbligatorio |
| `workAddress.country` | Facoltativo |
| `extSourceSystemAudit.createdDate` | Obbligatorio |
| `extendedWorkDetails.jobTitle` | Facoltativo |

>[!NOTE]
> 
>L’algoritmo controlla solo `sourceAccountKey.sourceKey` nel gruppo di campi Persona:componentiPersona.

* Profilo account

| Campo XDM | Obbligatorio/facoltativo |
| --- | --- |
| `accountKey.sourceKey` | Obbligatorio |
| `extSourceSystemAudit.createdDate` | Obbligatorio |
| `accountOrganization.industry` | Facoltativo |
| `accountOrganization.numberOfEmployees` | Facoltativo |
| `accountOrganization.annualRevenue.amount` | Facoltativo |

* Evento esperienza

| Campo XDM | Obbligatorio/facoltativo |
| --- | --- |
| `_id` | Obbligatorio |
| `personKey.sourceKey` | Obbligatorio |
| `timestamp` | Obbligatorio |
| `eventType` | Obbligatorio |

Sono supportati più modelli, con i seguenti limiti fissi impostati:

* Ogni sandbox di produzione ha diritto a cinque modelli.
* Ogni sandbox di sviluppo ha diritto a un modello.

I requisiti in materia di qualità dei dati sono i seguenti:

* Idealmente ci sono due anni di dati più recenti a scopo di formazione.
* La lunghezza minima dei dati richiesti è di sei mesi più la finestra di previsione.
* Per ogni obiettivo di previsione, sono necessari almeno 10 eventi di conversione qualificati.

I processi di assegnazione del punteggio vengono eseguiti quotidianamente e i risultati vengono salvati come attributi di profilo e attributi di conto, che possono quindi essere utilizzati nelle definizioni dei segmenti e nella personalizzazione. Le informazioni analitiche predefinite sono disponibili anche nella dashboard di panoramica dell’account.

Consulta la documentazione per ulteriori informazioni su come [gestire il punteggio predittivo di lead e account](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) servizio.

## Visualizzare i risultati predittivi del punteggio di lead e account {#how-to-view}

Dopo l’esecuzione del processo, i risultati vengono salvati in un nuovo set di dati di sistema per ciascun modello con il nome `LeadsAI.Scores` - ***il nome del punteggio***. Ogni gruppo di campi di punteggio può essere individuato in `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Attributo | Descrizione |
| --- | --- |
| Punteggio | La probabilità relativa che un profilo raggiunga l’obiettivo previsto entro l’intervallo di tempo definito. Questo valore non deve essere considerato come percentuale di probabilità, ma piuttosto la probabilità di un profilo rispetto alla popolazione complessiva. Questo punteggio è compreso tra 0 e 100. |
| Percentile | Questo valore fornisce informazioni sulle prestazioni di un profilo rispetto ad altri profili con punteggio simile. I percentili sono compresi tra 1 e 100. |
| Tipo di modello | Il tipo di modello selezionato indica se si tratta di un punteggio di persona o di account. |
| Data punteggio | Data in cui si è verificato il punteggio. |
| Fattori di influenza | Motivi previsti per la conversione di un profilo. I fattori sono costituiti dai seguenti attributi:<ul><li>Codice: il profilo o l’attributo comportamentale che influenza positivamente il punteggio previsto di un profilo.</li><li>Valore: il valore del profilo o dell’attributo comportamentale.</li><li>Importanza: indica il peso del profilo o dell’attributo comportamentale sul punteggio previsto (basso, medio, alto).</li></ul> |

### Visualizzare i punteggi del profilo cliente

Per visualizzare i punteggi predittivi di un profilo persona, seleziona **[!UICONTROL Profili]** nella sezione cliente del pannello a sinistra, quindi inserisci lo spazio dei nomi e il valore di identità. Al termine, seleziona **[!UICONTROL Visualizza]**.

Quindi, seleziona il profilo dall’elenco.

![Profilo cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

Il **[!UICONTROL Dettaglio]** La pagina ora include i punteggi predittivi. Fai clic sull’icona del grafico accanto al punteggio predittivo.

![Punteggio predittivo del profilo cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Una finestra di dialogo a comparsa mostra il punteggio, la distribuzione complessiva del punteggio, i principali fattori influenti per questo punteggio e la definizione dell’obiettivo del punteggio.

![Dettagli punteggio predittivo del profilo cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Monitoraggio dei processi predittivi di valutazione del lead e dell’account {#monitoring-jobs}

Puoi monitorare le metriche di base e lo stato dell’esecuzione giornaliera dei processi tramite la dashboard. Le metriche includono:

* Totale profili persona/account valutati
* Processo con punteggio successivo (data)
* Processo di formazione successivo (data)

Per ulteriori informazioni, consulta la documentazione su [monitoraggio dei processi per il punteggio predittivo di lead e account](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
