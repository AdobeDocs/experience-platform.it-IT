---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;struttura dello schema;gruppo di campi;gruppo di campi;prenotazione;alloggio;
title: Gruppo di campi dello schema di prenotazione alloggio
description: Scopri il gruppo di campi Schema prenotazione alloggio.
exl-id: f0eafc83-21f1-483d-9397-1133e3777699
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 7%

---

# [!UICONTROL Gruppo di campi schema per prenotazione alloggio]

[!UICONTROL Prenotazione alloggio] è un gruppo di campi di schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzata per acquisire informazioni relative a una prenotazione alloggio.

Il gruppo di campi è un&#39;estensione del gruppo di campi [!UICONTROL Dettagli prenotazione] e contiene tutti gli stessi campi in un unico campo di tipo oggetto, `reservations`. Oltre a questi campi generici, la [!UICONTROL prenotazione alloggio] include anche l&#39;array `lodgingReservations`. Questo array di oggetti viene utilizzato per descrivere una o più prenotazioni con proprietà univoche per l’alloggio.

>[!NOTE]
>
>Questo documento descrive i dettagli dell&#39;array `lodgingReservations`. Per informazioni sugli altri campi forniti nell&#39;oggetto `reservations`, fare riferimento al riferimento al gruppo di campi [[!UICONTROL Dettagli prenotazione]](./reservation-details.md).

![Struttura prenotazione alloggio](../../images/field-groups/lodging-reservation/structure.png)

## `lodgingReservations`

`lodgingReservations` è un array di oggetti che rappresenta un elenco di prenotazioni di alloggio. Se un evento di prenotazione comporta prenotazioni in più hotel diversi lungo il percorso di un viaggio, ad esempio, queste prenotazioni possono essere elencate come singoli oggetti in `lodgingReservations` per un singolo evento.

La struttura di ciascun oggetto fornito in `lodgingReservations` è riportata di seguito.

![struttura alloggiamentoPrenotazioni](../../images/field-groups/lodging-reservation/lodgingReservations.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `averageDailyPrice` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Il prezzo medio giornaliero della camera d&#39;albergo. |
| `lodgingCheckIn` | Oggetto | Oggetto che descrive i dettagli del check-in dell&#39;alloggio. Include i seguenti valori:<ul><li>`digitalKey`: (numero intero) indica quando un ospite seleziona l&#39;uso di una chiave digitale al momento dell&#39;archiviazione.</li><li>`earlyCheckInRequested`: (numero intero) indica quando un ospite richiede di effettuare il check-in prima del normale orario di check-in.</li><li>`lateCheckInRequested`: (numero intero) indica quando un ospite richiede di effettuare il check-in oltre le normali ore di check-in.</li><li>`noRoomCheckIn`: (numero intero) questo valore viene acquisito quando un ospite termina il check-in quando non sono disponibili stanze in quel momento.</li><li>`oneRoomCheckIn`: (numero intero) questo valore viene acquisito quando un ospite termina il check-in quando è disponibile una sola room in quel momento.</li><li>`roomKeys`: (numero intero) il numero di chiavi di camera standard fornite al check-in.</li><li>`userSelectedRoom`: (booleano) indica se l&#39;ospite ha selezionato la propria stanza al momento del check-in.</li></ul> |
| `rackrate` | [[!UICONTROL Valuta]](../../data-types/currency.md) | Il costo di una prenotazione in giornata senza precedenti accordi di prenotazione. |
| `ID` | Stringa | Il numero o l’identificatore della prenotazione. |
| `agentID` | Stringa | ID dell’agente associato alla prenotazione dell’hotel. |
| `basePrice` | Stringa | Prezzo di base prima dell’applicazione di eventuali sconti. |
| `bookingID` | Stringa | L’ID prenotazione associato alla prenotazione dell’hotel. |
| `cancellation` | Intero | Questo valore viene acquisito quando una prenotazione è stata annullata. |
| `checkInDate` | Data e ora | La data di check-in per la prenotazione della camera. |
| `checkOutDate` | Data e ora | La data di check-out per la prenotazione della camera. |
| `confirmationNumber` | Stringa | Il numero o l’identificatore di conferma della prenotazione. |
| `couponCode` | Stringa | Codice coupon associato alla prenotazione dell’hotel. |
| `created` | Intero | Questo valore viene acquisito quando viene creata una prenotazione. |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per effettuare l’acquisto. |
| `discountPercent` | Doppio | La percentuale di sconto associata alla prenotazione. |
| `freeCancelation` | Booleano | Indica se la room dispone di un criterio di cancellazione gratuito. |
| `guestID` | Stringa | ID dell’ospite associato alla prenotazione dell’hotel. |
| `length` | Intero | Il numero totale di giorni per la prenotazione. |
| `loyaltyID` | Stringa | L’ID del programma fedeltà per l’ospite elencato nella prenotazione. |
| `modification` | Intero | Questo valore viene acquisito quando una prenotazione è stata modificata. |
| `modificationDate` | Data e ora | L’ora dell’ultima modifica apportata alla prenotazione. |
| `numberOfAdults` | Intero | Il numero di adulti associati alla prenotazione. |
| `numberOfChildren` | Intero | Il numero di figli associati alla prenotazione. |
| `numberOfRooms` | Intero | Il numero di camere associate alla prenotazione. |
| `propertyID` | Stringa | Un identificatore dell’hotel o della località turistica per la prenotazione. |
| `propertyName` | Stringa | Il nome dell’hotel o della località turistica per la prenotazione. |
| `purpose` | Stringa | Lo scopo della prenotazione, in genere aziendale o personale. |
| `ratePlan` | Stringa | La tariffa alla quale è stata venduta la camera. |
| `refundable` | Booleano | Indica se la camera è rimborsabile. |
| `reservationStatus` | Stringa | Stato della prenotazione. |
| `roomAccessibilityType` | Stringa | Il tipo di accessibilità della stanza, ad esempio mobilità, udito o altro. |
| `roomCapacity` | Intero | Il numero di persone che la stanza d&#39;albergo può ospitare. |
| `roomType` | Stringa | Tipo di camera da prenotare. |
| `smoking` | Booleano | Indica se la camera consente di fumare. |
| `tripType` | Stringa | Indica se la prenotazione è per un viaggio di sola andata, andata e ritorno o un viaggio con più città. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json)
