---
title: Configurare e configurare le chiavi gestite dal cliente tramite l’interfaccia utente di Platform
description: Scopri come configurare l’app CMK con il tenant di Azure e inviare l’ID della chiave di crittografia a Adobe Experience Platform.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---

# Configurare e configurare le chiavi gestite dal cliente tramite l’interfaccia utente di Platform

Questo documento descrive il processo di abilitazione della funzione chiavi gestite dal cliente (CMK) in Platform tramite l’interfaccia utente di. Per istruzioni su come completare questo processo utilizzando l’API, consulta [Documento di configurazione CMK API](./api-set-up.md).

## Prerequisiti

Per visualizzare e visitare il [!UICONTROL Crittografia] in Adobe Experience Platform, è necessario aver creato un ruolo e assegnato il [!UICONTROL Gestisci chiave gestita dal cliente] autorizzazione per quel ruolo. Qualsiasi utente che dispone di [!UICONTROL Gestisci chiave gestita dal cliente] L’autorizzazione può abilitare la CMK per la loro organizzazione.

Per ulteriori informazioni sull’assegnazione di ruoli e autorizzazioni in Experienci Platform, consulta [configurare la documentazione sulle autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=it).

Per attivare la CMK, [[!DNL Azure] L’insieme di credenziali delle chiavi deve essere configurato](./azure-key-vault-config.md) con le seguenti impostazioni:

* [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurare l’accesso tramite [!DNL Azure] controllo degli accessi basato su ruoli](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configurare un [!DNL Azure] Key Vault](./azure-key-vault-config.md)

## Configurare l’app CMK {#register-app}

Dopo aver configurato l&#39;insieme di credenziali delle chiavi, il passaggio successivo consiste nel registrare l&#39;applicazione CMK che verrà collegata al [!DNL Azure] tenant.

### Introduzione

Per visualizzare [!UICONTROL Configurazioni crittografia] dashboard, seleziona **[!UICONTROL Crittografia]** sotto [!UICONTROL Amministrazione] intestazione della barra laterale di navigazione a sinistra.

![Dashboard di configurazione della crittografia con crittografia e scheda Chiavi gestite dal cliente evidenziati.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Seleziona **[!UICONTROL Configura]** per aprire [!UICONTROL Configurazione chiavi gestite dal cliente] visualizzazione. Questa area di lavoro contiene tutti i valori necessari per completare i passaggi descritti di seguito ed eseguire l’integrazione con l’insieme di credenziali delle chiavi di Azure.

### Copia URL di autenticazione {#copy-authentication-url}

Per avviare il processo di registrazione, copia l’URL di autenticazione dell’applicazione per l’organizzazione da [!UICONTROL Configurazione chiavi gestite dal cliente] visualizzarlo e incollarlo nel [!DNL Azure] ambiente **[!DNL Key Vault Crypto Service Encryption User]**. Dettagli su come [assegna una mansione](#assign-to-role) vengono fornite nella sezione successiva.

Seleziona l’icona Copia (![Icona Copia.](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png)) da [!UICONTROL URL di autenticazione applicazione].

![Il [!UICONTROL Configurazione chiavi gestite dal cliente] visualizzazione con la sezione URL autenticazione applicazione evidenziata.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Copiare e incollare [!UICONTROL URL di autenticazione applicazione] in un browser per aprire una finestra di dialogo di autenticazione. Seleziona **[!DNL Accept]** per aggiungere l’entità del servizio app CMK al tuo [!DNL Azure] tenant. La conferma dell’autenticazione ti reindirizza alla pagina di destinazione di Experience Cloud.

![Finestra di dialogo per la richiesta di autorizzazione di Microsoft con [!UICONTROL Accetta] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Se sono presenti più [!DNL Microsoft Azure] abbonamenti, potresti potenzialmente collegare la tua istanza Platform all’insieme di credenziali delle chiavi errato. In questa situazione, devi sostituire il `common` sezione del nome URL di autenticazione dell&#39;applicazione per l&#39;ID directory CMK.<br>Copiare l&#39;ID della directory CMK dalla pagina Impostazioni portale, Directory e Sottoscrizioni del [!DNL Microsoft Azure] applicazione<br>![Il [!DNL Microsoft Azure] pagina Impostazioni del portale applicazioni, Directory e Sottoscrizioni con l&#39;ID di directory evidenziato.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Quindi, incollalo nella barra degli indirizzi del browser.<br>![Una pagina del browser Google con la sezione &quot;common&quot; dell’URL di autenticazione dell’applicazione evidenziata.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Assegnare l&#39;app CMK a un ruolo {#assign-to-role}

Dopo aver completato il processo di autenticazione, torna al [!DNL Azure] Key Vault e selezione **[!DNL Access control]** nel menu di navigazione a sinistra. Da qui, seleziona **[!DNL Add]** seguito da **[!DNL Add role assignment]**.

![Il [!DNL Microsoft Azure] dashboard con [!DNL Add] e [!DNL Add role assignment] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Nella schermata successiva viene richiesto di scegliere un ruolo per l&#39;assegnazione. Seleziona **[!DNL Key Vault Crypto Service Encryption User]** prima di selezionare **[!DNL Next]** per continuare.

![Il [!DNL Microsoft Azure] dashboard con [!DNL Key Vault Crypto Service Encryption User] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Nella schermata successiva scegliere **[!DNL Select members]** per aprire una finestra di dialogo nella barra a destra. Utilizzare la barra di ricerca per individuare l&#39;entità servizio per l&#39;applicazione CMK e selezionarla dall&#39;elenco. Al termine, seleziona **[!DNL Save]**.

>[!NOTE]
>
>Se l&#39;applicazione non è presente nell&#39;elenco, l&#39;entità servizio non è stata accettata nel tenant. Per assicurarti di disporre dei privilegi corretti, utilizza [!DNL Azure] amministratore o rappresentante.

È possibile verificare l&#39;applicazione confrontando [!UICONTROL ID applicazione] fornito il [!UICONTROL Configurazione chiavi gestite dal cliente] visualizzare con [!DNL Application ID] fornito il [!DNL Microsoft Azure] panoramica dell’applicazione.

![Il [!UICONTROL Configurazione chiavi gestite dal cliente] visualizzare con [!UICONTROL ID applicazione] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Tutti i dettagli necessari per verificare gli strumenti di Azure sono inclusi nell’interfaccia utente di Platform. Questo livello di granularità viene fornito in quanto molti utenti desiderano utilizzare altri strumenti di Azure per migliorare la propria capacità di monitorare e registrare l’accesso di queste applicazioni al proprio archivio chiavi. Comprendere questi identificatori è fondamentale a tal fine e per aiutare i servizi Adobe ad accedere alla chiave.

## Abilita la configurazione della chiave di crittografia su Experienci Platform {#send-to-adobe}

Dopo aver installato l’app CMK su [!DNL Azure], puoi inviare l’identificatore della chiave di crittografia ad Adobe. Seleziona **[!DNL Keys]** nel menu di navigazione a sinistra, seguito dal nome della chiave che desideri inviare.

![Dashboard di Microsoft Azure con [!DNL Keys] e il nome chiave evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleziona la versione più recente della chiave e viene visualizzata la pagina dei relativi dettagli. Da qui, puoi facoltativamente configurare le operazioni consentite per la chiave.

>[!IMPORTANT]
>
>Le operazioni minime richieste per la chiave sono le **[!DNL Wrap Key]** e **[!DNL Unwrap Key]** autorizzazioni. Puoi includere [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], e [!DNL Verify] dovrebbe volere.

Il **[!UICONTROL Identificatore chiave]** visualizza l’identificatore URI della chiave. Copia questo valore URI da utilizzare nel passaggio successivo.

![I dettagli della chiave del dashboard di Microsoft Azure con [!DNL Permitted operations] ed evidenziate le sezioni copia URL chiave.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Dopo aver ottenuto il [!DNL Key vault URI], torna a [!UICONTROL Configurazione chiavi gestite dal cliente] visualizza e immetti un valore descrittivo **[!UICONTROL Nome configurazione]**. Quindi, aggiungere [!DNL Key Identifier] dalla pagina dei dettagli della chiave di Azure alla pagina **[!UICONTROL Identificatore chiave di Vault]** e seleziona **[!UICONTROL Salva]**.

![Il [!UICONTROL Configurazione chiavi gestite dal cliente] visualizzare con [!UICONTROL Nome configurazione] e [!UICONTROL Identificatore chiave di Vault] sezioni evidenziate.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Viene visualizzata di nuovo la [!UICONTROL Dashboard configurazioni di crittografia]. Stato del [!UICONTROL Chiavi gestite dal cliente] la configurazione viene visualizzata come [!UICONTROL Elaborazione].

![Il [!UICONTROL Configurazioni crittografia] dashboard con [!UICONTROL Elaborazione] evidenziato su [!UICONTROL Chiavi gestite dal cliente] Card.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Verificare lo stato della configurazione {#check-status}

Consenti una quantità significativa di tempo per l’elaborazione. Per verificare lo stato della configurazione, torna a [!UICONTROL Configurazione chiavi gestite dal cliente] visualizzare e scorrere verso il basso fino a [!UICONTROL Stato configurazione]. La barra di avanzamento è avanzata al passaggio 1 di tre e spiega che il sistema sta convalidando l’accesso di Platform all’insieme di credenziali delle chiavi.

Sono disponibili quattro stati potenziali della configurazione CMK. Essi sono i seguenti:

* Passaggio 1: verifica che Platform sia in grado di accedere all’insieme di credenziali delle chiavi.
* Passaggio 2: l’insieme di credenziali delle chiavi e il nome della chiave sono in fase di aggiunta a tutti gli archivi di dati dell’organizzazione.
* Passaggio 3: l’insieme di credenziali delle chiavi e il nome della chiave sono stati aggiunti correttamente agli archivi dati.
* `FAILED`: si è verificato un problema, principalmente relativo alla chiave, all’insieme di credenziali delle chiavi o alla configurazione di app multi-tenant.

## Passaggi successivi

Completando i passaggi precedenti, hai abilitato correttamente la CMK per la tua organizzazione. I dati acquisiti negli archivi di dati primari ora vengono crittografati e decrittografati utilizzando le chiavi nella [!DNL Azure] Key Vault
