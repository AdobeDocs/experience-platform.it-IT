---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketing da coinvolgere;marketo
solution: Experience Platform
title: Autenticazione del connettore sorgente Marketo
topic-legacy: overview
description: Questo documento fornisce informazioni su come generare le credenziali di autenticazione Marketo.
translation-type: tm+mt
source-git-commit: f12baaa9d4b37f1101792a4ae479b5a62893eb68
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---


# (Beta) Autentica il connettore di origine [!DNL Marketo Engage]

>[!IMPORTANT]
>
>La sorgente [!DNL Marketo Engage] è attualmente in versione beta. Le sue funzioni e la sua documentazione sono soggette a modifiche.

Prima di poter creare un connettore di origine [!DNL Marketo Engage] (in seguito denominato &quot;[!DNL Marketo]&quot;), è necessario impostare un servizio personalizzato tramite l&#39;interfaccia [!DNL Marketo] e recuperare i valori per l&#39;ID Munchkin, l&#39;ID client e il segreto client.

La documentazione seguente fornisce passaggi su come acquisire le credenziali di autenticazione per creare un connettore di origine [!DNL Marketo].

## Configurare un nuovo ruolo

Il primo passaggio nell&#39;acquisizione delle credenziali di autenticazione consiste nell&#39;impostare un nuovo ruolo tramite l&#39;interfaccia [[!DNL Marketo]](https://app-sjint.marketo.com/#MM0A1).

Accedi a [!DNL Marketo] e seleziona **[!DNL Admin]** dalla barra di navigazione superiore.

![Amministratore per un nuovo ruolo](../images/marketo/home.png)

La pagina *[!DNL Users & Role]s* contiene informazioni su utenti, ruoli e cronologia di accesso. Per creare un nuovo ruolo, seleziona **[!DNL Roles]** dall’intestazione superiore, quindi seleziona **[!DNL New Role]**.

![nuovo ruolo](../images/marketo/new-role.png)

Viene visualizzata la finestra di dialogo **[!DNL Create New Role]**. Immetti un nome e una descrizione, quindi seleziona le autorizzazioni da concedere per questo ruolo. Le autorizzazioni sono limitate a aree di lavoro specifiche e gli utenti possono eseguire azioni solo nelle aree di lavoro in cui dispongono delle autorizzazioni.

Dopo aver selezionato le autorizzazioni da concedere, seleziona **[!DNL Create]**.

![create-new-role](../images/marketo/create-new-role.png)

Puoi gestire le autorizzazioni limitate sull&#39;API durante la creazione di ruoli con [!DNL Marketo]. Invece di selezionare &quot;Access API&quot; (API di accesso), puoi fornire un ruolo con il livello minimo di accesso selezionando le seguenti autorizzazioni:

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

## Configurare un nuovo utente

Analogamente ai ruoli, puoi impostare un nuovo utente dalla pagina **[!DNL Users & Roles]** . La pagina **[!DNL Users]** fornisce un elenco degli utenti attivi attualmente in provisioning in Marketo. Seleziona **[!DNL Invite New User]** per eseguire il provisioning di un nuovo utente.

![invitare-new-user](../images/marketo/invite-new-user.png)

Viene visualizzato un menu di dialogo di selezione. Fornisci le informazioni appropriate per l’e-mail, il nome, il cognome e il motivo. Durante questo passaggio, puoi anche stabilire una data di scadenza per l’accesso al nuovo account utente che stai invitando. Al termine, seleziona **[!DNL Next]**.

>[!IMPORTANT]
>
>Quando imposti un nuovo utente, devi assegnare l’accesso a un utente che è strettamente dedicato al servizio personalizzato che stai creando.

![informazioni utente](../images/marketo/new-user-info.png)

Seleziona i campi appropriati nel passaggio **[!DNL Permissions]** , quindi seleziona la casella di controllo **[!DNL API Only]** per fornire un ruolo API al nuovo utente. Selezionare **[!DNL Next]** per continuare.

![permissions](../images/marketo/permissions.png)

Per completare il processo, selezionare **[!DNL Send]**.

![message](../images/marketo/message.png)

## Configurare un servizio personalizzato

Una volta stabilito un nuovo utente, puoi impostare un servizio personalizzato per recuperare le nuove credenziali. Dalla pagina di amministrazione, seleziona **[!DNL LaunchPoint]**.

![admin-launchpoint](../images/marketo/admin-launchpoint.png)

La pagina **[!DNL Installed services]** contiene un elenco di servizi esistenti e, per creare un nuovo servizio personalizzato, seleziona **[!DNL New]**, quindi seleziona **[!DNL New Service]**.

![nuovo servizio](../images/marketo/new-service.png)

Fornisci al nuovo servizio un nome visualizzato descrittivo, quindi seleziona **[!DNL Custom]** dal menu a discesa **[!DNL Service]** . Fornisci una descrizione appropriata, quindi seleziona l’utente a cui desideri eseguire il provisioning dal menu a discesa **[!DNL API Only User]** . Dopo aver compilato i dettagli necessari, seleziona **[!DNL Create]** per creare il nuovo servizio personalizzato.

![creare](../images/marketo/create.png)

## Ottieni il tuo ID client e il segreto client

Con la creazione di un nuovo servizio personalizzato, ora puoi recuperare i valori per l’ID client e il segreto client. Dal menu **[!DNL Installed Services]**, individua il servizio personalizzato a cui vuoi accedere e seleziona **[!DNL View Details]**.

![visualizza dettagli](../images/marketo/view-details.png)

Viene visualizzata una finestra di dialogo contenente l’ID client e il segreto client.

![credenziali](../images/marketo/credentials.png)

## Ottieni l&#39;ID Munchkin

Il passaggio finale da completare per autenticare il connettore di origine [!DNL Marketo] consiste nel recuperare l&#39;ID Munchkin. Dalla pagina di amministrazione, seleziona **[!DNL Munchkin]** nel pannello **[!DNL Integration]** .

![admin-munchkin](../images/marketo/admin-munchkin.png)

Viene visualizzata la pagina *[!DNL Munchkin]* con il tuo ID Munchkin univoco elencato nella parte superiore del pannello.

![munchkin-Id](../images/marketo/munchkin-id.png)

Insieme all&#39;ID client e al segreto client, puoi utilizzare il tuo ID Munchkin per configurare un nuovo account e [creare una nuova connessione [!DNL Marketo] sorgente](../../../tutorials/ui/create/adobe-applications/marketo.md) all&#39;Experience Platform.
