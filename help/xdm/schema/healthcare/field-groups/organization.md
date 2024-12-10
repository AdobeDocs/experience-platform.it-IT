---
title: Gruppo di campi schema organizzazione
description: Scopri il gruppo di campi Schema organizzazione.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: b0698d36-ebc3-4b76-adcc-1deb2cbb1564
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 6%

---

# [!UICONTROL Organizzazione] gruppo di campi dello schema

[!UICONTROL Organizzazione] è un gruppo di campi dello schema standard per la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) e la [[!DNL Provider class]](../../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcareOrganization` contenente informazioni relative a raggruppamenti di persone o organizzazioni con uno scopo comune.

![Struttura del gruppo di campi](../../../images/healthcare/field-groups/organization/organization.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| ---| --- | --- | --- |
| [!UICONTROL Dettagli contatto] | `contact` | Array di [[!UICONTROL Dettagli contatto estesi]](../data-types/extended-contact-detail.md) | I recapiti dei dispositivi di comunicazione disponibili per l’organizzazione specifica. Può includere indirizzi, numeri di telefono, numeri di fax, numeri di cellulare, indirizzi e-mail e siti web. |
| [!UICONTROL Punto finale] | `endpoint` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Endpoint tecnici che forniscono accesso ai servizi gestiti dall’organizzazione. |
| [!UICONTROL Identificatore] | `indentifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Identificatore utilizzato per identificare l’organizzazione su più sistemi diversi. |
| [!UICONTROL Parte Dell&#39;Organizzazione] | `partOf` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Organizzazione di cui fa parte questa organizzazione. |
| [!UICONTROL Qualifica] | `qualification` | Array di oggetti | Le certificazioni ufficiali, gli accreditamenti, la formazione, le designazioni e le licenze che autorizzano e/o in altro modo avallano la fornitura di assistenza da parte dell’organizzazione. Per ulteriori informazioni, consulta la [sezione seguente](#qualification). |
| [!UICONTROL Tipo] | `type` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il tipo di organizzazione che è. |
| [!UICONTROL Attivo] | `active` | Booleano | Indica se il record dell&#39;organizzazione è ancora in uso. |
| [!UICONTROL Alias] | `alias` | Array di stringhe | Un elenco di nomi alternativi noti all’organizzazione come o che erano noti in passato. |
| [!UICONTROL Descrizione] | `description` | Stringa | La descrizione dell’organizzazione che contribuisce a fornire il contesto generale per garantire che sia selezionata l’organizzazione corretta. |
| [!UICONTROL Nome] | `name` | Stringa | Il nome associato all’organizzazione. |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `qualification` {#qualification}

`qualification` viene fornito come array di oggetti. La struttura di ciascun oggetto è descritta di seguito.

![struttura delle qualifiche](../../../images/healthcare/field-groups/organization/qualification.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Codice] | `code` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Rappresentazione in codice della qualifica. |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Un identificatore assegnato a questa qualifica per questa organizzazione. |
| [!UICONTROL Emittente] | `issuer` | [[!UICONTROL Riferimento]](../data-types/reference.md) | Organizzazione che regola e rilascia la qualifica. |
| [!UICONTROL Periodo] | `period` | [[!UICONTROL Periodo]](../data-types/period.md) | Periodo di validità della qualifica. |
