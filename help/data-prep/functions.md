---
keywords: Experience Platform;home;argomenti popolari;mappare csv;mappare file csv;mappare file csv a xdm;mappare csv a xdm;guida interfaccia utente;mapper;mappare;mappare campi;mappare funzioni;
solution: Experience Platform
title: Funzioni di mappatura della preparazione dati
description: Questo documento introduce le funzioni di mappatura utilizzate con la preparazione dati.
exl-id: e95d9329-9dac-4b54-b804-ab5744ea6289
source-git-commit: ff61ec7bc1e67191a46f7d9bb9af642e9d601c3a
workflow-type: tm+mt
source-wordcount: '5080'
ht-degree: 2%

---

# Funzioni di mappatura della preparazione dati

Le funzioni di preparazione dati possono essere utilizzate per calcolare i valori in base a ciò che viene immesso nei campi sorgente.

## Campi

Un nome di campo può essere un qualsiasi identificatore legale: una sequenza illimitata di lettere e cifre Unicode che inizia con una lettera, il simbolo del dollaro (`$`) o il carattere di sottolineatura (`_`). Anche i nomi delle variabili fanno distinzione tra maiuscole e minuscole.

Se un nome di campo non segue questa convenzione, il nome del campo deve essere racchiuso tra `${}`. Ad esempio, se il nome del campo è &quot;First Name&quot; o &quot;First.Name&quot;, il nome deve essere racchiuso come `${First Name}` o `${First\.Name}` rispettivamente.

>[!TIP]
>
>Quando si interagisce con le gerarchie, se un attributo figlio ha un punto (`.`), è necessario utilizzare una barra rovesciata (`\`) per eliminare i caratteri speciali. Per ulteriori informazioni, consulta la guida su [escape di caratteri speciali](home.md#escape-special-characters).

Inoltre, se il nome di un campo è **qualsiasi** tra le seguenti parole chiave riservate, deve essere racchiuso con `${}`:

```console
new, mod, or, break, var, lt, for, false, while, eq, gt, div, not, null, continue, else, and, ne, true, le, if, ge, return, _errors
```

È possibile accedere ai dati all’interno dei sottocampi utilizzando la notazione del punto. Ad esempio, se è stato `name` oggetto, per accedere al `firstName` campo, utilizza `name.firstName`.

## Elenco delle funzioni

Nelle tabelle seguenti sono elencate tutte le funzioni di mappatura supportate, incluse le espressioni di esempio e i relativi output risultanti.

### Funzioni stringa {#string}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| concat | Concatena le stringhe specificate. | <ul><li>STRING: le stringhe che verranno concatenate.</li></ul> | concat(STRING_1, STRING_2) | concat(&quot;Ciao, &quot;, &quot;ci&quot;, &quot;!&quot;) | `"Hi, there!"` |
| esplodere | Divide la stringa in base a un regex e restituisce un array di parti. Facoltativamente, può includere regex per dividere la stringa. Per impostazione predefinita, la suddivisione viene risolta in &quot;,&quot;. I delimitatori seguenti **bisogno** da evitare con `\`: `+, ?, ^, \|, ., [, (, {, ), *, $, \` Se si includono più caratteri come delimitatore, il delimitatore verrà considerato come un delimitatore con più caratteri. | <ul><li>STRINGA: **Obbligatorio** Stringa da dividere.</li><li>REGEX: *Facoltativo* Espressione regolare che può essere utilizzata per dividere la stringa.</li></ul> | esplodi(STRING, REGEX) | esplodi(&quot;Salve!&quot;, &quot;&quot;) | `["Hi,", "there"]` |
| instr | Restituisce la posizione o l&#39;indice di una sottostringa. | <ul><li>INPUT: **Obbligatorio** Stringa in cui viene eseguita la ricerca.</li><li>SOTTOSTRINGA: **Obbligatorio** Sottostringa da cercare all&#39;interno della stringa.</li><li>POSIZIONE_INIZIALE: *Facoltativo* La posizione da cui iniziare a cercare nella stringa.</li><li>OCCORRENZA: *Facoltativo* L’ennesima occorrenza da cercare dalla posizione iniziale. Per impostazione predefinita, è 1. </li></ul> | instr(INPUT, SUBSTRING, START_POSITION, OCCURRENCE) | instr(&quot;adobe.com&quot;, &quot;com&quot;) | 6 |
| sostituto | Sostituisce la stringa di ricerca se presente nella stringa originale. | <ul><li>INPUT: **Obbligatorio** Stringa di input.</li><li>TO_FIND: **Obbligatorio** Stringa da cercare all’interno dell’input.</li><li>DA_SOSTITUIRE: **Obbligatorio** Stringa che sostituirà il valore all’interno di &quot;TO_FIND&quot;.</li></ul> | replacestr(INPUT, TO_FIND, TO_REPLACE) | replacestr(&quot;This is a string re test&quot;, &quot;re&quot;, &quot;replace&quot;) | &quot;Questo è un test di sostituzione della stringa&quot; |
| substr | Restituisce una sottostringa di una determinata lunghezza. | <ul><li>INPUT: **Obbligatorio** Stringa di input.</li><li>START_INDEX: **Obbligatorio** Indice della stringa di input da cui inizia la sottostringa.</li><li>LUNGHEZZA: **Obbligatorio** Lunghezza della sottostringa.</li></ul> | substr(INPUT, START_INDEX, LENGTH) | substr(&quot;Questo è un test di sottostringa&quot;, 7, 8) | &quot;a subst&quot; |
| lower /<br>lcase | Converte una stringa in minuscolo. | <ul><li>INPUT: **Obbligatorio** Stringa che verrà convertita in minuscolo.</li></ul> | lower(INPUT) | lower(&quot;HeLo&quot;)<br>lcase(&quot;HeLo&quot;) | &quot;ciao&quot; |
| upper /<br>caso | Converte una stringa in maiuscolo. | <ul><li>INPUT: **Obbligatorio** Stringa che verrà convertita in maiuscolo.</li></ul> | upper(INPUT) | upper(&quot;HeLo&quot;)<br>ucase(&quot;HeLo&quot;) | &quot;CIAO&quot; |
| split | Divide una stringa di input in un separatore. Il seguente separatore **esigenze** da evitare con `\`: `\`. Se si includono più delimitatori, la stringa verrà suddivisa in base a **qualsiasi** dei delimitatori presenti nella stringa. **Nota:** Questa funzione restituisce solo indici non nulli dalla stringa, indipendentemente dalla presenza del separatore. Se tutti gli indici, compresi i valori Null, sono necessari nell&#39;array risultante, utilizzare la funzione &quot;explode&quot;. | <ul><li>INPUT: **Obbligatorio** Stringa di input che verrà divisa.</li><li>SEPARATORE: **Obbligatorio** Stringa utilizzata per dividere l&#39;input.</li></ul> | split(INPUT, SEPARATOR) | split(&quot;Hello world&quot;, &quot;&quot;) | `["Hello", "world"]` |
| unire | Unisce un elenco di oggetti utilizzando il separatore. | <ul><li>SEPARATORE: **Obbligatorio** Stringa che verrà utilizzata per unire gli oggetti.</li><li>OGGETTI: **Obbligatorio** Matrice di stringhe che verranno unite.</li></ul> | `join(SEPARATOR, [OBJECTS])` | `join(" ", to_array(true, "Hello", "world"))` | &quot;Hello world&quot; |
| lpad | Aggiunge il lato sinistro di una stringa alla stringa specificata. | <ul><li>INPUT: **Obbligatorio** La stringa che verrà imbottita. Questa stringa può essere null.</li><li>CONTEGGIO: **Obbligatorio** Dimensione della stringa da aggiungere.</li><li>SPAZIATURA: **Obbligatorio** Stringa con cui incollare l’input. Se null o vuoto, verrà considerato come un singolo spazio.</li></ul> | lpad(INPUT, COUNT, PADDING) | lpad(&quot;bat&quot;, 8, &quot;yz&quot;) | yzyzybat |
| rpad | Aggiunge il lato destro di una stringa alla stringa specificata. | <ul><li>INPUT: **Obbligatorio** La stringa che verrà imbottita. Questa stringa può essere null.</li><li>CONTEGGIO: **Obbligatorio** Dimensione della stringa da aggiungere.</li><li>SPAZIATURA: **Obbligatorio** Stringa con cui incollare l’input. Se null o vuoto, verrà considerato come un singolo spazio.</li></ul> | rpad(INPUT, COUNT, PADDING) | rpad(&quot;bat&quot;, 8, &quot;yz&quot;) | &quot;batyzyzy&quot; |
| left | Ottiene i primi &quot;n&quot; caratteri della stringa specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa per la quale si stanno ottenendo i primi &quot;n&quot; caratteri.</li><li>CONTEGGIO: **Obbligatorio** I caratteri &quot;n&quot; che si desidera ottenere dalla stringa.</li></ul> | left(STRING, COUNT) | left(&quot;abcde&quot;, 2) | &quot;ab&quot; |
| destra | Ottiene gli ultimi &quot;n&quot; caratteri della stringa specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa per la quale si stanno ottenendo gli ultimi &quot;n&quot; caratteri.</li><li>CONTEGGIO: **Obbligatorio** I caratteri &quot;n&quot; che si desidera ottenere dalla stringa.</li></ul> | right(STRING, COUNT) | right(&quot;abcde&quot;, 2) | &quot;de&quot; |
| ltrim | Rimuove lo spazio vuoto dall&#39;inizio della stringa. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui rimuovere lo spazio vuoto.</li></ul> | ltrim(STRING) | ltrim(&quot;ciao&quot;) | &quot;ciao&quot; |
| rtrim | Rimuove lo spazio vuoto dalla fine della stringa. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui rimuovere lo spazio vuoto.</li></ul> | rtrim(STRING) | rtrim(&quot;hello&quot;) | &quot;ciao&quot; |
| trim | Rimuove lo spazio vuoto dall&#39;inizio e dalla fine della stringa. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui rimuovere lo spazio vuoto.</li></ul> | trim(STRING) | trim(&quot; hello &quot;) | &quot;ciao&quot; |
| è uguale a | Confronta due stringhe per verificare se sono uguali. Questa funzione distingue tra maiuscole e minuscole. | <ul><li>STRINGA1: **Obbligatorio** La prima stringa che si desidera confrontare.</li><li>STRINGA2: **Obbligatorio** Seconda stringa da confrontare.</li></ul> | STRINGA1.&#x200B;equals(&#x200B;STRING2) | &quot;string1&quot;.&#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| equalsIgnoreCase | Confronta due stringhe per verificare se sono uguali. Questa funzione è **non** distinzione tra maiuscole e minuscole. | <ul><li>STRINGA1: **Obbligatorio** La prima stringa che si desidera confrontare.</li><li>STRINGA2: **Obbligatorio** Seconda stringa da confrontare.</li></ul> | STRINGA1.&#x200B;equalsIgnoreCase&#x200B;(STRING2) | &quot;string1&quot;.&#x200B;equalsIgnoreCase&#x200B;(&quot;STRING1) | true |

{style="table-layout:auto"}

### Funzioni espressione regolare

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| extract_regex | Estrae gruppi dalla stringa di input, in base a un&#39;espressione regolare. | <ul><li>STRINGA: **Obbligatorio** Stringa da cui si stanno estraendo i gruppi.</li><li>REGEX: **Obbligatorio** Espressione regolare che si desidera associare al gruppo.</li></ul> | extract_regex(STRING, REGEX) | extract_regex&#x200B;(&quot;E259,E259B_009,1_1&quot;&#x200B;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | [&quot;E259,E259B_009,1_1&quot;, &quot;E259&quot;, &quot;1_1&quot;] |
| matches_regex | Verifica se la stringa corrisponde all’espressione regolare immessa. | <ul><li>STRINGA: **Obbligatorio** La stringa da controllare corrisponde all&#39;espressione regolare.</li><li>REGEX: **Obbligatorio** L’espressione regolare con cui stai effettuando il confronto.</li></ul> | matches_regex(STRING, REGEX) | matches_regex(&quot;E259,E259B_009,1_1&quot;, &quot;([^,]+),[^,]*,([^,]+)&quot;) | true |

{style="table-layout:auto"}

### Funzioni di hashing {#hashing}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| sha1 | Accetta un input e genera un valore hash utilizzando l’algoritmo 1 di hash sicuro (SHA-1). | <ul><li>INPUT: **Obbligatorio** Testo normale con hash.</li><li>CHARSET: *Facoltativo* Nome del set di caratteri. I valori possibili includono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha1(INPUT, CHARSET) | sha1(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | c3599c11e47719df18a24&#x200B;48690840c5dfcce3c80 |
| sha256 | Accetta un input e produce un valore hash utilizzando Secure Hash Algorithm 256 (SHA-256). | <ul><li>INPUT: **Obbligatorio** Testo normale con hash.</li><li>CHARSET: *Facoltativo* Nome del set di caratteri. I valori possibili includono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha256(INPUT, CHARSET) | sha256(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | 7330d2b39ca35eaf4cb95fc846c21&#x200B;ee6a39af698154a83a586ee270a0d372104 |
| sha512 | Accetta un input e genera un valore hash utilizzando Secure Hash Algorithm 512 (SHA-512). | <ul><li>INPUT: **Obbligatorio** Testo normale con hash.</li><li>CHARSET: *Facoltativo* Nome del set di caratteri. I valori possibili includono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | sha512(INPUT, CHARSET) | sha512(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | a3d7e45a0d9be4e4b9a3b8c9c2163c21ef&#x200B;708bf11b4232bb21d2a8704ada2cdcd7b367dd0788a89&#x200B;a5c908cfe377aceb1072a7b38 6b7d4fd2ff68a8fd24d16 |
| md5 | Accetta un input e produce un valore hash utilizzando MD5. | <ul><li>INPUT: **Obbligatorio** Testo normale con hash.</li><li>CHARSET: *Facoltativo* Nome del set di caratteri. I valori possibili includono UTF-8, UTF-16, ISO-8859-1 e US-ASCII. </li></ul> | md5(INPUT, CHARSET) | md5(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | d3b96ce8c9fb4&#x200B;e9bd0198d03ba6852c7 |
| crc32 | Prende un input utilizza un algoritmo CRC (Cyclic Redundancy Check) per produrre un codice ciclico a 32 bit. | <ul><li>INPUT: **Obbligatorio** Testo normale con hash.</li><li>CHARSET: *Facoltativo* Nome del set di caratteri. I valori possibili includono UTF-8, UTF-16, ISO-8859-1 e US-ASCII.</li></ul> | crc32(INPUT, CHARSET) | crc32(&quot;il mio testo&quot;, &quot;UTF-8&quot;) | 8df92e80 |

{style="table-layout:auto"}

### Funzioni URL {#url}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| get_url_protocol | Restituisce il protocollo dall&#39;URL specificato. Se l’input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** URL da cui estrarre il protocollo.</li></ul> | get_url_protocol&#x200B;(URL) | get_url_protocol(&quot;https://platform&#x200B;.adobe.com/home&quot;) | https |
| get_url_host | Restituisce l’host dell’URL specificato. Se l’input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** L’URL da cui deve essere estratto l’host.</li></ul> | get_url_host&#x200B;(URL) | get_url_host&#x200B;(&quot;https://platform&#x200B;.adobe.com/home&quot;) | platform.adobe.com |
| get_url_port | Restituisce la porta dell’URL specificato. Se l’input non è valido, restituisce null. | <ul><li>URL: **Obbligatorio** URL da cui estrarre la porta.</li></ul> | get_url_port(URL) | get_url_port&#x200B;(&quot;sftp://example.com//home/&#x200B;joe/employee.csv&quot;) | 22 |
| get_url_path | Restituisce il percorso dell’URL specificato. Per impostazione predefinita, viene restituito il percorso completo. | <ul><li>URL: **Obbligatorio** URL da cui estrarre il percorso.</li><li>PERCORSO_COMPLETO: *Facoltativo* Valore booleano che determina se viene restituito il percorso completo. Se impostato su false, viene restituita solo la fine del percorso.</li></ul> | get_url_path&#x200B;(URL, FULL_PATH) | get_url_path&#x200B;(&quot;sftp://example.com//&#x200B;home/joe/employee.csv&quot;) | &quot;//home/joe/&#x200B;employee.csv&quot; |
| get_url_query_str | Restituisce la stringa di query di un URL specificato come mappa del nome della stringa di query e del valore della stringa di query. | <ul><li>URL: **Obbligatorio** L’URL da cui stai tentando di ottenere la stringa di query.</li><li>ANCORAGGIO: **Obbligatorio** Determina l&#39;operazione che verrà eseguita con l&#39;ancoraggio nella stringa query. Può essere uno dei tre valori seguenti: &quot;keep&quot;, &quot;remove&quot; o &quot;append&quot;.<br><br>Se il valore è &quot;keep&quot; (mantieni), l’ancoraggio verrà attaccato al valore restituito.<br>Se il valore è &quot;remove&quot;, l’ancoraggio verrà rimosso dal valore restituito.<br>Se il valore è &quot;append&quot;, l’ancoraggio verrà restituito come valore separato.</li></ul> | get_url_query_str&#x200B;(URL, ANCHOR) | get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there?name=&#x200B;ferret#nose&quot;, &quot;keep&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com:8042&#x200B;/over/there?name=&#x200B;ferret#nose&quot;, &quot;remove&quot;)<br>get_url_query_str&#x200B;(&quot;foo://example.com&#x200B;:8042/over/there&#x200B;?name=ferret#nose&quot;, &quot;append&quot;) | `{"name": "ferret#nose"}`<br>`{"name": "ferret"}`<br>`{"name": "ferret", "_anchor_": "nose"}` |
| get_url_encoded | Questa funzione accetta un URL come input e sostituisce o codifica i caratteri speciali con caratteri ASCII. Per ulteriori informazioni sui caratteri speciali, leggere [elenco dei caratteri speciali](#special-characters) nell&#39;appendice del presente documento. | <ul><li>URL: **Obbligatorio** L’URL di input con caratteri speciali che desideri sostituire o codificare con caratteri ASCII.</li></ul> | get_url_encoded(URL) | get_url_encoded(&quot;https</span>://example.com/partneralliance_asia-pacific_2022&quot;) | https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022 |
| get_url_decoded | Questa funzione accetta un URL come input e decodifica i caratteri ASCII in caratteri speciali.  Per ulteriori informazioni sui caratteri speciali, leggere [elenco dei caratteri speciali](#special-characters) nell&#39;appendice del presente documento. | <ul><li>URL: **Obbligatorio** L’URL di input con caratteri ASCII che desideri decodificare in caratteri speciali.</li></ul> | get_url_decoded(URL) | get_url_decoded(&quot;https%3A%2F%2Fexample.com%2Fpartneralliance_asia-pacific_2022&quot;) | https</span>://example.com/partneralliance_asia-pacific_2022 |

{style="table-layout:auto"}

### Funzioni data e ora {#date-and-time}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella. Ulteriori informazioni su `date` è disponibile nella sezione date della sezione [guida alla gestione del formato dei dati](./data-handling.md#dates).

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| now | Recupera l&#39;ora corrente. | | now() | now() | `2021-10-26T10:10:24Z` |
| timestamp | Recupera l’ora Unix corrente. | | timestamp() | timestamp() | 1571850624571 |
| formato | Formatta la data di input in base a un formato specificato. | <ul><li>DATA: **Obbligatorio** Data di input, come oggetto ZonedDateTime, che si desidera formattare.</li><li>FORMATO: **Obbligatorio** Il formato in cui desideri modificare la data.</li></ul> | format(DATE, FORMAT) | format(2019-10-23T11):24:00+00:00, &quot;yyyy-MM-dd HH:mm:ss&quot;) | `2019-10-23 11:24:35` |
| format | Converte una marca temporale in una stringa di data in base al formato specificato. | <ul><li>TIMESTAMP: **Obbligatorio** Il timestamp da formattare. Questo è scritto in millisecondi.</li><li>FORMATO: **Obbligatorio** Il formato che vuoi che la marca temporale diventi.</li></ul> | format(TIMESTAMP, FORMAT) | dformat(1571829875000, &quot;yyyy-MM-dd&#39;T&#39;HH:mm:ss.SSSX&quot;) | `2019-10-23T11:24:35.000Z` |
| data | Converte una stringa di data in un oggetto ZonedDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** Stringa che rappresenta la data.</li><li>FORMATO: **Obbligatorio** Stringa che rappresenta il formato della data di origine.**Nota:** Questo fa **non** rappresenta il formato in cui desideri convertire la stringa di data. </li><li>DATA_PREDEFINITA: **Obbligatorio** Se la data specificata è nulla, viene restituita la data predefinita.</li></ul> | date(DATE, FORMAT, DEFAULT_DATE) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;, now()) | `2019-10-23T11:24:00Z` |
| data | Converte una stringa di data in un oggetto ZonedDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** Stringa che rappresenta la data.</li><li>FORMATO: **Obbligatorio** Stringa che rappresenta il formato della data di origine.**Nota:** Questo fa **non** rappresenta il formato in cui desideri convertire la stringa di data. </li></ul> | date(DATE, FORMAT) | date(&quot;2019-10-23 11:24&quot;, &quot;yyyy-MM-dd HH:mm&quot;) | `2019-10-23T11:24:00Z` |
| data | Converte una stringa di data in un oggetto ZonedDateTime (formato ISO 8601). | <ul><li>DATA: **Obbligatorio** Stringa che rappresenta la data.</li></ul> | date(DATE) | date(&quot;2019-10-23 11:24&quot;) | &quot;2019-10-23T11:24:00Z&quot; |
| date_part | Recupera le parti della data. Sono supportati i seguenti valori dei componenti: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;aa&quot;<br><br>&quot;quarter&quot;<br>&quot;qq&quot;<br>&quot;q&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>m&quot;<br><br>&quot;dayofyear&quot;<br>&quot;giorno&quot;<br>&quot;y&quot;<br><br>&quot;giorno&quot;<br>&quot;gg&quot;<br>&quot;d&quot;<br><br>&quot;week&quot;<br>&quot;ww&quot;<br>&quot;w&quot;<br><br>&quot;giorno feriale&quot;<br>&quot;dw&quot;<br>&quot;w&quot;<br><br>&quot;ora&quot;<br>&quot;hh&quot;<br>&quot;hh24&quot;<br>&quot;hh12&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot;<br><br>&quot;millisecondi&quot;<br>&quot;SSS&quot; | <ul><li>COMPONENTE: **Obbligatorio** Stringa che rappresenta la parte della data. </li><li>DATA: **Obbligatorio** La data, in un formato standard.</li></ul> | date_part&#x200B;(COMPONENT, DATE) | date_part(&quot;MM&quot;, date(&quot;2019-10-17 11:55:12&quot;) | 10 |
| set_date_part | Sostituisce un componente in una determinata data. Sono accettati i seguenti componenti: <br><br>&quot;year&quot;<br>&quot;yyyy&quot;<br>&quot;aa&quot;<br><br>&quot;month&quot;<br>&quot;mm&quot;<br>m&quot;<br><br>&quot;giorno&quot;<br>&quot;gg&quot;<br>&quot;d&quot;<br><br>&quot;ora&quot;<br>&quot;hh&quot;<br><br>&quot;minute&quot;<br>&quot;mi&quot;<br>&quot;n&quot;<br><br>&quot;second&quot;<br>&quot;ss&quot;<br>&quot;s&quot; | <ul><li>COMPONENTE: **Obbligatorio** Stringa che rappresenta la parte della data. </li><li>VALORE: **Obbligatorio** Il valore da impostare per il componente per una data specificata.</li><li>DATA: **Obbligatorio** La data, in un formato standard.</li></ul> | set_date_part&#x200B;(COMPONENT, VALUE, DATE) | set_date_part(&quot;m&quot;, 4, date(&quot;2016-11-09T11:44:44,797&quot;) | &quot;09/04/2016:44:44Z&quot; |
| make_date_time | Crea una data da parti. Questa funzione può essere indotta anche utilizzando make_timestamp. | <ul><li>ANNO: **Obbligatorio** L&#39;anno, composto da quattro cifre.</li><li>MESE: **Obbligatorio** Il mese. I valori consentiti sono compresi tra 1 e 12.</li><li>GIORNO: **Obbligatorio** Il giorno. I valori consentiti sono compresi tra 1 e 31.</li><li>ORA: **Obbligatorio** Ora. I valori consentiti sono compresi tra 0 e 23.</li><li>MINUTO: **Obbligatorio** Il minuto. I valori consentiti sono compresi tra 0 e 59.</li><li>NANOSECONDI: **Obbligatorio** I valori dei nanosecondi. I valori consentiti sono compresi tra 0 e 999999999.</li><li>FUSO ORARIO: **Obbligatorio** Il fuso orario per la data e l’ora.</li></ul> | make_date_time&#x200B;(YEAR, MONTH, DAY, HOUR, MINUTE, SECOND, NANOSECOND, TIMEZONE) | make_date_time&#x200B;(2019, 10, 17, 11, 55, 12, 999, &quot;America/Los_Angeles&quot;) | `2019-10-17T11:55:12Z` |
| zone_date_to_utc | Converte una data in qualsiasi fuso orario in una data in UTC. | <ul><li>DATA: **Obbligatorio** La data che stai tentando di convertire.</li></ul> | zone_date_to_utc&#x200B;(DATE) | `zone_date_to_utc&#x200B;(2019-10-17T11:55:&#x200B;12 PST` | `2019-10-17T19:55:12Z` |
| zone_date_to_zone | Converte una data da un fuso orario a un altro. | <ul><li>DATA: **Obbligatorio** La data che stai tentando di convertire.</li><li>ZONA: **Obbligatorio** Fuso orario in cui si sta tentando di convertire la data.</li></ul> | zone_date_to_zone&#x200B;(DATE, ZONE) | `zone_date_to_utc&#x200B;(now(), "Europe/Paris")` | `2021-10-26T15:43:59Z` |

{style="table-layout:auto"}

### Gerarchie - Oggetti {#objects}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| is_empty | Controlla se un oggetto è vuoto. | <ul><li>INPUT: **Obbligatorio** L&#39;oggetto che si sta tentando di controllare è vuoto.</li></ul> | is_empty(INPUT) | `is_empty([1, null, 2, 3])` | false |
| array_a_oggetto | Crea un elenco di oggetti. | <ul><li>INPUT: **Obbligatorio** Un raggruppamento di coppie chiave-array.</li></ul> | arrays_to_object(INPUT) | `arrays_to_objects('sku', explode("id1\|id2", '\\\|'), 'price', [22.5,14.35])` | ```[{ "sku": "id1", "price": 22.5 }, { "sku": "id2", "price": 14.35 }]``` |
| to_object | Crea un oggetto in base alle coppie chiave/valore fornite. | <ul><li>INPUT: **Obbligatorio** Un elenco semplice di coppie chiave/valore.</li></ul> | to_object(INPUT) | to_object&#x200B;(&quot;firstName&quot;, &quot;John&quot;, &quot;lastName&quot;, &quot;Doe&quot;) | `{"firstName": "John", "lastName": "Doe"}` |
| str_to_object | Crea un oggetto dalla stringa di input. | <ul><li>STRINGA: **Obbligatorio** Stringa analizzata per creare un oggetto.</li><li>DELIMITATORE_VALORE: *Facoltativo* Delimitatore che separa un campo dal valore. Il delimitatore predefinito è `:`.</li><li>DELIMITATORE_CAMPO: *Facoltativo* Il delimitatore che separa le coppie di valori di campo. Il delimitatore predefinito è `,`.</li></ul> | str_to_object&#x200B;(STRING, VALUE_DELIMITER, FIELD_DELIMITER) **Nota**: puoi utilizzare la `get()` funzione insieme a `str_to_object()` per recuperare i valori per le chiavi nella stringa. | <ul><li>Esempio #1: str_to_object(&quot;firstName - John ; lastName - ; - 123 345 7890&quot;, &quot;-&quot;, &quot;;&quot;)</li><li>Esempio #2: str_to_object(&quot;firstName - John ; lastName - ; phone - 123 456 7890&quot;, &quot;-&quot;, &quot;;&quot;).get(&quot;firstName&quot;)</li></ul> | <ul><li>Esempio #1:`{"firstName": "John", "lastName": "Doe", "phone": "123 456 7890"}`</li><li>Esempio #2: &quot;John&quot;</li></ul> |
| contains_key | Controlla se l&#39;oggetto esiste nei dati di origine. **Nota:** Questa funzione sostituisce la obsoleta `is_set()` funzione. | <ul><li>INPUT: **Obbligatorio** Percorso da controllare se esiste nei dati di origine.</li></ul> | contains_key(INPUT) | contains_key(&quot;evars.evar.field1&quot;) | true |
| annullare | Imposta il valore dell&#39;attributo su `null`. Da utilizzare quando non si desidera copiare il campo nello schema di destinazione. | | nullify() | nullify() | `null` |
| get_keys | Analizza le coppie chiave/valore e restituisce tutte le chiavi. | <ul><li>OGGETTO: **Obbligatorio** Oggetto da cui verranno estratte le chiavi.</li></ul> | get_keys(OBJECT) | get_keys({&quot;book1&quot;: &quot;Pride and Prejudice&quot;, &quot;book2&quot;: &quot;1984&quot;}) | `["book1", "book2"]` |
| get_values | Analizza le coppie chiave/valore e restituisce il valore della stringa, in base alla chiave specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa da analizzare.</li><li>CHIAVE: **Obbligatorio** Chiave per la quale estrarre il valore.</li><li>DELIMITATORE_VALORE: **Obbligatorio** Il delimitatore che separa il campo e il valore. Se uno dei due `null` o viene fornita una stringa vuota, questo valore è `:`.</li><li>DELIMITATORE_CAMPO: *Facoltativo* Il delimitatore che separa le coppie di campi e valori. Se uno dei due `null` o viene fornita una stringa vuota, questo valore è `,`.</li></ul> | get_values(STRING, KEY, VALUE_DELIMITER, FIELD_DELIMITER) | get_values(\&quot;firstName - John , lastName - Cena , phone - 555 420 8692\&quot;, \&quot;firstName\&quot;, \&quot;-\&quot;, \&quot;,\&quot;) | John |
| map_get_values | Prende una mappa e un input chiave. Se l’input è un singolo tasto, la funzione restituisce il valore associato a tale tasto. Se l’input è una matrice di stringhe, la funzione restituisce tutti i valori corrispondenti alle chiavi fornite. Se la mappa in ingresso contiene chiavi duplicate, il valore restituito deve deduplicare le chiavi e restituire valori univoci. | <ul><li>MAPPA: **Obbligatorio** I dati della mappa di input.</li><li>CHIAVE:  **Obbligatorio** La chiave può essere una singola stringa o una matrice di stringhe. Se viene fornito un altro tipo primitivo (dati/numero), viene trattato come una stringa.</li></ul> | get_values(MAP, KEY) | Consulta la sezione [appendice](#map_get_values) per un esempio di codice. | |
| map_has_keys | Se vengono forniti uno o più tasti di input, la funzione restituisce true. Se come input viene fornita una matrice di stringhe, la funzione restituisce true sulla prima chiave trovata. | <ul><li>MAPPA:  **Obbligatorio** Dati della mappa di input</li><li>CHIAVE:  **Obbligatorio** La chiave può essere una singola stringa o una matrice di stringhe. Se viene fornito un altro tipo primitivo (dati/numero), viene trattato come una stringa.</li></ul> | map_has_keys(MAP, KEY) | Consulta la sezione [appendice](#map_has_keys) per un esempio di codice. | |
| add_to_map | Accetta almeno due input. È possibile fornire come input qualsiasi numero di mappe. La preparazione dati restituisce una singola mappa contenente tutte le coppie chiave-valore provenienti da tutti gli input. Se una o più chiavi sono ripetute (nella stessa mappa o su più mappe), la preparazione dati deduplica le chiavi in modo che la prima coppia chiave-valore persista nell’ordine in cui sono state passate nell’input. | MAPPA: **Obbligatorio** I dati della mappa di input. | add_to_map(MAP 1, MAP 2, MAP 3, ...) | Consulta la sezione [appendice](#add_to_map) per un esempio di codice. | |

{style="table-layout:auto"}

Per informazioni sulla funzione di copia dell&#39;oggetto, vedere la sezione [sotto](#object-copy).

### Gerarchie - Array {#arrays}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| coalesce | Restituisce il primo oggetto non nullo in una matrice specificata. | <ul><li>INPUT: **Obbligatorio** Matrice di cui trovare il primo oggetto non Null.</li></ul> | coalesce(INPUT) | coalesce(null, null, null, &quot;first&quot;, null, &quot;second&quot;) | &quot;first&quot; |
| primo | Recupera il primo elemento dell’array specificato. | <ul><li>INPUT: **Obbligatorio** L’array di cui desideri trovare il primo elemento.</li></ul> | first(INPUT) | first(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | &quot;1&quot; |
| ultimo | Recupera l’ultimo elemento dell’array specificato. | <ul><li>INPUT: **Obbligatorio** L’array di cui desideri trovare l’ultimo elemento.</li></ul> | last(INPUT) | last(&quot;1&quot;, &quot;2&quot;, &quot;3&quot;) | 3&quot; |
| add_to_array | Aggiunge elementi alla fine dell&#39;array. | <ul><li>ARRAY: **Obbligatorio** Matrice a cui si stanno aggiungendo elementi.</li><li>VALORI: gli elementi che desideri aggiungere alla matrice.</li></ul> | add_to_array&#x200B;(ARRAY, VALUES) | add_to_array&#x200B;([&#39;a&#39;, &#39;b&#39;], &#39;c&#39;, &#39;d&#39;) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;] |
| join_array | Combina gli array tra loro. | <ul><li>ARRAY: **Obbligatorio** Matrice a cui si stanno aggiungendo elementi.</li><li>VALORI: gli array che si desidera aggiungere all’array principale.</li></ul> | join_arrays&#x200B;(ARRAY, VALUES) | join_arrays&#x200B;([&#39;a&#39;, &#39;b&#39;], [&#39;c&#39;], [d&#39;, e&#39;]) | [&#39;a&#39;, &#39;b&#39;, &#39;c&#39;, &#39;d&#39;, &#39;e&#39;] |
| to_array | Prende un elenco di input e lo converte in un array. | <ul><li>INCLUDE_NULLS: **Obbligatorio** Valore booleano per indicare se includere o meno valori Null nella matrice di risposta.</li><li>VALORI: **Obbligatorio** Elementi da convertire in un array.</li></ul> | to_array&#x200B;(INCLUDE_NULLS, VALUES) | to_array(false, 1, null, 2, 3) | `[1, 2, 3]` |
| size_of | Restituisce la dimensione dell&#39;input. | <ul><li>INPUT: **Obbligatorio** Oggetto di cui stai cercando le dimensioni.</li></ul> | size_of(INPUT) | `size_of([1, 2, 3, 4])` | 4 |
| upsert_array_append | Questa funzione viene utilizzata per aggiungere tutti gli elementi dell’intero array di input alla fine dell’array in Profilo. Questa funzione è **solo** applicabile durante gli aggiornamenti. Se utilizzata nel contesto degli inserti, questa funzione restituisce l’input così com’è. | <ul><li>ARRAY: **Obbligatorio** Array a cui aggiungere l’array nel profilo.</li></ul> | upsert_array_append(ARRAY) | `upsert_array_append([123, 456])` | [124, 456] |
| upsert_array_replace | Questa funzione viene utilizzata per sostituire gli elementi in un array. Questa funzione è **solo** applicabile durante gli aggiornamenti. Se utilizzata nel contesto degli inserti, questa funzione restituisce l’input così com’è. | <ul><li>ARRAY: **Obbligatorio** Array che sostituisce l’array nel profilo.</li></li> | upsert_array_replace(ARRAY) | `upsert_array_replace([123, 456], 1)` | [124, 456] |

{style="table-layout:auto"}

### Operatori logici {#logical-operators}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| decodificare | Dato un tasto e un elenco di coppie di valori chiave appiattite come array, la funzione restituisce il valore se viene trovata una chiave oppure restituisce un valore predefinito se presente nell’array. | <ul><li>CHIAVE: **Obbligatorio** Chiave da associare.</li><li>OPTIONS: **Obbligatorio** Array piatto di coppie chiave/valore. Facoltativamente, è possibile inserire un valore predefinito alla fine.</li></ul> | decode(KEY, OPTIONS) | decode(stateCode, &quot;ca&quot;, &quot;California&quot;, &quot;pa&quot;, &quot;Pennsylvania&quot;, &quot;N/A&quot;) | Se il codice stato dato è &quot;ca&quot;, &quot;California&quot;.<br>Se il codice dello stato dato è &quot;pa&quot;, &quot;Pennsylvania&quot;.<br>Se stateCode non corrisponde a quanto segue, &quot;N/D&quot;. |
| iif | Valuta una determinata espressione booleana e restituisce il valore specificato in base al risultato. | <ul><li>ESPRESSIONE: **Obbligatorio** Espressione booleana in fase di valutazione.</li><li>TRUE_VALUE: **Obbligatorio** Il valore che viene restituito se l’espressione restituisce true.</li><li>FALSE_VALUE: **Obbligatorio** Il valore che viene restituito se l’espressione restituisce false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Vero&quot; |

{style="table-layout:auto"}

### Aggregazione {#aggregation}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| min | Restituisce il minimo degli argomenti specificati. Utilizza l’ordinamento naturale. | <ul><li>OPTIONS: **Obbligatorio** Uno o più oggetti che possono essere confrontati.</li></ul> | min(OPTIONS) | min(3, 1, 4) | 1 |
| max | Restituisce il massimo degli argomenti specificati. Utilizza l’ordinamento naturale. | <ul><li>OPTIONS: **Obbligatorio** Uno o più oggetti che possono essere confrontati.</li></ul> | max(OPTIONS) | max(3, 1, 4) | 4 |

{style="table-layout:auto"}

### Conversioni tipo {#type-conversions}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| to_bigint | Converte una stringa in un BigInteger. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in un BigInteger.</li></ul> | to_bigint(STRING) | to_bigint&#x200B;(&quot;1000000.34&quot;) | 1000000,34 |
| to_decimal | Converte una stringa in un valore Double. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in Double.</li></ul> | to_decimal(STRING) | to_decimal(&quot;20.5&quot;) | 20,5 |
| to_float | Converte una stringa in un elemento mobile. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in Mobile.</li></ul> | to_float(STRING) | to_float(&quot;12.3456&quot;) | 12,34566 |
| to_integer | Converte una stringa in un numero intero. | <ul><li>STRINGA: **Obbligatorio** Stringa da convertire in un numero intero.</li></ul> | to_integer(STRING) | to_integer(&quot;12&quot;) | 12 |

{style="table-layout:auto"}

### Funzioni JSON {#json}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| json_to_object | Deserializza il contenuto JSON dalla stringa specificata. | <ul><li>STRINGA: **Obbligatorio** Stringa JSON da deserializzare.</li></ul> | json_to_object&#x200B;(STRING) | json_to_object&#x200B;({&quot;info&quot;:{&quot;firstName&quot;:&quot;John&quot;,&quot;lastName&quot;: &quot;Doe&quot;}}) | Oggetto che rappresenta il JSON. |

{style="table-layout:auto"}

### Operazioni speciali {#special-operations}

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| uuid /<br>GUID | Genera un ID pseudo-casuale. | | uuid()<br>guid() | uuid()<br>guid() | 7c0267d2-bb74-4e1a-9275-3bf4fccda5f4<br>c7016dc7-3163-43f7-afc7-2e1c9c206333 |
| `fpid_to_ecid ` | Questa funzione prende una stringa FPID e la converte in un ECID da utilizzare nelle applicazioni Adobe Experience Platform e Adobe Experience Cloud. | <ul><li>STRINGA: **Obbligatorio** Stringa FPID da convertire in ECID.</li></ul> | `fpid_to_ecid(STRING)` | `fpid_to_ecid("4ed70bee-b654-420a-a3fd-b58b6b65e991")` | `"28880788470263023831040523038280731744"` |

{style="table-layout:auto"}

### Funzioni dell’agente utente {#user-agent}

Una qualsiasi delle funzioni dell’agente utente contenute nella tabella seguente può restituire uno dei seguenti valori:

* Telefono - Un dispositivo mobile con uno schermo piccolo (comunemente &lt; 7&quot;)
* Mobile: dispositivo mobile non ancora identificato. Questo dispositivo mobile può essere un eReader, un tablet, un telefono, un orologio, ecc.

Per ulteriori informazioni sui valori dei campi dispositivo, leggi [elenco dei valori dei campi dispositivo](#device-field-values) nell&#39;appendice del presente documento.

>[!NOTE]
>
>Scorri verso sinistra o destra per visualizzare l’intero contenuto della tabella.

| Funzione | Descrizione | Parametri | Sintassi | Espressione | Output di esempio |
| -------- | ----------- | ---------- | -------| ---------- | ------------- |
| ua_os_name | Estrae il nome del sistema operativo dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_os_name&#x200B;(USER_AGENT) | ua_os_name&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS |
| ua_os_version_major | Estrae la versione principale del sistema operativo dalla stringa dell’agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_os_version_major&#x200B;(USER_AGENT) | ua_os_version_major&#x200B;s(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5 |
| ua_os_version | Estrae la versione del sistema operativo dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_os_version&#x200B;(USER_AGENT) | ua_os_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Versione/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5.1.1. |
| ua_os_name_version | Estrae il nome e la versione del sistema operativo dalla stringa agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_os_name_version&#x200B;(USER_AGENT) | ua_os_name_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | iOS 5.1.1 |
| ua_agent_version | Estrae la versione dell’agente dalla stringa dell’agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_agent_version&#x200B;(USER_AGENT) | ua_agent_version&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | 5,1 |
| ua_agent_version_major | Estrae il nome e la versione principale dell’agente dalla stringa dell’agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_agent_version_major&#x200B;(USER_AGENT) | ua_agent_version_major&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 come Mac OS X) AppleWebKit/534.46 (KHTML, come Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari 5 |
| ua_agent_name | Estrae il nome dell&#39;agente dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_agent_name&#x200B;(USER_AGENT) | ua_agent_name&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Safari |
| ua_device_class | Estrae la classe device dalla stringa dell&#39;agente utente. | <ul><li>USER_AGENT: **Obbligatorio** Stringa dell’agente utente.</li></ul> | ua_device_class&#x200B;(USER_AGENT) | ua_device_class&#x200B;(&quot;Mozilla/5.0 (iPhone; CPU iPhone OS 5_1_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B206 Safari/7534.48.3&quot;) | Telefono |

{style="table-layout:auto"}

### Copia oggetto {#object-copy}

>[!TIP]
>
>La funzione di copia degli oggetti viene applicata automaticamente quando un oggetto nell’origine viene mappato a un oggetto in XDM. Non è necessaria alcuna azione aggiuntiva da parte degli utenti.

È possibile utilizzare la funzione copia oggetto per copiare automaticamente gli attributi di un oggetto senza apportare modifiche alla mappatura. Ad esempio, se i dati di origine hanno una struttura di:

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

Quindi la mappatura diventa:

```json
address -> addr
address.line1 -> addr.addrLine1
```

Nell’esempio precedente, il `city` e `state` gli attributi vengono acquisiti automaticamente anche in fase di runtime perché `address` oggetto mappato a `addr`. Se dovessi creare un’ `line2` nella struttura XDM e i dati di input contengono anche un `line2` nel `address` , verranno acquisiti automaticamente anche senza la necessità di modificare manualmente la mappatura.

Per garantire il funzionamento della mappatura automatica, è necessario soddisfare i seguenti prerequisiti:

* Gli oggetti a livello principale devono essere mappati;
* I nuovi attributi devono essere stati creati nello schema XDM;
* I nuovi attributi devono avere nomi corrispondenti nello schema di origine e nello schema XDM.

Se uno dei prerequisiti non è soddisfatto, devi mappare manualmente lo schema di origine allo schema XDM utilizzando la preparazione dati.

## Appendice

Di seguito sono riportate ulteriori informazioni sull’utilizzo delle funzioni di mappatura della preparazione dati

### Caratteri speciali {#special-characters}

La tabella seguente delinea un elenco di caratteri riservati e dei corrispondenti caratteri codificati.

| Carattere riservato | Carattere codificato |
| --- | --- |
| spazio | %20 |
| ! | %21 |
| &quot; | %22 |
| # | %23 |
| $ | %24 |
| % | %25 |
| E | %26 |
| &#39; | %27 |
| ( | %28 |
| ). | %29 |
| * | %2A |
| + | %2B |
| , | %2C |
| / | %2F |
| : | %3A |
| ; | %3B |
| &lt; | %3C |
| = | %3D |
| > | %3E |
| ? | %3F |
| @ | %40 |
| [ | %5B |
| | | %5C |
| ] | %5D |
| ^ | %5E |
| ` | %60 |
| ~ | %7E |

{style="table-layout:auto"}

### Valori dei campi dispositivo {#device-field-values}

La tabella seguente illustra un elenco di valori dei campi dispositivo e le relative descrizioni.

| Dispositivo | Descrizione |
| --- | --- |
| Desktop | Dispositivo di tipo Desktop o Laptop. |
| Anonima | Un dispositivo anonimo. In alcuni casi, si tratta di `useragents` che sono stati modificati da un software di anonimizzazione. |
| Sconosciuto | Dispositivo sconosciuto. Questi sono di solito `useragents` che non contengono informazioni sul dispositivo. |
| Dispositivi mobili | Un dispositivo mobile non ancora identificato. Questo dispositivo mobile può essere un eReader, un tablet, un telefono, un orologio, ecc. |
| Tablet | Un dispositivo mobile con uno schermo grande (di solito > 7&quot;). |
| Telefono | Un dispositivo mobile con uno schermo piccolo (di solito &lt; 7&quot;). |
| Osserva | Un dispositivo mobile con uno schermo piccolo (di solito &lt; 2&quot;). Questi dispositivi normalmente funzionano come uno schermo aggiuntivo per un tipo di telefono/tablet di dispositivo. |
| Realtà aumentata | Un dispositivo mobile con funzionalità AR. |
| Realtà virtuale | Un dispositivo mobile con funzionalità VR. |
| eReader | Un dispositivo simile a una compressa, ma solitamente con [!DNL eInk] schermo. |
| Set-top box | Un dispositivo collegato che consente l&#39;interazione attraverso uno schermo di dimensioni televisive. |
| TV | Dispositivo simile al set-top box, ma incorporato nel televisore. |
| Apparecchiatura domestica | Un elettrodomestico (di solito grande), come un frigorifero. |
| Console giochi | Un sistema di gioco fisso come un [!DNL Playstation] o un [!DNL XBox]. |
| Console di gioco palmare | Un sistema di gioco mobile come un [!DNL Nintendo Switch]. |
| Voce | Un dispositivo basato sulla voce come [!DNL Amazon Alexa] o un [!DNL Google Home]. |
| Auto | Un browser basato su veicolo. |
| Robot | Robot che visitano un sito web. |
| Robot mobile | Robot che visitano un sito web ma indicano che desiderano essere visti come visitatori di Mobile. |
| Imitatore robot | Robot che visitano un sito web, fingono di essere robot come [!DNL Google], ma non lo sono. **Nota**: nella maggior parte dei casi, gli imitatori robot sono in effetti robot. |
| Cloud | Applicazione basata su cloud. Non si tratta né di robot né di hacker, ma di applicazioni che devono connettersi. Ciò include [!DNL Mastodon] server. |
| Hacker | Questo valore di dispositivo viene utilizzato nel caso in cui venga rilevato uno script in `useragent` stringa. |

{style="table-layout:auto"}

### Esempi di codice {#code-samples}

#### map_get_values {#map-get-values}

+++Seleziona per visualizzare l’esempio

```json
 example = "map_get_values(book_details,\"author\") where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "{\"author\": \"George R. R. Martin\"}"
```

+++

#### map_has_keys {#map_has_keys}

+++Seleziona per visualizzare l’esempio

```json
 example = "map_has_keys(book_details,\"author\")where input is : {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}",
      result = "true"
```

+++

#### add_to_map {#add_to_map}

+++Seleziona per visualizzare l’esempio

```json
example = "add_to_map(book_details, book_details2) where input is {\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "    }\n" +
        "}" +
        "{\n" +
        "    \"book_details2\":\n" +
        "    {\n" +
        "        \"author\": \"Neil Gaiman\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-0-380-97365-0\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      result = "{\n" +
        "    \"book_details\":\n" +
        "    {\n" +
        "        \"author\": \"George R. R. Martin\",\n" +
        "        \"price\": 17.99,\n" +
        "        \"ISBN\": \"ISBN-978-0553801477\"\n" +
        "        \"publisher\": \"William Morrow\"\n" +
        "    }\n" +
        "}",
      returns = "A new map with all elements from map and addends"
```

+++