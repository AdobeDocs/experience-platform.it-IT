---
title: cookie
description: Scrivi, modifica o elimina manualmente i cookie per la proprietà tag.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

L&#39;oggetto `_satellite.cookie` contiene metodi che consentono di scrivere, modificare o eliminare cookie a cui possono fare riferimento le regole dei tag. Si tratta di una copia parziale di [`js-cookie`](https://github.com/js-cookie/js-cookie), contenente molte caratteristiche principali della libreria.

## `cookie.set()`

Il metodo `set()` scrive un cookie a cui può fare riferimento la proprietà tag.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

Sono disponibili i seguenti parametri di metodo:

| Nome | Tipo | Obbligatorio | Descrizione |
|---|---|---|---|
| **`name`** | `string` | Sì | Nome del cookie. |
| **`value`** | `string` | Sì | Valore del cookie |
| **`attributes`** | `object` | No | Attributi aggiuntivi che desideri che il cookie abbia. |

L&#39;oggetto `attributes` supporta le proprietà seguenti:

| Nome attributo | Tipo | Obbligatorio | Predefinito | Descrizione |
|---|---|---|---|---|
| **`expires`** | `number` o [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | No | Il cookie scade al termine della sessione del browser | Il numero di giorni desiderati per la scadenza del cookie. |
| **`path`** | `string` | No | Cookie visibile a livello di sito | Dove nel dominio è visibile il cookie. |
| **`domain`** | `string` | No | Cookie visibile al dominio in cui è stato creato | Un dominio valido (con o senza un sottodominio) in cui il cookie è visibile. Se un dominio è incluso senza un sottodominio, il cookie è visibile a tutti i sottodomini all’interno di tale dominio. |
| **`secure`** | `boolean` | No | Nessun attributo impostato | Determina se il cookie richiede un protocollo protetto (`https://`). Se omesso, non esiste alcun requisito di protocollo sicuro. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | No | Nessun attributo impostato | Consente di impostare l&#39;attributo [`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) di un cookie. Se si imposta `sameSite` su `None`, è necessario impostare `secure` anche su `true`. |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

Richiamando questo metodo, viene scritto il cookie desiderato e viene restituita la stringa del cookie serializzato scritta. Questa stringa viene utilizzata principalmente a scopo di debug o registrazione.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>Le versioni precedenti dell&#39;oggetto tag utilizzavano `_satellite.setCookie()`. Il metodo `setCookie()` è obsoleto a favore di `_satellite.cookie.set()`.

## `cookie.get()`

Il metodo `get()` restituisce un valore cookie.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| Nome | Tipo | Obbligatorio | Descrizione |
|---|---|---|---|
| **`name`** | `string` | Sì | Il nome del cookie da cui desideri recuperare il valore (distinzione maiuscole/minuscole). |

Se il nome del cookie esiste, restituisce il valore del cookie. Se il nome del cookie non esiste, restituisce `undefined`.

>[!TIP]
>
>Le versioni precedenti dell&#39;oggetto tag utilizzavano `_satellite.getCookie()`. Il metodo `getCookie()` è obsoleto a favore di `_satellite.cookie.get()`.

## `cookie.remove()`

Il metodo `remove()` elimina un cookie impostato dall&#39;utente.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| Nome | Tipo | Obbligatorio | Descrizione |
|---|---|---|---|
| **`name`** | `string` | Sì | Il nome del cookie che desideri rimuovere. |
| **`attributes`** | `object` | No | Attributi associati al cookie che desideri rimuovere. Se imposti un cookie utilizzando gli attributi `path` o `domain`, includi gli stessi attributi durante la rimozione del cookie. Se questi attributi non vengono inclusi, il cookie non viene rimosso. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>Le versioni precedenti dell&#39;oggetto tag utilizzavano `_satellite.removeCookie()`. Il metodo `removeCookie()` è obsoleto a favore di `_satellite.cookie.remove()`.
