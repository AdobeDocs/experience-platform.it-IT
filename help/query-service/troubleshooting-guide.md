---
keywords: Experience Platform;home;argomenti popolari;servizio query;servizio query;guida alla risoluzione dei problemi;FAQ;risoluzione dei problemi;
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio query
topic-legacy: troubleshooting
description: Questo documento contiene informazioni sui codici di errore comuni riscontrati e sulle possibili cause.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---

# [!DNL Query Service] Guida alla risoluzione dei problemi

## Errori API REST

| Codice di stato HTTP | Descrizione | Possibili cause |
| ---------------- | ----------- | --------------- |
| 400 | Richiesta errata | Query non valida |
| 401 | Autenticazione non riuscita | Token di autenticazione non valido |
| 500 | Errore interno del server | Errore interno del sistema |

## Errori API PostgreSQL

| Codice di errore e stato di connessione | Descrizione | Possibile causa |
| ------------------------------- | ----------- | -------------- |
| **Start-up 28P01**  - autenticazione | Password non valida | Token di autenticazione non valido |
| **Start-up 28000**  - autenticazione | Tipo di autorizzazione non valido | Tipo di autorizzazione non valido. Deve essere `AuthenticationCleartextPassword`. |
| **42P12** Start-up - autenticazione | Nessuna tabella trovata | Non sono state trovate tabelle da utilizzare |
| **Query 42601**  | Errore di sintassi | Errore di comando o sintassi non valido |
| **Query 58000**  | Errore di sistema | Errore interno del sistema |
| **Query 42P01**  | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **Query 42P07**  | La tabella esiste | La tabella esiste già con lo stesso nome (CREATE TABLE) |
| **Query 53400**  | LIMITE supera il valore massimo | L&#39;utente ha specificato una clausola LIMIT superiore a 100.000 |
| **Query 53400**  | Timeout dell&#39;istruzione | La dichiarazione in diretta ha richiesto più di 10 minuti al massimo |
| **08P01** N/D | Tipo di messaggio non supportato | Tipo di messaggio non supportato |
