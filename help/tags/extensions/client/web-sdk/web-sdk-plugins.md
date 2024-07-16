---
title: Panoramica dell’estensione Common Web SDK Plugins
description: Scopri l’estensione tag Common Web SDK Plugins in Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '2064'
ht-degree: 0%

---

# Panoramica dell’estensione Common Web SDK Plugins

>[!IMPORTANT]
>
>L&#39;estensione deve essere utilizzata con l&#39;estensione Adobe Experience Platform Web SDK. Per informazioni sulla versione da utilizzare con AppMeasurement, consulta la panoramica sull&#39;[estensione Common Analytics Plugins](../plugins/overview.md).

In questo documento viene illustrato come configurare l&#39;estensione tag Plugin di Web SDK e utilizzarla per potenziare l&#39;estensione [Adobe Experience Platform Web SDK](../web-sdk/overview.md).

## Configurare l’estensione Common Web SDK Plugins

Questa sezione fornisce un riferimento per le opzioni disponibili durante la configurazione dell’estensione dei plug-in dell’SDK per web.

>[!IMPORTANT]
>
>L’estensione Common Web SDK Plugins ha lo scopo di potenziare l’estensione Adobe Experience Platform Web SDK, tuttavia non è necessario installarla affinché l’estensione funzioni come previsto.

## Aggiunta di plug-in all’estensione Adobe Experience Platform Web SDK

Non è necessaria alcuna configurazione per inizializzare o aggiungere un plug-in alla libreria al di fuori di utilizzando i seguenti elementi di dati nativi forniti dall’estensione Common Web SDK Plugins:

* [&quot;getAndPersistValue&quot;](#getAndPersistValue)
* [&quot;getGeoCoordinates&quot;](#getGeoCoordinates)
* [&quot;getNewRepeat&quot;](#getNewRepeat)
* [&quot;getPagename&quot;](#getPagename)
* [&quot;getPreviousValue&quot;](#getPreviousValue)
* [&#39;getQueryParam&#39;](#getQueryParam)
* [&quot;getTimeParting&quot;](#getTimeParting)
* [&quot;getTimeSinceLastVisit&quot;](#getTimeSInceLastVisit)
* [&quot;getValOnce&quot;](#getValOnce)
* [&quot;getVisitDuration&quot;](#getVisitDuration)
* [&quot;getVisitNum&quot;](#getVisitNum)
* [&#39;pFo&#39;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare nei cookie i valori generati dall’utente. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare il plug-in di Analytics [`getAndPersistValue`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). L&#39;elemento dati `getAndPersistValue` memorizza un valore in un cookie che può essere recuperato successivamente durante una visita.

L&#39;elemento dati `getAndPersistValue` fornisce i seguenti argomenti:

* `vtp` (obbligatorio): valore da mantenere da pagina a pagina
* `cn` (facoltativo): nome del cookie in cui memorizzare il valore. Se questo argomento non è impostato, il cookie è denominato `"s_gapv"`
* `ex` (facoltativo): numero di giorni prima della scadenza del cookie. Se questo argomento è `0` o non è impostato, il cookie scade alla fine della visita (30 minuti di inattività).

Se la variabile nell&#39;argomento `vtp` è impostata, l&#39;elemento dati imposta il cookie e restituisce il valore del cookie. Se la variabile nell&#39;argomento `vtp` non è impostata, l&#39;elemento dati restituisce solo il valore del cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Questo plug-in richiede l’accesso alla posizione sul client, ma non genera un’eccezione se non la ottiene.

Consente di configurare il plug-in di Analytics [`getGeoCoordinates`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). L&#39;elemento dati `getGeoCoordinates` acquisisce la latitudine e la longitudine dei dispositivi dei visitatori.

L&#39;elemento dati `getGeoCoordinates` non utilizza argomenti. Restituisce uno dei seguenti valori:

* `"geo coordinates not available"`: per dispositivi per i quali non sono disponibili dati di geolocalizzazione al momento dell&#39;esecuzione del plug-in. Questo valore è comune al primo hit della visita, soprattutto quando i visitatori devono fornire il consenso per il tracciamento della loro posizione.
* `"error retrieving geo coordinates"`: quando il plug-in rileva errori durante il tentativo di recupero del percorso del dispositivo
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: dove [LATITUDINE]/[LONGITUDINE] sono rispettivamente latitudine e longitudine

### `getNewRepeat`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare il plug-in di Analytics [`getNewRepeat`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). L&#39;elemento dati `getNewRepeat` determina se un visitatore del sito è un nuovo visitatore o un visitatore ripetuto entro un numero desiderato di giorni.

L&#39;elemento dati `getNewRepeat` utilizza gli argomenti seguenti:

* `d` (numero intero, facoltativo): il numero minimo di giorni necessari tra le visite che reimposta i visitatori su `"New"`. Se questo argomento non è impostato, il valore predefinito è 30 giorni.

Questo elemento dati restituisce il valore di `"New"` se il cookie impostato dall&#39;elemento dati non esiste o è scaduto. Restituisce il valore di `"Repeat"` se il cookie impostato dall&#39;elemento dati esiste e il tempo trascorso dall&#39;hit corrente e dal cookie è superiore a 30 minuti. Questo metodo restituisce lo stesso valore per un’intera visita.

### `getPageName`

Consente di configurare il plug-in di Analytics [`getPageName`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). L&#39;elemento dati `getPageName` crea una versione dell&#39;URL corrente in formato semplice e intuitivo.

L&#39;elemento dati `getPageName` utilizza gli argomenti seguenti:

* `si` (facoltativo, stringa): ID inserito all&#39;inizio della stringa che rappresenta l&#39;ID del sito. Questo valore può essere un ID numerico o un nome descrittivo. Se non viene impostato, per impostazione predefinita viene utilizzato il dominio corrente.
* `qv` (facoltativo, stringa): elenco delimitato da virgole di parametri della stringa di query che, se presenti nell&#39;URL, vengono aggiunti alla stringa
* `hv` (facoltativo, stringa): elenco delimitato da virgole di parametri presenti nell&#39;hash URL che, se presenti nell&#39;URL, verranno aggiunti alla stringa
* `de` (facoltativo, stringa): delimitatore per suddividere singole parti della stringa. Impostazione predefinita: una pipe (`|`).

L’elemento dati restituisce una stringa contenente una versione dell’URL in formato descrittivo. Questa stringa viene in genere assegnata alla variabile `pageName`, ma può essere utilizzata anche in altre variabili.

### `getPreviousValue`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare nei cookie i valori generati dall’utente. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare il plug-in di Analytics [`getPreviousValue`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). L&#39;elemento dati `getPreviousValue` imposta una variabile su un valore impostato su un hit precedente.

L&#39;elemento dati `getPreviousValue` utilizza gli argomenti seguenti:

* `v` (stringa, obbligatorio): variabile con il valore che si desidera passare alla successiva richiesta di immagine. Una variabile comune utilizzata è `s.pageName` per recuperare il valore della pagina precedente.
* `c` (stringa, facoltativo): nome del cookie che memorizza il valore.  Se questo argomento non è impostato, verrà utilizzato per impostazione predefinita `"s_gpv"`.

Quando chiami questo elemento dati, restituisce il valore stringa contenuto nel cookie. Il plug-in reimposta la scadenza del cookie e assegna il valore della variabile dall&#39;argomento `v`. Il cookie scade dopo 30 minuti di inattività.

### `getQueryParam`

Consente di configurare il plug-in di Analytics [`getQueryParam`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). L&#39;elemento dati `getQueryParam` estrae il valore di qualsiasi parametro di stringa di query contenuto in un URL. È utile per estrarre i codici campagna, sia interni che esterni, dagli URL della pagina di destinazione. È utile anche quando si estraggono termini di ricerca o altri parametri di stringa di query. Questo elemento dati fornisce funzioni affidabili per l’analisi di URL complessi, inclusi hash e URL contenenti più parametri di stringhe di query.

L&#39;elemento dati `getQueryParam` utilizza gli argomenti seguenti:

* `qsp` (obbligatorio): elenco delimitato da virgole di parametri della stringa di query da cercare all&#39;interno dell&#39;URL. Non fa distinzione tra maiuscole e minuscole.
* `de` (facoltativo): delimitatore da utilizzare se più parametri della stringa di query corrispondono. Impostazione predefinita: stringa vuota.
* `url` (facoltativo): URL personalizzato, stringa o variabile da cui estrarre i valori dei parametri della stringa di query. Impostazione predefinita: `window.location`.

La chiamata di questo elemento dati restituisce un valore che dipende dagli argomenti e dall’URL indicati sopra:

* Se non viene trovato un parametro di stringa di query corrispondente, il metodo restituisce una stringa vuota.
* Se viene trovato un parametro della stringa di query corrispondente, il metodo restituisce il valore del parametro della stringa di query.
* Se viene trovato un parametro di stringa di query corrispondente ma il valore è vuoto, il metodo restituisce `true`.
* Se vengono trovati più parametri di stringa di query corrispondenti, il metodo restituisce una stringa con ogni valore di parametro delimitato dalla stringa nell&#39;argomento `de`.

### `getTimeParting`

Consente di configurare il plug-in di Analytics [`getTimeParting`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). L&#39;elemento dati `getTimeParting` acquisisce i dettagli del momento in cui si verifica un&#39;attività misurabile sul sito. Questo elemento dati è utile quando si desidera suddividere le metriche in base a qualsiasi divisione del tempo ripetibile in un determinato intervallo di date. Ad esempio, puoi confrontare i tassi di conversione tra due giorni diversi della settimana, ad esempio tutte le domeniche e tutti i giovedì. Puoi anche confrontare periodi della giornata, ad esempio tutte le mattine rispetto a tutte le sere.

L&#39;elemento dati `getTimeParting` utilizza l&#39;argomento seguente:

`t` (facoltativo ma consigliato, stringa): nome del fuso orario in cui convertire l&#39;ora locale del visitatore.  Ora UTC/GMT predefinita. Per un elenco completo dei valori validi, consultare [Elenco dei fusi orari del database TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) su Wikipedia.

I valori validi comuni includono:

* `"America/New_York"` per Ora Est
* `"America/Chicago"` per ora centrale
* `"America/Denver"` per fuso occidentale
* `"America/Los_Angeles"` per Ora Pacifico

La chiamata di questo elemento dati restituisce una stringa che contiene il seguente delimitato da una barra verticale (`|`):

* L&#39;anno corrente
* Il mese corrente
* Il giorno del mese
* Il giorno della settimana
* Ora corrente (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare il plug-in di Analytics [`getTimeSinceLastVisit`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). L&#39;elemento dati `getTimeSinceLastVisit` tiene traccia di quanto tempo un visitatore ha impiegato per tornare al sito dopo l&#39;ultima visita.

L&#39;elemento dati `getTimeSinceLastVisit` non utilizza argomenti. Restituisce il tempo trascorso dall’ultima volta che il visitatore è arrivato al sito, bucket nel seguente formato:

* Il tempo compreso tra 30 minuti e un’ora dall’ultima visita viene impostato sul valore di riferimento di mezzo minuto più vicino. Ad esempio, `"30.5 minutes"`, `"53 minutes"`
* Il tempo compreso tra un’ora e un giorno viene arrotondato al valore di riferimento di un quarto d’ora più vicino. Ad esempio, `"2.25 hours"`, `"7.5 hours"`
* Il tempo maggiore di un giorno viene arrotondato al valore di riferimento del giorno più vicino. Ad esempio, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Se un visitatore non ha visitato in precedenza o il tempo trascorso è superiore a due anni, il valore è impostato su `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare nei cookie i valori generati dall’utente. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare il plug-in di Analytics [`getValOnce`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). L&#39;elemento dati `getValOnce` impedisce che una variabile venga impostata come uguale allo stesso valore più di una volta.

L&#39;elemento dati `getValOnce` utilizza gli argomenti seguenti:

* `vtc` (obbligatorio, stringa): variabile da controllare e verificare se è stato impostato in precedenza su un valore identico
* `cn` (facoltativo, stringa): nome del cookie che contiene il valore da verificare. Impostazione predefinita: `"s_gvo"`
* `et` (facoltativo, numero intero): scadenza del cookie in giorni o minuti, a seconda dell&#39;argomento `ep`. Impostazione predefinita: `0`, che scade alla fine della sessione del browser
* `ep` (facoltativo, stringa): impostare questo argomento solo se è impostato anche l&#39;argomento `et`. Impostare questo argomento su `"m"` se si desidera che l&#39;argomento `et` scada in minuti anziché in giorni. Il valore predefinito è `"d"`, che imposta l&#39;argomento `et` in giorni.

Se l&#39;argomento `vtc` e il valore del cookie corrispondono, questo metodo restituisce una stringa vuota. Se l&#39;argomento `vtc` e il valore del cookie non corrispondono, il metodo restituisce l&#39;argomento `vtc` come stringa.

### `getVisitDuration`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare il plug-in di Analytics [`getVisitDuration`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). L&#39;elemento dati `getVisitDuration` tiene traccia del tempo in minuti in cui il visitatore è stato sul sito fino a quel momento.

L&#39;elemento dati `getVisitDuration` non utilizza argomenti. Restituisce uno dei seguenti valori:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (dove `[x]` è il numero di minuti trascorsi dall&#39;arrivo del visitatore sul sito)

### `getVisitNum`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare il plug-in di Analytics [`getVisitNum`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). L&#39;elemento dati `getVisitNum` restituisce il numero di visita per tutti i visitatori che arrivano sul sito entro il numero di giorni desiderato.

L&#39;elemento dati `getVisitNum` utilizza gli argomenti seguenti:

* `rp` (facoltativo, numero intero o stringa): il numero di giorni prima che il contatore del numero di visite venga ripristinato.  Impostazione predefinita: `365` se non impostata.
   * Quando questo argomento è `"w"`, il contatore viene ripristinato alla fine della settimana (questo sabato alle 23:59)
   * Quando questo argomento è `"m"`, il contatore viene ripristinato alla fine del mese (l&#39;ultimo giorno del mese)
   * Quando questo argomento è `"y"`, il contatore viene ripristinato alla fine dell&#39;anno (31 dicembre)
* `erp` (facoltativo, booleano): quando l&#39;argomento `rp` è un numero, questo argomento determina se la scadenza del numero di visita deve essere estesa. Se è impostato su `true`, gli hit successivi nel sito reimpostano il contatore dei numeri di visita. Se è impostato su `false`, gli hit successivi sul sito non si estendono quando il contatore del numero di visite si ripristina. Impostazione predefinita: `true`. Argomento non valido se l&#39;argomento `rp` è una stringa.

Il numero di visite aumenta ogni volta che il visitatore ritorna al sito dopo 30 minuti di inattività. Quando si richiama questo metodo, viene restituito un numero intero che rappresenta il numero di visita corrente del visitatore.

### `p_fo` (Solo Pagina Prima)

Consente di configurare il plug-in di Analytics [`p_fo`](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). L&#39;elemento dati `p_fo` è un&#39;utility che verifica l&#39;esistenza di un oggetto JavaScript specifico. Se l&#39;oggetto non esiste, il plug-in crea l&#39;oggetto e restituisce `true`. Se l&#39;oggetto JavaScript esiste già nella pagina, restituisce `false`. Questo elemento dati è utile per eseguire il codice esattamente una volta su una pagina.

L&#39;elemento dati `p_fo` utilizza gli argomenti seguenti:

* `on` (obbligatorio, stringa): nome dell&#39;oggetto JavaScript creato dall&#39;elemento dati se l&#39;oggetto non esiste ancora nella pagina.

Se l&#39;oggetto non esiste ancora, questo metodo restituisce `true` e crea l&#39;oggetto. Se l&#39;oggetto esiste già, questo metodo restituisce `false`.
