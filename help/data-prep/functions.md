---
keywords: ' Experience Platform;home;argomenti popolari;mappare csv;mappare file CSV;mappare file csv a xdm;mappare csv a xdm;ui guide;mapper;mapping;mapping fields;mapping fields;mapping fields;mapping services;mapping function;'
solution: Experience Platform
title: Funzioni di mappatura dei dati
topic: ' - Panoramica'
description: Questo documento introduce le funzioni di mappatura utilizzate con Data Prep.
translation-type: tm+mt
source-git-commit: fd2dffd5b8957833b670e9cb434517bcb0f886a3
workflow-type: tm+mt
source-wordcount: '3625'
ht-degree: 3%

---


# Funzioni di mappatura di Data Prep

Le funzioni Prep dati possono essere utilizzate per calcolare e calcolare i valori in base a quanto immesso nei campi di origine.

## Campi

Un nome di campo può essere un qualsiasi identificatore valido, ovvero una sequenza illimitata di lettere e cifre Unicode, che inizia con una lettera, il simbolo del dollaro (`$`) o il carattere di sottolineatura (`_`). Anche i nomi delle variabili seguono la distinzione tra maiuscole e minuscole.

Se il nome di un campo non segue questa convenzione, il nome del campo deve essere racchiuso con `${}`. Quindi, ad esempio, se il nome del campo è &quot;Nome&quot; o &quot;Nome.Nome&quot;, il nome deve essere racchiuso come `${First Name}` o `${First.Name}` rispettivamente.

Inoltre, se il nome di un campo è **qualsiasi** delle seguenti parole chiave riservate, deve essere racchiuso con `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

È possibile accedere ai dati all&#39;interno dei campi secondari utilizzando la notazione del punto. Ad esempio, se è presente un oggetto `name` per accedere al campo `firstName`, utilizzare `name.firstName`.

## Elenco delle funzioni

Le tabelle seguenti elencano tutte le funzioni di mappatura supportate, incluse le espressioni di esempio e i relativi output.

### Funzioni stringa

>[!NOTE]
>
>Scorrere a sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| concat | Conconcentra le stringhe specificate. | <ul><li>STRINGA: Stringhe che verranno concatenate.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Ciao, &quot;, &quot;lì&quot;, &quot;!&quot;) | `"Hi, there!"` |
| esplodere | Divide la stringa in base a un regex e restituisce un array di parti. Facoltativamente, è possibile includere regex per dividere la stringa. Per impostazione predefinita, la divisione è uguale a &quot;,&quot;. I seguenti delimitatori **devono essere preceduti da un carattere di escape `\`: `+, ?, ^, |, ., [, (, {, ), *, $, \`** | <ul><li>STRINGA: **Obbligatorio** Stringa da dividere.</li><li>REGEX: *Facoltativo* L&#39;espressione regolare che può essere utilizzata per dividere la stringa.</li></ul> | esplode(STRING, REGEX) | esplode(&quot;Ciao, ciao!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Restituisce la posizione/indice di una sottostringa. | <ul><li>INGRESSO: **Obbligatorio** Stringa in fase di ricerca.</li><li>SOTTOSTRINGA: **Obbligatorio** Sottostringa cercata all&#39;interno della stringa.</li><li>START_POSITION: *Facoltativo* La posizione di dove iniziare a cercare nella stringa.</li><li>OCCORRENZA: *Facoltativo* L&#39;ennesima occorrenza da cercare dalla posizione iniziale. Per impostazione predefinita, è 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| sostituto | Sostituisce la stringa di ricerca, se presente nella stringa originale. | <ul><li>INGRESSO: **Obbligatorio** La stringa di input.</li><li>TO_FIND: **Obbligatorio** Stringa da cercare all&#39;interno dell&#39;input.</li><li>TO_REPLACE: **Obbligatorio** Stringa che sostituirà il valore in &quot;TO_FIND&quot;.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replace(&quot;Questa è una stringa ri test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Questo è un test di sostituzione delle stringhe&quot; |
| substr | Restituisce una sottostringa della lunghezza specificata. | <ul><li>INGRESSO: **Obbligatorio** La stringa di input.</li><li>START_INDEX: **Obbligatorio** L&#39;indice della stringa di input da cui inizia la sottostringa.</li><li>LUNGHEZZA: **Obbligatorio** Lunghezza della sottostringa.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;Questo è un test di sottostringa&quot;, 7, 8) | &quot; a subst&quot; |
| lower /<br>lcase | Converte una stringa in caratteri minuscoli. | <ul><li>INGRESSO: **Obbligatorio** Stringa che verrà convertita in lettere minuscole.</li></ul> | lower(INPUT) | lower(&quot;HeLL&quot;)<br>lcase(&quot;HeLL&quot;) | &quot;hello&quot; |
| maiuscola /<br>ucase | Converte una stringa in caratteri maiuscoli. | <ul><li>INGRESSO: **Obbligatorio** Stringa che verrà convertita in maiuscolo.</li></ul> | Upper(INPUT) | Upper(&quot;HeLL&quot;)<br>ucase(&quot;HeLL&quot;) | &quot;HELLO&quot; |
| split | Divide una stringa di input su un separatore. Il seguente separatore **deve essere preceduto da** con `\`: `\`. | <ul><li>INGRESSO: **Obbligatorio** Stringa di input da dividere.</li><li>SEPARATORE: **Obbligatorio** Stringa utilizzata per suddividere l&#39;input.</li></ul> | split(INPUT, SEPARATORE) | split(&quot;Hello world&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Unisce un elenco di oggetti utilizzando il separatore. | <ul><li>SEPARATORE: **Obbligatorio** Stringa che verrà utilizzata per unire gli oggetti.</li><li>OGGETTI: **Obbligatorio** Un array di stringhe da unire.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Inserisce il lato sinistro di una stringa con l&#39;altra stringa specificata. | <ul><li>INGRESSO: **Obbligatorio** Stringa che verrà rimossa. Questa stringa può essere null.</li><li>CONTEGGIO: **Obbligatorio** Dimensione della stringa da aggiungere.</li><li>PADDING: **Obbligatorio** Stringa con cui aggiungere il pad dell&#39;input. Se null o empty, verrà trattato come un singolo spazio.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| pad | Inserisce il lato destro di una stringa con l&#39;altra stringa specificata. | <ul><li>INGRESSO: **Obbligatorio** Stringa che verrà rimossa. Questa stringa può essere null.</li><li>CONTEGGIO: **Obbligatorio** Dimensione della stringa da aggiungere.</li><li>PADDING: **Obbligatorio** Stringa con cui aggiungere il pad dell&#39;input. Se null o empty, verrà trattato come un singolo spazio.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Ottiene i primi caratteri &quot;n&quot; della stringa specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa per la quale si ottengono i primi caratteri &quot;n&quot;.</li><li>CONTEGGIO: **Obbligatorio** I caratteri &quot;n&quot; che si desidera ottenere dalla stringa.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Ottiene gli ultimi caratteri &quot;n&quot; della stringa specificata. | <ul><li>STRING: **Obbligatorio** La stringa per cui si ricevono gli ultimi caratteri &quot;n&quot;.</li><li>COUNT: **Obbligatorio** I caratteri &quot;n&quot; che si desidera ottenere dalla stringa.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Rimuove lo spazio vuoto dall&#39;inizio della stringa. | <ul><li>STRING: **Obbligatorio** La stringa da cui si desidera rimuovere lo spazio vuoto.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| rtrim | Rimuove lo spazio vuoto dalla fine della stringa. | <ul><li>STRING: **Obbligatorio** La stringa da cui si desidera rimuovere lo spazio vuoto.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Rimuove lo spazio vuoto dall&#39;inizio e dalla fine della stringa. | <ul><li>STRING: **Obbligatorio** La stringa da cui si desidera rimuovere lo spazio vuoto.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| è uguale a | Confronta due stringhe per verificare se sono uguali. Questa funzione fa distinzione tra maiuscole e minuscole. | <ul><li>STRING1: **Obbligatorio** La prima stringa da confrontare.</li><li>STRING2: **Obbligatorio** La seconda stringa da confrontare.</li></ul> | STRING1.&#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Confronta due stringhe per verificare se sono uguali. Questa funzione fa distinzione tra maiuscole e minuscole **non**. | <ul><li>STRING1: **Obbligatorio** La prima stringa da confrontare.</li><li>STRING2: **Obbligatorio** La seconda stringa da confrontare.</li></ul> | STRING1.&#x200B;equalsignoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsignoreCase &#x200B;(&quot;STRING1) | true |

&#x200B;

### Funzioni di espressione regolari

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| extract_regex | Estrae i gruppi dalla stringa di input in base a un&#39;espressione regolare. | <ul><li>STRING: **Obbligatorio** La stringa da cui si stanno estraendo i gruppi.</li><li>REGEX: **Obbligatorio** L&#39;espressione regolare che si desidera far corrispondere al gruppo.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Verifica se la stringa corrisponde all&#39;espressione regolare inserita. | <ul><li>STRING: **Obbligatorio** La stringa che si sta verificando corrisponde all&#39;espressione regolare.</li><li>REGEX: **Obbligatorio** L&#39;espressione regolare con cui si sta confrontando.</li></ul> | match_regex(STRING, REGEX) | match_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

### Funzioni di hash

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| sha1 | Assume un input e produce un valore hash utilizzando Secure Hash Algorithm 1 (SHA-1). | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da barrare.</li><li>CARSET: *Opzionale* Il nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;my text&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Assume un input e produce un valore hash utilizzando Secure Hash Algorithm 256 (SHA-256). | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da barrare.</li><li>CARSET: *Opzionale* Il nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;my text&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Assume un input e produce un valore hash utilizzando Secure Hash Algorithm 512 (SHA-512). | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da barrare.</li><li>CARSET: *Opzionale* Il nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;my text&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd077 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Assume un input e produce un valore hash utilizzando MD5. | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da barrare.</li><li>CARSET: *Opzionale* Il nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;my text&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Assume un input che utilizza un algoritmo di controllo della ridondanza ciclico (CRC) per produrre un codice ciclico a 32 bit. | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da barrare.</li><li>CARSET: *Opzionale* Il nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;my text&quot;, &quot;UTF-8&quot;) | 8df92e80 |

### Funzioni URL

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| get_url_Protocol | Restituisce il protocollo dall&#39;URL specificato. Se l&#39;input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** L&#39;URL da cui deve essere estratto il protocollo.</li></ul> | get_url_Protocol &#x200B;(URL) | get_url_Protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Restituisce l&#39;host dell&#39;URL specificato. Se l&#39;input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** L&#39;URL da cui l&#39;host deve essere estratto.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Restituisce la porta dell&#39;URL specificato. Se l&#39;input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** L&#39;URL da cui deve essere estratta la porta.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Restituisce il percorso dell&#39;URL specificato. Per impostazione predefinita, viene restituito il percorso completo. | <ul><li>URL: **Obbligatorio** L&#39;URL da cui deve essere estratto il percorso.</li><li>FULL_PATH: *Valore booleano opzionale* che determina se viene restituito il percorso completo. Se è impostata su false, viene restituita solo la fine del percorso.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B; employee.csv&quot; |
| get_url_query_str | Restituisce la stringa di query di un determinato URL. | <ul><li>URL: **Obbligatorio** L&#39;URL da cui si sta tentando di ottenere la stringa di query.</li><li>ANCORAGGIO: **Obbligatorio** Determina l&#39;operazione che verrà eseguita con l&#39;ancoraggio nella stringa di query. Può essere uno dei tre valori seguenti: &quot;maintain&quot;, &quot;remove&quot; o &quot;append&quot;.<br><br>Se il valore è &quot;maintain&quot;, l&#39;ancoraggio viene associato al valore restituito.<br>Se il valore è &quot;remove&quot;, l&#39;ancoraggio viene rimosso dal valore restituito.<br>Se il valore è &quot;append&quot;, l&#39;ancoraggio viene restituito come valore separato.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;maintain&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/there?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com&quot;:8042/over/there?name=ferret?name#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

### Funzioni di data e ora

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella. Ulteriori informazioni sulla funzione `date` sono disponibili nella [guida alla funzione data](./dates.md).

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| now | Recupera l&#39;ora corrente. |  | now() | now() | `2020-09-23T10:10:24.556-07:00[America/Los_Angeles]` |
| timestamp | Recupera l&#39;ora Unix corrente. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formatta la data di input in base a un formato specificato. | <ul><li>DATA: **Obbligatorio** La data di input, sotto forma di oggetto ZoningDateTime, che si desidera formattare.</li><li>FORMATO: **Obbligatorio** Formato in cui si desidera modificare la data.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11:24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | &quot;2019-10-23 11:24:35&quot; |
| dformat | Converte un indicatore di data e ora in una stringa di data in base a un formato specificato. | <ul><li>TIMESTAMP: **Obbligatorio** La marca temporale che si desidera formattare. Questo viene scritto in millisecondi.</li><li>FORMATO: **Obbligatorio** Formato in cui si desidera modificare la marca temporale.</li></ul> | dformat &#x200B;(TIMESTAMP, FORMAT) | dformat(1571829875, &quot;dd-MMM-yyyy hh:mm&quot;) | &quot;23-ott-2019 11:24&quot; |
| data | Converte una stringa data in un oggetto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** La stringa che rappresenta la data.</li><li>FORMATO: **Obbligatorio** La stringa che rappresenta il formato della data.</li><li>DEFAULT_DATE: **Obbligatorio** La data predefinita restituita, se la data specificata è null.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now() | &quot;2019-10-23T11:24Z&quot; |
| data | Converte una stringa data in un oggetto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** La stringa che rappresenta la data.</li><li>FORMATO: **Obbligatorio** La stringa che rappresenta il formato della data.</li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | &quot;2019-10-23T11:24Z&quot; |
| data | Converte una stringa data in un oggetto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** La stringa che rappresenta la data.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24Z&quot; |
| date_part | Recupera le parti della data. Sono supportati i seguenti valori dei componenti: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;trimestri&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;dy&quot;&lt;a0 11/>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;week day&quot;<br>&quot;dw&quot;&lt;a 20/>&quot;w&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecond&quot;<br>&quot;ms&quot;<br><br> | <ul><li>COMPONENTE: **Obbligatorio** Una stringa che rappresenta la parte della data. </li><li>DATA: **Obbligatorio** La data, in un formato standard.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | Sostituisce un componente in una data specifica. Sono accettati i seguenti componenti: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;yy&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;hour&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPONENTE: **Obbligatorio** Una stringa che rappresenta la parte della data. </li><li>VALORE: **Obbligatorio** Il valore da impostare per il componente per una data specifica.</li><li>DATA: **Obbligatorio** La data, in un formato standard.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, data(&quot;2016-11-09T11:44:44.797&quot;) | &quot;2016-04-09T11:44:44.797&quot; |
| make_date_time | Crea una data da parti. Questa funzione può essere indotta anche mediante make_timestamp. | <ul><li>ANNO: **Obbligatorio** L&#39;anno, scritto in quattro cifre.</li><li>MESE: **Obbligatorio** Il mese. I valori consentiti sono compresi tra 1 e 12.</li><li>GIORNO: **Obbligatorio** Il giorno. I valori consentiti sono compresi tra 1 e 31.</li><li>ORA: **Obbligatorio** L&#39;ora. I valori consentiti sono compresi tra 0 e 23.</li><li>MINUTO: **Obbligatorio** Il minuto. I valori consentiti sono compresi tra 0 e 59.</li><li>NANOSECONDO: **Valore obbligatorio** I valori dei nanosecondi. I valori consentiti sono compresi tra 0 e 99999999.</li><li>TIMEZONE: **Obbligatorio** Il fuso orario per l&#39;ora della data.</li></ul> | make_date_time &#x200B;(ANNO, MESE, GIORNO, ORA, MINUTO, SECONDO, NANOSECONDO, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12.0&#x200B;00000999-07:00[America/Los_Angeles]` |
| zone_date_to_utc | Converte una data in qualsiasi fuso orario in una data in UTC. | <ul><li>DATA: **Obbligatorio** La data che si sta tentando di convertire.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12.000000999-&#x200B;07:00[America/Los_Angeles])` | `2019-10-17T18:55:12.000000999Z[UTC]` |
| zone_date_to_zone | Converte una data da un fuso orario a un altro. | <ul><li>DATA: **Obbligatorio** La data che si sta tentando di convertire.</li><li>ZONA: **Obbligatorio** Il fuso orario in cui si sta tentando di convertire la data.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:12&#x200B;.000000999-07:00&#x200B;[America/Los_Angeles], "Europe/Paris")` | `2019-10-17T20:55:12.000000999+02:00[Europe/Paris]` |

&#x200B;

### Gerarchie - Oggetti

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| size_of | Restituisce le dimensioni dell&#39;input. | <ul><li>INGRESSO: **Obbligatorio** L&#39;oggetto di cui si sta tentando di trovare le dimensioni.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| is_empty | Verifica se un oggetto è vuoto o meno. | <ul><li>INGRESSO: **Obbligatorio** L&#39;oggetto che si sta tentando di controllare è vuoto.</li></ul> | is_blank(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | Crea un elenco di oggetti. | <ul><li>INGRESSO: **Obbligatorio** Raggruppamento di coppie chiave/array.</li></ul> | array_to_object(INPUT) | bisogno di un campione | bisogno di un campione |
| to_object | Crea un oggetto in base alle coppie chiave/valore flat date. | <ul><li>INGRESSO: **Obbligatorio** Elenco semplice di coppie chiave/valore.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crea un oggetto dalla stringa di input. | <ul><li>STRING: **Obbligatorio** La stringa che viene analizzata per creare un oggetto.</li><li>VALUE_DELIMITER: *Opzionale* Il delimitatore che separa un campo dal valore. Il delimitatore predefinito è `:`.</li><li>FIELD_DELIMITER: *Opzionale* Il delimitatore che separa coppie di valori campo. Il delimitatore predefinito è `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName - John | lastName - | telefono - 123 456 7890&quot;, &quot;-&quot;, &quot; | &quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| is_set | Verifica se l&#39;oggetto esiste nei dati di origine. | <ul><li>INGRESSO: **Obbligatorio** Percorso da verificare se esiste nei dati di origine.</li></ul> | is_set(INPUT) | is_set &#x200B;(&quot;evars.evar.field1&quot;) | true |
| annullare | Imposta il valore dell&#39;attributo su `null`. Questa opzione deve essere utilizzata se non si desidera copiare il campo nello schema di destinazione. |  | nullify() | nullify() | `null` |

### Gerarchie - Array

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| fondersi | Restituisce il primo oggetto diverso da null in un determinato array. | <ul><li>INGRESSO: **Obbligatorio** L&#39;array di cui si desidera trovare il primo oggetto diverso da null.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;seconda&quot;) | &quot;first&quot; |
| primo | Recupera il primo elemento dell&#39;array specificato. | <ul><li>INGRESSO: **Obbligatorio** L&#39;array di cui si desidera trovare il primo elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera l&#39;ultimo elemento dell&#39;array specificato. | <ul><li>INGRESSO: **Obbligatorio** L&#39;array di cui si desidera trovare l&#39;ultimo elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| to_array | Scrive un elenco di input e lo converte in un array. | <ul><li>INCLUDE_NULLS: **Valore booleano obbligatorio** per indicare se includere o meno i Null nell&#39;array di risposte.</li><li>VALORI: **Elemento** obbligatorio che deve essere convertito in un array.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |

### Operatori logici

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| decodificare | Data una chiave e un elenco di coppie di valori chiave appiattite come array, la funzione restituisce il valore se la chiave viene trovata o restituisce un valore predefinito se presente nell&#39;array. | <ul><li>CHIAVE: **Obbligatorio** Il tasto da associare.</li><li>OPTIONS : **Obbligatorio** Un array appiattito di coppie chiave/valore. Facoltativamente, un valore predefinito può essere messo alla fine.</li></ul> | decode(KEY,  OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Se stateCode dato è &quot;ca&quot;, &quot;California&quot;.<br>Se il codice di stato fornito è &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Se stateCode non corrisponde a quanto segue, &quot;N/D&quot;. |
| iif | Valuta una determinata espressione booleana e restituisce il valore specificato in base al risultato. | <ul><li>ESPRESSIONE: **Obbligatorio** L&#39;espressione booleana in corso di valutazione.</li><li>TRUE_VALUE: **Required** Il valore restituito se l&#39;espressione restituisce true.</li><li>FALSE_VALUE: **Required** Il valore restituito se l&#39;espressione restituisce false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsignoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

### Aggregazione

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| min | Restituisce il minimo degli argomenti specificati. Usa l&#39;ordine naturale. | <ul><li>OPTIONS : **Obbligatorio** Uno o più oggetti che possono essere confrontati l&#39;uno con l&#39;altro.</li></ul> | min( OPTIONS) | min(3, 1, 4) | 1 |
| max | Restituisce il massimo degli argomenti specificati. Usa l&#39;ordine naturale. | <ul><li>OPTIONS : **Obbligatorio** Uno o più oggetti che possono essere confrontati l&#39;uno con l&#39;altro.</li></ul> | max( OPTIONS) | max(3, 1, 4) | 4 |

### Conversioni di tipo

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| to_bigint | Converte una stringa in un oggetto BigInteger. | <ul><li>STRING: **Obbligatorio** La stringa da convertire in un oggetto BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Converte una stringa in un valore Double. | <ul><li>STRING: **Obbligatorio** La stringa da convertire in un valore Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Converte una stringa in un valore Float. | <ul><li>STRING: **Obbligatorio** La stringa da convertire in un valore Float.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Converte una stringa in un valore Integer. | <ul><li>STRING: **Obbligatorio** La stringa da convertire in un numero intero.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

### Funzioni JSON

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| json_to_object | Deserializzare il contenuto JSON dalla stringa specificata. | <ul><li>STRING: **Obbligatorio** La stringa JSON da deserializzare.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Un oggetto che rappresenta il JSON. |

### Operazioni speciali

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| uuid /<br>guid | Genera un ID pseudo-casuale. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

### Funzioni agente utente

>[!NOTE]
>
>Scorrete verso sinistra/destra per visualizzare l&#39;intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
-------- | ----------- | ---------- | -------| ---------- | -------------
| ua_os_name | Estrae il nome del sistema operativo dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Estrae la versione principale del sistema operativo dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Estrae la versione del sistema operativo dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1 |
| ua_os_name_version | Estrae il nome e la versione del sistema operativo dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Estrae la versione dell&#39;agente dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Estrae il nome dell&#39;agente e la versione principale dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Estrae il nome dell&#39;agente dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Estrae la classe dispositivo dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** La stringa agente utente.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefono |