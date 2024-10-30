---
title: Rilasciare un’estensione
description: Scopri come rilasciare un’estensione tag in Adobe Experience Platform in modo privato o pubblico.
exl-id: a5eb6902-4b0f-4717-a431-a290c50fb5a6
source-git-commit: 2152cf98d9809654cca7abd7b8469a72e8387b2a
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 67%

---

# Rilasciare un’estensione

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch è ora una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Una volta completati i test e la documentazione, l’estensione è pronta per il rilascio. Attualmente è possibile eseguire due tipi di rilascio:

- **Rilascio privato**: l’estensione completata è disponibile per tutte le proprietà della tua società ma non per altre società presenti in Adobe Experience Platform.
- **Rilascio pubblico**: l’estensione completata è disponibile nel marketplace pubblico per tutti gli utenti di Adobe Experience Platform. 

>[!NOTE]
>
>Dopo che avrai rilasciato l’estensione, non sarà più possibile modificarla né annullarla.  Una volta rilasciata, sarà possibile implementare eventuali correzioni di bug e nuove funzionalità pubblicando (`POST`) una nuova versione del pacchetto dell’estensione e seguendo di nuovo per la nuova versione i passaggi di verifica e rilascio indicati sopra.

Prima di poter rilasciare l’estensione pubblicamente, devi rilasciarla come estensione privata.

## Rilascio privato

Il modo più semplice per rilasciare l&#39;estensione a disponibilità privata è tramite il Releaser [estensione tag](https://www.npmjs.com/package/@adobe/reactor-releaser).

```bash
npx @adobe/reactor-releaser
```

`npx` consente di scaricare ed eseguire un pacchetto npm senza installarlo sul computer. Questo è il modo più semplice per eseguire il releaser.

>[!NOTE]
> Per impostazione predefinita, il releaser richiede credenziali di Adobe I/O per un flusso OAuth da server a server. Le credenziali legacy di `jwt-auth`
> può essere utilizzato eseguendo `npx @adobe/reactor-releaser@v3.1.3` fino a quando non diventerà obsoleto il 1° gennaio 2025. Parametri richiesti
> per eseguire la versione `jwt-auth` è possibile trovare [qui](https://github.com/adobe/reactor-releaser/tree/9ea66aa2c683fe7da0cca50ff5c9b9372f183bb5).

Il releaser richiede di inserire solo alcune informazioni. È possibile recuperare `clientId` e `clientSecret` dalla console Adobe I/O. Passa alla [pagina Integrations](https://console.adobe.io/integrations) (Integrazioni) nella console di I/O. Seleziona l’organizzazione adatta dal menu a discesa, individua l’integrazione corretta e seleziona **[!UICONTROL Visualizza]**.

- Qual è `clientId`? è disponibile nella console I/O; usa Copia/Incolla.
- Qual è `clientSecret`? è disponibile nella console I/O; usa Copia/Incolla.

Il releaser leggerà i campi `name` e `platform` dal manifesto dell&#39;estensione ed eseguirà una query sull&#39;API per un pacchetto di estensione corrispondente nella disponibilità di sviluppo.
Il releaser ti chiederà quindi di confermare di aver trovato il pacchetto di estensione corretto da rilasciare a disponibilità privata.

Se desideri rilasciare l’estensione a disponibilità privata utilizzando direttamente le API, consulta la chiamata di esempio per [rilasciare il pacchetto di un’estensione in forma privata](../../api/endpoints/extension-packages.md/#private-release). nella documentazione delle API.

## Rilascio pubblico

Una volta completato il rilascio privato dell’estensione, puoi chiedere ad Adobe di rilasciarla pubblicamente.  In questo modo l’estensione sarà disponibile nel catalogo pubblico. Qualsiasi utente di Data Collection può installare l’estensione in qualsiasi proprietà.

Per avviare il processo di rilascio, completa il [modulo di richiesta di rilascio pubblico](https://www.feedbackprogram.adobe.com/c/r/DCExtensionReleaseRequest).
