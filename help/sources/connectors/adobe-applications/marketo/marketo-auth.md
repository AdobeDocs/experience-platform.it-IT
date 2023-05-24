---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketo;marketo;home;popular topic;system;marketo engagement;marketo
solution: Experience Platform
title: Autentica il connettore di origine Marketo
description: Questo documento fornisce informazioni su come generare le credenziali di autenticazione di Marketo.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Autentica il tuo [!DNL Marketo Engage] connettore di origine

Prima di creare un [!DNL Marketo Engage] (in seguito denominati &quot;[!DNL Marketo]&quot;) è necessario prima impostare un servizio personalizzato tramite il [!DNL Marketo] e recuperare i valori per l&#39;ID Munchkin, l&#39;ID client e il segreto client.

La documentazione seguente descrive i passaggi necessari per acquisire le credenziali di autenticazione e creare un [!DNL Marketo] connettore di origine.

## Imposta un nuovo ruolo

Il primo passaggio nell’acquisizione delle credenziali di autenticazione consiste nell’impostare un nuovo ruolo tramite [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1) di rete.

Accedi a [!DNL Marketo] e seleziona **[!DNL Admin]** dalla barra di navigazione superiore.

![Amministratore per un nuovo ruolo](../images/marketo/home.png)

Il *[!DNL Users & Role]s* Questa pagina contiene informazioni su utenti, ruoli e cronologie di accesso. Per creare un nuovo ruolo, seleziona **[!DNL Roles]** dall’intestazione in alto, quindi seleziona **[!DNL New Role]**.

![new-role](../images/marketo/new-role.png)

Viene visualizzata la finestra di dialogo **[!DNL Create New Role]**. Specifica un nome e una descrizione, quindi seleziona le autorizzazioni da concedere per questo ruolo. Le autorizzazioni sono limitate a specifiche aree di lavoro e gli utenti possono eseguire solo azioni nelle aree di lavoro per le quali dispongono delle autorizzazioni.

Dopo aver selezionato le autorizzazioni che desideri concedere, seleziona **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

Puoi gestire le autorizzazioni limitate nell’API quando crei ruoli con [!DNL Marketo]. Invece di selezionare &quot;Access API&quot; (API di accesso), puoi fornire a un ruolo il livello minimo di accesso selezionando le seguenti autorizzazioni:

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## Configura un nuovo utente

Analogamente ai ruoli, è possibile impostare un nuovo utente dal **[!DNL Users & Roles]** pagina. Il **[!DNL Users]** fornisce un elenco degli utenti attivi attualmente con provisioning in Marketo. Seleziona **[!DNL Invite New User]** per effettuare il provisioning di un nuovo utente.

![invita-nuovo-utente](../images/marketo/invite-new-user.png)

Viene visualizzato un menu di dialogo a comparsa. Fornisci le informazioni appropriate per e-mail, nome, cognome e motivo. Durante questo passaggio, puoi anche stabilire una data di scadenza per l’accesso al nuovo account utente che stai invitando. Al termine, seleziona **[!DNL Next]**.

>[!IMPORTANT]
>
>Quando configuri un nuovo utente, devi assegnare l’accesso a un utente dedicato esclusivamente al servizio personalizzato che stai creando.

![user-info](../images/marketo/new-user-info.png)

Seleziona i campi appropriati nella sezione **[!DNL Permissions]** e quindi selezionare il **[!DNL API Only]** per fornire un ruolo API al nuovo utente. Seleziona **[!DNL Next]** per procedere.

![autorizzazioni](../images/marketo/permissions.png)

Per completare il processo, seleziona **[!DNL Send]**.

![messaggio](../images/marketo/message.png)

## Configurare un servizio personalizzato

Dopo aver stabilito un nuovo utente, puoi impostare un servizio personalizzato per recuperare le nuove credenziali. Dalla pagina di amministrazione, seleziona **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

Il **[!DNL Installed services]** contiene un elenco dei servizi esistenti; per creare un nuovo servizio personalizzato, seleziona **[!DNL New]** e quindi seleziona **[!DNL New Service]**.

![new-service](../images/marketo/new-service.png)

Fornisci al nuovo servizio un nome visualizzato descrittivo, quindi seleziona **[!DNL Custom]** dal **[!DNL Service]** menu a discesa. Fornisci una descrizione appropriata, quindi seleziona l’utente da attivare dal menu **[!DNL API Only User]** menu a discesa. Dopo aver inserito i dettagli necessari, seleziona **[!DNL Create]** per creare il nuovo servizio personalizzato.

![create](../images/marketo/create.png)

## Ottieni l’ID client e il segreto client

Con il nuovo servizio personalizzato creato, ora puoi recuperare i valori per l’ID client e il segreto client. Dalla sezione **[!DNL Installed Services]** , individuare il servizio personalizzato a cui si desidera accedere e quindi selezionare **[!DNL View Details]**.

![view-details](../images/marketo/view-details.png)

Viene visualizzata una finestra di dialogo contenente l’ID client e il segreto client.

![credenziali](../images/marketo/credentials.png)

## Ottieni il tuo ID Munchkin

Il passaggio finale da completare per autenticare il [!DNL Marketo] Il connettore di origine deve recuperare l&#39;ID Munchkin. Dalla pagina di amministrazione, seleziona **[!DNL Munchkin]** sotto **[!DNL Integration]** pannello.

![admin-munchkin](../images/marketo/admin-munchkin.png)

Il *[!DNL Munchkin]* con il tuo ID Munchkin univoco elencato nella parte superiore del pannello.

![munchkin-Id](../images/marketo/munchkin-id.png)

Insieme all&#39;ID client e al segreto client, puoi utilizzare l&#39;ID Munchkin per configurare un nuovo account e [crea un nuovo [!DNL Marketo] connessione sorgente](../../../tutorials/ui/create/adobe-applications/marketo.md) su Experience Platform.
