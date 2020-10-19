---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;beacon;interaction details;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati beacon
topic: overview
description: Questo documento fornisce una panoramica della classe Profilo singolo XDM.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---


# [!UICONTROL Beacon] tipo di dati

[!UICONTROL Beacon] è un tipo di dati XDM standard che descrive il dispositivo wireless che comunica le informazioni di identità alle applicazioni mobili man mano che i dispositivi mobili rientrano nell&#39;intervallo.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconMajor` | Doppio | I valori principali identificano e distinguono i valori interi di un gruppo e non firmati compresi tra 1 e 65.535. |
| `beaconMinor` | Doppio | Valori secondari identificano e distinguono un singolo e un numero intero senza segno compreso tra 1 e 65.535. |
| `proximity` | Stringa | Distanza stimata dal beacon. Cfr. l&#39; [appendice](#proximity) per i valori e le definizioni accettati. |
| `proximityUUID` | Stringa | Un UUID di prossimità (Universally Unique Identifier) è un tipo speciale di identificatore utilizzato per distinguere i beacon nella rete da tutti gli altri beacon presenti nelle reti esterne al controllo. L&#39;UUID di prossimità è configurato in un beacon, da trasmettere ai dispositivi mobili nell&#39;intervallo per identificare i beacon di un&#39;organizzazione. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/beacon-interaction-details.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di [!UICONTROL Beacon] dati.

## Valori accettati per la prossimità {#proximity}

Nella tabella seguente sono riportati i valori accettati per `proximity` e i significati associati:

| Valore | Descrizione |
| --- | --- |
| `immediate` | Entro pochi centimetri. |
| `near` | A meno di 10 metri. |
| `far` | Più di 10 metri di distanza. |
| `unknown` | La distanza non è stata accertata, probabilmente a causa di un segnale debole. |