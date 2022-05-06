---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv su xdm;mappare da csv a xdm;guida interfaccia utente;mappatura;mappatura;campi di mappatura;funzioni di mappatura;
solution: Experience Platform
title: Funzioni di mappatura della preparazione dei dati
topic-legacy: overview
description: Questo documento introduce le funzioni di mappatura utilizzate con Data Prep.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: 14c7c3bd0bda0ab56767b9c0f5470090cf2bdb15
workflow-type: tm+mt
source-wordcount: '4164'
ht-degree: 3%

---

# Funzioni di mappatura della preparazione dei dati

Le funzioni di preparazione dei dati possono essere utilizzate per calcolare e calcolare i valori in base a quanto immesso nei campi di origine.

## Campi

Un nome campo può essere un qualsiasi identificatore legale, ovvero una sequenza illimitata di lettere e cifre Unicode, che inizia con una lettera, il simbolo del dollaro (`$`) o il carattere di sottolineatura (`_`). Anche i nomi delle variabili sono sensibili all’uso di maiuscole e minuscole.

Se il nome di un campo non segue questa convenzione, è necessario racchiudere il nome del campo con `${}`. Quindi, ad esempio, se il nome del campo è &quot;Nome&quot; o &quot;Nome.Nome&quot;, il nome deve essere racchiuso come `${First Name}` o `${First.Name}` rispettivamente.

Inoltre, se il nome di un campo è **qualsiasi** delle seguenti parole chiave riservate, deve essere racchiuso con `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return
```

È possibile accedere ai dati contenuti nei campi secondari utilizzando la notazione del punto. Ad esempio, se era presente un `name` per accedere all&#39;oggetto `firstName` campo, utilizzare `name.firstName`.

## Elenco delle funzioni

Nelle tabelle seguenti sono elencate tutte le funzioni di mappatura supportate, incluse le espressioni di esempio e i relativi output risultanti.

### Funzioni stringa {#string}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Concatena le stringhe specificate. | <ul><li>STRINGA: Stringhe che verranno concatenate.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Ciao, &quot;, &quot;ci&quot;, &quot;!&quot;) | `"Hi, there!"` |
| esplodere | Divide la stringa in base a un regex e restituisce un array di parti. Facoltativamente, può includere regex per dividere la stringa. Per impostazione predefinita, la divisione viene risolta in &quot;,&quot;. I seguenti delimitatori **necessità** deve essere evitato con `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Se si includono più caratteri come delimitatore, questo viene considerato come un delimitatore a più caratteri. | <ul><li>STRINGA: **Obbligatorio** Stringa da dividere.</li><li>REGEX: *Facoltativo* Espressione regolare che può essere utilizzata per dividere la stringa.</li></ul> | esplode(STRINGA, REGEX) | esplode(&quot;Ciao!&quot;, &quot; &quot;) | `["Hi,", "there"]` |
| instr | Restituisce la posizione/indice di una sottostringa. | <ul><li>INGRESSO: **Obbligatorio** Stringa in corso di ricerca.</li><li>SOTTOSTRINGA: **Obbligatorio** Sottostringa alla quale viene eseguita la ricerca all’interno della stringa.</li><li>AVVIO_POSIZIONE: *Facoltativo* La posizione in cui iniziare a cercare nella stringa.</li><li>OCCORRENZA: *Facoltativo* L&#39;ennesima occorrenza da cercare dalla posizione iniziale. Per impostazione predefinita, è 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| sostituto | Sostituisce la stringa di ricerca se presente nella stringa originale. | <ul><li>INGRESSO: **Obbligatorio** Stringa di input.</li><li>TO_TROVA: **Obbligatorio** Stringa da cercare all’interno dell’input.</li><li>TO_SOSTITUISCI: **Obbligatorio** Stringa che sostituirà il valore all&#39;interno di &quot;TO_FIND&quot;.</li></ul> | replace(INPUT, TO_FIND, TO_REPLACE) | replace(&quot;Questa è una stringa ri test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Questo è un test di sostituzione stringa&quot; |
| substr | Restituisce una sottostringa di una lunghezza specificata. | <ul><li>INGRESSO: **Obbligatorio** Stringa di input.</li><li>START_INDEX: **Obbligatorio** Indice della stringa di input da cui inizia la sottostringa.</li><li>LUNGHEZZA: **Obbligatorio** Lunghezza della sottostringa.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;This is a substring test&quot;, 7, 8) | &quot;a subst&quot; |
| Lower /<br>cassa | Converte una stringa in minuscolo. | <ul><li>INGRESSO: **Obbligatorio** Stringa che verrà convertita in minuscolo.</li></ul> | Lower(INPUT) | lower(&quot;HeTo&quot;)<br>lcase(&quot;HeTo&quot;) | &quot;hello&quot; |
| superiore /<br>ucasi | Converte una stringa in maiuscolo. | <ul><li>INGRESSO: **Obbligatorio** Stringa che verrà convertita in maiuscolo.</li></ul> | Upper(INPUT) | Upper(&quot;HeTo&quot;)<br>ucase(&quot;HeTo&quot;) | &quot;CIAO&quot; |
| split | Divide una stringa di input su un separatore. Il seguente separatore **esigenze** deve essere evitato con `\`: `\`. Se si includono più delimitatori, la stringa verrà suddivisa in **qualsiasi** dei delimitatori presenti nella stringa. | <ul><li>INGRESSO: **Obbligatorio** Stringa di input da dividere.</li><li>SEPARATORE: **Obbligatorio** Stringa utilizzata per dividere l&#39;input.</li></ul> | split(INGRESSO, SEPARATORE) | split(&quot;Ciao mondo&quot;, &quot; &quot;) | `["Hello", "world"]` |
| join | Unisce un elenco di oggetti utilizzando il separatore. | <ul><li>SEPARATORE: **Obbligatorio** Stringa che verrà utilizzata per unire gli oggetti.</li><li>OGGETTI: **Obbligatorio** Matrice di stringhe da unire.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Ciao a tutti&quot; |
| lembo | Aggiunge il lato sinistro di una stringa con l&#39;altra stringa specificata. | <ul><li>INGRESSO: **Obbligatorio** Stringa da eliminare. Questa stringa può essere null.</li><li>CONTEGGIO: **Obbligatorio** Dimensione della stringa da eliminare.</li><li>AGGIUNTA: **Obbligatorio** Stringa con cui incollare l’input. Se null o empty, verrà trattato come un singolo spazio.</li></ul> | Lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;yzyzybat&quot; |
| tappetino | Aggiunge il lato destro di una stringa all&#39;altra stringa specificata. | <ul><li>INGRESSO: **Obbligatorio** Stringa da eliminare. Questa stringa può essere null.</li><li>CONTEGGIO: **Obbligatorio** Dimensione della stringa da eliminare.</li><li>AGGIUNTA: **Obbligatorio** Stringa con cui incollare l’input. Se null o empty, verrà trattato come un singolo spazio.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| sinistra | Ottiene i primi caratteri &quot;n&quot; della stringa specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa per la quale si ottengono i primi caratteri &quot;n&quot;.</li><li>CONTEGGIO: **Obbligatorio** I caratteri &quot;n&quot; che si desidera ottenere dalla stringa.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| right | Ottiene gli ultimi caratteri &quot;n&quot; della stringa specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa per la quale si ricevono gli ultimi caratteri &quot;n&quot;.</li><li>CONTEGGIO: **Obbligatorio** I caratteri &quot;n&quot; che si desidera ottenere dalla stringa.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Rimuove lo spazio vuoto dall’inizio della stringa. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui si desidera rimuovere lo spazio vuoto.</li></ul> | ltrim(STRING) | ltrim(&quot; hello&quot;) | &quot;hello&quot; |
| trim | Rimuove lo spazio vuoto dalla fine della stringa. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui si desidera rimuovere lo spazio vuoto.</li></ul> | rtrim(STRING) | rtrim(&quot;hello &quot;) | &quot;hello&quot; |
| trim | Rimuove lo spazio vuoto dall’inizio e dalla fine della stringa. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui si desidera rimuovere lo spazio vuoto.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;hello&quot; |
| è uguale a | Confronta due stringhe per confermare se sono uguali. Questa funzione distingue tra maiuscole e minuscole. | <ul><li>STRINGA1: **Obbligatorio** La prima stringa da confrontare.</li><li>STRINGA2: **Obbligatorio** Seconda stringa da confrontare.</li></ul> | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;è uguale a &#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Confronta due stringhe per confermare se sono uguali. Questa funzione è **not** sensibile a maiuscole e minuscole. | <ul><li>STRINGA1: **Obbligatorio** La prima stringa da confrontare.</li><li>STRINGA2: **Obbligatorio** Seconda stringa da confrontare.</li></ul> | STRING1. &#x200B;equalsIgnoreCase &#x200B;(STRING2) | &quot;string1&quot;. &#x200B;equalsIgnoreCase &#x200B;(&quot;STRING1) | true |

{style=&quot;table-layout:auto&quot;}

### Funzioni con espressione regolare

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Estrae i gruppi dalla stringa di input, in base a un&#39;espressione regolare. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui si stanno estraendo i gruppi.</li><li>REGEX: **Obbligatorio** L&#39;espressione regolare a cui si desidera associare il gruppo.</li></ul> | extract_regex(STRING, REGEX) | extract_regex &#x200B;(&quot;E259,E259B_009,1_1&quot; &#x200B;, &quot;([^]+),[^]*,([^]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Controlla se la stringa corrisponde all&#39;espressione regolare inserita. | <ul><li>STRINGA: **Obbligatorio** La stringa che stai controllando corrisponde all&#39;espressione regolare.</li><li>REGEX: **Obbligatorio** L&#39;espressione regolare con cui si confronta.</li></ul> | match_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^]+),[^]*,([^]+)&quot;) | true |

{style=&quot;table-layout:auto&quot;}

### Funzioni di hashing {#hashing}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Prende un input e produce un valore hash utilizzando Secure Hash Algorithm 1 (SHA-1). | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da hash.</li><li>CARATTERE: *Facoltativo* Nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24 &#x200B; 48690840c5dfcce3c80 |
| sha256 | Prende un input e produce un valore hash utilizzando Secure Hash Algorithm 256 (SHA-256). | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da hash.</li><li>CARATTERE: *Facoltativo* Nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21 &#x200B; e6a39af698154a83a586ee270a0d372104 |
| sha512 | Prende un input e produce un valore hash utilizzando Secure Hash Algorithm 512 (SHA-512). | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da hash.</li><li>CARATTERE: *Facoltativo* Nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be5fd4e4b9a3b8c9c2163c21ef &#x200B; 708bf11b4232bb21d2a8704ada2cdcd7b367dd07 88a89 &#x200B; a5c908cfe377aceb1072a7b386b7d4fd2ff68a8fd24d16 |
| md5 | Prende un input e produce un valore hash utilizzando MD5. | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da hash.</li><li>CARATTERE: *Facoltativo* Nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4 &#x200B; e9bd0198d03ba6852c7 |
| crc32 | Accetta un input che utilizza un algoritmo di controllo della ridondanza ciclica (CRC) per produrre un codice ciclico a 32 bit. | <ul><li>INGRESSO: **Obbligatorio** Il testo normale da hash.</li><li>CARATTERE: *Facoltativo* Nome del set di caratteri. I valori possibili sono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | crc32 (INGRESSO, CHARSET) | crc32(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style=&quot;table-layout:auto&quot;}

### Funzioni URL {#url}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Restituisce il protocollo dall&#39;URL specificato. Se l&#39;input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** URL da cui è necessario estrarre il protocollo.</li></ul> | get_url_protocol &#x200B;(URL) | get_url_protocol(&quot;https://platform &#x200B; .adobe.com/home&quot;) | https |
| get_url_host | Restituisce l&#39;host dell&#39;URL specificato. Se l&#39;input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** L’URL da cui l’host deve essere estratto.</li></ul> | get_url_host &#x200B;(URL) | get_url_host &#x200B;(&quot;https://platform &#x200B; .adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Restituisce la porta dell’URL specificato. Se l&#39;input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** URL da cui estrarre la porta.</li></ul> | get_url_port(URL) | get_url_port &#x200B;(&quot;sftp://example.com//home/ &#x200B; joe/employee.csv&quot;) | 22 |
| get_url_path | Restituisce il percorso dell&#39;URL specificato. Per impostazione predefinita, viene restituito il percorso completo. | <ul><li>URL: **Obbligatorio** URL da cui estrarre il percorso.</li><li>FULL_PATH: *Facoltativo* Un valore booleano che determina se viene restituito il percorso completo. Se è impostato su false, viene restituita solo la fine del percorso.</li></ul> | get_url_path &#x200B;(URL, FULL_PATH) | get_url_path &#x200B;(&quot;sftp://example.com// &#x200B; home/joe/employee.csv&quot;) | &quot;//home/joe/ &#x200B;.csv&quot; |
| get_url_query_str | Restituisce la stringa di query di un URL specificato. | <ul><li>URL: **Obbligatorio** URL da cui si sta tentando di ottenere la stringa di query.</li><li>ANCORAGGIO: **Obbligatorio** Determina l’operazione che verrà eseguita con l’ancoraggio nella stringa di query. Può essere uno dei tre valori seguenti: &quot;keep&quot;, &quot;remove&quot; o &quot;append&quot;.<br><br>Se il valore è &quot;keep&quot;, l’ancoraggio viene associato al valore restituito.<br>Se il valore è &quot;remove&quot;, l’ancoraggio viene rimosso dal valore restituito.<br>Se il valore è &quot;append&quot;, l’ancoraggio viene restituito come valore separato.</li></ul> | get_url_query_str &#x200B;(URL, ANCHOR) | get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/here?name= &#x200B; ferret#nose&quot;, &quot;keep&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com:8042 &#x200B;/over/here?name= &#x200B; ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str &#x200B;(&quot;foo://example.com &#x200B;:8042/over/there &#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |

{style=&quot;table-layout:auto&quot;}

### Funzioni di data e ora {#date-and-time}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella. Ulteriori informazioni sulle `date` si trova nella sezione date del [guida alla gestione del formato dati](./data-handling.md#dates).

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Recupera l&#39;ora corrente. |  | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | Recupera l&#39;ora Unix corrente. |  | timestamp() | timestamp() | 1571850624571 |
| format | Formatta la data di input in base a un formato specificato. | <ul><li>DATA: **Obbligatorio** La data di input, sotto forma di oggetto ZoningDateTime, che si desidera formattare.</li><li>FORMATO: **Obbligatorio** Formato in cui si desidera modificare la data.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11):24:00+00:00, &quot;aaaa-MM-gg HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| dformat | Converte una marca temporale in una stringa di data in base a un formato specificato. | <ul><li>MARCA TEMPORALE: **Obbligatorio** La marca temporale che si desidera formattare. Scritto in millisecondi.</li><li>FORMATO: **Obbligatorio** Il formato che si desidera che diventi la marca temporale.</li></ul> | dformat(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;aaaa-MM-gg-T&#39;HH:mm:ss.SSSX&quot;) | `2019-10-23T11:24:35.000Z` |
| data | Converte una stringa data in un oggetto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** Stringa che rappresenta la data.</li><li>FORMATO: **Obbligatorio** Stringa che rappresenta il formato della data di origine.**Nota:** Questo **not** rappresenta il formato in cui si desidera convertire la stringa di data. </li><li>DEFAULT_DATE: **Obbligatorio** La data predefinita restituita, se la data fornita è null.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-gg HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| data | Converte una stringa data in un oggetto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** Stringa che rappresenta la data.</li><li>FORMATO: **Obbligatorio** Stringa che rappresenta il formato della data di origine.**Nota:** Questo **not** rappresenta il formato in cui si desidera convertire la stringa di data. </li></ul> | date(DATA, FORMATO) | date(&quot;2019-10-23 11:24&quot;, &quot;aaaa-MM-gg HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| data | Converte una stringa data in un oggetto ZoningDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** Stringa che rappresenta la data.</li></ul> | data(DATA) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Recupera le parti della data. Sono supportati i seguenti valori dei componenti: <br><br>&quot;anno&quot;<br>&quot;aaaa&quot;<br>Sì<br><br>&quot;trimestre&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;mese&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;giorno dell&#39;anno&quot;<br>&quot;dy&quot;<br>&quot;y&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;giorno feriale&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;ora&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minuto&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;secondo&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecondo&quot;<br>&quot;ms&quot; | <ul><li>COMPONENTE: **Obbligatorio** Una stringa che rappresenta la parte della data. </li><li>DATA: **Obbligatorio** La data, in un formato standard.</li></ul> | date_part &#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | Sostituisce un componente in una data specificata. Sono accettati i seguenti componenti: <br><br>&quot;anno&quot;<br>&quot;aaaa&quot;<br>Sì<br><br>&quot;mese&quot;<br>&quot;mm&quot;<br>&quot;m&quot;<br><br>&quot;day&quot;<br>&quot;dd&quot;<br>&quot;d&quot;<br><br>&quot;ora&quot;<br>&quot;hh&quot;<br><br>&quot;minuto&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;secondo&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPONENTE: **Obbligatorio** Una stringa che rappresenta la parte della data. </li><li>VALORE: **Obbligatorio** Il valore da impostare per il componente per una data specificata.</li><li>DATA: **Obbligatorio** La data, in un formato standard.</li></ul> | set_date_part &#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44,797&quot;) | &quot;2016-04-09T11:44:44Z&quot; |
| make_date_time | Crea una data da parti. Questa funzione può essere indotta anche utilizzando make_timestamp. | <ul><li>ANNO: **Obbligatorio** L&#39;anno, scritto in quattro cifre.</li><li>MESE: **Obbligatorio** Il mese. I valori consentiti sono compresi tra 1 e 12.</li><li>GIORNO: **Obbligatorio** La giornata. I valori consentiti sono compresi tra 1 e 31.</li><li>ORA: **Obbligatorio** L&#39;ora. I valori consentiti sono compresi tra 0 e 23.</li><li>MINUTO: **Obbligatorio** Il minuto. I valori consentiti sono compresi tra 0 e 59.</li><li>NANOSECONDO: **Obbligatorio** I valori nanosecondi. I valori consentiti sono compresi tra 0 e 999999999.</li><li>FUSO ORARIO: **Obbligatorio** Il fuso orario per l’ora della data.</li></ul> | make_date_time &#x200B;(ANNO, MESE, GIORNO, ORA, MINUTO, SECONDO, NANOSECOND, TIMEZONE) | make_date_time &#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Converte una data in qualsiasi fuso orario in una data in UTC. | <ul><li>DATA: **Obbligatorio** Data in cui si sta tentando di convertire.</li></ul> | zone_date_to_utc &#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Converte una data da un fuso orario a un altro. | <ul><li>DATA: **Obbligatorio** Data in cui si sta tentando di convertire.</li><li>ZONA: **Obbligatorio** Il fuso orario in cui si sta tentando di convertire la data.</li></ul> | zone_date_to_zone &#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style=&quot;table-layout:auto&quot;}
&#x200B;

### Gerarchie - Oggetti {#objects}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Controlla se un oggetto è vuoto o meno. | <ul><li>INGRESSO: **Obbligatorio** L&#39;oggetto che si sta tentando di controllare è vuoto.</li></ul> | is_empty(INPUT) | `is_empty([1, 2, 3])` | false |
| array_to_object | Crea un elenco di oggetti. | <ul><li>INGRESSO: **Obbligatorio** Un raggruppamento di coppie chiave-array.</li></ul> | array_to_object(INPUT) | campione necessario | campione necessario |
| to_object | Crea un oggetto in base alle coppie chiave/valore flat specificate. | <ul><li>INGRESSO: **Obbligatorio** Elenco semplice di coppie chiave/valore.</li></ul> | to_object(INPUT) | to_object &#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crea un oggetto dalla stringa di input. | <ul><li>STRINGA: **Obbligatorio** Stringa da analizzare per creare un oggetto.</li><li>VALUE_DELIMITER: *Facoltativo* Il delimitatore che separa un campo dal valore. Il delimitatore predefinito è `:`.</li><li>FIELD_DELIMITER: *Facoltativo* Il delimitatore che separa le coppie di valori di campo. Il delimitatore predefinito è `,`.</li></ul> | str_to_object &#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) | str_to_object(&quot;firstName=John,lastName=Doe,phone=123 456 7890&quot;, &quot;=&quot;, &quot;,&quot;) | `{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}` |
| contains_key | Controlla se l&#39;oggetto esiste all&#39;interno dei dati di origine. **Nota:** Questa funzione sostituisce la funzione obsoleta `is_set()` funzione . | <ul><li>INGRESSO: **Obbligatorio** Percorso da verificare se esiste all’interno dei dati di origine.</li></ul> | contains_key(INPUT) | contains_key(&quot;evar.evar.field1&quot;) | true |
| annullare | Imposta il valore dell&#39;attributo su `null`. Da utilizzare quando non si desidera copiare il campo nello schema di destinazione. |  | nullify() | nullify() | `null` |
| get_keys | Analizza le coppie chiave/valore e restituisce tutte le chiavi. | <ul><li>OGGETTO: **Obbligatorio** L&#39;oggetto da cui verranno estratte le chiavi.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;): &quot;Orgoglio e pregiudizio&quot;, &quot;libro2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analizza le coppie chiave/valore e restituisce il valore della stringa, in base alla chiave specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa da analizzare.</li><li>CHIAVE: **Obbligatorio** Chiave per cui estrarre il valore.</li><li>VALUE_DELIMITER: **Obbligatorio** Il delimitatore che separa il campo e il valore. Se `null` oppure viene fornita una stringa vuota, questo valore è `:`.</li><li>FIELD_DELIMITER: *Facoltativo* Il delimitatore che separa le coppie di campi e valori. Se `null` oppure viene fornita una stringa vuota, questo valore è `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , telefono - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |

{style=&quot;table-layout:auto&quot;}

Per informazioni sulla funzione di copia dell’oggetto, consulta la sezione . [di seguito](#object-copy).

### Gerarchie - Array {#arrays}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| fondere | Restituisce il primo oggetto non-null in una matrice specificata. | <ul><li>INGRESSO: **Obbligatorio** Matrice di cui si desidera trovare il primo oggetto non nullo.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;secondo&quot;) | &quot;first&quot; |
| first | Recupera il primo elemento dell’array specificato. | <ul><li>INGRESSO: **Obbligatorio** La matrice di cui si desidera trovare il primo elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| last | Recupera l&#39;ultimo elemento dell&#39;array specificato. | <ul><li>INGRESSO: **Obbligatorio** Matrice di cui si desidera trovare l’ultimo elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;3&quot; |
| add_to_array | Aggiunge elementi alla fine della matrice. | <ul><li>ARRAY: **Obbligatorio** Matrice a cui si aggiungono gli elementi.</li><li>VALORI: Gli elementi che si desidera aggiungere alla matrice.</li></ul> | add_to_array &#x200B;(ARRAY, VALUES) | add_to_array &#x200B;([&quot;a&quot;, &quot;b&quot;], &quot;c&quot;, &quot;d&quot;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_array | Combina gli array tra loro. | <ul><li>ARRAY: **Obbligatorio** Matrice a cui si aggiungono gli elementi.</li><li>VALORI: Matrice da aggiungere alla matrice padre.</li></ul> | join_array &#x200B;(ARRAY, VALUES) | join_array &#x200B;([&quot;a&quot;, &quot;b&quot;], [&#39;c&#39;], [&quot;d&quot;, &quot;e&quot;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Prende un elenco di input e lo converte in un array. | <ul><li>INCLUDE_NULLS: **Obbligatorio** Un valore booleano per indicare se includere o meno i valori Null nell&#39;array di risposta.</li><li>VALORI: **Obbligatorio** Gli elementi da convertire in una matrice.</li></ul> | to_array &#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Restituisce le dimensioni dell’input. | <ul><li>INGRESSO: **Obbligatorio** L&#39;oggetto di cui si sta tentando di trovare le dimensioni.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |

{style=&quot;table-layout:auto&quot;}

### Operatori logici {#logical-operators}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decodificare | Dato un tasto e un elenco di coppie di valori chiave appiattite come array, la funzione restituisce il valore se key viene trovato o restituisce un valore predefinito se presente nell&#39;array. | <ul><li>CHIAVE: **Obbligatorio** Chiave a cui deve corrispondere.</li><li>OPTIONS: **Obbligatorio** Matrice appiattita di coppie chiave/valore. Facoltativamente, è possibile inserire un valore predefinito alla fine.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Se il codice di stato specificato è &quot;ca&quot;, &quot;California&quot;.<br>Se lo statoCode dato è &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Se stateCode non corrisponde a quanto segue, &quot;N/D&quot;. |
| iif | Valuta una determinata espressione booleana e restituisce il valore specificato in base al risultato. | <ul><li>ESPRESSIONE: **Obbligatorio** Espressione booleana in fase di valutazione.</li><li>TRUE_VALUE: **Obbligatorio** Il valore restituito se l&#39;espressione restituisce true.</li><li>FALSE_VALUE: **Obbligatorio** Il valore restituito se l&#39;espressione restituisce false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |

{style=&quot;table-layout:auto&quot;}

### Aggregazione {#aggregation}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Restituisce il minimo degli argomenti specificati. Utilizza l&#39;ordine naturale. | <ul><li>OPTIONS: **Obbligatorio** Uno o più oggetti confrontabili tra loro.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Restituisce il massimo degli argomenti specificati. Utilizza l&#39;ordine naturale. | <ul><li>OPTIONS: **Obbligatorio** Uno o più oggetti confrontabili tra loro.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style=&quot;table-layout:auto&quot;}

### Conversioni di tipo {#type-conversions}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Converte una stringa in un BigInteger. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in BigInteger.</li></ul> | to_bigint(STRING) | to_bigint &#x200B;(&quot;100000.34&quot;) | 1000000,34 |
| to_decimal | Converte una stringa in un valore Double. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Converte una stringa in Mobile. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in Mobile.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Converte una stringa in un numero intero. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in un numero intero.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style=&quot;table-layout:auto&quot;}

### Funzioni JSON {#json}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserializza il contenuto JSON dalla stringa specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa JSON da deserializzare.</li></ul> | json_to_object &#x200B;(STRING) | json_to_object &#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}) | Un oggetto che rappresenta il JSON. |

{style=&quot;table-layout:auto&quot;}

### Operazioni speciali {#special-operations}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>guid | Genera un ID pseudo-casuale. |  | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |

{style=&quot;table-layout:auto&quot;}

### Funzioni dell&#39;agente utente {#user-agent}

>[!NOTE]
>
>Scorri verso sinistra/destra per visualizzare il contenuto completo della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Estrae il nome del sistema operativo dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_os_name &#x200B;(USER_AGENT) | ua_os_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Estrae la versione principale del sistema operativo dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_os_version_major &#x200B;(USER_AGENT) | ua_os_version_major &#x200B; s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Estrae la versione del sistema operativo dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_os_version &#x200B;(USER_AGENT) | ua_os_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1. |
| ua_os_name_version | Estrae il nome e la versione del sistema operativo dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_os_name_version &#x200B;(USER_AGENT) | ua_os_name_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Estrae la versione dell&#39;agente dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_agent_version &#x200B;(USER_AGENT) | ua_agent_version &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1 |
| ua_agent_version_major | Estrae il nome dell&#39;agente e la versione principale dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_agent_version_major &#x200B;(USER_AGENT) | ua_agent_version_major &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Estrae il nome dell&#39;agente dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_agent_name &#x200B;(USER_AGENT) | ua_agent_name &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Estrae la classe dispositivo dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell&#39;agente utente.</li></ul> | ua_device_class &#x200B;(USER_AGENT) | ua_device_class &#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefono |

{style=&quot;table-layout:auto&quot;}

### Copia oggetto {#object-copy}

>[!TIP]
>
>La funzione di copia dell&#39;oggetto viene applicata automaticamente quando un oggetto nell&#39;origine viene mappato a un oggetto in XDM. Non sono necessarie ulteriori azioni da parte degli utenti.

È possibile utilizzare la funzione di copia dell’oggetto per copiare automaticamente gli attributi di un oggetto senza apportare modifiche alla mappatura. Ad esempio, se i dati di origine hanno una struttura di:

```json
address{
        line1: 4191 Ridgebrook Way,
        city: San Jose,
        state: California
        }
```

e una struttura XDM di:

```json
addr{
    addrLine1: 4191 Ridgebrook Way,
    city: San Jose,
    state: California
    }
```

Poi la mappatura diventa:

```json
address -> addr
address.line1 -> addr.addrLine1
```

Nell’esempio precedente, il `city` e `state` gli attributi vengono inoltre acquisiti automaticamente in fase di runtime perché il `address` oggetto mappato su `addr`. Se doveste creare un `line2` nella struttura XDM e i dati di input contengono anche un `line2` in `address` e viene acquisito automaticamente senza la necessità di modificare manualmente la mappatura.

Per garantire il funzionamento della mappatura automatica, è necessario soddisfare i seguenti prerequisiti:

* È necessario mappare gli oggetti a livello principale;
* È necessario creare nuovi attributi nello schema XDM;
* I nuovi attributi devono avere nomi corrispondenti nello schema di origine e nello schema XDM.

Se uno dei prerequisiti non è soddisfatto, è necessario mappare manualmente lo schema di origine allo schema XDM utilizzando la preparazione dati.