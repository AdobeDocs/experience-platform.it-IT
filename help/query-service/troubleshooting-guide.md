---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ' Guida alla risoluzione dei problemi del servizio Query'
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---


# Errori e risoluzione dei problemi

## Errori API REST

| Codice di stato HTTP | Descrizione | Possibili cause |
| ---------------- | ----------- | --------------- |
| 400 | Richiesta non valida | Query non valida |
| 401 | Autenticazione non riuscita | Token autenticazione non valido |
| 500 | Errore interno del server | Errore interno del sistema |

## Errori API PostgreSQL

| Codice errore e stato connessione | Descrizione | Possibile causa |
| ------------------------------- | ----------- | -------------- |
| **Avvio 28P01** - autenticazione | Password non valida | Token di autenticazione non valido |
| **28000** Start-up - autenticazione | Tipo di autorizzazione non valido | Tipo di autorizzazione non valido. Dev&#39;essere `AuthenticationCleartextPassword`. |
| **Avvio 42P12** - autenticazione | Nessuna tabella trovata | Nessuna tabella trovata per l&#39;uso |
| **Query 42601** | Errore di sintassi | Errore di comando o sintassi non valido |
| **Query 58000** | Errore di sistema | Errore interno del sistema |
| **Query 42P01** | Tabella non trovata | Impossibile trovare la tabella specificata nella query |
| **Query 42P07** | Tabella esistente | La tabella esiste già con lo stesso nome (CREATE TABLE) |
| **Query 53400** | LIMIT supera il valore massimo | L&#39;utente ha specificato una clausola LIMIT superiore a 100.000 |
| **Query 53400** | Timeout istruzioni | Il resoconto live presentato dura più di 10 minuti |
| **08P01** N/D | Tipo di messaggio non supportato | Tipo di messaggio non supportato |
