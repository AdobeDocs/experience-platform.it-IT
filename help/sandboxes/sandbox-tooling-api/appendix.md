---
title: Appendice alla guida dell’API per gli strumenti sandbox
description: Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API Sandbox Tooling.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 1%

---

# Appendice alla guida delle API sandbox

Questo documento fornisce informazioni supplementari relative all&#39;utilizzo dell&#39;API [!DNL Sandbox].

## Utilizzo dei parametri di query {#query}

L’API degli strumenti sandbox supporta l’utilizzo di parametri di query per impaginare e filtrare i risultati quando si elencano i pacchetti.

>[!NOTE]
>
>`limit` può essere passato e avviato singolarmente.

| Parametro | Descrizione |
| --- | --- |
| `limit` | Numero massimo di record da restituire nella risposta. Il limite predefinito è 20. |
| `start` | L’inizio del punto da cui deve iniziare un elenco di elementi sottoimpostato. |
| `targetSandbox` | Rappresenta il nome della sandbox in cui si desidera importare gli artefatti. |
| `jobType` | Tipo di processo. Questo valore può essere NEW, RESUME e ROLLBACK. |
| `jobStatus` | Stato del processo. Questo valore può essere PENDING, IN_PROGRESS, SUCCESS, FAILED e CANCELED. |
| `requestType` | Tipo di richiesta. Questo valore può essere EXPORT, IMPORT e COPY. |
| `expiryPeriod ` | Questo periodo di tempo specificato dall&#39;utente definisce la data di scadenza del pacchetto (in giorni) dal momento in cui il pacchetto è stato pubblicato. Questo valore non deve essere negativo. Il valore predefinito è 90 giorni dalla chiamata dell’API di aggiornamento o pubblicazione. |
