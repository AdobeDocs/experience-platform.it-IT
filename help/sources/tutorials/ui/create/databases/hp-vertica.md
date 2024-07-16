---
keywords: Experience Platform;home;argomenti popolari;HP Vertica
solution: Experience Platform
title: Creare una connessione HP Vertica Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente HP Vertica utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# Creare una connessione sorgente HP [!DNL Vertica] nell&#39;interfaccia utente

>[!NOTE]
>
> Il connettore HP [!DNL Vertica] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial illustra i passaggi per la creazione di un connettore di origine HP [!DNL Vertica] tramite l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione HP [!DNL Vertica] valida, puoi saltare il resto di questo documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli le credenziali richieste

Le sezioni seguenti forniscono informazioni aggiuntive che è necessario conoscere per connettersi correttamente a HP [!DNL Vertica] utilizzando l&#39;API [!DNL Flow Service].

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per la connessione all&#39;istanza di HP [!DNL Vertica]. Il modello di stringa di connessione per HP [!DNL Vertica] è `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Per ulteriori informazioni su come iniziare, consulta [questo documento HP [!DNL Vertica] 2}.](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)

## Connetti il tuo account HP [!DNL Vertica]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account HP [!DNL Vertica] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Database]** selezionare **[!UICONTROL HP Vertica]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore HP [!DNL Vertica].

![catalogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a HP Vertica]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire un nome, una descrizione facoltativa e le credenziali HP [!DNL Vertica]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/hp-vertica/new.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account HP [!DNL Vertica] con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** nell&#39;angolo in alto a destra per continuare.

![esistente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo account HP [!DNL Vertica]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in [!DNL Platform]](../../dataflow/databases.md).
