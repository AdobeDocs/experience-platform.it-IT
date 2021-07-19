---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;beacon;dettagli interazione;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati beacon
topic-legacy: overview
description: Questo documento fornisce una panoramica della classe Profilo individuale XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 4%

---

#  Tipo di dati beacon

 Beaconis un tipo di dati XDM standard che descrive il dispositivo wireless che comunica le informazioni di identità alle applicazioni mobili man mano che i dispositivi mobili rientrano nell’intervallo.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconMajor` | Doppio | I valori principali identificano e distinguono un gruppo e valori interi senza segno compresi tra 1 e 65.535. |
| `beaconMinor` | Doppio | Valori secondari identificano e distinguono un singolo e un numero intero senza segno compreso tra 1 e 65.535. |
| `proximity` | Stringa | Distanza stimata dal beacon. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#proximity) . |
| `proximityUUID` | Stringa | Un UUID di prossimità (Universally Unique Identifier) è un tipo speciale di identificatore utilizzato per distinguere i beacon nella rete da tutti gli altri beacon presenti nelle reti esterne al controllo. L’UUID di prossimità è configurato in un beacon, da trasmettere a dispositivi mobili nella gamma per identificare i beacon di un’organizzazione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di dati [!UICONTROL Beacon].

## Valori accettati per la prossimità {#proximity}

La tabella seguente illustra i valori accettati per `proximity` e i relativi significati associati:

| Valore | Descrizione |
| --- | --- |
| `immediate` | Entro pochi centimetri. |
| `near` | A meno di 10 metri di distanza. |
| `far` | A più di 10 metri di distanza. |
| `unknown` | Impossibile verificare la distanza, probabilmente a causa di un segnale debole. |
