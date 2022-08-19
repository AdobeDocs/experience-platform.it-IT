---
title: Punteggio predittivo di lead e account in Real-time CDP B2B
type: Documentation
description: Panoramica e ulteriori informazioni sulla funzione di valutazione predittiva del lead e del conto in Experience Platform CDP B2B.
source-git-commit: 5ac8e099a6de563371f9a53a8b4816e6cf4d1953
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 2%

---

# Punteggio predittivo di lead e account in Real-time CDP B2B

Gli esperti di marketing B2B devono affrontare diverse sfide nella parte superiore del funnel di marketing. Per essere efficace, gli esperti di marketing B2B hanno bisogno di un modo automatizzato per qualificare un gran numero di persone in modo che possano concentrarsi sugli obiettivi di alto valore. La qualifica deve essere allineata con il risultato finale delle vendite, non solo con la conversione del marketing.

I conti sono le entità finali che acquistano prodotti e servizi B2B. Per commercializzare e vendere in modo efficace, gli esperti di marketing B2B devono conoscere non solo la probabilità di acquisto dei singoli, ma anche del conto.

Marketing basato su account, in particolare, stratega gli account come target di marketing. I punteggi di propensione all’acquisto dell’account aiutano notevolmente gli esperti di marketing B2B a dare priorità tra i conti al fine di massimizzare il loro ritorno sull’investimento.

Il servizio di valutazione predittiva del lead e del conto risponde alle problematiche di cui sopra imparando dagli eventi di conversione della fase dell’opportunità e prevedendo la conversione e aggregando le attività delle persone a livello di account per produrre i punteggi del conto. I punteggi sono prontamente disponibili come campi personalizzati sui profili delle persone e dei profili degli account e possono essere facilmente inclusi come criteri dei segmenti per perfezionare il pubblico. I fattori più influenti sono disponibili anche a livello di aggregato e di unità per aiutare gli esperti di marketing B2B a comprendere meglio quali elementi hanno determinato i punteggi.

## Informazioni sul punteggio predittivo per lead e account {#how-it-works}

>[!NOTE]
>
>[!DNL Marketo] l’origine dati è attualmente necessaria in quanto è l’unica origine dati in grado di fornire gli eventi di conversione a livello di profilo persona.

Il Punteggio predittivo del lead e dell’account utilizza un metodo di apprendimento automatico basato sulla struttura (incremento casuale della foresta/del gradiente) per creare il modello di punteggio predittivo del lead.

Gli amministratori possono configurare più obiettivi di punteggio del profilo, denominati anche modelli, uno per ogni evento di conversione configurato, consentendo la generazione di punteggi separati per ciascun obiettivo configurato.

Il punteggio predittivo per lead e account supporta i seguenti tipi e campi di obiettivo di conversione:

| Tipo di obiettivo | Campi |
| --- | --- |
| `leadOperation.convertLead` | <ul><li>`leadOperation.convertLead.convertedStatus`</li><li>`leadOperation.convertLead.assignTo`</li></ul> |
| `opportunityEvent.opportunityUpdated` | <ul><li>`opportunityEvent.dataValueChanges.attributeName`</li><li>`opportunityEvent.dataValueChanges.newValue`</li><li>`opportunityEvent.dataValueChanges.oldValue`</li>Esempio: `opportunityEvent.dataValueChanges.attributeName` è `Stage` e `opportunityEvent.dataValueChanges.newValue` è `Contract`</ul> |

L’algoritmo prende in considerazione i seguenti attributi e dati di input:

* Profilo persona

| Campo XDM | Obbligatorio/facoltativo |
| --- | --- |
| `personComponents.sourceAccountKey.sourceKey` | Obbligatorio |
| `workAddress.country` | Facoltativo |
| `extSourceSystemAudit.createdDate` | Obbligatorio |
| `extendedWorkDetails.jobTitle` | Facoltativo |

>[!NOTE]
> 
>L&#39;algoritmo esamina solo `sourceAccountKey.sourceKey` nel gruppo di campi Persona:personaComponenti .

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

Sono supportati più modelli, con i seguenti limiti rigidi impostati:

* Ogni sandbox di produzione ha diritto a cinque modelli.
* Ogni sandbox di sviluppo ha diritto a un modello.

I requisiti di qualità dei dati sono i seguenti:

* Idealmente esistono due anni dei dati più recenti a fini di formazione.
* La lunghezza minima dei dati richiesti è di sei mesi più la finestra di previsione.
* Per ogni obiettivo di previsione, sono necessari almeno 10 eventi di conversione qualificati.

I lavori di valutazione vengono eseguiti quotidianamente e i risultati vengono salvati come attributi di profilo e attributi di account, che possono quindi essere utilizzati nelle definizioni dei segmenti e nella personalizzazione. Le informazioni analitiche pronte all’uso sono disponibili anche nel dashboard di panoramica dell’account.

Consulta la documentazione per ulteriori informazioni su come [gestire il punteggio predittivo lead e account](/help/rtcdp/b2b-ai-ml-services/manage-predictive-lead-and-account-scoring.md) servizio.

## Visualizza i risultati del punteggio predittivo per lead e account {#how-to-view}

Dopo l&#39;esecuzione del processo, i risultati vengono salvati in un nuovo set di dati di sistema per ogni modello sotto il nome `LeadsAI.Scores` - ***il nome del punteggio***. Ogni gruppo di campi punteggio può essere posizionato in `{CUSTOM_FIELD_GROUP}.LeadsAI.the_score_name`.

| Attributo | Descrizione |
| --- | --- |
| Punteggio | La probabilità relativa che un profilo raggiunga l’obiettivo previsto entro l’intervallo di tempo definito. Questo valore non deve essere trattato come una percentuale di probabilità, ma piuttosto come la probabilità di un profilo rispetto alla popolazione complessiva. Questo punteggio va da 0 a 100. |
| Percentile | Questo valore fornisce informazioni sulle prestazioni di un profilo rispetto ad altri profili con punteggio simile. Le percentuali sono comprese tra 1 e 100. |
| Tipo di modello | Il tipo di modello selezionato indica se si tratta di un punteggio di persona o account. |
| Data punteggio | Data in cui si è verificato il punteggio. |
| Fattori influenti | Motivi previsti sul motivo per cui è probabile la conversione di un profilo. I fattori sono formati dai seguenti attributi:<ul><li>Codice: Il profilo o l’attributo comportamentale che influenza positivamente il punteggio previsto di un profilo.</li><li>Valore: Il valore dell’attributo di profilo o di comportamento.</li><li>Importanza: Indica il peso del profilo o dell’attributo comportamentale sul punteggio previsto (basso, medio, alto).</li></ul> |

### Visualizzare i punteggi del profilo cliente

Per visualizzare i punteggi predittivi per un profilo di persona, seleziona **[!UICONTROL Profili]** nella sezione cliente del pannello a sinistra, quindi immetti lo spazio dei nomi identità e il valore identity. Al termine, seleziona **[!UICONTROL Visualizza]**.

Quindi, seleziona il profilo dall’elenco.

![Profilo del cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile.png)

La **[!UICONTROL Dettaglio]** la pagina ora include i punteggi predittivi. Fai clic sull’icona del grafico accanto al punteggio predittivo.

![Punteggio predittivo del profilo cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score.png)

Una finestra di dialogo a comparsa mostra il punteggio, la distribuzione complessiva del punteggio, i principali fattori influenti per questo punteggio e la definizione dell&#39;obiettivo del punteggio.

![Dettagli del punteggio predittivo del profilo cliente](/help/rtcdp/accounts/images/b2b-view-customer-profile-predictive-score-details.png)

## Monitoraggio dei processi di valutazione predittivi dei lead e dei conti {#monitoring-jobs}

Puoi monitorare le metriche di base e lo stato giornaliero dell’esecuzione dei processi attraverso il dashboard. Le metriche includono:

* Totale profili persona/account valutati
* Processo di punteggio successivo (data)
* Lavoro di formazione successivo (data)

Per ulteriori informazioni, consulta la documentazione su [monitoraggio dei processi per il punteggio predittivo lead e account](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
