---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;query;experienceevent query;experienceevent query;Experience Event query;
title: Elencare i visitatori in base al loro numero di visualizzazioni di pagina
description: Scopri come scrivere query che utilizzano gli eventi esperienza per recuperare un elenco di visitatori organizzati in base al numero di visualizzazioni di pagina.
exl-id: 6e8eed0c-838e-4cd0-ae8c-453114fbf4ea
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 1%

---

# Elencare i visitatori in base al numero di visualizzazioni di pagina

Questo documento fornisce un esempio del codice SQL necessario per recuperare una lista di visitatori organizzata in base al numero di visualizzazioni di pagina. Con Adobe Experience Platform Query Service, puoi scrivere query che utilizzano [!DNL Experience Events] per acquisire diversi casi d’uso. Gli eventi esperienza sono rappresentati dalla classe ExperienceEvent di Experience Data Model (XDM), che acquisisce un’istantanea immutabile e non aggregata del sistema quando un utente interagisce con un sito web o un servizio. Gli eventi esperienza possono essere utilizzati anche per l’analisi del dominio temporale. Consulta la [sezione passaggi successivi](#next-steps) per ulteriori casi d’uso che coinvolgono [!DNL Experience Events] per generare rapporti sui visitatori.

Ulteriori informazioni su XDM e [!DNL Experience Events] si trova nella sezione [[!DNL XDM System] panoramica](../../xdm/home.md). Combinando Query Service con [!DNL Experience Events], puoi tenere traccia in modo efficace delle tendenze comportamentali tra i tuoi utenti. Il documento seguente fornisce esempi di query che coinvolgono [!DNL Experience Events].

## Oggetto

L’esempio seguente crea un rapporto che elenca i 10 ID degli utenti che hanno visualizzato più pagine.

```sql
SELECT 
endUserIds._experience.aaid.id, 
SUM(web.webPageDetails.pageviews.value) as pageViews 
FROM your_analytics_table
GROUP BY endUserIds._experience.aaid.id 
ORDER BY pageViews DESC
LIMIT 10;
```

I risultati della query vengono visualizzati nella tabella seguente.

```console
               id                  | pageViews
-----------------------------------+-----------
 457C3510571E5930-69AA721C4CBF9339 |     706.0
 776F85658792C017-6491FE6570382A01 |     700.0
 6BEC9C6AB52E779F-28F5B023113F2C85 |     654.0
 1C0CCFB2DC63611E-6E4A4D4142AEB613 |     642.0
 112EE9A6F3BE29D1-514A6C355A2C9EF6 |     629.0
 CCC75A0E6AC7F2FA-11D58515D370F626 |     624.0
 749F850A44153120-3710C53FA2162349 |     614.0
 2B668C6DDDAF0C505-92EDCC072F7CDDA |     587.0
 7EB7257335935320-101921AF45111FE6 |     586.0
 5F4759CA80DCA9C9-2C0DA93D80D9DBFA |     586.0
(10 rows)
```

## Passaggi successivi {#next-steps}

La lettura di questo documento consente di comprendere meglio come utilizzare Query Service con [!DNL Experience Events] per elencare gli utenti che hanno visualizzato il maggior numero di pagine.

Per informazioni su altri casi di utilizzo basati sui visitatori, consulta i seguenti:

- [Elencare le sessioni precedenti di un visitatore.](./list-visitor-sessions.md)
- [Visualizza un rapporto di aggregazione dati di un visitatore.](./roll-up-report-of-a-visitor.md)
- [Crea un rapporto con tendenze degli eventi per giorno.](./trended-report-of-events.md)
