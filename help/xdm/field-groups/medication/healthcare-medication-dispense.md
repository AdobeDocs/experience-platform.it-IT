---
title: Gruppo di campi Schema dispensa del medicinale
description: Scopri il gruppo di campi Schema dispensa di medicinali.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# [!UICONTROL Gruppo di campi dello schema dispensa di medicinali]

[!UICONTROL Disposizione medicinale] è un gruppo di campi dello schema standard per la [[!DNL Medication] classe](../../classes/location.md), la [[!DNL XDM Individual Profile] Classe](../../classes/individual-profile.md) e la [[!DNL Provider class]](../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcareMedicationDispense` che acquisisce informazioni su un medicinale che deve essere o è stato dispensato per una persona/paziente con nome.

![Struttura del gruppo di campi](../../images/field-groups/healthcare-medication-dispense/medication-dispense.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Autorizzazione della prescrizione] | `authorizingPrescription` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | L’ordine che consente la dispensazione della prescrizione. |
| [!UICONTROL Basato su] | `basedOn` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Il piano su cui si basa la somministrazione del medicinale. |
| [!UICONTROL Categoria] | `category` | Array di [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | Rientra nella categoria del farmaco dispensato, ad esempio la categoria legale del farmaco o la classificazione del farmaco. |
| [!UICONTROL Giorni di fornitura] | `daysSupply` | [[!UICONTROL Quantità semplice]](../../data-types/healthcare/simple-quantity.md) | Il numero di giorni per i quali il medicinale fornirà il paziente. |
| [!UICONTROL Destinazione] | `destination` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | La struttura o il luogo in cui il medicinale è stato o sarà spedito, come parte dell’evento di erogazione. |
| [!UICONTROL Istruzioni per il dosaggio] | `dosageInstruction` | Array di [[!UICONTROL dosaggio]](../../data-types/healthcare/dosage.md) | Descrive come il farmaco deve essere utilizzato dal paziente. |
| [!UICONTROL Incontro] | `encounter` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | L’incontro che stabilisce il contesto per questo evento. |
| [!UICONTROL Cronologia eventi] | `eventHistory` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Riepilogo degli eventi che si sono verificati intorno alla dispensazione. |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../../data-types/healthcare/identifier.md) | Identificatori associati alla dispensazione. Gli identificatori devono essere definiti dai processi aziendali e/o utilizzati per farvi riferimento quando un riferimento URL diretto non è appropriato. |
| [!UICONTROL Posizione] | `location` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Il luogo fisico principale in cui è stato dispensato il medicinale. |
| [!UICONTROL Medicinale] | `medication` | [[!UICONTROL Riferimento codificabile]](../../data-types/healthcare/codeable-reference.md) | Identifica il farmaco richiesto. Deve essere un collegamento a una risorsa che rappresenta i dettagli del medicinale o un codice che identifica il medicinale. |
| [!UICONTROL Motivo non eseguito] | `notPerformedReason` | [[!UICONTROL Riferimento codificabile]](../../data-types/healthcare/codeable-reference.md) | La ragione per cui il farmaco non è stato dispensato. |
| [!UICONTROL Nota] | `note` | Array di [[!UICONTROL annotazione]](../../data-types/healthcare/annotation.md) | Informazioni aggiuntive sulla dispensazione. |
| [!UICONTROL Parte Di] | `partOf` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | La procedura o la richiesta di trattamento che ha attivato la dispensazione. |
| [!UICONTROL Esecutore] | `performer` | Array di oggetti | Indica chi o cosa ha eseguito l’evento di dispensazione. Per ulteriori informazioni, consulta la [sezione seguente](#performer). |
| [!UICONTROL Quantità] | `quantity` | [[!UICONTROL Quantità semplice]](../../data-types/healthcare/simple-quantity.md) | La quantità di medicinale che è stata somministrata, inclusa l’unità di misura. |
| [!UICONTROL Destinatario] | `receiver` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Identifica la persona che ha preso il medicinale o il luogo in cui il medicinale è stato consegnato. |
| [!UICONTROL Oggetto] | `subject` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Collegamento a una risorsa che rappresenta la persona o il gruppo a cui verrà somministrato il farmaco. |
| [!UICONTROL Sostituzione] | `substitution` | Oggetto | Indica se la sostituzione è stata effettuata o meno nell&#39;ambito della dispensa. Contiene quattro proprietà: <li>`wasSubstituted`: valore booleano che è true se il dispenser ha richiesto una sostituzione.</li> <li>`type`: valore [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) che fornisce un codice che indica se è stata effettuata una sostituzione.</li> <li>`reason`: matrice di [[!UICONTROL valori Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) contenente i motivi della sostituzione.</li> <li>`responsibleParty`: valore [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) che fornisce la persona o la parte responsabile della sostituzione. </li> |
| [!UICONTROL Informazioni di supporto] | `supportingInformation` | Array di [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Informazioni aggiuntive che supportano il medicinale che viene dispensato. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | Descrive il tipo di evento di dispensazione eseguito, ad esempio un riempimento di emergenza o parziale. |
| [!UICONTROL Registrato] | `recorded` | Data e ora | La data e l&#39;ora di inizio dell&#39;attività di dispensazione se `whenPrepared` o `whenHandedOver` non è popolato. |
| [!UICONTROL Istruzioni per il dosaggio con rendering] | `renderedDosageInstruction` | Stringa | La rappresentazione completa della dose inclusa in tutte le istruzioni per il dosaggio. Da utilizzare quando sono incluse istruzioni per dosi multiple per rappresentare dosi complesse come dosi crescenti o decrescenti. |
| [!UICONTROL Stato] | `status` | Stringa | Stato della dispensazione. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Stato cambiato] | `statusChanged` | Data e ora | La data e l&#39;ora in cui lo stato del record dispensa è cambiato. |
| [!UICONTROL Alla consegna] | `whenHandedOver` | Data e ora | La data e l’ora in cui il medicinale dispensato è stato fornito al paziente. |
| [!UICONTROL Durante La Preparazione] | `whenPrepared` | Data e ora | La data e l’ora in cui il medicinale dispensato è stato confezionato e rivisto. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura esecutore](../../images/field-groups/healthcare-medication-dispense/performer.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Attore] | `actor` | [[!UICONTROL Riferimento]](../../data-types/healthcare/reference.md) | Il medico (o altro) che ha eseguito l’azione. Si deve presumere che l’attore sia il dispensatore del medicinale. |
| [!UICONTROL Funzione] | `function` | [[!UICONTROL Concetto codificabile]](../../data-types/healthcare/codeable-concept.md) | Il tipo di esecutore nella dispensazione, ad esempio l&#39;inseritore di data, l&#39;inserzionista o il controllore finale. |
