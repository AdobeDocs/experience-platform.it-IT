---
keywords: Experience Platform;home;argomenti popolari;Amazon Redshift;amazon redshift;Redshift;redshift
solution: Experience Platform
title: Creare una connessione sorgente Redshift di Amazon nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Amazon Redshift utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# Creare un [!DNL Amazon Redshift] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL Amazon Redshift] (in seguito denominati &quot;[!DNL Redshift]&quot;) connettore di origine utilizzando [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Redshift] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Redshift] account su [!DNL Platform], è necessario fornire i seguenti valori:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| `server` | Il server associato al tuo [!DNL Redshift] account. |
| `username` | Il nome utente associato al tuo [!DNL Redshift] account. |
| `password` | La password associata al tuo [!DNL Redshift] account. |
| `database` | Il [!DNL Redshift] database a cui si sta effettuando l&#39;accesso. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

## Connetti [!DNL Redshift] account

>[!NOTE]
>
>Standard di codifica predefinito per [!DNL Redshift] è Unicode. Questo non può essere modificato.

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Redshift] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL Amazon Redshift]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL Redshift] connettore.

![](../../../../images/tutorials/create/redshift/catalog.png)

Il **[!UICONTROL Connessione ad Amazon Redshift]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Redshift] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![](../../../../images/tutorials/create/redshift/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Redshift] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![](../../../../images/tutorials/create/redshift/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Redshift] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
