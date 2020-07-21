---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Metadati, comandi
topic: metadata
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Metadati, comandi

Per i metadati del set di dati, i seguenti comandi PSQL sono attualmente supportati per le query:

>[!NOTE]
>
>I comandi elencati di seguito sono con distinzione tra maiuscole e minuscole.

| Comando | Descrizione |
|------- | ------------|
| `\conninfo` | Invia informazioni sulla connessione corrente al database. |
| `\d` | Visualizza un elenco di tutte le tabelle, viste, viste materializzate, sequenze e tabelle esterne visibili. |
| `\dE` | Visualizza un elenco di tabelle esterne. |
| `\df or \df+` | Visualizza un elenco di funzioni. |
| `\di` | Visualizza un elenco di indici. |
| `\dm` | Visualizza un elenco di viste materializzate. |
| `\dn` | Visualizza un elenco di schemi (spazi dei nomi). |
| `\ds` | Visualizza un elenco di sequenze. |
| `\dS` | Visualizza un elenco di tabelle definite da PostgreSQL. |
| `\dt` | Visualizza un elenco di tabelle. |
| `\dT` | Visualizza un elenco dei tipi di dati. |
| `\dv` | Visualizza un elenco di viste. |
| `\encoding` | Elenca la codifica corrente del set di caratteri client. |
| `\errverbose` | Ripete il messaggio di errore server più recente alla massima verbosità. |
| `\l or \list` | Visualizza un elenco di database nel server. |
| `\set` | Visualizza i nomi e i valori di tutte le variabili psql correnti. |
| `\showtables` | Mostra le informazioni seguenti: <br>name: Nome a cui verrà fatto riferimento la tabella.<br>datasetId: ID del set di dati memorizzato.<br>dataset: Nome del set di dati memorizzato.<br>descrizione: Una descrizione del set di dati.<br>risolto: Un valore booleano che indica se il set di dati viene risolto o meno nella sessione corrente. |
| `\timing` | Attiva e disattiva la visualizzazione. La visualizzazione è espressa in millisecondi. Gli intervalli più lunghi di un secondo vengono visualizzati in formato minuti:secondi, con i campi ore e giorni aggiunti quando necessario. |

Tutti i comandi che iniziano con `\d` possono essere combinati. Ad esempio, è possibile pubblicare un elenco `\dtsn` di tutte le tabelle, le sequenze e gli schemi. `\d` di per sé mostra tutte le tabelle, le viste, le viste materializzate e le sequenze visibili.

Per ulteriori informazioni sui comandi elencati sopra, consulta la documentazione disponibile in [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). Tuttavia, tenete presente che non tutte le opzioni visualizzate nella documentazione PostSQL sono supportate da [!DNL Experience Platform].

