---
title: Riferimento risoluzione avviso CMK
description: Identifica, risolve e risolve i problemi relativi agli avvisi comuni generati da errori di configurazione della chiave gestita dal cliente (CMK) in Adobe Experience Platform. Utilizzare questa guida per seguire istruzioni chiare e dettagliate e ripristinare l'accesso con chiave sicura.
source-git-commit: 0d9cc046956dd380bb8816f0d8bf497bbad6140b
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 0%

---

# Riferimento risoluzione avvisi CMK

Utilizzare questa guida per risolvere i problemi relativi agli avvisi attivati da impostazioni di chiave gestita del cliente (CMK) non configurate correttamente in Adobe Experience Platform. Consente agli amministratori di sistema e agli specialisti dell’implementazione di identificare le cause e applicare le risoluzioni per ripristinare l’accesso sicuro.

## Categorie di avvisi {#categories}

Le sezioni seguenti descrivono i tipi di avvisi che possono essere attivati dai problemi di chiave gestita dal cliente (CMK) in Adobe Experience Platform:

- [Accesso chiave disabilitato](#key-access-disabled)
- [Errore di accesso alla chiave](#key-access-failure)
- [Notifica di avviso](#alert-notification)

## Accesso chiave disabilitato {#key-access-disabled}

Questo avviso indica che Adobe Experience Platform non è in grado di accedere alla CMK configurata perché la chiave è disabilitata o resa inaccessibile da problemi di configurazione delle chiavi correlati.

>[!IMPORTANT]
>
>In questo caso, Adobe CMK tratta il problema di accesso come una rimozione mirata e rimuoverà tutti i dati associati alla tua organizzazione in base al tuo SLA.

### Quando si verifica

Questo avviso viene attivato quando la chiave di crittografia nell&#39;insieme di credenziali delle chiavi di Azure si trova in uno stato disabilitato, eliminato o non configurato correttamente in modo da impedire l&#39;accesso durante le operazioni della piattaforma.

### Possibili cause

Di seguito sono riportati i motivi comuni per cui questo avviso può verificarsi:

- Chiave disabilitata manualmente.
- Le operazioni chiave (wrapKey/unwrapKey) sono state rimosse.
- La data di attivazione della chiave è impostata in futuro.
- La data di scadenza della chiave è nel passato.
- Chiave eliminata.
- Le autorizzazioni dell’app MultiTenant sono state rimosse o modificate.
- L’app MultiTenant è stata eliminata.
- Le proprietà dell’app MultiTenant sono state modificate.
- L&#39;insieme di credenziali delle chiavi è stato eliminato o non è più accessibile.

### Risoluzione

+++Se la chiave è disabilitata

1. Passare all&#39;[Archivio chiavi di Azure](https://portal.azure.com/) contenente la CMK.
2. Seleziona la chiave associata a Adobe Experience Platform.
3. Verificare che lo stato della chiave sia impostato su **Abilitato**.
4. Se la chiave è disabilitata, abilitarla utilizzando il portale di Azure o il comando CLI `az keyvault key enable`.

>[!NOTE]
>
>Personalizza questo comando per l’ambiente Azure.

+++

+++Se le operazioni chiave sono state modificate

1. Aggiungere nuovamente le autorizzazioni `wrapKey` e `unwrapKey` alla chiave.

>[!NOTE]
>
>Affinché la chiave funzioni, tutte le impostazioni della chiave, comprese le date di attivazione e di scadenza, devono essere valide.

+++

+++Se la data di attivazione o di scadenza non è configurata correttamente

1. Imposta la data di attivazione sul passato o sul presente.
2. Imposta la data di scadenza su una data futura.

+++

+++Se la chiave è stata eliminata

1. Verificare che l&#39;eliminazione temporanea sia abilitata nell&#39;insieme di credenziali delle chiavi di Azure.
2. Passa a &quot;Gestisci chiavi eliminate&quot; nel portale di Azure o nella CLI.
3. Seleziona la chiave eliminata dall’elenco degli elementi soft eliminati.
4. Fai clic su **Recupera** per ripristinare la chiave.

+++

+++Se le autorizzazioni per l’app MultiTenant sono state rimosse o modificate

1. Ripristina le autorizzazioni corrette per l’app MultiTenant.
2. Verificare che sia concessa la seguente autorizzazione: `Key Vault Crypto Service Encryption User`

+++

+++Se l’app MultiTenant è stata eliminata

Questo è un cambiamento rivoluzionario. Contatta Adobe per ripristinare o rigenerare l’app MultiTenant.

+++

+++Se le impostazioni dell’app MultiTenant sono state modificate

1. Ripristina le modifiche alle proprietà associate all’app MultiTenant.

+++

+++Se l’insieme di credenziali delle chiavi è stato eliminato

1. Conferma che l’eliminazione temporanea sia abilitata in Azure.
2. Passa a &quot;Gestisci archivi eliminati&quot; nel portale o CLI.
3. Recuperare l&#39;archivio eliminato entro il periodo di conservazione (7-90 giorni).
4. Se la protezione di eliminazione è disattivata, è possibile ripristinare l&#39;insieme di credenziali.

>[!NOTE]
>
>Se la protezione eliminazione temporanea o eliminazione non è configurata correttamente, la chiave o l&#39;insieme di credenziali potrebbero non essere ripristinabili.

+++

## Errore di accesso alla chiave {#key-access-failure}

Questo avviso indica che Adobe Experience Platform non è riuscito ad accedere alla CMK a causa di un rifiuto di accesso a livello di rete o basato sulla configurazione.

>[!IMPORTANT]
>
>Viene trattato come un errore recuperabile. In questo caso, i dati sono **not** eliminati in SLA.

### Quando si verifica

Questo avviso viene in genere attivato quando il firewall Key Vault non è configurato per consentire l’accesso a Adobe CMK o quando l’accesso basato su identità non riesce.

### Possibili cause

- Il firewall Key Vault sta bloccando l&#39;IP statico di Adobe (`20.88.123.53`)
- La chiave non esiste più nel percorso previsto
- Autorizzazioni mancanti per l’app Adobe MultiTenant
- L&#39;insieme di credenziali delle chiavi è stato eliminato o non configurato correttamente
- L&#39;ID oggetto dell&#39;app MultiTenant è stato modificato

### Risoluzione

+++Se l’insieme di credenziali delle chiavi o la chiave non esiste più

1. Verificare che l&#39;insieme di credenziali delle chiavi e la chiave di crittografia esistano ancora.
2. Se la chiave è stata eliminata, seguire i passaggi di recupero soft-delete in &quot;Accesso alla chiave disabilitato&quot;.

+++

+++Se le autorizzazioni dell’app MultiTenant sono mancanti o modificate

1. Conferma che l’app MultiTenant Adobe disponga delle seguenti autorizzazioni:
   - `get`, `wrapKey` e `unwrapKey` sulla chiave.
2. Verifica che l’ID dell’oggetto per l’app MultiTenant sia corretto. Se è stata modificata, applica nuovamente le autorizzazioni.

+++

+++Se il firewall blocca Adobe

1. Esamina le regole del firewall nell’insieme di credenziali delle chiavi di Azure.
2. Assicurarsi che consentano l&#39;accesso dall&#39;IP statico di Adobe: `20.88.123.53`.

>[!NOTE]
>
>Anche con le autorizzazioni corrette, un IP bloccato impedirà l’accesso alle chiavi.

+++

## Notifica di avviso {#alert-notification}

Questo avviso funge da notifica generale per la configurazione CMK o per le anomalie di accesso che non corrispondono a un tipo di errore noto.

>[!NOTE]
>
>Questo avviso può riflettere un errore interno, una configurazione errata o una condizione imprevista.

### Quando si verifica

Questo avviso viene visualizzato quando Adobe CMK rileva un problema sconosciuto, non supportato o nuovo durante l’accesso o il monitoraggio delle chiavi.

### Possibili cause

- Condizioni di rete/firewall impreviste
- Modifiche a chiavi o insiemi di credenziali non coperte da tipi di avviso predefiniti
- Interruzioni interne della rete Adobe
- Configurazione errata di Adobe non riscontrata in precedenza

### Risoluzione

+++Se la causa è sconosciuta o ambigua

1. Rivedi il messaggio di avviso per eventuali dettagli contestuali.
2. Controlla le impostazioni del firewall, dell&#39;archivio e delle chiavi per le modifiche recenti.
3. Se non viene trovata una causa chiara, contatta il supporto Adobe per assistenza.
4. Monitora i registri e il comportamento del sistema per identificare gli schemi.

+++

## Passaggi successivi

Per informazioni sull&#39;attivazione degli avvisi e sulla configurazione dell&#39;inserire nell&#39;elenco Consentiti di IP per la CMK [!DNL Azure], vedere la guida [Configurazione degli avvisi e del inserisco nell&#39;elenco Consentiti di IP per la CMK di Azure](./azure/alerts-and-ip-access.md).
