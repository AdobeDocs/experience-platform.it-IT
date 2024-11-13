---
title: Informazioni sul profilo account
description: Scopri il linguaggio SQL che attiva le informazioni sul profilo account e utilizza queste query per generare informazioni personalizzate che esplorano ulteriormente i clienti e le loro esperienze utente.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edizione B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: f9ef0e25dac1715bbb6d73db52d6368c543bf7ec
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Informazioni sul profilo account

[I profili account](../../rtcdp/accounts/account-profile-overview.md) vengono utilizzati per consolidare le informazioni sull&#39;account da varie origini, inclusi più canali di marketing e sistemi organizzativi. Questa visualizzazione unificata consente una comprensione completa degli account dei clienti, migliorando le campagne di marketing B2B. Le informazioni derivate dall’analisi del modello dati rendono i dati B2B di Adobe Real-time Customer Data Platform più accessibili, comprensibili e di impatto per il processo decisionale.

Grazie all’accesso al linguaggio SQL che potenzia le tue conoscenze, potrai comprendere meglio i dati B2B e generare informazioni riutilizzabili personalizzate per esplorare ulteriormente le informazioni sull’account del cliente. Trasforma i dati non elaborati in nuove informazioni fruibili utilizzando l’SQL esistente del modello dati di Real-Time CDP come ispirazione per creare query per le tue esigenze aziendali specifiche.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Tutte le informazioni seguenti sono disponibili per l&#39;utilizzo come parte del [dashboard dei profili account](../guides/account-profiles.md) o di un [dashboard personalizzato](../standard-dashboards.md). Consulta la [panoramica sulla personalizzazione](../customize/overview.md) per istruzioni su come personalizzare il dashboard o [creare e modificare nuovi widget](../customize/custom-widgets.md) nella libreria di widget e [dashboard definito dall&#39;utente](../standard-dashboards.md#create-widget).

## Profili account aggiunti {#account-profiles-added}

Domande a cui questa informazione ha risposto:

- Quanti profili di account sono stati aggiunti in un determinato periodo?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## Nuovi account per settore {#accounts-by-industry}

Domande a cui questa informazione ha risposto:

- Quali sono i primi cinque settori a cui appartengono i profili account?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## Nuovi account per tipo {#accounts-by-type}

Domande a cui questa informazione ha risposto:

- Qual è il numero di account in base al tipo?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

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

## Opportunità aggiunte {#opportunities-added}

Domande a cui questa informazione ha risposto:

- Quante opportunità sono state aggiunte in un determinato periodo?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## Nuove opportunità per ruolo persona {#opportunities-by-person-role}

Domande a cui questa informazione ha risposto:

- Qual è la dimensione relativa e il conteggio dei vari ruoli in un’opportunità?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## Nuove opportunità in base ai ricavi {#opportunities-by-revenue}

Domande a cui questa informazione ha risposto:

- Quali sono le prime 20 opportunità classificate in base ai ricavi (in USD)?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## Nuove opportunità per stato e fase {#opportunities-by-status-and-stage}

Domande a cui questa informazione ha risposto:

- Quali sono le opportunità aperte e in quale fase del funnel di vendita o marketing?
- Quali sono le opportunità chiuse e in quale fase del funnel di vendita o marketing?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## Nuove opportunità realizzate {#opportunities-won}

Domande a cui questa informazione ha risposto:

- Qual è il numero di opportunità chiuse o finalizzate correttamente?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## Opportunità realizzate (grafico a linee) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Domande a cui questa informazione ha risposto:

- Quante opportunità sono state chiuse o finalizzate in un determinato periodo?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## Panoramica sui clienti per account {#customers-per-account-overview}

>[!NOTE]
>
>Il grafico [!UICONTROL Panoramica clienti per account] include tre approfondimenti drill-through: [!UICONTROL Dettagli clienti per account], [!UICONTROL Panoramica opportunità per account] e [!UICONTROL Dettagli opportunità per account]. Questi drill-through forniscono informazioni più granulari, suddividendo il conteggio di clienti e opportunità per categorie (come clienti diretti e indiretti) e intervalli (come fasce di conteggio di clienti e opportunità). Questi grafici non sono influenzati dai filtri date globali eventualmente impostati.

Domande a cui questa informazione ha risposto:

- Qual è la distribuzione dei conti in base al fatto che abbiano clienti diretti o indiretti?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH LatestDate AS (SELECT MAX(inserted_date) AS max_inserted_date FROM adwh_b2b_account_person_association),
     CategorizedData AS (
         SELECT CASE 
                    WHEN is_direct = 'true' AND person_count = 0 THEN 'Accounts without Direct Customers' 
                    WHEN is_direct = 'false' AND person_count = 0 THEN 'Accounts without Indirect Customers' 
                    WHEN is_direct = 'true' AND person_count > 0 THEN 'Accounts with Direct Customers' 
                    WHEN is_direct = 'false' AND person_count > 0 THEN 'Accounts with Indirect Customers' 
                END AS Account_Category, 
                account_count 
         FROM adwh_b2b_account_person_association 
         WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
     ),
     AggregatedData AS (
         SELECT Account_Category, SUM(account_count) AS Accounts 
         FROM CategorizedData 
         GROUP BY Account_Category
     ),
     AllCategories AS (
         SELECT 'Accounts without Direct Customers' AS Account_Category 
         UNION ALL SELECT 'Accounts without Indirect Customers' 
         UNION ALL SELECT 'Accounts with Direct Customers' 
         UNION ALL SELECT 'Accounts with Indirect Customers'
     )
SELECT ac.Account_Category AS Account_Category, COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad ON ac.Account_Category = ad.Account_Category 
ORDER BY ac.Account_Category;
```

+++

## Dettagli clienti per account {#customers-per-account-detail}

>[!NOTE]
>
>Questa informazione non è influenzata dai filtri data globali.

Domande a cui questa informazione ha risposto:

- Quanti account hanno diversi intervalli di clienti diretti o indiretti?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH customer_ranges AS (
    SELECT 'Direct Customer' AS customer_type, '1-10 Customers' AS person_range 
    UNION ALL
    SELECT 'Direct Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Direct Customer', '1000+ Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1-10 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '11-100 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '101-1000 Customers' 
    UNION ALL
    SELECT 'Indirect Customer', '1000+ Customers'
)
SELECT 
    cr.customer_type, 
    cr.person_range, 
    COALESCE(SUM(ap.account_count), 0) AS Accounts
FROM customer_ranges cr
LEFT JOIN (
    SELECT 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END AS customer_type,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END AS person_range,
        SUM(account_count) AS account_count
    FROM adwh_b2b_account_person_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_person_association) 
    GROUP BY 
        CASE 
            WHEN is_direct = 'true' THEN 'Direct Customer' 
            ELSE 'Indirect Customer' 
        END,
        CASE 
            WHEN person_count BETWEEN 1 AND 10 THEN '1-10 Customers' 
            WHEN person_count BETWEEN 11 AND 100 THEN '11-100 Customers' 
            WHEN person_count BETWEEN 101 AND 1000 THEN '101-1000 Customers' 
            WHEN person_count > 1000 THEN '1000+ Customers' 
        END
) ap ON cr.customer_type = ap.customer_type AND cr.person_range = ap.person_range
GROUP BY cr.customer_type, cr.person_range
ORDER BY cr.customer_type, 
    CASE cr.person_range 
        WHEN '1-10 Customers' THEN 1 
        WHEN '11-100 Customers' THEN 2 
        WHEN '101-1000 Customers' THEN 3 
        WHEN '1000+ Customers' THEN 4 
    END;
```

+++

## Panoramica sulle opportunità per account {#opportunities-per-account-overview}

>[!NOTE]
>
>Questa informazione non è influenzata dai filtri data globali.

Domande a cui questa informazione ha risposto:

- Qual è la distribuzione dei conti in base al fatto che abbiano o meno opportunità associate?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH LatestDate AS (
    SELECT MAX(inserted_date) AS max_inserted_date 
    FROM adwh_b2b_account_opportunity_association
),
CategorizedData AS (
    SELECT 
        CASE 
            WHEN opportunity_count = 0 THEN 'Accounts without Opportunities'
            WHEN opportunity_count > 0 THEN 'Accounts with Opportunities'
        END AS Opportunity_Category, 
        account_count 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT max_inserted_date FROM LatestDate)
),
AggregatedData AS (
    SELECT 
        Opportunity_Category,
        SUM(account_count) AS Accounts 
    FROM CategorizedData 
    GROUP BY Opportunity_Category
),
AllCategories AS (
    SELECT 'Accounts without Opportunities' AS Opportunity_Category 
    UNION ALL 
    SELECT 'Accounts with Opportunities'
)
SELECT 
    ac.Opportunity_Category AS Opportunity_Category, 
    COALESCE(ad.Accounts, 0) AS Accounts 
FROM AllCategories ac 
LEFT JOIN AggregatedData ad 
    ON ac.Opportunity_Category = ad.Opportunity_Category 
ORDER BY ac.Opportunity_Category;
```

+++

## Dettagli opportunità per conto {#opportunities-per-account-detail}

>[!NOTE]
>
>Questa informazione non è influenzata dai filtri data globali.

Domande a cui questa informazione ha risposto:

- Quanti account hanno diversi intervalli di opportunità associate?

+++Seleziona questa opzione per visualizzare il codice SQL che genera questa informazione approfondita

```sql
WITH opportunity_ranges AS (
    SELECT '1-10 Opportunities' AS opportunity_range 
    UNION ALL 
    SELECT '11-50 Opportunities' 
    UNION ALL 
    SELECT '51-100 Opportunities' 
    UNION ALL 
    SELECT '100+ Opportunities'
)
SELECT opportunity_ranges.opportunity_range AS OPPORTUNITIES, 
       COALESCE(SUM(accounts.total_accounts), 0) AS ACCOUNTS 
FROM opportunity_ranges 
LEFT JOIN (
    SELECT 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END AS opportunity_range, 
        SUM(account_count) AS total_accounts 
    FROM adwh_b2b_account_opportunity_association 
    WHERE inserted_date = (SELECT MAX(inserted_date) FROM adwh_b2b_account_opportunity_association) 
      AND opportunity_count > 0 
    GROUP BY 
        CASE 
            WHEN opportunity_count BETWEEN 1 AND 10 THEN '1-10 Opportunities' 
            WHEN opportunity_count BETWEEN 11 AND 50 THEN '11-50 Opportunities' 
            WHEN opportunity_count BETWEEN 51 AND 100 THEN '51-100 Opportunities' 
            WHEN opportunity_count > 100 THEN '100+ Opportunities' 
        END
) AS accounts ON opportunity_ranges.opportunity_range = accounts.opportunity_range 
GROUP BY opportunity_ranges.opportunity_range 
ORDER BY CASE opportunity_ranges.opportunity_range 
            WHEN '1-10 Opportunities' THEN 1 
            WHEN '11-50 Opportunities' THEN 2 
            WHEN '51-100 Opportunities' THEN 3 
            WHEN '100+ Opportunities' THEN 4 
        END;
```

+++

## Passaggi successivi

Una volta letto questo documento, sarai in grado di comprendere il codice SQL che genera le informazioni approfondite sul dashboard del profilo account e le domande comuni che questa analisi risolve. Ora puoi modificare e ripetere le istruzioni SQL per generare informazioni personalizzate. Per informazioni su come generare informazioni personalizzate con SQL, consulta la [panoramica sulla modalità Query Pro](../sql-insights-query-pro-mode/overview.md).

È inoltre possibile leggere e comprendere l&#39;istruzione SQL che genera informazioni approfondite per le dashboard [Profili](./profiles.md), [Tipi di pubblico](./audiences.md) e [Destinazioni](./destinations.md).
