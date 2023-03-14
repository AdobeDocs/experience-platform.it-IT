---
keywords: personalizzazione; target; destinazione; personalizzazione o destinazioni; configurare destinazioni di personalizzazione; stessa pagina; pagina successiva;
title: Configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva
type: Tutorial
description: Scopri come configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva

## Panoramica {#overview}

>[!NOTE]
>
>Quando [configurazione della connessione Adobe Target](../catalog/personalization/adobe-target-connection.md) senza l’utilizzo di un ID dello stream di dati, i casi d’uso descritti in questo articolo non sono supportati.

Adobe Experience Platform utilizza [segmentazione Edge](../../segmentation/ui/edge-segmentation.md) per consentire ai clienti di creare e indirizzare i segmenti di pubblico su larga scala, in tempo reale.

Questa funzionalità consente di configurare casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.

Questo articolo fornisce istruzioni dettagliate su come configurare Experience Platform e le destinazioni di personalizzazione per questi casi d’uso.

Inoltre, guarda il video seguente per una panoramica del processo di configurazione end-to-end.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>L’interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione del video. Per informazioni aggiornate, consulta i passaggi di configurazione descritti nelle sezioni seguenti.

## Passaggio 1: configurare uno stream di dati nell’interfaccia utente di Data Collection {#configure-datastream}

Il primo passaggio nella configurazione della destinazione di personalizzazione consiste nel configurare uno stream di dati per l’SDK per web di Experience Platform. Questa operazione viene eseguita nell’interfaccia utente di Data Collection.

Durante la configurazione dello stream di dati, in **[!UICONTROL Adobe Experience Platform]** assicurati che entrambi **[!UICONTROL Segmentazione Edge]** e **[!UICONTROL Destinazioni di personalizzazione]** sono selezionati.

![Configurazione dello stream di dati](../assets/ui/configure-personalization-destinations/datastream-config.png)

Per ulteriori informazioni su come impostare un flusso di dati, segui le istruzioni descritte nella sezione [Documentazione di Platform Web SDK](../../edge/datastreams/overview.md).

## Passaggio 2: configurare la destinazione di personalizzazione {#configure-destination}

Dopo aver configurato lo stream di dati, puoi iniziare a configurare la destinazione di personalizzazione.

Segui le [tutorial sulla creazione della connessione di destinazione](../ui/connect-destination.md) per istruzioni dettagliate su come creare una nuova connessione di destinazione.

A seconda della destinazione che stai configurando, consulta i seguenti articoli per i prerequisiti specifici per la destinazione e le relative informazioni:

* [Connessione Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Connessione di personalizzazione personalizzata](../catalog/personalization/custom-personalization.md)

## Passaggio 3: creare un [!DNL Active-On-Edge] criterio di unione {#create-merge-policy}

Dopo aver creato la connessione di destinazione, è necessario creare una [!DNL Active-On-Edge] criterio di unione.

Segui le istruzioni su [creazione di un criterio di unione](../../profile/merge-policies/ui-guide.md#create-a-merge-policy), e assicurati di abilitare **[!UICONTROL Criterio di unione Attivo su Edge]** attivare/disattivare.

## Passaggio 4: creare un nuovo segmento in Platform {#create-segment}

Dopo aver creato [!DNL Active-On-Edge] criterio di unione, devi creare un nuovo segmento in Platform.

Segui le [Generatore di segmenti](../../segmentation/ui/segment-builder.md) per creare il nuovo segmento e assicurati di [assegnarlo](../../segmentation/ui/segment-builder.md#merge-policies) il [!DNL Active-On-Edge] criterio di unione creato nel passaggio 3.

## Passaggio 5: attivare il segmento nella destinazione

L’ultimo passaggio del processo di configurazione consiste nell’attivare il segmento creato nel passaggio 4 nella destinazione creata nel passaggio 2.

Per farlo, segui questa procedura [tutorial di attivazione](../ui/activate-profile-request-destinations.md).

## Convalidare la configurazione {#validate-configuration}

Dopo aver seguito correttamente i passaggi precedenti, dovresti visualizzare i nuovi segmenti nella destinazione di personalizzazione.
