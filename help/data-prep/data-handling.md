---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv a xdm;mappare csv a xdm;guida interfaccia utente;mapper;mappare;preparazione dati;preparazione dati;preparazione dati;
solution: Experience Platform
title: Gestione dei formati dei dati con la preparazione dati
description: Questo documento offre una panoramica della gestione dei diversi tipi di dati nella preparazione dati.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# Gestione dei formati dei dati con la preparazione dati

La preparazione dati può gestire in modo affidabile diversi formati di dati acquisiti in Adobe Experience Platform. Questo documento illustra come vengono trattati i diversi formati di dati con la preparazione dati.

## Booleani {#booleans}

Se il tipo di origine è una stringa e il tipo di destinazione è booleano, Preparazione dati può analizzare automaticamente il valore e convertirlo in booleano.

I valori `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true`, e `TRUE` vengono analizzate automaticamente per essere `true`.

I valori `n`, `N`, `no`, `NO`, `off`, `OFF`, `false`, e `FALSE` vengono analizzate automaticamente per essere `false`.

## Date {#dates}

La preparazione dati supporta le funzioni data, sia come stringhe che come oggetti datetime.

### Formato funzione data

La funzione date converte stringhe e oggetti datetime in un oggetto formattato ISO 8601 ZonedDateTime.

**Formato**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATE}` | Obbligatorio. Stringa che rappresenta la data. |
| `{FORMAT}` | Facoltativo. Stringa che rappresenta il formato della data di origine. Ulteriori informazioni sulla formattazione delle stringhe sono disponibili nella [sezione stringa formato data/ora](#format). |
| `{DEFAULT_DATE}` | Facoltativo. Data predefinita da restituire se la data specificata è null. |

Ad esempio, l’espressione `date(orderDate, "yyyy-MM-dd")` convertirà un `orderDate` valore &quot;31 dicembre 2020&quot; in un valore datetime &quot;2020-12-31&quot;.

### Conversioni di funzione data

Quando i campi stringa dei dati in arrivo vengono mappati su campi data negli schemi utilizzando Experience Data Model (XDM), il formato della data deve essere menzionato esplicitamente. Se non è menzionato esplicitamente, la preparazione dati tenterà di convertire i dati di input confrontandoli con i seguenti formati. Una volta trovato un formato corrispondente, non verrà più valutata alcuna formattazione successiva.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> La preparazione dati cercherà di convertire le stringhe in date nel modo migliore possibile. Tuttavia, queste conversioni possono portare a risultati indesiderati. Ad esempio, il valore stringa &quot;12112020&quot; corrisponde al pattern &quot;MMddyyy&quot;, ma l’utente potrebbe aver impostato la data per la lettura con il pattern &quot;ddMMyyyy&quot;. Di conseguenza, gli utenti devono menzionare esplicitamente il formato della data per le stringhe.

### Stringhe di formato data/ora {#format}

Nella tabella seguente vengono illustrate le lettere di serie definite per le stringhe di formato. Le lettere fanno distinzione tra maiuscole e minuscole.

| Simbolo | Significato | Presentazione | Esempio |
| ------ | ------- | ------------ | ------- |
| G | L&#39;era | Testo | AD; Anno Domini; A |
| S | Anno, in base alla settimana ISO | Numero | 1996; 96 |
| y | L&#39;anno | Numero | 2004; 04 |
| M/L | Mese dell’anno | Numero/Testo | 7; 07; lug; luglio; J |
| w | Settimana dell’anno | Numero | 27 |
| W | Settimana del mese | Numero | 3 |
| D | Giorno dell&#39;anno | Numero | 189 |
| d | Giorno del mese | Numero | 10 |
| F | Giorno della settimana in un mese | Numero | 2 |
| E | Nome del giorno della settimana | Testo | martedì, martedì |
| u | Giorno della settimana, come numero. 1 rappresenta lunedì, ..., 7 rappresenta domenica | Numero | 1 |
| a | Indicatore AM/PM | Testo | PM |
| H | Ora del giorno (0-23) | Numero | 0 |
| k | Ora del giorno (1-24) | Numero | 24 |
| K | Ora in AM/PM (0-11) | Numero | 0 |
| h | Ora in AM/PM (1-12) | Numero | 12 |
| m | Minuto dell&#39;ora | Numero | 38 |
| s | Secondo nel minuto | Numero | 44 |
| S | millisecondo | Numero | 245 |
| z | Fuso orario | Fuso orario generale | Ora solare Pacifico; PST; GMT-08:00 |
| Z | Fuso orario | Fuso orario RFC 822 | -0800 |
| X | Fuso orario | Fuso orario ISO 8601 | -08; -0800; -08:00 |
| V | ID fuso orario | Testo | America/Los_Angeles |
| O | Scostamento fuso orario | Testo | GMT+8 |
| Q/q | Trimestre dell’anno | Numero/Testo | 3; 03; Q3; terzo trimestre |

## Mappe {#maps}

Le mappe non sono attualmente supportate in [!DNL Data Prep].
