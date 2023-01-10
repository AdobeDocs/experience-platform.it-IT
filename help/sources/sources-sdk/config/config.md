---
keywords: Experience Platform;home;argomenti popolari;sorgenti;connettori;connettori sorgente;origini sdk;sdk;SDK
title: Opzioni di configurazione in Origini self-service (SDK batch)
description: Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare Origini self-service (SDK batch).
exl-id: a41b3b80-599a-47ed-a391-419721be5aa2
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%

---

# Opzioni di configurazione in Origini self-service (SDK batch)

Questo documento fornisce una panoramica delle configurazioni da preparare per utilizzare Origini self-service (SDK batch).

## Specifica di connessione

Le specifiche di connessione restituiscono le proprietà del connettore di un&#39;origine. Includono specifiche di autenticazione relative alla creazione delle connessioni di base e di origine e un ID di specifica di connessione fisso assegnato a una particolare origine. Le specifiche di connessione sono agnostiche del tenant e dell’organizzazione. Una specifica di connessione tipica contiene informazioni di base su una determinata origine, oltre a tre sezioni distinte: `authSpec`, `sourceSpec`e `exploreSpec`.

| Specifiche | Descrizione |
| --- | --- |
| `authSpec` | La `authSpec` contiene informazioni sui parametri di autenticazione necessari per collegare un’origine a Platform. Qualsiasi origine può supportare diversi tipi di autenticazione. |
| `sourceSpec` | La `sourceSpec` array contiene informazioni generali relative a un’origine, incluse informazioni sugli attributi necessari per presentare l’origine nell’interfaccia utente, il collegamento alla documentazione e i parametri relativi all’impaginazione, all’intestazione, al corpo e alla pianificazione. Inoltre, `sourceSpec` descrive lo schema dei parametri necessari per creare una connessione di origine da una connessione di base ed è necessario per creare una connessione di origine. |
| `exploreSpec` | La `exploreSpec` La matrice definisce i parametri necessari per l&#39;esplorazione e l&#39;ispezione degli oggetti contenuti nell&#39;origine. La `exploreSpec` definisce anche il formato di risposta restituito quando gli oggetti vengono esplorati ed ispezionati. |

{style=&quot;table-layout:auto&quot;}

## Compilare i valori delle specifiche di connessione

Una specifica di connessione può essere divisa in tre parti distinte: le specifiche di autenticazione, le specifiche di origine e le specifiche di esplorazione.

Per istruzioni su come compilare i valori di ciascuna parte di una specifica di connessione, consultare i documenti seguenti:

* [Configurare le specifiche di autenticazione](./authspec.md)
* [Configurare le specifiche di origine](./sourcespec.md)
* [Configurare la specifica di esplorazione](./explorespec.md)
