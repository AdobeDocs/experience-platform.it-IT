---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv su xdm;mappare csv su xdm;guida interfaccia utente;mappatura;mappatura;preparazione dati;preparazione dati;preparazione dei dati;
solution: Experience Platform
title: Gestione dei formati di dati con Data Prep
description: Questo documento offre una panoramica della gestione dei diversi tipi di dati in Preparazione dati.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 13%

---

# Gestione dei formati di dati con Data Prep

Data Prep può gestire in modo affidabile diversi formati di dati acquisiti in Adobe Experience Platform. Questo documento illustra come vengono trattati i diversi formati di dati con Data Prep.

## Booleani {#booleans}

Se il tipo di origine è una stringa e il tipo di destinazione è booleano, Data Prep può analizzare automaticamente il valore e convertire il valore di origine in booleano.

I valori `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true`e `TRUE` vengono analizzati automaticamente `true`.

I valori `n`, `N`, `no`, `NO`, `off`, `OFF`, `false`e `FALSE` vengono analizzati automaticamente `false`.

## Date {#dates}

Data Prep supporta le funzioni data, sia come stringhe che come oggetti datetime.

### Formato della funzione data

La funzione date converte stringhe e oggetti datetime in un oggetto ZoningDateTime formattato ISO 8601.

**Formato**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parametro | Descrizione |
| --------- | ----------- |
| `{DATE}` | Obbligatorio. Stringa che rappresenta la data. |
| `{FORMAT}` | Facoltativo. Stringa che rappresenta il formato della data di origine. Ulteriori informazioni sulla formattazione delle stringhe sono disponibili nella sezione [sezione stringa formato data/ora](#format). |
| `{DEFAULT_DATE}` | Facoltativo. La data predefinita da restituire se la data specificata è null. |

Ad esempio, l’espressione `date(orderDate, "yyyy-MM-dd")` convertirà un `orderDate` valore di &quot;31 dicembre 2020&quot; in un valore datetime di &quot;2020-12-31&quot;.

### Conversioni di funzioni data

Quando i campi stringa dei dati in arrivo sono mappati ai campi data negli schemi che utilizzano Experience Data Model (XDM), il formato data deve essere menzionato esplicitamente. Se non viene menzionato esplicitamente, Data Prep tenterà di convertire i dati di input confrontandoli con i seguenti formati. Una volta trovato un formato corrispondente, smetterà di valutare tutti i formati successivi.

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
> Preparazione dei dati cercherà di convertire le stringhe in date il più possibile migliori. Tuttavia, queste conversioni possono portare a risultati indesiderati. Ad esempio, il valore della stringa &quot;12112020&quot; corrisponde al pattern &quot;gggAaaaa&quot;, ma l’utente potrebbe avere intenzione di leggere la data con il pattern &quot;ggaaaa&quot;. Di conseguenza, gli utenti devono indicare esplicitamente il formato della data per le stringhe.

### Stringhe formato data/ora {#format}

Nella tabella seguente sono illustrate le lettere del pattern definite per le stringhe di formato. Si prega di notare che le lettere distinguono tra maiuscole e minuscole.

| Simbolo | Significato | Presentazione | Esempio |
| ------ | ------- | ------------ | ------- |
| G | L&#39;era | Testo | AD; Anno Domini; A |
| S | Anno, basato sulla settimana ISO | Numero | 1996; 96 |
| y | L&#39;anno | Numero | 2004; 04 |
| M/L | Mese dell&#39;anno | Numero/Testo | 7; 07; Lug; luglio; J |
| w | Settimana dell&#39;anno | Numero | 27 |
| W | Settimana del mese | Numero | 3 |
| D | Giorno dell’anno | Numero | 189 |
| d | Giorno del mese | Numero | 10 |
| F | Giorno della settimana in un mese | Numero | 2 |
| E | Nome del giorno della settimana | Testo | martedì; Tonalità |
| u | Giorno della settimana, come numero. 1 rappresenta lunedì, ... 7 rappresenta domenica | Numero | 1 |
| a | Marcatore AM/PM | Testo | PM |
| H | Ora al giorno (0-23) | Numero | 0 |
| k | Ora al giorno (1-24) | Numero | 24 |
| K | Ora in AM/PM (0-11) | Numero | 0 |
| h | Ora in AM/PM (1-12) | Numero | 12 |
| m | Minuto nell&#39;ora | Numero | 38 |
| s | Secondo minuto | Numero | 44 |
| S | Millisecondo | Numero | 245 |
| z | Fuso orario | Fuso orario generale | ora solare del Pacifico; PST; GMT-08.00 |
| Z | Fuso orario | Fuso orario RFC 822 | -0800 |
| X | Fuso orario | Fuso orario ISO 8601 | -08; -0800; -08:00 |
| V | ID fuso orario | Testo | America/Los Angeles |
| O | Offset fuso orario | Testo | GMT+8 |
| Q/q | Trimestre dell’anno | Numero/Testo | 3; 03; Q3; 3° trimestre |

## Mappe {#maps}

Le mappe non sono attualmente supportate in [!DNL Data Prep].
