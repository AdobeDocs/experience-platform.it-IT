---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine Microsoft Dynamics nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 7cc76eab53adf6a40d16b368854a2e7f178e7244
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 1%

---


# Creare un connettore [!DNL Microsoft Dynamics] sorgente nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati CRM di origine esterna su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore [!DNL Microsoft Dynamics] (in seguito denominato &quot;[!DNL Dynamics]&quot;) sorgente utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): Il framework standard con cui [!DNL Experience Platform] organizzare i dati relativi all&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Profilo cliente in tempo reale]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di un [!DNL Dynamics] account valido, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `serviceUri` | L’URL del servizio dell’ [!DNL Dynamics] istanza. |
| `username` | Nome utente per l’account [!DNL Dynamics] utente. |
| `password` | La password del tuo [!DNL Dynamics] account. |

Per ulteriori informazioni su come iniziare, consulta [ [!DNL Dynamics] questo documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## Collegamento dell&#39; [!DNL Dynamics] account

Dopo aver raccolto le credenziali necessarie, potete seguire i passaggi descritti di seguito per collegare il vostro [!DNL Dynamics] account a [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; **[!UICONTROL Sources]** area di lavoro. Nella **[!UICONTROL Catalog]** schermata sono visualizzate diverse sorgenti con cui è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la **[!UICONTROL Databases]** categoria, selezionare **[!UICONTROL Dynamics]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo [!DNL Dynamics] connettore.

![catalogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

Viene **[!UICONTROL Connect to Dynamics]** visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e [!DNL Dynamics] le credenziali. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39; [!DNL Dynamics] account con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** nell&#39;angolo superiore destro per proseguire.

![esistenti](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39; [!DNL Dynamics] account. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati in cui inserire i dati [!DNL Platform]](../../dataflow/crm.md).