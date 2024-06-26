---
keywords: Experience Platform;home;argomenti popolari;onetrust;OneTrust
solution: Experience Platform
title: Creare una connessione sorgente OneTrust nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine OneTrust utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# Creare un [!DNL OneTrust Integration] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL OneTrust Integration] La sorgente supporta solo l’acquisizione dei dati di consenso e preferenze e non dei cookie.

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
| Nome host | L&#39;ambiente da cui è stato [!DNL OneTrust Integration] è necessario estrarre i dati da. | `app.onetrust.com` |
| URL test di autorizzazione | (Facoltativo) L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non vengono fornite, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. |  |
| Token di accesso | Il token di accesso corrispondente al [!DNL OneTrust Integration] account. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Per ulteriori informazioni su queste credenziali, vedere [[!DNL OneTrust Integration] documentazione di autenticazione](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Connetti [!DNL OneTrust Integration] account

>[!NOTE]
>
>Il [!DNL OneTrust Integration] Le specifiche API vengono condivise con Adobe per l’acquisizione dei dati.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] workspace per un catalogo di origini disponibile in Experience Platform.

Utilizza il *[!UICONTROL Categorie]* per filtrare le sorgenti per categoria. In alternativa, immettere un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai a [!UICONTROL Consenso e preferenze] categoria per il [!DNL OneTrust Integration] scheda sorgente. Per iniziare, seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini dell’interfaccia utente di Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

Il **[!UICONTROL Connetti account di integrazione OneTrust]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL OneTrust Integration] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![Il passaggio di autenticazione dell’account esistente nel flusso di lavoro di origini.](../../../../images/tutorials/create/onetrust/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![Il nuovo passaggio di autenticazione dell’account nel flusso di lavoro di origini.](../../../../images/tutorials/create/onetrust/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL OneTrust Integration] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati sul consenso in Platform](../../dataflow/consent-and-preferences.md).
