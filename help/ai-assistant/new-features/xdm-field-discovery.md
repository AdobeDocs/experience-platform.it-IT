---
title: Individuazione campi XDM con l’Assistente AI
description: Leggi questo documento per scoprire come utilizzare l’Assistente all’intelligenza artificiale per l’individuazione dei campi di Experience Data Model (XDM).
badge: Alpha
hide: true
hidefromtoc: true
source-git-commit: 2348001facd7ae3a95254130ae377b4ef3f2a749
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Individuazione campi XDM per con Assistente IA

>[!AVAILABILITY]
>
>Questa funzione è disponibile in Alpha e potrebbe non essere disponibile per la tua organizzazione. Per partecipare al programma di Alpha e accedere a questa funzione, contatta il team del tuo account Adobe.

È possibile utilizzare l’Assistente AI per cercare e individuare i campi Experience Data Model (XDM) che possono essere utilizzati per creare tipi di pubblico mirati in Experience Platform.

Leggi la tabella seguente per i pattern di query e prompt supportati per l’individuazione dei campi XDM nell’Assistente IA.

>[!TIP]
>
>Anche se i pattern di query e prompt possono essere gli stessi in diversi casi d’uso, la formulazione esatta di una domanda varia a seconda dei campi XDM e degli schemi utilizzati per una determinata sandbox.

| Tipo di query | Pattern query/prompt | Esempi |
| --- | --- | --- |
| Individuazione campi XDM per dominio o area dati | Mostra i campi XDM utilizzati per rappresentare {DATA_DOMAIN/AREA}. | <ul><li>Mostra i campi XDM utilizzati per rappresentare i dati del consenso.</li><li>Mostra i campi XDM utilizzati per rappresentare informazioni sugli abbonamenti e-mail.</li></ul> |
| Individuazione campo XDM per nome campo generale | <ul><li>Visualizza i campi XDM relativi a {DATA_DOMAIN/AREA}.</li><li>Quali campi XDM contengono {GENERAL_FIELD_NAME}.</li></ul> | <ul><li>Mostra i campi XDM relativi agli ordini.</li><li>Mostra i campi XDM relativi ai dettagli di interazione.</li><li>Quale campo XDM contiene gli ID visitatore?</li><li>Quale campo XDM contiene le categorie di prodotto?</li></ul> |
| Individuazione campi XDM per derivazione del modello di dati | <ul><li>Mostra tutti i campi del {FIELD_GROUP/CLASS_NAME} che contengono {GENERAL_FIELD_NAME}.</li><li>Cos’è {FIELD_GROUP/CLASS_NAME} del campo XDM {GENERAL_FIELD_NAME}?</li></ul> | <ul><li>Mostra tutti i campi del gruppo di campi che contengono i dati dei prodotti.</li><li>Mostra tutti i campi del gruppo di campi che contiene i dati di analisi.</li><li>Qual è la classe del nome del campo XDM?</li><li>Qual è la classe del campo XDM e-mail subscriptions?</li></ul> |
| Richiesta di ottenere descrizioni avanzate insieme ai nomi dei campi | {FIELD_DISCOVERY_QUERY}. Includi anche descrizioni avanzate. | <ul><li>Mostra i campi XDM utilizzati per rappresentare i dati del consenso. Includi anche la descrizione avanzata del campo.</li><li>Mostra i campi XDM relativi ai dettagli di interazione. Includi anche la descrizione avanzata del campo.</li></ul> |

{style="table-layout:auto"}