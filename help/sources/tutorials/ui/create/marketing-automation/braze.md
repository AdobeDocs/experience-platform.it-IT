---
title: Creare un flusso di dati per Braze dati nell’interfaccia utente
description: Scopri come creare un flusso di dati per l’account Braze utilizzando l’interfaccia utente di Adobe Experience Platform.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: bfcea2a30a0ecadcafaddf7660eef90952dcade6
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---

# Creare un [!DNL Braze Currents] connessione sorgente nell’interfaccia utente

>[!NOTE]
>
>Il [!DNL Braze Currents] sorgente in versione beta. Leggi le [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

[!DNL Braze] potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi. [!DNL Braze Currents] è un flusso di dati in tempo reale di eventi di coinvolgimento dalla piattaforma Braze che rappresenta l’esportazione più solida ma granulare dal [!DNL Braze] piattaforma.

Leggi il seguente tutorial per scoprire come estrarre i dati degli eventi di coinvolgimento dal tuo [!DNL Braze] Adobe Experience Platform nell’interfaccia utente.

## Prerequisiti

Per completare i passaggi descritti in questa guida, è necessario:

* Accesso a [Adobe Experience Platform](https://platform.adobe.com) e l’autorizzazione per creare una nuova connessione sorgente di streaming.
* Accesso al [[!DNL Braze] dashboard](https://dashboard.braze.com/sign_in), non utilizzato [Licenza del connettore corrente](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents), e le autorizzazioni per creare un connettore. Per ulteriori informazioni, leggere [requisiti per l&#39;impostazione [!DNL Currents]](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#requirements).

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Experience Platform] organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Questo tutorial richiede anche una buona conoscenza di [[!DNL Braze] Correnti](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents).

Se si dispone già di un [!DNL Braze] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/marketing-automation.md).

## Connetti [!DNL Braze] account da Experience Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *Marketing Automation* categoria, seleziona **[!UICONTROL Braze correnti]** e quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell’interfaccia utente di Experienci Platform con l’origine Braze Currents selezionata.](../../../../images/tutorials/create/braze/catalog.png)

Quindi, carica il fornito [File di esempio Braze Currents](https://github.com/Appboy/currents-examples/blob/master/sample-data/Adobe/adobe_examples.json). Questo file contiene tutti i possibili campi che Braze potrebbe inviare come parte di un evento.

![La schermata &quot;Add Data&quot; (Aggiungi dati).](../../../../images/tutorials/create/braze/select-data.png)

Una volta caricato il file, devi fornire i dettagli del flusso di dati, incluse le informazioni sul set di dati e lo schema a cui stai eseguendo la mappatura.
![La schermata &quot;Dettagli flusso di dati&quot; evidenziava &quot;Dettagli set di dati&quot;.](../../../../images/tutorials/create/braze/dataflow-detail.png)

Quindi, configura la mappatura per i dati utilizzando l’interfaccia di mappatura.

![La schermata &quot;Mappatura&quot;.](../../../../images/tutorials/create/braze/mapping.png)

>[!IMPORTANT]
>
>I timestamp di brasatura non sono espressi in millisecondi, ma in secondi. Affinché i timestamp in Experienci Platform vengano rispecchiati accuratamente, è necessario creare campi calcolati in millisecondi. Un calcolo di &quot;tempo * 1000&quot; convertirà correttamente in millisecondi, adatto per la mappatura a un campo marca temporale in Experienci Platform.
>
>![Creazione di un campo calcolato per la marca temporale ](../../../../images/tutorials/create/braze/create-calculated-field.png)

### Raccogli le credenziali richieste

Una volta creata la connessione, è necessario raccogliere i seguenti valori delle credenziali, che verranno quindi forniti nel dashboard Braze per inviare i dati ad Experienci Platform. Per ulteriori informazioni, leggere [!DNL Braze] [guida alla navigazione in Correnti](https://www.braze.com/docs/user_guide/data_and_analytics/braze_currents/setting_up_currents/#step-2-navigate-to-currents).

| Campo | Descrizione |
| --- | --- |
| ID client | L’ID client associato alla sorgente dell’Experience Platform. |
| Segreto client | Il segreto client associato alla tua origine Experience Platform. |
| ID tenant | L’ID tenant associato alla tua origine Experience Platform. |
| Nome sandbox | La sandbox associata alla sorgente di Experience Platform. |
| ID flusso di dati | L’ID del flusso di dati associato alla sorgente di Experience Platform. |
| Endpoint di streaming | L’endpoint di streaming associato alla sorgente di Experience Platform. **Nota**: [!DNL Braze] converte automaticamente questo valore nell&#39;endpoint di streaming batch. |

### Configura [!DNL Braze Currents] per inviare dati all&#39;origine dati in streaming

All&#39;interno del [!DNL Braze Dashboard], passare a Integrazioni partner **->** Esportazione dati, quindi selezionare **[!DNL Create New Current]**. Verrà richiesto di specificare un nome per il connettore, le informazioni di contatto per le notifiche sul connettore e le credenziali elencate in precedenza. Seleziona gli eventi che desideri ricevere, se lo desideri configura le esclusioni/trasformazioni di campo desiderate, quindi seleziona **[!DNL Launch Current]**.

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Braze] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati di marketing automation system in [!DNL Platform]](../../dataflow/marketing-automation.md).