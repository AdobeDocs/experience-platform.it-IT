---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;source connectors;sources sdk;sdk;SDK
title: Opzioni di configurazione in Origini self-service (SDK in batch)
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare le origini self-service (Batch SDK).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Opzioni di configurazione in Origini self-service (SDK in batch)

Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare le origini self-service (Batch SDK).

## Specifica di connessione

Le specifiche di connessione restituiscono le proprietà del connettore di un&#39;origine. Includono specifiche di autenticazione relative alla creazione delle connessioni di base e di origine e un ID di specifica di connessione fisso assegnato a una determinata origine. Le specifiche di connessione sono indipendenti dal tenant e dall’organizzazione. Una specifica di connessione tipica contiene informazioni di base su una determinata origine e tre sezioni distinte: `authSpec`, `sourceSpec` e `exploreSpec`.

| Specifiche | Descrizione |
| --- | --- |
| `authSpec` | L&#39;array `authSpec` contiene informazioni sui parametri di autenticazione necessari per connettere un&#39;origine ad Experience Platform. Qualsiasi origine può supportare più tipi diversi di autenticazione. |
| `sourceSpec` | L&#39;array `sourceSpec` contiene informazioni generali relative a un&#39;origine, incluse informazioni sugli attributi necessari per presentare l&#39;origine nell&#39;interfaccia utente, sul collegamento alla documentazione e sui parametri relativi all&#39;impaginazione, all&#39;intestazione, al corpo e alla pianificazione. Inoltre, `sourceSpec` descrive lo schema dei parametri necessari per creare una connessione di origine da una connessione di base ed è necessario per creare una connessione di origine. |
| `exploreSpec` | L&#39;array `exploreSpec` definisce i parametri necessari per l&#39;esplorazione e l&#39;analisi degli oggetti contenuti nell&#39;origine. `exploreSpec` definisce anche il formato di risposta restituito durante l&#39;esplorazione e l&#39;ispezione degli oggetti. |

{style="table-layout:auto"}

## Popolare i valori delle specifiche di connessione

Una specifica di connessione può essere divisa in tre parti distinte: le specifiche di autenticazione, le specifiche di origine e le specifiche di esplorazione.

Per istruzioni su come popolare i valori di ciascuna parte di una specifica di connessione, vedere i documenti seguenti:

* [Configurare le specifiche di autenticazione](./authspec.md)
* [Configurare le specifiche di origine](./sourcespec.md)
* [Configurare le specifiche di esplorazione](./explorespec.md)
