---
title: Gestione degli errori
description: Scopri come vengono gestiti gli errori nell’API di Reactor.
exl-id: 336c0ced-1067-4519-94e1-85aea700fce6
source-git-commit: f3c23665229a83d6c63c7d6026ebf463069d8ad9
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 99%

---

# Gestione degli errori

Quando si verifica un problema durante una chiamata all’API di Reactor, può essere restituito un errore in uno dei seguenti modi:

* **Errori immediati**: quando si esegue una richiesta che genera un errore immediato, l’API restituisce una risposta di errore, con lo stato HTTP che riflette il tipo generale di errore che si è verificato.
* **Errori ritardati**: quando si esegue una richiesta API che causa un errore ritardato (ad esempio un’attività asincrona), l’API potrebbe restituire un errore in `meta.status_details` di una risorsa correlata.

## Formato degli errori

Le risposte di errore mirano a conformarsi alle [specifiche degli errori JSON:API](http://jsonapi.org/format/#errors) e in genere si attengono alla seguente struttura:

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
| `status` | Codice di stato HTTP applicabile a questo problema, espresso come valore stringa. |
| `code` | Codice di errore specifico per l’applicazione, espresso come valore stringa. |
| `title` | Riepilogo breve e leggibile del problema, che **non deve cambiare** da occorrenza a occorrenza, a meno che non sia a scopo di localizzazione. |
| `detail` | Spiegazione leggibile specifica per questa occorrenza del problema. Come `title`, il valore di questo campo può essere localizzato. |
| `source` | Oggetto contenente riferimenti all’origine dell’errore, facoltativamente con uno o più dei seguenti membri:<ul><li>`pointer`: una stringa [JSON Pointer (RFC6901)](https://datatracker.ietf.org/doc/html/rfc6901) che fa riferimento all’entità associata nel documento della richiesta (ad esempio `/data` per un oggetto dati principale o `/data/attributes/title` per un attributo specifico).</li></ul> |
| `meta` | Oggetto contenente metadati non standard sull’errore. |

{style="table-layout:auto"}

## Descrizione degli errori

Nella tabella seguente sono elencati i diversi errori che l’API può restituire.

| Titolo dell’errore | Descrizione |
| --- | --- |
| `authentication-failure` | Il token di accesso IMS non è valido. Per ottenere un nuovo token di accesso, accedi nuovamente. Oppure per gli account tecnici, genera di un nuovo JWT e scambialo per un token di accesso IMS. |
| `connection-refused` | Impossibile stabilire una connessione al server. |
| `decrypt-bad-passphrase` | Impossibile decrittografare i dati con la passphrase fornita. |
| `decrypt-failed` | Impossibile decrittografare i dati con la chiave privata fornita. Assicurati che la chiave funzioni localmente e che non contenga spazi vuoti. |
| `decrypt-no-data` | I dati non possono essere decrittografati senza una chiave privata. Fornisci una chiave privata crittografata. |
| `delegate-descriptor-unresolved` | L’estensione non ha fornito la definizione prevista di questo descrittore di delegato. Potrebbe essere necessario aggiornare l’estensione. |
| `deleted-resources` | Le risorse che stai tentando di aggiungere alla libreria sono state eliminate. |
| `environment-in-use` | A ogni ambiente può essere assegnata una sola libreria alla volta. L’opzione 1 consiste nel scegliere un ambiente diverso. L’opzione 2 consiste nel liberare l’ambiente spostando la libreria in un altro ambiente o eliminandola. |
| `environment-required` | Prima di poter creare una build, deve essere assegnato un ambiente alla libreria. |
| `extension-not-found` | L’estensione che definisce un elemento dati o un componente regola non è inclusa nella libreria. Verifica che tutte le estensioni richieste siano state aggiunte alla libreria. |
| `extension-package-path-error` | Un percorso definito in extension.json non è stato costruito correttamente. |
| `extension-package-transform-definition-error` | È stata definita una trasformazione non valida per una proprietà oggetto. Ogni proprietà oggetto può avere una trasformazione definita, che deve essere di tipo di file o funzione. |
| `extension-package-zip-error` | Errore durante la decompressione di ExtensionPackage o la creazione dell’archivio zip dei file per la distribuzione. |
| `host-in-use` | Un host non può essere eliminato se uno o più ambienti lo utilizzano. |
| `host-required` | L’ambiente assegnato a questa libreria non dispone di un host valido. Controlla quale ambiente è assegnato alla libreria. Quindi assegna un host valido a tale ambiente. |
| `host-type-error` | Solo gli host SFTP richiedono la verifica delle credenziali prima di poter essere utilizzati, quindi il pre-test è disponibile solo per quel tipo di host. |
| `illegal-custom-code-transform` | Non è consentito utilizzare la trasformazione customCode. Specifica una trasformazione di tipo funzione o file. |
| `ims-not-authorized` | Errore sconosciuto durante l’autorizzazione dell’account. Riprova più tardi. |
| `ims-session-error` | Si è verificato un problema con la sessione di accesso. Esci e accedi di nuovo. |
| `internal-error` | Errore interno. Attendi alcuni minuti e riprova. Se il problema persiste, contatta l’Assistenza clienti. |
| `invalid-data_element` | Non è possibile aggiungere un elemento dati non valido a una libreria. |
| `invalid-embed_code` | Il codice di incorporamento non è valido oppure si sta tentando di collegarlo a un ambiente di sviluppo o di staging. I codici di incorporamento Dynamic Tag Management (DTM) possono essere collegati solo agli ambienti di produzione. |
| `invalid-extension` | Non è possibile aggiungere un’estensione non valida a una libreria. |
| `invalid-extension_package_id` | Puoi modificare solo alcune proprietà dell’oggetto di un pacchetto di estensione. Hai provato a modificare uno di quelli non consentiti. |
| `invalid-new-owner-org-id` | L’ID organizzazione che hai tentato di assegnare non è un ID organizzazione valido. |
| `invalid-org` | La tua organizzazione attiva non ha accesso all’API. Verifica di utilizzare l’organizzazione corretta. |
| `invalid-rule` | Impossibile aggiungere una regola non valida a una libreria. |
| `invalid-settings-syntax` | Errore di sintassi durante l’analisi delle impostazioni JSON. |
| `library-file-not-found` | Impossibile trovare un file necessario definito in extension.json all’interno del pacchetto zip. |
| `minification-error` | Impossibile compilare il codice. Codice non valido. |
| `multiple-revisions` | È possibile includere in una libreria una sola revisione di ogni risorsa. |
| `no-available-orgs` | Questo account utente non appartiene a un profilo di prodotto con accesso ai tag. Utilizza Admin Console per aggiungere questo utente a un profilo di prodotto con diritti di tag. |
| `not-authorized` | Questo account utente non dispone delle autorizzazioni necessarie per eseguire questa azione. |
| `not-found` | Impossibile trovare il record. Verifica l’ID dell’oggetto che stai tentando di recuperare. |
| `not-unique` | Il nome che stai cercando di utilizzare è già in uso. Per questa risorsa, la proprietà “name” deve essere univoca. |
| `public-release-not-authorized` | La versione pubblica delle estensioni è coordinata da `launch-ext-dev@adobe.com`. Per ulteriori informazioni, consulta il documento sul [rilascio di estensioni](../../extension-dev/submit/release.md). |
| `read-only` | La risorsa è di sola lettura e non può essere modificata. |
| `session-timeout` | La sessione utente è scaduta. Esci e accedi di nuovo. |
| `sftp-authentication-failed` | Autenticazione non riuscita per la connessione SFTP. |
| `sftp-connection-timeout` | Timeout della connessione SFTP. |
| `sftp-exception` | Eccezione durante l’utilizzo di SFTP per la connessione al server. |
| `sftp-status-exception` | Eccezione SFTP durante il tentativo di comunicazione con il server. |
| `socket-error` | Errore del socket durante il tentativo di comunicazione con il server. |
| `ssh-disconnect` | La sessione SSH è stata disconnessa. |
| `timeout-error` | Timeout della connessione con il server. |
| `unknown-error` | Errore imprevisto. Riprova più tardi oppure chiama l’Assistenza clienti e spiega cosa stavi facendo quando si è verificato l’errore. |
| `unsupported-custom-code-language` | È stato fornito un linguaggio di codice personalizzato non supportato. |
| `upgraded-extension-required` | Dopo aver installato un aggiornamento dell’estensione, devi includerlo in tutte le librerie fino a quando l’aggiornamento non arriva a Produzione. L’unica eccezione è se l’estensione non è ancora stata pubblicata. |
| `upstream-build-required` | È necessaria una build corretta per la libreria a monte prima di poterla generare. |

{style="table-layout:auto"}
