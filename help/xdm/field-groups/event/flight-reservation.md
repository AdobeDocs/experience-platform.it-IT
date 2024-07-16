---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;ExperienceEvent;campi;schemi;schemi;schema design;gruppo di campi;gruppo di campi;prenotazione;volo;
title: Gruppo di campi schema prenotazione volo
description: Scopri il gruppo di campi dello schema Prenotazione del volo.
exl-id: df4bb525-c2d3-4e1d-921f-903142a570ac
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 10%

---

# [!UICONTROL Gruppo di campi dello schema Prenotazione del volo]

[!UICONTROL Prenotazione del volo] è un gruppo di campi dello schema standard per la [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md) utilizzata per acquisire informazioni relative a una prenotazione del volo.

Il gruppo di campi è un&#39;estensione del gruppo di campi [!UICONTROL Dettagli prenotazione] e contiene tutti gli stessi campi in un unico campo di tipo oggetto, `reservations`. Oltre a questi campi generici, [!UICONTROL Prenotazione del volo] include anche `flightReservations` array. Questo array di oggetti viene utilizzato per descrivere una o più prenotazioni con proprietà specifiche per i viaggi aerei.

>[!NOTE]
>
>Questo documento descrive i dettagli dell&#39;array `flightReservations`. Per informazioni sugli altri campi forniti nell&#39;oggetto `reservations`, fare riferimento al riferimento al gruppo di campi [[!UICONTROL Dettagli prenotazione]](./reservation-details.md).

![Struttura prenotazione voli](../../images/field-groups/flight-reservation/structure.png)

## `flightReservations`

`flightReservations` è un array di oggetti che rappresenta un elenco di prenotazioni di voli. Se un evento di prenotazione comporta prenotazioni per più voli in coincidenza in un viaggio, ad esempio, queste prenotazioni possono essere elencate come singoli oggetti in `flightReservations` per un singolo evento.

La struttura di ciascun oggetto fornito in `flightReservations` è riportata di seguito.

![struttura flightReservations](../../images/field-groups/flight-reservation/flightReservations.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `flightCheckIn` | Oggetto | Acquisisce i dettagli sul check-in del volo. L’oggetto include le seguenti proprietà:<ul><li>`arrivalAirportCode`: (stringa) il codice dell&#39;aeroporto della città di arrivo.</li><li>`boardingGroup`: (stringa) l&#39;indicatore specifico della compagnia aerea relativo all&#39;ordine di imbarco.</li><li>`checkInMethod`: (stringa) metodo utilizzato per il check-in, ad esempio contatore, online, chiosco o self-service.</li><li>`checkedBags`: (numero intero) il numero di bagagli registrati per il volo.</li><li>`checkedPassengers`: (numero intero) il numero di passeggeri registrati per il volo, se esistono più passeggeri per lo stesso numero di prenotazione.</li><li>`confirmationNumber`: (stringa) il numero o l&#39;identificatore di conferma della prenotazione.</li><li>`departureAirportCode`: (Stringa) Il codice dell&#39;aeroporto della città di partenza.</li><li>`flightNumber`: (Stringa) Il numero del volo che viene prenotato.</li></ul> |
| `flightStatusSearch` | Oggetto | Acquisisce i dettagli restituiti durante la ricerca dello stato del volo. L’oggetto include le seguenti proprietà:<ul><li>`arrivalAirportCode`: (stringa) il codice dell&#39;aeroporto della città di arrivo.</li><li>`boardingGroup`: (stringa) l&#39;indicatore specifico della compagnia aerea relativo all&#39;ordine di imbarco.</li><li>`departureAirportCode`: (Stringa) Il codice dell&#39;aeroporto della città di partenza.</li><li>`departureDate`: (DateTime) la data di partenza del volo che viene prenotato.</li><li>`flightNumber`: (Stringa) Il numero del volo che viene prenotato.</li><li>`searchCount`: (numero intero) il numero di volte in cui è stata eseguita la ricerca dello stato del volo prenotato.</li></ul> |
| `agentID` | Stringa | L’agente o il prenotatore responsabile della prenotazione, se applicabile. |
| `aircraftID` | Stringa | Un identificatore dell’aeromobile. |
| `aircraftType` | Stringa | Il tipo di aeromobile. |
| `arrivalAirportCode` | Stringa | Il codice dell’aeroporto della città di arrivo. |
| `arrivalDate` | Data e ora | La data di arrivo del volo che viene prenotato. |
| `cancellation` | Intero | Questo valore viene acquisito quando una prenotazione è stata annullata. |
| `confirmationNumber` | Stringa | Il numero o l’identificatore di conferma della prenotazione. |
| `created` | Stringa | Questo valore viene acquisito quando viene creata una prenotazione. |
| `currencyCode` | Stringa | Il codice valuta ISO 4217 utilizzato per effettuare l’acquisto. |
| `departureAirportCode` | Stringa | Il codice dell’aeroporto della città di partenza. |
| `departureDate` | Data e ora | La data di partenza del volo che viene prenotato. |
| `fareClass` | Stringa | La classe tariffaria del volo che viene prenotato. |
| `flightNumber` | Stringa | Il numero del volo che viene prenotato. |
| `length` | Intero | Il numero totale di giorni per la prenotazione. |
| `loyaltyID` | Stringa | L’ID del programma fedeltà o premi per il passeggero elencato nella prenotazione. |
| `modification` | Intero | Questo valore viene acquisito quando una prenotazione è stata modificata. |
| `modificationDate` | Data e ora | L’ora dell’ultima modifica apportata alla prenotazione. |
| `numberOfAdults` | Intero | Il numero di adulti associati alla prenotazione. |
| `numberOfChildren` | Intero | Il numero di figli associati alla prenotazione. |
| `passengerID` | Stringa | Informazioni sul passeggero associate alla prenotazione. |
| `purpose` | Stringa | Lo scopo della prenotazione, in genere aziendale o personale. |
| `salesChannel` | Stringa | Il canale di vendita da cui è stata effettuata la prenotazione. |
| `securityScreening` | Stringa | Il tipo di controllo di sicurezza a cui è soggetto il passeggero. |
| `status` | Stringa | Lo stato della prenotazione del volo. |
| `ticketNumber` | Stringa | Il numero o l’identificatore della prenotazione. |
| `tripType` | Stringa | Indica se la prenotazione è per un viaggio di sola andata, andata e ritorno o un viaggio con più città. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-flight-reservation.schema.json)
