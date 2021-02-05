---
keywords: ' Experience Platform;home;argomenti popolari;mappare csv;mappare file CSV;mappare file CSV su xdm;mappare csv a xdm;ui guide;mapper;mapping;date;date function;date;'
solution: Experience Platform
title: Funzioni data di preparazione dati
topic: overview
description: Questo documento introduce le funzioni data utilizzate con Data Prep.
translation-type: tm+mt
source-git-commit: 37c1c98ccba50fa917acc5e93763294f4dde5c36
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 16%

---


# Funzioni data di preparazione dati

Data Prep supporta le funzioni data, sia come stringhe che come oggetti datetime.

## Conversioni di funzioni data

Quando i campi stringa dai dati in arrivo vengono mappati ai campi data negli schemi tramite Experience Data Model (XDM), il formato data deve essere esplicitamente menzionato. Se non menzionato esplicitamente, Data Prep tenterà di convertire i dati di input facendoli corrispondere ai seguenti formati. Una volta trovato il formato corrispondente, questo smetterà di valutare tutti i formati successivi.

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
> Prep dati cercherà di convertire le stringhe in date nel modo migliore possibile. Tuttavia, queste conversioni possono portare a risultati indesiderati. Ad esempio, il valore della stringa &quot;12112020&quot; corrisponde al pattern &quot;gggaaaa&quot;, ma l&#39;utente potrebbe aver intenzione di leggere la data con il pattern &quot;ggaaaa&quot;. Di conseguenza, gli utenti dovrebbero indicare esplicitamente il formato della data per le stringhe.

## Stringhe formato data/ora

Nella tabella seguente sono illustrate le lettere del pattern definite per le stringhe di formato. Si prega di notare che le lettere sono con distinzione tra maiuscole e minuscole.

| Simbolo | Significato | Presentazione | Esempio |
| ------ | ------- | ------------ | ------- |
| G | L&#39;era | Testo | AD; Anno Domini; A |
| Y | Anno, in base alla settimana ISO | Numero | 1996; 96 |
| y | L&#39;anno | Numero | 2004; 04 |
| M/L | Mese dell&#39;anno | Numero/Testo | 7; 07; Lug; luglio; J |
| w | Settimana dell&#39;anno | Numero | 27 |
| W | Settimana del mese | Numero | 3 |
| D | Giorno dell&#39;anno | Numero | 189 |
| d | Giorno del mese | Numero | 10 |
| F | Giorno della settimana in un mese | Numero | 2 |
| E | Nome del giorno della settimana | Testo | martedì; Tonalità |
| u | Giorno della settimana, come numero. 1 rappresenta lunedì, ... 7 rappresenta domenica | Numero | 1 |
| a | Marcatore AM/PM | Testo | PM |
| H | Ora del giorno (0-23) | Numero | 0 |
| k | Ora del giorno (1-24) | Numero | 24 |
| K | Ora in AM/PM (0-11) | Numero | 0 |
| h | Ora in AM/PM (1-12) | Numero | 12 |
| m | Minuto nell&#39;ora | Numero | 38 |
| s | Secondo nel minuto | Numero | 44 |
| S | Millisecondo | Numero | 245 |
| z | Fuso orario | Fuso orario generale | Ora standard del Pacifico; PST; GMT-08:00 |
| Z | Fuso orario | Fuso orario RFC 822 | -0800 |
| X | Fuso orario | Fuso orario ISO 8601 | -08; -0800; -08:00 |
| V | ID fuso orario | Testo | America/Los Angeles |
| O | Offset fuso orario | Testo | GMT+8 |
| Q/q | Trimestre dell&#39;anno | Numero/Testo | 3; 03; Q3; 3° trimestre |

**Esempio**

L&#39;espressione `date(orderDate, "yyyy-MM-dd")` converte un valore `orderDate` di &quot;31 dicembre 2020&quot; in un valore datetime di &quot;2020-12-31&quot;.