---
title: Tipo di dati dettagli account
description: Questo documento fornisce una panoramica del tipo di dati XDM (Account Details Experience Data Model).
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# [!UICONTROL Dettagli account] tipo di dati

[!UICONTROL Dettagli account] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli relativi a un’organizzazione aziendale.

![Struttura del tipo di dati](../images/data-types/account-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Valuta]](./currency.md) | Importo stimato delle entrate annuali dell&#39;organizzazione. |
| `DUNSNumber` | Stringa | Il numero Dun &amp; Bradstreet D-U-N-S dell&#39;organizzazione. Si tratta di un numero non indicativo di nove cifre assegnato a ogni posizione commerciale nel database Dun &amp; Bradstreet con un funzionamento unico, separato e distinto, ed è gestito esclusivamente da Dun &amp; Bradstreet. |
| `NAICSCode` | Stringa | Classificazione dell&#39;organizzazione nell&#39;ambito del sistema di classificazione dell&#39;industria nordamericana. |
| `NAICSDescription` | Stringa | Breve descrizione della linea di business di un’organizzazione, basata sul codice NAICS. |
| `SICCode` | Stringa | Codice di classificazione industriale standard (SIC) dell&#39;organizzazione. Questo è un codice a quattro cifre che classifica il settore a cui appartengono le aziende in base alle loro attività commerciali. |
| `SICDescription` | Stringa | Breve descrizione della linea di attività di un’organizzazione, basata sul suo codice SIC. |
| `companyProductAndServices` | Stringa | I prodotti e i servizi in cui l&#39;organizzazione ha a che fare o svolge attività commerciali. |
| `facebookPageUrl` | Stringa | Collegamento a un sito web dell’account Facebook dell’organizzazione. |
| `industry` | Stringa | L&#39;industria di cui fa parte questa organizzazione. Si tratta di un campo a forma libera ed è consigliabile utilizzare un valore strutturato per le query o per utilizzare il `xdm:classifier` proprietà. |
| `jigsaw` | Stringa | Chiave Data.com per l&#39;organizzazione. |
| `linkedinPageUrl` | Stringa | Collegamento a un sito web dell’account LinkedIn dell’organizzazione. |
| `logoUrl` | Stringa | Un percorso da combinare con l’URL di un’istanza Salesforce (ad esempio, `https://yourInstance.salesforce.com/`) per generare un URL per richiedere l&#39;immagine del profilo di social network associata all&#39;organizzazione. L&#39;URL generato restituisce un reindirizzamento HTTP (codice 302) all&#39;immagine del profilo del social network per l&#39;organizzazione. |
| `marketSegment` | Stringa | Il segmento di mercato denominato a cui partecipa l&#39;organizzazione. Si tratta di un campo a forma libera ed è consigliabile utilizzare un valore strutturato per le query o per utilizzare il `xdm:identifier` proprietà. |
| `numberOfEmployees` | Intero | Numero di dipendenti dell&#39;organizzazione. |
| `organizationType` | Stringa | Etichetta che descrive il tipo di organizzazione. |
| `primaryEmailDomain` | Stringa | Il dominio e-mail principale utilizzato dall’organizzazione per il proprio personale. |
| `rating` | Doppio | Punteggio calcolato o valutazione a stelle per questa organizzazione. `1` indica la classificazione massima possibile, e `0` è la valutazione minima possibile. |
| `tickerSymbol` | Stringa | Il simbolo del mercato azionario per questo conto. Massimo 20 caratteri. |
| `twitterHandleUrl` | Stringa | Un collegamento a un sito Web all’handle twitter dell’organizzazione. |
| `website` | Stringa | URL del sito web dell’organizzazione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
