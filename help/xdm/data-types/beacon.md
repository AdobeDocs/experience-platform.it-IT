---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;beacon;dettagli interazione;datatype;data-type;data type;data type;
solution: Experience Platform
title: Tipo di dati beacon
description: Scopri la classe Profilo individuale XDM.
exl-id: a3767c8d-a009-49b4-81a4-b084b6e5101a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 17%

---

# Tipo di dati [!UICONTROL Beacon]

[!UICONTROL Beacon] è un tipo di dati XDM standard che descrive il dispositivo wireless che comunica le informazioni di identità alle applicazioni mobili quando i dispositivi mobili rientrano nell&#39;intervallo.

<img src="../images/data-types/beacon.png" width="450" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `beaconMajor` | Doppio | I valori maggiori identificano e distinguono un gruppo e valori interi senza segno compresi tra 1 e 65.535. |
| `beaconMinor` | Doppio | I valori minori identificano e distinguono un individuo e valori interi senza segno compresi tra 1 e 65.535. |
| `proximity` | Stringa | Distanza stimata dal beacon. Per informazioni sui valori e le definizioni accettati, vedere [appendice](#proximity). |
| `proximityUUID` | Stringa | Un UUID (Universally Unique Identifier) di prossimità è un tipo di identificatore utilizzato per distinguere i beacon nella tua rete da tutti gli altri beacon in reti che non puoi controllare. L’UUID di prossimità è configurato in un beacon per essere trasmesso a dispositivi mobili entro il raggio di portata al fine di identificare i beacon di un’organizzazione. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/beacon-interaction-details.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di dati [!UICONTROL Beacon].

## Valori accettati per prossimità {#proximity}

Nella tabella seguente vengono illustrati i valori accettati per `proximity` e i relativi significati associati:

| Valore | Descrizione |
| --- | --- |
| `immediate` | Entro pochi centimetri. |
| `near` | A meno di 10 metri. |
| `far` | A più di 10 metri. |
| `unknown` | Impossibile determinare la distanza, probabilmente a causa di un segnale debole. |
