---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;sottoscrizione;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati sottoscrizione
description: Questo documento fornisce una panoramica del tipo di dati XDM (Subscription Experience Data Model).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 10%

---

# [!UICONTROL Abbonamento] tipo di dati

[!UICONTROL Abbonamento] è un tipo di dati XDM (Experience Data Model) standard che descrive le adesioni concesse in licenza a software, servizi o beni utilizzati in base all’ora o all’utilizzo.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `device` | [[!UICONTROL Dispositivo]](./device.md) | Descrive i dettagli del dispositivo collegato alla sottoscrizione. |
| `environment` | [[!UICONTROL Ambiente]](./environment.md) | Contiene informazioni sulla situazione circostante in cui si è verificata l&#39;osservazione dell&#39;evento, in particolare informazioni transitorie come le versioni di rete o software. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Descrive una singola persona. Può anche rappresentare una persona che agisce in vari ruoli, ad esempio un cliente, un contatto o un proprietario. |
| `SKU` | Stringa | L&#39;unità di conservazione delle scorte (SKU), un identificatore univoco per un prodotto. |
| `billingPeriod` | Stringa | La durata tra le fatture. |
| `billingStartDate` | Data | Data di scadenza della prima fattura. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `category` | Stringa | La classificazione principale di questo tipo di abbonamento. |
| `chargeMethod` | Stringa | Modalità di configurazione della fatturazione per addebitare al cliente. |
| `contractID` | Stringa | ID univoco del contratto che regola la sottoscrizione. |
| `country` | Stringa | Il paese in cui le condizioni contrattuali e contrattuali dell&#39;abbonamento sono radicate. |
| `endDate` | Data | Data di fine del termine di abbonamento corrente. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `paymentMethod` | Stringa | Metodo di pagamento per pagamenti ricorrenti. |
| `paymentStatus` | Stringa | Il saldo del conto. |
| `planName` | Stringa | Nome leggibile per l&#39;abbonamento. |
| `reason` | Stringa | Intento generale del membro per l&#39;utilizzo della sottoscrizione. |
| `renew` | Stringa | Modalità concordate per il proseguimento della sottoscrizione dopo la data di scadenza. |
| `revision` | Stringa | Identificazione tra sottoscrizioni dello stesso nome e gerarchia di categorie. |
| `startDate` | Data | Data di inizio dell&#39;abbonamento. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `status` | Stringa | Lo stato corrente della sottoscrizione. |
| `subCategory` | Stringa | Sottoclassificazione specifica dell’abbonamento. |
| `term` | Intero | Il valore numerico del termine di abbonamento. |
| `termUnitOfTime` | Stringa | Unità di tempo per il periodo di tempo. |
| `topUp` | Stringa | Descrive i termini concordati per il modo in cui gli aspetti di consumo di un abbonamento vengono riacquistati durante un periodo di fatturazione. |
| `type` | Stringa | La portata del diritto in relazione al numero di persone che rientrano nel campo di applicazione della sottoscrizione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
