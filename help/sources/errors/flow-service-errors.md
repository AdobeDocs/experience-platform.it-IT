---
title: Messaggi di errore del servizio di flusso
description: Scopri i messaggi di errore che potresti incontrare durante l’utilizzo di Flusso Service per le origini.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 1%

---

# Messaggi di errore del servizio di flusso

Flow Service viene utilizzato per raccogliere e centralizzare i dati dei clienti da varie fonti diverse all’interno di Platform. Il servizio fornisce un’interfaccia utente e un’API RESTful che consente di configurare facilmente le connessioni sorgente a vari provider di dati. Queste connessioni di origine consentono di autenticare i sistemi di terze parti, impostare i tempi di esecuzione dell’acquisizione e gestire il throughput di inserimento dei dati.

Questo documento fornisce un catalogo di messaggi di errore, descrizioni e risoluzioni consigliate relative a Flusso Service.

## Errori di convalida interna in Flow Service

Nella tabella seguente sono riportati gli errori relativi alla convalida interna in Flow Service.

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1100-400` | Richiesta non valida | Impossibile elaborare la richiesta. Errore del provider di flusso: Non ha diritto a questa operazione. |
| `1101-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. Errore del provider di flusso: La risorsa con ID specificato non esiste. |
| `1102-500` | Errore interno | Errore interno. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1103-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1104-504` | Timeout gateway | Timeout del gateway. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1400-500` | Errore interno | Errore interno. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1401-400` | Richiesta non valida | I parametri di limite e conteggio non possono essere forniti insieme nella stessa richiesta. Specificare solo il limite o il parametro di conteggio e riprovare. |
| `1402-400` | Richiesta non valida | L’azione &quot;finalize&quot; è supportata solo per le richieste del provider. |
| `1403-400` | Intestazione mancante | Intestazione &quot;If-Match&quot; mancante nella richiesta. Fornisci l&#39;intestazione e riprova. |
| `1404-412` | Versione non corrispondente | La versione fornita &#39;v1&#39; non corrisponde alla versione corrente dell&#39;entità &#39;cc01fc2c-0000-0200&#39;. Assicurati che la versione fornita corrisponda alla versione corrente nell&#39;entità e riprova. |
| `1405-400` | Richiesta non valida | Il corpo della richiesta non può essere null o vuoto. Fornire un corpo della richiesta e riprovare. |
| `1406-400` | Richiesta non valida | La sottooperazione &quot;progresso&quot; non può essere applicata ad altre sottooperazioni. Aggiornare l&#39;elenco delle operazioni secondarie e riprovare. |
| `1407-400` | Richiesta non valida | Impossibile utilizzare lo stato non riuscito con il `progress` subOp Rimuovere la `progress` subOp o utilizza status=&#39;inProgress&#39; e riprova. |
| `1408-400` | Richiesta non valida | La percentuale di completamento deve essere 100 per gli stati completati o non completati. Aggiornare la percentuale completata e riprovare. |
| `1409-400` | Richiesta non valida | Impossibile applicare l&#39;operazione &#39;finalize&#39; allo stato corrente abilitato-finalization. Aggiornare l&#39;operazione e riprovare. |
| `1410-400` | Richiesta non valida | `State` non è consentito nella richiesta di creazione del flusso. |
| `1411-400` | Richiesta non valida | Impossibile recuperare entityId. Richiesta non valida ricevuta con il percorso &#39;baseConnections/123&#39;. |
| `1412-400` | Richiesta non valida | Versione mapping non valida nella richiesta. Fornire una versione corretta della mappatura. |
| `1413-400` | Richiesta non valida | L&#39;ID di specifica fornito non è valido. Immetti un ID di specifica valido e riprova. |
| `1414-400` | Richiesta non valida | Impossibile aggiornare le specifiche di connessione di una connessione. |
| `1415-400` | Richiesta non valida | Impossibile trovare la specifica di autenticazione &#39;authConnection&#39; per la specifica di connessione ID ba6e206f-f233-ab16. |
| `1416-400` | Richiesta non valida | È possibile applicare l&#39;eliminazione o l&#39;aggiornamento solo in caso di connessione con stato abilitato, disattivato o inizializzato. |
| `1417-400` | Richiesta non valida | Elimina o aggiorna le connessioni in `initializing` lo stato non è consentito con UserToken. |
| `1418-400` | Richiesta non valida | Impossibile eliminare la connessione di base con ID 35dcaad3-122a-4278 perché la connessione di base viene utilizzata in uno o più flussi. Assicurarsi che i flussi corrispondenti vengano eliminati prima di eliminare una connessione di base. |
| `1419-400` | Richiesta non valida | Errore durante la convalida della mappatura con id 45d90285d2d249acb87a72a2f12f7401, versione 0. Ciò potrebbe essere dovuto a autorizzazioni insufficienti sui campi mappati. Controlla la mappatura o contatta l&#39;amministratore. |
| `1420-400` | Richiesta non valida | Impossibile aggiornare lo stato corrente di disabilitazione. |
| `1421-400` | Richiesta non valida | Impossibile effettuare la transizione all&#39;aggiornamento dello stato corrente. |
| `1422-400` | Richiesta non valida | Impossibile applicare la disattivazione dell&#39;azione sullo stato corrente {state}. Aggiorna l&#39;azione e riprova. |
| `1423-400` | Richiesta non valida | È stato fornito un campo baseSpec non gestito in ConnectionSpecFiltering. Aggiorna il campo {field} e riprova. |
| `1424-400` | Richiesta non valida | OrderBy non è supportato con query sandbox incrociata. |
| `1425-400` | Richiesta non valida | Errore durante la corrispondenza dello schema nel set di dati di destinazione 64ef1a3c0ef con lo schema nella mappatura 91ac5a2c0eb. Lo schema con lo stesso ID e la stessa versione deve essere utilizzato sia nel set di dati di mappatura che di destinazione. |
| `1426-400` | Richiesta non valida | Il token utente non è autorizzato a creare/aggiornare la specifica di connessione. Verifica che il token utente sia autorizzato e riprova. |
| `1427-400` | Richiesta non valida | Il token utente non è autorizzato a creare/aggiornare le esecuzioni del flusso. Verifica che il token utente sia autorizzato e riprova. |
| `1428-400` | Richiesta non valida | Esecuzione del flusso predecessore non trovata con id aa6a206f-f233-4c2d. |
| `1429-400` | Richiesta non valida | Flusso predecessore non trovato con id aa6a206f-f233-4c2d. |
| `1430-400` | Richiesta non valida | Flusso non trovato con id aa6a206f-f233-4c2d. |
| `1431-400` | Richiesta non valida | I &#39;campi&#39; della matrice vuota non sono consentiti nel criterio. |
| `1432-400` | Richiesta non valida | L&#39;ordinamento specificato non è corretto, anteporre + per l&#39;ordine crescente e - per l&#39;ordine decrescente nel campoName. |
| `1433-400` | Richiesta non valida | Campo= #id passato in orderBy, ad esempio +name, -name, name. |
| `1434-400` | Richiesta non valida | Operazione &quot;Sposta&quot; non supportata ricevuta. Utilizzare uno dei tipi di operazione supportati e riprovare. |
| `1435-400` | Richiesta non valida | Ricevuta sottoazione non supportata &quot;reverse&quot;. Utilizzare uno dei tipi di sottoazioni supportati e riprovare. |
| `1436-400` | Richiesta non valida | Attività secondaria non supportata PROGRESS ricevuta per l&#39;abilitazione dell&#39;operazione. |
| `1437-400` | Richiesta non valida | Ricevuto valore di stato non supportato &quot;avviato&quot;. Aggiornare il valore di stato e riprovare. |
| `1438-400` | Richiesta non valida | Operazione aggregata non supportata &quot;media&quot; ricevuta. |
| `1439-400` | Risorsa non trovata | Impossibile trovare la risorsa dei flussi richiesta 3f4ae131-b384-4e73. Verifica l&#39;ID risorsa prima di riprovare. |
| `1440-400` | Richiesta non valida | Operatore &#39;~&#39; non implementato. |
| `1441-400` | Richiesta non valida | Funzione di aggregazione &#39;media&#39; non implementata. |
| `1442-400` | Richiesta non valida | Aggregazione non consentita sull&#39;ID campo. |
| `1443-400` | Richiesta non valida | L&#39;operatore &#39;&lt;=&#39; non è consentito per più valori. |
| `1444-400` | Richiesta non valida | Il flusso 3f4ae131-b384-4e73 non è nello stato previsto in sospeso. |
| `1445-400` | Richiesta non valida | Funzionalità di connessione PATCH non abilitata. |
| `1446-400` | Richiesta non valida | L&#39;ID flusso non può essere null o vuoto. Aggiorna l&#39;ID di flusso e riprova. |
| `1447-400` | Richiesta non valida | Trovati flussi attivi contenenti id aa6a206f-f233-4c2d. |
| `1448-400` | Richiesta non valida | Operatore >= non supportato per l’ID campo. |
| `1449-400` | Richiesta non valida | Connessioni campo non valide nei parametri del filtro. |
| `1450-400` | Richiesta non valida | Operatore non valido.> nei parametri del filtro. |
| `1451-400` | Richiesta non valida | Parametro testParam non valido fornito nei parametri di query. |
| `1452-400` | Richiesta non valida | Valore non valido 1676643256,1676643210 per il campo creatoAt. |
| `1453-400` | Richiesta non valida | Valore query non valido creatoAt== specificato nel parametro di query. |
| `1454-400` | Richiesta non valida | È stato fornito il tipo di valore del filtro non gestito. |
| `1455-400` | Richiesta non valida | Errore durante la convalida delle istruzioni della patch: Campo mancante &quot;keyICHDoesNotExist&quot;. |
| `1456-400` | Richiesta non valida | Il termine di eliminazione dello stato non è un valore valido. I valori consentiti sono [abilitato, disabilitato, inizializzazione]. |
| `1457-400` | Richiesta non valida | Impossibile applicare l&#39;aggiornamento dell&#39;operazione nella fase di eliminazione-finalizzazione dello stato. |
| `1458-400` | Richiesta non valida | Impossibile applicare l&#39;eliminazione dell&#39;operazione durante l&#39;eliminazione dello stato. |

{style="table-layout:auto"}


## Errori di verifica del token utente per l&#39;autorizzazione

La tabella seguente illustra gli errori relativi alla verifica del token utente per l&#39;autorizzazione

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `2000-401` | Token di autorizzazione non valido | Il token di autorizzazione non ha accesso a questa organizzazione o l&#39;organizzazione non esiste. Assicurati che l&#39;organizzazione esista o contatta il tuo amministratore per ottenere l&#39;accesso. |
| `2001-401` | Intestazione mancante o vuota | L&#39;intestazione x-gw-ims-org-id è mancante o vuota. Aggiorna il valore dell&#39;intestazione e riprova. |
| `2002-401` | Intestazione mancante | Nella richiesta manca l’intestazione x-gw-ims-org-id. Aggiorna il valore dell&#39;intestazione e riprova. |
| `2100-404` | Sandbox non trovato | Impossibile trovare la sandbox con il nome &#39;dev&#39;. Verifica che il nome della sandbox sia corretto e riprova. |
| `2101-404` | Sandbox non trovato | Impossibile trovare la sandbox con il nome &#39;dev&#39;. Errore dall&#39;API di gestione sandbox: Sandbox con nome &#39;dev&#39; non presente. Controlla se la risorsa esiste. |
| `2102-500` | Errore di acquisizione sandbox per nome | Si è verificato un problema durante il recupero di una sandbox con il nome &#39;dev&#39;. Errore dall&#39;API di gestione sandbox: Qualcosa è andato storto. Riprova. |
| `2103-404` | Sandbox non trovato | Impossibile trovare la sandbox con ID 8da3ef09-b469-404a e nome dev. Verifica che i valori ID e nome sandbox siano corretti e riprova. |
| `2104-500` | Errore di recupero sandbox per identificatore | Si è verificato un problema durante il recupero di una sandbox con id &#39;8da3ef09-b469-404a&#39; e nome &#39;dev&#39;. Errore dall&#39;API di gestione sandbox: Qualcosa è andato storto. Riprova. |
| `2105-400` | Intestazione mancante | Nella richiesta manca l’intestazione x-sandbox-name. Aggiungi l’intestazione nella richiesta e riprova. |
| `2106-404` | Errore sandbox predefinito | Impossibile trovare le informazioni predefinite sulla sandbox. |
| `2107-500` | Errore sandbox predefinito | Si è verificato un problema durante il recupero di una sandbox predefinita. Errore dall&#39;API di gestione sandbox: Qualcosa è andato storto. Riprova. |
| `2108-500` | Errore di Get active sandbox | Errore durante il recupero di una sandbox attiva. Errore dall&#39;API di gestione sandbox: Qualcosa è andato storto. Riprova. |
| `2110-400` | Intestazioni non consentite | L&#39;intestazione x-sandbox-id non è consentita con il token utente. Aggiorna l&#39;intestazione e riprova. |
| `2111-403` | Intestazioni con valore limitato | L’intestazione x-sandbox-name con valore * è limitata con il token utente. Aggiorna intestazione e valore e riprova. |
| `2112-400` | Intestazioni con valori diversi non consentite | Le intestazioni x-sandbox-name e x-sandbox-id devono entrambe avere il valore * per la query cross-sandbox. Aggiornare le intestazioni e riprovare. |
| `2113-400` | Intestazioni con valore non consentite | Le intestazioni x-sandbox-id e x-sandbox-name con valore * non sono consentite per la richiesta. Aggiornare le intestazioni e riprovare. |
| `2114-400` | Token vuoto | Token vuoto fornito. Immetti un token e riprova. |
| `2115-400` | Token non valido | Token non valido fornito. Specificare un token valido e riprovare. |
| `2116-500` | Errore interno | Errore interno durante la decodifica offline del token portatore per la risoluzione dell&#39;ambito. |
| `2117-500` | Errore interno | Errore interno durante il controllo delle autorizzazioni per l&#39;utente. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `2118-403` | Autorizzazione mancante | Scrittura autorizzazione mancante. Contattare l&#39;amministratore per risolvere le autorizzazioni e riprovare. |
| `2119-400` | Parametro query mancante | Il contesto della richiesta non contiene il parametro specId della query richiesto. Fornisci il parametro di query mancante e riprova. |
| `2120-403` | Proibito | Autorizzazioni insufficienti per eseguire l&#39;operazione. Contattare l&#39;amministratore per risolvere le autorizzazioni e riprovare. |
| `2121-403` | Proibito | La gestione delle autorizzazioni è negata nella risorsa Enterprise Source. Contattare l&#39;amministratore per risolvere le autorizzazioni e riprovare. |
| `2200-500` | Errore di richiesta del servizio esterno | Si è verificato un problema durante la chiamata del servizio Catalogo per la convalida dello schema. |
| `2250-500` | Errore di richiesta del servizio esterno | Si è verificato un problema durante la chiamata del servizio Preparazione dati per la convalida della mappatura. |

{style="table-layout:auto"}
