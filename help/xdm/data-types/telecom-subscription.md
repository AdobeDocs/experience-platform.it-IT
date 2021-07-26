---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;telecom;abbonamento;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati di abbonamento a una rete telefonica
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Telecom Subscription Experience Data Model).
source-git-commit: 19675e4042c28061a4b2ed4e68374d5e09216ba1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 10%

---

# [!UICONTROL Tipo di dati ] sottoscrizione Telecom

[!UICONTROL Telecom ] Subscriptionè un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli per tipi di sottoscrizione di telecomunicazioni specifici, come Internet, dispositivi mobili, media o linea fissa.

>[!NOTE]
>
>Questo documento descrive il tipo di dati. Per il gruppo di campi con lo stesso nome, fare riferimento alla guida di riferimento del gruppo di campi [[!UICONTROL Sottoscrizione alle telecomunicazioni]](../field-groups/profile/telecom-subscription.md).
>
>Se stai descrivendo un tipo di abbonamento non correlato al settore delle telecomunicazioni, utilizza invece il tipo di dati generico [[!UICONTROL Abbonamento]](./subscription.md).

![Struttura di abbonamento a telecomunicazioni](../images/data-types/telecom-subscription/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `devices` | Array di oggetti | Descrive un elenco di dispositivi e/o accessori associati al piano. Per informazioni dettagliate sulla struttura prevista di ciascun elemento dell&#39;array, vedere la sezione [riportata di seguito](#devices). |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Descrive il proprietario della sottoscrizione. |
| `ID` | Stringa | Identificatore univoco per l&#39;istanza di abbonamento. |
| `billingPeriod` | Stringa | La durata tra le fatture. |
| `billingStartDate` | Data | Data di inizio del periodo di fatturazione. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) . |
| `chargeMethod` | Stringa | Modalità di configurazione della fatturazione per addebitare al cliente. |
| `contractID` | Stringa | ID univoco del contratto che regola la sottoscrizione. |
| `country` | Stringa | Il paese in cui le condizioni contrattuali e contrattuali dell&#39;abbonamento sono radicate. |
| `endDate` | Data | Data di fine del termine di abbonamento corrente. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) . |
| `paymentDueDate` | Data | Data di scadenza del pagamento dell’abbonamento. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) . |
| `paymentMethod` | Stringa | Metodo di pagamento per pagamenti ricorrenti. |
| `paymentStatus` | Stringa | Il saldo del conto. |
| `planName` | Stringa | Nome leggibile per l&#39;abbonamento. |
| `reason` | Stringa | Intento generale del membro per l&#39;utilizzo della sottoscrizione. |
| `renew` | Stringa | Modalità concordate per il proseguimento della sottoscrizione dopo la data di scadenza. |
| `startDate` | Data | Data di inizio dell&#39;abbonamento. Il formato della data (senza tempo) deve seguire lo standard [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) . |
| `status` | Stringa | Lo stato corrente della sottoscrizione. |
| `subscriptionCategory` | Stringa | La classificazione principale di questo tipo di abbonamento. |
| `subscriptionSKU` | Stringa | Unità di conservazione delle scorte (SKU) per la sottoscrizione. |
| `subscriptionSubCategory` | Stringa | Sottoclassificazione specifica dell’abbonamento. |
| `term` | Intero | Il valore numerico del termine di abbonamento. |
| `termUnitOfTime` | Stringa | Unità di tempo per il periodo di tempo. |
| `topUp` | Stringa | Descrive i termini concordati per il modo in cui gli aspetti di consumo di un abbonamento vengono riacquistati durante un periodo di fatturazione. |
| `type` | Stringa | La portata del diritto in relazione al numero di persone che rientrano nel campo di applicazione della sottoscrizione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` è un array di oggetti, in cui ogni oggetto descrive un dispositivo o un accessorio associato alla sottoscrizione.

![Struttura della matrice dei dispositivi](../images/data-types/telecom-subscription/devices.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `deviceFees` | Oggetto | Un oggetto che acquisisce qualsiasi costo dispositivo per elementi quali router, modem e ricevitori. Si aspetta le seguenti proprietà:<ul><li>`amount`: L&#39;ammontare monetario rappresentato dal  `currencyCode`.</li><li>`conversionDate`: Data in cui è stata effettuata la conversione della valuta.</li><li>`currencyCode`: Il codice della valuta  [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) per  `amount`.</li></ul> |
| `ID` | Stringa | Un ID univoco per il dispositivo. |
| `OS` | Stringa | Sistema operativo del dispositivo. |
| `deviceInsurance` | Stringa | Indica se un cliente ha acconsentito all&#39;assicurazione del dispositivo. |
| `manufacturer` | Stringa | Il produttore del dispositivo. |
| `name` | Stringa | Un nome per il dispositivo. |
| `paymentOptions` | Stringa | Indica se il dispositivo verrà pagato a rate o al prezzo pieno al dettaglio. |
| `serialNumber` | Stringa | Numero di serie del dispositivo. |
| `status` | Stringa | Lo stato del dispositivo. |
| `storageCapacity` | Stringa | Capacità di archiviazione del dispositivo. |
| `type` | Stringa | Il tipo di dispositivo. |

{style=&quot;table-layout:auto&quot;}