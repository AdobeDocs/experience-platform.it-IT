---
keywords: Experience Platform;home;argomenti popolari;Greenplum;greenplum
solution: Experience Platform
title: Creare una connessione sorgente GreenPlum nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente GreenPlum utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: e6c6a495-25ce-4497-b20e-91374c7bb548
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 1%

---

# Creare un [!DNL GreenPlum] connessione sorgente nell’interfaccia utente

I connettori di origini in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare [!DNL GreenPlum] connettore di origine che utilizza [!DNL Platform] dell&#39;utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL GreenPlum] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a [!DNL GreenPlum] utilizzando [!DNL Flow Service] API.

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per la connessione al [!DNL GreenPlum] dell&#39;istanza. Schema della stringa di connessione per [!DNL GreenPlum] è `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Per ulteriori informazioni su come iniziare, consulta [questo documento GreenPlum](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Connetti [!DNL GreenPlum] account

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL GreenPlum] account a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e quindi seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Sorgenti]** Workspace. Il **[!UICONTROL Catalogo]** Nella schermata vengono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL GreenPlum]**. Se è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo [!DNL GreenPlum] connettore.

![catalogo](../../../../images/tutorials/create/greenplum/catalog.png)

Il **[!UICONTROL Connetti a GreenPlum]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL GreenPlum] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/greenplum/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL GreenPlum] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** nell’angolo in alto a destra per procedere.

![esistente](../../../../images/tutorials/create/greenplum/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL GreenPlum] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
