---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Guida introduttiva alla piattaforma dati cliente  Adobe in tempo reale
seo-title: Guida introduttiva alla piattaforma dati cliente  Adobe in tempo reale
description: Scenario di esempio per  Adobe Real-time Customer Data Platform
seo-description: Scenario di esempio per  Adobe Real-time Customer Data Platform
translation-type: tm+mt
source-git-commit: 54df4778a025811504801306120bda78e04281c1
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 0%

---


# Guida introduttiva alla piattaforma dati cliente  Adobe in tempo reale

Questa guida introduttiva illustra un esempio di implementazione  piattaforma dati cliente in tempo reale (Real-time CDP, Real-time CDP) del Adobe. Potete utilizzarlo come esempio per configurare la vostra implementazione. Anche se questa guida mostra esempi specifici, contiene collegamenti verso informazioni aggiuntive utilizzabili durante la creazione della configurazione.

Questo esempio mostra la potenza  piattaforma dati cliente in tempo reale Adobe, basata su Adobe Experience Platform, per:

* Acquisizione di dati da più origini
* Unirli in un unico [!DNL real-time customer profile]
* Offri un&#39;esperienza coerente, rilevante e personalizzata tra i dispositivi.

## Caso d’uso

Luma, una compagnia di abbigliamento atletico, cerca sempre di migliorare la loro esperienza cliente. Hanno una nuova iniziativa per aumentare le vendite relative ai regali. Vogliono anche ridurre la sovraesposizione, come annunci fastidiosi che seguono i clienti.

Attualmente, stanno spendendo troppo sui supporti multimediali che si ritirano rispetto agli elementi che il visitatore non acquisterà andando avanti. Ad esempio, Luma non desidera richiamare un utente con un elemento destinato a essere acquistato una sola volta per un altro utente.

Al momento, i dati di Luma sono dispersi tra più fonti. Di conseguenza, devono affrontare sfide importanti:

* L&#39;organizzazione marketing deve lavorare con diversi team che possiedono ciascuna un&#39;origine dati, inclusi un sito Web, un&#39;app mobile, sistemi fedeltà, CRM e così via.
* Quando il team di marketing accede ai dati, spesso risulta obsoleto e non è più rilevante per la campagna con un fattore temporale sensibile.
* Devono unificare i dati in modo da indirizzare una persona, non i canali.

Di conseguenza, Luma ha i seguenti obiettivi aziendali:

* Crea una visione singola in tempo reale dei loro consumatori dalle loro diverse fonti di dati.
* Personalizza le campagne di marketing con messaggi pertinenti su diversi canali e dispositivi.

Per raggiungere questi obiettivi, il team marketing deve essere in grado di gestire i dati dei clienti su larga scala.

Con CDP in tempo reale, basato su Adobe Experience Platform, l&#39;organizzazione di marketing di Luma può:

1. Raccogliere i dati da piattaforme diverse e assicurarsi che siano disponibili a valle per altre attività di marketing.
1. Crea una visione unica e in tempo reale dei loro consumatori, indipendentemente da dove i dati sono originati.
1. Crea un&#39;esperienza coerente, rilevante e personalizzata in ogni punto di contatto.

## Passaggi

Questa esercitazione include i passaggi seguenti:

1. Crea il profilo [del](#customer-profile)cliente.
1. [Personalizzate](#personalizing-the-user-experience) l&#39;esperienza utente.
1. Utilizzare [più origini](#using-multiple-data-sources)dati.
1. [Configurare un&#39;origine](#configuring-a-data-source)dati.
1. [Raccogliere i dati](#bringing-the-data-together-for-a-specific-customer) per un cliente specifico.
1. Imposta [segmenti](#segments).
1. Configurare [le destinazioni](#destinations).
1. [Stitch il profilo su più dispositivi](#cross-device-identity-stitching).
1. [Analizzare il profilo](#analyzing-the-profile).

## Customer profile

La prima volta che i clienti visitano il tuo sito, non sai nulla di loro.

![immagine](assets/luma-site.png)

Mentre si spostano, i dati vengono acquisiti in tempo reale e inviati non solo a una suite di rapporti in  Adobe Analytics, ma anche direttamente ad Adobe Experience Platform. Quando i dati vengono raccolti, si inizia a formare una singola vista del consumatore, basata sui dati comportamentali contenuti in [!DNL Experience Platform's real-time customer profile].

Molti visitatori del sito Web sono probabilmente clienti ripetuti che hanno precedentemente acquistato da Luma.  Per Luma è importante personalizzare messaggi e offerte per i visitatori nuovi e ripetuti, nonché per i clienti noti.

### Prima visita del cliente

Ad esempio, un visitatore non identificato accede alla sezione Uomo del sito Luma e visualizza una coppia di maglie in esecuzione.

![immagine](assets/luma-sweatshirts.png)

Quando il cliente fa clic per saperne di più su questi prodotti, queste visualizzazioni di prodotto vengono raccolte  Adobe Analytics e inviate a [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma può mappare il comportamento del visitatore su un profilo utente su Adobe Experience Platform e iniziare a ricavare una visione più completa del comportamento del consumatore.

### Visualizzazione più dettagliata del cliente

Mentre il cliente continua a interagire con il sito Web, emerge un&#39;immagine più chiara. Ad esempio, supponiamo che il visitatore aggiunga un prodotto al carrello e acceda.

Quando il cliente accede, si identifica come Sarah Rose.

![immagine](assets/luma-login.png)

Vengono unite due identità:

* I dati di navigazione anonimi
* I dati esistenti associati al conto di Sarah Rose

Entrambe le identità sono combinate in un unico profilo in [!DNL Experience Platform]. La luma ha ora una visione unificata di questo consumatore.

In base al comportamento di navigazione del visitatore anonimo nella sezione Uomo del sito, si potrebbe supporre che il cliente fosse un maschio. Ora che ha effettuato l’accesso, Luma riconosce Sarah Rose. Luma utilizza la potenza del [!DNL Real-time Customer Profile] sistema per perfezionare i messaggi che le vengono trasmessi attraverso i canali.

## Personalizzazione dell&#39;esperienza utente

Sarah è accolta con un messaggio di fedeltà e ringraziata per essere un membro del Bronzo con maggiori informazioni sui benefici e come aumentare il suo status e punti.

Fa clic sulla home page per ulteriori informazioni.

![immagine](assets/luma-personal.png)

Sarah riceve un&#39;esperienza di home page personalizzata che viene distribuita in modo dinamico, in base a lei [!DNL Real-time Customer Profile] in Adobe Experience Platform.

Vede contenuti rilevanti, grazie  personalizzazione basata su Adobe Sensei in  Adobe Target, che tiene conto dei suoi acquisti passati e dell&#39;affinità verso l&#39;uso di abbigliamento e abbigliamento. Luma inoltre adatta il contenuto del catalogo degli uomini verso l&#39;attrezzatura di marcia per gli uomini in base alla sua ricerca più recente.

Più in basso nella pagina, Sarah viene mostrato i prodotti in evidenza, così come un nuovo vassoio delle raccomandazioni basato sui suoi ultimi elementi visualizzati.

Questo contenuto personalizzato aiuta Sarah a trovare rapidamente gli elementi rilevanti. Questo aumenta le conversioni e offre un&#39;esperienza cliente più piacevole.

### Riportare il cliente

Sarah si distrae e lascia il sito, terminando la sessione. Luma può usare i suoi dati in Adobe Experience Platform per aiutarla a riportarla sul sito.

 Adobe Real-time Customer Data Platform, basato su Adobe Experience Platform, è progettato per la gestione dell&#39;esperienza dei clienti. Consente alle organizzazioni di:

* Integrazione e attivazione dei dati semplificata
* Gestione dell&#39;utilizzo dei dati noti e sconosciuti
* Accelerare i casi di utilizzo del marketing su larga scala

## Utilizzo di più origini dati

Il team di Luma dispone di tutti i dati comportamentali e dei clienti in un&#39;unica posizione.

![immagine](assets/luma-dash.png)

Possono acquisire dati da tutte le origini seguenti:

* Dati delle soluzioni Adobe Experience Cloud esistenti
* Origini non  Adobe, come il programma fedeltà di Luma, i dati del call center e del sistema di punti vendita
* Dati in streaming in tempo reale da origini dati Luma
* Dati in tempo reale dalle soluzioni  Adobe (non sono necessari nuovi tag)

Tutti questi dati provenienti da origini diverse vengono uniti in un unico profilo cliente unificato.

## Configurazione di un’origine dati

Utilizzare [!DNL Real-time Customer Data Platform] per portare nuove origini di dati nella piattaforma. CDP in tempo reale include un catalogo di origini dati che possono essere aggiunte al profilo con pochi clic.

![immagine](assets/luma-source-cat.png)

Ad esempio, per acquisire i dati CRM di Luma, filtrare il catalogo in base a *CRM* e vengono elencati tutti i connettori out-of-the-box contenenti *CRM* . Per aggiungere [!DNL Microsoft Dynamics CRM] dati:

1. Autorizzate la connessione.

   ![immagine](assets/luma-source-auth.png)

1. Scegliete cosa importare da un elenco consigliato di tabelle XDM pre-mappate.

   <!--    ![image](assets/luma-source-import.png) -->

   Ad esempio, selezionare **[!UICONTROL Contacts]**. L&#39;anteprima dei dati dei contatti viene caricata automaticamente in modo da poter verificare che l&#39;aspetto sia quello previsto.

   La piattaforma Adobe Experience Traccia molto del lavoro manuale da questo processo mappando automaticamente i campi standard allo schema di profilo [!DNL Experience Data Model] (XDM).

1. Esaminare le mappature dei campi.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Ad esempio, verificate che il campo e-mail per i contatti sia mappato correttamente.\
   È possibile visualizzare in anteprima i dati ed eseguire la mappatura avanzata.

1. Impostate una pianificazione.

   ![immagine](assets/luma-source-sched.png)

È fatta. Hai appena aggiunto [!DNL Microsoft CRM] come origine dati in [!DNL Experience Platform].

### Etichettatura dei dati acquisiti per i criteri di utilizzo

Luma ha molte politiche interne che limitano l&#39;uso di certi tipi di informazioni raccolte, e devono anche rispettare le preoccupazioni legali e sulla privacy relative all&#39;utilizzo dei dati. Utilizzando Adobe Experience Platform [!DNL Data Governance]è possibile applicare etichette di utilizzo dati predefinite ai set di dati (e a campi specifici all&#39;interno di tali set di dati), consentendo a Luma di suddividere i dati in categorie in base a specifiche restrizioni di utilizzo.

![](assets/governance-labels.png)

Una volta applicate le etichette di utilizzo dei dati, Luma può quindi utilizzare [!DNL Data Governance] per creare criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni consentite sui dati che contengono determinate etichette. Quando si tenta di eseguire un&#39;azione in tempo reale CDP che costituisce una violazione della politica, l&#39;azione viene impedita e viene segnalato un avviso per indicare quale politica è stata violata e perché.

## Raggruppamento dei dati per un cliente specifico

In questo scenario, cercate i profili per Sarah Rose. Viene visualizzato il suo profilo, con l&#39;e-mail che ha usato per effettuare l&#39;accesso.

<!-- ![image](assets/luma-find-profile.png) -->

Tutte le informazioni di profilo che Luma ha su Sarah display. Questo include informazioni personali come indirizzo e numero di telefono, preferenze di comunicazione e i segmenti per i quali si qualifica.

| Categoria | Descrizione |
|---|---|
| Identità | Mostra le identità che sono state collegate tra loro [!DNL Platform] dalle interazioni di Sarah con Luma attraverso canali e dispositivi. Viene visualizzato il suo ECID dal sito Web. La sua identità include anche l&#39;ECID dalla sua app mobile, il suo ID e-mail, un ID CRM dal [!DNL Microsoft Dynamics] set di dati aggiunto di recente e un ID fedeltà passato in Adobe Experience Platform dal sistema lealtà Luma. |
| Eventi | Mostra tutti i dati di interazione di Sarah con il marchio Luma. Questo include l&#39;elemento che ha appena visualizzato, tutto ciò che ha visto in passato, le e-mail che ha ricevuto, le interazioni con il call center, e quale canale e dispositivo ha attivato ciascuna di queste interazioni. |

Il profilo CDP in tempo reale riduce il flusso di lavoro del team di marketing Luma da settimane a minuti e svela le possibilità di personalizzazione in base a questa visualizzazione cliente a 360 gradi. Il profilo unisce i dati comportamentali da quando ha consultato il sito prima di accedere, con il profilo cliente esistente, creando una visione completa di Sarah.

Il team marketing può utilizzare questa funzionalità avanzata [!DNL Real-time Customer Profile] per personalizzare meglio l&#39;esperienza di Sarah e aumentare la sua fedeltà al marchio con Luma.

## Segmenti

Le potenti funzionalità di segmentazione di Adobe Experience Platform consentono agli esperti di marketing di combinare attributi, eventi e segmenti esistenti, in base ai dati acquisiti nel [!DNL Real-time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

In questo scenario, le recenti interazioni di Sarah sul sito mostrano un comportamento diverso rispetto alle sue azioni passate. Di solito compra l&#39;abbigliamento femminile. Tuttavia, l&#39;articolo nel suo carrello è una maglia grande da uomo.

Il team scientifico dei dati Luma ha creato dei modelli sulla propensione all&#39;acquisto. Un modello identifica un cambiamento improvviso nella categoria degli indumenti (ad esempio uomini/donne) o nella dimensione per il consumatore esistente. Il cambiamento nel comportamento di acquisto di Sarah suggerisce che non sta facendo acquisti da sola.

<!-- ![image](assets/luma-gift.png) -->

### Definizione di un segmento

Modifica o crea un segmento che rappresenta gli abbandonatori del carrello che sembrano essere nel processo di acquisto di un regalo:

```
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

Dato che Sarah ha aggiunto un oggetto regalo apparente nel carrello e lo ha abbandonato, Luma può mirare con un&#39;offerta regalo gratuita.

## Destinazioni

Quando hai aggiunto il segmento &quot;Regalo agli abbandonatori del carrello&quot;, puoi vedere più o meno quante persone fanno parte di questo segmento. Puoi agire su di esso e renderlo disponibile per la personalizzazione su più canali.

Fai clic su **[!UICONTROL Send to destinations]**.

In  CDP in tempo reale, Luma può agire direttamente sui segmenti di pubblico per la personalizzazione.\
Qui vediamo tutte le destinazioni disponibili per Luma per l&#39;invio di questa destinazione, sia  soluzioni di Adobe che non :

![immagine](assets/luma-dest.png)

### Selezione delle destinazioni

In questo scenario, Luma desidera riassegnare l&#39;audience con la personalizzazione tra le seguenti destinazioni:

* Google, per la visualizzazione

   <!--* Facebook -->
*  Adobe Campaign, per e-mail

<!-- ![image](assets/luma-sched-dest.png) -->

### Destinazioni di programmazione

Puoi anche pianificare l’inizio o la fine del segmento in un dato momento. Il segmento verrà pubblicato e aggiornato automaticamente nelle piattaforme configurate alle date pianificate.

>[!NOTE]
>Se si fa clic nel campo data, il programma viene pianificato automaticamente per 90 giorni.

Fare clic **[!UICONTROL Save]** per passare alla pagina successiva.

Quando un cliente di questo pubblico effettua un acquisto, la sua appartenenza a questo pubblico viene soppressa in tempo reale. Non si qualificano più perché il loro stato è cambiato.

In questo modo, il direttore del team multimediale Luma risparmia centinaia di migliaia di dollari, evitando di utilizzare scorte per un pubblico non qualificato.

### Applicazione dei criteri di utilizzo dei dati per le destinazioni

Adobe Experience Platform include controlli sulla privacy e sulla sicurezza per stabilire se un segmento è disponibile per essere attivato a una particolare destinazione. L&#39;attivazione è abilitata o limitata in base agli scopi di marketing assegnati alla destinazione al momento della creazione, nonché ai criteri di utilizzo dei dati definiti dall&#39;organizzazione.

Se l&#39;attività viola il criterio, viene visualizzato un avviso. Questo avviso contiene informazioni sulla linea di dati che possono essere utili per identificare il motivo della violazione del criterio e le azioni che è possibile eseguire per risolvere la violazione.

Con questi controlli, [!DNL Experience Platform] aiuta Luma a rispettare le normative e a commercializzare in modo responsabile. Questi controlli sono flessibili e possono essere modificati per soddisfare i requisiti dei team di sicurezza e governance di Luma, consentendo loro di soddisfare con sicurezza i requisiti regionali e organizzativi per la gestione dei dati noti e sconosciuti dei clienti.

### Area di lavoro del flusso di dati

Durante il salvataggio, un&#39;area di dati visiva mostra il segmento mappato dal profilo unificato alle tre destinazioni selezionate.

![immagine](assets/luma-flow.png)

## Cucitura identità tra dispositivi

Sarah naviga su un sito di social media sul suo dispositivo mobile e vede una pubblicità Luma. Le ricorda l&#39;oggetto che ha lasciato nel suo carrello.

In seguito, apre la sua e-mail e visualizza le e-mail ritirate. Fa clic su un collegamento a Luma da un&#39;e-mail.

Il link porta Sarah alla homepage di Luma mobile, dove vede un&#39;esperienza altamente personalizzata con  Adobe Target.

* È accolta come membro del Bronzo.
* Vede il messaggio &quot;Regalo&quot;.
* Vede anche il messaggio &quot;Free Gift Wrap&quot;, che fa parte dei benefici della sua iscrizione al Bronzo.
* È ancora nel mirino dell&#39;immagine hero, in base alla sua affinità di correre.

Compra il maglione, aggiunge un involucro regalo e scrive una nota regalo. Ha anche la possibilità di ricordare questo evento e ottenere un promemoria l&#39;anno prossimo per ottenere in regalo in questo momento. Dice di sì, ed è programmata per una campagna email l&#39;anno successivo per ricordarle di comprare un altro regalo.

Grazie alle capacità di soppressione del pubblico, Sarah non sarà preso di mira con il maglione di quell&#39;uomo che va avanti.

## Analisi del profilo

Gli esperti di marketing della luma utilizzano Adobe Experience Platform per esaminare il segmento dei donatori nel dashboard CDP in tempo reale. Vedono i risultati di questa iniziativa nel tempo e vedono che sta crescendo. I clienti rispondono alle offerte e spendono più denaro.

Queste informazioni consentono agli esperti di marketing di agire su questo segnale, che è stato alimentato dalla disponibilità di questi dati in CDP e dall&#39;associazione di clienti come Sarah al segmento.

Luma utilizza questi dati CDP per aumentare la fedeltà e la soddisfazione dei clienti.
