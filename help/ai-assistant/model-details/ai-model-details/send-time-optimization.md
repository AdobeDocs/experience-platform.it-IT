---
title: Dettagli del modello di ottimizzazione dell’ora di invio
description: Scopri il modello di intelligenza artificiale utilizzato per l’ottimizzazione dell’ora di invio in Adobe Journey Optimizer.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: 4c3f6ead150a2f793db92d2418df3177eba2d255
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Dettagli del modello di ottimizzazione dell’ora di invio

## Panoramica del modello {#model-overview}

* **Nome modello e versione**: ottimizzazione dell&#39;ora di invio
* **Data di rilascio modello**: settembre 2024
* **Scopo del modello**: il modello di ottimizzazione dell&#39;ora di invio di Adobe Journey Optimizer sceglie il tempo di invio ottimale per le e-mail e i messaggi push per massimizzare il coinvolgimento del consumatore, in base al comportamento storico di apertura e clic dei consumatori.
* **Utenti previsti**: gli utenti principali di questo modello sono professionisti del marketing, product manager e team di coinvolgimento dei clienti che sfruttano Adobe Journey Optimizer per promuovere strategie di marketing basate sui dati.
* **Casi d&#39;uso**: l&#39;ottimizzazione dell&#39;ora di invio è più indicata per le comunicazioni di marketing meno urgenti, ad esempio annunci settimanali, informazioni promozionali su un nuovo prodotto o informazioni su una vendita della durata di un mese. L’ottimizzazione dell’ora di invio è disponibile solo per i tipi di azione e-mail e push incorporati di Journey Optimizer e non è attualmente disponibile per i messaggi inviati tramite azioni personalizzate o per altri tipi di azione.
* **Possibile utilizzo improprio**: non utilizzare l&#39;ottimizzazione dell&#39;ora di invio per messaggi operativi urgenti e sensibili all&#39;ora, ad esempio una conferma di un ordine, una notifica di reimpostazione della password o una notifica di modifica del gate di volo.

## Dettagli modello {#model-details}

* **Tipo di modello**: il modello di ottimizzazione dell&#39;ora di invio acquisisce i dati sul comportamento del consumatore Adobe Journey Optimizer dell&#39;organizzazione e analizza gli eventi di apertura e clic a livello di utente per prevedere quando è più probabile che i consumatori interagiscano con i messaggi. Il comportamento di apertura e clic a livello di consumatore per ogni ora della settimana viene ponderato e combinato con il comportamento simile e complessivo del consumatore utilizzando uno stimatore [!DNL Bayesian]. Vengono quindi classificate le previsioni [!DNL Bayesian] per ogni ora della settimana, con conseguente &quot;mappa di calore&quot; per ogni metrica (aperture di e-mail, clic e aperture push), per ogni cliente, per prevedere le ore della settimana in cui è più e meno probabile che contattare ogni consumatore porti al risultato di coinvolgimento desiderato.
* **Input**: l&#39;ottimizzazione dell&#39;ora di invio utilizza i dati del fuso orario del consumatore nel campo `timeZone` all&#39;interno del gruppo di campi [!UICONTROL Dettagli preferenza], se forniti, per determinare il fuso orario di un consumatore. Se il fuso orario di un consumatore non è disponibile nel campo `timeZone`, l&#39;ottimizzazione dell&#39;ora di invio tenta di dedurre il fuso orario del consumatore, in base alla corrispondenza del fuso orario più comune al primo indirizzo postale trovato memorizzato nel profilo del consumatore utilizzando il tipo di dati dell&#39;indirizzo postale [&#128279;](../../../xdm/data-types/postal-address.md). L’ottimizzazione dell’ora di invio fa previsioni per ogni consumatore in base a tre tipi di dati comportamentali:
   * Il comportamento di apertura e clic dei consumatori in generale.
   * Il comportamento di apertura e clic dei consumatori simili nello stesso fuso orario.
   * Il comportamento di apertura e clic del singolo consumatore.
* **Output**: queste previsioni sono ponderate e combinate utilizzando un approccio [!DNL Bayesian], con conseguente &quot;mappa di calore&quot; per ogni metrica (aperture di e-mail, clic su e aperture push), che indica le ore della settimana in cui contattare il consumatore ha la maggiore e minore probabilità di produrre il risultato di coinvolgimento desiderato (apertura/clic), come illustrato nell&#39;esempio di mappa di calore seguente:

![Mappa di calore per l&#39;ottimizzazione dell&#39;ora di invio.](../../images/models/send-time-optimization.png)

* **Input e output di esempio**: per ridurre al minimo l&#39;impatto del modello sulla ricchezza del profilo, i punteggi del modello vengono memorizzati e compressi in tre attributi di profilo memorizzati in `_experience.intelligentServices.journeyAI.sendTimeOptimization` e non sono progettati per essere leggibili dall&#39;utente.

## Formazione sui modelli {#model-training}

* **Dati di formazione e pre-elaborazione**: il set di dati di formazione per ogni organizzazione proviene solo dai propri dati in Adobe Experience Platform.
   * Una volta abilitata la funzione di ottimizzazione dell’ora di invio per l’organizzazione, il modello viene addestrato agli eventi e-mail e push, di invio, apertura e clic in tutti i percorsi e le azioni dell’organizzazione nelle ultime 16 settimane, indipendentemente dal fatto che tali azioni utilizzino o meno l’ottimizzazione dell’ora di invio. In questo modo l’ottimizzazione dell’ora di invio può sfruttare tutti i dati generati dai consumatori.
   * I modelli vengono inizialmente addestrati e valutati settimanalmente. Dopo 16 settimane, i modelli vengono riaddestrati e rivalutati mensilmente. Il punteggio modello include tutti i profili cliente, esistenti e nuovi, dall’ultima esecuzione del punteggio.
   * I messaggi inviati da Ottimizzazione del tempo di invio ricevono uno dei seguenti messaggi:
      * Tempo di invio di un messaggio di &quot;esplorazione&quot;, selezionato per testare diversi orari di invio e osservare come rispondono i consumatori.
      * Un tempo di invio del messaggio &quot;ottimizzato&quot;, selezionato per massimizzare i tassi di clic/apertura. Il 5% degli eventi di invio riceve un tempo di invio di &quot;esplorazione&quot; e il 95% degli eventi di invio è &quot;ottimizzato&quot;.
   * I tempi di invio dell’esplorazione vengono selezionati in modo casuale tra i tempi di invio resi disponibili dal tempo di attesa massimo configurato. Ad esempio, nel caso in cui un messaggio venga selezionato alle 9 di mercoledì con Ottimizzazione dell’ora di invio attivata e un tempo di attesa massimo di 3 ore, gli orari di invio dell’esplorazione per il messaggio verranno suddivisi in modo uniforme tra le 9, le 10, le 11 e le 12.

## Valutazione del modello {#model-evaluation}

* **Valutazione del modello**: l&#39;ottimizzazione del tempo di invio può aumentare la percentuale di clic e di apertura delle e-mail e dei messaggi push in un intervallo compreso tra il 2% e il 10% circa in tutti i messaggi ottimizzati da un&#39;organizzazione.
   * Ad esempio, se un’organizzazione che invia e-mail senza ottimizzare il tempo di invio ha una percentuale di clic del 5,0% in media, lo stesso insieme di e-mail con ottimizzazione del tempo di invio potrebbe causare una percentuale di clic del 5,5% in media (5,0% * (1+10%) = 5,5%).
   * A causa della variabilità all’interno di campioni di piccole dimensioni, è possibile che non sia possibile osservare un vantaggio dall’ottimizzazione dell’ora di invio in caso di invii di un singolo messaggio.
   * È più probabile che le organizzazioni traggano maggiori vantaggi dall’utilizzo dell’ottimizzazione dell’ora di invio quando:
      * I percorsi esistenti utilizzano orari di invio fissi e non ottimizzati correttamente;
      * La variabilità del comportamento del consumatore (clic e aperture) corrisponde alla posizione del consumatore e alle sue preferenze;
      * Le organizzazioni utilizzano l’ottimizzazione dell’ora di invio su una percentuale più ampia di e-mail e messaggi push;
      * Le organizzazioni scelgono tempi di attesa massimi entro l’intervallo consigliato di 6-12 ore.

## Distribuzione del modello {#model-deployment}

* **Aggiornamento modello**: i modelli vengono inizialmente addestrati e valutati settimanalmente. Dopo 16 settimane, i modelli vengono riaddestrati e rivalutati mensilmente. Il punteggio del modello include tutti i profili di consumo, sia nuovi che esistenti, dall’ultima esecuzione del punteggio.

## Equità e parzialità {#fairness-and-bias}

* **Correttezza del modello**: l&#39;inferenza errata del fuso orario di un consumatore può comportare l&#39;invio di un messaggio prima del valore ottimale per un determinato consumatore o dopo il valore ottimale per un determinato consumatore. Tuttavia, tutti i consumatori in una comunicazione che utilizza l’ottimizzazione dell’ora di invio riceveranno un messaggio e avranno l’opportunità di interagire con esso. Inoltre, questo modello non utilizza dati demografici o proxy dei consumatori per i dati demografici; vengono utilizzati solo i dati relativi al comportamento dei consumatori e al fuso orario dei consumatori. Pertanto, i problemi di equità sono limitati e attenuati.
* **Disturbi dei dati**: l&#39;inferenza errata del fuso orario di un consumatore può comportare l&#39;invio di un messaggio prima del valore ottimale per un determinato consumatore o dopo il valore ottimale per un determinato consumatore. Tuttavia, tutti i consumatori in una comunicazione che utilizza l’ottimizzazione dell’ora di invio riceveranno un messaggio e avranno l’opportunità di interagire con esso. Inoltre, questo modello non utilizza dati demografici o proxy dei consumatori per i dati demografici; vengono utilizzati solo i dati relativi al comportamento dei consumatori e al fuso orario dei consumatori. Pertanto, i timori di distorsione sono limitati e attenuati.

## Robustezza {#robustness}

* **Robustezza del modello**: i profili senza dati sufficienti sull&#39;evento di interazione (spesso nel caso di nuovi profili) riceveranno un tempo di invio immediato, un tempo di invio dell&#39;esplorazione nella finestra selezionata o un tempo di invio basato sul tempo di invio con le prestazioni più elevate per tutti i clienti.

## Considerazioni etiche {#ethical-considerations}

* **Considerazioni etiche associate al modello**: l&#39;inferenza errata del fuso orario di un consumatore può comportare l&#39;invio di un messaggio prima del valore ottimale per un determinato consumatore o dopo il valore ottimale per un determinato consumatore. Tuttavia, tutti i consumatori in una comunicazione che utilizza l’ottimizzazione dell’ora di invio riceveranno un messaggio e avranno l’opportunità di interagire con esso. Inoltre, questo modello non utilizza dati demografici o proxy dei consumatori per i dati demografici; vengono utilizzati solo i dati relativi al comportamento dei consumatori e al fuso orario dei consumatori. Pertanto, le preoccupazioni etiche sono limitate e attenuate.