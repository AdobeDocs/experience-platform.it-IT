---
title: Gruppo di campi dello schema della richiesta del medicinale
description: Scopri il gruppo di campi Schema della richiesta di medicinale.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7f7de89a843d867d18ef84051eee69face0570a0
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# [!UICONTROL Richiesta di medicinale] gruppo di campi dello schema

[!UICONTROL Richiesta medicinale] è un gruppo di campi dello schema standard per la [[!DNL Medication] classe](../../classes/location.md), la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) e la [[!DNL Provider class]](../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcareMedicationDispense` che acquisisce un ordine o una richiesta sia per la fornitura del medicinale che per le istruzioni per la somministrazione del medicinale a un paziente.

![Struttura del gruppo di campi](../../images/field-groups/healthcare-medication-request/medication-request.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Basato su] | `basedOn` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Il piano o la richiesta che viene soddisfatta da questa richiesta di trattamento. |
| [!UICONTROL Categoria] | `category` | Array di [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | La categorizzazione o il raggruppamento della richiesta di trattamento farmacologico. |
| [!UICONTROL Corso Di Tipo Terapeutico] | `courseOfTherapyType` | [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | La descrizione del modello generale per la somministrazione del medicinale al paziente. |
| [!UICONTROL Dispositivo] | `device` | Array di [[!UICONTROL Riferimento codificabile]](../../data-types/healthcare/codeable-reference.md) | Il tipo di dispositivo da utilizzare per la somministrazione del medicinale. |
| [!UICONTROL Richiesta di erogazione] | `dispenseRequest` | Oggetto | Indica i dettagli specifici della richiesta di dispensazione, spesso nota come ordine di somministrazione del medicinale. Per ulteriori informazioni, consulta la [sezione seguente](#dispense-request). |
| [!UICONTROL Istruzioni per il dosaggio] | `dosageInstructions` | Array di [[!UICONTROL dosaggio]](../../data-types/healthcare/dosage.md) | Istruzioni specifiche per l’uso del medicinale da parte del paziente. |
| [!UICONTROL Periodo di dose efficace] | `effectiveDosePeriod` | [[!UICONTROL Periodo]](../../data-types/healthcare/period.md) | Il periodo durante il quale il medicinale deve essere assunto. Se sono presenti più `dosageInstruction` righe (ad esempio, quando si riducono le dosi), questa è la data più vicina e la data più recente delle istruzioni sul dosaggio. |
| [!UICONTROL Incontro] | `encounter` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | L’incontro durante il quale è stata creata la richiesta. |
| [!UICONTROL Cronologia eventi] | `eventHistory` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Collegamento ai record di eventi relativi alla richiesta di trattamento, come il soddisfacimento della richiesta, momenti di transizioni chiave dello stato o aggiornamenti rilevanti. |
| [!UICONTROL Identificatore gruppo] | `groupIdentifier` | [[!UICONTROL Identificatore]](../../data-types/healthcare/identifier.md) | Identificatore condiviso tra più istanze di richiesta indipendenti attivate da un singolo autore. |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../../data-types/healthcare/identifier.md) | Identificatori associati alla richiesta di farmaci definiti dai processi aziendali e/o utilizzati per farvi riferimento quando un riferimento URL diretto alla risorsa stessa non è appropriato. |
| [!UICONTROL Informazioni su Source] | `informationSource` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Persona o organizzazione che ha fornito le informazioni per la richiesta se l&#39;origine è un utente diverso da `requester`. |
| [!UICONTROL Assicurazione] | `insurance` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Piani assicurativi, estensioni della copertura, preautorizzazioni e/o predeterminazioni che possono essere necessari per la prestazione del servizio richiesto. |
| [!UICONTROL Medicinale] | `medication` | [[!UICONTROL Riferimento codificabile]](../../data-types/healthcare/codeable-reference.md) | Identifica il farmaco richiesto. Deve essere un collegamento a una risorsa che rappresenta i dettagli del medicinale o un codice che identifica il medicinale. |
| [!UICONTROL Nota] | `note` | Array di [[!UICONTROL annotazione]](../../data-types/healthcare/annotation.md) | Informazioni aggiuntive sulla prescrizione che non possono essere trasmesse dagli altri attributi. |
| [!UICONTROL Esecutore] | `performer` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | L’esecutore specificato del trattamento/somministrazione del medicinale. Per i dispositivi, si tratta del dispositivo destinato a eseguire la somministrazione del medicinale. |
| [!UICONTROL Tipo di esecutore] | `performerType` | [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | Indica il tipo di esecutore per la somministrazione del farmaco. |
| [!UICONTROL Prescrizione precedente] | `priorPrescription` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Il riferimento a un ordine o una prescrizione che viene sostituito da questa richiesta. |
| [!UICONTROL Motivo] | `reason` | Array di [[!UICONTROL Riferimento codificabile]](../../data-types/healthcare/reference.md) | Motivo o indicazione per ordinare o non ordinare il medicinale. |
| [!UICONTROL Registratore] | `recorder` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | La persona che ha inserito l’ordine per conto di un altro individuo. |
| [!UICONTROL Richiedente] | `requester` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | L’individuo, l’organizzazione o il dispositivo che ha avviato la richiesta ed è responsabile della sua attivazione. |
| [!UICONTROL Motivo dello stato] | `statusReason` | [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | Motivo dello stato corrente della richiesta. |
| [!UICONTROL Oggetto] | `subject` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | L’individuo o il gruppo per il quale è stato richiesto il medicinale. |
| [!UICONTROL Sostituzione] | `substitution` | Oggetto | Indica se una sostituzione può o deve far parte della dispensa. Contiene tre proprietà: <li>`allowedBoolean`: valore booleano che è true se il medico prescrittore consente una sostituzione.</li> <li>`allowedCodeableConcept`: valore [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) che fornisce un codice se il medico prescrittore consente una sostituzione.</li> <li>`reason`: valore [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) che indica un motivo per la sostituzione.</li> |
| [!UICONTROL Informazioni di supporto] | `supportingInformation` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Informazioni a supporto dell’assunzione del medicinale, come altezza e peso del paziente. |
| [!UICONTROL Data creazione] | `authoredOn` | Data e ora | Data (e facoltativamente ora) in cui è stata scritta la prescrizione. |
| [!UICONTROL Non eseguire] | `doNotPerform` | Booleano | Un indicatore booleano che è vero è che il paziente deve interrompere (o non iniziare) l’assunzione del medicinale. |
| [!UICONTROL Intento] | `intent` | Stringa | Intento della richiesta. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL Priorità] | `priority` | Stringa | Priorità della richiesta. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL Istruzioni per il dosaggio con rendering] | `renderedDosageInstruction` | Stringa | La rappresentazione completa della dose inclusa in tutte le istruzioni per il dosaggio. Da utilizzare quando sono incluse istruzioni per dosi multiple per rappresentare dosi complesse come dosi crescenti o decrescenti. |
| [!UICONTROL Segnalato] | `reported` | Booleano | Indica se il record è stato acquisito come record secondario segnalato anziché come record originale di origine primaria della verità. |
| [!UICONTROL Stato] | `status` | Stringa | Stato della dispensazione. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Stato cambiato] | `statusChanged` | Data e ora | La data (e facoltativamente l’ora) in cui lo stato è cambiato. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Struttura della richiesta di Dispense](../../images/field-groups/healthcare-medication-request/dispense-request.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Intervallo di erogazione] | `dispenseInterval` | [[!UICONTROL Durata]](../../data-types/healthcare/duration.md) | Il periodo minimo di tempo che deve trascorrere tra una somministrazione e l’altra del farmaco. |
| [!UICONTROL Dispenser] | `dispenser` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | L’organizzazione prevista che dispenserà il medicinale come specificato dal medico prescrittore. |
| [!UICONTROL Istruzione dispenser] | `dispenserInstruction` | Array di [[!UICONTROL annotazione]](../../data-types/healthcare/annotation.md) | Informazioni aggiuntive per il dosatore, come la consulenza da fornire al paziente |
| [!UICONTROL Strumento Di Somministrazione Della Dose] | `doseAdministrationAid` | [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | Informazioni sul tipo di confezione di aderenza da fornire per la dispensazione del medicinale. |
| [!UICONTROL Durata prevista fornitura] | `expectedSupplyDuration` | [[!UICONTROL Durata]](../../data-types/healthcare/duration.md) | Il periodo di tempo durante il quale si prevede di utilizzare il prodotto fornito o la durata prevista dell’erogazione. |
| [!UICONTROL Riempimento iniziale] | `initialFill` | Oggetto | Informazioni per il riempimento iniziale. Contiene due proprietà: <li>`quantity`: un valore di [[!UICONTROL Quantità semplice]](../../data-types/healthcare/simple-quantity.md) che fornisce la quantità da fornire durante la prima dispensazione.</li> <li>`duration`: un valore di [[!UICONTROL Durata]](../../data-types/healthcare/duration.md) che fornisce il periodo di tempo previsto per la durata della prima dispensa.</li> |
| [!UICONTROL Quantità] | `quantity` | [[!UICONTROL Quantità semplice]](../../data-types/healthcare/simple-quantity.md) | Quantità da distribuire per un riempimento. |
| [!UICONTROL Periodo di validità] | `validityPeriod` | [[!UICONTROL Periodo]](../../data-types/healthcare/period.md) | Il periodo di validità della prescrizione. |
| [!UICONTROL Numero Di Ripetizioni Consentite] | `numberOfRepeatsAllowed` | Intero | Il numero di ricariche autorizzate, con un valore minimo di 0. |
