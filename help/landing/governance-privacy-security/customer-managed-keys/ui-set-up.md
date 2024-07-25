---
title: Configurare e configurare le chiavi gestite dal cliente tramite l’interfaccia utente di Platform
description: Scopri come configurare l’app CMK con il tenant di Azure e inviare l’ID della chiave di crittografia a Adobe Experience Platform.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 0%

---

# Configurare e configurare le chiavi gestite dal cliente tramite l’interfaccia utente di Platform

Questo documento descrive il processo di abilitazione della funzione chiavi gestite dal cliente (CMK) in Platform tramite l’interfaccia utente di. Per istruzioni su come completare il processo utilizzando l&#39;API, fare riferimento al [documento di installazione CMK API](./api-set-up.md).

## Prerequisiti

Per visualizzare e visitare la sezione [!UICONTROL Crittografia] in Adobe Experience Platform, è necessario aver creato un ruolo e assegnato l&#39;autorizzazione [!UICONTROL Gestione chiave gestita dal cliente] a tale ruolo. Qualsiasi utente con l&#39;autorizzazione [!UICONTROL Gestione chiave gestita dal cliente] può abilitare la CMK per la propria organizzazione.

Per ulteriori informazioni sull&#39;assegnazione di ruoli e autorizzazioni in Experience Platform, consulta la [documentazione sulla configurazione delle autorizzazioni](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Per abilitare CMK, l&#39;insieme di credenziali delle chiavi [[!DNL Azure] deve essere configurato](./azure-key-vault-config.md) con le impostazioni seguenti:

* [Abilita protezione eliminazione](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Abilita eliminazione temporanea](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurare l&#39;accesso utilizzando [!DNL Azure] il controllo dell&#39;accesso basato su ruolo](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configura un insieme di credenziali delle chiavi  [!DNL Azure] ](./azure-key-vault-config.md)

## Configurare l’app CMK {#register-app}

Dopo aver configurato l&#39;insieme di credenziali delle chiavi, il passaggio successivo consiste nel registrare l&#39;applicazione CMK che verrà collegata al tenant [!DNL Azure].

### Introduzione

Per visualizzare il dashboard [!UICONTROL Configurazioni crittografia], seleziona **[!UICONTROL Crittografia]** nell&#39;intestazione [!UICONTROL Amministrazione] della barra laterale di navigazione a sinistra.

![Dashboard di configurazione della crittografia con crittografia e scheda Chiavi gestite dal cliente evidenziate.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Seleziona **[!UICONTROL Configura]** per aprire la visualizzazione [!UICONTROL Configurazione chiavi gestite dal cliente]. Questa area di lavoro contiene tutti i valori necessari per completare i passaggi descritti di seguito ed eseguire l’integrazione con l’insieme di credenziali delle chiavi di Azure.

### Copia URL di autenticazione {#copy-authentication-url}

Per avviare il processo di registrazione, copiare l&#39;URL di autenticazione dell&#39;applicazione per l&#39;organizzazione dalla visualizzazione [!UICONTROL Configurazione chiavi gestite dal cliente] e incollarlo nell&#39;ambiente [!DNL Azure] **[!DNL Key Vault Crypto Service Encryption User]**. I dettagli su come [assegnare un ruolo](#assign-to-role) sono forniti nella sezione successiva.

Selezionare l&#39;icona Copia (![Icona Copia.](/help/images/icons/copy.png)) da [!UICONTROL URL di autenticazione applicazione].

![Visualizzazione della [!UICONTROL configurazione delle chiavi gestite dal cliente] con la sezione URL di autenticazione dell&#39;applicazione evidenziata.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Copiare e incollare l&#39;[!UICONTROL URL di autenticazione applicazione] in un browser per aprire una finestra di dialogo di autenticazione. Selezionare **[!DNL Accept]** per aggiungere l&#39;entità servizio app CMK al tenant [!DNL Azure]. La conferma dell’autenticazione ti reindirizza alla pagina di destinazione di Experience Cloud.

![Finestra di dialogo per la richiesta di autorizzazione di Microsoft con [!UICONTROL Accept] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Se disponi di più sottoscrizioni a [!DNL Microsoft Azure], potresti collegare potenzialmente l&#39;istanza Platform all&#39;insieme di credenziali delle chiavi errato. In questa situazione, è necessario sostituire la sezione `common` del nome URL di autenticazione dell&#39;applicazione con l&#39;ID di directory CMK.<br>Copiare l&#39;ID della directory CMK dalla pagina Impostazioni portale, Directory e Sottoscrizioni dell&#39;applicazione [!DNL Microsoft Azure]<br>![La pagina Impostazioni portale applicazioni, Directory e Sottoscrizioni di [!DNL Microsoft Azure] con l&#39;ID della directory evidenziato.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>Incollalo nella barra degli indirizzi del browser.<br>![Una pagina del browser Google con la sezione &#39;common&#39; dell&#39;URL di autenticazione dell&#39;applicazione evidenziata.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Assegnare l&#39;app CMK a un ruolo {#assign-to-role}

Dopo aver completato il processo di autenticazione, torna all&#39;insieme di credenziali delle chiavi [!DNL Azure] e seleziona **[!DNL Access control]** nell&#39;area di navigazione a sinistra. Da qui, seleziona **[!DNL Add]** seguito da **[!DNL Add role assignment]**.

![Dashboard [!DNL Microsoft Azure] con [!DNL Add] e [!DNL Add role assignment] evidenziati.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

Nella schermata successiva viene richiesto di scegliere un ruolo per l&#39;assegnazione. Selezionare **[!DNL Key Vault Crypto Service Encryption User]** prima di selezionare **[!DNL Next]** per continuare.

>[!NOTE]
>
>Se si dispone del livello [!DNL Managed-HSM Key Vault], è necessario selezionare il ruolo utente **[!DNL Managed HSM Crypto Service Encryption User]**.

![Dashboard [!DNL Microsoft Azure] con [!DNL Key Vault Crypto Service Encryption User] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

Nella schermata successiva, scegli **[!DNL Select members]** per aprire una finestra di dialogo nella barra a destra. Utilizzare la barra di ricerca per individuare l&#39;entità servizio per l&#39;applicazione CMK e selezionarla dall&#39;elenco. Al termine, selezionare **[!DNL Save]**.

>[!NOTE]
>
>Se l&#39;applicazione non è presente nell&#39;elenco, l&#39;entità servizio non è stata accettata nel tenant. Per assicurarsi di disporre dei privilegi corretti, rivolgersi all&#39;amministratore o al rappresentante [!DNL Azure].

È possibile verificare l&#39;applicazione confrontando l&#39;[!UICONTROL ID applicazione] fornito nella [!UICONTROL configurazione chiavi gestite dal cliente] con [!DNL Application ID] fornito nella panoramica dell&#39;applicazione [!DNL Microsoft Azure].

![La [!UICONTROL configurazione chiavi gestite dal cliente] con [!UICONTROL ID applicazione] evidenziato.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Tutti i dettagli necessari per verificare gli strumenti di Azure sono inclusi nell’interfaccia utente di Platform. Questo livello di granularità viene fornito in quanto molti utenti desiderano utilizzare altri strumenti di Azure per migliorare la propria capacità di monitorare e registrare l’accesso di queste applicazioni al proprio archivio chiavi. Comprendere questi identificatori è fondamentale a tal fine e per aiutare i servizi Adobe ad accedere alla chiave.

## Abilita la configurazione della chiave di crittografia su Experience Platform {#send-to-adobe}

Dopo aver installato l&#39;app CMK in [!DNL Azure], puoi inviare ad Adobe l&#39;identificatore della chiave di crittografia. Selezionare **[!DNL Keys]** nel menu di navigazione a sinistra, seguito dal nome della chiave che si desidera inviare.

![Dashboard di Microsoft Azure con l&#39;oggetto [!DNL Keys] e il nome della chiave evidenziato.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleziona la versione più recente della chiave e viene visualizzata la pagina dei relativi dettagli. Da qui, puoi facoltativamente configurare le operazioni consentite per la chiave.

>[!IMPORTANT]
>
>Le operazioni minime richieste per la chiave sono le autorizzazioni **[!DNL Wrap Key]** e **[!DNL Unwrap Key]**. Puoi includere [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign] e [!DNL Verify] nel caso lo desideri.

Nel campo **[!UICONTROL Identificatore chiave]** viene visualizzato l&#39;identificatore URI della chiave. Copia questo valore URI da utilizzare nel passaggio successivo.

![Dettagli della chiave del dashboard di Microsoft Azure con le sezioni [!DNL Permitted operations] e Copia URL chiave evidenziate.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Dopo aver ottenuto [!DNL Key vault URI], torna alla [!UICONTROL configurazione chiavi gestite dal cliente] e immetti un **[!UICONTROL nome configurazione]** descrittivo. Quindi, aggiungere [!DNL Key Identifier] preso dalla pagina dei dettagli della chiave di Azure all&#39;identificatore della chiave dell&#39;insieme di credenziali **[!UICONTROL Chiave]** e selezionare **[!UICONTROL Salva]**.

![Visualizzazione della [!UICONTROL configurazione delle chiavi gestite dal cliente] con [!UICONTROL nome configurazione] e [!UICONTROL sezioni dell&#39;identificatore chiave dell&#39;insieme di credenziali] evidenziate.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Sei tornato al [!UICONTROL Dashboard configurazioni di crittografia]. Lo stato della configurazione di [!UICONTROL Chiavi gestite dal cliente] è [!UICONTROL Elaborazione].

![Il dashboard [!UICONTROL Configurazioni crittografia] con [!UICONTROL Elaborazione] è evidenziato nella scheda [!UICONTROL Chiavi gestite dal cliente].](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Verificare lo stato della configurazione {#check-status}

Consenti una quantità significativa di tempo per l’elaborazione. Per verificare lo stato della configurazione, torna alla visualizzazione [!UICONTROL Configurazione chiavi gestite dal cliente] e scorri verso il basso fino allo [!UICONTROL Stato configurazione]. La barra di avanzamento è avanzata al passaggio 1 di tre e spiega che il sistema sta convalidando l’accesso di Platform all’insieme di credenziali delle chiavi.

Sono disponibili quattro stati potenziali della configurazione CMK. Essi sono i seguenti:

* Passaggio 1: verifica che Platform sia in grado di accedere all’insieme di credenziali delle chiavi.
* Passaggio 2: l’insieme di credenziali delle chiavi e il nome della chiave sono in fase di aggiunta a tutti gli archivi di dati dell’organizzazione.
* Passaggio 3: l’insieme di credenziali delle chiavi e il nome della chiave sono stati aggiunti correttamente agli archivi dati.
* `FAILED`: si è verificato un problema, principalmente relativo alla chiave, all&#39;insieme di credenziali delle chiavi o alla configurazione di app multi-tenant.

## Passaggi successivi

Completando i passaggi precedenti, hai abilitato correttamente la CMK per la tua organizzazione. I dati acquisiti negli archivi dati primari verranno ora crittografati e decrittografati utilizzando le chiavi nell&#39;insieme di credenziali delle chiavi [!DNL Azure].
