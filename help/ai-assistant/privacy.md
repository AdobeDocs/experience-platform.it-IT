---
title: Privacy, sicurezza e governance nell’Assistente di IA
description: Scopri le procedure di privacy, sicurezza e governance per l’Assistente IA.
hide: true
hidefromtoc: true
source-git-commit: 723638fcd580c81a84ffe6bf38c197c62fabc1f3
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Privacy, sicurezza e governance nell’Assistente di IA

L’Assistente per l’intelligenza artificiale in Adobe Experience Platform è stato progettato con privacy, sicurezza e governance in primo piano.

Leggi questo documento per scoprire le funzionalità incentrate sulla fiducia dei clienti che puoi aspettarti dall’Assistente AI:

* Nessun dato personale viene utilizzato oggi da AI Assistant, anche a scopo di formazione.
* L’Assistente AI non è a conoscenza dei dati del consumatore.
* Tutti gli esistenti [controllo degli accessi](../access-control/home.md) I criteri saranno rispettati dall’Assistente IA.
   * Il controllo dell&#39;accesso a livello di oggetto è supportato per gli oggetti. Il supporto per il controllo dell’accesso a livello di oggetto per gli attributi sarà presto disponibile.
   * Eventuali nuovi criteri di controllo dell’accesso basati su attributi vengono rispecchiati in IA Assistant dopo un massimo di 24 ore*
* Per interagire con l&#39;Assistente AI è necessario disporre dell&#39;autorizzazione esplicita.
   * È possibile impostare le autorizzazioni in modo diverso, ad Experience Platform per Journey Optimizer utilizzando [Interfaccia utente autorizzazioni](../access-control/abac/ui/permissions.md) e puoi utilizzare il [Admin Console](../access-control/ui/browse.md) per assegnare le autorizzazioni per il Customer Journey Analytics.
   * Le autorizzazioni sono granulari e l’amministratore della sandbox può configurare quali dei tuoi utenti possono porre diverse categorie di domande (domande basate sulla conoscenza del prodotto con l’Assistente AI o domande sulle informazioni operative).
* L&#39;Assistente AI è una funzione compatibile con HIPAA e soddisfa i requisiti HIPAA relativi all&#39;elaborazione e all&#39;utilizzo di informazioni sanitarie protette (PHI).
* È possibile visualizzare un registro delle interazioni precedenti con l’Assistente AI con un criterio di conservazione di 30 giorni.
* L’Assistente AI si basa su dati specifici delle sandbox e su documentazione pubblica di Adobe per rispondere alle richieste degli utenti. I dati non sono condivisi tra sandbox diverse.
* I prompt forniti all&#39;Assistente IA non vengono condivisi con altri clienti.


**Ciò significa che se vengono aggiunte nuove etichette a campi e oggetti o vengono creati nuovi criteri, l’Assistente AI impiegherà fino a 24 ore per rispettarli. Durante queste 24 ore, gli utenti con accesso limitato di recente possono comunque accedere a tali campi e oggetti.*