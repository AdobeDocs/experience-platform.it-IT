---
title: Gestione degli errori
description: Scopri come vengono gestiti gli errori nell’API di Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# Gestione degli errori

Quando si verifica un problema durante una chiamata all&#39;API Reactor, può essere restituito un errore in uno dei seguenti modi:

* **Errori** immediati: Quando si esegue una richiesta che genera un errore immediato, l’API restituisce una risposta di errore, con lo stato HTTP che riflette il tipo generale di errore che si è verificato.
* **Errori** ritardati: Quando si esegue una richiesta API che causa un errore ritardato (ad esempio un’attività asincrona), l’API potrebbe restituire un errore in  `meta.status_details` una risorsa correlata.

## Formato errore

Le risposte di errore mirano a conformarsi alla [JSON:API errors Specification](http://jsonapi.org/format/#errors) e in genere si attengono alla seguente struttura:

```json
{
  "errors": [
    {
      "id": "8a5526da-ab12-4be9-b084-2efe537f388c",
      "status": "404",
      "code": "not-found",
      "title": "Record Not Found",
      "meta": {
        "request_id": "jfb0dQ2e0XVTkQ6AOfEJFfTDjguw9x3d"
      },
      "source": {
        "pointer": "/data"
      }
    }
  ]
}
```

| Proprietà | Descrizione |
| --- | --- |
| `id` | Identificatore univoco per questa particolare occorrenza del problema. |
| `status` | Il codice di stato HTTP applicabile a questo problema, espresso come valore stringa. |
| `code` | Un codice di errore specifico per l&#39;applicazione, espresso come valore stringa. |
| `title` | Riepilogo breve e leggibile del problema che **non deve cambiare** dall&#39;occorrenza all&#39;occorrenza, a meno che non sia a scopo di localizzazione. |
| `detail` | Una spiegazione leggibile dall&#39;uomo specifica di questo evento del problema. Come `title`, il valore di questo campo può essere localizzato. |
| `source` | Un oggetto contenente riferimenti all&#39;origine dell&#39;errore, includendo facoltativamente uno dei seguenti membri:<ul><li>`pointer`: una stringa  [JSON Pointer (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) che fa riferimento all&#39;entità associata nel documento della richiesta (ad esempio  `/data` per un oggetto dati principale o  `/data/attributes/title` per un attributo specifico).</li></ul> |
| `meta` | Un oggetto contenente metadati non standard sull&#39;errore. |

{style=&quot;table-layout:auto&quot;}

## Riferimento errore

Nella tabella seguente sono elencati i diversi errori che l’API può restituire.

| Titolo errore | Descrizione |
| --- | --- |
| `authentication-failure` | Il token di accesso IMS non è valido. Puoi ottenere un nuovo token di accesso accedendo nuovamente. Oppure per gli account tecnici, generazione di un nuovo JWT e scambio di un token di accesso IMS. |
| `connection-refused` | Impossibile stabilire una connessione al server. |
| `decrypt-bad-passphrase` | Impossibile decrittografare i dati con la passphrase fornita. |
| `decrypt-failed` | Impossibile decrittografare i dati con la chiave privata fornita. Assicurati che la chiave funzioni localmente e che lo spazio vuoto sia stato tagliato. |
| `decrypt-no-data` | I dati non possono essere decrittografati senza una chiave privata. Fornire una chiave privata crittografata. |
| `delegate-descriptor-unresolved` | L&#39;estensione non forniva la definizione prevista di questo descrittore delegato. Potrebbe essere necessario aggiornare l’estensione. |
| `deleted-resources` | Le risorse che stai tentando di aggiungere alla libreria sono state eliminate. |
| `environment-in-use` | Un ambiente può essere assegnato a una sola libreria alla volta. L&#39;opzione 1 consiste nel scegliere un ambiente diverso. L&#39;opzione 2 consiste nel liberare l&#39;ambiente spostando la libreria in un altro ambiente o eliminando la libreria. |
| `environment-required` | Prima di poter creare una build, alla libreria deve essere assegnato un ambiente . |
| `extension-not-found` | L&#39;estensione che definisce un elemento dati o un componente regola non è inclusa nella libreria. Verifica che tutte le estensioni richieste siano state aggiunte alla libreria. |
| `extension-package-path-error` | Un percorso definito in extension.json non è stato costruito correttamente. |
| `extension-package-transform-definition-error` | È stata definita una trasformazione non valida per una proprietà oggetto. Ogni proprietà dell&#39;oggetto può avere una trasformazione definita e deve essere una trasformazione di file o una trasformazione di funzione. |
| `extension-package-zip-error` | Errore durante la decompressione di ExtensionPackage o lo zip dei file per la distribuzione. |
| `host-in-use` | Un host non può essere eliminato se uno o più ambienti lo utilizzano. |
| `host-required` | L&#39;ambiente assegnato a questa libreria non dispone di un host valido. Controlla quale ambiente è assegnato alla libreria. Quindi assegna un host valido a tale ambiente. |
| `host-type-error` | Solo gli host SFTP devono aver verificato le credenziali prima di poter essere utilizzati, quindi il test è disponibile solo per quel tipo di host. |
| `illegal-custom-code-transform` | Non è consentito utilizzare la trasformazione customCode. Specificare una funzione o una trasformazione file. |
| `ims-not-authorized` | Errore sconosciuto durante l&#39;autorizzazione dell&#39;account. Riprova più tardi. |
| `ims-session-error` | Si è verificato un problema con la sessione di accesso. Disconnettiti e accedi di nuovo. |
| `internal-error` | Errore interno. Attendere alcuni minuti e riprovare. Se il problema persiste, contatta l’Assistenza clienti. |
| `invalid-data_element` | Impossibile aggiungere un elemento dati non valido a una libreria. |
| `invalid-embed_code` | Codice di incorporamento non valido oppure si sta tentando di collegarlo a un ambiente di sviluppo o di staging. I codici di incorporamento Dynamic Tag Management (DTM) possono essere collegati solo agli ambienti di produzione. |
| `invalid-extension` | Impossibile aggiungere un&#39;estensione non valida a una libreria. |
| `invalid-extension_package_id` | Puoi modificare solo alcune proprietà dell’oggetto di un pacchetto di estensione. Hai provato a modificare uno di quelli non consentiti. |
| `invalid-new-owner-org-id` | L&#39;ID organizzazione che si è tentato di assegnare non è un ID organizzazione valido. |
| `invalid-org` | La tua organizzazione attiva non ha accesso all&#39;API. Verifica di utilizzare l&#39;organizzazione corretta. |
| `invalid-rule` | Impossibile aggiungere una regola non valida a una libreria. |
| `invalid-settings-syntax` | Errore di sintassi durante l&#39;analisi delle impostazioni JSON. |
| `library-file-not-found` | Impossibile trovare un file necessario definito in extension.json all&#39;interno del pacchetto zip. |
| `minification-error` | Impossibile compilare il codice a causa di codice non valido o codice ES6. |
| `multiple-revisions` | È possibile includere in una libreria una sola revisione di ogni risorsa. |
| `no-available-orgs` | Questo account utente non appartiene a un profilo di prodotto con accesso ai tag. Utilizza l’Admin Console per aggiungere questo utente a un profilo di prodotto con diritti di tag. |
| `not-authorized` | Questo account utente non dispone delle autorizzazioni necessarie per eseguire questa azione. |
| `not-found` | Impossibile trovare il record. Verifica l&#39;id dell&#39;oggetto che stai tentando di recuperare. |
| `not-unique` | Il nome che stai cercando di utilizzare è già in uso. Per questa risorsa, la proprietà &#39;name&#39; deve essere univoca. |
| `public-release-not-authorized` | La versione pubblica delle estensioni è coordinata da `launch-ext-dev@adobe.com`. Per ulteriori informazioni, consulta il documento sul rilascio di estensioni](../../extension-dev/submit/release.md) .[ |
| `read-only` | Questa risorsa è di sola lettura e non può essere modificata. |
| `session-timeout` | La sessione utente è scaduta. Disconnettiti e accedi di nuovo. |
| `sftp-authentication-failed` | Autenticazione non riuscita per la connessione SFTP. |
| `sftp-connection-timeout` | Timeout della connessione SFTP. |
| `sftp-exception` | Eccezione durante l&#39;utilizzo di SFTP per la connessione al server. |
| `sftp-status-exception` | Eccezione SFTP durante il tentativo di comunicazione con il server. |
| `socket-error` | Errore del socket durante il tentativo di comunicazione con il server. |
| `ssh-disconnect` | La sessione SSH è stata disconnessa. |
| `timeout-error` | Timeout della connessione con il server. |
| `unknown-error` | Errore imprevisto. Puoi riprovare più tardi o chiamare l’Assistenza clienti per spiegare cosa stavi facendo quando è successo. |
| `unsupported-custom-code-language` | È stata fornita una lingua del codice personalizzata non supportata. |
| `upgraded-extension-required` | Dopo aver installato un aggiornamento dell’estensione, devi includerlo in tutte le librerie fino a quando l’aggiornamento non arriva a Produzione. L&#39;unica eccezione è se l&#39;estensione non è ancora stata pubblicata. |
| `upstream-build-required` | È necessaria una build corretta per la libreria a monte prima di poter generare questa. |

{style=&quot;table-layout:auto&quot;}
