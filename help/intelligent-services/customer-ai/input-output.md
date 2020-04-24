---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Guida introduttiva all'intelligenza artificiale
topic: Getting started
translation-type: tm+mt
source-git-commit: 3146442ed0638559ddd68452fd42cc5731b4dc8a

---


# Ingresso e uscita AI del cliente

Il seguente documento delinea i diversi input e output utilizzati nell&#39;AI del cliente.

## Dati di input AI del cliente

L&#39;AI del cliente utilizza i dati Evento esperienza cliente per calcolare i punteggi di propensione. Per ulteriori informazioni su Consumer Experience Event, consulta la sezione [Prepara dati per l&#39;utilizzo nella documentazione](../data-preparation.md)dei servizi intelligenti.

## Dati di output AI del cliente

L&#39;AI del cliente genera diversi attributi per i singoli profili ritenuti idonei. Esistono due modi per consumare il punteggio in base al provisioning eseguito. Se il profilo cliente in tempo reale è abilitato per il set di dati, puoi utilizzarlo tramite il profilo cliente in tempo reale. Se non hai il profilo cliente in tempo reale puoi scaricare il set di dati di output AI del cliente disponibile sul lago dati.

>[!NOTE]
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