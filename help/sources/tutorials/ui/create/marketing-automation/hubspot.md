---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente HubSpot nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: dd036cf4df5d772206d2b73292c60f2d866ba0de
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# Creare un connettore [!DNL HubSpot] sorgente nell’interfaccia utente

>[!NOTE]
> Il [!DNL HubSpot] connettore è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la panoramica [](../../../../home.md#terms-and-conditions) Origini.

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL HubSpot] sorgente utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Profilo cliente in tempo reale]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una [!DNL HubSpot] connessione, è possibile ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/marketing-automation.md).

### Raccogli credenziali richieste

Per accedere al tuo [!DNL HubSpot] account su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientId` | L&#39;ID client associato all&#39; [!DNL HubSpot] applicazione. |
| `clientSecret` | Il segreto client associato all&#39; [!DNL HubSpot] applicazione. |
| `accessToken` | Token di accesso ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |
| `refreshToken` | Token di aggiornamento ottenuto durante l&#39;autenticazione iniziale dell&#39;integrazione OAuth. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL HubSpot] documento](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## Collegamento dell&#39; [!DNL HubSpot] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare il vostro [!DNL HubSpot] account a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse sorgenti con cui è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Marketing automation]** categoria, selezionare **[!UICONTROL HubSpot]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo [!DNL HubSpot] connettore.

![catalogo](../../../../images/tutorials/create/hubspot/catalog.png)

Viene **[!UICONTROL Connect to HubSpot]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL HubSpot] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL HubSpot] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/hubspot/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL HubSpot] account. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per l&#39;inserimento [!DNL Platform]](../../dataflow/marketing-automation.md)dei dati del sistema di automazione marketing.