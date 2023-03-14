---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Creare una connessione sorgente di Zoho CRM nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente di Zoho CRM utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Creare un [!DNL Zoho CRM] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati CRM di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL Zoho CRM] connettore di origine che utilizza [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Zoho CRM] account, puoi saltare il resto di questo documento e passare all’esercitazione su [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli le credenziali richieste

Per connettersi [!DNL Zoho CRM] In Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | Endpoint del [!DNL Zoho CRM] server a cui si sta effettuando la richiesta. |
| URL account | L’URL dell’account viene utilizzato per generare i token di accesso e di aggiornamento. L’URL deve essere specifico per il dominio. |
| ID client | L’ID client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| Segreto client | Il segreto client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| Token di accesso | Il token di accesso autorizza l’accesso protetto e temporaneo al tuo [!DNL Zoho CRM] account. |
| Aggiorna token | Un token di aggiornamento è un token utilizzato per generare un nuovo token di accesso, una volta scaduto il token di accesso. |

Per ulteriori informazioni su queste credenziali, consulta la documentazione su [[!DNL Zoho CRM] autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connetti [!DNL Zoho CRM] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Zoho CRM] account a [!DNL Platform].

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL CRM] categoria, seleziona **[!UICONTROL Zoho CRM]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/zoho/catalog.png)

Il **[!UICONTROL Connetti account di Zoho CRM]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Zoho CRM] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/zoho/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e il tuo [!DNL Zoho CRM] credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

>[!TIP]
>
>Il dominio dell’URL dell’account deve corrispondere alla posizione di dominio appropriata. Di seguito sono riportati i vari domini e gli URL dei relativi account:<ul><li>Stati Uniti: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>Cina: https://accounts.zoho.com.cn</li></ul>

![nuovo](../../../../images/tutorials/create/zoho/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Zoho CRM] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](../../dataflow/crm.md).
