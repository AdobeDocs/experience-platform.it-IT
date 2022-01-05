---
title: Note sulla versione dell’estensione Core
description: Note aggiornate sulla versione dell’estensione Core in Adobe Experience Platform.
exl-id: a049b2d5-7a00-435d-bcc7-112658a53a1e
source-git-commit: 5441c6ca0c15996ee06afa2c795ec5ae6e030f35
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 74%

---

# Note sulla versione dell’estensione Core

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## 4 gennaio 2022

v3.3.0

* Modifica il [Azione Trigger Direct Call](./overview.md#direct-call-action) in modo da poter fornire informazioni sull’evento personalizzato da inviare alle regole di chiamata diretta.

## 8 ottobre 2021

v3.2.2

* Correggi lo schema JSON dell’elemento dati del valore condizionale per tutti gli operatori disponibili.
* Correzione https://github.com/adobe/reactor-extension-core/issues/64.

## 23 settembre 2021

v3.2.1

* È stato corretto un errore a causa del quale l’inizializzazione della visualizzazione dell’elemento dati del valore condizionale non funzionava correttamente quando i valori del campo erano 0.

## 23 settembre 2021

v3.2.0

Nell’elemento dati Valore condizionale sono state introdotte le seguenti modifiche:

* Aggiungi una casella di controllo per i valori condizionali e di fallback che consentono all’utente di scegliere se non definiti deve essere il valore restituito.
* I valori numerici sono esposti come numeri nell&#39;oggetto settings.
* Il valore condizionale non è più necessario in modo che possa comportarsi nello stesso modo del valore di fallback.

## 17 settembre 2021

v3.1.1

* È stato corretto un errore JS che impediva il caricamento della visualizzazione della condizione dell’intervallo di date.

## 16 settembre 2021

v3.1.0

Sono stati aggiunti nuovi elementi dati:

* Oggetto unito: consente di selezionare più elementi dati che forniranno ciascuno un oggetto. Questi oggetti verranno profondamente (ricorsivamente) uniti per produrre un nuovo oggetto.
* Valore condizionale - Restituisce uno dei due valori (condizionaleValue o fallbackValue) in base al risultato del confronto.
* Ambiente runtime - Restituisce una delle seguenti variabili di ambiente Launch: stage dell&#39;ambiente, data build della libreria, nome della proprietà, ID della proprietà, nome della regola, id della regola, tipo di evento, payload dei dettagli dell&#39;evento, identificatore di chiamata diretta.
* Strumenti JavaScript - Wrapper per operazioni JavaScript comuni: manipolazione di base delle stringhe (sostituzione, sottostringa, corrispondenza regex, primo e ultimo indice, divisione, sezione), operazioni di base array (sezione, join, pop, shift) e operazioni universali di base (sezione, lunghezza).
* Attributi del dispositivo - Restituisce gli attributi del dispositivo come le dimensioni della finestra o dello schermo.

## 11 agosto 2021

v3.0.0

* PDCL-6153: Aggiunge il supporto per richiamare in modo affidabile l’URL completo per le azioni del codice personalizzato memorizzate nella cache.

La versione 3.0.0 dell’estensione Core è associata a modifiche in [v27.2.0 del runtime web Turbine](https://github.com/adobe/reactor-turbine/releases/tag/v27.2.0), che consente agli utenti di caricare la propria libreria tra molte aree di hosting gestite da Adobe se l&#39;azienda dell&#39;utente supporta la rete CDN Premium.

Questo aggiornamento è facoltativo e retrocompatibile per gli utenti senza CDN Premium e obbligatorio per i clienti che hanno abilitato CDN Premium sulla propria azienda.

## 20 maggio 2021

v2.0.7

* È stato corretto un problema a causa del quale le interazioni del mouse sugli input di testo non funzionavano più correttamente.
* L’utilizzo delle condizioni Browser e Sistema operativo è stato dichiarato obsoleto.

## 4 maggio 2021

v2.0.6

* Aggiornamento minore per correggere la distorsione delle icone che si verifica quando si cambiano le dimensioni dello schermo.

## 11 marzo 2021

v2.0.5

* È stato aggiornato il codice nella valutazione runtime per gli eventi e le azioni che dispongono di un’opzione di ritardo, che ora supporta i valori degli elementi dati aggiunti nella versione v2.0.4, in modo da forzare correttamente le stringhe con i numeri.

## 9 marzo 2021

v2.0.4

* Supporto per elementi dati per vari campi. Il supporto per gli elementi dati è stato aggiunto ai seguenti eventi: “Tempo sulla pagina”, “Entra in viewport”, “Passaggio del mouse” e “Tempo file multimediale riprodotto”; e alle seguenti condizioni: “Tempo sul sito” e “Confronto valori”.
* È stato aggiunto il supporto del comportamento predefinito per Ctrl/Comando + clic e per clic del pulsante centrale del mouse quando si utilizza Ritardo collegamento.
* **Ritardo collegamento contrassegnato sull’evento clic come “non più supportato”.** - Ulteriori informazioni sono disponibili sul [Blog di Data Collection](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) per Adobe Experience Platform.

## 6 gennaio 2021

v1.9.0

* **Nuova azione &quot;Trigger Direct Call&quot;**: l&#39;estensione Core ora include un nuovo tipo di azione denominato `Trigger Direct Call`. Può essere utilizzato quando si desidera attivare una regola di chiamata diretta tramite un&#39;azione di una regola diversa. Viene mappato direttamente sul metodo `_satellite.track()`. Ringraziamo [Jan Exner](https://twitter.com/jexner) per questo contributo.

## 8 dicembre 2020

v1.8.4

* È stato corretto un bug a causa del quale un utente non poteva cancellare o annullare l’impostazione della chiave nonce di CSP.

## 28 luglio 2020

v1.8.3

* È stato corretto un bug a causa del quale il nonce CSP veniva letto una sola volta all’avvio dell’estensione, invece di essere estratto nuovamente durante la chiamata dell’azione codice personalizzata.

## 13 luglio 2020

v1.8.2

* È stato corretto un bug a causa del quale l’azione Codice personalizzato generava un errore se il codice HTML conteneva token senza un nome di tag (ad esempio, commenti).

## 10 luglio 2020

v1.8.1

* È stato corretto un bug a causa del quale le entità HTML personalizzate all’interno degli attributi dei tag `script` e `style` non venivano decodificate correttamente prima di essere scritte sulla pagina.
* È stato corretto un bug che provocava un errore in presenza di un’azione esterna con codice personalizzato priva di contenuto. L’azione esterna con codice personalizzato è un’azione caricata da un file diverso dalla libreria (quando l’evento che attiva la regola non è libraryLoaded o pageBottom).

## 6 luglio 2020

v1.8.0

* **Promesse in Custom Code**: le condizioni di Custom Code e le azioni JavaScript che non vengono eseguite nell’ambito globale ora possono restituire promesse. È possibile utilizzarle per fare in modo che condizioni e azioni successive attendano il completamento di un processo asincrono nel Custom Code prima di passare all’elemento successivo.
* **Callback nelle azioni Custom Code HTML**: è possibile ottenere lo stesso risultato nelle azioni Custom Code HTML utilizzando i callback `onCustomCodeSuccess()` e `onCustomCodeFailure()`.

Per informazioni più dettagliate, consulta il [riferimento all’estensione core](./overview.md) in Condizioni > Custom Code e Azioni > Custom Code.

## 7 aprile 2020

v1.7.3

* **Aumento della lunghezza del campo di testo**: i campi di input di testo ora hanno un layout flex per utilizzare al meglio la larghezza dello schermo degli utenti e dare più spazio a stringhe di testo più lunghe.

## 1 novembre 2019

v1.7.0

* **Accesso a `event` Variable Within Custom Code Data Element**: È ora possibile fare riferimento all&#39;evento dall&#39;interno di un elemento dati con codice personalizzato quando viene eseguito facendo riferimento a una regola. L&#39;oggetto conterrà informazioni utili sull&#39;evento che ha attivato la regola. Ringraziamo [Stewart Schilling](https://twitter.com/sdi_stewart) per questo contributo.

## 7 ottobre 2019

v1.6.2

* **Nuovo tipo di elemento dati “Constant”**: l’estensione core ora include un nuovo tipo di elemento dati chiamato `Constant`. Può essere utilizzato quando devi memorizzare un valore costante a cui verrà fatto riferimento in varie condizioni, azioni o codice personalizzato. Ringraziamo [Jan Exner](https://twitter.com/jexner) per questo contributo.

## 11 settembre 2019

v1.6.1

* **Supporto per nonce CSP**: l&#39;estensione core presenta ora un parametro di configurazione opzionale. È possibile aggiungere un elemento dati che faccia riferimento a un nonce. Se configurati, tutti gli script in linea aggiunti alla pagina da un tag usano il nonce configurato. Questa modifica supporta l’utilizzo di criteri sulla sicurezza dei contenuti con un nonce in modo che gli script di tag possano essere caricati in un ambiente CSP. Per ulteriori informazioni sull’utilizzo dei tag con un CSP, consulta [qui](../../../ui/client-side/content-security-policy.md).

## 18 giugno 2019

v1.5.0

* **Direct Call Logging**: la registrazione del browser per le regole di chiamata diretta fornirà ulteriori dettagli quando trasmessa.

## 8 maggio 2019

v1.4.3

* **Campi di input**: i campi di input ora sono molto più lunghi.
* **Custom Event**: ora è possibile utilizzare il tipo di evento personalizzato con gli eventi inviati dalla finestra.
* **Correzione bug**: è stato corretto un bug a causa del quale il valore della condizione Value Comparison non supportava il valore 0.
* **Correzione bug**: exchange\_ url è stato aggiornato, quindi puoi visualizzare l&#39;elenco delle estensioni principali in Adobe Exchange.

## 8 gennaio 2019

v1.4.2

* **Evento Enters Viewport**: in precedenza l&#39;evento Enters Viewport veniva attivato solo una volta per pagina. Questo comportamento può essere configurato per attivarsi ogni volta che l&#39;elemento entra nel viewport.
* **Evento Custom Event**: gli eventi personalizzati possono ora contenere dati contestuali che possono essere utilizzati all&#39;interno di condizioni e azioni.
* **Evento Click**: quando imposti un ritardo di collegamento sull&#39;evento Click, che registra correttamente per i discendenti dell&#39;ancoraggio e non solo sull&#39;ancoraggio stesso.

## 8 novembre 2018

* **Opzione Persist Cohort**: l&#39;opzione di mantenere una coorte è stata aggiunta alla condizione Sampling. Ciò ha l&#39;effetto di mantenere un utente dentro o fuori la coorte di campionamento tra le diverse sessioni. Ad esempio, se la casella di controllo “persist cohort” è selezionata e la condizione restituisce true la prima volta che viene eseguita per un visitatore specifico, restituirà true su tutte le esecuzioni successive della condizione per lo stesso visitatore. Analogamente, se la casella di controllo &quot;persist cohort&quot; è selezionata e la condizione restituisce false la prima volta che viene eseguita per un visitatore specifico, restituirà false su tutte le esecuzioni successive della condizione per lo stesso visitatore.
* **Correzione di bug**: è stato risolto un problema che causava la cancellazione del contenuto del sito Web da parte di una regola con un evento Page Bottom e un’azione Custom Code su una pagina in cui i tag venivano caricati in modo sincrono ma non erano installati correttamente (nessuna chiamata a `_satellite.pageBottom()`).
* **Correzione di bug**: è stato risolto un problema che causava il mancato funzionamento di Enters Viewport se la libreria di tag veniva caricata in modo asincrono e il caricamento veniva completato dopo che l’evento DOMContentLoaded del browser era stato avviato.

## 24 maggio 2018

* **Funzionalità**: è stata aggiunta una condizione Value Comparison, che confronta due valori utilizzando uno qualsiasi dei vari operatori disponibili. Questo sostituisce la funzionalità di diverse condizioni precedenti che erano troppo specifiche.
* **Funzionalità**: aggiunta di una condizione Max Frequency, che consente di specificare il numero di volte che la condizione deve restituire true entro un intervallo di tempo o nell&#39;occorrenza dell&#39;evento. Esempi: 5 volte al giorno, 2 volte per visita.

## 11 aprile 2018

* **Funzionalità**: i Data elements possono ora fare riferimento ad altri elementi di dati.

## 20 marzo 2018

* **Correzione bug**: le finestre di Custom Code generavano `document.write` errori e non venivano eseguite in implementazioni asincrone
* **Correzione bug**: i moduli principali non erano inclusi in una libreria
* **Correzione bug**: si sono verificati problemi con valori minimi e massimi sull&#39;elemento dati Random Number

## 10 gennaio 2018

* **Funzionalità**: Random Number Data Element
* **Funzionalità**: Page Info Data Element
* **Funzionalità**: Date Condition
* **Funzionalità**: Sampling Condition
