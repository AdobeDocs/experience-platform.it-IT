---
keywords: Experience Platform;home;argomenti popolari;Amazon Redshift;amazon redshift;Redshift;redshift;redshift
solution: Experience Platform
title: Creare una connessione Amazon Redshift Source nell'interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Amazon Redshift utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Amazon Redshift] nell&#39;interfaccia utente

>[!NOTE]
>
>Il connettore [!DNL Amazon Redshift] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica delle sorgenti](../../../../home.md#terms-and-conditions) .

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Amazon Redshift] (in seguito denominato &quot;[!DNL Redshift]&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Redshift] valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Redshift] su [!DNL Platform], devi fornire i seguenti valori:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Server associato al tuo account [!DNL Redshift]. |
| `username` | Il nome utente associato al tuo account [!DNL Redshift]. |
| `password` | La password associata al tuo account [!DNL Redshift]. |
| `database` | Il database [!DNL Redshift] a cui si accede. |

Per ulteriori informazioni su come iniziare, consulta [this [!DNL Redshift] document](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Connetti il tuo account [!DNL Redshift]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Redshift] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Amazon Redshift]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Redshift].

![](../../../../images/tutorials/create/redshift/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Amazon Redshift]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Redshift]. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![](../../../../images/tutorials/create/redshift/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account [!DNL Redshift] con cui si desidera connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/redshift/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Redshift] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in [!DNL Platform]](../../dataflow/databases.md).
