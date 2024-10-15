---
title: Edizione B2B di Real-time Customer Data Platform Insights Data Model
description: Scopri come utilizzare le query SQL con Real-time Customer Data Platform Insights Data Models (B2B edition) per personalizzare i rapporti di Real-Time CDP per i casi d’uso di marketing e KPI.
badgeB2B: label="Edizione B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edizione B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Edizione B2B del modello dati di Real-time Customer Data Platform Insights

Il modello dati di Real-time Customer Data Platform Insights per B2B edition espone i modelli di dati e le istruzioni SQL che alimentano le informazioni per [profili account](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview). Puoi personalizzare questi modelli di query SQL per creare rapporti Real-Time CDP per i casi d’uso di marketing B2B e indicatori di prestazioni chiave (KPI, Key Performance Indicator). Queste informazioni possono quindi essere utilizzate come widget personalizzati per le dashboard.

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il pacchetto Real-Time CDP Prime e Ultimate. Per ulteriori informazioni, consulta la documentazione sulle [edizioni Real-Time CDP](../../rtcdp/overview.md#rtcdp-editions) disponibili oppure contatta il tuo rappresentante di Adobe.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/sql-insights/reporting-insights-data-model.md).
 -->

## Prerequisiti

Questa guida richiede una buona conoscenza delle dashboard personalizzate. Leggi la documentazione su [come creare un dashboard personalizzato](../standard-dashboards.md) prima di continuare con questa guida.

## Rapporti di approfondimento B2B di Real-Time CDP e casi d’uso {#B2B-insight-reports-and-use-cases}

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

La logica utilizzata per [!UICONTROL Nuovi account per settore] insight restituisce i primi cinque settori in base al numero di profili di account e alle loro dimensioni relative tra loro. Per ulteriori informazioni, consulta la [[!UICONTROL documentazione dei nuovi account per settore] widget](../guides/account-profiles.md#accounts-by-industry).

>[!TIP]
>
>È possibile personalizzare questa query SQL per restituire un numero maggiore o minore di quello dei primi cinque settori.

L&#39;istruzione SQL che genera i [!UICONTROL nuovi account per settore] approfondimenti è visualizzata nella sezione comprimibile seguente.

Query +++SQL

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

La logica utilizzata per [!UICONTROL Nuovi account per tipo] insight restituisce il raggruppamento numerico degli account per il relativo tipo. Questa informazione può essere utile per guidare la strategia e le operazioni aziendali, incluse le strategie di allocazione delle risorse o di marketing. Per ulteriori informazioni, consulta la [[!UICONTROL documentazione dei nuovi account per tipo] widget](../guides/account-profiles.md#accounts-by-type).

L&#39;istruzione SQL che genera l&#39;approfondimento [!UICONTROL Nuovi account per tipo] è visualizzata nella sezione comprimibile seguente.

Query +++SQL

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
