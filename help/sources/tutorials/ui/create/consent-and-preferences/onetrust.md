---
keywords: Experience Platform;home;argomenti popolari;onetrust;OneTrust
solution: Experience Platform
title: (Beta) Creare una connessione sorgente OneTrust nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine OneTrust utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 0%

---

# (Beta) Creare un [!DNL OneTrust Integration] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL OneTrust Integration] sorgente in versione beta. Le sue funzioni e la sua documentazione sono soggette a modifiche. Per informazioni sull&#39;utilizzo di fonti con etichetta beta, vedere [panoramica sulle origini](../../../../home.md#terms-and-conditions).

Questo tutorial descrive i passaggi necessari per creare [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) connessione di origine per acquisire in Adobe Experience Platform dati di consenso storici e pianificati tramite l’interfaccia utente di Platform.

## Prerequisiti

>[!IMPORTANT]
>
>Il [!DNL OneTrust Integration] il connettore di origine e la documentazione sono stati creati da [!DNL OneTrust Integration] team. Per ulteriori informazioni o richieste di aggiornamento, contattare [[!DNL OneTrust] team](https://my.onetrust.com/s/contactsupport?language=en_US) direttamente.

Prima di connettersi [!DNL OneTrust Integration] in Platform, devi prima recuperare il token di accesso. Per istruzioni dettagliate su come trovare il token di accesso, vedi [[!DNL OneTrust Integration] Guida di OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Il token di accesso non viene aggiornato automaticamente dopo la scadenza perché i token di aggiornamento da sistema a sistema non sono supportati da [!DNL OneTrust]. Pertanto, è necessario assicurarsi che il token di accesso sia aggiornato nella connessione prima della scadenza. La durata massima configurabile per un token di accesso è di un anno. Per ulteriori informazioni sull’aggiornamento del token di accesso, consulta [[!DNL OneTrust] documento sulla gestione delle credenziali client OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Raccogli le credenziali richieste

Per connettersi [!DNL OneTrust Integration] In Platform, devi fornire i valori per le seguenti credenziali di autenticazione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Nome host | L&#39;ambiente da cui è stato [!DNL OneTrust Integration] è necessario estrarre i dati da. | `https://uat.onetrust.com/` |
| URL test di autorizzazione | (Facoltativo) L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non vengono fornite, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |  |
| Token di accesso | Il token di accesso corrispondente al [!DNL OneTrust Integration] account. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Per ulteriori informazioni su queste credenziali, vedere [[!DNL OneTrust Integration] documentazione di autenticazione](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Connetti [!DNL OneTrust Integration] account

>[!NOTE]
>
>Il [!DNL OneTrust Integration] Le specifiche API vengono condivise con Adobe per l’acquisizione dei dati.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *[!UICONTROL Consenso e preferenze]* categoria, seleziona [!DNL OneTrust Integration], quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/onetrust/catalog.png)

Il **[!UICONTROL Connetti account di integrazione OneTrust]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL OneTrust Integration] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/onetrust/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/onetrust/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL OneTrust Integration] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati sul consenso in Platform](../../dataflow/consent-and-preferences.md).
