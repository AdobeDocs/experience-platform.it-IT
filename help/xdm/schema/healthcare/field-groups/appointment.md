---
title: Gruppo di campi schema appuntamento
description: Scopri il gruppo di campi Schema appuntamento.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8224a2ee-51ac-4512-b0e4-5f1ab6bfddc4
source-git-commit: cb39966de77846758c16153f78fcf521f6a421e3
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 5%

---

# [!UICONTROL Appuntamento] gruppo di campi dello schema

[!UICONTROL Appuntamento] è un gruppo di campi dello schema standard per la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e la [[!DNL Provider class]](../../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcareAppointment` che contiene informazioni sulla prenotazione di un evento sanitario tra pazienti, operatori sanitari, persone correlate e/o dispositivi per una data e un&#39;ora specifiche.

![Diagramma di schema della struttura del gruppo di campi per gli appuntamenti.](../../../images/healthcare/field-groups/appointment/appointment.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Account] | `account` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Set di conti che si prevede verranno utilizzati per la fatturazione. |
| [!UICONTROL Tipo di appuntamento] | `appointmentType` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Lo stile dell’appuntamento o del paziente che è stato prenotato nello slot (non il tipo di servizio). |
| [!UICONTROL Basato su] | `basedOn` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | La richiesta che la nomina è assegnata a valutare, ad esempio una richiesta di procedura. |
| [!UICONTROL Motivo annullamento] | `cancellationReason` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Motivo codificato dell&#39;annullamento dell&#39;appuntamento. Questo viene spesso utilizzato nei rapporti, nella fatturazione o nell’elaborazione per determinare se sono necessarie ulteriori azioni o se si applicano tariffe specifiche. |
| [!UICONTROL Classe] | `class` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Concetti che rappresentano la classificazione di un incontro con un paziente come ambulatoriale, ambulatoriale, ospedaliero o di emergenza. |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Elenco di identificatori univoci collegati all&#39;appuntamento. Questi identificatori vengono assegnati in base alle regole aziendali o quando un collegamento URL diretto all’appuntamento non è appropriato. |
| [!UICONTROL Nota] | `note` | Array di [[!UICONTROL annotazione]](../data-types/annotation.md) | Note o commenti aggiuntivi sull&#39;appuntamento. |
| [!UICONTROL Appuntamento di origine] | `originatingAppointment` | [[!UICONTROL Riferimento]](../data-types/reference.md) | L&#39;appuntamento di origine in un insieme ricorrente di appuntamenti correlati. |
| [!UICONTROL Partecipante] | `participant` | Array di oggetti | Un elenco dei partecipanti coinvolti nella nomina. Per ulteriori informazioni, consulta la [sezione seguente](#participant). |
| [!UICONTROL Istruzioni per il paziente] | `patientInstruction` | Array di [[!UICONTROL Riferimento codificabile]](../data-types/reference.md) | La diagnosi rilevante per l’appuntamento. |
| [!UICONTROL Appuntamento precedente] | `previousAppointment` | [[!UICONTROL Riferimento]](../data-types/reference.md) | L&#39;appuntamento precedente in una serie di appuntamenti correlati. |
| [!UICONTROL Priorità] | `priority` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | La priorità della nomina che può essere utilizzata per prendere decisioni informate se è necessario ridefinire le priorità delle nomine. ICal Standard specifica `0` come non definito, `1` come priorità massima e `9` come priorità minima. |
| [!UICONTROL Motivo] | `reason` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Motivo della pianificazione dell&#39;appuntamento, in genere una condizione o una procedura. |
| [!UICONTROL Modello ricorrenze] | `recurrenceTemplate` | Array di oggetti | Contiene i dettagli del criterio di ricorrenza o del modello utilizzato per creare appuntamenti ricorrenti.  Per ulteriori informazioni, consulta la [sezione seguente](#recurrence). |
| [!UICONTROL Sostituisce] | `replaces` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | L&#39;appuntamento è sostituito da questo appuntamento. Nei casi in cui si verifica un annullamento, i dettagli dell&#39;annullamento sono disponibili nella proprietà `cancellationReason` della risorsa di riferimento. |
| [!UICONTROL Periodo richiesto] | `requestedPeriod` | Array di [[!UICONTROL Periodo]](../data-types/period.md) | Un insieme di intervalli di date (che potrebbero includere ore) durante i quali si preferisce pianificare l’appuntamento. |
| [!UICONTROL Categoria servizio] | `serviceCategory` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Un&#39;ampia categorizzazione del servizio che deve essere svolto durante l&#39;appuntamento. |
| [!UICONTROL Tipo di servizio] | `serviceType` | Array di [[!UICONTROL Riferimento codificabile]](../data-types/codeable-reference.md) | Il servizio specifico da eseguire durante l&#39;appuntamento. |
| [!UICONTROL Slot] | `slot` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Fasce orarie delle pianificazioni dei partecipanti che verranno compilate dall&#39;appuntamento. |
| [!UICONTROL Specializzazione] | `speciality` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | La specializzazione di un professionista necessaria per svolgere il servizio richiesto nel presente appuntamento. |
| [!UICONTROL Oggetto] | `subject` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Il paziente o il gruppo associato all’appuntamento. |
| [!UICONTROL Informazioni di supporto] | `supportingInformation` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Ulteriori informazioni fornite in occasione dell&#39;appuntamento per supportarla. |
| [!UICONTROL Servizio virtuale] | `virtualService` | Array di [[!UICONTROL Dettagli servizio virtuale]](../data-types/virtual-service-detail.md) | Dettagli di connessione di un servizio virtuale, ad esempio una conferenza telefonica. |
| [!UICONTROL Data annullamento] | `cancellationDate` | Data e ora | La data e l&#39;ora in cui l&#39;appuntamento è stato annullato. |
| [!UICONTROL Creato] | `created` | Data e ora | Data e ora di creazione dell&#39;appuntamento. |
| [!UICONTROL Descrizione] | `description` | Stringa | Breve descrizione dell&#39;appuntamento. Le informazioni dettagliate o estese devono essere inserite nel campo `note`. |
| [!UICONTROL Fine] | `end` | Data e ora | La data e l&#39;ora di conclusione dell&#39;appuntamento. |
| Durata [!UICONTROL minuti] | `minutesDuration` | Intero | Numero di minuti necessari per l&#39;appuntamento. Questo valore può essere inferiore alla durata compresa tra l&#39;ora di inizio e l&#39;ora di fine. Il valore minimo accettato è `0`. |
| [!UICONTROL Occorrenza modificata] | `occurenceChanged` | Booleano | Flag che indica se l&#39;appuntamento è diverso dal modello ricorrente. |
| [!UICONTROL IDRicorrenza] | `RecurrenceId` | Intero | Numero di sequenza che identifica un appuntamento specifico in un modello ricorrente. Il valore minimo è `0`. |
| [!UICONTROL Inizio] | `start` | Data e ora | La data e l’ora in cui avrà luogo l’appuntamento. |
| [!UICONTROL Stato] | `status` | Stringa | Stato dell&#39;appuntamento. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti: <li> `proposed` </li> <li> `pending` </li> <li> `booked` </li> <li> `arrived` </li> <li> `fulfilled` </li> <li> `cancelled` </li> <li> `noshow` </li> <li> `entered-in-error` </li> <li> `checked-in` </li> <li> `waitlist` </li> |


Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/appointment.schema.json)

## `participant` {#participant}

`participant` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Diagramma di schema della struttura dell&#39;oggetto partecipante.](../../../images/healthcare/field-groups/appointment/participant.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Attore] | `actor` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Individuo, dispositivo, luogo o servizio che partecipa all&#39;appuntamento. |
| [!UICONTROL Periodo] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Periodo di tempo durante il quale il partecipante (attore) è coinvolto nella nomina. |
| [!UICONTROL Tipo] | `type` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il ruolo del partecipante (attore) nell&#39;appuntamento. |
| [!UICONTROL Obbligatorio] | `required` | Booleano | Indica se il partecipante deve essere presente o meno. |
| [!UICONTROL stato] | `status` | Stringa | Lo stato di accettazione del partecipante. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti: <li> `accepted` </li> <li> `declined` </li> <li> `tentative` </li> <li> `needs-action` </li> |

## `recurrenceTemplate` {#recurrence}

`recurrenceTemplate` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Diagramma di schema della struttura dell&#39;oggetto modello di ricorrenza.](../../../images/healthcare/field-groups/appointment/recurrence-template.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Modello mensile] | `monthlyTemplate` | Array di oggetti | Informazioni sugli appuntamenti mensili ricorrenti. Per ulteriori informazioni, consulta la [sezione seguente](#monthly-template). |
| [!UICONTROL Tipo di Ricorrenza] | `recurrenceType` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Frequenza con cui la serie di appuntamenti deve ripresentarsi, ad esempio settimanale, mensile o annuale. |
| [!UICONTROL Fuso orario] | `timezone` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Fuso orario dell&#39;appuntamento ricorrente. |
| [!UICONTROL Modello settimanale] | `weeklyTemplate` | Array di oggetti | Informazioni sugli appuntamenti ricorrenti settimanali. Per ulteriori informazioni, consulta la [sezione seguente](#weekly-template). |
| [!UICONTROL Modello annuale] | `yearlyTemplate` | Oggetto | Informazioni sugli appuntamenti ricorrenti annuali. Contiene una proprietà, `yearInterval`, che contiene un valore intero che indica ogni nono anno che l&#39;appuntamento ricorre. |
| [!UICONTROL Data di esclusione] | `excludingDate` | Array di date | Tutte le date, ad esempio le festività, che devono essere escluse dalla ricorrenza. |
| [!UICONTROL Esclusione Id Ricorrenza] | `excludingRecurrenceId` | Array di interi | Eventuali ID di ricorrenza che devono essere esclusi dalla ricorrenza. Si tratta di un&#39;alternativa a `excludingDate` in cui si indica `reccurenceID` dell&#39;appuntamento da escludere. |
| [!UICONTROL Data ultima occorrenza] | `lastOccurenceDate` | Data | Data dopo la quale non verranno pianificati ulteriori appuntamenti ricorrenti. |
| [!UICONTROL Conteggio occorrenze] | `occurenceCount` | Intero | Quanti appuntamenti sono pianificati nella ricorrenza. Il valore minimo è `0`. |
| [!UICONTROL Data occorrenza] | `occurenceDate` | Array di date | Elenco di date specifiche in cui sono pianificati gli appuntamenti. |

## `weeklyTemplate` {#weekly-template}

`weeklyTemplate` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Diagramma di schema della struttura dell&#39;oggetto modello settimanale.](../../../images/healthcare/field-groups/appointment/weekly-template.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Venerdì] | `friday` | Booleano | Indica che gli appuntamenti ricorrenti devono avvenire il venerdì. |
| [!UICONTROL Lunedì] | `monday` | Booleano | Indica che gli appuntamenti ricorrenti devono avvenire il lunedì. |
| [!UICONTROL Sabato] | `saturday` | Booleano | Indica che gli appuntamenti ricorrenti devono avvenire il sabato. |
| [!UICONTROL Domenica] | `sunday` | Booleano | Indica che gli appuntamenti ricorrenti devono avvenire di domenica. |
| [!UICONTROL Giovedì] | `thursday` | Booleano | Indica che gli appuntamenti ricorrenti devono avvenire il giovedì. |
| [!UICONTROL Martedì] | `tuesday` | Booleano | Indica che gli appuntamenti ricorrenti devono avvenire il martedì. |
| [!UICONTROL Mercoledì] | `wednesday` | Booleano | Indica che gli appuntamenti ricorrenti devono avvenire il mercoledì. |
| [!UICONTROL Intervallo settimana] | `weekInterval` | Intero | Specifica la frequenza di ricorrenza degli appuntamenti, in termini di settimane consecutive. Il valore predefinito è ogni settimana, quindi il valore tipico è 2 o superiore. |

## `monthlyTemplate` {#monthly-template}

`monthlyTemplate` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Diagramma di schema della struttura di oggetti modello mensile.](../../../images/healthcare/field-groups/appointment/monthly-template.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Giorno Della Settimana] | `dayOfWeek` | [[!UICONTROL Codifica]] | Indica che gli appuntamenti devono avvenire in questo giorno specifico della settimana. |
| [!UICONTROL ° settimana del mese] | `nthWeekOfMonth` | [[!UICONTROL Codifica]](../data-types/coding.md) | Indica l&#39;ennesima settimana del mese in cui l&#39;appuntamento deve essere registrato. |
| [!UICONTROL Giorno Del Mese] | `dayOfMonth` | Intero | Indica che gli appuntamenti devono avvenire in questo giorno specifico del mese. |
| [!UICONTROL Intervallo di mesi] | `monthInterval` | Intero | Indica che gli appuntamenti ricorrenti devono avvenire ogni mese. |

