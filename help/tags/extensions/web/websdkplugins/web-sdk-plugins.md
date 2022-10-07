---
title: Panoramica dell’estensione Common Web SDK Plugins
description: Scopri l’estensione tag Common Web SDK Plugins in Adobe Experience Platform.
exl-id: null
source-git-commit: 482ea64e25c7bbbb2eef772fb97064e34f0689e7
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 4%

---

# Panoramica dell’estensione Common Web SDK Plugins

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../launch-term-updates.md) come riferimento consolidato delle modifiche terminologiche.

>[!IMPORTANT]
>
>L&#39;estensione è destinata all&#39;utilizzo con [!DNL Adobe Experience Platform Web SDK] estensione. Per informazioni sulla versione da utilizzare con AppMeasurement, consulta questo collegamento.

Utilizza questo riferimento per informazioni sulla configurazione dell’estensione Plugins dell’SDK per web e sulle opzioni disponibili quando utilizzi questa estensione per potenziare il [!DNL Adobe Experience Platform Web SDK] Estensione.

## Configurare l’estensione Common Web SDK Plugins

Questa sezione fornisce un riferimento per le opzioni disponibili durante la configurazione dell’estensione Plugins dell’SDK per web.

>[!IMPORTANT]
>
>L’estensione Common Web SDK Plugins è destinata ad aumentare il [!DNL Adobe Experience Platform Web SDK] tuttavia, non è necessario che l&#39;estensione funzioni come previsto.

Non è richiesta alcuna configurazione aggiuntiva a livello di estensione.

## Aggiunta di plug-in all’estensione [!DNL Adobe Experience Platform Web SDK]

A differenza della controparte AppMeasurement, non è necessaria alcuna configurazione per inizializzare o aggiungere un plug-in alla libreria al di fuori dell&#39;utilizzo degli elementi dati nativi forniti. Vedi sotto per ulteriori informazioni su ciascun elemento dati.

## Elementi dati dell’estensione Common Web SDK Plugins

L’estensione Common Web SDK Plugins fornisce i seguenti elementi dati:

* [getAndPersistValue](#getAndPersistValue)
* [getGeoCoordinates](#getGeoCoordinates)
* [getNewRepeat](#getNewRepeat)
* [getPagename](#getPagename)
* [getPreviousValue](#getPreviousValue)
* [getQueryParam](#getQueryParam)
* [getTimeParting](#getTimeParting)
* [getTimeSinceLastVisit](#getTimeSInceLastVisit)
* [getValOnce](#getValOnce)
* [getVisitDuration](#getVisitDuration)
* [getVisitNum](#getVisitNum)
* [pFo](#pFo)

[//]: # (- [ ] Add links to plugin pages within the data elements below)

### getAndPersistValue

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare i valori generati dall’utente nei cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in .

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati in Adobe Experience Platform per configurare e configurare il [plugin getAndPersistValue](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getandpersistvalue.html). La `getAndPersistValue` l’elemento dati ti consente di memorizzare un valore in un cookie che può essere recuperato successivamente durante una visita. Ruolo simile al [!UICONTROL Durata dello storage] in Adobe Experience Platform Launch.

La `getAndPersistValue` data element fornisce i seguenti argomenti:

* **`vtp`** (obbligatorio): Valore da persistere da pagina a pagina
* **`cn`** (facoltativo): Nome del cookie da cui memorizzare il valore. Se questo argomento non è impostato, il cookie viene denominato `"s_gapv"`
* **`ex`** (facoltativo): Il numero di giorni prima della scadenza del cookie. Se questo argomento è `0` o non è impostato, il cookie scade alla fine della visita (30 minuti di inattività).

Se la variabile nel `vtp` viene impostato, quindi l&#39;elemento dati imposta il cookie e restituisce il valore del cookie. Se la variabile nel `vtp` L&#39;argomento non è impostato, quindi l&#39;elemento dati restituisce solo il valore del cookie.

### getGeoCoordinates

>[!IMPORTANT]
>
>Questo plug-in richiede l&#39;accesso alla posizione sul client ma non genera un&#39;eccezione se non lo ottiene.

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati in Adobe Experience Platform per configurare e configurare il [Plug-in getGeoCoordinates](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getgeocoordinates.html). La `getGeoCoordinates` data element consente di acquisire la latitudine e la longitudine dei dispositivi dei visitatori.

La `getGeoCoordinates` l&#39;elemento dati non utilizza argomenti. Restituisce uno dei seguenti valori:

* `"geo coordinates not available"`: Per i dispositivi che non dispongono di dati di geolocalizzazione al momento dell&#39;esecuzione del plug-in. Questo valore è comune per il primo hit della visita, soprattutto quando i visitatori hanno bisogno del consenso per tracciare la propria posizione.
* `"error retrieving geo coordinates"`: Quando il plug-in rileva errori durante il tentativo di recupero della posizione del dispositivo
* `"latitude=[LATITUDE] | longtitude=[LONGITUDE]"`: Dove [LATITUDINE]/[LONGITUDINE] sono rispettivamente latitudine e longitudine

### getNewRepeat

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in .

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [plugin getNewRepeat](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getnewrepeat.html). La `getNewRepeat` data element consente di determinare se un visitatore del sito è un nuovo visitatore o un visitatore ripetuto entro un numero desiderato di giorni.

La `getNewRepeat` l&#39;elemento dati utilizza i seguenti argomenti:

* **`d`** (intero, facoltativo): Il numero minimo di giorni necessari tra le visite che reimposta i visitatori su `"New"`. Se questo argomento non viene impostato, viene impostato automaticamente su 30 giorni.

Questo elemento dati restituisce il valore di `"New"` se il cookie impostato dall&#39;elemento dati non esiste o è scaduto. Restituisce il valore di `"Repeat"` se il cookie impostato dall&#39;elemento dati esiste e il tempo trascorso dall&#39;hit corrente e il tempo impostato nel cookie è maggiore di 30 minuti. Questo metodo restituisce lo stesso valore per un’intera visita.

### getPageName

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [Plug-in getPageName](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpagename.html). La `getPageName` data element crea una versione formattata semplice e intuitiva dell&#39;URL corrente.

La `getPageName` l&#39;elemento dati utilizza i seguenti argomenti:

* **`si`** (facoltativo, stringa): Un ID inserito all&#39;inizio della stringa che rappresenta l&#39;ID del sito. Questo valore può essere un ID numerico o un nome descrittivo. Se non è impostato, viene impostato automaticamente sul dominio corrente.
* **`qv`** (facoltativo, stringa): Elenco delimitato da virgole di parametri della stringa di query che, se trovati nell’URL, vengono aggiunti alla stringa
* **`hv`** (facoltativo, stringa): Elenco di parametri delimitati da virgole trovati nell’hash dell’URL che, se trovato nell’URL, vengono aggiunti alla stringa
* **`de`** (facoltativo, stringa): Il delimitatore per suddividere singole parti della stringa. Impostazione predefinita di una tubazione (`|`).

L&#39;elemento dati restituisce una stringa contenente una versione in formato descrittivo dell&#39;URL. Questa stringa viene generalmente assegnata alla `pageName` , ma può essere utilizzato anche in altre variabili.

### getPreviousValue

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare i valori generati dall’utente nei cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in .

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [plug-in getPreviousValue](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getpreviousvalue.html). La `getPreviousValue` data element consente di impostare una variabile su un valore impostato su un hit precedente.

La `getPreviousValue` l&#39;elemento dati utilizza i seguenti argomenti:

* **`v`** (stringa, obbligatoria): Variabile con il valore che si desidera passare alla richiesta di immagine successiva. Una variabile comune utilizzata è `s.pageName` per recuperare il valore della pagina precedente.
* **`c`** (stringa, facoltativo): Nome del cookie che memorizza il valore.  Se questo argomento non è impostato, viene utilizzata l&#39;impostazione predefinita `"s_gpv"`.

Quando chiami questo elemento dati, restituisce il valore stringa contenuto nel cookie. Il plug-in quindi reimposta la scadenza del cookie e gli assegna il valore della variabile dal `v` argomento. Il cookie scade dopo 30 minuti di inattività.

### getQueryParam

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [Plug-in getQueryParam](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getqueryparam.html). La `getQueryParam` l’elemento dati ti consente di estrarre il valore di qualsiasi parametro della stringa di query contenuto in un URL. È utile per estrarre i codici della campagna, sia interni che esterni, dagli URL della pagina di destinazione. È utile anche per l’estrazione dei termini di ricerca o di altri parametri della stringa di query. Questo elemento dati fornisce solide funzioni per l’analisi di URL complessi, tra cui hash e URL contenenti più parametri di stringa di query.

La `getQueryParam` l&#39;elemento dati utilizza i seguenti argomenti:

* **`qsp`** (obbligatorio): Elenco delimitato da virgole dei parametri della stringa di query da cercare all’interno dell’URL. Non fa distinzione tra maiuscole e minuscole.
* **`de`** (facoltativo): Il delimitatore da utilizzare se più parametri della stringa di query corrispondono. Impostazione predefinita di una stringa vuota.
* **`url`** (facoltativo): Un URL personalizzato, una stringa o una variabile da cui estrarre i valori dei parametri della stringa di query. Predefinito su `window.location`.

Una chiamata a questo elemento dati restituisce un valore a seconda degli argomenti precedenti e dell&#39;URL:

* Se non viene trovato un parametro della stringa di query corrispondente, il metodo restituisce una stringa vuota.
* Se viene trovato un parametro della stringa di query corrispondente, il metodo restituisce il valore del parametro della stringa di query.
* Se viene trovato un parametro della stringa di query corrispondente ma il valore è vuoto, il metodo restituisce `true`.
* Se vengono trovati più parametri di stringa di query corrispondenti, il metodo restituisce una stringa con ogni valore di parametro delimitato dalla stringa nel `de` argomento.

### getTimeParting

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [plugin getTimeParting](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimeparting.html). La `getTimeParting` data element ti consente di acquisire i dettagli del momento in cui si svolge un’attività misurabile sul tuo sito. Questo elemento dati è utile quando desideri suddividere le metriche in base a una suddivisione ripetibile del tempo su un determinato intervallo di date. Ad esempio, puoi confrontare i tassi di conversione tra due giorni della settimana diversi, ad esempio tutti i giorni della domenica rispetto a tutti i giovedì. Puoi anche confrontare i periodi del giorno, ad esempio tutte le mattine rispetto a tutte le serate.

La `getTimeParting` l&#39;elemento dati utilizza il seguente argomento:

**`t`** (Facoltativo ma consigliato, stringa): Nome del fuso orario in cui convertire l’ora locale del visitatore.  Impostazione predefinita per l’ora UTC/GMT. Vedi [Elenco dei fusi orari del database TZ](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) su Wikipedia per un elenco completo di valori validi.

I valori validi comuni includono:

* `"America/New_York"` per l&#39;ora orientale
* `"America/Chicago"` per l&#39;ora centrale
* `"America/Denver"` per l&#39;ora di montagna
* `"America/Los_Angeles"` per l&#39;ora del Pacifico

Se si richiama questo elemento dati, viene restituita una stringa contenente i seguenti elementi delimitati da una tubazione (`|`):

* L&#39;anno in corso
* Il mese in corso
* Il giorno del mese
* Il giorno della settimana
* Ora attuale (AM/PM)

### getTimeSinceLastVisit

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in .

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [plug-in getTimeSinceLastVisit](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/gettimesincelastvisit.html). La `getTimeSinceLastVisit` data element consente di tenere traccia di quanto tempo un visitatore ha impiegato per tornare al tuo sito dopo la sua ultima visita.

La `getTimeSinceLastVisit` l&#39;elemento dati non utilizza argomenti. Restituisce la quantità di tempo trascorso dall’ultima volta che il visitatore è arrivato al sito, bucket nel seguente formato:

* Tempo compreso tra 30 minuti e un’ora dall’ultima visita impostato sul valore di riferimento di mezzo minuto più vicino. Esempio, `"30.5 minutes"`, `"53 minutes"`
* Il tempo tra un’ora e un giorno viene arrotondato al valore di riferimento di trimestre più vicino. Esempio, `"2.25 hours"`, `"7.5 hours"`
* L’ora maggiore di un giorno viene arrotondata al valore di riferimento del giorno più vicino. Esempio, `"1 day"`, `"3 days"`, `"9 days"`, `"372 days"`
* Se un visitatore non ha visitato il sito prima o se il tempo trascorso è superiore a due anni, il valore è impostato su `"New Visitor"`.

### getValOnce

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie e consente di memorizzare i valori generati dall’utente nei cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in .

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [plug-in getValOnce](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html). La `getValOnce` l&#39;elemento dati impedisce che una variabile venga impostata più di una volta sullo stesso valore.

La `getValOnce` l&#39;elemento dati utilizza i seguenti argomenti:

* **`vtc`** (obbligatorio, stringa): Variabile da controllare e vedere se è stata impostata in precedenza su un valore identico
* **`cn`** (facoltativo, stringa): Nome del cookie che contiene il valore da controllare. Predefinito su `"s_gvo"`
* **`et`** (facoltativo, numero intero): La scadenza del cookie in giorni (o minuti, a seconda del `ep` (argomento). Predefinito su `0`, che scade alla fine della sessione del browser
* **`ep`** (facoltativo, stringa): Imposta questo argomento solo se `et` viene impostato anche l&#39;argomento . Imposta questo argomento su `"m"` se vuoi `et` argomento che scade in minuti anziché in giorni. Predefinito su `"d"`, che imposta `et` argomento in giorni.

Se la `vtc` corrispondenza tra argomento e valore cookie, questo metodo restituisce una stringa vuota. Se la `vtc` l&#39;argomento e il valore del cookie non corrispondono, il metodo restituisce il `vtc` come stringa.

### getVisitDuration

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in .

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [Plug-in getVisitDuration](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitduration.html). La `getVisitDuration` elemento dati tiene traccia della quantità di tempo in minuti che il visitatore ha visitato il sito fino a quel momento.

La `getVisitDuration` l&#39;elemento dati non utilizza argomenti. Restituisce uno dei seguenti valori:

* `"first hit of visit"`
* `"less than a minute"`
* `"1 minute"`
* `"[x] minutes"` (4) `[x]` è il numero di minuti trascorsi dall&#39;arrivo del visitatore sul sito)

### getVisitNum

>[!IMPORTANT]
>
>Questo elemento dati imposta i cookie. Per ulteriori informazioni, consulta la documentazione specifica del plug-in .

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [plug-in getVisitNum](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvisitnum.html). La `getVisitNum` data element restituisce il numero di visita per tutti i visitatori che accedono al sito entro il numero di giorni desiderato.

La `getVisitNum` l&#39;elemento dati utilizza i seguenti argomenti:

* **`rp`** (facoltativo, stringa OR intera): Il numero di giorni prima della reimpostazione del contatore del numero di visita.  Predefinito su `365` quando non è impostato.
   * Quando questo argomento è `"w"`, il contatore riprende alla fine della settimana (questo sabato alle 11:59)
   * Quando questo argomento è `"m"`, il contatore viene reimpostato alla fine del mese (l’ultimo giorno del mese)
   * Quando questo argomento è `"y"`, il contatore riprende alla fine dell&#39;anno (31 dicembre)
* **`erp`** (facoltativo, booleano): Quando il `rp` argomento è un numero, questo argomento determina se la scadenza del numero di visita deve essere estesa. Se impostato su `true`, gli hit successivi al sito reimpostano il contatore dei numeri di visita. Se impostato su `false`, gli hit successivi al sito non si estendono quando il contatore del numero di visite viene reimpostato. Predefinito su `true`. Questo argomento non è valido quando `rp` argomento è una stringa.

Il numero di visite aumenta ogni volta che il visitatore ritorna al tuo sito dopo 30 minuti di inattività. Una chiamata a questo metodo restituisce un numero intero che rappresenta il numero di visita corrente del visitatore.

### p_fo (solo pagina prima)

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il [plug-in p_fo](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/p-fo.html). La `p_fo` data element è un&#39;utility che controlla l&#39;esistenza di un oggetto JavaScript specifico. Se l&#39;oggetto non esiste, il plug-in crea l&#39;oggetto e restituisce `true`. Se l&#39;oggetto JavaScript esiste già nella pagina, restituisce `false`. Questo elemento dati è utile per eseguire il codice esattamente una volta su una pagina.

La `p_fo` l&#39;elemento dati utilizza i seguenti argomenti:

* **su** (obbligatorio, stringa): Nome dell&#39;oggetto JavaScript creato dall&#39;elemento dati se l&#39;oggetto non esiste ancora nella pagina.

Se l&#39;oggetto non esiste ancora, questo metodo restituisce `true` e crea l&#39;oggetto. Se l&#39;oggetto esiste già, questo metodo restituisce `false`.
