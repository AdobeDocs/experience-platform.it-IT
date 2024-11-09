---
title: Guida API per l’autorizzazione di Query Service
description: Scopri come utilizzare l’API di autorizzazione di Query Service per applicare restrizioni IP basate sulla rete per le connessioni sicure tramite SQL. Utilizza questa API per migliorare il controllo dell’accesso ai dati per i dati Adobe Experience Platform.
role: Developer
source-git-commit: f673d0d71458fe87491318f06be59719e4c9d76c
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# Guida API per l’autorizzazione di Query Service

Per applicare le restrizioni basate su IP, utilizza l’API di autorizzazione del servizio di query. L&#39;applicazione di queste misure garantisce che solo le reti e i computer client approvati possano accedere ai dati tramite SQL in Adobe Experience Platform. Questi controlli consentono di soddisfare gli standard di sicurezza più severi e forniscono al contempo il monitoraggio e l&#39;avviso degli accessi in tempo reale.

Con questa API, puoi configurare, applicare e monitorare le restrizioni IP per l’accesso ai dati tramite l’interfaccia SQL. Questo documento fornisce una panoramica di alto livello delle funzioni principali dell’API, delle funzioni endpoint e delle funzionalità future.

## Funzioni chiave

Le seguenti funzionalità consentono di definire restrizioni di accesso basate su IP, monitorare i tentativi di accesso e personalizzare le impostazioni di sicurezza di rete per Query Service:

- **Definire i controlli di accesso ai dati basati sulla rete**: specificare gli intervalli IP consentiti per l&#39;accesso a Query Service. Questa restrizione si applica in modo specifico alle connessioni al database SQL, incluse quelle effettuate tramite strumenti di Business Intelligence (BI), client di database o interfacce di programmazione come JDBC.
- **Attiva monitoraggio completo e avvisi**: tutti i tentativi di accesso, incluse le connessioni negate, vengono registrati e inviati ai [registri di controllo di Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md) per il monitoraggio in tempo reale. Utilizzare questa funzionalità per monitorare i pattern di accesso e rilevare potenziali violazioni della sicurezza.
- **Configurare le restrizioni IP flessibili**: specificare gli IP consentiti nei singoli formati di blocco IP e CIDR. Queste impostazioni si applicano a ogni sandbox e consentono di personalizzare le restrizioni di rete in base alle esigenze di sicurezza specifiche.

## Funzionalità di controllo e monitoraggio

Per supportare le procedure di accesso ai dati protette, Query Service registra tutti gli IP client che accedono o tentano di accedere ad AEP. Gli eventi di controllo, comprese le connessioni negate, vengono inviati ai registri di controllo della piattaforma. Ciò consente di:

- **Monitoraggio in tempo reale**: tieni traccia dei modelli di accesso basati su IP per garantire la conformità.
- **Avvisi sull&#39;accesso non autorizzato**: identifica e risponde ai tentativi di accesso da IP non autorizzati.

Per ulteriori dettagli sulla registrazione di controllo, consulta la [documentazione del servizio di controllo](https://experienceleague.adobe.com/docs/experience-platform/audit/audit-overview.html).

## Passaggi successivi

Inizia a usare l&#39;API di autorizzazione di Query Service consultando la [Guida introduttiva](./getting-started.md) per i passaggi di configurazione essenziali, incluse le intestazioni richieste e le convenzioni di chiamata API. Quindi, esplora le guide specifiche per l&#39;endpoint in [Accesso IP](./ip-access.md) e [Convalida IP](./validate.md) per configurare e gestire l&#39;accesso sicuro ai dati.
