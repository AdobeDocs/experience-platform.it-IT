---
solution: Experience Platform
title: Classe di definizione del segmento
topic-legacy: overview
description: Questo documento fornisce una panoramica della classe di definizione del segmento in Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# [!UICONTROL Segment definition] Classe

&quot;[!UICONTROL Segment definition]&quot; è una classe Experience Data Model (XDM) standard che acquisisce i dettagli di una definizione di segmento. La classe include campi obbligatori, come ID e nome di un segmento, insieme ad altri attributi facoltativi. Questa classe deve essere utilizzata se inserisci in Adobe Experience Platform le definizioni di segmenti da sistemi esterni.

>[!NOTE]
>
>Questa classe deve essere utilizzata solo per acquisire informazioni sulle definizioni dei segmenti stesse. Per acquisire le informazioni sull’appartenenza al segmento nei dati del profilo, utilizza il mixin [Dettagli appartenenza al segmento](../mixins/profile/segmentation.md) nello schema [!UICONTROL XDM Individual Profile].

![](../images/classes/segment-definition.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Un oggetto contenente i seguenti campi [!UICONTROL DateTime]: <ul><li>`createDate`: La data e l’ora in cui la risorsa è stata creata nell’archivio dati, ad esempio la prima acquisizione dei dati.</li><li>`modifyDate`: Data e ora dell’ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non viene fornito un valore esplicito durante l’inserimento dei dati. Tuttavia, se lo desideri, puoi comunque scegliere di fornire i tuoi valori ID univoci.<br><br>È importante distinguere che questo campo  **non** rappresenta un&#39;identità correlata a una singola persona, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere invece relegati a [campi di identità](../schema/composition.md#identity). |
| `createdByBatchID` | ID del batch acquisito che ha causato la creazione del record. |
| `description` | Una descrizione per la definizione del segmento. |
| `identityMap` | Campo mappa che contiene un set di identità con spazi dei nomi per i singoli utenti a cui si applica il segmento. Questo campo viene aggiornato automaticamente dal sistema durante l’acquisizione dei dati di identità.<br /><br />Per ulteriori informazioni sul relativo caso d’uso, consulta la sezione sulle mappe di identità nelle  [nozioni di base sulla ](../schema/composition.md#identityMap) composizione degli schemi . |
| `modifiedByBatchID` | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;utente che ha modificato il record per l&#39;ultima volta. |
| `segmentName` | **(Obbligatorio)** Un nome per la definizione del segmento. |
| `segmentStatus` | Lo stato del segmento dal sistema esterno. Sono accettati i seguenti valori: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Numero di versione più recente della definizione del segmento. |
