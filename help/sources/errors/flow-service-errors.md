---
title: Messaggi di errore del servizio Flusso
description: Scopri i messaggi di errore che possono verificarsi quando utilizzi il servizio Flusso per le origini.
exl-id: af79c547-25d0-459a-8de7-eb14206a8694
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Messaggi di errore del servizio Flusso

Il Servizio Flusso viene utilizzato per raccogliere e centralizzare i dati dei clienti da diverse origini all’interno di Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consentono di impostare facilmente le connessioni sorgente a vari provider di dati. Queste connessioni di origine ti consentono di autenticare i sistemi di terze parti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

Questo documento fornisce un catalogo di messaggi di errore, descrizioni e risoluzioni consigliate relativi al servizio Flow.

## Errori di convalida interna nel servizio Flow

La tabella seguente illustra gli errori relativi alla convalida interna in Flow Service.

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1100-400` | Richiesta non valida | Impossibile elaborare la richiesta. Errore dal provider di flussi: non autorizzato a questa operazione. |
| `1101-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. Errore dal provider di flusso: la risorsa con l&#39;ID specificato non esiste. |
| `1102-500` | Errore interno | Errore interno. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1103-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1104-504` | Timeout del gateway | Timeout del gateway. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1400-500` | Errore interno | Errore interno. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1401-400` | Richiesta non valida | I parametri di limite e conteggio non possono essere forniti insieme nella stessa richiesta. Specifica solo il limite o il parametro del conteggio e riprova. |
| `1402-400` | Richiesta non valida | L&#39;azione &#39;finalize&#39; è supportata solo per le richieste di provider. |
| `1403-400` | Intestazione mancante | Intestazione &quot;If-Match&quot; mancante nella richiesta. Specifica l’intestazione e riprova. |
| `1404-412` | Versione non corrispondente | La versione specificata &#39;v1&#39; non corrisponde alla versione corrente sull&#39;entità &#39;cc01fc2c-0000-0200&#39;. Verifica che la versione fornita corrisponda alla versione corrente sull’entità e riprova. |
| `1405-400` | Richiesta non valida | Il corpo della richiesta non può essere null o vuoto. Specifica un corpo della richiesta e riprova. |
| `1406-400` | Richiesta non valida | Impossibile applicare l&#39;operazione secondaria &#39;progress&#39; ad altre operazioni secondarie. Aggiorna l’elenco delle operazioni secondarie e riprova. |
| `1407-400` | Richiesta non valida | Impossibile utilizzare lo stato non riuscito con `progress` subOp. Rimuovi il `progress` subOppure usa status=&#39;inProgress&#39; e riprova. |
| `1408-400` | Richiesta non valida | La percentuale di completamento deve essere 100 per gli stati completato o non riuscito. Aggiorna la percentuale di completamento e riprova. |
| `1409-400` | Richiesta non valida | Impossibile applicare l&#39;operazione &#39;finalize&#39; allo stato corrente enabled-finalizing. Aggiorna l’operazione e riprova. |
| `1410-400` | Richiesta non valida | `State` non è consentito nella richiesta di creazione del flusso. |
| `1411-400` | Richiesta non valida | Impossibile recuperare entityId. Richiesta non valida ricevuta con il percorso &#39;baseConnections/123&#39;. |
| `1412-400` | Richiesta non valida | Versione di mappatura non valida nella richiesta. Fornisci la versione di mappatura corretta. |
| `1413-400` | Richiesta non valida | L&#39;ID della specifica fornito non è valido. Specifica un ID di specifica valido e riprova. |
| `1414-400` | Richiesta non valida | Impossibile aggiornare la specifica di connessione di una connessione. |
| `1415-400` | Richiesta non valida | Impossibile trovare la specifica di autenticazione &#39;authConnection&#39; per l&#39;ID della specifica di connessione ba6e206f-f233-ab16. |
| `1416-400` | Richiesta non valida | È possibile applicare Elimina o Aggiorna solo in caso di connessione con stato abilitato, disabilitato o di inizializzazione. |
| `1417-400` | Richiesta non valida | Eliminare o aggiornare le connessioni in `initializing` non sono consentiti con UserToken. |
| `1418-400` | Richiesta non valida | Impossibile eliminare la connessione di base con ID 35dcaad3-122a-4278 perché la connessione di base è utilizzata in uno o più flussi. Prima di eliminare una connessione di base, assicurati che i flussi corrispondenti vengano eliminati. |
| `1419-400` | Richiesta non valida | Errore durante la convalida della mappatura con ID 45d90285d2d249acb87a72a2f12f7401, versione 0. Ciò potrebbe essere dovuto a autorizzazioni inadeguate sui campi mappati. Controlla la mappatura o contatta l’amministratore. |
| `1420-400` | Richiesta non valida | Impossibile aggiornare la disabilitazione dello stato corrente. |
| `1421-400` | Richiesta non valida | Impossibile eseguire la transizione dell&#39;aggiornamento dello stato corrente. |
| `1422-400` | Richiesta non valida | Impossibile applicare la disattivazione azione allo stato corrente {state}. Aggiorna l’azione e riprova. |
| `1423-400` | Richiesta non valida | In ConnectionSpecFiltering è stato fornito un campo baseSpec non gestito. Aggiorna il campo {field} e riprova. |
| `1424-400` | Richiesta non valida | OrderBy non è supportato con query sandbox incrociate. |
| `1425-400` | Richiesta non valida | Errore durante la corrispondenza dello schema nel set di dati di destinazione 64ef1a3c0ef con lo schema nella mappatura 91ac5a2c0eb. Lo schema con lo stesso ID e la stessa versione deve essere utilizzato sia nel set di dati di mappatura che in quello di destinazione. |
| `1426-400` | Richiesta non valida | Il token utente non è autorizzato a creare/aggiornare la specifica di connessione. Verifica che il token utente sia autorizzato e riprova. |
| `1427-400` | Richiesta non valida | Il token utente non è autorizzato a creare/aggiornare esecuzioni del flusso. Verifica che il token utente sia autorizzato e riprova. |
| `1428-400` | Richiesta non valida | Esecuzione del flusso del predecessore non trovata con id aa6a206f-f233-4c2d. |
| `1429-400` | Richiesta non valida | Flusso del predecessore non trovato con id aa6a206f-f233-4c2d. |
| `1430-400` | Richiesta non valida | Flusso non trovato con id aa6a206f-f233-4c2d. |
| `1431-400` | Richiesta non valida | La matrice vuota &#39;fields&#39; non è consentita nel criterio. |
| `1432-400` | Richiesta non valida | Il tipo di ordinamento specificato non è corretto, anteporre + per ordine crescente e - per ordine decrescente in fieldName. |
| `1433-400` | Richiesta non valida | Campo errato= #id passato in orderBy, ad esempio +name, -name, name. |
| `1434-400` | Richiesta non valida | Operazione &#39;move&#39; non supportata ricevuta. Utilizza uno dei tipi di operazione supportati e riprova. |
| `1435-400` | Richiesta non valida | Ricevuta azione secondaria &#39;reverse&#39; non supportata. Utilizza uno dei tipi di azioni secondarie supportati e riprova. |
| `1436-400` | Richiesta non valida | Stato operazione secondaria non supportato ricevuto per l&#39;abilitazione dell&#39;operazione. |
| `1437-400` | Richiesta non valida | Ricevuto valore di stato non supportato &#39;started&#39;. Aggiorna il valore dello stato e riprova. |
| `1438-400` | Richiesta non valida | Ricevuta operazione di aggregazione &#39;average&#39; non supportata. |
| `1439-400` | Risorsa non trovata | Impossibile trovare la risorsa dei flussi richiesta 3f4ae131-b384-4e73. Verifica l’ID risorsa prima di riprovare. |
| `1440-400` | Richiesta non valida | Operatore &#39;~&#39; non implementato. |
| `1441-400` | Richiesta non valida | Funzione di aggregazione &#39;average&#39; non implementata. |
| `1442-400` | Richiesta non valida | Aggregazione non consentita per l’ID campo. |
| `1443-400` | Richiesta non valida | Operatore &#39;&lt;=&#39; non consentito per più valori. |
| `1444-400` | Richiesta non valida | Il flusso 3f4ae131-b384-4e73 non è nello stato previsto in sospeso. |
| `1445-400` | Richiesta non valida | Funzione di connessione PATCH non abilitata. |
| `1446-400` | Richiesta non valida | L&#39;ID di flusso non può essere nullo o vuoto. Aggiorna l’ID flusso e riprova. |
| `1447-400` | Richiesta non valida | Trovati flussi attivi contenenti id aa6a206f-f233-4c2d. |
| `1448-400` | Richiesta non valida | Operatore >= non supportato per l’ID campo. |
| `1449-400` | Richiesta non valida | Connessioni di campi non valide nei parametri del filtro. |
| `1450-400` | Richiesta non valida | Operatore non valido.> nei parametri dei filtri. |
| `1451-400` | Richiesta non valida | Parametri testParam non validi forniti nei parametri di query. |
| `1452-400` | Richiesta non valida | Valore non valido 1676643256,1676643210 per il campo createdAt. |
| `1453-400` | Richiesta non valida | Valore di query createdAt== non valido fornito nel parametro di query. |
| `1454-400` | Richiesta non valida | È stato fornito un tipo di valore di filtro non gestito. |
| `1455-400` | Richiesta non valida | Si è verificato un errore durante la convalida delle istruzioni di patch: campo &quot;keyWhatDoesNotExist&quot; mancante. |
| `1456-400` | Richiesta non valida | Eliminazione-finalizzazione stato non è un valore valido. I valori consentiti sono [abilitato, disabilitato, inizializzazione]. |
| `1457-400` | Richiesta non valida | Impossibile applicare l&#39;aggiornamento dell&#39;operazione in fase di eliminazione-finalizzazione dello stato. |
| `1458-400` | Richiesta non valida | Impossibile applicare l&#39;operazione di eliminazione allo stato di eliminazione-finalizzazione. |

{style="table-layout:auto"}


## Errori di verifica del token utente per l’autorizzazione

La tabella seguente illustra gli errori relativi alla verifica del token utente per l’autorizzazione

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `2000-401` | Token di autorizzazione non valido | Il token di autorizzazione non ha accesso a questa organizzazione oppure l’organizzazione non esiste. Assicurati che l’organizzazione esista o contatta l’amministratore per ottenere l’accesso. |
| `2001-401` | Intestazione mancante o vuota | L’intestazione x-gw-ims-org-id è mancante o vuota. Aggiorna il valore dell’intestazione e riprova. |
| `2002-401` | Intestazione mancante | L’intestazione x-gw-ims-org-id non è presente nella richiesta. Aggiorna il valore dell’intestazione e riprova. |
| `2100-404` | Sandbox non trovata | Impossibile trovare la sandbox denominata &#39;dev&#39;. Verifica che il nome della sandbox sia corretto e riprova. |
| `2101-404` | Sandbox non trovata | Impossibile trovare la sandbox denominata &#39;dev&#39;. Errore dall’API di gestione sandbox: sandbox con nome &quot;dev&quot; non presente. Verifica se la risorsa esiste. |
| `2102-500` | Errore nell’ottenere la sandbox per nome | Si è verificato un problema durante il recupero di una sandbox denominata &#39;dev&#39;. Errore dall’API di gestione sandbox: si è verificato un errore. Riprova. |
| `2103-404` | Sandbox non trovata | Impossibile trovare la sandbox con ID 8da3ef09-b469-404a e nome dev. Verifica che i valori ID e nome sandbox siano corretti e riprova. |
| `2104-500` | Errore nell’ottenere la sandbox per identificatore | Si è verificato un problema durante il recupero di una sandbox con ID &#39;8da3ef09-b469-404a&#39; e nome &#39;dev&#39;. Errore dall’API di gestione sandbox: si è verificato un errore. Riprova. |
| `2105-400` | Intestazione mancante | Nella richiesta manca l’intestazione x-sandbox-name. Aggiungi l’intestazione nella richiesta e riprova. |
| `2106-404` | Errore nell’ottenere la sandbox predefinita | Impossibile trovare le informazioni sandbox predefinite. |
| `2107-500` | Errore nell’ottenere la sandbox predefinita | Si è verificato un problema nel recuperare una sandbox predefinita. Errore dall’API di gestione sandbox: si è verificato un errore. Riprova. |
| `2108-500` | Errore nell’ottenere le sandbox attive | Si è verificato un problema nel recuperare una sandbox attiva. Errore dall’API di gestione sandbox: si è verificato un errore. Riprova. |
| `2110-400` | Intestazioni non consentite | L’intestazione x-sandbox-id non è consentita con il token utente. Aggiorna l’intestazione e riprova. |
| `2111-403` | Intestazioni con valore limitato | L’intestazione x-sandbox-name con valore * è limitata al token utente. Aggiorna l’intestazione e il valore e riprova. |
| `2112-400` | Intestazioni con valore diverso non consentite | Le intestazioni x-sandbox-name e x-sandbox-id devono avere entrambe il valore * per le query tra sandbox. Aggiorna le intestazioni e riprova. |
| `2113-400` | Intestazioni con valore non consentito | Le intestazioni x-sandbox-id e x-sandbox-name con valore * non sono consentite per la richiesta. Aggiorna le intestazioni e riprova. |
| `2114-400` | Token vuoto | È stato fornito un token vuoto. Specifica un token e riprova. |
| `2115-400` | Token non valido | Token non valido fornito. Specifica un token valido e riprova. |
| `2116-500` | Errore interno | Si è verificato un errore interno durante la decodifica offline del token Bearer per la risoluzione dell&#39;ambito. |
| `2117-500` | Errore interno | Si è verificato un errore interno durante la verifica delle autorizzazioni per l’utente. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `2118-403` | Autorizzazione mancante | Manca la scrittura dell’autorizzazione. Contatta l’amministratore per risolvere le autorizzazioni e riprova. |
| `2119-400` | Parametro query mancante | Il contesto della richiesta non contiene il parametro di query specId richiesto. Specifica il parametro di query mancante e riprova. |
| `2120-403` | Non consentito | Autorizzazioni insufficienti per eseguire l&#39;operazione. Contatta l’amministratore per risolvere le autorizzazioni e riprova. |
| `2121-403` | Non consentito | La gestione delle autorizzazioni è negata per la risorsa Origine organizzazione. Contatta l’amministratore per risolvere le autorizzazioni e riprova. |
| `2200-500` | Errore di richiesta di un servizio esterno | Si è verificato un problema durante la chiamata al servizio Catalogo per la convalida dello schema. |
| `2250-500` | Errore di richiesta di un servizio esterno | Si è verificato un problema durante la chiamata al servizio Preparazione dati per la convalida della mappatura. |

{style="table-layout:auto"}
