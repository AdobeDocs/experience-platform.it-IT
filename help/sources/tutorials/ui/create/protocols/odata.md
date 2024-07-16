---
keywords: Experience Platform;home;argomenti popolari;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Creare una connessione Source OData generica nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione sorgente Generic Open Data Protocol utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: aad6b6f7-622c-4ab6-bf6d-1221fe1132d1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL Generic OData] nell&#39;interfaccia utente

I connettori Source in Adobe Experience Platform consentono di acquisire dati di origine esterna in base a una pianificazione. Questo tutorial descrive i passaggi necessari per creare un connettore di origine [!DNL Generic Open Data Protocol] (di seguito &quot;[!DNL OData]&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL OData] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/protocols.md)

### Raccogli le credenziali richieste

Per accedere all&#39;account [!DNL OData] in [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `url` | URL principale del servizio [!DNL OData]. |

Per ulteriori informazioni su come iniziare, fare riferimento a [questo [!DNL OData] documento](https://www.odata.org/getting-started/basic-tutorial/).

## Connetti il tuo account [!DNL OData]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;account [!DNL OData] a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Origini]**. Nella schermata **[!UICONTROL Catalogo]** sono visualizzate diverse origini per le quali è possibile creare un account con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria **[!UICONTROL Protocolli]**, selezionare **[!UICONTROL OData generica]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore [!DNL OData].

![catalogo](../../../../images/tutorials/create/odata/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a OData generica]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornire alla connessione un nome, una descrizione facoltativa e le credenziali [!DNL OData]. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![connetti](../../../../images/tutorials/create/odata/connect.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account [!DNL OData] con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/odata/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL OData]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire i dati dei protocolli in [!DNL Platform]](../../dataflow/protocols.md).
