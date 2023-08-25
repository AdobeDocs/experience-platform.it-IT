---
title: Classe profilo cliente individuale XDM
description: Questo documento fornisce una panoramica della classe XDM Individual Prospect Profile in Experience Data Model (XDM).
source-git-commit: 437bd602462330a96f356b83d7afe922b5315d9f
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# [!UICONTROL Profilo potenziale individuale XDM] classe

In Experience Data Model (XDM), la [!UICONTROL Profilo potenziale individuale XDM] la classe acquisisce i profili di potenziali clienti in genere provenienti dai partner dati per casi d’uso di acquisizione clienti top-of-the-funnel.

![Il diagramma dello schema della classe Prospect XDM.](../images/classes/individual-prospect-profile.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `_repo` | Oggetto | Questa classe ti consente di inserire profili di potenziali clienti provenienti da fornitori di dati per incanalare i casi di utilizzo di acquisizione dei clienti. |
| `_repo.createDate` | [!UICONTROL DateTime] | La data e l’ora del server in cui la risorsa è stata creata nell’archivio. L’ora di creazione potrebbe essere la prima volta che viene caricato un file di risorse oppure che una directory viene creata dal server come directory principale di una nuova risorsa. La proprietà datetime deve essere conforme allo standard ISO 8601. Un esempio di questo formato è &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | La data e l’ora del server in cui la risorsa è stata modificata l’ultima volta nell’archivio, ad esempio quando viene caricata una nuova versione di una risorsa o viene aggiunta o rimossa una risorsa secondaria di una directory. La proprietà datetime deve essere conforme allo standard ISO 8601. Un modulo di esempio è &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non fornisce un valore esplicito durante l’acquisizione dei dati. Tuttavia, se lo desideri, puoi fornire valori ID univoci. |
| `createdByBatchID` | [!UICONTROL Stringa] | ID del batch acquisito che ha causato la creazione del record. |
| `modifiedByBatchID` | [!UICONTROL Stringa] | ID dell’ultimo batch acquisito che ha causato l’aggiornamento del record. |
| `partnerID` | [!UICONTROL Stringa] | In genere, un identificatore pseudonimo univoco che identifica un singolo potenziale cliente potenziale. Consulta la documentazione su [tipi di identità](../../identity-service/namespaces.md#identity-types) per ulteriori informazioni sul Partner ID e sugli altri tipi di identità disponibili in Adobe Experience Platform. |
| `repositoryCreatedBy` | [!UICONTROL Stringa] | ID dell&#39;utente che ha creato il record. |
| `repositoryLastModifiedBy` | [!UICONTROL Stringa] | ID dell&#39;ultimo utente che ha modificato il record. Al momento della creazione del record, `modifiedByUser` viene impostato come `createdByUser` valore. |

{style="table-layout:auto"}
