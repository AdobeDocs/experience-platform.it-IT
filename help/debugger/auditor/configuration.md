---
title: Riferimento test di configurazione
description: Scopri come la funzione di auditor verifica le configurazioni in Adobe Experience Platform Debugger.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 797d4f305b4a6884ada4e0619beadff6a45ab42d
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 52%

---

# Riferimento test di configurazione

Questo riferimento fornisce ulteriori informazioni sul modo in cui la funzione auditor in Adobe Experience Platform Debugger esegue i test di configurazione.

>[!NOTE]
>
>Per ulteriori informazioni sui test dell&#39;auditor in Platform Debugger, consulta la [panoramica delle funzionalità dell&#39;auditor](./overview.md).

I test di configurazione eseguono la ricerca di impostazioni, valori o potenziali conflitti specifici nell’implementazione. Platform Auditor valuta i tag rispetto ad altre regole e best practice consigliate.

| Test | Spessore | Criteri | Consiglio |
| --- | --- | --- | --- |
| Advertising Cloud - I nomi di conversione utilizzano solo caratteri alfanumerici | 3 | Il parametro `ev_conversion_property_name` può contenere solo valori numerici e decimali ECCETTO il parametro `ev_transid`, che può contenere valori di testo o numerici. Cerca `everesttech.net` pixel che contengono un parametro URL che inizia con `ev_`. | Assicurati che i parametri delle proprietà della transazione contengano solo valori numerici e decimali.<br><br>Avviso: qualsiasi altro tipo di valore potrebbe causare la perdita di dati. |
| Advertising Cloud - I nomi di conversione utilizzano caratteri URL-safe | 3 | I nomi delle proprietà di conversione non devono contenere una e commerciale o un punto interrogativo. | Assicurati che i parametri della proprietà della transazione non contengano una e commerciale o un punto interrogativo non codificati. Interrompono il formato URL.<br><br>Avviso: i parametri di proprietà che contengono una e commerciale o un punto interrogativo non codificati (ad esempio: `ev_formComplete?=1` o `ev_formComplete&Submit=1`) potrebbero causare la perdita di dati. |
| Advertising Cloud - ID transazione implementato correttamente | 1 | Il nome proprietà `ev_transid=` non può essere vuoto. | Il nome della proprietà `ev_transid=` non deve essere lasciato senza un valore. Se lasciato senza valori, potrebbe verificarsi una perdita di dati della transazione. Assegnare un valore a `ev_transid=` o rimuovere il parametro dal pixel. |
| Analytics - Istanziato in DOM | 5 | Il codice Adobe Analytics non è installato o l’esecuzione non è riuscita. Restituisce 0 quando non viene trovato alcun codice Analytics nella pagina web. | Verifica che il tag Analytics sia implementato nella pagina e non sia bloccato dalle attività di script successive.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics - Istanziato una volta | 5 | Il codice Adobe Analytics è stato rilevato più di una volta nella pagina. Restituisce 0 se nella pagina web non è presente alcun codice A-nalytics. | Accertati che nella pagina sia presente un solo tag Analytics.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics - Versione più recente | 3 | Nelle pagine non è in esecuzione la versione più recente della libreria di codici di Analytics. Le librerie di codici che alimentano le tecnologie Experience Cloud vengono costantemente aggiornate e modificate al fine di trarre vantaggio dai miglioramenti delle prestazioni e fornire le funzionalità più recenti. Restituisce 0 quando non viene trovato alcun codice Analytics nella pagina web. | Installa la versione più recente della libreria Analytics.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=it) |
| Launch - I tag di terze parti vengono caricati in modo asincrono dopo l’evento DOM ready | 3 | Per trovare un compromesso tra una buona esperienza utente e la raccolta di dati accurati, i tag di terze parti devono essere attivati durante l’evento DOM ready. In questo modo gli script di tracciamento verranno eseguiti senza influire sulle funzionalità del sito. | Per risolvere questo problema, regola tutte le regole che eseguono pixel di terze parti in modo che vengano attivate in corrispondenza di DOM Ready.<br><br>[Informazioni aggiuntive](../../tags/ui/managing-resources/rules.md) |
| Servizio ID Experience Cloud - Versione più recente | 2 | Nelle pagine non è in esecuzione la versione più recente della libreria di codici del servizio Visitor ID, visitorAPI.js. Le librerie di codici che alimentano le tecnologie Experience Cloud vengono costantemente aggiornate e modificate al fine di trarre vantaggio dai miglioramenti delle prestazioni e fornire le funzionalità più recenti. | Installa la versione più recente della libreria del servizio Visitor ID.<br><br>[Informazioni aggiuntive](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch - Versione più recente | 2 | Nelle pagine non è in esecuzione la versione più recente della libreria di codici dei tag (Turbine). Le librerie di codici che alimentano le tecnologie Experience Cloud vengono costantemente aggiornate e modificate al fine di trarre vantaggio dai miglioramenti delle prestazioni e fornire le funzionalità più recenti. | Rigenera e pubblica la libreria di tag.<br><br>[Informazioni aggiuntive](../../tags/quick-start/quick-start.md) |
| Target - Versione più recente | 2 | Nelle pagine non è in esecuzione la versione più recente della libreria di codici di Target. Le librerie di codici che alimentano le tecnologie Experience Cloud vengono costantemente aggiornate e modificate al fine di trarre vantaggio dai miglioramenti delle prestazioni e fornire le funzionalità più recenti. | Installa la versione più recente della libreria Target.<br><br>[Informazioni aggiuntive](https://developer.adobe.com/target/implement/client-side/) |
| Target - mboxDefault precede mboxCreate | 5 | L&#39;utilizzo corretto di mboxCreate è simile al seguente:<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Assicurarsi di includere un tag `<div class="mboxDefault"></div>` prima di richiamare mboxCreate(). at.js non ne aggiungerà uno.<br><br>[Informazioni aggiuntive](https://developer.adobe.com/target/implement/client-side/) |
| Target - DOCTYPE valido | 5 | È stato rilevato un DOCTYPE non valido. In questo scenario non verrà attivata alcuna mbox.  Per at.js, il DOCTYPE deve essere in modalità Standard oppure Target non funzionerà. | Aggiorna il DOCTYPE nella pagina.<br><br>[Informazioni aggiuntive](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style="table-layout:auto"}
