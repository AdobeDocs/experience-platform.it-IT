---
title: Scheda Riepilogo
description: Scopri come utilizzare la scheda Riepilogo in Adobe Experience Platform Debugger.
keywords: debugger;estensione debugger di Experience Platform;chrome;estensione;riepilogo;cancellare;richieste;schermata di riepilogo;soluzione;informazioni;analytics;target;dtm;audience manager;launch;servizio id
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: f94bba7eb4763230dae6794eb70a75f53a853c53
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 73%

---

# Scheda Riepilogo

Per eseguire Adobe Experience Platform Debugger, apri la pagina da esaminare nel browser, quindi seleziona l’icona (![](images/start-icon.jpg)) sulla barra del browser. L’estensione si apre su **Riepilogo** scheda.

![](images/summary.jpg)

La schermata contiene informazioni su ciascuna soluzione Adobe Experience Cloud. Le informazioni visualizzate variano in base alla soluzione, ma in genere includono informazioni quali la libreria e la versione della soluzione (ad esempio, “AppMeasurement v2.9”) e gli identificatori dell’account (come l’ID suite di rapporti di Analytics, il codice client di Target, l’ID partner di Audience Manager e così via).

## Informazioni visualizzate in Experience Platform Debugger

Experience Platform Debugger mostra le seguenti informazioni per ciascuna soluzione:

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Suite di rapporti </p> </td> 
   <td colname="col2"> <p>Una <a href="https://experiencecloud.adobe.com/resources/help/it_IT/reference/report_suites_admin.html" format="html" scope="external"> suite di rapporti</a> definisce il reporting indipendente e completo su un sito web scelto, su un insieme di siti web o su un sottoinsieme di pagine web. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versione </p> </td> 
   <td colname="col2"> <p>Versione <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=it" format="html" scope="external"> AppMeasurement</a> definita per la pagina. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versione visitatore </p> </td> 
   <td colname="col2"> <p>Versione della libreria <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=it" format="html" scope="external"> ID visitatore</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome pagina </p> </td> 
   <td colname="col2"> <p>Variabile <a href="https://experiencecloud.adobe.com/resources/help/it_IT/sc/implement/pageName.html" format="html" scope="external"> pageName</a> inviata ad Analytics che contiene un nome semplice del sito. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Moduli </p> </td> 
   <td colname="col2"> <p>Moduli caricati da Adobe Analytics. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Partner </p> </td> 
   <td colname="col2"> <p>Il <a href="https://experiencecloud.adobe.com/resources/help/it_IT/aam/r_dil_get_partner.html" format="html" scope="external">nome del partner</a> per l’istanza DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versione </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/it_IT/aam/r_api_return_versions_dil.html" format="html" scope="external"> Numero di versione</a> per l’istanza DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/it_IT/aam/ids-in-aam.html" format="html" scope="external">ID utente univoco</a> associato all’istanza DIL. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Tag Adobe Experience Platform**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Nome </p> </td> 
   <td colname="col2"> <p>Nome del tag <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html" format="https" scope="external"> proprietà</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versione </p> </td> 
   <td colname="col2"> <p>Versione di Turbine.</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Data build </p> </td> 
   <td colname="col2"> <p>Il tag <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html" format="https" scope="external"> libreria</a> data build </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Ambiente </p> </td> 
   <td colname="col2"> <p>Il <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" format="https" scope="external"> ambiente</a> utilizzato dalla libreria di tag </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Estensioni </p> </td> 
   <td colname="col2"> <p>Estensioni utilizzate nella pagina. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform Web SDK**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Versione libreria </p> </td> 
   <td colname="col2"> <p>Numero della <a href="https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-ext-release-notes.html" format="html" scope="external">versione della libreria</a> dell’SDK web di Adobe Experience Platform. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namespace</p> </td> 
   <td colname="col2"> <p>Nome identificato nell’estensione.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID proprietà </p> </td> 
   <td colname="col2"> <p>Nome della proprietà tag specificata nell’estensione </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Dominio Edge </p> </td> 
   <td colname="col2"> <p>Dominio da cui l’estensione Adobe Experience Platform invia e riceve i dati. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID organizzazione IMS </p> </td> 
   <td colname="col2"> <p>Organizzazione a cui si desidera inviare i dati in Adobe, come specificato nell’estensione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Registrazione abilitata </p> </td> 
   <td colname="col2"> <p>Specifica se la registrazione è stata abilitata per questa proprietà.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Servizio Adobe Experience Cloud ID**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>ID organizzazione Experience Cloud </p> </td> 
   <td colname="col2"> <p>Il tuo <a href="https://experiencecloud.adobe.com/resources/help/it_IT/mcvid/" format="https" scope="external"> Organization ID</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versione </p> </td> 
   <td colname="col2"> <p>Versione della libreria<a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=it" format="html" scope="external"> ID visitatore</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Codice client </p> </td> 
   <td colname="col2"> <p>Il <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external"> Codice client </a> di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versione </p> </td> 
   <td colname="col2"> <p>La versione corrente di <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external"> at.js</a> o mbox.js. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome richiesta globale </p> </td> 
   <td colname="col2"> <p>La<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> mbox globale</a> si riferisce alla singola chiamata server effettuata nella parte superiore di ogni pagina web nell’implementazione di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Evento caricamento pagina </p> </td> 
   <td colname="col2"> <p>Tipo di <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=it" format="html" scope="external">evento</a> che attiva il caricamento della pagina. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome richiesta </p> </td> 
   <td colname="col2"> <p>Nome di una richiesta relativa a una <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> posizione</a> sulla pagina. Disponibile senza autenticazione solo se implementi il listener di eventi Debugging nel codice o nel gestore di tag e attivi i <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> token di risposta necessari</a> nell’interfaccia utente di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome attività </p> </td> 
   <td colname="col2"> <p>Il nome della <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external"> campagna o dell’attività</a> Target. Disponibile senza autenticazione solo se implementi il listener di eventi Debugging nel codice o nel gestore di tag e attivi i <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> token di risposta necessari</a> nell’interfaccia utente di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Attività ID </p> </td> 
   <td colname="col2"> <p>ID dell’attività Target. Disponibile senza autenticazione solo se implementi il listener di eventi Debugging nel codice o nel gestore di tag e attivi i <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> token di risposta necessari</a> nell’interfaccia utente di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome esperienza </p> </td> 
   <td colname="col2"> <p>Il nome dell’<a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external"> esperienza</a> Target. Disponibile senza autenticazione solo se implementi il listener di eventi Debugging nel codice o nel gestore di tag e attivi i <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> token di risposta necessari</a> nell’interfaccia utente di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID esperienza </p> </td> 
   <td colname="col2"> <p>ID dell’esperienza Target. Disponibile senza autenticazione solo se implementi il listener di eventi Debugging nel codice o nel gestore di tag e attivi i <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> token di risposta necessari</a> nell’interfaccia utente di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nome Nome</p> </td> 
   <td colname="col2"> <p>Nome dell’<a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external"> offerta</a> Target. Disponibile senza autenticazione solo se implementi il listener di eventi Debugging nel codice o nel gestore di tag e attivi i <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> token di risposta necessari</a> nell’interfaccia utente di Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID offerta </p> </td> 
   <td colname="col2"> <p>ID dell’offerta Target. Disponibile senza autenticazione solo se implementi il listener di eventi Debugging nel codice o nel gestore di tag e attivi i <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> token di risposta necessari</a> nell’interfaccia utente di Target. </p> </td> 
  </tr> 
 </tbody> 
</table>
