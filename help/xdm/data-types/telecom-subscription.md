---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;telefonia;abbonamento;tipo dati;tipo dati;tipo dati;
solution: Experience Platform
title: Tipo di dati abbonamento telefonia
description: Scopri il tipo di dati XDM (Telecom Subscription Experience Data Model).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 20%

---

# Tipo di dati [!UICONTROL abbonamento Telecom]

[!UICONTROL Sottoscrizione telecomunicazioni] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli per tipi di abbonamento di telecomunicazioni specifici, ad esempio Internet, dispositivi mobili, supporti o rete fissa.

>[!NOTE]
>
>Questo documento descrive il tipo di dati. Per il gruppo di campi con lo stesso nome, fare riferimento alla [[!UICONTROL Guida di riferimento per il gruppo di campi Sottoscrizione telefonica]](../field-groups/profile/telecom-subscription.md).
>
>Se si descrive un tipo di abbonamento non correlato al settore delle telecomunicazioni, utilizzare il tipo di dati generico [[!UICONTROL Abbonamento]](./subscription.md).

![Struttura abbonamento telecomunicazioni](../images/data-types/telecom-subscription/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `devices` | Array di oggetti | Descrive un elenco di dispositivi e/o accessori associati al piano. Per informazioni dettagliate sulla struttura prevista di ciascun elemento dell&#39;array, consulta la [sezione seguente](#devices). |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Descrive il proprietario della sottoscrizione. |
| `ID` | Stringa | Un identificatore univoco per l’istanza di abbonamento. |
| `billingPeriod` | Stringa | La durata del periodo tra le fatture. |
| `billingStartDate` | Data | La data di inizio del periodo di fatturazione. Il formato della data (senza ora) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `chargeMethod` | Stringa | Il modo in cui la fatturazione è impostata per addebitare il cliente. |
| `contractID` | Stringa | ID univoco del contratto che regola questo abbonamento. |
| `country` | Stringa | Il paese a cui sono legati i termini contrattuali dell’abbonamento. |
| `endDate` | Data | Data di fine del periodo di abbonamento corrente. Il formato della data (senza ora) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentDueDate` | Data | La data di scadenza dell’abbonamento. Il formato della data (senza ora) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Stringa | Il metodo di pagamento per i pagamenti ricorrenti. |
| `paymentStatus` | Stringa | La condizione di pagamento del conto. |
| `planName` | Stringa | Nome leggibile dell’abbonamento. |
| `reason` | Stringa | L’intento generale del membro in relazione all’utilizzo dell’abbonamento. |
| `renew` | Stringa | Il modo concordato in cui l’abbonamento può continuare dopo la data di fine. |
| `startDate` | Data | La data di inizio dell’abbonamento. Il formato della data (senza ora) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Stringa | Lo stato attuale dell’abbonamento. |
| `subscriptionCategory` | Stringa | La categorizzazione principale e di primo livello di questo tipo di abbonamento. |
| `subscriptionSKU` | Stringa | L’unità di gestione delle scorte (SKU) per l’abbonamento. |
| `subscriptionSubCategory` | Stringa | La sottocategoria specifica dell’abbonamento. |
| `term` | Intero | Il valore numerico del termine di abbonamento. |
| `termUnitOfTime` | Stringa | L’unità di tempo della durata del periodo. |
| `topUp` | Stringa | Descrive i termini concordati per il riacquisto degli aspetti consumabili di un abbonamento durante un periodo di fatturazione. |
| `type` | Stringa | Ambito di autorizzazione in relazione al numero di persone incluse nell’abbonamento. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` è un array di oggetti, ognuno dei quali descrive un dispositivo o un accessorio associato alla sottoscrizione.

![Struttura array dispositivi](../images/data-types/telecom-subscription/devices.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `deviceFees` | Oggetto | Oggetto che acquisisce qualsiasi tariffa del dispositivo per elementi quali router, modem e ricevitori. Prevede le seguenti proprietà:<ul><li>`amount`: importo monetario rappresentato da `currencyCode`.</li><li>`conversionDate`: la data in cui è stata effettuata la conversione della valuta.</li><li>`currencyCode`: il codice valuta [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) per `amount`.</li></ul> |
| `ID` | Stringa | ID univoco del dispositivo. |
| `OS` | Stringa | Il sistema operativo del dispositivo. |
| `deviceInsurance` | Stringa | Indica se un cliente ha acconsentito all&#39;assicurazione per questo dispositivo. |
| `manufacturer` | Stringa | Il produttore del dispositivo. |
| `name` | Stringa | Nome del dispositivo. |
| `paymentOptions` | Stringa | Indica se il dispositivo verrà pagato a rate o a prezzo intero al dettaglio. |
| `serialNumber` | Stringa | Il numero di serie del dispositivo. |
| `status` | Stringa | Lo stato del dispositivo. |
| `storageCapacity` | Stringa | La capacità di archiviazione del dispositivo. |
| `type` | Stringa | Il tipo di dispositivo. |

{style="table-layout:auto"}
