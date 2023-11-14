---
title: Creare una connessione sorgente Redshift di Amazon nell’interfaccia utente
description: Scopri come creare una connessione sorgente Amazon Redshift utilizzando l’interfaccia utente di Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 2%

---

# Connetti [!DNL Amazon Redshift] account che utilizza l’area di lavoro origini

>[!IMPORTANT]
>
>Il [!DNL Amazon Redshift] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Questo tutorial descrive come collegare [!DNL Amazon Redshift] (in seguito denominati &quot;[!DNL Redshift]&quot;) a Adobe Experience Platform tramite l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Redshift] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Redshift] account di Experience Platform, è necessario fornire i seguenti valori:

| **Credenziali** | **Descrizione** |
| -------------- | --------------- |
| Server | Il server associato al tuo [!DNL Redshift] account. |
| Porta  | La porta TCP che [!DNL Redshift] il server utilizza per l&#39;ascolto delle connessioni client. |
| Nome utente | Il nome utente associato al tuo [!DNL Redshift] account. |
| Password | La password associata al tuo [!DNL Redshift] account. |
| Database | Il [!DNL Redshift] database a cui si sta effettuando l&#39;accesso. |

Per ulteriori informazioni su come iniziare, consulta [questo [!DNL Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Redshift] da Experience Platform.

## Connetti [!DNL Redshift] account

>[!NOTE]
>
>Standard di codifica predefinito per [!DNL Redshift] è Unicode. Questo non può essere modificato.

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

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Redshift] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in Experienci Platform](../../dataflow/databases.md).
