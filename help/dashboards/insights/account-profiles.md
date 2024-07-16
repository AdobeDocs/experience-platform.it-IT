---
title: Informazioni sul profilo account
description: Scopri il linguaggio SQL che attiva le informazioni sul profilo account e utilizza queste query per generare informazioni personalizzate che esplorano ulteriormente i clienti e le loro esperienze utente.
badgeB2B: label="Edizione B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edizione B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: 8b6cd84a31f9cdccef9f342df7f7b8450c2405dc
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Informazioni sul profilo account

[I profili account](../../rtcdp/accounts/account-profile-overview.md) vengono utilizzati per consolidare le informazioni sull&#39;account da varie origini, inclusi più canali di marketing e sistemi organizzativi. Questa visualizzazione unificata consente una comprensione completa degli account dei clienti, migliorando le campagne di marketing B2B. Le informazioni derivate dall’analisi del modello dati rendono i dati B2B di Adobe Real-time Customer Data Platform più accessibili, comprensibili e di impatto per il processo decisionale.

Grazie all’accesso al linguaggio SQL che potenzia le tue conoscenze, potrai comprendere meglio i dati B2B e generare informazioni riutilizzabili personalizzate per esplorare ulteriormente le informazioni sull’account del cliente. Trasforma i dati non elaborati in nuove informazioni fruibili utilizzando l’SQL esistente del modello dati di Real-Time CDP come ispirazione per creare query per le tue esigenze aziendali specifiche.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Tutte le informazioni seguenti sono disponibili per l&#39;utilizzo come parte del [dashboard dei profili account](../guides/account-profiles.md) o di un [dashboard personalizzato](../user-defined-dashboards.md). Consulta la [panoramica sulla personalizzazione](../customize/overview.md) per istruzioni su come personalizzare il dashboard o [creare e modificare nuovi widget](../customize/custom-widgets.md) nella libreria di widget e [dashboard definito dall&#39;utente](../user-defined-dashboards.md#create-widget).

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

## Passaggi successivi

Una volta letto questo documento, sarai in grado di comprendere il codice SQL che genera le informazioni approfondite sul dashboard del profilo account e le domande comuni che questa analisi risolve. Ora puoi modificare e ripetere le istruzioni SQL per generare informazioni personalizzate.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

È inoltre possibile leggere e comprendere l&#39;istruzione SQL che genera informazioni approfondite per le dashboard [Profili](./profiles.md), [Tipi di pubblico](./audiences.md) e [Destinazioni](./destinations.md).
