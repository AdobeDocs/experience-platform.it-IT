---
title: Modello dati sanitario V2
description: Scopri alcuni casi d’uso comuni per l’assistenza sanitaria, le classi migliori, i gruppi di campi correlati e i tipi di dati da utilizzare.
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: 36f1a443eda47917d5b6bd84d4765ff044b5093a
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 12%

---

# [!UICONTROL Healthcare] Data Model V2

## Gruppi di campi e classi {#field-groups}

La tabella seguente illustra le classi e i gruppi di campi di schema consigliati per diversi casi d’uso comuni di assistenza sanitaria.

<table>
  <thead>
    <tr>
      <th>Casi d’uso</th>
      <th>Gruppi di campi</th>
      <th>Classi compatibili</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Crea/aggiorna paziente</strong>: quando un paziente arriva al front desk dell'ospedale, viene creata una cartella clinica del paziente contenente dettagli demografici come un identificatore (facoltativo), il nome del paziente, la data di nascita, il genere e l'indirizzo. Questo è un componente essenziale dell'IT per il settore sanitario.</td>
      <td><a href="./field-groups/patient.md">Paziente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Vaccinazione</strong>: facilitazione del processo di vaccinazione, gestione dei record di vaccinazione dei pazienti e integrazione di EMR con i sistemi di gestione dei vaccini.</td>
      <td><a href="./field-groups/immunization.md">Immunizzazione</a></td>
      <td>
        <li><a href="../../classes/experienceevent.md">Evento esperienza XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/patient.md">Paziente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Posizione</a></td>
      <td>
        <li><a href="./classes/location.md">Posizione</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication.md">Medicinale</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicinale</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">Distribuzione di medicinali</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicinale</a></li>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">Richiesta di medicinale</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicinale</a></li>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Adesione post-terapia</strong>: motivare i pazienti e gli assistenti a completare i piani di trattamento e ridurre le percentuali di rimesse.</td>
      <td><a href="./field-groups/patient.md">Paziente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Posizione</a></td>
      <td>
        <li><a href="./classes/location.md">Posizione</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/care-plan.md">Piano di assistenza</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/goal.md">Obiettivo</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>Esperienza del consumatore per l'assicurazione</strong>: migliora l'acquisizione digitale e le esperienze tra i consumatori che acquistano un'assicurazione. Gli esempi includono: 
        <li> Comprensione del comportamento dei consumatori nell’inviare e-mail promozionali o annunci mirati di terze parti a persone che accedono a pagine contenenti informazioni generali (come piani, nomi dei piani/livelli, Medicaid o programmi per il benessere)
        </li> 
        <li> Invio di informazioni relative al vaccino sulla salute cardiaca per creare consapevolezza del marchio o richieste di programmazione di vaccini a persone alla ricerca di informazioni sulla salute cardiaca e sui vaccini.
        </li>
      </td>
      <td><a href="./field-groups/patient.md">Paziente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/coverage.md">Copertura</a></td>
      <td>
        <li><a href="../../classes/plan.md">Piano</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/account.md">Account</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Posizione</a></td>
      <td>
        <li><a href="./classes/location.md">Posizione</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="./field-groups/medication.md">Medicinale</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicinale</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-dispense.md">Distribuzione di medicinali</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicinale</a></li>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/medication-request.md">Richiesta di medicinale</a></td>
      <td>
        <li><a href="../../classes/medication.md">Medicinale</a></li>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>Esperienza provider migliorata</strong>: utilizzo dei dati del provider dal sistema EMR per suggerire provider alternativi in base alla disponibilità, alla posizione e alla specializzazione degli appuntamenti. <br> <br>Miglioramento delle ricerche dei provider per visualizzare i risultati con la disponibilità desiderata, verifica che il provider selezionato faccia parte della rete di payor e fornitura di stime dei costi.
      </td>
      <td><a href="./field-groups/patient.md">Paziente</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/location.md">Posizione</a></td>
      <td>
        <li><a href="./classes/location.md">Posizione</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/organization.md">Organizzazione</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/practioner.md">Professionista</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="./field-groups/schedule.md">Pianificazione</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">Profilo individuale XDM</a></li>
        <li><a href="../../classes/provider.md">Provider</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Tipi di dati {#data-types}

La tabella seguente illustra i tipi di dati creati in base alle specifiche [!DNL HL7 FHIR Release 5].

| Nome | Descrizione |
| --- | --- |
| [[!UICONTROL Indirizzo]](./data-types/address.md) | Descrive un indirizzo espresso utilizzando le convenzioni postali (anziché il formato GPS o altri formati di definizione della posizione). |
| [[!UICONTROL Annotazione]](./data-types/annotation.md) | Un nodo di testo con attribuzione all’autore. |
| [[!UICONTROL Disponibilità]](./data-types/availability.md) | Dati sulla disponibilità di un elemento. |
| [[!UICONTROL Concetto codificabile]](./data-types/codeable-concept.md) | Riferimento da una risorsa a un&#39;altra. |
| [[!UICONTROL Riferimento codificabile]](./data-types/codeable-reference.md) | Riferimento a una risorsa o a un concetto. |
| [[!UICONTROL Codifica]](./data-types/coding.md) | Riferimento a un codice definito da un sistema terminologico. |
| [[!UICONTROL Punto di contatto]](./data-types/contact-point.md) | Dettagli di contatto di una persona. |
| [[!UICONTROL Dosaggio]](./data-types/dosage.md) | Come il medicinale è/è stato assunto o deve essere assunto. |
| [[!UICONTROL Durata]](./data-types/duration.md) | Un periodo di tempo. |
| [[!UICONTROL Dettagli di contatto estesi]](./data-types/extended-contact-detail.md) | Informazioni di un contatto esteso. |
| [[!UICONTROL Nome umano]](./data-types/human-name.md) | Informazioni sul nome di un&#39;entità umana o di un&#39;altra entità vivente. |
| [[!UICONTROL Identificatore]](./data-types/identifier.md) | Identificatore destinato al calcolo. |
| [[!UICONTROL Soldi]](./data-types/money.md) | Una quantità di utilità economica in una valuta riconosciuta. |
| [[!UICONTROL Periodo]](./data-types/period.md) | Un periodo di tempo definito da una data/ora di inizio e di fine. |
| [[!UICONTROL Persona]](./data-types/person.md) | Informazioni su un record persona generico. |
| [[!UICONTROL Quantità]](./data-types/quantity.md) | Un importo misurato o misurabile. |
| [[!UICONTROL Range]](./data-types/range.md) | Un insieme di valori associati a valori minimi e massimi. |
| [[!UICONTROL Rapporto]](./data-types/ratio.md) | Un rapporto di due valori [[!UICONTROL Quantity]](./data-types/quantity.md) tramite un numeratore e un denominatore. |
| [[!UICONTROL Riferimento]](./data-types/reference.md) | Riferimento da una risorsa a un&#39;altra. |
| [[!UICONTROL Ripeti]](./data-types/repeat.md) | Un set di regole che descrivono quando un evento è pianificato. |
| [[!UICONTROL Quantità semplice]](./data-types/simple-quantity.md) | Un importo misurato o misurabile. |
| [[!UICONTROL Intervallo]](./data-types/timing.md) | Informazioni su un evento che può verificarsi più volte. |
| [[!UICONTROL Dettagli servizio virtuale]](./data-types/virtual-service-detail.md) | Dettagli di contatto del servizio virtuale. |
