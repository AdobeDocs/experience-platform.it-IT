---
keywords: Experience Platform;home;argomenti popolari;Google AdWords;connettore di origine Google AdWords;connettore di riferimento Google adwords
solution: Experience Platform
title: Creare una connessione sorgente Google AdWords nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Google AdWords utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Google AdWords] nell&#39;interfaccia utente

>[!NOTE]
>
>Il connettore [!DNL Google AdWords] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Google AdWords] utilizzando l&#39;interfaccia utente [!DNL Platform] .

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Google AdWords] valida, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/payments.md)

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Google AdWords] [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `clientCustomerId` | ID cliente client dell&#39;account [!DNL AdWords]. |
| `developerToken` | Il token sviluppatore associato all’account manager. |
| `refreshToken` | Il token di aggiornamento ottenuto da [!DNL Google] per autorizzare l&#39;accesso a [!DNL AdWords]. |
| `clientId` | L&#39;ID client dell&#39;applicazione [!DNL Google] utilizzata per acquisire il token di aggiornamento. |
| `clientSecret` | Il segreto client dell&#39;applicazione [!DNL Google] utilizzata per acquisire il token di aggiornamento. |

Per ulteriori informazioni su come iniziare, consulta questo [[!DNL Google AdWords] documento](https://developers.google.com/adwords/api/docs/guides/authentication).

## Connetti il tuo account [!DNL Google AdWords]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Google AdWords] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Advertising]**, selezionare **[!UICONTROL Google AdWords]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Google AdWords].

![catalogo](../../../../images/tutorials/create/ads/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Google AdWords]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Google AdWords]. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account [!DNL Google AdWords] con cui si desidera connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistente](../../../../images/tutorials/create/ads/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Google AdWords] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire dati pubblicitari in [!DNL Platform]](../../dataflow/advertising.md).
