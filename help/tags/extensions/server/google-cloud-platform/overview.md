---
title: Estensione Inoltro eventi di Google Cloud Platform
description: Questa estensione di inoltro degli eventi Adobe Experience Platform invia eventi di Edge Network a Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# Estensione [!DNL Google Cloud Platform] per l’inoltro degli eventi

[[!DNL Google Cloud Platform]](https://cloud.google.com/) è una piattaforma di cloud computing che offre un&#39;ampia gamma di servizi, ad esempio elaborazione distribuita, archiviazione di database, distribuzione di contenuti e servizi di integrazione SaaS (Software-as-a-Service) per la gestione delle relazioni con i clienti (CRM) e la pianificazione delle risorse aziendali (ERP).

L&#39;estensione [!DNL Google Cloud Platform] [event forwarding](../../../ui/event-forwarding/overview.md) sfrutta [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) per inviare eventi dall&#39;Edge Network Adobe Experience Platform a [!DNL Google Cloud Platform] per l&#39;ulteriore elaborazione. Questa guida illustra come installare l’estensione e utilizzarne le funzionalità in una regola di inoltro degli eventi.

## Prerequisiti

Per utilizzare questa estensione, è necessario disporre di un account [!DNL Google Cloud Platform] con un argomento [!DNL Cloud Pub/Sub] esistente. Se non hai un argomento preesistente, consulta la documentazione [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) sulla creazione e la gestione degli argomenti.

### Creare un segreto e un elemento dati

Crea un nuovo `Google OAuth 2` [segreto di inoltro eventi](../../../ui/event-forwarding/secrets.md), che verrà utilizzato per autenticare la connessione all&#39;account mantenendo il valore sicuro.

Quindi, [crea un elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) utilizzando l&#39;estensione **[!UICONTROL Core]** e un tipo di elemento dati **[!UICONTROL Secret]** per fare riferimento al segreto `Google OAuth 2` appena creato.

## Installa e configura l&#39;estensione [!DNL Google Cloud Platform] {#install}

Per installare l&#39;estensione, [crea una proprietà di inoltro eventi](../../../ui/event-forwarding/overview.md#properties) o scegli una proprietà esistente da modificare.

Seleziona **[!UICONTROL Estensioni]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalogo]**, seleziona **[!UICONTROL Installa]** sulla scheda per l&#39;estensione [!DNL Google Cloud Platform].

![L&#39;estensione [!DNL Google Cloud Platform] del catalogo evidenzia l&#39;installazione.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Nella schermata di configurazione, immetti il segreto dell&#39;elemento dati creato in precedenza nel campo **[!UICONTROL Token di accesso]**. Il segreto dell&#39;elemento dati conterrà il token OAuth 2 [!DNL Google Cloud Platform]. Al termine, seleziona **[!UICONTROL Salva]**.

![Pagina di configurazione dell&#39;estensione [!DNL Google Cloud Platform].](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Crea una regola [!DNL Send Data to Cloud Pub/Sub] {#tracking-rule}

Una volta installata l&#39;estensione, crea una nuova [regola](../../../ui/managing-resources/rules.md) di inoltro eventi e configurane le condizioni come desiderato. Durante la configurazione delle azioni per la regola, seleziona l&#39;estensione **[!UICONTROL Google Cloud Platform]**, quindi seleziona **[!UICONTROL Invia dati a Cloud Pub/Sub]** per il tipo di azione.

![Visualizzazione della configurazione dell&#39;azione per [!UICONTROL Google Cloud Platform], con l&#39;azione evidenziata e [!UICONTROL Invia dati a Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Input | Descrizione |
| --- | --- |
| [!UICONTROL Argomento] | L’argomento che riceverà gli eventi dall’inoltro degli eventi. Il valore deve avere il formato `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Dati] | Questo campo contiene i dati da inoltrare all&#39;argomento [!DNL Cloud Pub/Sub] in formato JSON.<br><br>Con l&#39;opzione **[!UICONTROL Raw]**, puoi incollare l&#39;oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l&#39;icona dell&#39;elemento dati (![icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per effettuare una selezione da un elenco di elementi dati esistenti per rappresentare i dati.<br><br>È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. |
| [!UICONTROL Attributi] | Questo campo contiene l’oggetto JSON con attributi aggiuntivi da inviare insieme al messaggio.<br><br>Con l&#39;opzione **[!UICONTROL Raw]**, puoi incollare l&#39;oggetto JSON direttamente nel campo di testo fornito, oppure puoi selezionare l&#39;icona dell&#39;elemento dati (![icona del set di dati](../../../images/extensions/server/aws/data-element-icon.png)) per effettuare una selezione da un elenco di elementi dati esistenti per rappresentare i dati.<br><br>È inoltre possibile utilizzare l&#39;opzione **[!UICONTROL Editor coppie chiave-valore JSON]** per aggiungere manualmente ogni coppia chiave-valore tramite un editor di interfaccia utente. Ogni valore può essere rappresentato da un input non elaborato, oppure è possibile selezionare un elemento dati. |

{style="table-layout:auto"}

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Cloud Pub/Sub] utilizzando l&#39;estensione di inoltro eventi [!DNL Google Cloud Platform]. Per ulteriori informazioni sulle funzionalità di inoltro degli eventi in Experience Platform, consulta la [panoramica sull&#39;inoltro degli eventi](../../../ui/event-forwarding/overview.md).
