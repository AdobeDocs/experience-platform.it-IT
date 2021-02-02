---
keywords: ' Experience Platform;home;argomenti comuni;schema;schema;XDM;campi;schemi;sottoscrizione;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo di dati iscrizione
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Subscription Experience Data Model).
translation-type: tm+mt
source-git-commit: 8ccf0a53f231c9f59cd87735126b180c6b678e51
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 9%

---


# [!UICONTROL Subscription] tipo di dati

[!UICONTROL Subscription] è un tipo di dati XDM (Experience Data Model) standard che descrive le adesioni con licenza a software, servizi o beni che vengono utilizzati in base all&#39;ora o all&#39;uso.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `device` | [[!UICONTROL Device]](./device.md) | Descrive i dettagli del dispositivo collegato alla sottoscrizione. |
| `environment` | [[!UICONTROL Environment]](./environment.md) | Contiene informazioni sulla situazione in cui si è verificata l&#39;osservazione dell&#39;evento, in particolare informazioni transitorie come le versioni di rete o software. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Descrive una singola persona. Può anche rappresentare una persona che agisce in vari ruoli, come un cliente, un contatto o un proprietario. |
| `SKU` | Stringa | L’unità di gestione delle scorte (SKU), un identificatore univoco per un prodotto. |
| `billingPeriod` | Stringa | Durata tra le fatture. |
| `billingStartDate` | Data | Data di scadenza della prima fattura. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `category` | Stringa | La principale categorizzazione di livello principale di questo tipo di iscrizione. |
| `chargeMethod` | Stringa | Modalità di configurazione della fatturazione per addebitare al cliente. |
| `contractID` | Stringa | ID univoco per il contratto che disciplina la sottoscrizione. |
| `country` | Stringa | Il paese in cui le condizioni contrattuali e contrattuali della sottoscrizione hanno origine. |
| `endDate` | Data | Data di fine del periodo di iscrizione corrente. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Stringa | Metodo di pagamento per pagamenti periodici. |
| `paymentStatus` | Stringa | Il saldo del conto. |
| `planName` | Stringa | Nome leggibile per l’iscrizione. |
| `reason` | Stringa | Intento generale di cui dispone il membro per l&#39;utilizzo della sottoscrizione. |
| `renew` | Stringa | Il modo concordato in cui la sottoscrizione può continuare dopo la data di fine. |
| `revision` | Stringa | Identificazione tra le sottoscrizioni con lo stesso nome e la stessa gerarchia di categorie. |
| `startDate` | Data | Data di inizio dell’iscrizione. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Stringa | Stato corrente della sottoscrizione. |
| `subCategory` | Stringa | Sottoclassificazione specifica della sottoscrizione. |
| `term` | Intero | Il valore numerico del termine di sottoscrizione. |
| `termUnitOfTime` | Stringa | Unità di tempo per il periodo di tempo. |
| `topUp` | Stringa | Descrive i termini concordati per determinare in che modo gli aspetti di consumo di un&#39;iscrizione vengono riacquistati durante un periodo di fatturazione. |
| `type` | Stringa | Ambito di applicazione dell&#39;adesione in relazione al numero di persone che rientrano nell&#39;iscrizione. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)