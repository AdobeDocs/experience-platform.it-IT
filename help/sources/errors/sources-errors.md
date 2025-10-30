---
title: Messaggi di errore origini
description: Scopri i messaggi di errore che possono verificarsi quando utilizzi il servizio Flusso per le origini.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '3057'
ht-degree: 48%

---

# Messaggi di errore origini

Questo documento fornisce un catalogo di messaggi di errore, descrizioni e risoluzioni consigliate per le origini.

## Errori generici

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1000-400` | Richiesta non valida | Richiesta non valida. Controlla la richiesta e riprova. |
| `1001-401` | Non autorizzato | Utente non autorizzato. Contatta l’amministratore per ottenere l’accesso alla risorsa. |
| `1002-403` | Non consentito | L’operazione richiesta non è consentita. Verifica l’operazione richiesta e riprova. |
| `1003-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. Verifica la richiesta fornita e riprova. |
| `1004-415` | Tipo di file multimediale non supportato | Il formato di payload fornito non è supportato. Controlla la richiesta fornita e riprova. |
| `1005-500` | Errore interno | Si è verificato un errore interno. Riprova più tardi e contatta l’assistenza clienti se il problema persiste. |
| `1006-408` | Timeout della richiesta | Si è verificato un errore durante l’elaborazione della richiesta. Timeout della richiesta. Riprova e contatta l&#39;assistenza clienti se il problema persiste. |
| `1007-400` | Parametro di intestazione non valido | Parametro di intestazione non valido: {headerName} ricevuto. Controlla i parametri di intestazione e riprova. |
| `1008-401` | | Token di autorizzazione non valido | Il token di autorizzazione non ha accesso a questa organizzazione oppure l’organizzazione non esiste. Verifica che l’organizzazione esista o contatta l’amministratore per ottenere l’accesso. |
| `1009-403` | ID organizzazione IMS mancante o vuoto | L’intestazione della richiesta ID organizzazione è mancante o vuota. Aggiorna il valore dell’intestazione e riprova. |
| `1010-500` | Messaggio dettagliato non valido | Il parametro nel messaggio dettagliato non è stato fornito correttamente. Verifica il parametro nel messaggio dettagliato e riprova. |
| `1011-503` | Servizio non disponibile | Il servizio non è al momento disponibile. Riprova. Se il problema persiste contatta l’assistenza clienti. |
| `1012-504` | Timeout del gateway | Timeout del gateway. Riprova e contatta l’assistenza clienti se il problema persiste. |
| `1013-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. Verifica e riprova. |
| `1014-400` | Argomento non valido richiesta errata | Impossibile elaborare la richiesta. {detailedMessage} |

## Errori framework

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1100-400` | Richiesta non valida | Impossibile elaborare la richiesta. {detailedMessage} |
| `1101-500` | Errore interno | Si è verificato un errore interno. Riprova più tardi e contatta l’assistenza clienti se il problema persiste. |
| `1102-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. {detailedMessage} |
| `1103-503` | Servizio non disponibile | Il servizio non è al momento disponibile. Riprova. Se il problema persiste contatta l’assistenza clienti. |
| `1104-504` | Timeout del gateway | Timeout del gateway. Riprova e contatta l’assistenza clienti se il problema persiste. |
| `1105-401` | Non autorizzato | Utente non autorizzato. {detailedMessage} |
| `1106-403` | Non consentito | Operazione richiesta non consentita. {detailedMessage} |
| `1107-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. {detailedMessage} |

## Errori di crittografia

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1200-500` | Errore interno | Si è verificato un errore interno. Riprova più tardi e contatta l’assistenza clienti se il problema persiste. |
| `1201-400` | Richiesta non valida | Il valore flowId non può essere nullo o vuoto. Specifica un flowId valido nella richiesta e riprova. |
| `1202-400` | Richiesta non valida | PublicKeyId mancante nelle trasformazioni del flusso={transformations}. Specifica publicKeyId nella richiesta e riprova. |
| `1203-400` | Richiesta non valida | La chiave di crittografia non esiste per la chiave ID={keyID} nelle trasformazioni del flusso={transformations}. Controlla l’ID chiave fornito e riprova. |
| `1204-400` | Richiesta non valida | L’algoritmo di crittografia fornito non è valido. Fornisci un algoritmo di crittografia valido e riprova. |
| `1205-400` | Richiesta non valida | La passphrase non è presente nella sezione parametri della richiesta fornita. Fornisci la passPhrase nei parametri e riprova. |

## Errori REST API

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1300-400` | Richiesta non valida | La richiesta di connessione patch non è supportata per il connettore {connectorType}. Controlla la richiesta fornita e riprova. |
| `1301-400` | Richiesta non valida | Il parametro authSpecType fornito: {authSpecType} non è supportato. Specifica un tipo di specifica di autenticazione valido e riprova. |
| `1302-400` | Richiesta non valida | Il tipo di autenticazione fornito = {authType} non è supportato per il connettore={connectorType}. Fornisci un tipo di autenticazione valido per il connettore specificato. |
| `1303-400` | Richiesta non valida | Impossibile codificare l&#39;URL con i parametri di autenticazione specificati perché la codifica URL non è supportata per {value}. Verifica i parametri di autenticazione e riprova. |
| `1304-400` | Richiesta non valida | Il campo obbligatorio {field} non è stato specificato. Specifica {field} e riprova. |
| `1305-400` | Richiesta non valida | Il tipo di connettore fornito = {connectorType} non è supportato per questa operazione. |
| `1306-400` | Richiesta non valida | La connessione di destinazione non può essere nulla durante la convalida dell’ID della specifica di connessione di destinazione. Verifica la richiesta fornita e riprova. |
| `1307-400` | Richiesta non valida | ID della specifica di connessione di destinazione non valido={targetConnectionSpecId}. Valore consentito: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Richiesta non valida | Impossibile elaborare la richiesta. Messaggio di errore: {msftErrorMessage} |
| `1309-400` | Richiesta non valida | La trasformazione di crittografia fornita non è valida perché {requiredParam} manca nei parametri. Specifica {requiredParam} e riprova. |
| `1310-400` | Richiesta non valida | Il publicKeyId fornito nei parametri è scaduto. Specifica un publicKeyId valido e riprova. |
| `1311-400` | Richiesta non valida | Il publicKeyId fornito nei parametri non è valido. Specifica un publicKeyId valido e riprova. |
| 1312 - 400 | Richiesta non valida | Il valore del parametro {paramValue} specificato non è un input valido per la proprietà={requestParam}. Specifica un valore di parametro valido e riprova. |
| `1313-400` | Richiesta non valida | L&#39;attributo di percorso {attribute} non esiste. Verifica che l’attributo esista e riprova. |
| `1314-400` | Richiesta non valida | È stato fornito un percorso complesso che non è consentito. Verifica che non venga fornito un percorso complesso e riprova. |
| `1315-400` | Richiesta non valida | Il percorso specificato {path} deve puntare a un array di record. Verifica che il percorso fornito punti all’array di record e riprova. |
| `1316-400` | Richiesta non valida | I parametri di paginazione forniti non possono essere vuoti. Specifica parametri di paginazione validi e riprova. |
| `1317-400` | Richiesta non valida | I parametri di pianificazione forniti sono vuoti, ma non devono essere vuoti. Fornisci parametri di pianificazione validi e riprova. |
| `1318-400` | Richiesta non valida | {combinedMessage}. Controlla la richiesta fornita e riprova. |
| `1319-400` | Richiesta non valida | {param} deve far parte della raccolta padre. Specifica {param} nella raccolta padre e riprova. |
| `1320-400` | Richiesta non valida | {idType} non può essere null o vuoto. Fornisci {idType} valido e riprova. |
| `1321-400` | Richiesta non valida | La lunghezza di {idType} deve essere uno, la dimensione fornita è {size}. Specifica una dimensione valida e riprova. |
| `1322-400` | Richiesta non valida | La connessione di origine non può essere nulla per la creazione del riferimento di schema. Fornisci una connessione di origine valida e riprova. |
| `1323-400` | Richiesta non valida | {entity} non può essere null o vuoto nella connessione di origine: {sourceConnection}. Fornisci {entity} valido e riprova. |
| `1324-400` | Richiesta non valida | La connessione di destinazione non può essere nulla durante l’estrazione dell’ID del set di dati. Specifica una connessione di destinazione valida e riprova. |
| `1325-400` | Richiesta non valida | Il parametro dataSetId non può essere null o vuoto nella connessione di destinazione: {TargetConnection}. Specifica un parametro dataSetId valido e riprova. |
| `1326-400` | Richiesta non valida | La connessione di origine non può essere nulla durante il recupero del formato di origine. Fornisci una connessione sorgente valida e riprova. |
| `1327-400` | Richiesta non valida | Il formato dei dati di origine forniti={sourceFormat} in SourceConnection non è supportato. I valori consentiti sono: {values}. Specifica i valori consentiti e riprova. |
| `1328-400` | Richiesta non valida | La trasformazione di mappatura non può essere Null durante l&#39;estrazione di {param}. Fornisci una trasformazione di mappatura valida e riprova. |
| `1329-400` | Richiesta non valida | Il parametro {param} non può essere null o vuoto nella richiesta fornita. Fornisci {param} valido e riprova. |
| `1330-400` | Richiesta non valida | Nessuna colonna trovata per la tabella {tableName}. Specifica un nome di tabella valido e riprova. |
| `1331-400` | Richiesta non valida | Il delimitatore di colonna non può contenere più di un carattere in SourceConnection: {sourceConnection}. Specifica un delimitatore di colonna valido e riprova. |
| `1332-400` | Richiesta non valida | La richiesta di connessione di origine con connectionSpecId {connectionSpecId} non può avere un baseConnectionId. Rimuovi l’ID baseConnectionId e riprova. |
| `1333-400` | Richieste non valide | FlowRunAction={flowRunAction} non supportato per l&#39;origine con ID specifica={specId}. Specifica un’azione di esecuzione del flusso valida e riprova. |
| `1334-400` | Richiesta non valida | Il parametro di query {param} non può essere vuoto. Fornisci {param} valido e riprova. |
| `1335-400` | Richiesta non valida | Si è verificato un errore durante la serializzazione dei parametri del filtro per l’esplorazione. Verifica la richiesta del parametro del filtro e riprova. |
| `1336-400` | Richiesta non valida | Esplora connessione non supportata per l&#39;ID della specifica di connessione: {connectionSpecId}. Specifica l’ID di connessione supportato e riprova. |
| `1337-400` | Richiesta non valida | {QueryParam} non può essere vuoto per objectType={objectType}. Fornisci {QueryParam} valido e riprova. |
| `1338-400` | Richiesta non valida | L&#39;ID connessione {connectionType} non può essere null in flowRequest. Fornire un ID connessione {connectionType} valido in flowRequest. |
| `1339-400` | Richiesta non valida | Il formato dell&#39;organizzazione={imsOrg} fornito nella richiesta non è valido. Specifica un ID organizzazione valido e riprova. |
| `1340-400` | Richiesta non valida | Errore durante l&#39;analisi di {time}. Controlla il formato dell’ora fornito nella richiesta e riprova. |
| `1341-400` | Richiesta non valida | Il JSON ODI fornito è vuoto. Specifica un JSON ODI valido e riprova. |
| `1342-400` | Richiesta non valida | Definizioni mancanti nel segmento &#39;dls:folder&#39; in &#39;odi.json&#39;. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1343-400` | Richiesta non valida | I segmenti &#39;dls:entityReferences&#39; e &#39;dls:partitionSpec&#39; in &#39;odi.json&#39; non contengono entrambe le definizioni. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1344-400` | Richiesta non valida | La definizione di &#39;dls:partitionSpec&#39; in &#39;odi.json&#39; non è valida perché sono state trovate più partitionSpecs. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1345-400` | Richiesta non valida | Definizioni mancanti in 1 o più segmenti nei percorsi: &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&#39; in &#39;odi.json&#39;. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1346-400` | Richiesta non valida | La definizione &#39;@type&#39; fornita in &#39;dls:fileFormat&#39; in &#39;odi.json&#39; non è valida. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1347-400` | Richiesta non valida | La definizione dls:csvDelimiters&#39; in &#39;odi.json&#39; non è supportata. I delimitatori csv supportati sono: [&#39;,&#39;]. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1348-400` | Richiesta non valida | Errore durante la deserializzazione di &#39;dls:entityReferences&#39;. Verifica che i dati siano in un formato valido e riprova. |
| `1349-400` | Richiesta non valida | I parametri di filtro forniti non sono validi. Specifica parametri di filtro validi e riprova. |
| `1350-400` | Richiesta non valida | Non è stato fornito alcun operatore per il filtro all’origine. Fornisci una richiesta di filtro valida con l’operatore appropriato e riprova. |
| `1351-400` | Richiesta non valida | L&#39;operatore {operator} specificato non è supportato per il filtro all&#39;origine per questo connettore. Specifica un operatore valido e riprova. |
| `1352-400` | Richiesta non valida | L&#39;operatore {operator} specificato non può essere mappato ad alcun operatore nativo supportato per {ql}. Specifica un operatore valido e riprova. |
| `1353-400` | Richiesta non valida | Il filtro all&#39;origine non è ancora supportato per il connettore {connectorType}. Controlla i connettori supportati nella documentazione: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html?lang=it. |
| `1354-400` | Richiesta non valida | Il linguaggio di query {ql} non è ancora supportato per il filtro all&#39;origine. Specifica una lingua di query valida e riprova. |
| `1355-400` | Richiesta non valida | Il tipo di filtro fornito non è valido. Il tipo di filtro supportato è: PQL. Fornisci un tipo di filtro valido e riprova. |
| `1356-400` | Richiesta non valida | Il formato di filtro specificato non è valido. Il formato di filtro supportato è: pql/json. Fornisci un formato di filtro valido e riprova. |
| `1357-400` | Richiesta non valida | Il filtro fornito non è valido. Il valore deve essere fornito con filtri dettagliati. Specifica un filtro valido e riprova. |
| `1358-400` | Richiesta non valida | Il parametro “objectType” specificato non è valido. Fornisci un objectType valido e riprova. |
| `1359-400` | Richiesta non valida | Parametro {param} mancante nella richiesta. Specifica un {param} valido e riprova. |
| `1360-400` | Richiesta non valida | L’ora di inizio non può essere impostata nel passato. Specifica un’ora di inizio valida e riprova. |
| `1361-400` | Richiesta non valida | L’intervallo non è consentito per l’acquisizione una tantum. Rimuovi l’intervallo o modifica la frequenza e riprova. |
| `1362-400` | Richiesta non valida | L&#39;intervallo non può essere minore di {minInterval}. Specifica un valore di intervallo valido e riprova. |
| `1363-400` | Richiesta non valida | Intervallo {interval} non consentito con frequenza: {frequency}. Specifica un valore di intervallo valido e riprova. |
| `1364-400` | Richiesta non valida | Il flag di retrocompilazione non è consentito se la frequenza è impostata su uno. Rimuovi il flag di retrocompilazione quando la frequenza è impostata su una volta e riprova. |
| `1365-400` | Richiesta non valida | Il percorso {path} fornito in ops non è valido. Specificare un percorso valido {path} e riprovare. |
| `1366-400` | Richiesta non valida | L’ora di inizio è trascorsa e l&#39;operazione di aggiornamento non è più consentita. |
| `1367-400` | Richiesta non valida | La colonna delta è necessaria nella trasformazione della copia durante la creazione di un connettore di gestione delle relazioni con i clienti. Specifica la colonna delta e riprova. |
| `1368-400` | Richiesta non valida | Modalità non consentita nella richiesta di flusso. Controlla la richiesta e riprova. |
| `1369-400` | Richiesta non valida | La colonna delta nella trasformazione di copia non è consentita se la frequenza è impostata su una volta. Rimuovi la colonna delta e riprova. |
| `1370-400` | Richiesta non valida | Impossibile recuperare le colonne sorgente per l’acquisizione perché manca la trasformazione di mappatura. Aggiungi la trasformazione di mappatura e riprova. |
| `1371-400` | Richiesta non valida | Il rilevamento delle proprietà del file non è supportato per il connettore {connectorType}. Specifica manualmente le proprietà del file. |
| `1372-400` | Richiesta non valida | L&#39;operazione corrente non è consentita. L&#39;esplorazione tramite la specifica di connessione non è consentita per l&#39;ID della specifica di connessione={connectionSpecId}. |
| `1373-400` | Richiesta non valida | Manca il flowSpecType nella richiesta. Fornisci un flowSpecType valido e riprova. |
| `1374-400` | Richiesta non valida | I parametri di query forniti non sono validi. Nella stessa richiesta non è possibile avere il flag determineProperties e le proprietà definite dall’utente. Correggi la richiesta e riprova. |
| `1375-400` | Richiesta non valida | Rilevamento delle proprietà del file non riuscito. Inserisci le proprietà manualmente. |
| `1376-400` | Richiesta non valida | Il rilevamento delle proprietà del file non è supportato per la specifica di connessione con ID={connectionSpecId}. Specifica manualmente le proprietà del file. |
| `1377-400` | Richiesta non valida | Il parametro del valore specificato è null e non può essere confrontato con l&#39;operatore {operator}. Specifica un parametro di valore valido e riprova. |
| `1378-400` | Richiesta non valida | Errore durante la convalida della colonna di input {column} per il filtro all&#39;origine. Il nome della colonna deve essere una colonna valida nella tabella. Specifica un nome di colonna valido e riprova. |
| `1379-400` | Richiesta non valida | Errore durante la convalida dell&#39;input {value} per il filtro all&#39;origine. La colonna DataType all&#39;origine è {columnDataType} e il valore DataType [String] non corrisponde. Specifica un {value} valido e riprova. |
| `1380-400` | Richiesta non valida | Impossibile creare l&#39;esecuzione del flusso. Messaggio di errore: {message} |
| `1381-400` | Richiesta non valida | WindowEndTime={endTime} non può precedere Window StartTime={startTime}. Specifica un orario di fine valido e riprova. |
| `1382-400` | Richiesta non valida | La colonna delta deve corrispondere al valore presente nelle trasformazioni di copia del flusso. Specifica una colonna delta valida e riprova. |
| `1383-400` | Richiesta non valida | Manca la colonna delta nei parametri ricevuti per la creazione di un’esecuzione di flusso. Fornisci la colonna delta nei parametri e riprova. |
| `1384-400` | Richiesta non valida | I parametri {params} forniti per la creazione dell&#39;esecuzione del flusso non sono validi o sono vuoti. Specifica parametri validi e riprova. |
| `1385-400` | Richiesta non valida | Il tipo di connettore fornito={connectorType} non è supportato per la creazione di esecuzioni di flusso. Specifica un connectorType valido e riprova. |
| `1386-400` | Richiesta non valida | Il flowId={flowId} con frequenza scheduleParams={frequency} non è supportato per la creazione di esecuzioni di flusso. Specifica una frequenza valida e riprova. |
| `1387-400` | Richiesta non valida | Il flowRunId={flowRunId} è in uno stato non valido={state} per la riattivazione. Riprova più tardi e, se il problema persiste, contatta l’assistenza clienti. |
| `1388-400` | Richiesta non valida | Flusso={flow} nello stato={state}. Impossibile riattivarlo. Il flusso deve essere in stato abilitato per essere riattivato. |
| `1389-400` | Richiesta non valida | Si è verificato un errore durante l’analisi della stringa con codifica base64 fornita. Specifica una stringa di filtro codificata valida e riprova. |
| `1390-400` | Richiesta non valida | L’operatore “not” non può avere più di un confronto. Fornisci un numero valido di confronti e riprova. |
| `1391-400` | Richiesta non valida | Impossibile analizzare SchemaMetaData in sourceConnection per ID={sourceConnectionId}. Controlla gli schemiMetaData nella richiesta e riprova. |
| `1392-400` | Richiesta non valida | Impossibile analizzare le trasformazioni nella richiesta di flusso per flowId={flowId}. Controlla le trasformazioni nella richiesta e riprova. |
| `1393-400` | Richiesta non valida | Il parametro fornito {parameter} è null o vuoto. Specifica un {parameter} valido e riprova. |
| `1394-400` | Richiesta non valida | Il valore minimo per un parametro {parameter} è uno. Specifica un {parameter} valido e riprova. |
| `1395-400` | Richiesta non valida | La connessione di origine trovata nel flusso è nulla o vuota. Fornisci una connessione di origine valida nel flusso e riprova. |
| `1396-400` | Richiesta non valida | Impossibile trovare un formato corrispondente. Fornisci un formato corrispondente e riprova. |
| `1397-400` | Richiesta non valida | La frequenza specificata: {frequency} non è valida. Specifica una frequenza valida e riprova. |
| `1398-400` | Richiesta non valida | L&#39;operazione specificata {action} non è supportata. Controlla l’operazione fornita e riprova. |
| `1399-400` | Richiesta non valida | Impossibile trovare un requestFileType valido. Specifica un requestFileType valido e riprova. |
| `1400-400` | Richiesta non valida | Il parametro fornito “templateType” non è valido. Fornisci un tipo di modello valido e riprova. |
| `1401-400` | Richiesta non valida | L&#39;azione di esecuzione del flusso specificata={flowRunAction} non è supportata. Specifica un’azione di esecuzione del flusso valida e riprova. |
| `1402-500` | Errore interno | Si è verificato un errore interno. Riprova più tardi e contatta l’assistenza clienti se il problema persiste. |
| `1403-400` | Richiesta non valida | L’ora di inizio è passata e non è più possibile cambiare la frequenza in una volta. |
| `1404-400` | Richiesta non valida | L’ora di inizio è trascorsa e non è più possibile aggiornare la retrocompilazione. |

## Eccezioni servizio flusso (1600-1699)

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1600-400` | Richiesta non valida | Impossibile elaborare la richiesta. {detailedMessage} |
| `1601-500` | Errore interno | Si è verificato un errore interno. Riprova più tardi e contatta l’assistenza clienti se il problema persiste. |
| `1602-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. {detailedMessage} |
| `1603-503` | Servizio non disponibile | Il servizio non è temporaneamente disponibile. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1604-504` | Timeout del gateway | Timeout del gateway. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1605-401` | Non autorizzato | Utente non autorizzato. {detailedMessage} |
| `1606-403` | Non consentito | Operazione richiesta non consentita. {detailedMessage} |
| `1607-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. {detailedMessage} |

## Errori nelle aree di destinazione dati

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1700-500` | Errore interno | Si è verificato un errore interno. Riprova più tardi e contatta l’assistenza clienti se il problema persiste. |
| `1701-400` | Richiesta non valida | La zona di destinazione fornita è inattiva. Attiva la zona di destinazione e riprova. |
| `1702-400` | Richiesta non valida | Il tipo SAS={sasType} fornito per la zona di destinazione non è consentito. Specificare un SAS valido e riprovare. |
| `1703-400` | Richiesta non valida | Aggiornamento delle credenziali non consentito. |
| `1704-400` | Richiesta non valida | Le chiavi restituite per storageAccountName={accountName} in subscriptionId={subscriptionId} e resourceGroupName={resourceGroupName} non sono valide. Verifica la richiesta e riprova. Se il problema persiste, contatta il supporto. |
| `1705-400` | Richiesta non valida | L’azione della zona di destinazione dati fornita non è supportata. Specifica un’azione valida e riprova. |
| `1706-400` | Richiesta non valida | La configurazione delle attivazioni consentite non è configurata correttamente per la zona di destinazione={landingZoneType}. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1707-400` | Richiesta non valida | Non è stato possibile avviare il servizio perché la configurazione della zona di destinazione non può essere nulla o vuota. Assicurati che la configurazione della zona di destinazione non sia nulla e riprova. |
| `1708-400` | Richiesta non valida | La configurazione del contenitore non può essere null in landingZoneType={landingZoneType}. Verifica che la configurazione del contenitore non sia nulla e riprova. |
| `1709-400` | Richiesta non valida | I dettagli SAS non possono essere null per {tokenConfig} in landingZoneType={landingZoneType}. Specifica un SAS valido nella configurazione e riprova. |
| `1710-400` | Richiesta non valida | La zona di destinazione specificata di tipo {landingZoneUseCase} non è supportata. Specifica un tipo di zona di destinazione valido e riprova. |
| `1711-400` | Richiesta non valida | Dettagli SAS non trovati per l&#39;area di destinazione dati fornita di tipo: {landingZoneUseCase}. Verificare se i dettagli SAS sono forniti per il tipo di zona di destinazione specificato. |
| `1712-400` | Richiesta non valida | L&#39;azione della zona di destinazione specificata: {actionType} non è consentita. Specifica un’azione valida per la zona di destinazione dati e riprova. |
| `1713-400` | Richiesta non valida | {OperationType} non è consentito per il {tokenType} fornito. Verifica la richiesta e riprova. |
| `1714-400` | Richiesta non valida | ClientId={clientId} non è autorizzato a eseguire questa operazione. Verifica la richiesta con le autorizzazioni e riprova. |
