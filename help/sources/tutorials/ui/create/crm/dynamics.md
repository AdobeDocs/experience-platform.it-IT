---
keywords: ' Experience Platform;home;argomenti popolari;Microsoft Dynamics;microsoft dDynamics;Dynamics;dDynamics'
solution: Experience Platform
title: Creare un connettore di origine Microsoft Dynamics nell'interfaccia utente
topic: overview
type: Tutorial
description: Questa esercitazione fornisce i passaggi per la creazione di un connettore di origine Microsoft Dynamics (in seguito denominato "Dynamics") tramite l'interfaccia utente della piattaforma.
translation-type: tm+mt
source-git-commit: 4241e00fd444969e5a40c8b34dd7786b1a3c6dcb
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Creare un connettore [!DNL Microsoft Dynamics] sorgente nell&#39;interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente [!DNL Microsoft Dynamics] (di seguito &quot;[!DNL Dynamics]&quot;) tramite l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Dynamics] valido, puoi ignorare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati per un&#39;origine CRM](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L&#39;URL del servizio dell&#39;istanza [!DNL Dynamics]. |
| `username` | Il nome utente per l&#39;account utente [!DNL Dynamics]. |
| `password` | La password dell&#39;account [!DNL Dynamics]. |
| `servicePrincipalId` | L&#39;ID client dell&#39;account [!DNL Dynamics]. Questo ID è richiesto quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |
| `servicePrincipalKey` | La chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |

Per ulteriori informazioni su come iniziare, fare riferimento a [this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Collegare l&#39;account [!DNL Dynamics]

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account [!DNL Dynamics] alla piattaforma.

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL CRM]**, selezionare **[!UICONTROL Microsoft Dynamics]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Dynamics].

![catalogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Dynamics]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome e una descrizione facoltativa per il nuovo account [!DNL Dynamics].

Il connettore [!DNL Dynamics] fornisce diversi tipi di autenticazione per l&#39;accesso. In [!UICONTROL Account authentication] selezionare **[!UICONTROL Basic authentication]** per utilizzare le credenziali basate su password.

Al termine, selezionare **[!UICONTROL Connect to source]**, quindi concedere un po&#39; di tempo per l&#39;impostazione del nuovo account.

![autenticazione di base](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

In alternativa, è possibile selezionare **[!UICONTROL Service-principal and key authentication]** e collegare l&#39;account [!DNL Dynamics] utilizzando una combinazione di [!UICONTROL Service principal ID] e [!UICONTROL Service principal key].

>[!IMPORTANT]
>
> L&#39;autenticazione di base in [!DNL Dynamics] può essere bloccata dall&#39;autenticazione a due fattori, che al momento non è supportata dalla piattaforma. In questo caso, si consiglia di utilizzare l&#39;autenticazione basata sulle chiavi per creare un connettore di origine utilizzando [!DNL Dynamics].

![autenticazione basata su chiave](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| Credenziali | Descrizione |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | L&#39;ID client dell&#39;account [!DNL Dynamics]. Questo ID è richiesto quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |
| [!UICONTROL Service principal key] | La chiave segreta principale del servizio. Questa credenziale è necessaria quando si utilizzano l&#39;entità del servizio e l&#39;autenticazione basata sulle chiavi. |

### Account esistente

Per collegare un account esistente, selezionate l&#39;account [!DNL Dynamics] con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo superiore destro per continuare.

![esistenti](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account [!DNL Dynamics]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per l&#39;inserimento di dati nella piattaforma](../../dataflow/crm.md).