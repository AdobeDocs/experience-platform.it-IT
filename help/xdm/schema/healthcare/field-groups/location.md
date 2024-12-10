---
title: Gruppo di campi dello schema posizione
description: Scopri il gruppo di campi Schema posizione.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 99831093-89da-4329-be29-c130c1d48f63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 5%

---

# Gruppo di campi schema [!UICONTROL Posizione]

[!UICONTROL Posizione] è un gruppo di campi dello schema standard per la [[!DNL Location] classe](../classes/location.md). Fornisce un singolo campo di tipo oggetto `healthcareLocation` che acquisisce dettagli e informazioni sulla posizione per un luogo.

![Struttura del gruppo di campi](../../../images/healthcare/field-groups/location.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Indirizzo] | `address` | [[!UICONTROL Indirizzo]](../data-types/address.md) | Indirizzo del luogo fisico. |
| [!UICONTROL Caratteristica] | `characteristic` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Una raccolta delle caratteristiche della posizione. |
| [!UICONTROL Contatto] | `contact` | Array di [[!UICONTROL Dettagli contatto estesi]](../data-types/extended-contact-detail.md) | I dettagli di contatto per la posizione. |
| [!UICONTROL Endpoint] | `endpoint` | Array di [[!UICONTROL Riferimento]](../data-types/reference.md) | Gli endpoint tecnici che forniscono accesso ai servizi operativi per la sede. |
| [!UICONTROL Modulo] | `form` | [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | La forma fisica della posizione. |
| [!UICONTROL Ore di funzionamento] | `hoursOfOperation` | Array di [[!UICONTROL Disponibilità]](../data-types/availability.md) | Giorni e ore in cui questa posizione è generalmente aperta (incluse le eccezioni). |
| [!UICONTROL Identificatore] | `identifier` | Array di [[!UICONTROL Identificatore]](../data-types/identifier.md) | Il codice o il numero univoco che identifica la posizione. |
| [!UICONTROL Gestione dell&#39;organizzazione] | `managingOrganization` | [[!UICONTROL Riferimento]](../data-types/reference.md) | L’organizzazione responsabile del provisioning e della manutenzione. |
| [!UICONTROL Stato operativo] | `operationalStatus` | [[!UICONTROL Codifica]](../data-types/coding.md) | Stato operativo della posizione. |
| [!UICONTROL Parte Del Percorso] | `partOf` | [[!UICONTROL Riferimento]](../data-types/reference.md) | La posizione di cui fa parte questa posizione. |
| [!UICONTROL Posizione] | `position` | Oggetto | La posizione geografica assoluta. Contiene tre proprietà in formato Doppio: <li>`longitude`: longitudine con riferimento WGS84</li> <li>`latitude`: Latitude con Riferimento WGS84.</li> <li>`altitude`: altitudine con riferimento WGS84.</li> |
| [!UICONTROL Tipo] | `type` | Array di [[!UICONTROL Concetto codificabile]](../data-types/codeable-concept.md) | Il tipo di funzione eseguita nella posizione. |
| [!UICONTROL Servizio virtuale] | `virtualService` | Array di [[!UICONTROL Dettagli servizio virtuale]](../data-types/virtual-service-detail.md) | Dettagli di connessione di un servizio virtuale. |
| [!UICONTROL Alias] | `alias` | Array di stringhe | Un elenco di nomi alternativi denominati posizione. |
| [!UICONTROL Descrizione] | `description` | Stringa | Ulteriori informazioni per identificare la posizione oltre il nome. |
| [!UICONTROL Modalità] | `mode` | Stringa | Modalità della posizione. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL Nome] | `name` | Stringa | Nome della posizione. |
| [!UICONTROL Stato] | `status` | Stringa | Stato della posizione. Il valore di questa proprietà deve essere uguale a uno dei seguenti valori enum noti. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)
