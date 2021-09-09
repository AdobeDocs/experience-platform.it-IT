---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;schema;schema di schema;gruppo di campi;gruppo di campi;prenotazione;dettagli sulla prenotazione;
title: Gruppo campi schema dettagli prenotazione
description: Questo documento fornisce una panoramica del gruppo di campi dello schema Dettagli prenotazione.
source-git-commit: 295dc040f3af7342226e3d78d0ae21e73db58d57
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 5%

---


# [!UICONTROL Gruppo di campi ] Dettagli prenotazione

[!UICONTROL Riserva ] Dettagli un gruppo di campi schema standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe utilizzato per acquisire informazioni relative a una prenotazione, tra cui lunghezza, modifica, stato rimborsabile e numero di stanze.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `reservations`. Le proprietà contenute in questo oggetto sono illustrate di seguito.

![Struttura dei dettagli di prenotazione](../../images/field-groups/reservation-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `nonRefundableAmount` | [Valuta](../../data-types/currency.md) | Importo del prezzo di prenotazione contrassegnato come non rimborsabile. |
| `transaction` | [Transazione](../../data-types/transaction.md) | Descrive la transazione di valuta per la prenotazione. |
| `id` | Stringa | Identificatore univoco della prenotazione. |
| `cancellation` | Intero | Questo valore viene acquisito quando una prenotazione è stata annullata. |
| `confirmationNumber` | Stringa | Il numero o l&#39;identificativo della prenotazione. |
| `created` | Intero | Questo valore viene acquisito al momento della creazione della prenotazione. |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per effettuare l&#39;acquisto. |
| `endDate` | DateTime | Data di fine del rilascio, della restituzione o del check-out della prenotazione. |
| `length` | Intero | Numero totale di giorni per la prenotazione. |
| `modification` | Intero | Questo valore viene acquisito quando una prenotazione è stata modificata. |
| `modificationDate` | DateTime | Data dell&#39;ultima modifica della prenotazione. |
| `numberOfAdults` | Intero | Numero di adulti associati alla prenotazione. |
| `numberOfChildren` | Intero | Il numero di figli associati alla prenotazione. |
| `purpose` | Stringa | Lo scopo della prenotazione, in genere sia commerciale che personale. |
| `startDate` | DateTime | Data di inizio ritiro, uscita o check-in per la prenotazione. |
| `triptype` | Stringa | Indica se la prenotazione è per un viaggio di sola andata, un viaggio di andata e ritorno o un viaggio in più città. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Gruppi di campi di prenotazione specifici per il settore

Esistono diversi altri gruppi di campi standard che estendono lo schema [!UICONTROL Dettagli prenotazione] per casi d’uso specifici del settore. Per ulteriori informazioni, consulta la seguente documentazione:

* [[!UICONTROL Prenotazione pranzo]](./dining-reservation.md)
* [[!UICONTROL Riserva di volo]](./flight-reservation.md)
* [[!UICONTROL Riserva]](./lodging-reservation.md)