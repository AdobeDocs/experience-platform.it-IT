---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;beacon;dettagli interazione;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati beacon
description: Questo documento fornisce una panoramica della classe Profilo individuale XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 4%

---

# [!UICONTROL Beacon] tipo di dati

[!UICONTROL Beacon] è un tipo di dati XDM standard che descrive il dispositivo wireless che comunica informazioni di identità alle applicazioni mobili quando i dispositivi mobili rientrano nel raggio d’azione.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconMajor` | Doppio | I valori principali identificano e distinguono un gruppo e valori interi senza segno compresi tra 1 e 65.535. |
| `beaconMinor` | Doppio | I valori minori identificano e distinguono un individuo e valori interi senza segno compresi tra 1 e 65.535. |
| `proximity` | Stringa | Distanza stimata dal beacon. Consulta la [appendice](#proximity) per i valori e le definizioni accettati. |
| `proximityUUID` | Stringa | Un UUID (Universally Unique Identifier) di prossimità è un tipo di identificatore utilizzato per distinguere i beacon nella tua rete da tutti gli altri beacon in reti che non puoi controllare. L’UUID di prossimità è configurato in un beacon per essere trasmesso a dispositivi mobili entro il raggio di portata al fine di identificare i beacon di un’organizzazione. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sulle [!UICONTROL Beacon] tipo di dati.

## Valori accettati per prossimità {#proximity}

La tabella seguente illustra i valori accettati per `proximity` e il significato associato:

| Valore | Descrizione |
| --- | --- |
| `immediate` | Entro pochi centimetri. |
| `near` | A meno di 10 metri. |
| `far` | A più di 10 metri. |
| `unknown` | Impossibile determinare la distanza, probabilmente a causa di un segnale debole. |
