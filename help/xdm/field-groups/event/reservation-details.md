---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;struttura dello schema;gruppo di campi;gruppo di campi;riserva;dettagli prenotazione;
title: Gruppo di campi schema Dettagli prenotazione
description: Scopri il gruppo di campi dello schema Dettagli prenotazione.
exl-id: 06f9ee37-9879-4db2-af68-9336366f7521
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 5%

---

# [!UICONTROL Dettagli prenotazione] gruppo di campi schema

[!UICONTROL Dettagli prenotazione] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzato per acquisire informazioni relative a una prenotazione, tra cui durata, modifica, stato rimborsabile e numero di camere.

Il gruppo di campi fornisce un singolo campo di tipo oggetto, `reservations`. Le proprietà contenute in questo oggetto sono illustrate di seguito.

![Struttura dei dettagli prenotazione](../../images/field-groups/reservation-details.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `nonRefundableAmount` | [Valuta](../../data-types/currency.md) | Importo del prezzo della prenotazione contrassegnato come non rimborsabile. |
| `transaction` | [Transazione](../../data-types/transaction.md) | Descrive la transazione in valuta per la prenotazione. |
| `id` | Stringa | Un identificatore univoco della prenotazione. |
| `cancellation` | Intero | Questo valore viene acquisito quando una prenotazione è stata annullata. |
| `confirmationNumber` | Stringa | Il numero o l’identificatore di conferma della prenotazione. |
| `created` | Intero | Questo valore viene acquisito al momento della creazione della prenotazione. |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per effettuare l’acquisto. |
| `endDate` | DateTime | La data finale di consegna, restituzione o check-out della prenotazione. |
| `length` | Intero | Il numero totale di giorni per la prenotazione. |
| `modification` | Intero | Questo valore viene acquisito quando una prenotazione è stata modificata. |
| `modificationDate` | DateTime | L’ora dell’ultima modifica apportata alla prenotazione. |
| `numberOfAdults` | Intero | Il numero di adulti associati alla prenotazione. |
| `numberOfChildren` | Intero | Il numero di figli associati alla prenotazione. |
| `purpose` | Stringa | Lo scopo della prenotazione, in genere aziendale o personale. |
| `startDate` | DateTime | Data di inizio del ritiro, dell’uscita o del check-in della prenotazione. |
| `triptype` | Stringa | Indica se la prenotazione è per un viaggio di sola andata, andata e ritorno o un viaggio con più città. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-reservation-details.schema.json)

## Gruppi di campi di prenotazione specifici per il settore

Esistono diversi altri gruppi di campi standard che estendono [!UICONTROL Dettagli prenotazione] schema per casi d’uso specifici per il settore. Per ulteriori informazioni, consulta la seguente documentazione:

* [[!UICONTROL Prenotazione ristorante]](./dining-reservation.md)
* [[!UICONTROL Prenotazione del volo]](./flight-reservation.md)
* [[!UICONTROL Prenotazione alloggio]](./lodging-reservation.md)
