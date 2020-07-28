---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: 'Panoramica sulle Attribution AI '
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# Panoramica sulle Attribution AI 

 Attribution AI, come parte di Intelligent Services è un servizio di attribuzione algoritmica multicanale che calcola l&#39;influenza e l&#39;impatto incrementale delle interazioni dei clienti rispetto a determinati risultati. Con  Attribution AI, gli esperti di marketing possono misurare e ottimizzare le spese di marketing e pubblicitarie comprendendo l&#39;impatto di ogni singola interazione con i clienti in ogni fase dei viaggi dei clienti.

## Comprensione  Attribution AI

 Attribution AI viene utilizzata per attribuire i crediti ai punti di contatto che determinano gli eventi di conversione. Questo può essere utilizzato dagli addetti al marketing per quantificare l&#39;impatto di marketing di ogni singolo punto di contatto marketing sui percorsi dei clienti. Alcuni esempi di punti di contatto includono visualizzazioni ad impression, invii di e-mail, aperture di e-mail e clic di ricerca a pagamento.

 uscite di Attribution AI possono essere suddivise in diverse dimensioni e utilizzate in diverse fasi del percorso del cliente. Ciò è possibile senza dover tradurre le esigenze aziendali in problemi di machine learning, algoritmi di scelta, formazione o implementazione di modelli.

 i dati delle Attribution AI possono provenire da  Adobe (ad es. [!DNL Analytics]) o origini dati non  Adobe.

 Attribution AI supporta due categorie di punteggi, algoritmici e basati su regole. Algorithmic scores include incremental and influenced scores. Rule-based scores include First touch, Last touch, Linear, U-shaped, and Time-Decay.

The following video is designed to support your understanding of Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32667?learn=on&quality=12)

## Attribution AI algorithmic scores

Attribution AI supports two categories of attribution scores, algorithmic and rule-based scores.

Attribution AI produces two different types of algorithmic scores, incremental and influenced. An influenced score is the fraction of the conversion that each marketing touchpoint is responsible for. An incremental score is the amount of marginal impact directly caused by the marketing touchpoint. The main difference between the incremental score and the influenced score is that the incremental score takes the baseline effect into account. Non presuppone che una conversione sia causata esclusivamente dai punti di contatto di marketing precedenti.

See the table below for more details about each of these attribution scores:

| Attribution scores | Descrizione |
| ----- | ----------- |
| Primo contatto | Rule-based attribution score that assigns all credits to the initial touchpoint on a conversion path. |
| Ultimo contatto | Punteggio di attribuzione basato su regole che assegna tutti i crediti al punto di contatto più vicino alla conversione. |
| Lineare | Punteggio di attribuzione basato su regole che assegna lo stesso credito a ogni punto di contatto di un percorso di conversione. |
| A forma di U | Punteggio di attribuzione basato su regole che assegna il 40% del credito al primo punto di contatto e il 40% del credito all&#39;ultimo punto di contatto, con gli altri punti di contatto che dividono il restante 20% in modo uniforme. |
| Decadimento nel tempo | Punteggio di attribuzione basato su regole in cui i punti di contatto più vicini alla conversione ricevono più credito rispetto ai punti di contatto più distanti nel tempo dalla conversione. |
| Influenzato (algoritmico) | Il punteggio influenzato è la frazione della conversione di cui è responsabile ogni punto di contatto marketing. |
| Incremental (algoritmico) | Il punteggio incrementale è la quantità di impatto marginale direttamente causato da un punto di contatto di marketing. |

## Esempi di casi di utilizzo aziendale

 Attribution AI possono essere utilizzate per fornire assistenza nei seguenti casi di utilizzo di esempio:

- **Segnalazione** esecutiva: Consentire ai dirigenti di comprendere il vero impatto incrementale del marketing, sia nel suo insieme che per canale, regione, SKU, ecc.
- **Stanziamento** di bilancio: Informare le decisioni di allocazione del budget tra i canali di marketing.
- **Ottimizzazione** campagna: All&#39;interno di ciascun canale, potete comprendere quali campagne, creativi e parole chiave funzionano meglio per le quali SKU o Geos. Questo consente di guardare ogni canale in modo che il team marketing possa ottimizzare le tattiche.
- **Attribuzione** full-funnel: Comprendi l&#39;impatto del marketing sull&#39;intero percorso del cliente. Ad esempio, l&#39;iscrizione gratuita all&#39;account per la conversione a pagamento e oltre.
- **Valutazioni** partner: Valutare l&#39;efficacia delle agenzie e dei partner, sulla base dei risultati dell&#39;attribuzione.

### Funzioni aggiuntive

 Attribution AI offre inoltre l&#39;integrazione con altre soluzioni  Adobi come [!DNL Adobe Analytics]. Questo consente di utilizzare queste soluzioni per utilizzare il modello algoritmico personalizzabile per valutare le prestazioni dei supporti e fornire informazioni analitiche.

## Passaggi successivi

Per iniziare, segui la guida [introduttiva](./getting-started.md) . Questa guida illustra come impostare tutte le pre-richieste necessarie per  Attribution AI. Se disponete già di credenziali e dati, visitate la guida [utente](./user-guide.md)Attribution AI. Questa guida illustra come creare un’istanza e inviarla per la formazione e il punteggio.