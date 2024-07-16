---
solution: Experience Platform
title: Classe definizione segmento
description: Scopri la classe di definizione dei segmenti in Experience Data Model (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# [!UICONTROL Definizione segmento] classe

&quot;[!UICONTROL Definizione segmento]&quot; è una classe XDM (Experience Data Model) standard che acquisisce i dettagli di una definizione segmento. La classe include campi obbligatori come l’ID e il nome di un pubblico, insieme ad altri attributi facoltativi. Questa classe deve essere utilizzata se inserisci in Adobe Experience Platform le definizioni dei segmenti da sistemi esterni.

>[!NOTE]
>
>Questa classe deve essere utilizzata solo per acquisire informazioni sulle definizioni dei segmenti stesse. Per acquisire informazioni sull&#39;iscrizione al pubblico nei dati del profilo, è necessario utilizzare il gruppo di campi [Dettagli sull&#39;iscrizione al segmento](../field-groups/profile/segmentation.md) nello schema [!UICONTROL Profilo individuale XDM].

![](../images/classes/segment-definition.png)

| Proprietà | Descrizione |
| --- | --- |
| `_repo` | Oggetto contenente i seguenti campi [!UICONTROL DateTime]: <ul><li>`createDate`: la data e l&#39;ora in cui la risorsa è stata creata nell&#39;archivio dati, ad esempio quando i dati sono stati acquisiti per la prima volta.</li><li>`modifyDate`: data e ora dell&#39;ultima modifica della risorsa.</li></ul> |
| `_id` | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l&#39;inserimento dei dati non verrà fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci.<br><br>È importante distinguere che questo campo **non** rappresenta un&#39;identità correlata a una singola persona, ma piuttosto il record dei dati stessi. I dati di identità relativi a una persona devono essere invece relegati a [campi di identità](../schema/composition.md#identity). |
| `createdByBatchID` | ID del batch acquisito che ha causato la creazione del record. |
| `description` | Una descrizione per la definizione del segmento. |
| `identityMap` | Un campo mappa che contiene un set di identità con spazio dei nomi per gli individui a cui si applica il pubblico. Per ulteriori informazioni sul caso d&#39;uso, consulta la sezione sulle mappe delle identità nelle [nozioni di base sulla composizione dello schema](../schema/composition.md#identityMap). |
| `modifiedByBatchID` | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `repositoryCreatedBy` | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | ID dell&#39;ultimo utente che ha modificato il record. |
| `segmentName` | **(Obbligatorio)** Nome per la definizione del segmento. |
| `segmentStatus` | Lo stato del pubblico dal sistema esterno. Sono accettati i seguenti valori: <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Numero di versione più recente della definizione del segmento. |

{style="table-layout:auto"}
