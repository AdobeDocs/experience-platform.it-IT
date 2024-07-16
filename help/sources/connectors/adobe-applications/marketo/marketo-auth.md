---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketo;marketo;home;popular topic;system;marketo engagement;marketo
solution: Experience Platform
title: Autentica il connettore di origine Marketo
description: Questo documento fornisce informazioni su come generare le credenziali di autenticazione di Marketo.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Autentica il connettore di origine [!DNL Marketo Engage]

Prima di poter creare un connettore di origine [!DNL Marketo Engage] (di seguito denominato &quot;[!DNL Marketo]&quot;), è necessario innanzitutto impostare un servizio personalizzato tramite l&#39;interfaccia [!DNL Marketo] e recuperare i valori per l&#39;ID Munchkin, l&#39;ID client e il segreto client.

La documentazione seguente descrive i passaggi necessari per acquisire le credenziali di autenticazione e creare un connettore di origine [!DNL Marketo].

## Imposta un nuovo ruolo

Il primo passaggio per l&#39;acquisizione delle credenziali di autenticazione consiste nell&#39;impostare un nuovo ruolo tramite l&#39;interfaccia [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1).

Accedi a [!DNL Marketo] e seleziona **[!DNL Admin]** dalla barra di navigazione superiore.

![Amministratore per un nuovo ruolo](../images/marketo/home.png)

La pagina *[!DNL Users & Role]s* contiene informazioni su utenti, ruoli e cronologie di accesso. Per creare un nuovo ruolo, selezionare **[!DNL Roles]** dall&#39;intestazione superiore, quindi selezionare **[!DNL New Role]**.

![nuovo-ruolo](../images/marketo/new-role.png)

Verrà visualizzata la finestra di dialogo **[!DNL Create New Role]**. Specifica un nome e una descrizione, quindi seleziona le autorizzazioni da concedere per questo ruolo. Le autorizzazioni sono limitate a specifiche aree di lavoro e gli utenti possono eseguire solo azioni nelle aree di lavoro per le quali dispongono delle autorizzazioni.

Dopo aver selezionato le autorizzazioni da concedere, selezionare **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

È possibile gestire le autorizzazioni limitate nell&#39;API durante la creazione di ruoli con [!DNL Marketo]. Invece di selezionare &quot;Access API&quot; (API di accesso), puoi fornire a un ruolo il livello minimo di accesso selezionando le seguenti autorizzazioni:

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

Analogamente ai ruoli, è possibile impostare un nuovo utente dalla pagina **[!DNL Users & Roles]**. La pagina **[!DNL Users]** fornisce un elenco degli utenti attivi attualmente con provisioning in Marketo. Selezionare **[!DNL Invite New User]** per eseguire il provisioning di un nuovo utente.

![invita-nuovo-utente](../images/marketo/invite-new-user.png)

Viene visualizzato un menu di dialogo a comparsa. Fornisci le informazioni appropriate per e-mail, nome, cognome e motivo. Durante questo passaggio, puoi anche stabilire una data di scadenza per l’accesso al nuovo account utente che stai invitando. Al termine, selezionare **[!DNL Next]**.

>[!IMPORTANT]
>
>Quando configuri un nuovo utente, devi assegnare l’accesso a un utente dedicato esclusivamente al servizio personalizzato che stai creando.

![info-utente](../images/marketo/new-user-info.png)

Selezionare i campi appropriati nel passaggio **[!DNL Permissions]**, quindi selezionare la casella di controllo **[!DNL API Only]** per fornire un ruolo API al nuovo utente. Selezionare **[!DNL Next]** per continuare.

![autorizzazioni](../images/marketo/permissions.png)

Per completare il processo, selezionare **[!DNL Send]**.

![messaggio](../images/marketo/message.png)

## Configurare un servizio personalizzato

Dopo aver stabilito un nuovo utente, puoi impostare un servizio personalizzato per recuperare le nuove credenziali. Dalla pagina di amministrazione, selezionare **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

La pagina **[!DNL Installed services]** contiene un elenco dei servizi esistenti. Per creare un nuovo servizio personalizzato, selezionare **[!DNL New]**, quindi selezionare **[!DNL New Service]**.

![new-service](../images/marketo/new-service.png)

Fornisci al nuovo servizio un nome visualizzato descrittivo, quindi seleziona **[!DNL Custom]** dal menu a discesa **[!DNL Service]**. Fornire una descrizione appropriata, quindi selezionare l&#39;utente di cui si desidera eseguire il provisioning dal menu a discesa **[!DNL API Only User]**. Dopo aver inserito i dettagli necessari, selezionare **[!DNL Create]** per creare il nuovo servizio personalizzato.

![crea](../images/marketo/create.png)

## Ottieni l’ID client e il segreto client

Con il nuovo servizio personalizzato creato, ora puoi recuperare i valori per l’ID client e il segreto client. Individuare il servizio personalizzato a cui si desidera accedere dal menu **[!DNL Installed Services]**, quindi selezionare **[!DNL View Details]**.

![dettagli-visualizzazione](../images/marketo/view-details.png)

Viene visualizzata una finestra di dialogo contenente l’ID client e il segreto client.

![credenziali](../images/marketo/credentials.png)

## Ottieni il tuo ID Munchkin

Per autenticare il connettore di origine [!DNL Marketo], è necessario completare l&#39;ultimo passaggio: recuperare l&#39;ID Munchkin. Dalla pagina di amministrazione, seleziona **[!DNL Munchkin]** nel pannello **[!DNL Integration]**.

![admin-munchkin](../images/marketo/admin-munchkin.png)

Viene visualizzata la pagina *[!DNL Munchkin]* con l&#39;ID Munchkin univoco elencato nella parte superiore del pannello.

![munchkin-Id](../images/marketo/munchkin-id.png)

In combinazione con l&#39;ID client e il segreto client, puoi utilizzare l&#39;ID Munchkin per configurare un nuovo account e [creare una nuova [!DNL Marketo] connessione di origine](../../../tutorials/ui/create/adobe-applications/marketo.md) su Experience Platform.
