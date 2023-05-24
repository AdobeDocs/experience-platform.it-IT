---
title: Messaggi di errore origini
description: Scopri i messaggi di errore che possono verificarsi quando utilizzi il servizio Flusso per le origini.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# Messaggi di errore origini

Questo documento fornisce un catalogo di messaggi di errore, descrizioni e risoluzioni consigliate per le origini.

## Errori generici

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1000-400` | Richiesta non valida | Richiesta non valida. Verifica la richiesta e riprova. |
| `1001-401` | Non autorizzato | Utente non autorizzato. Contatta l’amministratore per ottenere l’accesso alla risorsa. |
| `1002-403` | Non consentito | Operazione richiesta non consentita. Controlla l’operazione richiesta e riprova. |
| `1003-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. Controlla la richiesta fornita e riprova. |
| `1004-415` | Tipo di file multimediale non supportato | Il formato di payload fornito non è supportato. Verifica la richiesta fornita e riprova. |
| `1005-500` | Errore interno | Errore interno. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1006-408` | Timeout richiesta | Si è verificato un errore durante l’elaborazione della richiesta. Timeout della richiesta. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1007-400` | Parametro di intestazione non valido | Parametro di intestazione non valido: {headerName} ricevuto. Controlla i parametri di intestazione e riprova. |
| `1008-401` |  | Token di autorizzazione non valido | Il token di autorizzazione non ha accesso a questa organizzazione oppure l’organizzazione non esiste. Assicurati che l’organizzazione esista o contatta l’amministratore per ottenere l’accesso. |
| `1009-403` | ID organizzazione IMS mancante o vuoto | L’intestazione della richiesta dell’ID organizzazione è mancante o vuota. Aggiorna il valore dell’intestazione e riprova. |
| `1010-500` | Messaggio dettagliato non valido | Il parametro nel messaggio dettagliato non è stato fornito correttamente. Controlla il parametro nel messaggio dettagliato e riprova. |
| `1011-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1012-504` | Timeout del gateway | Timeout del gateway. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1013-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. Verifica e riprova. |
| `1014-400` | Richiesta non valida Argomento non valido | Impossibile elaborare la richiesta. {detailedMessage} |

## Errori framework

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1100-400` | Richiesta errata | Impossibile elaborare la richiesta. {detailedMessage} |
| `1101-500` | Errore interno | Errore interno. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1102-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. {detailedMessage} |
| `1103-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1104-504` | Timeout del gateway | Timeout del gateway. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1105-401` | Non autorizzato | Utente non autorizzato. {detailedMessage} |
| `1106-403` | Non consentito | Operazione richiesta non consentita. {detailedMessage} |
| `1107-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. {detailedMessage} |

## Errori di crittografia

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1200-500` | Errore interno | Errore interno. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1201-400` | Richiesta errata | Il flowId non può essere null o vuoto. Specifica un flowId valido nella richiesta e riprova. |
| `1202-400` | Richiesta errata | PublicKeyId mancante nelle trasformazioni del flusso={transformations}. Specifica publicKeyId nella richiesta e riprova. |
| `1203-400` | Richiesta errata | La chiave di crittografia non esiste per la chiave ID={keyID} nelle trasformazioni del flusso={transformations}. Controlla l’ID chiave fornito e riprova. |
| `1204-400` | Richiesta errata | L&#39;algoritmo di crittografia fornito non è valido. Specifica un algoritmo di crittografia valido e riprova. |
| `1205-400` | Richiesta errata | La passphrase non è presente nella sezione dei parametri della richiesta fornita. Specifica la frase di accesso nei parametri e riprova. |

## Errori REST API

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1300-400` | Richiesta errata | La richiesta di connessione patch non è supportata per il connettore {connectorType}. Controlla la richiesta fornita e riprova. |
| `1301-400` | Richiesta errata | Il parametro authSpecType fornito: {authSpecType} non è supportato. Specifica un tipo di specifica di autenticazione valido e riprova. |
| `1302-400` | Richiesta errata | Il tipo di autenticazione fornito = {authType} non è supportato per il connettore={connectorType}. Fornisci un tipo di autenticazione valido per il connettore specificato. |
| `1303-400` | Richiesta errata | Impossibile codificare l’URL con i parametri di autenticazione specificati perché la codifica URL non è supportata per {value}. Verifica i parametri di autenticazione e riprova. |
| `1304-400` | Richiesta errata | Il campo obbligatorio {field} non è stato fornito. Specifica il {field} e riprova. |
| `1305-400` | Richiesta errata | Il tipo di connettore fornito = {connectorType} non è supportato per questa operazione. |
| `1306-400` | Richiesta errata | La connessione di destinazione non può essere null durante la convalida dell&#39;ID della specifica di connessione di destinazione. Controlla la richiesta fornita e riprova. |
| `1307-400` | Richiesta errata | L’ID della specifica di connessione di destinazione non è valido={targetConnectionSpecId}. Il valore consentito è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Richiesta errata | Impossibile elaborare la richiesta. Messaggio di errore: {msftErrorMessage} |
| `1309-400` | Richiesta errata | La trasformazione di crittografia fornita non è valida perché {requiredParam} non è presente nei parametri. Specifica {requiredParam} e riprova. |
| `1310-400` | Richiesta errata | Il valore publicKeyId fornito nei parametri è scaduto. Specifica un publicKeyId valido e riprova. |
| `1311-400` | Richiesta errata | Il valore publicKeyId fornito nei parametri non è valido. Specifica un publicKeyId valido e riprova. |
| 1312-400 | Richiesta errata | Il valore del parametro fornito {paramValue} non è un input valido per la proprietà={requestParam}. Specifica un valore di parametro valido e riprova. |
| `1313-400` | Richiesta errata | L’attributo percorso {attribute} non esiste. Verifica che l’attributo esista e riprova. |
| `1314-400` | Richiesta errata | È stato fornito un percorso complesso, ma non è consentito. Verifica che non sia stato fornito un percorso complesso e riprova. |
| `1315-400` | Richiesta errata | Il percorso {path} fornito deve puntare a un array di record. Verifica che il percorso fornito punti all’array di record e riprova. |
| `1316-400` | Richiesta errata | I parametri di paginazione forniti non possono essere vuoti. Specifica parametri di impaginazione validi e riprova. |
| `1317-400` | Richiesta errata | I parametri di pianificazione forniti sono vuoti, ma non possono essere vuoti. Specifica parametri di pianificazione validi e riprova. |
| `1318-400` | Richiesta errata | {combinedMessage}. Controlla la richiesta fornita e riprova. |
| `1319-400` | Richiesta errata | {param} deve far parte della raccolta principale. Specifica {param} nella raccolta principale e riprova. |
| `1320-400` | Richiesta errata | {idType} non può essere null o vuoto. Specifica un {idType} valido e riprova. |
| `1321-400` | Richiesta errata | La lunghezza di {idType} deve essere uno, la dimensione fornita è {size}. Specifica una dimensione valida e riprova. |
| `1322-400` | Richiesta errata | La connessione di origine non può essere null per la creazione del riferimento schema. Specifica una connessione sorgente valida e riprova. |
| `1323-400` | Richiesta errata | L’entità {entity} non può essere nulla o vuota nella connessione di origine {sourceConnection}. Specifica un’entità {entity} valida e riprova. |
| `1324-400` | Richiesta errata | La connessione di destinazione non può essere null durante l’estrazione dell’ID del set di dati. Specifica una connessione di destinazione valida e riprova. |
| `1325-400` | Richiesta errata | Il parametro dataSetId non può essere null o vuoto nella connessione di destinazione {TargetConnection}. Specifica un parametro dataSetId valido e riprova. |
| `1326-400` | Richiesta errata | La connessione di origine non può essere null durante il recupero del formato di origine. Specifica una connessione sorgente valida e riprova. |
| `1327-400` | Richiesta errata | Il formato dei dati di origine forniti={sourceFormat} in SourceConnection non è supportato. I valori consentiti sono: {values}. Specifica i valori consentiti e riprova. |
| `1328-400` | Richiesta errata | La trasformazione di mappatura non può essere null durante l’estrazione di {param}. Fornisci una trasformazione di mappatura valida e riprova. |
| `1329-400` | Richiesta errata | Il parametro {param} non può essere nullo o vuoto nella richiesta fornita. Specifica un {param} valido e riprova. |
| `1330-400` | Richiesta errata | Non è stata trovata alcuna colonna per la tabella {tableName}. Specifica un nome di tabella valido e riprova. |
| `1331-400` | Richiesta errata | Il delimitatore di colonna non può contenere più di un carattere in SourceConnection: {sourceConnection}. Specifica un delimitatore di colonna valido e riprova. |
| `1332-400` | Richiesta errata | La richiesta di connessione di origine con connectionSpecId {connectionSpecId} non può avere un baseConnectionId. Rimuovi l’ID baseConnectionId e riprova. |
| `1333-400` | Richieste non valide | FlowRunAction={flowRunAction} non è supportato per l’origine con ID specifica={specId}. Specifica un’azione di esecuzione del flusso valida e riprova. |
| `1334-400` | Richiesta errata | Il parametro di query {param} non può essere vuoto. Specifica un {param} valido e riprova. |
| `1335-400` | Richiesta errata | Si è verificato un errore durante la serializzazione dei parametri del filtro per l’esplorazione. Verifica la richiesta del parametro di filtro e riprova. |
| `1336-400` | Richiesta errata | La connessione di esplorazione non è supportata per l’ID della specifica di connessione {connectionSpecId}. Specifica l’ID di connessione supportato e riprova. |
| `1337-400` | Richiesta errata | {QueryParam} non può essere vuoto per objectType={objectType}. Specifica un {QueryParam} valido e riprova. |
| `1338-400` | Richiesta errata | L’ID di connessione {connectionType} non può essere nullo in flowRequest. Fornisci un ID connessione {connectionType} valido in flowRequest. |
| `1339-400` | Richiesta errata | Il formato dell’organizzazione={imsOrg} fornito nella richiesta non è valido. Specifica un ID organizzazione valido e riprova. |
| `1340-400` | Richiesta errata | Si è verificato un errore durante l’analisi di {time}. Controlla il formato dell’ora fornito nella richiesta e riprova. |
| `1341-400` | Richiesta errata | Il codice Json ODI fornito è vuoto. Specifica un codice Json ODI valido e riprova. |
| `1342-400` | Richiesta errata | Definizioni mancanti nel segmento &quot;dls:folder&quot; in &quot;odi.json&quot;. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1343-400` | Richiesta errata | I segmenti &quot;dls:entityReferences&quot; e &quot;dls:partitionSpec&quot; in &quot;odi.json&quot; non contengono entrambe le definizioni. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1344-400` | Richiesta errata | La definizione di &#39;dls:partitionSpec&#39; in &#39;odi.json&#39; non è valida perché sono state trovate più di una partitionSpecs. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1345-400` | Richiesta errata | Nei percorsi mancano le definizioni in 1 o più segmenti: &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls:fileFormat/dls:csvDelimiters&#39; in &#39;odi.json&#39;. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1346-400` | Richiesta errata | La definizione &#39;@type&#39; fornita in &#39;dls:fileFormat&#39; in &#39;odi.json&#39; non è valida. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1347-400` | Richiesta errata | La definizione dls:csvDelimiters&#39; in ’odi.json’ non è supportata. I delimitatori csvDelimiter supportati sono: [&#39;,&#39;]. Specifica le definizioni appropriate in ’odi.json’ e riprova. |
| `1348-400` | Richiesta errata | Errore durante la deserializzazione di &#39;dls:entityReferences&#39;. Verifica che i dati siano in un formato valido e riprova. |
| `1349-400` | Richiesta errata | I parametri di filtro forniti non sono validi. Specifica parametri di filtro validi e riprova. |
| `1350-400` | Richiesta errata | Non è stato fornito alcun operatore per il filtro all’origine. Fornisci una richiesta di filtro valida con l’operatore appropriato e riprova. |
| `1351-400` | Richiesta errata | L’operatore {operator} fornito non è supportato per il filtro all’origine per questo connettore. Specifica un operatore valido e riprova. |
| `1352-400` | Richiesta errata | Impossibile mappare l’operatore {operator} fornito ad alcun operatore nativo supportato per {ql}. Specifica un operatore valido e riprova. |
| `1353-400` | Richiesta errata | Il filtro all’origine non è ancora supportato per il connettore {connectorType}. Controlla i connettori supportati nella documentazione: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html. |
| `1354-400` | Richiesta errata | Il linguaggio di query {ql} non è ancora supportato per il filtro all’origine. Specifica una lingua di query valida e riprova. |
| `1355-400` | Richiesta errata | Il tipo di filtro fornito non è valido. Il tipo di filtro supportato è: PQL. Specifica un tipo di filtro valido e riprova. |
| `1356-400` | Richiesta errata | Il formato di filtro fornito non è valido. Il formato di filtro supportato è: pql/json. Specifica un formato di filtro valido e riprova. |
| `1357-400` | Richiesta errata | Il filtro fornito non è valido. Il valore deve essere fornito con filtri dettagliati. Specifica un filtro valido e riprova. |
| `1358-400` | Richiesta errata | Il parametro &#39;objectType&#39; specificato non è valido. Specifica un objectType valido e riprova. |
| `1359-400` | Richiesta errata | Parametro {param} mancante nella richiesta. Specifica un {param} valido e riprova. |
| `1360-400` | Richiesta errata | Impossibile impostare l&#39;ora di inizio nel passato. Specifica un’ora di inizio valida e riprova. |
| `1361-400` | Richiesta errata | Intervallo non consentito con l’acquisizione una tantum. Rimuovi l’intervallo o cambia la frequenza, quindi riprova. |
| `1362-400` | Richiesta errata | L’intervallo non può essere inferiore a {minInterval}. Specifica un valore di intervallo valido e riprova. |
| `1363-400` | Richiesta errata | Intervallo {interval} non consentito con frequenza: {frequency}. Specifica un valore di intervallo valido e riprova. |
| `1364-400` | Richiesta errata | Il flag di retrocompilazione non è consentito se la frequenza è impostata su uno. Rimuovi il flag di retrocompilazione quando la frequenza è impostata su una volta e riprova. |
| `1365-400` | Richiesta errata | Il percorso {path} fornito in ops non è valido. Specifica un percorso valido {path} e riprova. |
| `1366-400` | Richiesta errata | L&#39;ora di inizio è stata superata e l&#39;operazione di aggiornamento non è più consentita. |
| `1367-400` | Richiesta errata | La colonna delta è necessaria nella trasformazione di copia durante la creazione di un connettore di gestione delle relazioni con i clienti. Specifica la colonna delta e riprova. |
| `1368-400` | Richiesta errata | Modalità non consentita nella richiesta di flusso. Verifica la richiesta e riprova. |
| `1369-400` | Richiesta errata | La colonna delta nella trasformazione di copia non è consentita se la frequenza è impostata su una volta. Rimuovi la colonna delta e riprova. |
| `1370-400` | Richiesta errata | Impossibile recuperare le colonne di origine per l’acquisizione perché manca la trasformazione di mappatura. Aggiungi la trasformazione di mappatura e riprova. |
| `1371-400` | Richiesta errata | Il rilevamento delle proprietà del file non è supportato per il connettore {connectorType}. Specifica manualmente le proprietà del file. |
| `1372-400` | Richiesta errata | L&#39;operazione corrente non è consentita. L’esplorazione tramite la specifica di connessione non è consentita per la specifica di connessione ID={connectionSpecId}. |
| `1373-400` | Richiesta errata | Il flowSpecType non è presente nella richiesta. Specifica un flowSpecType valido e riprova. |
| `1374-400` | Richiesta errata | I parametri di query forniti non sono validi. Nella stessa richiesta non è possibile avere il flag determinaProperties e le proprietà definite dall&#39;utente. Correggi la richiesta e riprova. |
| `1375-400` | Richiesta errata | Rilevamento delle proprietà del file non riuscito. Immetti le proprietà manualmente. |
| `1376-400` | Richiesta errata | Il rilevamento delle proprietà del file non è supportato per la specifica di connessione id={connectionSpecId}. Specifica manualmente le proprietà del file. |
| `1377-400` | Richiesta errata | Il parametro del valore fornito è nullo e non può essere confrontato con l’operatore {operator}. Specifica un parametro di valore valido e riprova. |
| `1378-400` | Richiesta errata | Errore durante la convalida della colonna di input {column} per il filtro all’origine. Il nome della colonna deve essere una colonna valida nella tabella. Specifica un nome di colonna valido e riprova. |
| `1379-400` | Richiesta errata | Errore durante la convalida dell’input {value} per il filtro all’origine. Il DataType della colonna all’origine è {columnDataType} e il valore DataType [Stringa] non corrisponde. Specifica un {value} valido e riprova. |
| `1380-400` | Richiesta errata | Impossibile creare l&#39;esecuzione del flusso. Messaggio di errore: {message} |
| `1381-400` | Richiesta errata | WindowEndTime={endTime} non può precedere Window StartTime={startTime}. Specifica un orario di fine valido e riprova. |
| `1382-400` | Richiesta errata | La colonna delta deve corrispondere al valore presente nelle trasformazioni di copia del flusso. Specifica una colonna delta valida e riprova. |
| `1383-400` | Richiesta errata | La colonna delta non è presente nei parametri ricevuti per la creazione di un’esecuzione di flusso. Specifica la colonna delta nei parametri e riprova. |
| `1384-400` | Richiesta errata | I parametri={params} forniti per la creazione dell’esecuzione del flusso non sono validi o sono vuoti. Specifica parametri validi e riprova. |
| `1385-400` | Richiesta errata | Il tipo di connettore fornito {connectorType} non è supportato per la creazione di esecuzioni di flusso. Specifica un connectorType valido e riprova. |
| `1386-400` | Richiesta errata | Il flowId={flowId} con frequenza scheduleParams={frequency} non è supportato per la creazione di esecuzioni di flusso. Specifica una frequenza valida e riprova. |
| `1387-400` | Richiesta errata | Il flowRunId={flowRunId} è in uno stato non valido={state} per la riattivazione. Riprova più tardi e, se il problema persiste, contatta l’assistenza clienti. |
| `1388-400` | Richiesta errata | Il flusso {flow} si trova nello stato {state} e non può essere riattivato. Il flusso deve essere in stato abilitato per essere riattivato. |
| `1389-400` | Richiesta errata | Si è verificato un errore durante l’analisi della stringa con codifica base64 fornita. Specifica una stringa di filtro codificata valida e riprova. |
| `1390-400` | Richiesta errata | L&#39;operatore &#39;not&#39; non può avere più di un confronto. Specifica un numero valido di confronti e riprova. |
| `1391-400` | Richiesta errata | Impossibile analizzare SchemaMetaData in sourceConnection per ID={sourceConnectionId}. Controlla gli schemiMetaData nella richiesta e riprova. |
| `1392-400` | Richiesta errata | Impossibile analizzare le trasformazioni nella richiesta di flusso per flowId={flowId}. Controlla le trasformazioni nella richiesta e riprova. |
| `1393-400` | Richiesta errata | Il parametro {parameter} fornito è nullo o vuoto. Specifica un {parameter} valido e riprova. |
| `1394-400` | Richiesta errata | Il valore minimo per un parametro {parameter} è uno. Specifica un {parameter} valido e riprova. |
| `1395-400` | Richiesta errata | La connessione di origine trovata nel flusso è null o vuota. Specifica una connessione di origine valida nel flusso e riprova. |
| `1396-400` | Richiesta errata | Impossibile trovare un formato corrispondente. Specifica un formato corrispondente e riprova. |
| `1397-400` | Richiesta errata | La frequenza fornita: {frequency} non è valida. Specifica una frequenza valida e riprova. |
| `1398-400` | Richiesta errata | L’operazione fornita {action} non è supportata. Controlla l’operazione fornita e riprova. |
| `1399-400` | Richiesta errata | Impossibile trovare un requestFileType valido. Specifica un requestFileType valido e riprova. |
| `1400-400` | Richiesta errata | Il parametro &#39;templateType&#39; fornito non è valido. Specifica un tipo di modello valido e riprova. |
| `1401-400` | Richiesta errata | L’azione di esecuzione del flusso fornita={flowRunAction} non è supportata. Specifica un’azione di esecuzione del flusso valida e riprova. |
| `1402-500` | Errore interno | Errore interno. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1403-400` | Richiesta errata | L&#39;ora di inizio è trascorsa e non è più possibile modificare la frequenza in una sola volta. |
| `1404-400` | Richiesta errata | L&#39;ora di inizio è trascorsa e non è più possibile aggiornare la retrocompilazione. |

## Eccezioni servizio flusso (1600-1699)

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1600-400` | Richiesta errata | Impossibile elaborare la richiesta. {detailedMessage} |
| `1601-500` | Errore interno | Errore interno. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1602-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. {detailedMessage} |
| `1603-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1604-504` | Timeout del gateway | Timeout del gateway. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1605-401` | Non autorizzato | Utente non autorizzato. {detailedMessage} |
| `1606-403` | Non consentito | Operazione richiesta non consentita. {detailedMessage} |
| `1607-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. {detailedMessage} |

## Errori nelle aree di destinazione dati

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1700-500` | Errore interno | Errore interno. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1701-400` | Richiesta errata | La zona di destinazione specificata è inattiva. Attiva la zona di destinazione e riprova. |
| `1702-400` | Richiesta errata | Il tipo SAS={sasType} fornito per la zona di destinazione non è consentito. Specificare un SAS valido e riprovare. |
| `1703-400` | Richiesta errata | Aggiornamento delle credenziali non consentito. |
| `1704-400` | Richiesta errata | Le chiavi restituite per storageAccountName={accountName} in subscriptionId={subscriptionId} e resourceGroupName={resourceGroupName} non sono valide. Verifica la richiesta e riprova. Se il problema persiste, contatta il supporto. |
| `1705-400` | Richiesta errata | L’azione della zona di destinazione dati fornita non è supportata. Specifica un&#39;azione valida e riprova. |
| `1706-400` | Richiesta errata | La configurazione delle attivazioni consentite non è configurata correttamente per la zona di destinazione={landingZoneType}. Se il problema persiste, riprova e contatta l’assistenza clienti. |
| `1707-400` | Richiesta errata | Impossibile avviare il servizio. La configurazione della zona di destinazione non può essere null o vuota. Verifica che la configurazione della zona di destinazione non sia nulla e riprova. |
| `1708-400` | Richiesta errata | La configurazione del contenitore non può essere null in landingZoneType={landingZoneType}. Verifica che la configurazione del contenitore non sia nulla e riprova. |
| `1709-400` | Richiesta errata | I dettagli SAS non possono essere null per {tokenConfig} in landingZoneType={landingZoneType}. Specifica un SAS valido nella configurazione e riprova. |
| `1710-400` | Richiesta errata | La zona di destinazione fornita di tipo {landingZoneUseCase} non è supportata. Specifica un tipo di zona di destinazione valido e riprova. |
| `1711-400` | Richiesta errata | Impossibile trovare i dettagli SAS per l’area di destinazione dati fornita di tipo {landingZoneUseCase}. Verificare se i dettagli SAS sono forniti per il tipo di zona di destinazione specificato. |
| `1712-400` | Richiesta errata | L’azione della zona di destinazione specificata {actionType} non è consentita. Specifica un’azione valida per la zona di destinazione dati e riprova. |
| `1713-400` | Richiesta errata | {OperationType} non consentito per il {tokenType} fornito. Verifica la richiesta e riprova. |
| `1714-400` | Richiesta errata | ClientId={clientId} non è autorizzato a eseguire questa operazione. Verifica la richiesta con le autorizzazioni e riprova. |
