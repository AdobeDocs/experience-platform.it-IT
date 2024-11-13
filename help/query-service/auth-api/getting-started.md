---
keywords: Experience Platform; Query Service; controllo dell’accesso IP; autorizzazione; API; guida introduttiva
title: Guida API per l’autorizzazione di Query Service
description: Scopri come iniziare a richiedere l’autorizzazione e le restrizioni dell’intervallo IP per l’accesso sicuro ai dati in Adobe Experience Platform Query Service.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 6%

---

# Guida API di autorizzazione di Query Service

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il componente aggiuntivo Data Distiller. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

L’API di autorizzazione di Query Service offre alle organizzazioni un controllo più rigoroso sull’accesso ai dati tramite l’interfaccia SQL in Adobe Experience Platform. Puoi utilizzare questa API per definire le restrizioni IP, limitare l’accesso ai dati a reti specifiche e migliorare il monitoraggio della sicurezza.

Questa guida illustra come impostare le credenziali e le autorizzazioni di autorizzazione necessarie per effettuare chiamate all’API di autorizzazione di Query Service.

## Introduzione {#getting-started}

Le sezioni seguenti forniscono informazioni sulla preparazione dei valori di autorizzazione richiesti e sull’esecuzione delle prime richieste all’API di autorizzazione di Query Service.

### Autorizzazioni richieste {#required-permissions}

Per abilitare le restrizioni di accesso ai dati protetti in Query Service, devi disporre dell&#39;autorizzazione **[!UICONTROL Gestisci Elenco Consentiti]**. Questa autorizzazione consente alle organizzazioni di definire intervalli IP specifici (in formato IPv4 o IPv6) autorizzati ad accedere ai dati in Platform tramite l’interfaccia SQL. L’accesso viene gestito a livello di sandbox, dove gli utenti possono configurare un elenco di indirizzi IP approvati o blocchi CIDR che limitano l’accesso solo alle reti consentite.

>[!NOTE]
>
>Gli amministratori di sistema possono impostare le autorizzazioni utente dall&#39;Adobe [Admin Console](https://adminconsole.adobe.com/). Per ulteriori informazioni, consulta la [Guida utente di Admin Console](https://helpx.adobe.com/it/enterprise/using/admin-console.html).

Le funzionalità seguenti sono disponibili con l&#39;autorizzazione **[!UICONTROL Gestisci Elenco Consentiti]**:

- **Definire gli intervalli IP consentiti**: solo gli indirizzi IP o i blocchi CIDR di questi intervalli definiti possono accedere ai dati in Platform utilizzando SQL tramite Query Service.
- **Applica controlli intervallo IP**: le connessioni da IP che non rientrano negli intervalli consentiti vengono negate.
- **Funzionalità di controllo e avvisi**: tutti i tentativi di accesso, incluse le connessioni negate, vengono registrati come eventi di controllo. Questi eventi sono disponibili nei [registri di controllo di Adobe Experience Platform](../../landing/governance-privacy-security/audit-logs/overview.md), che consentono il monitoraggio di potenziali violazioni della sicurezza.

### Raccogliere i valori per le intestazioni richieste {#gather-values-for-required-headers}

Per effettuare chiamate all&#39;API di autorizzazione di Query Service, devi completare l&#39;[esercitazione sull&#39;autenticazione API di Platform](../../landing/api-authentication.md), che fornisce i valori per le intestazioni richieste nelle chiamate API. Includi le seguenti intestazioni in ogni richiesta:

- **Autorizzazione**: `Bearer {ACCESS_TOKEN}`
- **x-api-key**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-sandbox-name**: `{SANDBOX_NAME}`

>[!NOTE]
>
> Per ulteriori informazioni sulle sandbox, consulta la [documentazione di panoramica sulle sandbox](../../sandboxes/home.md).

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono anche questa intestazione:

- **Tipo di contenuto**: `application/json`

### Passaggi successivi

Una volta raccolte le autorizzazioni richieste e i valori di intestazione, puoi iniziare a configurare le restrizioni IP per Query Service. Procedi alla documentazione dell’endpoint per esempi dettagliati di operazioni CRUD, che includono:

- Formato API e coppie di richiesta/risposta di esempio.
- Intestazioni, payload e codici di risposta per ogni operazione.

Ogni esempio di chiamata API illustra come formattare le richieste e interpretare le risposte, per consentire di applicare un accesso sicuro ai dati in Query Service.

Per istruzioni specifiche sulla configurazione e la convalida delle restrizioni IP, consulta la [documentazione dell&#39;endpoint di accesso IP](./ip-access.md) e la [documentazione dell&#39;endpoint di convalida IP](./validate.md).
