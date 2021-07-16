---
title: Supporto di Content Security Policy (CSP)
description: Scopri come gestire le restrizioni dell’informativa sulla sicurezza dei contenuti (CSP) durante l’integrazione del sito web con i tag in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 59%

---

# Supporto di Content Security Policy (CSP)

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

I Criteri sulla sicurezza dei contenuti (CSP) sono una funzione di sicurezza che aiuta a prevenire attacchi alla vulnerabilità cross-site scripting (XSS). Questo accade quando il browser viene indotto a eseguire contenuto dannoso che sembra provenire da una fonte attendibile ma che in realtà proviene da un&#39;altra posizione. I CSP consentono al browser di verificare (per conto dell’utente) che lo script provenga effettivamente da una sorgente affidabile.

I CSP sono implementati aggiungendo un’intestazione HTTP `Content-Security-Policy` alle risposte del server o aggiungendo un elemento `<meta>` configurato nella sezione `<head>` dei file HTML.

>[!NOTE]
>
> Per informazioni più dettagliate sui CSP, consulta i [documenti web MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

I tag in Adobe Experience Platform sono un sistema di gestione dei tag progettato per caricare dinamicamente gli script sul sito web. I CSP predefiniti bloccano questi script caricati dinamicamente per potenziali problemi di sicurezza. Questo documento fornisce indicazioni su come configurare i CSP per consentire gli script caricati in modo dinamico dai tag.

Se desideri che i tag funzionino con i CSP, ci sono due sfide principali da superare:

* **L&#39;origine della libreria di tag deve essere attendibile.** Se questa condizione non viene soddisfatta, la libreria di tag e gli altri file JavaScript richiesti vengono bloccati dal browser e non vengono caricati sulla pagina.
* **Gli script in linea devono essere consentiti.** Se questa condizione non viene soddisfatta, le azioni della regola Codice personalizzato vengono bloccate sulla pagina e non vengono eseguite correttamente.

Una maggiore sicurezza richiede una maggiore quantità di lavoro da parte del creatore dei contenuti. Se desideri utilizzare i tag e disporre di un CSP, è necessario risolvere entrambi i problemi senza che altri script vengano erroneamente contrassegnati come sicuri. Il resto del presente documento fornisce indicazioni su come raggiungere questo obiettivo.

## Aggiungere tag come origine affidabile

Quando utilizzi CSP, devi includere tutti i domini affidabili nel valore dell’intestazione `Content-Security-Policy`. Il valore da fornire per i tag varia a seconda del tipo di hosting utilizzato.

### Hosting autonomo

Se utilizzi l’[hosting autonomo](../publishing/hosts/self-hosting-libraries.md) per la libreria, la sorgente della build sarà probabilmente il dominio di tua proprietà. Puoi specificare che il dominio host è una sorgente affidabile utilizzando la seguente configurazione:

**Intestazione HTTP**

```http
Content-Security-Policy: script-src 'self'
```

**Tag HTML `<meta>`**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Hosting gestito da Adobe

Se utilizzi un [hosting gestito da Adobe](../publishing/hosts/managed-by-adobe-host.md), la build viene mantenuta su `assets.adobedtm.com`. È necessario specificare `self` come dominio sicuro in modo da non interrompere gli script già in fase di caricamento, ma è anche necessario elencare `assets.adobedtm.com` come attendibile, altrimenti la libreria di tag non verrà caricata sulla pagina. In questo caso, utilizza la configurazione seguente:

**Intestazione HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**Tag HTML `<meta>`**


Esiste un prerequisito molto importante: Devi caricare la libreria di tag [in modo asincrono](https://experienceleague.adobe.com/docs/launch/using/reference/client-side-info/asynchronous-deployment.html?lang=it). Questo non funziona con un caricamento sincrono della libreria di tag (il che si traduce in errori della console e regole non eseguite correttamente).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

Occorre specificare `self` come dominio sicuro in modo che eventuali script già in fase di caricamento continuino a funzionare, ma occorre inoltre indicare `assets.adobedtm.com` come sicuro, altrimenti la build della libreria non verrà caricata sulla pagina.

## Script in linea

I CSP disattivano gli script in linea per impostazione predefinita e devono pertanto essere configurati manualmente per consentirli. Sono disponibili due opzioni per consentire gli script in linea:

* [Consenti per nonce](#nonce) (sicurezza maggiore)
* [Consenti tutti gli script in linea](#unsafe-inline) (sicurezza minore)

>[!NOTE]
>
>La specifica CSP contiene dettagli per una terza opzione che utilizza gli hash, ma questo approccio non è compatibile con i sistemi di gestione dei tag come i tag. Per ulteriori informazioni sulle limitazioni dell’utilizzo di hash con tag in Platform, consulta la guida [Integrità della sottorisorsa (SRI)](./sri.md).

### Consentire per nonce {#nonce}

Questo metodo comporta la generazione di un nonce di crittografia e l’aggiunta di quest’ultimo ai CSP e a ogni script in linea sul sito. Quando il browser riceve l’istruzione di caricare uno script in linea che contiene un nonce, esso confronta il valore del nonce con il contenuto dell’intestazione dei CSP. Se corrisponde, lo script è caricato. Questo nonce deve essere modificato con ogni nuovo caricamento di pagina.

>[!IMPORTANT]
>
>Per utilizzare questo metodo, è necessario caricare la build in modo asincrono. Caricare la build in modo sincrono causerebbe infatti errori della console e l’esecuzione scorretta delle regole. Per ulteriori informazioni, consulta la guida sulla [distribuzione asincrona](./asynchronous-deployment.md).

Gli esempi seguenti mostrano come aggiungere il nonce alla configurazione CSP per un host gestito da Adobe. Se utilizzi l’hosting autonomo, puoi escludere `assets.adobedtm.com`.

**Intestazione HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**Tag HTML `<meta>`**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Una volta configurati l’intestazione o il tag HTML, è necessario indicare al tag dove trovare il nonce quando si carica uno script in linea. Affinché un tag utilizzi il nonce durante il caricamento dello script, è necessario:

1. Crea un elemento dati che faccia riferimento alla posizione del nonce all’interno del livello dati.
1. Configura l’Estensione core e specifica l’elemento dati utilizzato.
1. Pubblica il tuo elemento dati e le modifiche all’Estensione core.

>[!NOTE]
>
>Il processo sopracitato gestisce solo il caricamento del codice personalizzato, non ciò che il codice personalizzato fa. Se uno script in linea contiene codice personalizzato non conforme ai CSP, questi ultimi hanno la precedenza. Ad esempio, se utilizzi un codice personalizzato per caricare uno script in linea aggiungendolo al DOM, il tag non può aggiungere il nonce correttamente, pertanto l’azione del codice personalizzato non funzionerà come previsto.

### Consentire tutti gli script in linea {#unsafe-inline}

In caso tu non possa utilizzare i nonce, puoi configurare i CSP in modo che consentano tutti gli script in linea. Si tratta dell’opzione meno sicura, ma è più facile da implementare e mantenere.

Gli esempi seguenti mostrano come consentire tutti gli script in linea nell’intestazione CSP.

#### Hosting autonomo

Imposta le seguenti configurazioni se utilizzi l’hosting autonomo:

**Intestazione HTTP**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**Tag HTML `<meta>`**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Hosting gestito da Adobe

Imposta le seguenti configurazioni se utilizzi un hosting gestito da Adobe:

**Intestazione HTTP**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**Tag HTML `<meta>`**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Passaggi successivi

Leggendo questo documento, sarai in grado di configurare l’intestazione CSP per accettare il file della libreria di tag e gli script in linea.

Come ulteriore misura di sicurezza, puoi scegliere inoltre di utilizzare l’integrità della sottorisorsa (SRI) per convalidare le build della libreria recuperate. Tuttavia, questa funzione presenta alcune limitazioni importanti se utilizzata con sistemi di gestione dei tag come i tag. Per ulteriori informazioni, consulta la guida sulla [compatibilità SRI in Platform](./sri.md) .
