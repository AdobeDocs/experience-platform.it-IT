---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query experienceevent;query experienceevent;query Experience Event;
title: Visualizzare un rapporto roll-up per un visitatore specifico
description: Il seguente documento fornisce esempi di query che coinvolgono eventi di esperienza in Adobe Experience Platform Query Service.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 1%

---

# Visualizzare un rapporto roll-up per un visitatore specifico

Questo documento fornisce un esempio SQL per aggregare i dati da più proprietà di analisi per un utente specifico e visualizzarli insieme in un unico rapporto. Con Adobe Experience Platform Query Service puoi scrivere query che utilizzano [!DNL Experience Events] per acquisire diversi casi d’uso. Gli eventi di esperienza sono rappresentati dalla classe Experience Data Model (XDM) ExperienceEvent , che acquisisce uno snapshot immutabile e non aggregato del sistema quando un utente interagisce con un sito web o un servizio. Gli eventi di esperienza possono essere utilizzati anche per l’analisi del dominio temporale. Consulta la sezione [sezione passaggi successivi](#next-steps) per ulteriori casi d&#39;uso [!DNL Experience Events] per generare rapporti sui visitatori.

Ulteriori informazioni su XDM e [!DNL Experience Events] si trova nella [[!DNL XDM System] panoramica](../../xdm/home.md). Combinando il servizio query con [!DNL Experience Events], è possibile monitorare efficacemente le tendenze comportamentali tra gli utenti. Il seguente documento fornisce esempi di query che coinvolgono [!DNL Experience Events].

## Oggetto

L&#39;esempio SQL seguente mostra come visualizzare un report aggregato di vari valori di analisi per un utente specificato.

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

Leggendo questo documento, hai una migliore comprensione di come utilizzare Query Service con [!DNL Experience Events] per visualizzare un report aggregato dei valori di analytics per un utente specificato.

Consulta i seguenti casi d’uso per informazioni su altri casi d’uso basati su visitatore:

- [Recupera un elenco di visitatori organizzati per numero di visualizzazioni di pagina.](./visitors-by-number-of-page-views.md)
- [Elenca le sessioni precedenti di un visitatore.](./list-visitor-sessions.md)
- [Crea un rapporto con tendenze degli eventi per giorno.](./trended-report-of-events.md)
