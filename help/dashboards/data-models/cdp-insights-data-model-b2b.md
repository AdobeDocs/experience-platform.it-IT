---
title: Real-Time Customer Data Platform Insights Data Model B2B edition
description: Scopri come utilizzare le query SQL con Real-Time Customer Data Platform Insights Data Models (B2B edition) per personalizzare i rapporti di Real-Time CDP per i casi d’uso di marketing e KPI.
badgeB2B: null
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
source-git-commit: a32064848809d1cad07f769f04d82c35df451e38
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 1%

---

# Modello dati Real-Time CDP Insights B2B edition

Il modello dati di Real-Time CDP Insights per B2B edition espone i modelli di dati e le istruzioni SQL che alimentano le informazioni per [profili account](https://experienceleague.adobe.com/it/docs/experience-platform/rtcdp/account/account-profile-overview). Puoi personalizzare questi modelli di query SQL per creare rapporti Real-Time CDP per i casi d’uso di marketing B2B e indicatori di prestazioni chiave (KPI, Key Performance Indicator). Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard.

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il pacchetto Real-Time CDP Prime e Ultimate. Per ulteriori informazioni, consulta la documentazione sulle [edizioni di Real-Time CDP](../../rtcdp/overview.md#rtcdp-editions) disponibili oppure contatta il tuo rappresentante Adobe.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).
 -->

## Prerequisiti

Questa guida richiede una buona conoscenza delle dashboard personalizzate. Leggi la documentazione su [come creare un dashboard personalizzato](../standard-dashboards.md) prima di continuare con questa guida.

## Rapporti e casi d’uso di Real-Time CDP B2B insight {#B2B-insight-reports-and-use-cases}

Il reporting B2B di Real-Time CDP fornisce informazioni approfondite sui dati dei profili dell’account e sulla relazione tra account e opportunità. I seguenti modelli di schema a stella sono stati sviluppati per rispondere a una serie di casi d’uso comuni di marketing e ogni modello di dati può supportare diversi casi d’uso.

>[!IMPORTANT]
>
>I dati utilizzati per il reporting B2B di Real-Time CDP sono accurati per un criterio di unione scelto e dall’istantanea giornaliera più recente.

### Modello del profilo account {#account-profile-model}

Il modello Profilo account è costituito da otto set di dati:

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

Il diagramma seguente mostra i campi di dati rilevanti in ciascun set di dati, il loro tipo di dati e le chiavi esterne che collegano i set di dati.

![Diagramma relazionale dell&#39;entità per il modello del profilo account.](../images/data-models/account-profile-model.png)

#### Il nuovo caso d’uso account per settore {#accounts-by-industry}

La logica utilizzata per l&#39;insight [!UICONTROL New accounts by industry] restituisce i primi cinque settori in base al numero di profili di account e alle relative dimensioni reciproche. Per ulteriori informazioni, vedere la documentazione del widget [[!UICONTROL New accounts By Industry]](../guides/account-profiles.md#accounts-by-industry).

>[!TIP]
>
>È possibile personalizzare questa query SQL per restituire un numero maggiore o minore di quello dei primi cinque settori.

L&#39;istruzione SQL che genera l&#39;insight [!UICONTROL New accounts by industry] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
WITH RankedIndustries AS (
    SELECT
        i.industry,
        SUM(f.counts) AS total_accounts,
        ROW_NUMBER() OVER (ORDER BY SUM(f.counts) DESC) AS industry_rank
    FROM
        adwh_fact_account f
    INNER JOIN adwh_dim_industry i ON f.industry_id = i.industry_id
    WHERE f.accounts_created_date between UPPER(COALESCE('$START_DATE', '')) and UPPER(COALESCE('$END_DATE', ''))
    GROUP BY
        i.industry
)
SELECT
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END AS industry_group,
    SUM(total_accounts) AS total_accounts
FROM
    RankedIndustries
GROUP BY
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END
ORDER BY
    total_accounts DESC
LIMIT 5000;
```

+++

#### Caso di utilizzo: Nuovi account per tipo {#accounts-by-type}

La logica utilizzata per l&#39;insight [!UICONTROL New accounts by type] restituisce il raggruppamento numerico degli account per il relativo tipo. Questo insight può aiutare a guidare la strategia e le operazioni aziendali, incluse le strategie di allocazione delle risorse o di marketing. Per ulteriori informazioni, vedere la documentazione del widget [[!UICONTROL New accounts by type]](../guides/account-profiles.md#accounts-by-type).

L&#39;istruzione SQL che genera l&#39;insight [!UICONTROL New accounts by type] è visualizzata nella sezione comprimibile seguente.

+++Query SQL

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

### Modello di opportunità {#opportunity-model}

Il modello Opportunity è costituito da sette set di dati:

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

Il diagramma seguente mostra i campi di dati rilevanti in ogni set di dati.

![Diagramma relazionale dell&#39;entità per il modello di opportunità.](../images/data-models/opportunity-model.png)
