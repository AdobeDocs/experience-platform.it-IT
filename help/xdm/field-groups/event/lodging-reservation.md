---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schema;schema di schema;gruppo di campi;gruppo di campi;prenotazione;alloggio;
title: Caricamento del gruppo di campi dello schema di prenotazione
description: In questo documento viene fornita una panoramica del gruppo di campi dello schema di prenotazione di Lodging.
source-git-commit: d230cfa9e74eb96aa44e8b83ca8f2306db4ba4ec
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 5%

---


# [!UICONTROL Gruppo di campi ] dello schema di prenotazione

[!UICONTROL Lodging ] Reservationè un gruppo di campi di schema standard per la  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) classe utilizzata per acquisire informazioni relative a una prenotazione di alloggio.

Il gruppo di campi è un&#39;estensione del gruppo di campi [!UICONTROL Dettagli prenotazione] e contiene tutti gli stessi campi in un singolo campo di tipo oggetto, `reservations`. Oltre a questi campi generici, [!UICONTROL Lodging Reservation] include anche la matrice `lodgingReservations`. Questo array di oggetti viene utilizzato per descrivere una o più prenotazioni con proprietà uniche alla sistemazione.

>[!NOTE]
>
>Questo documento descrive i dettagli dell&#39;array `lodgingReservations`. Per informazioni sugli altri campi forniti nell&#39;oggetto `reservations`, fare riferimento al riferimento al gruppo di campi [[!UICONTROL Dettagli prenotazione]](./reservation-details.md).

![Struttura di riserva](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` è un array di oggetti che rappresenta un elenco di prenotazioni di alloggio. Se un evento di prenotazione comporta prenotazioni in più alberghi diversi lungo il percorso di un viaggio, ad esempio, queste prenotazioni possono essere elencate come singoli oggetti in `lodgingReservations` per un singolo evento.

La struttura di ciascun oggetto fornito in `lodgingReservations` è fornita di seguito.

![Struttura delle prenotazioni](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Prezzo medio giornaliero della camera d&#39;albergo. |
| `lodgingCheckIn` | Oggetto | Oggetto che descrive i dettagli del check-in della struttura. Include i seguenti valori:<ul><li>`digitalKey`: (Intero) Indica quando un ospite seleziona l’uso di una chiave digitale al momento del check-in.</li><li>`earlyCheckInRequested`: (Intero) Indica quando un ospite richiede di eseguire il check-in prima delle ore di check-in normali.</li><li>`lateCheckInRequested`: (Intero) Indica quando un ospite richiede di effettuare il check-in più tardi delle normali ore di check-in.</li><li>`noRoomCheckIn`: (Intero) Questo valore viene acquisito quando un ospite termina il check-in quando non sono disponibili stanze in quel momento.</li><li>`oneRoomCheckIn`: (Intero) Questo valore viene acquisito quando un ospite termina il check-in quando è disponibile una sola stanza in quel momento.</li><li>`roomKeys`: (Intero) Il numero di chiavi standard fornite al momento del check-in.</li><li>`userSelectedRoom`: (Booleano) Indica se l&#39;ospite ha selezionato la propria stanza al momento del check-in.</li></ul> |
| `rackrate` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Il costo per una prenotazione dello stesso giorno senza prenotazioni precedenti. |
| `ID` | Stringa | Numero o identificativo della prenotazione. |
| `agentID` | Stringa | ID agente associato alla prenotazione dell&#39;hotel. |
| `basePrice` | Stringa | Il prezzo di base prima di eventuali sconti. |
| `bookingID` | Stringa | ID prenotazione associato alla prenotazione dell&#39;hotel. |
| `cancellation` | Intero | Questo valore viene acquisito quando una prenotazione è stata annullata. |
| `checkInDate` | DateTime | Data del check-in per la prenotazione della camera. |
| `checkOutDate` | DateTime | Data del check-out per la prenotazione della stanza. |
| `confirmationNumber` | Stringa | Numero o identificativo della prenotazione. |
| `couponCode` | Stringa | Codice coupon associato alla prenotazione dell&#39;hotel. |
| `created` | Intero | Questo valore viene acquisito quando viene creata una prenotazione. |
| `currencyCode` | Stringa | Codice valuta ISO 4217 utilizzato per effettuare l&#39;acquisto. |
| `discountPercent` | Doppio | Percentuale di sconto associata alla prenotazione. |
| `freeCancelation` | Booleano | Indica se la stanza dispone di una politica di cancellazione gratuita. |
| `guestID` | Stringa | ID ospite associato alla prenotazione dell&#39;hotel. |
| `length` | Intero | Numero totale di giorni per la prenotazione. |
| `loyaltyID` | Stringa | ID del programma fedeltà per gli ospiti elencati nella prenotazione. |
| `modification` | Intero | Questo valore viene acquisito quando una prenotazione è stata modificata. |
| `modificationDate` | DateTime | Data dell&#39;ultima modifica della prenotazione. |
| `numberOfAdults` | Intero | Numero di adulti associati alla prenotazione. |
| `numberOfChildren` | Intero | Il numero di figli associati alla prenotazione. |
| `numberOfRooms` | Intero | Numero di stanze associate alla prenotazione. |
| `propertyID` | Stringa | Identificatore dell&#39;hotel o del resort per la prenotazione. |
| `propertyName` | Stringa | Nome dell&#39;hotel o del resort per la prenotazione. |
| `purpose` | Stringa | Lo scopo della prenotazione, in genere sia commerciale che personale. |
| `ratePlan` | Stringa | L&#39;accordo di prezzo su cui la stanza è stata venduta. |
| `refundable` | Booleano | Indica se la stanza è rimborsabile. |
| `reservationStatus` | Stringa | Lo stato della prenotazione. |
| `roomAccessibilityType` | Stringa | Tipo di accessibilità della stanza, ad esempio mobilità, udito o altro. |
| `roomCapacity` | Intero | Il numero di persone in cui si trova la stanza dell&#39;hotel. |
| `roomType` | Stringa | Tipo di camera riservata. |
| `smoking` | Booleano | Indica se la camera permette di fumare. |
| `tripType` | Stringa | Indica se la prenotazione è per un viaggio di sola andata, un viaggio di andata e ritorno o un viaggio in più città. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
