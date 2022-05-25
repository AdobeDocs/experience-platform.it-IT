---
keywords: personalizzazione; target; destinazione; la personalizzazione delle destinazioni; configurare le destinazioni di personalizzazione; stessa pagina; pagina successiva;
title: Configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Scopri come configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva.
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: 99a60621bca43ecf2dacb6202e005bbd8f191c99
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# Configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva

## Panoramica {#overview}

>[!NOTE]
>
>Quando [configurazione della connessione Adobe Target](../catalog/personalization/adobe-target-connection.md) senza utilizzare un ID datastream, i casi d’uso descritti in questo articolo non sono supportati.

Adobe Experience Platform utilizza [segmentazione dei bordi](../../segmentation/ui/edge-segmentation.md) per consentire ai clienti di creare e indirizzare segmenti di pubblico su larga scala in tempo reale.

Questa funzionalità consente di configurare casi d’uso per la personalizzazione della stessa pagina e della pagina successiva.

Questo articolo fornisce istruzioni dettagliate su come configurare Experience Platform e le destinazioni di personalizzazione per questi casi d’uso.

Inoltre, guarda il video seguente per una panoramica del processo di configurazione end-to-end.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>L&#39;interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione di questo video. Per informazioni aggiornate, consulta i passaggi di configurazione descritti nelle sezioni seguenti.

## Passaggio 1: Configurare un datastream nell’interfaccia utente Raccolta dati {#configure-datastream}

Il primo passaggio nella configurazione della destinazione di personalizzazione è quello di configurare un datastream per l’SDK Web di Experience Platform. Questa operazione viene eseguita nell’interfaccia utente di raccolta dati.

Durante la configurazione del datastream, in **[!UICONTROL Adobe Experience Platform]** assicurati che entrambe **[!UICONTROL Segmentazione Edge]** e **[!UICONTROL Destinazioni personalizzazione]** sono selezionati.

![Configurazione di Datastream](../assets/ui/configure-personalization-destinations/datastream-config.png)

Per ulteriori dettagli su come impostare un datastream, segui le istruzioni descritte nel [Documentazione di Platform Web SDK](../../edge/datastreams/overview.md).

## Passaggio 2: Configurare la destinazione di personalizzazione {#configure-destination}

Dopo aver configurato il datastream, puoi iniziare a configurare la destinazione di personalizzazione.

Segui [esercitazione sulla creazione della connessione di destinazione](../ui/connect-destination.md) per istruzioni dettagliate su come creare una nuova connessione di destinazione.

A seconda della destinazione che stai configurando, consulta i seguenti articoli per i prerequisiti specifici per la destinazione e le relative informazioni:

* [Connessione Adobe Target](../catalog/personalization/adobe-target-connection.md)
* [Connessione di personalizzazione personalizzata](../catalog/personalization/custom-personalization.md)

## Passaggio 3: Crea un [!DNL Active-On-Edge] criterio di unione {#create-merge-policy}

Dopo aver creato la connessione di destinazione, devi creare un [!DNL Active-On-Edge] criteri di unione.

Segui le istruzioni su [creazione di un criterio di unione](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)e assicurati di abilitare **[!UICONTROL Criterio di unione attiva sul bordo]** alternare.

## Passaggio 4: Creare un nuovo segmento in Platform {#create-segment}

Dopo aver creato il [!DNL Active-On-Edge] Criteri di unione, devi creare un nuovo segmento in Platform.

Segui [generatore di segmenti](../../segmentation/ui/segment-builder.md) guida per creare il nuovo segmento e assicurati di [assegnalo](../../segmentation/ui/segment-builder.md#merge-policies) la [!DNL Active-On-Edge] unione dei criteri creati al passaggio 3.

## Passaggio 5: Attiva il segmento nella destinazione

L’ultimo passaggio del processo di configurazione consiste nell’attivare il segmento creato al passaggio 4 nella destinazione creata al passaggio 2.

Per fare questo, segui questo [esercitazione sull&#39;attivazione](../ui/activate-profile-request-destinations.md).

## Convalidare la configurazione {#validate-configuration}

Dopo aver completato correttamente i passaggi precedenti, dovresti visualizzare i nuovi segmenti nella tua destinazione di personalizzazione.
