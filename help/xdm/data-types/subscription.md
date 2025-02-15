---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;sottoscrizione;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati abbonamento
description: Scopri il tipo di dati Subscription Experience Data Model (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 28%

---

# Tipo di dati [!UICONTROL Sottoscrizione]

[!UICONTROL Abbonamento] è un tipo di dati XDM (Experience Data Model) standard che descrive i diritti concessi in licenza a software, servizi o beni utilizzati in base al tempo o all&#39;utilizzo.

![](../images/data-types/subscription-data-type.png){width=500}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `device` | [[!UICONTROL Dispositivo]](./device.md) | Descrive i dettagli del dispositivo collegato all’abbonamento. |
| `environment` | [[!UICONTROL Ambiente]](./environment.md) | Contiene informazioni sulla situazione circostante in cui si è verificata l’osservazione dell’evento, in particolare informazioni transitorie come la rete o le versioni del software. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Descrive una singola persona. Può anche rappresentare una persona che svolge vari ruoli, ad esempio un cliente, un contatto o un proprietario. |
| `SKU` | Stringa | L’SKU (Stock Keeping Unit), un identificatore univoco di un prodotto. |
| `billingPeriod` | Stringa | La durata del periodo tra le fatture. |
| `billingStartDate` | Data | La data di scadenza della prima fattura. Il formato della data (senza ora) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `category` | Stringa | La categorizzazione principale e di primo livello di questo tipo di abbonamento. |
| `chargeMethod` | Stringa | Il modo in cui la fatturazione è impostata per addebitare il cliente. |
| `contractID` | Stringa | ID univoco del contratto che regola questo abbonamento. |
| `country` | Stringa | Il paese a cui sono legati i termini contrattuali dell’abbonamento. |
| `endDate` | Data | Data di fine del periodo di abbonamento corrente. Il formato della data (senza ora) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Stringa | Il metodo di pagamento per i pagamenti ricorrenti. |
| `paymentStatus` | Stringa | La condizione di pagamento del conto. |
| `planName` | Stringa | Nome leggibile dell’abbonamento. |
| `reason` | Stringa | L’intento generale del membro in relazione all’utilizzo dell’abbonamento. |
| `renew` | Stringa | Il modo concordato in cui l’abbonamento può continuare dopo la data di fine. |
| `revision` | Stringa | L’identificazione tra gli abbonamenti con lo stesso nome e la gerarchia delle categorie. |
| `startDate` | Data | La data di inizio dell’abbonamento. Il formato della data (senza ora) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Stringa | Lo stato attuale dell’abbonamento. |
| `subCategory` | Stringa | La sottocategoria specifica dell’abbonamento. |
| `term` | Intero | Il valore numerico del termine di abbonamento. |
| `termUnitOfTime` | Stringa | L’unità di tempo della durata del periodo. |
| `topUp` | Stringa | Descrive i termini concordati per il riacquisto degli aspetti consumabili di un abbonamento durante un periodo di fatturazione. |
| `type` | Stringa | Ambito di autorizzazione in relazione al numero di persone incluse nell’abbonamento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
