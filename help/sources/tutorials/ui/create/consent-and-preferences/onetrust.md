---
keywords: Experience Platform;home;argomenti popolari;onetrust;OneTrust
solution: Experience Platform
title: Creare una connessione Source OneTrust nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione di origine OneTrust utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL OneTrust Integration] nell&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL OneTrust Integration] supporta solo l&#39;acquisizione dei dati di consenso e preferenze e non dei cookie.

Questo tutorial illustra i passaggi per la creazione di una connessione di origine [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) per acquisire in Adobe Experience Platform dati di consenso storici e pianificati tramite l&#39;interfaccia utente di Platform.

## Prerequisiti

>[!IMPORTANT]
>
>Il connettore di origine [!DNL OneTrust Integration] e la documentazione sono stati creati dal team [!DNL OneTrust Integration]. Per richieste di informazioni o richieste di aggiornamento, contatta direttamente il [[!DNL OneTrust] team](https://my.onetrust.com/s/contactsupport?language=en_US).

Prima di poter connettere [!DNL OneTrust Integration] a Platform, è necessario recuperare il token di accesso. Per istruzioni dettagliate su come trovare il token di accesso, consulta la [[!DNL OneTrust Integration] guida OAuth 2](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

Il token di accesso non viene aggiornato automaticamente dopo la scadenza perché i token di aggiornamento da sistema a sistema non sono supportati da [!DNL OneTrust]. Pertanto, è necessario assicurarsi che il token di accesso sia aggiornato nella connessione prima della scadenza. La durata massima configurabile per un token di accesso è di un anno. Per ulteriori informazioni sull&#39;aggiornamento del token di accesso, consulta il documento [[!DNL OneTrust] sulla gestione delle credenziali client OAuth 2.0](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### Raccogli le credenziali richieste

Per connettere [!DNL OneTrust Integration] a Platform, è necessario fornire i valori per le credenziali di autenticazione seguenti:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| Nome host | Ambiente da cui è necessario estrarre i dati [!DNL OneTrust Integration]. | `app.onetrust.com` |
| URL test di autorizzazione | (Facoltativo) L’URL del test di autorizzazione viene utilizzato per convalidare le credenziali durante la creazione di una connessione di base. Se non vengono fornite, le credenziali vengono controllate automaticamente durante il passaggio di creazione della connessione di origine. | |
| Token di accesso | Il token di accesso corrispondente al tuo account [!DNL OneTrust Integration]. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

Per ulteriori informazioni su queste credenziali, consulta la [[!DNL OneTrust Integration] documentazione sull&#39;autenticazione](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## Connetti il tuo account [!DNL OneTrust Integration]

>[!NOTE]
>
>Le specifiche API [!DNL OneTrust Integration] sono condivise con Adobe per l&#39;acquisizione dei dati.

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini] per un catalogo di origini disponibili in Experience Platform.

Utilizza il menu *[!UICONTROL Categorie]* per filtrare le origini per categoria. In alternativa, immettere un nome di origine nella barra di ricerca per trovare un&#39;origine specifica dal catalogo.

Vai alla categoria [!UICONTROL Consenso e preferenze] per la scheda di origine [!DNL OneTrust Integration]. Per iniziare, selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini dell&#39;interfaccia utente Experience Platform.](../../../../images/tutorials/create/onetrust/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account di integrazione OneTrust]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL OneTrust Integration] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![Il passaggio di autenticazione dell&#39;account esistente nel flusso di lavoro di origine.](../../../../images/tutorials/create/onetrust/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Il nuovo passaggio di autenticazione dell&#39;account nel flusso di lavoro di origine.](../../../../images/tutorials/create/onetrust/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL OneTrust Integration]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire i dati sul consenso in Platform](../../dataflow/consent-and-preferences.md).
