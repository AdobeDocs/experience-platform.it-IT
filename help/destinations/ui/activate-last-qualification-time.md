---
title: Utilizza l’ultimo attributo XDM del tempo di qualificazione nelle nuove destinazioni di archiviazione cloud beta
description: Scopri come utilizzare l’attributo XDM dell’ultimo tempo di qualificazione nelle nuove destinazioni di archiviazione cloud beta
hidefromtoc: y
hide: y
source-git-commit: 03031dcaad82932f92e76177adf3b55447c3c153
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Utilizza l’ultimo attributo XDM del tempo di qualificazione nelle nuove destinazioni di archiviazione cloud beta {#last-qualification-time}

>[!IMPORTANT]
> 
>Questa pagina descrive la funzionalità in versione beta. La funzionalità e la documentazione sono soggette a modifiche. Contatta il tuo rappresentante di Adobe o l’Assistenza clienti se desideri accedere a questo programma beta.

## Prerequisiti {#prerequisites}

Per utilizzare l&#39;ultima ora di qualificazione (`lastQualificationTime`) Attributo XDM, devi essere iscritto nel [programma beta](/help/release-notes/2022/october-2022.md#destinations) per utilizzare la funzionalità di esportazione file migliorata ed esportare i dati in uno dei sei [destinazioni di archiviazione cloud beta](/help/release-notes/2022/october-2022.md#destinations) ([[!DNL ADLS Gen 2]](/help/destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](/help/destinations/catalog/cloud-storage/azure-blob.md), [[!DNL Data Landing Zon]e](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [SFTP](/help/destinations/catalog/cloud-storage/sftp.md)). Sei iscritto se puoi vedere le nuove schede beta per le destinazioni di archiviazione cloud nel catalogo, come mostrato di seguito per [!DNL Amazon S3].

![Immagine che mostra la nuova scheda beta di Amazon S3](/help/destinations/assets/ui/activate-destinations/new-amazon-s3-beta-card.png)

## Come utilizzare l&#39;attributo XDM dell&#39;ultimo tempo di qualificazione {#how-to-use}

Se utilizzi uno dei sei nuovi connettori beta per l’archiviazione cloud, puoi utilizzare l’ultimo attributo XDM del tempo di qualificazione in [fase di mappatura](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) del flusso di lavoro di attivazione per creare una colonna nel file esportato con la marca temporale più recente di quando un profilo si qualifica per un segmento. Questo può essere utile per alcuni casi d’uso di misurazione o analisi, oltre a fornire un’idea migliore di quando attivare determinati tipi di pubblico.

Aggiungi `lastQualificationTime` alle esportazioni di file, al momento è necessario inserire manualmente il valore `xdm: segmentMembership.ups.seg_id.lastQualificationTime` nel campo sorgente, come illustrato di seguito. Puoi anche modificare il campo di destinazione in `lastQualificationTime` o qualsiasi altro valore che si desidera assegnare a questa colonna. Poiché si tratta di una funzionalità beta, la sintassi della `xdm: segmentMembership.ups.seg_id.lastQualificationTime` Il valore può cambiare in futuro.

![Registrazione dello schermo che mostra l&#39;ultima volta in cui l&#39;attributo XDM viene incollato nella fase di mappatura](/help/destinations/ui/last-qualification-time.gif)

## Ulteriori informazioni {#more-information}

Per informazioni dettagliate sull’attivazione dei dati alle destinazioni basate su file, compresi tutti i passaggi del flusso di lavoro e le autorizzazioni necessarie, consulta la sezione [esercitazione su come attivare destinazioni basate su file](/help/destinations/ui/activate-batch-profile-destinations.md).