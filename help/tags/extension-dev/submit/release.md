---
title: Rilasciare un’estensione
description: Scopri come rilasciare un’estensione tag in Adobe Experience Platform in modo privato o pubblico.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 52%

---

# Rilasciare un’estensione

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Una volta completati i test e la documentazione, l’estensione è pronta per la versione. Attualmente è possibile eseguire due tipi di rilascio:

- **Rilascio privato**: l’estensione completata è disponibile per tutte le proprietà della tua società ma non per altre società presenti in Adobe Experience Platform.
- **Versione** pubblica: L’estensione completata è disponibile nel marketplace pubblico per tutti gli utenti di Adobe Experience Platform.

>[!NOTE]
>
>Una volta rilasciata l&#39;estensione, non puoi più apportare modifiche e non puoi annullarla.  Una volta rilasciata, sarà possibile implementare eventuali correzioni di bug e nuove funzionalità pubblicando (`POST`) una nuova versione del pacchetto dell’estensione e seguendo di nuovo per la nuova versione i passaggi di verifica e rilascio indicati sopra.

Per poter rilasciare l’estensione pubblicamente, è necessario rilasciarla innanzitutto come estensione privata.

## Rilascio privato

Il modo più semplice per rilasciare l&#39;estensione con disponibilità privata è quello di utilizzare il [rilasciatore di estensioni di tag](https://www.npmjs.com/package/@adobe/reactor-releaser). Ulteriori istruzioni sono reperibili nella relativa documentazione.

Se desideri rilasciare l&#39;estensione con disponibilità privata utilizzando direttamente l&#39;API, consulta la chiamata di esempio per [rilasciare in privato un pacchetto di estensione](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/release_private/) nei documenti API per ulteriori dettagli.

## Rilascio pubblico

Una volta completato il rilascio privato dell’estensione, puoi chiedere ad Adobe di rilasciarla pubblicamente.  In questo modo l’estensione sarà disponibile nel catalogo pubblico. Qualsiasi utente della raccolta dati può installare l&#39;estensione su qualsiasi proprietà.

Per avviare il processo di rilascio, completa il [modulo di richiesta di rilascio pubblico](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=7DRB5U).
