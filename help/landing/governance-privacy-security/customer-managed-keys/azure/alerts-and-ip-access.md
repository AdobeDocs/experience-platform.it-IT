---
title: Configurare il inserisco nell'elenco Consentiti di avvisi e IP per Azure CMK
description: Inserire nell'elenco Consentiti Scopri come l’indirizzo IP statico di Adobe in Azure Key Vault e come gli avvisi di Experience Platform consentono di rilevare e risolvere i problemi di accesso alle chiavi gestite dal cliente.
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Configura avvisi e inserisco nell&#39;elenco Consentiti di IP per la CMK [!DNL Azure]

Per migliorare la trasparenza, Adobe fornisce un [servizio di monitoraggio](../../../../observability/alerts/ui.md){target="_blank"} che controlla lo stato di accesso dell&#39;insieme di credenziali delle chiavi e attiva avvisi in caso di problemi. Questi avvisi consentono di rispondere rapidamente ed evitare interruzioni del servizio. Inserire nell&#39;elenco Consentiti Per abilitare questo servizio, l’indirizzo IP statico di Adobe.

>[!IMPORTANT]
>
>Se hai disabilitato l&#39;accesso alla rete pubblica o hai configurato l&#39;insieme di credenziali delle chiavi [!DNL Azure] per consentire solo alcune reti, devi aggiungere l&#39;indirizzo IP statico di Adobe al tuo inserisco nell&#39;elenco Consentiti di. In caso contrario, potresti non ricevere notifiche sui problemi di accesso che potrebbero interessare la tua istanza di Experience Platform.

## Inserire nell&#39;elenco Consentiti l&#39;IP statico di Adobe nell&#39;insieme di credenziali delle chiavi [!DNL Azure] {#add-adobe-static-ip}

Per attivare questi avvisi mantenendo le restrizioni di rete, passare a **[!DNL Azure Key Vault]** > **[!DNL Networking settings]**. Nella scheda **[!DNL Firewalls and virtual networks]**, selezionare **[!DNL Allow public access from specific virtual networks and IP addresses]**.

Schermata delle impostazioni di rete dell&#39;insieme di credenziali delle chiavi ![[!DNL Azure] che mostra dove aggiungere l&#39;indirizzo IP statico di Adobe e con l&#39;opzione Consenti accesso da evidenziata.](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Indirizzo IP statico di Adobe

>[!IMPORTANT]
>
>Indirizzo IP statico fornito da Adobe: `20.88.123.53`.

Nella sezione **[!DNL Firewall]** selezionare **[!DNL Add your current IP address]** e sostituirlo con l&#39;indirizzo IP statico di Adobe. Tutte le connessioni in uscita vengono trattate come ambienti di produzione, pertanto questo indirizzo IP statico deve essere inserito nell&#39;elenco Consentiti per garantire un accesso ininterrotto all’archivio chiavi in configurazioni di rete limitate.

>[!NOTE]
>
>Dopo aver aggiunto o aggiornato l&#39;indirizzo IP statico nelle impostazioni dell&#39;insieme di credenziali delle chiavi [!DNL Azure], attendi fino a 10 minuti per rendere effettiva la modifica. Una volta aggiunto l’IP, l’app CMK accede all’insieme di credenziali delle chiavi per verificare le autorizzazioni.

Dopo aver inserito nell&#39;elenco Consentiti l’IP statico di Adobe, Experience Platform può monitorare l’accesso all’archivio chiavi e attivare gli avvisi in caso di problemi. Questi avvisi forniscono avvisi tempestivi che consentono di intervenire prima che il servizio sia interessato. Nella sezione successiva vengono descritti i tipi di avvisi che è possibile ricevere e le modalità di risposta.

## Monitorare gli avvisi {#monitor-alerts}

Gli avvisi di Platform ti segnalano problemi che possono interrompere l&#39;accesso alla chiave, ad esempio **[!UICONTROL Errore di accesso alla chiave]** o **[!UICONTROL Disattivazione chiave]**. Questi avvisi consentono di identificare rapidamente problemi quali un IP statico rimosso o un firewall non configurato correttamente. Per ripristinare l&#39;accesso, controllare le impostazioni del firewall [!DNL Azure] e aggiungere nuovamente l&#39;indirizzo IP richiesto.

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

Iscriviti alle notifiche degli eventi di Adobe I/O per ricevere avvisi in tempo reale nei tuoi strumenti di monitoraggio. Per le istruzioni di installazione, consulta [Abbonati alle notifiche degli eventi di Adobe I/O](../../../../observability/alerts/subscribe.md). Per informazioni su come visualizzare e gestire gli avvisi in Experience Platform, consulta anche la [guida dell&#39;interfaccia utente avvisi](../../../../observability/alerts/ui.md).

## Passaggi successivi

Hai ora configurato l&#39;inserire nell&#39;elenco Consentiti degli indirizzi IP e il monitoraggio degli avvisi per l&#39;insieme di credenziali delle chiavi [!DNL Azure]. Per completare la configurazione di Chiavi gestite dal cliente in [!DNL Azure], seguire queste istruzioni di configurazione.

- [Configurare un  [!DNL Azure] insieme di credenziali delle chiavi](./azure-key-vault-config.md)
- [Utilizzare l&#39;API per configurare CMK](./api-set-up.md)
- [Utilizzare l’interfaccia utente per configurare la CMK](./ui-set-up.md)
