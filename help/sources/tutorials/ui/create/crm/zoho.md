---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho;zoho
solution: Experience Platform
title: Creare una connessione sorgente di gestione delle relazioni con i clienti Zoho nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Zoho CRM utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: 46b2fd6bc715bf1d8ccfeed576a2a2d193f92edd
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Crea un [!DNL Zoho CRM] connessione sorgente nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di acquisire dati CRM di origine esterna su base pianificata. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Zoho CRM] connettore di origine con [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Zoho CRM] account, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

Per connettersi [!DNL Zoho CRM] in Platform, devi fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| --- | --- |
| Endpoint | Il punto finale del [!DNL Zoho CRM] server a cui si sta effettuando la richiesta. |
| URL account | L’URL dell’account viene utilizzato per generare i token di accesso e aggiornamento. L&#39;URL deve essere specifico del dominio. |
| ID client | L&#39;ID client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| Segreto client | Il segreto client che corrisponde al tuo [!DNL Zoho CRM] account utente. |
| Token di accesso | Il token di accesso autorizza l’accesso sicuro e temporaneo al tuo [!DNL Zoho CRM] conto. |
| Aggiorna token | Un token di aggiornamento è un token utilizzato per generare un nuovo token di accesso, una volta scaduto il token di accesso. |

Per ulteriori informazioni su queste credenziali, consulta la documentazione su [[!DNL Zoho CRM] autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Collega il tuo [!DNL Zoho CRM] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Zoho CRM] account a [!DNL Platform].

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL CRM] categoria, seleziona **[!UICONTROL Zoo CRM]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/zoho/catalog.png)

La **[!UICONTROL Connetti account CRM Zoho]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Zoho CRM] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/zoho/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e [!DNL Zoho CRM] credenziali. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

>[!TIP]
>
>Il dominio dell&#39;URL degli account deve corrispondere alla posizione di dominio appropriata. Di seguito sono riportati i vari domini e gli URL dei loro account corrispondenti:<ul><li>Stati Uniti: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>Cina: https://accounts.zoho.com.cn</li></ul>

![nuovo](../../../../images/tutorials/create/zoho/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Zoho CRM] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’importazione di dati in Platform](../../dataflow/crm.md).
