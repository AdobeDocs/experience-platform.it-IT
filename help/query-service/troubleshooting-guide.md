---
keywords: ' Experience Platform;home;argomenti comuni;servizio query;servizio query;guida alla risoluzione dei problemi;faq;risoluzione dei problemi;'
solution: Experience Platform
title: Guida alla risoluzione dei problemi del servizio query
topic: troubleshooting
description: Questo documento contiene informazioni sui codici di errore comuni riscontrati e sulle possibili cause.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---


# [!DNL Query Service] Guida alla risoluzione dei problemi

## Errori API REST

| Codice di stato HTTP | Descrizione | Possibili cause |
| ---------------- | ----------- | --------------- |
| 400 | Richiesta non valida | Query non valida |
| 401 | Autenticazione non riuscita | Token autenticazione non valido |
| 500 | Errore interno del server | Errore interno del sistema |

## Errori API PostgreSQL

| Codice errore e stato connessione | Descrizione | Possibile causa |
| ------------------------------- | ----------- | -------------- |
| **28P01** Start-up - autenticazione | Password non valida | Token di autenticazione non valido |
| **28000** Start-up - autenticazione | Tipo di autorizzazione non valido | Tipo di autorizzazione non valido. Deve essere `AuthenticationCleartextPassword`. |
| **42P12** Start-up - autenticazione | Nessuna tabella trovata | Nessuna tabella trovata per l&#39;uso |
| **42601** Query | Errore di sintassi | Errore di comando o sintassi non valido |
| **58000** Query | Errore di sistema | Errore interno del sistema |
| **42P01** Query | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **42P07** Query | Tabella esistente | La tabella esiste già con lo stesso nome (CREATE TABLE) |
| **53400** Query | LIMIT supera il valore massimo | L&#39;utente ha specificato una clausola LIMIT superiore a 100.000 |
| **53400** Query | Timeout istruzioni | Il resoconto live presentato dura più di 10 minuti |
| **08P01** N/D | Tipo di messaggio non supportato | Tipo di messaggio non supportato |
