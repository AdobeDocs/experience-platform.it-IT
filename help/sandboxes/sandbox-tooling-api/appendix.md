---
title: Appendice alla guida dell’API per gli strumenti sandbox
description: Questo documento fornisce informazioni supplementari relative all’utilizzo dell’API Sandbox Tooling.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 955c6946786e9425bdb99d623595420a6d13747e
workflow-type: tm+mt
source-wordcount: '188'
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
| `jobType` | Tipo di processo. Questo valore può essere `NEW`, `RESUME` o `ROLLBACK`. |
| `jobStatus` | Stato del processo. Il valore può essere `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` o `CANCELLED`. |
| `requestType` | Tipo di richiesta. Questo valore può essere `EXPORT`, `IMPORT` o `COPY`. |
| `expiryPeriod` | Questo periodo di tempo specificato dall&#39;utente definisce la data di scadenza del pacchetto (in giorni) dal momento in cui il pacchetto è stato pubblicato. Questo valore non deve essere negativo. Il valore predefinito è 90 giorni dalla chiamata dell’API di aggiornamento o pubblicazione. |
| `packageType` | Tipo di pacchetto. Questo valore può essere `PARTIAL` o `FULL`. |
| `status` | Stato del pacchetto. Il valore può essere `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` o `PUBLISH_FAILED`. |
