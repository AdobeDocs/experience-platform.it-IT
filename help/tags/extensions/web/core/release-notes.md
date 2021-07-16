---
title: Note sulla versione dell’estensione Core
description: Note aggiornate sulla versione dell’estensione Core in Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 90%

---

# Note sulla versione dell’estensione Core

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

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
* **Ritardo collegamento contrassegnato sull’evento clic come “non più supportato”.** - ulteriori informazioni sono disponibili sul  [Data Collection ](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) Blogfor Adobe Experience Platform

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

* **Supporto per nonce CSP**: l&#39;estensione core presenta ora un parametro di configurazione opzionale. È possibile aggiungere un elemento dati che faccia riferimento a un nonce. Se configurati, tutti gli script in linea aggiunti da un tag alla pagina utilizzano il nonce configurato. Questa modifica supporta l’utilizzo di criteri sulla sicurezza dei contenuti (Content Security Policy, CSP) con un nonce, in modo che gli script Platform Launch possano essere caricati in un ambiente CSP. Per ulteriori informazioni sull’utilizzo di Platform Launch con CSP, consulta [questo articolo](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/content-security-policy.html).

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
* **Correzione bug** : è stato corretto un problema a causa del quale una regola, utilizzando un evento Page Bottom e un’azione Custom Code su una pagina in cui i tag venivano caricati in modo sincrono ma non correttamente installati (nessuna chiamata a  `_satellite.pageBottom()`), avrebbe azzerato il contenuto del sito web.
* **Correzione bug** : è stato corretto un problema a causa del quale l’opzione Enter Viewport non funzionava se la libreria di tag veniva caricata in modo asincrono e terminava il caricamento dopo l’attivazione dell’evento DOMContentLoaded del browser.

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
