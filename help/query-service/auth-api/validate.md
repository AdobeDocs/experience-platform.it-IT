---
keywords: Experience Platform; sicurezza; accesso ip; convalida; guida API; servizio query; verifica IP
title: Endpoint di convalida IP
description: Scopri come convalidare l’accesso IP per le sandbox in Query Service utilizzando l’endpoint API di convalida IP.
role: Developer
exl-id: 4ce9ab1c-e333-4ed5-a430-43ffec36a46d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 4%

---

# Endpoint di convalida IP

>[!AVAILABILITY]
>
>Questa funzionalità è disponibile per i clienti che hanno acquistato il componente aggiuntivo Data Distiller. Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

Utilizza l’endpoint API di convalida IP per verificare se a un indirizzo IP specificato è consentito l’accesso a una sandbox designata in Query Service. Questo controllo conferma se si applicano restrizioni di accesso o se a un indirizzo IP è consentito l’accesso ai dati all’interno di una sandbox.

## Convalida IP per accesso sandbox {#validate-ip-for-sandbox-access}

Utilizzare l&#39;endpoint di convalida IP per verificare se a un determinato indirizzo IP è consentito l&#39;accesso ai dati per la sandbox specificata. Se per la sandbox non è configurata alcuna restrizione IP, per impostazione predefinita sono consentiti tutti gli indirizzi IP. Se esistono restrizioni IP o CIDR, questa API verifica se l’indirizzo IP specificato corrisponde a eventuali intervalli configurati.

>[!NOTE]
>
>Puoi accedere a questo endpoint con **token utente** o **token servizio**. Non sono necessari requisiti di ruolo specifici.

**Formato API**

```http
POST /security/validate/ip-access
```

**Richiesta**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un valore booleano che indica se l’IP è consentito.

>[!NOTE]
>
>Il campo `isAllowed` nella risposta restituisce `true` se all&#39;IP fornito è consentito l&#39;accesso alla sandbox e `false` in caso contrario. Questa API supporta la convalida dinamica dell’accesso e la garanzia di conformità in materia di sicurezza per gli ambienti sandbox.

```json
{
"isAllowed": true
}
```
