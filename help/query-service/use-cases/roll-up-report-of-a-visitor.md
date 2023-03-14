---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;experienceevent query;experienceevent query;Experience Event query;
title: Visualizzare un rapporto di aggregazione per un visitatore specifico
description: Il documento seguente fornisce esempi di query che coinvolgono eventi di esperienza in Adobe Experience Platform Query Service.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Visualizzare un rapporto di aggregazione per un visitatore specifico

Questo documento fornisce un esempio SQL per aggregare dati da più proprietà di analisi per un utente specifico e visualizzare tali dati in un unico rapporto. Con Adobe Experience Platform Query Service, puoi scrivere query che utilizzano [!DNL Experience Events] per acquisire diversi casi d’uso. Gli eventi esperienza sono rappresentati dalla classe ExperienceEvent di Experience Data Model (XDM), che acquisisce un’istantanea immutabile e non aggregata del sistema quando un utente interagisce con un sito web o un servizio. Gli eventi esperienza possono essere utilizzati anche per l’analisi del dominio temporale. Consulta la [sezione passaggi successivi](#next-steps) per ulteriori casi d’uso che coinvolgono [!DNL Experience Events] per generare rapporti sui visitatori.

Ulteriori informazioni su XDM e [!DNL Experience Events] si trova nella sezione [[!DNL XDM System] panoramica](../../xdm/home.md). Combinando Query Service con [!DNL Experience Events], puoi tenere traccia in modo efficace delle tendenze comportamentali tra i tuoi utenti. Il documento seguente fornisce esempi di query che coinvolgono [!DNL Experience Events].

## Oggetto

Nell&#39;esempio SQL seguente viene illustrato come visualizzare un report aggregato di vari valori di analisi per un utente specificato.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews, 
SUM(_experience.analytics.event1to100.event1.value) as A, 
SUM(_experience.analytics.event1to100.event2.value) as B, 
SUM(_experience.analytics.event1to100.event3.value) as C,
SUM(
    CASE 
    WHEN _experience.analytics.customDimensions.evars.evar1 = 'parkas' 
    THEN 1 
    ELSE 0 
    END) as viewedParkas
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
GROUP BY endUserIds._experience.aaid.id
ORDER BY pageViews DESC;
```

I risultati della query vengono visualizzati nella tabella seguente.

```console
               id                 | pageViews |   A   |   B   |   C   | viewedParkas
----------------------------------+-----------+-------+-------+-------+--------------
457C3510571E5930-69AA721C4CBF9339 |     706.0 | 83.0  |  7.0  | 38.0  |          22
```

## Passaggi successivi {#next-steps}

La lettura di questo documento consente di comprendere meglio come utilizzare Query Service con [!DNL Experience Events] per visualizzare un rapporto aggregato dei valori di analytics per un utente specificato.

Per informazioni su altri casi di utilizzo basati sui visitatori, consulta i seguenti:

- [Recupera un elenco di visitatori organizzato per numero di visualizzazioni di pagina.](./visitors-by-number-of-page-views.md)
- [Elencare le sessioni precedenti di un visitatore.](./list-visitor-sessions.md)
- [Crea un rapporto con tendenze degli eventi per giorno.](./trended-report-of-events.md)
