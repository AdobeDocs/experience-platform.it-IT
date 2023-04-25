---
keywords: Experience Platform;home;argomenti popolari;onetrust;OneTrust
solution: Experience Platform
title: Creare una connessione di origine OneTrust nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente OneTrust utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Crea un [!DNL OneTrust Integration] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>La [!DNL OneTrust Integration] source supporta solo l’acquisizione di dati di consenso e preferenze e non di cookie.

Questa esercitazione fornisce i passaggi per la creazione di un [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) la connessione sorgente per l’acquisizione di dati di consenso storici e pianificati in Adobe Experience Platform tramite l’interfaccia utente di Platform.

## Prerequisiti

>[!IMPORTANT]
>
>La [!DNL OneTrust Integration] il connettore di origine e la documentazione sono stati creati da [!DNL OneTrust Integration] squadra. Per qualsiasi richiesta di informazioni o aggiornamento, contatta il [[!DNL OneTrust] team](https://my.onetrust.com/s/contactsupport?language=en_US) direttamente.

Prima di poterti connettere [!DNL OneTrust Integration] su Platform, devi prima recuperare il token di accesso. Per istruzioni dettagliate su come trovare il token di accesso, consulta [[!DNL OneTrust Integration] Guida di OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Il token di accesso non si aggiorna automaticamente dopo la scadenza perché i token di aggiornamento da sistema a sistema non sono supportati da [!DNL OneTrust]. Pertanto, è necessario assicurarsi che il token di accesso sia aggiornato nella connessione prima della scadenza. La durata massima configurabile per un token di accesso è di un anno. Per ulteriori informazioni sull’aggiornamento del token di accesso, consulta la [[!DNL OneTrust] documento sulla gestione delle credenziali client OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Raccogli credenziali richieste

Per connettersi [!DNL OneTrust Integration] su Platform, devi fornire i valori per le seguenti credenziali di autenticazione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Nome host | L&#39;ambiente da cui [!DNL OneTrust Integration] i dati devono essere estratti da . | `app.onetrust.com` |
| URL del test di autorizzazione | (Facoltativo) L&#39;URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non viene fornito, le credenziali vengono automaticamente controllate durante il passaggio di creazione della connessione di origine. |  |
| Token di accesso | Il token di accesso che corrisponde al tuo [!DNL OneTrust Integration] conto. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Per ulteriori informazioni su queste credenziali, consulta la sezione [[!DNL OneTrust Integration] documentazione di autenticazione](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Collega il tuo [!DNL OneTrust Integration] account

>[!NOTE]
>
>La [!DNL OneTrust Integration] Le specifiche API vengono condivise con Adobe per l’inserimento dei dati.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] area di lavoro per un catalogo di origini disponibili in Experience Platform.

Utilizza la *[!UICONTROL Categorie]* per filtrare le origini per categoria. In alternativa, immetti un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL Consenso e preferenze] per la categoria [!DNL OneTrust Integration] scheda sorgente. Per iniziare, seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle sorgenti dell’interfaccia utente di Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

La **[!UICONTROL Account di integrazione Connect OneTrust]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL OneTrust Integration] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![Il passaggio di autenticazione dell’account esistente nel flusso di lavoro origini.](../../../../images/tutorials/create/onetrust/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![Il nuovo passaggio di autenticazione dell’account nel flusso di lavoro origini.](../../../../images/tutorials/create/onetrust/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL OneTrust Integration] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per inserire i dati di consenso in Platform](../../dataflow/consent-and-preferences.md).
