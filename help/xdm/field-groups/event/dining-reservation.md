---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;schema;schema di schema;gruppo di campi;gruppo di campi;prenotazione;pranzo;
title: Gruppo campi schema prenotazione pranzo
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema Riserva di pranzo.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 5%

---


# [!UICONTROL Gruppo di campi schema ] prenotazione pranzo

[!UICONTROL Dining ] Reservationè un gruppo di campi schema standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe utilizzato per acquisire informazioni relative a una prenotazione pranzo.

Il gruppo di campi è un&#39;estensione del gruppo di campi [!UICONTROL Dettagli prenotazione] e contiene tutti gli stessi campi in un singolo campo di tipo oggetto, `reservations`. Oltre a questi campi generici, [!UICONTROL Riserva da pranzo] include anche la matrice `diningReservations`. Questa serie di oggetti viene utilizzata per descrivere una o più prenotazioni con proprietà specifiche del ristorante.

>[!NOTE]
>
>Questo documento descrive i dettagli dell&#39;array `diningReservations`. Per informazioni sugli altri campi forniti nell&#39;oggetto `reservations`, fare riferimento al riferimento al gruppo di campi [[!UICONTROL Dettagli prenotazione]](./reservation-details.md).

![Struttura di prenotazione](../../images/field-groups/dining-reservation/structure.png)

## `diningReservations`

`diningReservations` è un array di oggetti che rappresenta un elenco di prenotazioni di pranzo. Se un evento di prenotazione comporta prenotazioni in più ristoranti diversi in momenti diversi della giornata, ad esempio, queste prenotazioni possono essere elencate come singoli oggetti in `diningReservations` per un singolo evento.

La struttura di ciascun oggetto fornito in `diningReservations` è fornita di seguito.

![struttura diningReservations](../../images/field-groups/dining-reservation/diningReservations.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `ID` | Stringa | Numero o identificativo della prenotazione. |
| `cancellation` | Intero | Questo valore viene acquisito quando una prenotazione è stata annullata. |
| `confirmationNumber` | Stringa | Numero o identificativo della prenotazione. |
| `created` | Intero | Questo valore viene acquisito quando viene creata una prenotazione. |
| `cuisine` | Intero | Il tipo di cucina ristorante. |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per effettuare l&#39;acquisto. |
| `deliveryPartners` | Stringa | Partner di consegna disponibili dal ristorante. |
| `diningOptions` | Stringa | Opzioni di consegna e pranzo disponibili presso il ristorante. |
| `groupReservation` | Booleano | Indica se la prenotazione viene effettuata per un gruppo. |
| `length` | Intero | Numero totale di giorni per la prenotazione. |
| `loyaltyID` | Stringa | ID del programma fedeltà per gli ospiti elencati nella prenotazione. |
| `modification` | Intero | Questo valore viene acquisito quando una prenotazione è stata modificata. |
| `modificationDate` | DateTime | Data dell&#39;ultima modifica della prenotazione. |
| `numberOfAdults` | Intero | Numero di adulti associati alla prenotazione. |
| `numberOfChildren` | Intero | Il numero di figli associati alla prenotazione. |
| `numberOfRooms` | Intero | Numero di stanze associate alla prenotazione. |
| `partySize` | Intero | Il numero di individui nella festa di pranzo. |
| `priceCategory` | Stringa | Categoria di prezzo per la prenotazione effettuata. |
| `purpose` | Stringa | Lo scopo della prenotazione, in genere sia commerciale che personale. |
| `reservationTime` | DateTime | L&#39;orario per il quale è prenotata la prenotazione. |
| `restaurantID` | Stringa | Identificatore del ristorante o della posizione pranzo. |
| `reservationStatus` | Stringa | Lo stato della prenotazione. |
| `specialOccasion` | Booleano | Indica se la prenotazione viene effettuata per un&#39;occasione speciale. |
| `status` | Intero | Lo stato della prenotazione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-dining-reservation.schema.json)
