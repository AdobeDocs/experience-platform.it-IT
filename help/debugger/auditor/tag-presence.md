---
title: Riferimento test presenza tag
description: Scopri come la funzione di auditor verifica la presenza di tag in Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 31%

---

# Riferimento test di presenza tag

Questa documentazione fornisce ulteriori informazioni su come la funzionalità auditor di Adobe Experience Platform Debugger verifica la presenza di tag.

>[!NOTE]
>
>Per ulteriori informazioni sui test dell’auditor in Platform Debugger, consulta [panoramica della funzione di auditor](./overview.md).

I test di presenza dei tag valutano se determinati tag esistono nella pagina e se si trovano nella posizione giusta nel codice della pagina.

| Test | Peso | Criteri | Consiglio |
| --- | --- | --- | --- |
| Advertising Cloud - Presenza codice | 5 | Il tag Advertising Cloud non è disponibile nel DOM. | Implementare il tag di Advertising Cloud utilizzando [Estensione tag Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Pixel di segmento implementati | 5 | Aggiorna i pixel del segmento di Advertising Cloud ai nuovi tag di sola immagine di Advertising Cloud. L’utilizzo di tag di segmento AMO obsoleti può causare la perdita di dati. | Implementare il pixel del segmento di Advertising Cloud utilizzando [Estensione tag Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - Caricato nel DOM | 5 | Il tag Adobe Analytics non è stato rilevato. | Installa la versione più recente di Analytics. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=it) |
| Launch - Libreria caricata | 5 | A `global _satellite` L’oggetto non è stato trovato nel DOM, il che significa che la libreria di tag non è installata o non può essere eseguita. | Verifica che la libreria di tag sia implementata nella pagina e non sia bloccata dalle attività di script successive. |
| Launch - Non sono presenti più script incorporati | 5 | I siti di produzione devono caricare un solo codice di incorporamento per pagina. | Verifica che nella pagina venga caricata solo la libreria di produzione. |
| Lancio - `pageBottom` il callback esiste in `<body>` | 5 | Il valore richiesto `_satellite.pageBottom()` callback non trovato all&#39;interno del `<body>` della pagina. Il test ha esito negativo se `pageBottom` chiamata non è stata trovata nella pagina o se si trova nella `<head>` (o in un’altra posizione imprevista). Il test avrà esito positivo solo se `pageBottom` si trova da qualche parte all’interno del `<body>` tag. | Aggiungi lo script in linea immediatamente prima della chiusura `</body>` per garantire la funzionalità dei tag corretta.<br><br>[Informazioni aggiuntive](../../tags/ui/client-side/asynchronous-deployment.md) |
| Lancio - `pageBottom` il callback non deve esistere quando viene distribuito in modo asincrono | 5 | Il `_satellite.pageBottom()` callback trovato nella pagina. questo non dovrebbe accadere quando i tag vengono distribuiti in modo asincrono. | Rimuovi il `_satellite.pageBottom()` script per abilitare la funzionalità dei tag corretta. <br><br>[Informazioni aggiuntive](../../tags/ui/client-side/asynchronous-deployment.md) |
| Servizio Experience Cloud ID - Presenza di codice | 5 | Codice del servizio Experience Cloud ID non trovato. L’utilizzo degli ID Experience Cloud (ECID) è vivamente consigliato per garantire il massimo valore dalle soluzioni Experience Cloud ed è fondamentale per la gestione ID nelle soluzioni Experience Cloud. | Installa la versione più recente di ECID.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) |
| Servizio Experience Cloud ID - Presenza di cookie | 5 | Il `AMCV_` cookie non trovato. Devi creare un’istanza di un oggetto visitatore dal codice `VisitorAPI.js` . | Se si tratta di un’implementazione di tag, verifica che l’ID AdobeOrg sia stato immesso correttamente nello strumento ECID. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Servizio Experience Cloud ID - Valore MID presente | 5 | Valore MID non trovato nel `AMCV_` cookie. | Esegui di nuovo il test per verificare la presenza di eventuali latenze API ECID. Se la condizione persiste, contatta l’Assistenza clienti Adobe. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - Presenza di codice | 5 | Adobe Target deve essere definito nel DOM. | Installa la versione più recente di Target (at.js). <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - Libreria caricata in `<head>` | 4 | La libreria Target deve essere caricata in `<head>` tag. | Verifica che la libreria Target sia caricata in `<head>` tag. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
