---
keywords: Experience Platform;home;argomenti popolari;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: Creare una connessione sorgente del Marketing Cloud Salesforce nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente del Marketing Cloud Salesforce utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Crea un [!DNL Salesforce Marketing Cloud] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
> La [!DNL Salesforce Marketing Cloud] la sorgente è in versione beta. Consulta la sezione [panoramica di origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Salesforce Marketing Cloud] connettore di origine tramite l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se hai già un [!DNL Salesforce Marketing Cloud] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/marketing-automation.md).

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Salesforce Marketing Cloud] su Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Server host dell&#39;applicazione. Questo è spesso il tuo sottodominio. **Nota:** Quando immetti il tuo `host` devi solo specificare il sottodominio e non l’intero URL. Ad esempio, se l&#39;URL host è `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, quindi devi solo entrare `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` come valore host. |
| `clientId` | L&#39;ID client associato al [!DNL Salesforce Marketing Cloud] applicazione. |
| `clientSecret` | Il segreto client associato al tuo [!DNL Salesforce Marketing Cloud] applicazione. |

Per ulteriori informazioni su come iniziare, consulta questo articolo [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Collega il tuo [!DNL Salesforce Marketing Cloud] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Salesforce Marketing Cloud] a Platform.

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. Puoi anche usare la barra di ricerca per restringere i connettori visualizzati.

Sotto la [!UICONTROL Automazione del marketing] categoria, seleziona **[!UICONTROL Marketing Cloud Salesforce]** quindi seleziona **[!UICONTROL Configurazione]**.

![catalogo](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

La **[!UICONTROL Connetti al Marketing Cloud Salesforce]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e il [!DNL Salesforce Marketing Cloud] credenziali. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Salesforce Marketing Cloud] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Salesforce Marketing Cloud] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per inserire i dati del sistema di automazione di marketing in Platform](../../dataflow/marketing-automation.md).
