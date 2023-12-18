---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;gruppo di campi;gruppo di campi;prenotazione;pranzo;
title: Gruppo di campi Schema prenotazione ristorante
description: Scopri il gruppo di campi Schema prenotazione ristorante.
exl-id: 672b7a77-c433-4502-a1ad-a17c811b253e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 5%

---

# [!UICONTROL Prenotazione ristorante] gruppo di campi schema

[!UICONTROL Prenotazione ristorante] è un gruppo di campi di schema standard per [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzato per acquisire informazioni relative a una prenotazione di un ristorante.

Il gruppo di campi è un&#39;estensione del [!UICONTROL Dettagli prenotazione] e contiene tutti gli stessi campi in un unico campo di tipo oggetto, `reservations`. Oltre a questi campi generici, [!UICONTROL Prenotazione ristorante] include anche `diningReservations` array. Questo array di oggetti viene utilizzato per descrivere una o più prenotazioni con proprietà specifiche per il ristorante.

>[!NOTE]
>
>Il presente documento descrive in dettaglio `diningReservations` array. Per informazioni sugli altri campi di cui al `reservations` oggetto, fare riferimento al [[!UICONTROL Dettagli prenotazione] riferimento gruppo di campi](./reservation-details.md).

![Struttura prenotazione ristorante](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` è un array di oggetti che rappresenta un elenco di prenotazioni di ristoranti. Se un evento di prenotazione prevede prenotazioni in più ristoranti diversi in momenti diversi della giornata, ad esempio, queste prenotazioni possono essere elencate come singoli oggetti in `diningReservations` per un singolo evento.

La struttura di ciascun oggetto fornito in `diningReservations` viene fornito di seguito.

![struttura ristorantePrenotazioni](../../images/field-groups/dining-reservation/diningReservations.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `ID` | Stringa | Il numero o l’identificatore della prenotazione. |
| `cancellation` | Intero | Questo valore viene acquisito quando una prenotazione è stata annullata. |
| `confirmationNumber` | Stringa | Il numero o l’identificatore di conferma della prenotazione. |
| `created` | Intero | Questo valore viene acquisito quando viene creata una prenotazione. |
| `cuisine` | Intero | Il tipo di cucina del ristorante. |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per effettuare l’acquisto. |
| `deliveryPartners` | Stringa | Partner di consegna disponibili presso il ristorante. |
| `diningOptions` | Stringa | Opzioni di consegna e ristorazione disponibili presso il ristorante. |
| `groupReservation` | Booleano | Indica se la prenotazione viene effettuata per un gruppo. |
| `length` | Intero | Il numero totale di giorni per la prenotazione. |
| `loyaltyID` | Stringa | L’ID del programma fedeltà per l’ospite elencato nella prenotazione. |
| `modification` | Intero | Questo valore viene acquisito quando una prenotazione è stata modificata. |
| `modificationDate` | DateTime | L’ora dell’ultima modifica apportata alla prenotazione. |
| `numberOfAdults` | Intero | Il numero di adulti associati alla prenotazione. |
| `numberOfChildren` | Intero | Il numero di figli associati alla prenotazione. |
| `numberOfRooms` | Intero | Il numero di camere associate alla prenotazione. |
| `partySize` | Intero | Il numero di persone alla cena. |
| `priceCategory` | Stringa | Categoria di prezzo per la prenotazione in corso. |
| `purpose` | Stringa | Lo scopo della prenotazione, in genere aziendale o personale. |
| `reservationTime` | DateTime | L’orario per il quale è stata effettuata la prenotazione del ristorante. |
| `restaurantID` | Stringa | Identificatore del ristorante o del luogo di ristorazione. |
| `reservationStatus` | Stringa | Stato della prenotazione. |
| `specialOccasion` | Booleano | Indica se la prenotazione viene effettuata per un’occasione speciale. |
| `status` | Intero | Lo stato della prenotazione del ristorante. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
