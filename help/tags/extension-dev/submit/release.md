---
title: Rilasciare un’estensione
description: Scopri come rilasciare un’estensione tag in Adobe Experience Platform in modo privato o pubblico.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 93%

---

# Rilasciare un’estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Una volta completati i test e la documentazione, l’estensione è pronta per il rilascio. Attualmente è possibile eseguire due tipi di rilascio:

- **Rilascio privato**: l’estensione completata è disponibile per tutte le proprietà della tua società ma non per altre società presenti in Adobe Experience Platform.
- **Rilascio pubblico**: l’estensione completata è disponibile nel marketplace pubblico per tutti gli utenti di Adobe Experience Platform. 

>[!NOTE]
>
>Dopo che avrai rilasciato l’estensione, non sarà più possibile modificarla né annullarla.  Una volta rilasciata, sarà possibile implementare eventuali correzioni di bug e nuove funzionalità pubblicando (`POST`) una nuova versione del pacchetto dell’estensione e seguendo di nuovo per la nuova versione i passaggi di verifica e rilascio indicati sopra.

Per poter rilasciare l’estensione pubblicamente, è necessario rilasciarla innanzitutto come estensione privata.

## Rilascio privato

Il modo più semplice per rilasciare l’estensione a disponibilità privata è tramite lo strumento [Releaser per estensioni tag](https://www.npmjs.com/package/@adobe/reactor-releaser). Ulteriori istruzioni sono reperibili nella relativa documentazione.

Se desideri rilasciare l’estensione a disponibilità privata utilizzando direttamente le API, consulta la chiamata di esempio per [rilasciare il pacchetto di un’estensione in forma privata](../../api/endpoints/extension-packages.md/#private-release). nella documentazione delle API.

## Rilascio pubblico

Una volta completato il rilascio privato dell’estensione, puoi chiedere ad Adobe di rilasciarla pubblicamente.  In questo modo l’estensione sarà disponibile nel catalogo pubblico. Qualsiasi utente di Data Collection può installare l’estensione in qualsiasi proprietà.

Per avviare il processo di rilascio, completa il [modulo di richiesta di rilascio pubblico](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest).
