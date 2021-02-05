---
keywords: ' Experience Platform;home;argomenti popolari;Google AdWords;Google AdWords connettore di origine;google adwords connettore'
solution: Experience Platform
title: Creare una connessione di origine Google AdWords nell'interfaccia utente
topic: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Google AdWords utilizzando l’interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Google AdWords] nell&#39;interfaccia utente

>[!NOTE]
>
>Il connettore [!DNL Google AdWords] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, vedere [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions).

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore di origine [!DNL Google AdWords] utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione [!DNL Google AdWords] valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Google AdWords] [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientCustomerId` | L&#39;ID cliente client dell&#39;account [!DNL AdWords]. |
| `developerToken` | Token sviluppatore associato all&#39;account manager. |
| `refreshToken` | Token di aggiornamento ottenuto da [!DNL Google] per autorizzare l&#39;accesso a [!DNL AdWords]. |
| `clientId` | ID client dell&#39;applicazione [!DNL Google] utilizzata per acquisire il token di aggiornamento. |
| `clientSecret` | Il segreto client dell&#39;applicazione [!DNL Google] utilizzata per acquisire il token di aggiornamento. |

Per ulteriori informazioni su come iniziare, fare riferimento a questo [[!DNL Google AdWords] documento](https://developers.google.com/adwords/api/docs/guides/authentication).

## Collegare l&#39;account [!DNL Google AdWords]

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account [!DNL Google AdWords] a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL Advertising]**, selezionare **[!UICONTROL Google AdWords]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Google AdWords].

![catalogo](../../../../images/tutorials/create/ads/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Google AdWords]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Google AdWords]. Al termine, selezionare **[!UICONTROL Connect]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account [!DNL Google AdWords] con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/ads/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account [!DNL Google AdWords]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire i dati pubblicitari in  [!DNL Platform]](../../dataflow/advertising.md).