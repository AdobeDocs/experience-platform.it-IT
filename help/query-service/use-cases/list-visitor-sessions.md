---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query experienceevent;query experienceevent;query Experience Event;
title: Elencare le visualizzazioni di pagina di un utente
description: Scopri come scrivere query che utilizzano Experience Events per creare un elenco delle ultime 100 pagine utilizzate da un utente specifico.
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# Elencare le visualizzazioni di pagina di un utente

Questo documento fornisce un esempio dell&#39;istruzione SQL necessaria per elencare le visualizzazioni di pagina di un utente specificato. Con Adobe Experience Platform Query Service puoi scrivere query che utilizzano [!DNL Experience Events] per acquisire diversi casi d’uso. Gli eventi di esperienza sono rappresentati dalla classe Experience Data Model (XDM) ExperienceEvent , che acquisisce uno snapshot immutabile e non aggregato del sistema quando un utente interagisce con un sito web o un servizio. Gli eventi di esperienza possono essere utilizzati anche per l’analisi del dominio temporale. Consulta la sezione [sezione passaggi successivi](#next-steps) per ulteriori casi d&#39;uso [!DNL Experience Events] per generare rapporti sui visitatori.

Ulteriori informazioni su XDM e [!DNL Experience Events] si trova nella [[!DNL XDM System] panoramica](../../xdm/home.md). Combinando il servizio query con [!DNL Experience Events], è possibile monitorare efficacemente le tendenze comportamentali tra gli utenti. Il seguente documento fornisce esempi di query che coinvolgono [!DNL Experience Events].

## Oggetto

Nell&#39;esempio seguente sono elencate le ultime 100 pagine visualizzate da un utente specificato.

```sql
SELECT 
timestamp, 
web.webReferrer.type as referrerType, 
web.webReferrer.URL as referrer, 
web.webPageDetails.name as pageName, 
_experience.analytics.event1to100.event1.value as A, 
_experience.analytics.event1to100.event2.value as B, 
_experience.analytics.event1to100.event3.value as C, 
web.webPageDetails.pageviews.value as pageViews
FROM your_analytics_table 
WHERE endUserIds._experience.aaid.id = '457C3510571E5930-69AA721C4CBF9339' 
ORDER BY timestamp 
LIMIT 100;
```

Di seguito sono riportati i risultati di questa query.

```console
      timestamp       |  referrerType  |                            referrer                                |                 pageName            |  A  |  B  |  C  | pageViews
----------------------+----------------+--------------------------------------------------------------------+-------------------------------------+-----+-----+-----+--------------
2019-11-08 17:15:28.0 | typed_bookmark |                                                                    |                                     |     |     |     |
2019-11-08 17:53:05.0 | social         | http://www.reddit.com                                              | Home                                |     |     |     |          1.0
2019-11-08 17:53:45.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 19:22:34.0 | typed_bookmark |                                                                    |                                     |     |     |     |          
2019-11-08 20:01:12.0 | search_engine  | http://www.google.com/search?ie=UTF-8&q=laundry parkas&cid=sem:115 | Home                                |     |     |     |          1.0 
2019-11-08 20:01:57.0 | typed_bookmark |                                                                    | Kids                                |     |     |     |          1.0
2019-11-08 20:03:36.0 | typed_bookmark |                                                                    | Search Results                      | 1.0 |     |     |          1.0
2019-11-08 20:04:30.0 | typed_bookmark |                                                                    | Product Details: Pemmican Power Bar |     |     |     |          1.0
2019-11-08 20:05:27.0 | typed_bookmark |                                                                    | Shopping Cart: Cart Details         |     |     |     |          1.0
2019-11-08 20:06:07.0 | typed_bookmark |                                                                    | Shopping Cart: Shipping Information |     |     |     |          1.0
2019-11-08 20:07:02.0 | typed_bookmark |                                                                    | Shopping Cart: Billing Information  |     |     | 1.0 |          1.0
2019-11-08 20:07:52.0 | typed_bookmark |                                                                    | Shopping Cart: Order Review         |     |     |     |          1.0
2019-11-08 20:08:45.0 | typed_bookmark |                                                                    | Order Confirmation                  |     |     |     |          1.0
2019-11-08 20:09:24.0 | typed_bookmark |                                                                    | Home                                |     |     |     |          1.0
2019-11-08 20:10:03.0 | typed_bookmark |                                                                    | Editorial Page: Camping Essentials  |     |     |     |          1.0
2019-11-08 20:11:01.0 | typed_bookmark |                                                                    | Account Registration|Form           |     |     |     |          1.0
2019-11-08 20:11:38.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
2019-11-08 20:12:10.0 | typed_bookmark |                                                                    | Blog: Iris Sagan                    |     |     |     |          1.0
2019-11-08 20:13:09.0 | typed_bookmark |                                                                    | Product Details: UltraTech Socks    |     |     |     |          1.0
2019-11-08 20:14:05.0 | typed_bookmark |                                                                    | Seasonal Sale                       |     |     |     |          1.0
```

## Passaggi successivi {#next-steps}

Leggendo questo documento, hai una migliore comprensione di come utilizzare Query Service con [!DNL Experience Events] per elencare le visualizzazioni di pagina come utente specificato.

Consulta i seguenti casi d’uso per informazioni su altri casi d’uso basati su visitatore:

- [Recupera un elenco di visitatori organizzati per numero di visualizzazioni di pagina.](./visitors-by-number-of-page-views.md)
- [Visualizza un rapporto roll-up di un visitatore.](./roll-up-report-of-a-visitor.md)
- [Crea un rapporto con tendenze degli eventi per giorno.](./trended-report-of-events.md)
