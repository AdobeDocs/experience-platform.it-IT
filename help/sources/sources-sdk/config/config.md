---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Opzioni di configurazione in Origini self-service (SDK batch)
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare Self-Service Sources (SDK batch).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Opzioni di configurazione in Origini self-service (SDK batch)

Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare Self-Service Sources (SDK batch).

## Specifica di connessione

Le specifiche di connessione restituiscono le proprietà del connettore di un&#39;origine. Includono specifiche di autenticazione relative alla creazione delle connessioni di base e di origine e un ID di specifica di connessione fisso assegnato a una determinata origine. Le specifiche di connessione sono indipendenti dal tenant e dall’organizzazione. Una specifica di connessione tipica contiene informazioni di base su una determinata origine, nonché tre sezioni distinte: `authSpec`, `sourceSpec`, e `exploreSpec`.

| Specifiche | Descrizione |
| --- | --- |
| `authSpec` | Il `authSpec` L’array contiene informazioni sui parametri di autenticazione necessari per connettere un’origine a Platform. Qualsiasi origine può supportare più tipi diversi di autenticazione. |
| `sourceSpec` | Il `sourceSpec` array contiene informazioni generali relative a un’origine, incluse informazioni sugli attributi necessari per presentare l’origine nell’interfaccia utente, sul collegamento alla documentazione e sui parametri relativi a impaginazione, intestazione, corpo e pianificazione. Inoltre, `sourceSpec` descrive lo schema dei parametri necessari per creare una connessione di origine da una connessione di base ed è necessario per creare una connessione di origine. |
| `exploreSpec` | Il `exploreSpec` array definisce i parametri necessari per l&#39;esplorazione e l&#39;analisi degli oggetti contenuti nell&#39;origine. Il `exploreSpec` definisce anche il formato di risposta restituito quando gli oggetti vengono esplorati e ispezionati. |

{style="table-layout:auto"}

## Popolare i valori delle specifiche di connessione

Una specifica di connessione può essere divisa in tre parti distinte: le specifiche di autenticazione, le specifiche di origine e le specifiche di esplorazione.

Per istruzioni su come popolare i valori di ciascuna parte di una specifica di connessione, vedere i documenti seguenti:

* [Configurare le specifiche di autenticazione](./authspec.md)
* [Configurare le specifiche di origine](./sourcespec.md)
* [Configurare le specifiche di esplorazione](./explorespec.md)
