---
keywords: Experience Platform;home;argomenti popolari;Amazon Redshift;amazon redshift;Redshift;redshift;redshift
solution: Experience Platform
title: Creare una connessione Amazon Redshift Source nell'interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Amazon Redshift utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Crea un [!DNL Amazon Redshift] connessione sorgente nell’interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Amazon Redshift] (in appresso denominato &quot;[!DNL Redshift]&quot;) connettore di origine con [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Redshift] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Redshift] conto su [!DNL Platform], è necessario fornire i seguenti valori:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Il server associato al [!DNL Redshift] conto. |
| `username` | Il nome utente associato al tuo [!DNL Redshift] conto. |
| `password` | La password associata al [!DNL Redshift] conto. |
| `database` | La [!DNL Redshift] database a cui si accede. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Collega il tuo [!DNL Redshift] account

>[!NOTE]
>
>Standard di codifica predefinito per [!DNL Redshift] è Unicode. Questo non può essere modificato.

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Redshift] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL Amazon Redshift]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare una nuova [!DNL Redshift] connettore.

![](../../../../images/tutorials/create/redshift/catalog.png)

La **[!UICONTROL Connessione a Amazon Redshift]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e il [!DNL Redshift] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/redshift/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Redshift] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/redshift/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Redshift] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’immissione di dati in [!DNL Platform]](../../dataflow/databases.md).
