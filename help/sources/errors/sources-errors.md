---
title: Messaggi di errore di Origini
description: Scopri i messaggi di errore che potresti incontrare durante l’utilizzo di Flusso Service per le origini.
source-git-commit: 10edb5dfd9ce99b69cf5bb014f4903942c9bff3e
workflow-type: tm+mt
source-wordcount: '3192'
ht-degree: 8%

---

# Messaggi di errore origine

Questo documento fornisce un catalogo di messaggi di errore, descrizioni e risoluzioni consigliate per le origini.

## Errori generici

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1000-400` | Richiesta errata | Richiesta non valida. Controlla la richiesta e riprova. |
| `1001-401` | Non autorizzato | L&#39;utente non è autorizzato. Contatta il tuo amministratore per accedere alla risorsa. |
| `1002-403` | Proibito | Operazione richiesta non consentita. Controllare l&#39;operazione richiesta e riprovare. |
| `1003-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. Controlla la richiesta fornita e riprova. |
| `1004-415` | Tipo di supporto non supportato | Il formato del payload specificato non è supportato. Controlla la richiesta fornita e riprova. |
| `1005-500` | Errore interno | Errore interno. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1006-408` | Timeout richiesta | Errore durante l&#39;elaborazione della richiesta. Timeout della richiesta. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1007-400` | Parametro di intestazione non valido | Parametro di intestazione non valido: {headerName} ricevuto. Controlla i parametri dell&#39;intestazione e riprova. |
| `1008-401` |  | Token di autorizzazione non valido | Il token di autorizzazione non ha accesso a questa organizzazione o l&#39;organizzazione non esiste. Assicurati che l&#39;organizzazione esista o contatta il tuo amministratore per ottenere l&#39;accesso. |
| `1009-403` | ID organizzazione IMS mancante o vuoto | L&#39;intestazione della richiesta dell&#39;ID organizzazione è mancante o vuota. Aggiorna il valore dell&#39;intestazione e riprova. |
| `1010-500` | Messaggio dettagliato non valido | Il parametro nel messaggio dettagliato non è stato fornito correttamente. Controlla il parametro nel messaggio dettagliato e riprova. |
| `1011-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1012-504` | Timeout gateway | Timeout del gateway. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1013-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. Controlla e riprova. |
| `1014-400` | Argomento non valido della richiesta | Impossibile elaborare la richiesta. {detailMessage} |

## Errori di framework

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1100-400` | Richiesta errata | Impossibile elaborare la richiesta. {detailMessage} |
| `1101-500` | Errore interno | Errore interno. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1102-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. {detailMessage} |
| `1103-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1104-504` | Timeout gateway | Timeout del gateway. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1105-401` | Non autorizzato | L&#39;utente non è autorizzato. {detailMessage} |
| `1106-403` | Proibito | Operazione richiesta non consentita. {detailMessage} |
| `1107-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. {detailMessage} |

## Errori di crittografia

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1200-500` | Errore interno | Errore interno. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1201-400` | Richiesta errata | Il flowId non può essere null o vuoto. Immetti un valore flowId valido nella richiesta e riprova. |
| `1202-400` | Richiesta errata | PublicKeyId mancante nelle trasformazioni={transformations} del flusso. Fornisci publicKeyId nella richiesta e riprova. |
| `1203-400` | Richiesta errata | La chiave di crittografia non esiste rispetto al keyID={keyID} nelle trasformazioni del flusso={transformations}. Controlla l&#39;ID chiave fornito e riprova. |
| `1204-400` | Richiesta errata | L&#39;algoritmo di crittografia specificato non è valido. Fornire un algoritmo di crittografia valido e riprovare. |
| `1205-400` | Richiesta errata | La passphrase è mancante nella sezione params della richiesta fornita. Fornisci passPhrase nei parametri e riprova. |

## Errori API REST

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1300-400` | Richiesta errata | La richiesta di connessione patch non è supportata per il connettore {connectorType}. Controlla la richiesta fornita e riprova. |
| `1301-400` | Richiesta errata | Parametro authSpecType fornito : {authSpecType} non supportato. Specificare un tipo di specifica di autenticazione valido e riprovare. |
| `1302-400` | Richiesta errata | Il tipo di autenticazione specificato = {authType} non è supportato per connector={connectorType}. Specificare un tipo di autenticazione valido per il connettore specificato. |
| `1303-400` | Richiesta errata | Impossibile codificare l&#39;URL con i parametri di autenticazione specificati perché la codifica URL non è supportata per {value}. Controlla i parametri di autenticazione e riprova. |
| `1304-400` | Richiesta errata | Il campo obbligatorio {field} non è fornito. Fornisci {field} e riprova. |
| `1305-400` | Richiesta errata | Il tipo di connettore specificato = {connectorType} non è supportato per questa operazione. |
| `1306-400` | Richiesta errata | La connessione di destinazione non può essere Null durante la convalida dell&#39;ID della specifica di connessione di destinazione. Controlla la richiesta fornita e riprova. |
| `1307-400` | Richiesta errata | ID della specifica di connessione di destinazione non valido={targetConnectionSpecId}. Il valore consentito è: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `1308-400` | Richiesta errata | Impossibile elaborare la richiesta. Messaggio di errore: {msftErrorMessage} |
| `1309-400` | Richiesta errata | La trasformazione di crittografia fornita non è valida perché {requiredParam} è mancante nei parametri. Fornisci {requiredParam} e riprova. |
| `1310-400` | Richiesta errata | Il valore publicKeyId fornito nei parametri è scaduto. Fornire un publicKeyId valido e riprovare. |
| `1311-400` | Richiesta errata | L&#39;ID publicKeyId fornito nei parametri non è valido. Fornire un publicKeyId valido e riprovare. |
| 1312-400 | Richiesta errata | Il valore di parametro specificato {paramValue} non è un input valido per property={requestParam}. Specificare un valore di parametro valido e riprovare. |
| `1313-400` | Richiesta errata | L&#39;attributo percorso {attribute} non esiste. Assicurati che l&#39;attributo esista e riprova. |
| `1314-400` | Richiesta errata | È stato fornito un percorso complesso ma non è consentito. Assicurati che non sia stato fornito il percorso complesso e riprova. |
| `1315-400` | Richiesta errata | Il percorso fornito {path} deve puntare a una matrice di record. Assicurati che il percorso fornito punti all&#39;array di record e riprova. |
| `1316-400` | Richiesta errata | I parametri di impaginazione specificati non devono essere vuoti. Specificare parametri di impaginazione validi e riprovare. |
| `1317-400` | Richiesta errata | I parametri di pianificazione specificati sono vuoti ma non devono essere vuoti. Specificare parametri di pianificazione validi e riprovare. |
| `1318-400` | Richiesta errata | {combinedMessage}. Controlla la richiesta fornita e riprova. |
| `1319-400` | Richiesta errata | {param} deve far parte della raccolta padre. Fornire {param} nella raccolta padre e riprovare. |
| `1320-400` | Richiesta errata | {idType} non può essere Null o vuoto. Specificare {idType} valido e riprovare. |
| `1321-400` | Richiesta errata | La lunghezza di {idType} deve essere una, la dimensione fornita è {size}. Specificare una dimensione valida e riprovare. |
| `1322-400` | Richiesta errata | La connessione di origine non può essere Null per la creazione del riferimento allo schema. Specificare una connessione sorgente valida e riprovare. |
| `1323-400` | Richiesta errata | L&#39;entità {entity} non può essere Null o vuota nella connessione di origine: {sourceConnection}. Specificare {entity} valido e riprovare. |
| `1324-400` | Richiesta errata | La connessione di destinazione non può essere null quando si estrae l’ID del set di dati. Specificare una connessione di destinazione valida e riprovare. |
| `1325-400` | Richiesta errata | Il parametro dataSetId non può essere null o vuoto nella connessione di destinazione: {TargetConnection}. Fornisci un parametro dataSetId valido e riprova. |
| `1326-400` | Richiesta errata | La connessione di origine non può essere Null quando si recupera il formato di origine. Specificare una connessione sorgente valida e riprovare. |
| `1327-400` | Richiesta errata | Il formato dei dati di origine forniti={sourceFormat} in SourceConnection non è supportato. I valori consentiti sono: {values}. Immetti i valori consentiti e riprova. |
| `1328-400` | Richiesta errata | La trasformazione di mappatura non può essere Null durante l&#39;estrazione di {param}. Fornire una trasformazione di mappatura valida e riprovare. |
| `1329-400` | Richiesta errata | Il parametro: {param} non può essere Null o vuoto nella richiesta fornita. Specificare {param} valido e riprovare. |
| `1330-400` | Richiesta errata | Impossibile trovare colonne per la tabella {tableName}. Specificare un nome di tabella valido e riprovare. |
| `1331-400` | Richiesta errata | Il delimitatore colonna non può essere costituito da più di un carattere in SourceConnection: {sourceConnection}. Specificare un delimitatore di colonna valido e riprovare. |
| `1332-400` | Richiesta errata | La richiesta di connessione di origine con connectionSpecId: {connectionSpecId} non può avere un baseConnectionId. Rimuovi baseConnectionId e riprova. |
| `1333-400` | Richieste errate | Il flussoRunAction={flowRunAction} non è supportato per l&#39;origine con spec id={specId}. Specificare un&#39;azione di esecuzione di flusso valida e riprovare. |
| `1334-400` | Richiesta errata | Parametro query : {param} non può essere vuoto. Specificare {param} valido e riprovare. |
| `1335-400` | Richiesta errata | Errore durante la serializzazione dei parametri del filtro per l&#39;esplorazione. Controlla la richiesta del parametro del filtro e riprova. |
| `1336-400` | Richiesta errata | La connessione Esplora non è supportata per l&#39;ID delle specifiche di connessione: {connectionSpecId}. Specificare l&#39;ID delle specifiche di connessione supportate e riprovare. |
| `1337-400` | Richiesta errata | {QueryParam} non può essere vuoto per objectType={objectType}. Fornisci {QueryParam} valido e riprova. |
| `1338-400` | Richiesta errata | L&#39;ID di connessione {connectionType} non può essere null in flowRequest. Fornire un ID di connessione {connectionType} valido in flowRequest. |
| `1339-400` | Richiesta errata | Il formato dell&#39;organizzazione={imsOrg} fornito nella richiesta non è valido. Immetti un ID organizzazione valido e riprova. |
| `1340-400` | Richiesta errata | Errore durante l&#39;analisi di {time}. Controlla il formato ora fornito nella richiesta e riprova. |
| `1341-400` | Richiesta errata | Il Json ODI fornito è vuoto. Fornire Json ODI valido e riprovare. |
| `1342-400` | Richiesta errata | Nel segmento &#39;dls:folder&#39; in &#39;odi.json&#39; mancano le definizioni. Fornisci le definizioni appropriate in &#39;odi.json&#39; e riprova. |
| `1343-400` | Richiesta errata | I segmenti &#39;dls:entityReferences&#39; e &#39;dls:partidSpec&#39; in &#39;odi.json&#39; mancano entrambe delle definizioni. Fornisci le definizioni appropriate in &#39;odi.json&#39; e riprova. |
| `1344-400` | Richiesta errata | La definizione di &#39;dls:partidSpec&#39; in &#39;odi.json&#39; non è valida perché sono state trovate più specifiche di partizione. Fornisci le definizioni appropriate in &#39;odi.json&#39; e riprova. |
| `1345-400` | Richiesta errata | Mancano definizioni in uno o più segmenti nei percorsi: &#39;dls:partizSpec/dls:fileFormat&#39;, &#39;dls:partizSpec/dls:partizTemplate&#39;,&#39;dls:partizSpec/dls:fileFormat/@type&#39;, &#39;dls:partizSpec/dls:fileFormat/dls:csvDelimiters&#39; in &#39;odi.json&#39;. Fornisci le definizioni appropriate in &#39;odi.json&#39; e riprova. |
| `1346-400` | Richiesta errata | La definizione &#39;@type&#39; fornita in &#39;dls:fileFormat&#39; in &#39;odi.json&#39; non è valida. Fornisci le definizioni appropriate in &#39;odi.json&#39; e riprova. |
| `1347-400` | Richiesta errata | La definizione dls:csvDelimiters&#39; in &#39;odi.json&#39; non è supportata. I delimitatori csv supportati sono: [&#39;,&#39;]. Fornisci le definizioni appropriate in &#39;odi.json&#39; e riprova. |
| `1348-400` | Richiesta errata | Errore durante la deserializzazione di &#39;dls:entityReferences&#39;. Verificare che il formato dei dati sia valido e riprovare. |
| `1349-400` | Richiesta errata | I parametri del filtro specificati non sono validi. Specificare parametri di filtro validi e riprovare. |
| `1350-400` | Richiesta errata | Nessun operatore fornito per il filtro all&#39;origine. Fornire una richiesta di filtro valida con l&#39;operatore appropriato e riprovare. |
| `1351-400` | Richiesta errata | L&#39;operatore {operator} fornito non è supportato per il filtro all&#39;origine per questo connettore. Specificare un operatore valido e riprovare. |
| `1352-400` | Richiesta errata | Impossibile mappare l&#39;operatore {operator} fornito a qualsiasi operatore nativo supportato per {ql}. Specificare un operatore valido e riprovare. |
| `1353-400` | Richiesta errata | Il filtro all&#39;origine non è ancora supportato per il connettore {connectorType}. Controlla i connettori supportati nella documentazione: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html. |
| `1354-400` | Richiesta errata | Il linguaggio di query {ql} non è ancora supportato per il filtro all&#39;origine. Specificare una lingua di query valida e riprovare. |
| `1355-400` | Richiesta errata | Il tipo di filtro specificato non è valido. Il tipo di filtro supportato è: PQL Specificare un tipo di filtro valido e riprovare. |
| `1356-400` | Richiesta errata | Il formato del filtro specificato non è valido. Il formato del filtro supportato è : pql/json. Specificare un formato di filtro valido e riprovare. |
| `1357-400` | Richiesta errata | Il filtro fornito non è valido. Il valore deve essere corredato di filtri dettagliati. Specificare un filtro valido e riprovare. |
| `1358-400` | Richiesta errata | Il parametro &#39;objectType&#39; specificato non è valido. Specificare un oggettoType valido e riprovare. |
| `1359-400` | Richiesta errata | Parametro {param} mancante nella richiesta. Specificare un {param} valido e riprovare. |
| `1360-400` | Richiesta errata | L&#39;ora di inizio non può essere impostata in passato. Specificare un&#39;ora di inizio valida e riprovare. |
| `1361-400` | Richiesta errata | L’intervallo non è consentito con un’acquisizione una tantum. Rimuovere l&#39;intervallo o modificare la frequenza, quindi riprovare. |
| `1362-400` | Richiesta errata | L&#39;intervallo non può essere minore di {minInterval}. Specificare un valore di intervallo valido e riprovare. |
| `1363-400` | Richiesta errata | Intervallo {intervallo} non consentito con frequenza: {frequency}. Specificare un valore di intervallo valido e riprovare. |
| `1364-400` | Richiesta errata | Il flag di backfill non è consentito quando la frequenza è impostata su uno. Rimuovere il flag di backfill quando la frequenza è impostata su una volta e riprovare. |
| `1365-400` | Richiesta errata | Il percorso {path} fornito in ops non è valido. Fornire un percorso valido {path} e riprovare. |
| `1366-400` | Richiesta errata | L&#39;ora di inizio è passata e l&#39;operazione di aggiornamento non è più consentita. |
| `1367-400` | Richiesta errata | La colonna delta è necessaria nella trasformazione copia durante la creazione di un connettore CRM. Fornire la colonna delta e riprovare. |
| `1368-400` | Richiesta errata | Modalità non consentita nella richiesta di flusso. Controlla la tua richiesta e riprova. |
| `1369-400` | Richiesta errata | La colonna delta nella trasformazione copia non è consentita quando la frequenza è impostata su una sola volta. Rimuovere la colonna delta e riprovare. |
| `1370-400` | Richiesta errata | Impossibile recuperare le colonne di origine per l&#39;acquisizione perché manca la trasformazione di mappatura. Aggiungi la trasformazione di mappatura e riprova. |
| `1371-400` | Richiesta errata | Il rilevamento delle proprietà del file non è supportato per il connettore {connectorType}. Fornire manualmente le proprietà del file. |
| `1372-400` | Richiesta errata | Operazione corrente non consentita. L&#39;esplorazione tramite la specifica di connessione non è consentita per la specifica di connessione ID={connectionSpecId}. |
| `1373-400` | Richiesta errata | Nella richiesta manca il flowSpecType. Specificare un valore di flowSpecType valido e riprovare. |
| `1374-400` | Richiesta errata | I parametri di query forniti non sono validi. Nella stessa richiesta non è possibile avere il flag resolve e le proprietà definite dall&#39;utente. Correggi la richiesta e riprova. |
| `1375-400` | Richiesta errata | Rilevamento delle proprietà del file non riuscito. Immetti le proprietà manualmente. |
| `1376-400` | Richiesta errata | Il rilevamento delle proprietà del file non è supportato per la specifica di connessione id={connectionSpecId}. Fornire manualmente le proprietà del file. |
| `1377-400` | Richiesta errata | Il parametro del valore specificato è nullo e non può essere confrontato con l&#39;operatore {operator}. Specificare un parametro di valore valido e riprovare. |
| `1378-400` | Richiesta errata | Errore durante la convalida della colonna di input {column} per il filtro all&#39;origine. Il nome della colonna deve essere una colonna valida nella tabella. Specificare un nome di colonna valido e riprovare. |
| `1379-400` | Richiesta errata | Errore durante la convalida dell&#39;input {value} per il filtro all&#39;origine. La colonna DataType all&#39;origine è {columnDataType} e il valore DataType [Stringa] non corrisponde. Specificare un {valore} valido e riprovare. |
| `1380-400` | Richiesta errata | Impossibile creare l&#39;esecuzione di flusso. Messaggio di errore: {message} |
| `1381-400` | Richiesta errata | WindowEndTime={endTime} non può essere precedente a Window StartTime={startTime}. Specificare un&#39;ora di fine valida e riprovare. |
| `1382-400` | Richiesta errata | La colonna delta deve corrispondere al valore presente nelle trasformazioni Copy del flusso. Specificare una colonna delta valida e riprovare. |
| `1383-400` | Richiesta errata | Colonna delta mancante nei parametri ricevuti per la creazione di un’esecuzione di flusso. Fornisci la colonna delta nei parametri e riprova. |
| `1384-400` | Richiesta errata | I parametri={params} forniti per la creazione dell&#39;esecuzione di flusso non sono validi o sono vuoti. Specificare parametri validi e riprovare. |
| `1385-400` | Richiesta errata | Il connettoreType={connectorType} fornito non è supportato per la creazione di esecuzioni di flusso. Specificare un valore ConnectorType valido e riprovare. |
| `1386-400` | Richiesta errata | Il flowId={flowId} con ScheduleParams frequency={frequency} non è supportato per la creazione di esecuzioni di flusso. Specificare una frequenza valida e riprovare. |
| `1387-400` | Richiesta errata | Il flowRunId={flowRunId} è in uno stato non valido={state} per il riavvio. Riprovare più tardi e, se il problema persiste, contattare l&#39;assistenza clienti. |
| `1388-400` | Richiesta errata | Il flusso={flow} è in stato={state} e non può essere riattivato. Il flusso deve essere abilitato per essere riattivato. |
| `1389-400` | Richiesta errata | Errore durante l&#39;analisi della stringa con codifica base64 fornita. Immetti una stringa di filtro codificata valida e riprova. |
| `1390-400` | Richiesta errata | L&#39;operatore &quot;not&quot; non può avere più di un confronto. Specificare un numero valido di confronti e riprovare. |
| `1391-400` | Richiesta errata | Impossibile analizzare SchemaMetaData in sourceConnection per Id={sourceConnectionId}. Controlla lo schemaMetaData nella richiesta e riprova. |
| `1392-400` | Richiesta errata | Impossibile analizzare le trasformazioni nella richiesta di flusso per flowId={flowId}. Controlla le trasformazioni nella richiesta e riprova. |
| `1393-400` | Richiesta errata | Il parametro fornito {parameter} è Null o vuoto. Specificare un {parametro} valido e riprovare. |
| `1394-400` | Richiesta errata | Il valore minimo per un parametro {parameter} è uno. Specificare un {parametro} valido e riprovare. |
| `1395-400` | Richiesta errata | La connessione di origine trovata nel flusso è Null o vuota. Specificare una connessione sorgente valida nel flusso e riprovare. |
| `1396-400` | Richiesta errata | Impossibile trovare un formato corrispondente. Specificare un formato corrispondente e riprovare. |
| `1397-400` | Richiesta errata | Frequenza fornita : {frequency} non valido. Specificare una frequenza valida e riprovare. |
| `1398-400` | Richiesta errata | L’operazione fornita : {action} non supportato. Controllare l&#39;operazione fornita e riprovare. |
| `1399-400` | Richiesta errata | Impossibile trovare un requestFileType valido. Fornire un requestFileType valido e riprovare. |
| `1400-400` | Richiesta errata | Il parametro &#39;templateType&#39; specificato non è valido. Specificare un tipo di modello valido e riprovare. |
| `1401-400` | Richiesta errata | L&#39;azione di esecuzione del flusso fornita={flowRunAction} non è supportata. Specificare un&#39;azione di esecuzione di flusso valida e riprovare. |
| `1402-500` | Errore interno | Errore interno. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1403-400` | Richiesta errata | L&#39;ora di inizio è passata e non puoi più cambiare la frequenza in una sola volta. |
| `1404-400` | Richiesta errata | L&#39;ora di inizio è passata e non è più possibile aggiornare il backfill. |

## Eccezioni del servizio di flusso (1600-1699)

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1600-400` | Richiesta errata | Impossibile elaborare la richiesta. {detailMessage} |
| `1601-500` | Errore interno | Errore interno. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1602-404` | Risorsa non trovata | Impossibile trovare la risorsa richiesta. {detailMessage} |
| `1603-503` | Servizio non disponibile | Servizio temporaneamente non disponibile. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1604-504` | Timeout gateway | Timeout del gateway. Riprova. Se il problema persiste, contatta l’assistenza clienti. |
| `1605-401` | Non autorizzato | L&#39;utente non è autorizzato. {detailMessage} |
| `1606-403` | Proibito | Operazione richiesta non consentita. {detailMessage} |
| `1607-412` | Precondizione non riuscita | La condizione definita dalle intestazioni If-Unmodified-Since o If-None-Match non è soddisfatta. {detailMessage} |

## Errori della zona di destinazione dei dati

| Codice errore | Titolo | Messaggio dettagliato |
| --- | --- | --- |
| `1700-500` | Errore interno | Errore interno. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1701-400` | Richiesta errata | La zona di destinazione specificata non è attiva. Attiva la zona di destinazione e riprova. |
| `1702-400` | Richiesta errata | Tipo SAS={sasType} specificato per la zona di destinazione non consentito. Fornire un SAS valido e riprovare. |
| `1703-400` | Richiesta errata | L&#39;aggiornamento delle credenziali non è consentito. |
| `1704-400` | Richiesta errata | Le chiavi restituite per storageAccountName={accountName} in subscriptionId={subscriptionId} e resourceGroupName={resourceGroupName} non sono corrette. Controlla la tua richiesta e riprova. Se il problema persiste, contattare il supporto tecnico. |
| `1705-400` | Richiesta errata | L’azione della zona di destinazione dati fornita non è supportata. Specificare un&#39;azione valida e riprovare. |
| `1706-400` | Richiesta errata | La configurazione delle attivazioni consentite non è configurata correttamente per la zona di destinazione={landingZoneType}. Riprovare e contattare l&#39;assistenza clienti se il problema persiste. |
| `1707-400` | Richiesta errata | Impossibile avviare il servizio perché la configurazione della zona di destinazione non può essere null o vuota. Verifica che la configurazione della zona di destinazione non sia null e riprova. |
| `1708-400` | Richiesta errata | La configurazione del contenitore non può essere null in landingZoneType={landingZoneType}. Verifica che la configurazione del contenitore non sia null e riprova. |
| `1709-400` | Richiesta errata | I dettagli SAS non possono essere Null per {tokenConfig} in landingZoneType={landingZoneType}. Fornire un SAS valido nella configurazione e riprovare. |
| `1710-400` | Richiesta errata | Zona di sbarco di tipo: {landingZoneUseCase} non supportato. Specificare un tipo di zona di destinazione valido e riprovare. |
| `1711-400` | Richiesta errata | Impossibile trovare i dettagli SAS per la zona di destinazione dati fornita di tipo: {landingZoneUseCase}. Verificare se sono forniti i dettagli SAS per il tipo di zona di destinazione specificato. |
| `1712-400` | Richiesta errata | Azione relativa alla zona di sbarco fornita : {actionType} non consentito. Specificare un&#39;azione valida per la zona di destinazione dei dati e riprovare. |
| `1713-400` | Richiesta errata | {OperationType} non consentito per il {tokenType} fornito. Controlla la tua richiesta e riprova. |
| `1714-400` | Richiesta errata | ClientId={clientId} non è autorizzato a eseguire questa operazione. Controlla la tua richiesta con le autorizzazioni e riprova. |