---
title: Riferimento test presenza tag
description: Scopri come la funzione di auditor verifica la presenza di tag in Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 17%

---

# Riferimento test di presenza tag

Questo riferimento fornisce ulteriori informazioni su come la funzione di auditor in Adobe Experience Platform Debugger verifica la presenza di tag.

>[!NOTE]
>
>Per ulteriori informazioni sui test dell&#39;auditor in Platform Debugger, consulta la [panoramica delle funzionalità dell&#39;auditor](./overview.md).

I test di presenza dei tag valutano se determinati tag esistono nella pagina e se si trovano nella posizione giusta nel codice della pagina.

| Test | Spessore | Criteri | Consiglio |
| --- | --- | --- | --- |
| Advertising Cloud - Presenza di codice | 5 | Il tag Advertising Cloud non è disponibile nel DOM. | Implementa il tag Advertising Cloud utilizzando l&#39;estensione tag [Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Pixel di segmento implementati | 5 | Aggiorna i pixel del segmento di Advertising Cloud ai nuovi tag di sola immagine di Advertising Cloud. L’utilizzo di tag di segmento AMO obsoleti può causare la perdita di dati. | Implementa il pixel del segmento di Advertising Cloud utilizzando l&#39;estensione tag [Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - Caricato nel DOM | 5 | Il tag Adobe Analytics non è stato rilevato. | Installa la versione più recente di Analytics. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Launch - Libreria caricata | 5 | Impossibile trovare un oggetto `global _satellite` nel DOM. La libreria di tag non è installata o non può essere eseguita. | Verifica che la libreria di tag sia implementata nella pagina e non sia bloccata dalle attività di script successive. |
| Launch - Non sono presenti più script incorporati | 5 | I siti di produzione devono caricare un solo codice di incorporamento per pagina. | Verifica che nella pagina venga caricata solo la libreria di produzione. |
| Launch - Il callback `pageBottom` esiste in `<body>` | 5 | Impossibile trovare il callback `_satellite.pageBottom()` richiesto all&#39;interno del `<body>` della pagina. Il test ha esito negativo se la chiamata `pageBottom` non viene trovata nella pagina o se si trova nel tag `<head>` (o in un&#39;altra posizione imprevista). Il test avrà esito positivo solo se `pageBottom` si troverà all&#39;interno del tag `<body>`. | Aggiungere lo script in linea immediatamente prima del tag di chiusura `</body>` per garantire la funzionalità dei tag corretta.<br><br>[Informazioni aggiuntive](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - Il callback `pageBottom` non deve esistere quando viene distribuito in modo asincrono | 5 | Il callback `_satellite.pageBottom()` è stato trovato nella pagina. Ciò non dovrebbe accadere quando i tag vengono distribuiti in modo asincrono. | Rimuovere lo script `_satellite.pageBottom()` per abilitare la funzionalità dei tag corretta. <br><br>[Informazioni aggiuntive](../../tags/ui/client-side/asynchronous-deployment.md) |
| Servizio ID Experience Cloud - Presenza di codice | 5 | Codice del servizio Experience Cloud ID non trovato. L’utilizzo degli ID Experience Cloud (ECID) è vivamente consigliato per garantire il massimo valore dalle soluzioni Experience Cloud ed è fondamentale per la gestione ID nelle soluzioni Experience Cloud. | Installa la versione più recente di ECID.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=it) |
| Servizio ID Experience Cloud - Presenza di cookie | 5 | Impossibile trovare il cookie `AMCV_`. Creare un&#39;istanza di un oggetto visitatore dal codice `VisitorAPI.js`. | Se si tratta di un’implementazione di tag, verifica che l’ID AdobeOrg sia stato immesso correttamente nello strumento ECID. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Servizio ID Experience Cloud: valore MID presente | 5 | Valore MID non trovato nel cookie `AMCV_`. | Esegui di nuovo il test per verificare la presenza di eventuali latenze API ECID. Se la condizione persiste, contatta l’Assistenza clienti di Adobe. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - Presenza di codice | 5 | Adobe Target deve essere definito nel DOM. | Installa la versione più recente di Target (at.js). <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - Libreria caricata in `<head>` | 4 | La libreria Target deve essere caricata nel tag `<head>`. | Verificare che la libreria Target sia caricata nel tag `<head>`. <br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
