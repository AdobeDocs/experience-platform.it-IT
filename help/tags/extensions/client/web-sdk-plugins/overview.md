---
title: Panoramica dell’estensione Common Web SDK Plugins
description: Scopri l’estensione tag Common Web SDK Plugins in Adobe Experience Platform.
exl-id: 6052603b-1537-4dc7-9278-969d892ca15b
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 1%

---

# Panoramica dell’estensione Common Web SDK Plugins

>[!IMPORTANT]
>
>L&#39;estensione deve essere utilizzata con l&#39;estensione Adobe Experience Platform Web SDK. Per visualizzare informazioni sulla versione da utilizzare con AppMeasurement, consulta la panoramica sul [Estensione Common Analytics Plugins](../plugins/overview.md).

Questo documento illustra come configurare l’estensione tag Plugin dell’SDK Web e utilizzarla per potenziare [Estensione Adobe Experience Platform Web SDK](../sdk/overview.md).

## Configurare l’estensione Common Web SDK Plugins

Questa sezione fornisce un riferimento per le opzioni disponibili durante la configurazione dell’estensione dei plug-in dell’SDK per web.

>[!IMPORTANT]
>
>L’estensione Common Web SDK Plugins ha lo scopo di potenziare l’estensione Adobe Experience Platform Web SDK, tuttavia non è necessario installarla affinché l’estensione funzioni come previsto.

## Aggiunta di plug-in all’estensione Adobe Experience Platform Web SDK

Non è necessaria alcuna configurazione per inizializzare o aggiungere un plug-in alla libreria al di fuori di utilizzando i seguenti elementi di dati nativi forniti dall’estensione Common Web SDK Plugins:

* [`getAndPersistValue`](#getAndPersistValue)
* [`getGeoCoordinates`](#getGeoCoordinates)
* [`getNewRepeat`](#getNewRepeat)
* [&quot;getPagename&quot;](#getPagename)
* [`getPreviousValue`](#getPreviousValue)
* [`getQueryParam`](#getQueryParam)
* [`getTimeParting`](#getTimeParting)
* [`getTimeSinceLastVisit`](#getTimeSInceLastVisit)
* [`getValOnce`](#getValOnce)
* [`getVisitDuration`](#getVisitDuration)
* [`getVisitNum`](#getVisitNum)
* [&#39;pFo&#39;](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### `getAndPersistValue`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare nei cookie i valori generati dall’utente. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare [`getAndPersistValue` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). Il `getAndPersistValue` l’elemento dati memorizza un valore in un cookie che può essere recuperato in un secondo momento durante una visita.

Il `getAndPersistValue` l&#39;elemento dati fornisce i seguenti argomenti:

* `vtp` (obbligatorio): valore da mantenere da pagina a pagina
* `cn` (facoltativo): nome del cookie in cui memorizzare il valore. Se questo argomento non è impostato, il cookie viene denominato `"s_gapv"`
* `ex` (facoltativo): numero di giorni prima della scadenza del cookie. Se questo argomento è `0` o non è impostato, il cookie scade alla fine della visita (30 minuti di inattività).

Se la variabile in `vtp` viene impostato, quindi l&#39;elemento dati imposta il cookie e restituisce il valore del cookie. Se la variabile in `vtp` non è impostato, l&#39;elemento dati restituisce solo il valore del cookie.

### `getGeoCoordinates`

>[!IMPORTANT]
>
>Questo plug-in richiede l’accesso alla posizione sul client, ma non genera un’eccezione se non la ottiene.

Consente di configurare [`getGeoCoordinates` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). Il `getGeoCoordinates` l&#39;elemento dati acquisisce la latitudine e la longitudine dei dispositivi dei visitatori.

Il `getGeoCoordinates` l&#39;elemento dati non utilizza alcun argomento. Restituisce uno dei seguenti valori:

* `"geo coordinates not available"`: per dispositivi per i quali non sono disponibili dati di geolocalizzazione al momento dell’esecuzione del plug-in. Questo valore è comune al primo hit della visita, soprattutto quando i visitatori devono fornire il consenso per il tracciamento della loro posizione.
* `"error retrieving geo coordinates"`: quando il plug-in rileva errori durante il tentativo di recupero del percorso del dispositivo
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Dove [LATITUDINE]/[LONGITUDINE] sono rispettivamente latitudine e longitudine

### `getNewRepeat`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare [`getNewRepeat` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). Il `getNewRepeat` elemento dati determina se un visitatore del sito è un nuovo visitatore o un visitatore ripetuto entro un numero desiderato di giorni.

Il `getNewRepeat` data element utilizza gli argomenti seguenti:

* `d` (numero intero, facoltativo): il numero minimo di giorni necessari tra una visita e l’altra per reimpostare i visitatori su `"New"`. Se questo argomento non è impostato, il valore predefinito è 30 giorni.

Questo elemento dati restituisce il valore di `"New"` se il cookie impostato dall&#39;elemento dati non esiste o è scaduto. Restituisce il valore di `"Repeat"` se il cookie impostato dall&#39;elemento dati esiste e il tempo trascorso dall&#39;hit corrente e dal tempo impostato nel cookie è superiore a 30 minuti. Questo metodo restituisce lo stesso valore per un’intera visita.

### `getPageName`

Consente di configurare [`getPageName` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). Il `getPageName` L’elemento dati crea una versione dell’URL corrente in formato semplice e di facile lettura.

Il `getPageName` data element utilizza gli argomenti seguenti:

* `si` (facoltativo, stringa): ID inserito all’inizio della stringa che rappresenta l’ID del sito. Questo valore può essere un ID numerico o un nome descrittivo. Se non viene impostato, per impostazione predefinita viene utilizzato il dominio corrente.
* `qv` (facoltativo, stringa): elenco delimitato da virgole di parametri della stringa di query che, se presenti nell’URL, vengono aggiunti alla stringa
* `hv` (facoltativo, stringa): elenco delimitato da virgole di parametri presenti nell’hash dell’URL che, se presenti nell’URL, vengono aggiunti alla stringa
* `de` (facoltativo, stringa): delimitatore per suddividere singole parti della stringa. Valore predefinito per una pipe (`|`).

L’elemento dati restituisce una stringa contenente una versione dell’URL in formato descrittivo. Questa stringa viene in genere assegnata al `pageName` , ma può essere utilizzato anche in altre variabili.

### `getPreviousValue`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare nei cookie i valori generati dall’utente. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare [`getPreviousValue` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). Il `getPreviousValue` l’elemento dati imposta una variabile su un valore impostato sull’hit precedente.

Il `getPreviousValue` data element utilizza gli argomenti seguenti:

* `v` (stringa, obbligatorio): variabile con il valore che desideri trasmettere alla successiva richiesta di immagine. Una variabile comune utilizzata è `s.pageName` per recuperare il valore della pagina precedente.
* `c` (stringa, facoltativo): nome del cookie che memorizza il valore.  Se questo argomento non è impostato, viene utilizzato il valore predefinito `"s_gpv"`.

Quando chiami questo elemento dati, restituisce il valore stringa contenuto nel cookie. Il plug-in reimposta la scadenza del cookie e gli assegna il valore di variabile dalla `v` argomento. Il cookie scade dopo 30 minuti di inattività.

### `getQueryParam`

Consente di configurare [`getQueryParam` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). Il `getQueryParam` L’elemento dati estrae il valore di qualsiasi parametro della stringa di query contenuto in un URL. È utile per estrarre i codici campagna, sia interni che esterni, dagli URL della pagina di destinazione. È utile anche quando si estraggono termini di ricerca o altri parametri di stringa di query. Questo elemento dati fornisce funzioni affidabili per l’analisi di URL complessi, inclusi hash e URL contenenti più parametri di stringhe di query.

Il `getQueryParam` data element utilizza gli argomenti seguenti:

* `qsp` (obbligatorio): elenco delimitato da virgole di parametri della stringa di query da cercare all’interno dell’URL. Non fa distinzione tra maiuscole e minuscole.
* `de` (facoltativo): delimitatore da utilizzare se più parametri della stringa di query corrispondono. Impostazione predefinita: stringa vuota.
* `url` (facoltativo): URL personalizzato, stringa o variabile da cui estrarre i valori dei parametri della stringa di query. Predefinito su `window.location`.

La chiamata di questo elemento dati restituisce un valore che dipende dagli argomenti e dall’URL indicati sopra:

* Se non viene trovato un parametro di stringa di query corrispondente, il metodo restituisce una stringa vuota.
* Se viene trovato un parametro della stringa di query corrispondente, il metodo restituisce il valore del parametro della stringa di query.
* Se viene trovato un parametro di stringa di query corrispondente ma il valore è vuoto, il metodo restituisce `true`.
* Se vengono trovati più parametri di stringa di query corrispondenti, il metodo restituisce una stringa con ciascun valore di parametro delimitato dalla stringa nella `de` argomento.

### `getTimeParting`

Consente di configurare [`getTimeParting` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html?lang=it). Il `getTimeParting` data element acquisisce i dettagli del momento in cui si verifica un’attività misurabile sul sito. Questo elemento dati è utile quando si desidera suddividere le metriche in base a qualsiasi divisione del tempo ripetibile in un determinato intervallo di date. Ad esempio, puoi confrontare i tassi di conversione tra due giorni diversi della settimana, ad esempio tutte le domeniche e tutti i giovedì. Puoi anche confrontare periodi della giornata, ad esempio tutte le mattine rispetto a tutte le sere.

Il `getTimeParting` data element utilizza l’argomento seguente:

`t` (Facoltativo ma consigliato, stringa): nome del fuso orario in cui convertire l’ora locale del visitatore.  Ora UTC/GMT predefinita. Consulta la sezione [Elenco dei fusi orari del database TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) su Wikipedia per un elenco completo dei valori validi.

I valori validi comuni includono:

* `"America/New_York"` per l’ora orientale
* `"America/Chicago"` per l’ora centrale
* `"America/Denver"` per fuso occidentale
* `"America/Los_Angeles"` per l’ora Pacifico

Quando si richiama questo elemento dati, viene restituita una stringa contenente i seguenti elementi delimitati da una barra verticale (`|`):

* L&#39;anno corrente
* Il mese corrente
* Il giorno del mese
* Il giorno della settimana
* Ora corrente (AM/PM)

### `getTimeSinceLastVisit`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare [`getTimeSinceLastVisit` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). Il `getTimeSinceLastVisit` l’elemento dati tiene traccia di quanto tempo un visitatore ha impiegato per tornare al sito dopo l’ultima visita.

Il `getTimeSinceLastVisit` l&#39;elemento dati non utilizza alcun argomento. Restituisce il tempo trascorso dall’ultima volta che il visitatore è arrivato al sito, bucket nel seguente formato:

* Il tempo compreso tra 30 minuti e un’ora dall’ultima visita viene impostato sul valore di riferimento di mezzo minuto più vicino. Ad esempio, `"30.5 minutes"`, `"53 minutes"`
* Il tempo compreso tra un’ora e un giorno viene arrotondato al valore di riferimento di un quarto d’ora più vicino. Ad esempio, `"2.25 hours"`, `"7.5 hours"`
* Il tempo maggiore di un giorno viene arrotondato al valore di riferimento del giorno più vicino. Ad esempio, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Se un visitatore non ha visitato in precedenza o il tempo trascorso è superiore a due anni, il valore viene impostato su `"New Visitor"`.

### `getValOnce`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare nei cookie i valori generati dall’utente. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare [`getValOnce` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). Il `getValOnce` L’elemento dati impedisce che una variabile venga impostata uguale più volte allo stesso valore.

Il `getValOnce` data element utilizza gli argomenti seguenti:

* `vtc` (obbligatorio, stringa): variabile da verificare e vedere se è stata impostata su un valore identico in precedenza
* `cn` (facoltativo, stringa): nome del cookie che contiene il valore da verificare. Predefinito su `"s_gvo"`
* `et` (facoltativo, numero intero): scadenza del cookie in giorni (o minuti, a seconda del `ep` ). Impostazione predefinita `0`, che scade alla fine della sessione del browser
* `ep` (facoltativo, stringa): imposta questo argomento solo se `et` viene impostato anche. Imposta questo argomento su `"m"` se si desidera `et` l&#39;argomento scade in minuti anziché in giorni. Impostazione predefinita `"d"`, che imposta `et` in giorni.

Se il `vtc` corrisponde al valore di argomento e cookie, questo metodo restituisce una stringa vuota. Se il `vtc` e cookie non corrispondono, il metodo restituisce il valore `vtc` come stringa.

### `getVisitDuration`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare [`getVisitDuration` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). Il `getVisitDuration` data element tiene traccia della quantità di tempo in minuti in cui il visitatore è stato sul sito fino a quel momento.

Il `getVisitDuration` l&#39;elemento dati non utilizza alcun argomento. Restituisce uno dei seguenti valori:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (dove `[x]` è il numero di minuti trascorsi dall’arrivo del visitatore sul sito)

### `getVisitNum`

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in.

Consente di configurare [`getVisitNum` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). Il `getVisitNum` l’elemento dati restituisce il numero di visita per tutti i visitatori che arrivano sul sito entro il numero di giorni desiderato.

Il `getVisitNum` data element utilizza gli argomenti seguenti:

* `rp` (facoltativo, numero intero O stringa): il numero di giorni prima che il contatore dei numeri di visita venga ripristinato.  Impostazione predefinita `365` quando non è impostato.
   * Quando questo argomento è `"w"`, il contatore si ripristina alla fine della settimana (questo sabato alle 23:59)
   * Quando questo argomento è `"m"`, il contatore si ripristina alla fine del mese (l&#39;ultimo giorno del mese)
   * Quando questo argomento è `"y"`, il contatore viene ripristinato alla fine dell&#39;anno (31 dicembre)
* `erp` (facoltativo, booleano): quando `rp` argomento è un numero, questo argomento determina se la scadenza del numero di visita deve essere estesa. Se impostato su `true`, gli hit successivi sul sito reimpostano il contatore dei numeri di visita. Se impostato su `false`, gli hit successivi sul sito non si estendono quando il contatore dei numeri di visita si ripristina. Predefinito su `true`. Questo argomento non è valido quando `rp` è una stringa.

Il numero di visite aumenta ogni volta che il visitatore ritorna al sito dopo 30 minuti di inattività. Quando si richiama questo metodo, viene restituito un numero intero che rappresenta il numero di visita corrente del visitatore.

### `p_fo` (Solo Pagina Prima)

Consente di configurare [`p_fo` Plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). Il `p_fo` DataElement è un&#39;utility che controlla l&#39;esistenza di un oggetto JavaScript specifico. Se l&#39;oggetto non esiste, il plug-in crea l&#39;oggetto e restituisce `true`. Se l&#39;oggetto JavaScript esiste già nella pagina, restituisce `false`. Questo elemento dati è utile per eseguire il codice esattamente una volta su una pagina.

Il `p_fo` data element utilizza gli argomenti seguenti:

* `on` (obbligatorio, stringa): nome dell&#39;oggetto JavaScript creato dall&#39;elemento dati, se l&#39;oggetto non esiste ancora nella pagina.

Se l&#39;oggetto non esiste ancora, questo metodo restituisce `true` e crea l’oggetto. Se l&#39;oggetto esiste già, questo metodo restituisce `false`.
