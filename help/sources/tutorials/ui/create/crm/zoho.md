---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Creare una connessione Source di Zoho CRM nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente di Zoho CRM utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL Zoho CRM] nell&#39;interfaccia utente

I connettori Source in Adobe Experience Platform consentono di acquisire dati CRM di origine esterna in base a una pianificazione. Questo tutorial illustra i passaggi per la creazione di un connettore di origine [!DNL Zoho CRM] tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Zoho CRM] valido, puoi saltare il resto di questo documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli le credenziali richieste

Per connettere [!DNL Zoho CRM] a Platform, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | Endpoint del server [!DNL Zoho CRM] a cui si sta effettuando la richiesta. |
| URL account | L’URL dell’account viene utilizzato per generare i token di accesso e di aggiornamento. L’URL deve essere specifico per il dominio. |
| ID client | L&#39;ID client corrispondente all&#39;account utente [!DNL Zoho CRM]. |
| Segreto client | Segreto client corrispondente all&#39;account utente [!DNL Zoho CRM]. |
| Token di accesso | Il token di accesso autorizza l&#39;accesso protetto e temporaneo all&#39;account [!DNL Zoho CRM]. |
| Aggiorna token | Un token di aggiornamento è un token utilizzato per generare un nuovo token di accesso, una volta scaduto il token di accesso. |

Per ulteriori informazioni su queste credenziali, consulta la documentazione sull&#39;[[!DNL Zoho CRM] autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connetti il tuo account [!DNL Zoho CRM]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL Zoho CRM] a [!DNL Platform].

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL CRM] selezionare **[!UICONTROL Zoho CRM]**, quindi **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/zoho/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account Zoho CRM]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Zoho CRM] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/zoho/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali di [!DNL Zoho CRM]. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

>[!TIP]
>
>Il dominio dell’URL dell’account deve corrispondere alla posizione di dominio appropriata. Di seguito sono riportati i vari domini e gli URL dei relativi account:<ul><li>Stati Uniti: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>Cina: https://accounts.zoho.com.cn</li></ul>

![nuovo](../../../../images/tutorials/create/zoho/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Zoho CRM]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/crm.md).
