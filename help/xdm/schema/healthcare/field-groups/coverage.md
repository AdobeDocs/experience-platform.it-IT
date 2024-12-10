---
title: Gruppo di campi schema di copertura
description: Scopri il gruppo di campi Schema di copertura.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 7b84c0cf-3bd4-4ba8-a8cc-85e6b3f2b59e
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 6%

---

# [!UICONTROL Copertura] gruppo di campi schema

[!UICONTROL Copertura] è un gruppo di campi dello schema standard per la [[!DNL Plan] classe](../../../classes/plan.md). Fornisce un unico campo di tipo oggetto `healthcareCoverage` che è destinato a fornire gli identificatori e i descrittori di alto livello di un piano assicurativo, in genere le informazioni che compaiono su una carta di assicurazione, che possono essere utilizzati per pagare, in parte o in tutto, la fornitura di prodotti e servizi sanitari.

![Struttura del gruppo di campi](../../../images/healthcare/field-groups/coverage/coverage.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Beneficiario del piano] | `beneficiary` | [[!UICONTROL Riferimento]](../data-types/reference.md) | La parte che beneficia della copertura assicurativa e il paziente quando vengono forniti prodotti o servizi. |
| [!UICONTROL Classe] | `class` | Array di oggetti | Una suite di classificatori specifici del sottoscrittore. Per ulteriori informazioni, consulta la [sezione seguente](#class). |
| [!UICONTROL Contatto] | `contract` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Le polizze che costituiscono tale copertura assicurativa. |
| [!UICONTROL Costo Per Beneficiario] | `costToBeneficiary` | Array di oggetti | Una suite di codici che indica la categoria di costo e l’importo associato che sono stati dettagliati nella polizza e che potrebbero essere stati inclusi nella scheda sanitaria. Per ulteriori informazioni, consulta la [sezione seguente](#cost-to-beneficiary). |
| [!UICONTROL Eccezione] | `exception` | Array di oggetti | Una suite di codici che indicano eccezioni o riduzioni dei costi dei pazienti e dei periodi effettivi. Per ulteriori informazioni, consulta la [sezione seguente](#exception). |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | L’identificativo della copertura emessa dall’assicuratore. |
| [!UICONTROL Piano assicurativo] | `insurancePlan` | [[!UICONTROL Riferimento]](../data-types/reference.md) | I dettagli del piano assicurativo, i benefici e i costi che costituiscono tale copertura assicurativa. |
| [!UICONTROL Assicuratore] | `insurer` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Il programma o piano sottoscrittore, pagatore o società di assicurazione. |
| [!UICONTROL Pagamento di] | `paymentBy` | Array di oggetti | Il legame con il soggetto pagatore e, facoltativamente, ciò che sarà tenuto a pagare. Per ulteriori informazioni, consulta la [sezione seguente](#payment-by). |
| [!UICONTROL Date di inizio e fine copertura] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Periodo di tempo durante il quale è attiva la copertura. Una data di inizio mancante indica che la data di inizio non è nota, una data di fine mancante indica che la copertura è in corso. |
| [!UICONTROL Titolare del criterio] | `policyHolder` | [[!UICONTROL Riferimento]](../data-types/reference.md) | La parte che detiene la polizza assicurativa. |
| [!UICONTROL Relazione beneficiario] | `relationship` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il rapporto del beneficiario con l’abbonato. |
| [!UICONTROL Sottoscrittore] | `subscriber` | [[!UICONTROL Riferimento]](../data-types/reference.md) | La parte che detiene il rapporto contrattuale con la polizza. |
| [!UICONTROL Identificatore Sottoscrittore] | `subscriberId` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | ID dell’assicuratore assegnato dell’abbonato. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Tipo di copertura. |
| [!UICONTROL Numero dipendente] | `dependent` | Stringa | Designazione di un dipendente nell&#39;ambito della copertura. |
| [!UICONTROL Tipo] | `kind` | Stringa | Il tipo di copertura. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `insurance` </li> <li> `self-pay` </li> <li> `other` </li> |
| [!UICONTROL Rete assicuratore] | `network` | Stringa | La rete di fornitori a cui il beneficiario può chiedere un trattamento che sarà coperto al tasso interno alla rete, altrimenti si applicano condizioni e termini esterni alla rete. |
| [!UICONTROL Ordine di copertura] | `order` | Intero | Ordine relativo della copertura, con valore minimo `0`. |
| [!UICONTROL Stato] | `status` | Stringa | Stato della copertura. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `active` </li> <li> `cancelled` </li> <li> `draft` </li> <li> `entered-in-error` </li> |
| [!UICONTROL Subrogazione] | `subrogation` | Booleano | Quando `true`, questa istanza assicurativa è stata inclusa non per l&#39;aggiudicazione, ma per fornire agli assicuratori i dettagli per il recupero dei costi. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `class` {#class}

`class` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Struttura di classe](../../../images/healthcare/field-groups/coverage/class.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Tipo] | `type` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Tipo di classificazione per il quale viene fornita un’etichetta di classe specifica dell’assicuratore, ovvero un numero e un nome facoltativo. Ad esempio, il tipo può essere utilizzato per identificare una classe di copertura, un gruppo di datori di lavoro, una policy o un piano. |
| [!UICONTROL Valore] | `value` | [[!UICONTROL Identificatore]](../data-types/identifier.md) | L’identificatore alfanumerico associato all’etichetta rilasciata dall’assicuratore. |
| [!UICONTROL Nome] | `name` | Stringa | Breve descrizione della classe. |

## `costToBeneficiary` {#cost-to-beneficiary}

`costToBeneficiary` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Struttura costi per beneficiario](../../../images/healthcare/field-groups/coverage/cost-to-beneficiary.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Categoria] | `category` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il codice per identificare il tipo generale di prestazioni nell&#39;ambito delle quali sono forniti prodotti e servizi. |
| [!UICONTROL Rete] | `network` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il codice per indicare se i vantaggi si riferiscono a provider in-network o out-of-network. |
| [!UICONTROL Durata] | `term` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | La durata dei valori, ad esempio il beneficio massimo nell’arco della vita. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | La categoria dei costi incentrati sul paziente associati al trattamento. |
| [!UICONTROL Unità] | `unit` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Indica se le prestazioni si applicano a un individuo o alla famiglia. |

## `exception` {#exception}

`exception` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Struttura eccezione](../../../images/healthcare/field-groups/coverage/exception.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Codice dell&#39;eccezione specifica. |
| [!UICONTROL Periodo] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | L’intervallo di tempo in cui l’eccezione è attiva. |

## `paymentBy` {#payment-by}

`paymentBy` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![Pagamento per struttura](../../../images/healthcare/field-groups/coverage/payment-by.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Parte] | `party` | [[!UICONTROL Riferimento]](../data-types/reference.md) | L’elenco dei soggetti che erogano pagamenti non assicurativi per i costi del trattamento. |
| [!UICONTROL Responsabilità] | `responsibility` | Stringa | La descrizione della responsabilità finanziaria. |
