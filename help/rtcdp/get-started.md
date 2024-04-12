---
keywords: RTCDP;CDP;Real-time Customer Data Platform;real time customer data platform;real time cdp;cdp;rtcdp
title: Guida introduttiva a Real-time Customer Data Platform
description: Utilizza questo scenario di esempio per la configurazione dell’implementazione di Adobe Real-time Customer Data Platform.
feature: Get Started, Use Cases
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 1%

---

# Guida introduttiva a Real-time Customer Data Platform

Questa guida introduttiva illustra un esempio di implementazione di Real-time Customer Data Platform (Real-Time CDP). Puoi utilizzarlo come esempio quando configuri la tua implementazione. Sebbene questa guida mostri esempi specifici, contiene collegamenti a informazioni aggiuntive che è possibile utilizzare durante la creazione della configurazione.

Questo esempio mostra la potenza di Real-time Customer Data Platform, con tecnologia Adobe Experience Platform, per:

* Acquisire dati da più origini
* Uniscili in un’unica [!DNL real-time customer profile]
* Fornisci un’esperienza coerente, rilevante e personalizzata tra i dispositivi.

## Caso d’uso

Luma, un’azienda di abbigliamento sportivo, cerca sempre di migliorare la propria esperienza cliente. Hanno una nuova iniziativa per aumentare le vendite legate ai regali. Vogliono anche ridurre la sovraesposizione, come fastidiosi annunci pubblicitari che seguono i clienti in giro.

Al momento, spendono troppo per i media che eseguono il retargeting per oggetti che il visitatore non acquisterà più. Ad esempio, Luma non vuole effettuare il retargeting di un utente con un articolo destinato all’acquisto una tantum per un altro utente.

Al momento, i dati di Luma sono dispersi tra più sorgenti. Di conseguenza, si trovano ad affrontare sfide importanti:

* L’organizzazione di marketing deve lavorare con vari team che possiedono ciascuno un’origine dati, tra cui un sito web, un’app mobile, sistemi di fidelizzazione, CRM e così via.
* Quando il team marketing ha accesso ai dati, spesso non sono aggiornati e non sono più rilevanti per le campagne sensibili al tempo.
* Devono unificare i dati in modo che eseguano il targeting di una persona, non di canali.

Di conseguenza, Luma ha i seguenti obiettivi aziendali:

* Creare una visualizzazione unica in tempo reale dei propri consumatori da fonti di dati diverse.
* Personalizza le campagne di marketing con messaggi pertinenti su diversi canali e dispositivi.

Per raggiungere questi obiettivi, il team di marketing deve essere in grado di gestire i dati dei clienti su larga scala.

Con Real-Time CDP, con tecnologia Adobe Experience Platform, l’organizzazione di marketing Luma può:

1. Raccogli dati da piattaforme diverse e assicurati che siano disponibili a valle per altre attività di marketing.
1. Crea una visualizzazione unica e in tempo reale dei loro consumatori, indipendentemente da dove provengono i dati.
1. Genera un’esperienza coerente, rilevante e personalizzata in ogni punto di contatto.

## Passaggi

Questo tutorial include i seguenti passaggi:

1. Creare [profilo cliente](#customer-profile).
1. [Personalizzazione](#personalizing-the-user-experience) l’esperienza utente.
1. Utilizzare [più origini dati](#using-multiple-data-sources).
1. [Configurare un’origine dati](#configuring-a-data-source).
1. [Raccogliere i dati](#bringing-the-data-together-for-a-specific-customer) per un cliente specifico.
1. Configurazione [audience](#audiences).
1. Configurazione [destinazioni](#destinations).
1. [Unire il profilo tra i dispositivi](#cross-device-identity-stitching).
1. [Analizzare il profilo](#analyzing-the-profile).

## Profilo cliente

Quando i clienti visitano il tuo sito per la prima volta, non sai nulla su di loro.

![immagine](assets/luma-site.png)

Durante la navigazione, i dati vengono acquisiti in tempo reale e inviati non solo a una suite di rapporti in Adobe Analytics, ma anche direttamente a Adobe Experience Platform. Man mano che i dati vengono raccolti, si inizia a formare un’unica vista del consumatore, basata sui dati comportamentali in [!DNL Experience Platform's real-time customer profile].

Molti visitatori del sito web sono probabilmente clienti frequenti che hanno acquistato in precedenza da Luma.  È importante che Luma personalizzi i messaggi e le offerte per indirizzarli sia ai visitatori nuovi che a quelli ripetuti, nonché ai clienti noti.

### Prima visita del nuovo cliente

Ad esempio, un visitatore non identificato accede alla sezione Uomo del sito Luma e visualizza un paio di felpe running.

![immagine](assets/luma-sweatshirts.png)

Man mano che il cliente accede a questi prodotti, le visualizzazioni vengono raccolte in Adobe Analytics e inviate a [!DNL Experience Platform].

<!--![image](assets/luma-shirt-detail.png)-->

Luma può mappare il comportamento del visitatore su un profilo utente su Adobe Experience Platform e iniziare ad assemblare una visualizzazione più ricca del comportamento del consumatore.

### Visualizzazione più dettagliata del cliente

Mentre il cliente continua a interagire con il sito web, emerge un quadro più chiaro. Ad esempio, supponiamo che il visitatore aggiunga un prodotto al carrello e acceda.

Quando il cliente effettua l’accesso, si identifica come Sarah Rose.

![immagine](assets/luma-login.png)

Vengono unite due identità:

* Dati di navigazione anonimi
* I dati esistenti associati all’account di Sarah Rose

Entrambe le identità sono combinate in un unico profilo in [!DNL Experience Platform]. Luma ora ha una visione unificata di questo consumatore.

Sulla base del comportamento di navigazione del visitatore anonimo nella sezione maschile del sito, si potrebbe supporre che il cliente fosse un maschio. Ora che ha effettuato l’accesso, Luma riconosce Sarah Rose. Luma utilizza la potenza del [!DNL Real-Time Customer Profile] per perfezionare i messaggi inviati a lei attraverso i canali.

## Personalizzazione dell’esperienza utente

Sarah viene accolta con un messaggio di fedeltà e ringraziata per essere stata un membro Bronze con maggiori informazioni sui benefici e su come aumentare il suo status e punti.

Passa alla home page per sfogliarne un po’ di più.

![immagine](assets/luma-personal.png)

Sarah riceve un’esperienza di home page personalizzata e viene distribuita in modo dinamico, in base a lei [!DNL Real-Time Customer Profile] in Adobe Experience Platform.

Vede contenuti rilevanti, grazie alla personalizzazione basata su Adobe Sensei in Adobe Target, che tiene conto dei suoi acquisti passati e dell’affinità verso capi di abbigliamento e attrezzature correnti. Luma adatta inoltre il contenuto del catalogo maschile all’attrezzatura da corsa per gli uomini in base alla sua navigazione più recente.

Più in basso nella pagina, Sarah viene mostrata con i prodotti in primo piano, così come una nuova barra di consigli basata sui suoi articoli visualizzati più di recente.

Questo contenuto personalizzato consente a Sarah di trovare rapidamente gli elementi rilevanti. Questo aumenta le conversioni e offre un’esperienza del cliente più piacevole.

### Riportare il cliente indietro

Sarah si distrae e lascia il sito, terminando la sua sessione. Luma può utilizzare i suoi dati in Adobe Experience Platform per aiutarla a riportarla al sito.

Real-time Customer Data Platform, con tecnologia Adobe Experience Platform, è progettato per la gestione della customer experience. Consente alle organizzazioni di:

* Semplificare l&#39;integrazione e l&#39;attivazione dei dati
* Gestire l’utilizzo di dati noti e sconosciuti
* Casi d’uso di marketing più rapidi su larga scala

## Utilizzo di più origini dati

Il team di Luma dispone di tutti i dati comportamentali e dei clienti in un’unica posizione.

![immagine](assets/luma-dash.png)

Possono acquisire dati da tutte le seguenti origini:

* Dati delle soluzioni Adobe Experience Cloud esistenti
* Fonti non basate su Adobi, come il programma fedeltà di Luma, call center e dati di sistema del punto vendita
* Dati in streaming in tempo reale da origini dati Luma
* Dati in tempo reale da soluzioni Adobe (non sono necessari nuovi tag)

Tutti questi dati provenienti da origini diverse vengono uniti in un unico profilo cliente unificato.

## Configurazione di un’origine dati

Utilizzare [!DNL Real-Time Customer Data Platform] per inserire nuove fonti di dati in Platform. Real-Time CDP include un catalogo di origini dati che possono essere aggiunte al profilo in modo rapido e semplice.

![immagine](assets/luma-source-cat.png)

Ad esempio, per acquisire i dati CRM di Luma, filtra il catalogo per *CRM* e tutti i connettori predefiniti contenenti *CRM* sono elencati. Da aggiungere [!DNL Microsoft Dynamics CRM] dati:

1. Autorizza la connessione.

   ![immagine](assets/luma-source-auth.png)

1. Scegli cosa importare da un elenco consigliato di tabelle XDM pre-mappate.

   <!--    ![image](assets/luma-source-import.png) -->

   Ad esempio, seleziona **[!UICONTROL Contatti]**. Viene caricata automaticamente un&#39;anteprima dei dati dei contatti, in modo da poter verificare che l&#39;aspetto sia quello previsto.

   Real-Time CDP consente di eseguire molte operazioni manuali eseguendo la mappatura automatica dei campi standard in [!DNL Experience Data Model] Schema del profilo (XDM).

1. Controlla le mappature dei campi.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Ad esempio, verifica che il campo e-mail per i contatti sia mappato correttamente.\
   Puoi visualizzare in anteprima i dati ed eseguire la mappatura avanzata.

1. Imposta una pianificazione.

   ![immagine](assets/luma-source-sched.png)

È fatta. Hai appena aggiunto [!DNL Microsoft CRM] come origine di dati in [!DNL Experience Platform].

### Etichettatura dei dati acquisiti per i criteri di utilizzo

Luma dispone di molte policy interne che limitano l’utilizzo di alcuni tipi di informazioni raccolte e deve inoltre rispettare i problemi legali e relativi alla privacy relativi all’utilizzo dei dati. Utilizzando la governance dei dati di Adobe Experience Platform, è possibile applicare etichette di utilizzo dei dati predefinite ai set di dati (e a campi specifici all’interno di tali set di dati), consentendo a Luma di categorizzare i propri dati in base a specifiche restrizioni di utilizzo.

![](assets/governance-labels.png)

Una volta applicate le etichette di utilizzo dei dati, Luma può quindi utilizzare la governance dei dati per creare criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni che è consentito eseguire sui dati che contengono determinate etichette. Quando si tenta di eseguire in Real-Time CDP un’azione che costituisce una violazione della policy, l’azione viene impedita e viene visualizzato un avviso per mostrare quale policy è stata violata e perché.

Inoltre, Real-Time CDP

## Riunire i dati per un cliente specifico

In questo scenario, cerca i profili per Sarah Rose. Viene visualizzato il suo profilo, con l’e-mail che utilizzava per accedere.

<!-- ![image](assets/luma-find-profile.png) -->

Tutte le informazioni di profilo di Luma su Sarah vengono visualizzate. Ciò include le sue informazioni personali come l&#39;indirizzo e il numero di telefono, le preferenze di comunicazione e i tipi di pubblico per cui si qualifica.

| Categoria | Descrizione |
|---|---|
| Identità | Mostra le identità collegate tra loro in [!DNL Platform] dalle interazioni di Sarah con Luma su canali e dispositivi. Viene visualizzato il suo ECID dal sito web. La sua identità include anche l’ECID dalla sua app mobile, il suo ID e-mail, un ID del sistema di gestione delle relazioni con i clienti aggiunto di recente [!DNL Microsoft Dynamics] un set di dati e un ID fedeltà trasmessi in Adobe Experience Platform dal sistema fedeltà Luma. |
| Eventi | Mostra tutti i dati di interazione di Sarah con il brand Luma. Questo include l’articolo che ha appena visualizzato, tutto ciò che ha visto in passato, le e-mail che ha ricevuto, le sue interazioni con il call center e su quale canale e dispositivo si sono verificate ognuna di queste interazioni. |

Il profilo Real-Time CDP riduce il flusso di lavoro del team di marketing Luma da settimane a minuti e offre possibilità di personalizzazione basate su questa visualizzazione a 360 gradi per il cliente. Il profilo unisce i dati comportamentali di quando ha navigato sul sito prima di accedere, con il suo profilo cliente esistente, creando una visualizzazione completa di Sarah.

Il team marketing può utilizzare questo [!DNL Real-Time Customer Profile] per personalizzare meglio l’esperienza di Sarah e aumentare la sua brand loyalty con Luma.

## Tipi di pubblico

Le potenti funzionalità di segmentazione di Adobe Experience Platform consentono agli esperti di marketing di combinare attributi, eventi e tipi di pubblico esistenti, in base ai dati acquisiti in [!DNL Real-Time Customer Profile].

<!-- ![image](assets/luma-segments.png) -->

In questo scenario, le recenti interazioni di Sarah sul sito mostrano un comportamento diverso dalle sue azioni passate. Lei di solito compra abbigliamento da donna. Tuttavia, l&#39;oggetto nel suo carrello è una felpa grande da uomo.

Il team di Data Science di Luma ha creato modelli sulla propensione all’acquisto. Un modello identifica un cambiamento improvviso nella categoria di abbigliamento (come uomini/donne) o nelle dimensioni per il consumatore esistente. Il cambiamento nel comportamento d&#39;acquisto di Sarah fa pensare che non stia facendo acquisti per se stessa.

<!-- ![image](assets/luma-gift.png) -->

### Definire un pubblico

Utilizza le varie opzioni dell’editor di espressioni visive o basate su codice nell’area di lavoro tipi di pubblico per modificare o creare un pubblico che rappresenti utenti che abbandonano il carrello e che sembrano in procinto di acquistare un regalo:

```sql
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

Poiché Sarah ha aggiunto un oggetto regalo apparente nel carrello e lo ha abbandonato, Luma può colpirla con un’offerta regalo gratuita.

## Destinazioni

Dopo aver aggiunto il pubblico &quot;Abbandoni del carrello regali&quot;, puoi vedere approssimativamente quante persone fanno parte di questo pubblico. Puoi intervenire e renderla disponibile per la personalizzazione su tutti i canali.

Seleziona **[!UICONTROL Invia a destinazioni]**.

In Real-Time CDP, Luma può agire direttamente sui propri tipi di pubblico a scopo di personalizzazione.\
Qui vediamo tutte le destinazioni disponibili per l’invio di questa destinazione da parte di Luma, sia per le soluzioni Adobi che per quelle non Adobi:

![immagine](assets/luma-dest.png)

### Selezione delle destinazioni

In questo scenario, Luma desidera eseguire il retargeting del pubblico con la personalizzazione tra queste destinazioni:

* Google, per la visualizzazione
  <!--* Facebook -->
* Adobe Campaign, per e-mail

<!-- ![image](assets/luma-sched-dest.png) -->

### Pianificazione delle destinazioni

Puoi anche pianificare l’esportazione del pubblico in modo che inizi o finisca in un determinato momento. Il pubblico verrà pubblicato e aggiornato automaticamente nelle piattaforme configurate alle date pianificate.

>[!NOTE]
>
>Facoltativamente, se selezioni il campo data, questo pianifica automaticamente 90 giorni di uscita.

Seleziona **[!UICONTROL Salva]** per passare alla pagina successiva.

Quando un cliente in questo pubblico effettua un acquisto, la sua iscrizione a questo pubblico viene eliminata in tempo reale. Non si qualificano più perché il loro stato è cambiato.

In questo modo il direttore del team multimediale Luma risparmia centinaia di migliaia di dollari non utilizzando l’inventario per un pubblico non qualificato.

### Applicazione dei criteri di utilizzo dei dati per le destinazioni

Adobe Experience Platform include controlli di privacy e sicurezza per determinare se un pubblico è disponibile per essere attivato su una particolare destinazione. L’attivazione è abilitata o limitata in base agli scopi di marketing assegnati alla destinazione al momento della creazione e ai criteri di utilizzo dei dati definiti dall’organizzazione.

Se l’attività viola i criteri, viene visualizzato un avviso. Questo avviso contiene informazioni sulla derivazione dei dati che possono aiutarti a identificare il motivo della violazione dei criteri e cosa puoi fare per risolvere la violazione.

Con questi controlli, [!DNL Experience Platform] aiuta Luma a rispettare le normative e a commercializzare in modo responsabile. Questi controlli sono flessibili e possono essere modificati per soddisfare i requisiti dei team di sicurezza e governance di Luma, consentendo loro di soddisfare in modo sicuro i requisiti regionali e organizzativi per la gestione di dati noti e sconosciuti dei clienti.

<!--

### Data flow canvas

When you save, a visual data flow canvas shows the segment mapped from the unified profile to the three destinations you selected.

![image](assets/luma-flow.png)

-->

## Unione delle identità tra dispositivi

Sarah naviga in un sito di social media sul suo dispositivo mobile e vede un annuncio Luma. Le ricorda l&#39;oggetto che ha lasciato nel carrello.

Successivamente, apre l’e-mail e visualizza le e-mail retargetizzate. Seleziona un collegamento a Luma da un’e-mail.

Il collegamento porta Sarah alla home page mobile di Luma, dove vede un’esperienza altamente personalizzata basata su Adobe Target.

* È accolta come membro del Bronzo.
* Vede il messaggio &quot;Regalo&quot;.
* Vede anche il messaggio &quot;Free Gift Wrap&quot;, che fa parte dei suoi benefici per l&#39;iscrizione al Bronze.
* È ancora presa di mira nell&#39;immagine protagonista in base alla sua affinità per la corsa.

Compra il maglione, aggiunge un involucro regalo e scrive una nota regalo. Ha anche la possibilità di ricordare questo evento e ottenere un promemoria il prossimo anno per ottenere in questo momento il regalo. Dice di sì, ed è prevista in una campagna e-mail l&#39;anno successivo per ricordarle di comprare un altro regalo.

Grazie alle funzionalità di soppressione del pubblico, Sarah non sarà presa di mira con quel maglione da uomo che va avanti.

## Analisi del profilo

Gli esperti di marketing Luma utilizzano Adobe Experience Platform per esaminare il pubblico dei gift giver nella dashboard di Real-Time CDP. Vedono i risultati di questa iniziativa nel tempo e vedono che sta crescendo. I clienti rispondono alle offerte e spendono di più.

Queste informazioni consentono agli esperti di marketing di intervenire su questo segnale, che è stato alimentato dalla disponibilità di questi dati in CDP e dalla partecipazione al pubblico di clienti come Sarah.

Luma utilizza questi dati CDP per incrementare la fedeltà e la soddisfazione dei clienti.
