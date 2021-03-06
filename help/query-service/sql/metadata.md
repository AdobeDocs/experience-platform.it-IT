---
keywords: Experience Platform;home;argomenti popolari;PSQL;psql;Query service;query service;metadati;comandi;comandi di metadati;
solution: Experience Platform
title: Comandi PostgreSQL per metadati nel servizio query
topic-legacy: metadata
description: Elenco di comandi PostgreSQL attualmente supportati per la query dei metadati in Adobe Experience Platform Query Service.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Comandi PostgreSQL per metadati nel servizio query

Per i metadati del set di dati, i seguenti comandi PostgreSQL sono attualmente supportati per le query:

>[!NOTE]
>
>I comandi elencati di seguito distinguono tra maiuscole e minuscole.

| Comando | Descrizione |
|------- | ------------|
| `\conninfo` | Invia informazioni sulla connessione al database corrente. |
| `\d` | Visualizza un elenco di tutte le tabelle, viste, viste materializzate, sequenze e tabelle esterne visibili. |
| `\dE` | Visualizza un elenco di tabelle esterne. |
| `\df or \df+` | Visualizza un elenco di funzioni. |
| `\di` | Visualizza un elenco di indici. |
| `\dm` | Visualizza un elenco di viste materializzate. |
| `\dn` | Visualizza un elenco di schemi (namespace). |
| `\ds` | Visualizza un elenco di sequenze. |
| `\dS` | Visualizza un elenco di tabelle definite da PostgreSQL. |
| `\dt` | Visualizza un elenco di tabelle. |
| `\dT` | Visualizza un elenco dei tipi di dati. |
| `\dv` | Visualizza un elenco di visualizzazioni. |
| `\encoding` | Elenca la codifica corrente del set di caratteri client. |
| `\errverbose` | Ripete il messaggio di errore server più recente alla massima verbosità. |
| `\l or \list` | Visualizza un elenco di database nel server. |
| `\set` | Visualizza i nomi e i valori di tutte le variabili psql correnti. |
| `\showtables` | Mostra le seguenti informazioni: <br>nome: Nome a cui fare riferimento la tabella.<br>datasetId: ID del set di dati memorizzato.<br>set di dati: Nome del set di dati memorizzato.<br>descrizione: Una descrizione del set di dati.<br>risolto: Un valore booleano che indica se il set di dati è risolto o meno nella sessione corrente. |
| `\timing` | Attiva e disattiva la visualizzazione. La visualizzazione è in millisecondi. Gli intervalli più lunghi di un secondo vengono visualizzati in formato minuti:secondi, con i campi ore e giorni aggiunti quando necessario. |

Tutti i comandi che iniziano con `\d` possono essere combinati. Ad esempio, è possibile pubblicare `\dtsn` per visualizzare un elenco di tutte le tabelle, le sequenze e gli schemi. `\d` mostra di per sé tutte le tabelle, viste, viste materializzate e sequenze visibili.

Per ulteriori informazioni sui comandi elencati sopra, consulta la documentazione all&#39;indirizzo [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Tuttavia, tieni presente che non tutte le opzioni visualizzate nella documentazione PostgreSQL sono supportate da [!DNL Experience Platform].
