---
title: Utilizza l’ultimo attributo XDM del tempo di qualifica nelle nuove destinazioni di archiviazione cloud beta
description: Scopri come utilizzare l’attributo XDM dell’ora dell’ultima qualifica nelle nuove destinazioni di archiviazione cloud in versione beta
hidefromtoc: y
hide: y
exl-id: d077ea10-5ff2-4acc-8ee6-78ea6cd752d1
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Utilizza l’ultimo attributo XDM del tempo di qualifica nelle nuove destinazioni di archiviazione cloud beta {#last-qualification-time}

>[!IMPORTANT]
> 
>Questa pagina descrive le funzionalità presenti in versione beta. La funzionalità e la documentazione sono soggette a modifiche. Contatta il tuo rappresentante di Adobe o l’Assistenza clienti per accedere a questo programma beta.

## Prerequisiti {#prerequisites}

Per utilizzare l&#39;ora dell&#39;ultima qualifica (`lastQualificationTime`) XDM, devi essere iscritto al [programma beta](/help/release-notes/2022/october-2022.md#destinations) per utilizzare la funzionalità di esportazione dei file migliorata ed esportare i dati in uno dei sei [destinazioni di archiviazione cloud beta](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). Sei iscritto se riesci a visualizzare le nuove schede beta per le destinazioni di archiviazione cloud nel catalogo, come mostrato di seguito per [!DNL Amazon S3].

![Immagine che mostra la nuova scheda beta Amazon S3](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## Come utilizzare l’ultimo attributo XDM dell’ora di qualifica {#how-to-use}

Se utilizzi uno dei sei nuovi connettori beta per l’archiviazione cloud, puoi utilizzare l’ultimo attributo xdm del tempo di qualificazione nell’oggetto [passaggio di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) del flusso di lavoro di attivazione per creare una colonna nel file esportato con la marca temporale più recente di quando un profilo risulta idoneo per un segmento. Questo può aiutarti con alcuni casi di utilizzo di misurazione o analisi e ti può dare un’idea migliore di quando attivare determinati tipi di pubblico.

Nota che per aggiungere `lastQualificationTime` alle esportazioni di file, al momento devi inserire manualmente il valore `xdm: segmentMembership.ups.seg_id.lastQualificationTime` nel campo sorgente, come illustrato di seguito. Puoi anche modificare il campo di destinazione in `lastQualificationTime` o qualsiasi altro valore a cui assegnare un nome per la colonna. Poiché si tratta di una funzionalità beta, la sintassi della `xdm: segmentMembership.ups.seg_id.lastQualificationTime` il valore può cambiare in futuro.

![Registrazione schermata che mostra l’ora dell’ultima qualifica Incolla l’attributo XDM nel passaggio di mappatura](/help/destinations/ui/last-qualification-time.gif)

## Ulteriori informazioni {#more-information}

Per informazioni dettagliate sull’attivazione dei dati in destinazioni basate su file, compresi tutti i passaggi del flusso di lavoro e le autorizzazioni necessarie, leggi la [esercitazione sull&#39;attivazione di destinazioni basate su file](/help/destinations/ui/activate-batch-profile-destinations.md).
