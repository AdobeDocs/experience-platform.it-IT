---
title: Gruppo di campi schema obiettivo
description: Scopri il gruppo di campi Schema obiettivo.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 87715274-cc9d-41da-9ca7-1634903b4e8f
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---

# [!UICONTROL Obiettivo] gruppo di campi schema

[!UICONTROL L&#39;obiettivo] è un gruppo di campi dello schema standard per la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e la [[!DNL Provider class]](../../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcareGoal` che descrive gli obiettivi previsti per un paziente, un gruppo o un&#39;organizzazione di assistenza.

![Struttura del gruppo di campi](../../../images/healthcare/field-groups/goal/goal.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Stato conseguimento] | `achievementStatus` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Descrive la progressione, o la mancanza di progressione, verso l&#39;obiettivo contro il target. |
| [!UICONTROL Indirizzi] | `addresses` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Le condizioni e altri elementi della cartella clinica che devono essere affrontati dall’obiettivo. |
| [!UICONTROL Categoria] | `category` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Indica una categoria in cui rientra l’obiettivo, ad esempio dieta o comportamento. |
| [!UICONTROL Descrizione] | `description` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il codice o il testo che descrive l’obiettivo. |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Gli identificatori aziendali assegnati a questo obiettivo dall&#39;esecutore o da altri sistemi che rimangono costanti man mano che la risorsa viene aggiornata e si propaga da server a server. |
| [!UICONTROL Nota] | `note` | Array di [[!UICONTROL annotazione]](../data-types/annotation.md) | Commenti relativi all’obiettivo. |
| [!UICONTROL Risultato] | `outcome` | Array di [[!UICONTROL Riferimento codificabile]](../data-types/codeable-reference.md) | Identifica la modifica (o l’assenza di modifica) quando viene valutato lo stato dell’obiettivo. |
| [!UICONTROL Priorità] | `priority` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Identifica il livello di importanza concordato di comune accordo associato al raggiungimento o al mantenimento dell’obiettivo. |
| [!UICONTROL Source] | `source` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Indica la fonte dell’obiettivo, ad esempio il paziente o l’operatore sanitario. |
| [!UICONTROL Avvia concetto codificabile] | `startCodeableConcept` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | L’evento dopo il quale l’obiettivo dovrebbe quindi essere persuaso. |
| [!UICONTROL Oggetto |]`subject` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Identifica il paziente, il gruppo o l’organizzazione per cui viene stabilito l’obiettivo. |
| [!UICONTROL Target] | `target` | Array di oggetti | Indica la timeline di passaggi specifici nell’obiettivo. Per ulteriori informazioni, consulta la [sezione seguente](#target). |
| [!UICONTROL Continua] | `continous` | Booleano | Indica se dopo il raggiungimento dell’obiettivo è necessaria un’attività continuativa per sostenere l’obiettivo. |
| [!UICONTROL Stato ciclo di vita] | `lifecycleStatus` | Stringa | Stato del ciclo di vita dell’obiettivo. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL Data inizio] | `startDate` | Data | La data dopo la quale l’obiettivo deve iniziare a essere perseguito. |
| [!UICONTROL Data stato] | `statusDate` | Data | Identifica quando è stato creato lo stato. |
| [!UICONTROL Motivo dello stato] | `statusReason` | Stringa | Acquisisce il motivo dello stato corrente. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura di destinazione](../../../images/healthcare/field-groups/goal/target.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Concetto codificabile dettagliato] | `detailCodeableConcept` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il codice target da raggiungere per indicare il raggiungimento dell’obiettivo. |
| [!UICONTROL Quantità dettagliata] | `detailQuantity` | [[!UICONTROL Quantità]](../data-types/quantity.md) | Quantità target da raggiungere per indicare il raggiungimento dell&#39;obiettivo. |
| [!UICONTROL Intervallo dettagli] | `detailRange` | [[!UICONTROL Range]](../data-types/range.md) | L’intervallo di obiettivi da raggiungere per indicare il raggiungimento dell’obiettivo. |
| [!UICONTROL Rapporto dettagli] | `detailRatio` | [[!UICONTROL Rapporto]](../data-types/ratio.md) | Il rapporto target da raggiungere per indicare il raggiungimento dell’obiettivo. |
| [!UICONTROL Misura] | `measure` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Viene tracciato il parametro che contiene il valore. |
| [!UICONTROL Valore booleano dettagliato] | `detailBoolean` | Booleano | Indica il raggiungimento dell’obiettivo. |
| [!UICONTROL Intero dettagli] | `detailInteger` | Intero | Numero obiettivo da raggiungere per indicare il raggiungimento dell’obiettivo. |
| [!UICONTROL Stringa dettagli] | `detailString` | Stringa | Il valore obiettivo da raggiungere per indicare il raggiungimento dell’obiettivo. |
| [!UICONTROL Data di scadenza] | `dueDate` | Data | Data entro la quale il target deve essere raggiunto. |
