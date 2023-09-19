---
title: Estensione Inoltro eventi di Google Cloud Platform
description: Questa estensione per l’inoltro di eventi Adobe Experience Platform invia gli eventi di Edge Network a Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---

# Estensione [!DNL Google Cloud Platform] per l’inoltro degli eventi

[[!DNL Google Cloud Platform]](https://cloud.google.com/) è una piattaforma di cloud computing che offre un’ampia gamma di servizi, tra cui elaborazione distribuita, archiviazione di database, distribuzione di contenuti e servizi di integrazione software-as-a-service (SaaS) per la gestione delle relazioni con i clienti (CRM) e la pianificazione delle risorse aziendali (ERP).

Il [!DNL Google Cloud Platform] [inoltro eventi](../../../ui/event-forwarding/overview.md) l&#39;estensione sfrutta [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) per inviare eventi da Adobe Experience Platform Edge Network a [!DNL Google Cloud Platform] per ulteriore elaborazione. Questa guida illustra come installare l’estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Per utilizzare questa estensione, è necessario disporre di un [!DNL Google Cloud Platform] account con esistente [!DNL Cloud Pub/Sub] argomento. Se non hai un argomento preesistente, vedi [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) documentazione sulla creazione e la gestione di argomenti.

### Creare un segreto e un elemento dati

Innanzitutto, crea un nuovo `Google OAuth 2` [segreto di inoltro eventi](../../../ui/event-forwarding/secrets.md), che verrà utilizzato per autenticare la connessione al tuo account mantenendo il valore sicuro.

Avanti, [creare un elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) utilizzando **[!UICONTROL Core]** e un **[!UICONTROL Segreto]** tipo di elemento dati per fare riferimento a `Google OAuth 2` segreto appena creato.

## Installare e configurare [!DNL Google Cloud Platform] estensione {#install}

Per installare l&#39;estensione: [creare una proprietà di inoltro degli eventi](../../../ui/event-forwarding/overview.md#properties) oppure scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. In **[!UICONTROL Catalogo]** , seleziona **[!UICONTROL Installa]** sulla scheda per [!DNL Google Cloud Platform] estensione.

![Il catalogo [!DNL Google Cloud Platform] estensione che evidenzia install.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Nella schermata di configurazione, immetti il segreto dell&#39;elemento dati creato in precedenza in **[!UICONTROL Token di accesso]** campo. Il segreto dell’elemento dati conterrà i [!DNL Google Cloud Platform] Token OAuth 2. Al termine, seleziona **[!UICONTROL Salva]**.

![Il [!DNL Google Cloud Platform] pagina di configurazione dell&#39;estensione.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Creare un [!DNL Send Data to Cloud Pub/Sub] regola {#tracking-rule}

Una volta installata l’estensione, crea un nuovo inoltro eventi [regola](../../../ui/managing-resources/rules.md) e configurarne le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona la **[!UICONTROL Piattaforma Google Cloud]** , quindi seleziona **[!UICONTROL Inviare dati a Cloud Pub/Sub]** per il tipo di azione.

![La vista di configurazione dell’azione per [!UICONTROL Piattaforma Google Cloud], con l&#39;azione evidenziata e [!UICONTROL Inviare dati a Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Argomento] | L’argomento che riceverà gli eventi dall’inoltro degli eventi. Il valore deve avere il formato `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Dati] | Questo campo contiene i dati da inoltrare al [!DNL Cloud Pub/Sub] in formato JSON.<br><br>Sotto **[!UICONTROL Raw]** , puoi incollare l’oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l’icona dell’elemento dati (![Icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per scegliere da un elenco di elementi dati esistenti per rappresentare i dati.<br><br>È inoltre possibile utilizzare **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. |
| [!UICONTROL Attributi] | Questo campo contiene l’oggetto JSON con attributi aggiuntivi da inviare insieme al messaggio.<br><br>Sotto **[!UICONTROL Raw]** , puoi incollare l’oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l’icona dell’elemento dati (![Icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per scegliere da un elenco di elementi dati esistenti per rappresentare i dati.<br><br>È inoltre possibile utilizzare **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. |

{style="table-layout:auto"}

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Cloud Pub/Sub] utilizzando [!DNL Google Cloud Platform] estensione di inoltro degli eventi. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experienci Platform, consulta [panoramica sull’inoltro degli eventi](../../../ui/event-forwarding/overview.md).