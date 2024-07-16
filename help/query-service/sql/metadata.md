---
keywords: Experience Platform;home;argomenti popolari;PSQL;psql;servizio query;servizio query;metadati;comandi;comandi metadati;
solution: Experience Platform
title: Comandi PostgreSQL dei metadati in Query Service
description: Elenco di comandi PostgreSQL attualmente supportati per l'esecuzione di query sui metadati in Adobe Experience Platform Query Service.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Metadati [!DNL PostgreSQL] comandi in Query Service

Per i metadati nel set di dati, i seguenti comandi [!DNL PostgreSQL] sono attualmente supportati per l&#39;esecuzione di query:

>[!NOTE]
>
>I comandi elencati di seguito fanno distinzione tra maiuscole e minuscole.

| Comando | Descrizione |
|------- | ------------|
| `\conninfo` | Restituisce informazioni sulla connessione al database corrente. |
| `\d` | Visualizza un elenco di tutte le tabelle, viste, viste materializzate, sequenze e tabelle esterne visibili. |
| `\dE` | Visualizza un elenco di tabelle esterne. |
| `\df or \df+` | Visualizza un elenco di funzioni. |
| `\di` | Visualizza un elenco di indici. |
| `\dm` | Visualizza un elenco di viste materializzate. |
| `\dn` | Visualizza un elenco di schemi (spazi dei nomi). |
| `\ds` | Visualizza un elenco di sequenze. |
| `\dS` | Visualizza un elenco di tabelle definite da PostgreSQL. |
| `\dt` | Visualizza un elenco di tabelle. |
| `\dT` | Visualizza un elenco di tipi di dati. |
| `\dv` | Visualizza un elenco di visualizzazioni. |
| `\encoding` | Elenca la codifica del set di caratteri client corrente. |
| `\errverbose` | Ripete il messaggio di errore server più recente alla massima gravità. |
| `\l or \list` | Visualizza un elenco di database nel server. |
| `\set` | Visualizza i nomi e i valori di tutte le variabili psql correnti. |
| `\showtables` | Mostra le seguenti informazioni: <br>nome: il nome in base al quale verrà fatto riferimento alla tabella.<br>datasetId: ID del set di dati archiviato.<br>set di dati: nome del set di dati archiviato.<br>descrizione: una descrizione del set di dati.<br>resolved: valore booleano che indica se il set di dati viene risolto o meno nella sessione corrente. |
| `\timing` | Attiva o disattiva la visualizzazione. La visualizzazione è in millisecondi. Gli intervalli superiori a un secondo vengono visualizzati in formato minuti:secondi, con campi ore e giorni aggiunti quando necessario. |

Tutti i comandi che iniziano con `\d` possono essere combinati. Ad esempio, è possibile emettere `\dtsn` per visualizzare un elenco di tutte le tabelle, sequenze e schemi. `\d` mostra tutte le tabelle, le viste, le viste materializzate e le sequenze visibili.

Per ulteriori informazioni sui comandi elencati in precedenza, consulta la documentazione all&#39;indirizzo [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Si noti tuttavia che non tutte le opzioni visualizzate nella documentazione di [!DNL PostgreSQL] sono supportate da [!DNL Experience Platform].
