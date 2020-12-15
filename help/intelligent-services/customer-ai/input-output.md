---
keywords: Experience Platform;getting started;customer ai;popular topics;customer ai input;customer ai output
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Ingresso e uscita AI del cliente
topic: Getting started
description: Il seguente documento delinea i diversi input e output utilizzati nell'AI del cliente.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# Ingresso e uscita AI del cliente

Il seguente documento delinea i diversi input e output utilizzati nell&#39;AI del cliente.

## Dati di input AI del cliente

L&#39;AI del cliente utilizza i dati Evento esperienza cliente per calcolare i punteggi di propensione. Per ulteriori informazioni su Consumer Experience Event, consulta la sezione [Prepara dati per l&#39;utilizzo nella documentazione](../data-preparation.md)dei servizi intelligenti.

### Dati storici

L&#39;AI del cliente richiede dati storici per la formazione dei modelli, ma la quantità di dati richiesta è basata su due elementi chiave: finestra dei risultati e popolazione ammissibile.

Per impostazione predefinita, l&#39;API del cliente cerca che un utente abbia avuto attività negli ultimi 120 giorni, se durante la configurazione dell&#39;applicazione non viene fornita alcuna definizione di popolazione idonea. Inoltre, l&#39;AI del cliente richiede un minimo di 500 eventi idonei e 500 non qualificati (1000 totali) di dati storici basati su una definizione dell&#39;obiettivo prevista.

Gli esempi seguenti hanno fornito una semplice formula per determinare la quantità minima di dati richiesti. Se il requisito minimo è superiore, è probabile che il modello fornisca risultati più precisi. Se la quantità minima richiesta è inferiore, il modello non riuscirà in quanto non è disponibile una quantità sufficiente di dati per la formazione dei modelli.

**Formula**:

Lunghezza minima dei dati richiesti = popolazione ammissibile + finestra dei risultati

>[!NOTE]
>
> 30 è il numero minimo di giorni richiesti per la popolazione ammissibile. Se non viene fornito, il valore predefinito è 120 giorni.

Esempi :

- Si desidera prevedere se è probabile che un cliente acquisti un orologio nei prossimi 30 giorni. Desiderate anche segnare gli utenti che hanno un&#39;attività Web negli ultimi 60 giorni. In questo caso la lunghezza minima dei dati richiesti = 60 giorni + 30 giorni. La popolazione ammissibile è di 60 giorni e la finestra di risultato è di 30 giorni per un totale di 90 giorni.

- Si desidera prevedere se è probabile che l&#39;utente acquisti un orologio nei prossimi 7 giorni. In questo caso la lunghezza minima dei dati richiesti = 120 giorni + 7 giorni. Il valore predefinito della popolazione ammissibile è 120 giorni e la finestra di risultato è di 7 giorni per un totale di 127 giorni.

- Si desidera prevedere se è probabile che il cliente acquisti un orologio nei prossimi 7 giorni. Desiderate anche segnare gli utenti che hanno un&#39;attività Web negli ultimi 7 giorni. In questo caso la lunghezza minima dei dati richiesti = 30 giorni + 7 giorni. La popolazione ammissibile ha bisogno di almeno 30 giorni e il periodo finale è di 7 giorni per un totale di 37 giorni.

Oltre ai dati minimi richiesti, anche l&#39;API del cliente funziona meglio con i dati recenti. In questo caso d&#39;uso, l&#39;AI cliente sta facendo una previsione per il futuro sulla base dei dati comportamentali recenti di un utente. In altre parole, dati più recenti produrranno probabilmente una previsione più accurata.

## Dati di output AI del cliente

L&#39;AI del cliente genera diversi attributi per i singoli profili ritenuti idonei. Esistono due modi per consumare il punteggio in base al provisioning eseguito. Se il profilo cliente in tempo reale è abilitato per il set di dati, puoi utilizzarlo tramite il profilo cliente in tempo reale. Se non hai il profilo cliente in tempo reale puoi scaricare il set di dati di output AI del cliente disponibile sul lago dati.

>[!NOTE]
>
>I valori di output sono utilizzati dal profilo cliente in tempo reale, che può essere utilizzato per creare e definire segmenti.

La tabella seguente descrive i vari attributi rilevati nell&#39;output dell&#39;AI cliente:

| Attributo | Descrizione |
| ----- | ----------- |
| Punteggio | La probabilità relativa che un cliente raggiunga l&#39;obiettivo previsto entro il periodo di tempo definito. Questo valore non deve essere trattato come una percentuale di probabilità, ma piuttosto come la probabilità di un individuo rispetto alla popolazione complessiva. Questo punteggio va da 0 a 100. |
| Probabilità | Questo attributo è la vera probabilità di un profilo per raggiungere l&#39;obiettivo previsto entro il periodo di tempo definito. Quando si confrontano gli output tra obiettivi diversi, si consiglia di considerare la probabilità rispetto al percentile o al punteggio. La probabilità dovrebbe sempre essere utilizzata per determinare la probabilità media tra la popolazione ammissibile, in quanto la probabilità tende a essere sul lato inferiore per gli eventi che non si verificano frequentemente. I valori per l’intervallo di probabilità sono compresi tra 0 e 1. |
| Percentile | Questo valore fornisce informazioni sulle prestazioni di un profilo rispetto ad altri profili con punteggio simile. Ad esempio, un profilo con un grado percentile pari a 99 per il churn indica che il rischio di esecuzione è maggiore rispetto al 99% di tutti gli altri profili con punteggio. Le percentuali sono comprese tra 1 e 100. |
| Tipo tendenza | Il tipo di propensione selezionato. |
| Data punteggio | Data in cui si è verificato il punteggio. |
| Fattori di influenza | Motivi previsti sul motivo per cui un profilo può essere convertito o churn. I fattori sono formati dai seguenti attributi:<ul><li>Codice: L&#39;attributo di profilo o di comportamento che influenza positivamente il punteggio previsto di un profilo. </li><li>Valore: Il valore dell&#39;attributo di profilo o di comportamento.</li><li>Importanza: Indica il peso dell&#39;attributo di profilo o di comportamento sul punteggio previsto (basso, medio, alto)</li></ul> |

## Passaggi successivi {#next-steps}

Dopo aver preparato i dati e avere a disposizione tutte le credenziali e gli schemi, inizia seguendo la guida [Configura un&#39;istanza](./user-guide/configure.md) AI del cliente. Questa guida illustra come creare un&#39;istanza per l&#39;AI cliente.