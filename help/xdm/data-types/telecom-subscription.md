---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;telecom;abbonamento;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati di abbonamento a una rete telefonica
description: Questo documento fornisce una panoramica del tipo di dati XDM (Telecom Subscription Experience Data Model).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 11%

---

# [!UICONTROL Abbonamento a domicilio] tipo di dati

[!UICONTROL Abbonamento a domicilio] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli di tipi di sottoscrizione di telecomunicazioni specifici, come Internet, dispositivi mobili, media o linea fissa.

>[!NOTE]
>
>Questo documento descrive il tipo di dati. Per il gruppo di campi con lo stesso nome, fai riferimento al [[!UICONTROL Abbonamento a domicilio] guida di riferimento per i gruppi di campi](../field-groups/profile/telecom-subscription.md).
>
>Se stai descrivendo un tipo di abbonamento che non è collegato al settore delle telecomunicazioni, utilizza il [[!UICONTROL Abbonamento] tipo di dati](./subscription.md) invece.

![Struttura di abbonamento a telecomunicazioni](../images/data-types/telecom-subscription/structure.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `devices` | Array di oggetti | Descrive un elenco di dispositivi e/o accessori associati al piano. Consulta la sezione [sezione sottostante](#devices) per informazioni dettagliate sulla struttura prevista di ogni elemento della matrice. |
| `subscriber` | [[!UICONTROL Persona]](./person.md) | Descrive il proprietario della sottoscrizione. |
| `ID` | Stringa | Identificatore univoco per l&#39;istanza di abbonamento. |
| `billingPeriod` | Stringa | La durata tra le fatture. |
| `billingStartDate` | Data | Data di inizio del periodo di fatturazione. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `chargeMethod` | Stringa | Modalità di configurazione della fatturazione per addebitare al cliente. |
| `contractID` | Stringa | ID univoco del contratto che regola la sottoscrizione. |
| `country` | Stringa | Il paese in cui le condizioni contrattuali e contrattuali dell&#39;abbonamento sono radicate. |
| `endDate` | Data | Data di fine del termine di abbonamento corrente. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `paymentDueDate` | Data | Data di scadenza del pagamento dell’abbonamento. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `paymentMethod` | Stringa | Metodo di pagamento per pagamenti ricorrenti. |
| `paymentStatus` | Stringa | Il saldo del conto. |
| `planName` | Stringa | Nome leggibile per l&#39;abbonamento. |
| `reason` | Stringa | Intento generale del membro per l&#39;utilizzo della sottoscrizione. |
| `renew` | Stringa | Modalità concordate per il proseguimento della sottoscrizione dopo la data di scadenza. |
| `startDate` | Data | Data di inizio dell&#39;abbonamento. Il formato della data (senza tempo) deve seguire il [RFC 3339, sezione 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
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
| `deviceFees` | Oggetto | Un oggetto che acquisisce qualsiasi costo dispositivo per elementi quali router, modem e ricevitori. Si aspetta le seguenti proprietà:<ul><li>`amount`: L&#39;importo monetario rappresentato dal `currencyCode`.</li><li>`conversionDate`: Data in cui è stata effettuata la conversione della valuta.</li><li>`currencyCode`: La [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) codice della valuta per `amount`.</li></ul> |
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
