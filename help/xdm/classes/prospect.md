---
title: Classe profilo cliente individuale XDM
description: Scopri la classe XDM Individual Prospect Profile in Experience Data Model (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: f4ddcf14de7a5cec42b5ebc521203cfdd1498a9f
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# [!UICONTROL Prospect Profile individuale XDM] classe

In Experience Data Model (XDM), la classe [!UICONTROL XDM Individual Prospect Profile] acquisisce i profili di potenziali clienti solitamente provenienti dai partner dati per casi d&#39;uso principali di acquisizione clienti.

>[!NOTE]
>
>Per impostare un campo nel Profilo potenziale individuale XDM come identità, devi prima creare almeno uno spazio dei nomi ID partner. Per ulteriori informazioni sullo spazio dei nomi ID partner, consulta la [sezione sui tipi di identità](../../identity-service/features/namespaces.md).

![Diagramma dello schema della classe XDM Prospect.](../images/classes/individual-prospect-profile.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_repo` | Oggetto | Questa classe ti consente di inserire profili di potenziali clienti provenienti da fornitori di dati per incanalare i casi di utilizzo di acquisizione dei clienti. |
| `_repo.createDate` | [!UICONTROL DataOra] | La data e l’ora del server in cui la risorsa è stata creata nell’archivio. L’ora di creazione potrebbe essere la prima volta che viene caricato un file di risorse oppure che una directory viene creata dal server come directory principale di una nuova risorsa. La proprietà datetime deve essere conforme allo standard ISO 8601. Un esempio di questo formato è &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DataOra] | La data e l’ora del server in cui la risorsa è stata modificata l’ultima volta nell’archivio, ad esempio quando viene caricata una nuova versione di una risorsa o viene aggiunta o rimossa una risorsa secondaria di una directory. La proprietà datetime deve essere conforme allo standard ISO 8601. Un modulo di esempio è &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non fornisce un valore esplicito durante l&#39;acquisizione dei dati. Tuttavia, se lo desideri, puoi fornire valori ID univoci. |
| `createdByBatchID` | [!UICONTROL Stringa] | ID del batch acquisito che ha causato la creazione del record. |
| `modifiedByBatchID` | [!UICONTROL Stringa] | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `partnerID` | [!UICONTROL Stringa] | In genere, un identificatore pseudonimo univoco che identifica un singolo potenziale cliente potenziale. Per ulteriori informazioni sull&#39;ID partner e sugli altri tipi di identità disponibili in Adobe Experience Platform, consulta la documentazione sui [tipi di identità](../../identity-service/features/namespaces.md#identity-type). |
| `repositoryCreatedBy` | [!UICONTROL Stringa] | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | [!UICONTROL Stringa] | ID dell&#39;ultimo utente che ha modificato il record. Al momento della creazione del record, il valore `modifiedByUser` viene impostato come valore `createdByUser`. |

{style="table-layout:auto"}
