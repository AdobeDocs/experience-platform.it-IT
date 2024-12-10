---
title: Classe ubicazione
description: Scopri la classe Location in Experience Data Model (XDM).
badgePrivateBeta: label="Beta privata" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1d100981-49fb-4f02-b2c6-324f9c541f76
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 7%

---

# [!UICONTROL Posizione] classe

In Experience Data Model (XDM), la classe [!UICONTROL Location] acquisisce informazioni sulla posizione di un evento live, ad esempio una sala viaggi o un&#39;arena sportiva.

![Struttura classe posizione](../../../images/healthcare/classes/location.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- | --- |
| [!UICONTROL Identificatore] | `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non è necessario specificarne un valore esplicito durante l&#39;acquisizione dei dati. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| [!UICONTROL Identificatore località] | `locationID` | [!UICONTROL Stringa] | Identificatore univoco della posizione. |
| [!UICONTROL Nome località] | `locationName` | [!UICONTROL Stringa] | Nome della posizione. |

La classe può essere estesa con il gruppo di campi [[!UICONTROL Posizione]](../field-groups/location.md) per descrivere ulteriori dettagli su una posizione.
