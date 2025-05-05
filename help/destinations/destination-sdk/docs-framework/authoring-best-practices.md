---
title: Best practice di authoring
description: Scopri le regole e i suggerimenti da seguire per creare la pagina della documentazione di destinazione in modo che soddisfi gli standard di qualità della documentazione di Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Best practice di authoring

## Panoramica {#overview}

Questa pagina descrive le regole da seguire per [creare la documentazione di destinazione](./documentation-instructions.md) per assicurarsi che soddisfi gli standard di qualità della documentazione di Adobe Experience Platform.

## Indicazioni generali {#general-guidance}

* Durante la compilazione del [modello](./self-service-template.md) per la documentazione di destinazione, consulta la guida per i collaboratori di Adobe per informazioni su [collegamenti](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=it), [tabelle](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=it#tables), [sintassi markdown supportata](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=it), [istruzioni per la scrittura](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=it) e altro ancora.
* Non includere osservazioni e stime nella documentazione del prodotto.
* Nella documentazione di Experience Platform, gli autori di Adobe utilizzano **la formattazione in grassetto** per fare riferimento ai controlli dell&#39;interfaccia utente, come riportato di seguito:
   * Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]** e seleziona la scheda **[!UICONTROL Catalogo]**. Visualizza un esempio di come i controlli dell&#39;interfaccia utente sono documentati in un [tutorial sulle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=it#select-destination).

## Stile di scrittura

>[!IMPORTANT]
>
>Leggi [Indicazioni sulla scrittura per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=it) prima di iniziare a creare la pagina della documentazione di destinazione.

* Mantieni le tue frasi brevi e arriva rapidamente al punto. Se la tua frase è lunga più di 20 parole o utilizza più virgole, prendi in considerazione di suddividerla in frasi separate. Frasi di lunghezza superiore a 20 parole possono essere particolarmente difficili per i lettori.
* Non siate eccessivamente educate. Evita di utilizzare &quot;per favore&quot; o &quot;gentilmente fare ...&quot; nella documentazione tecnica.

## Collegamento {#linking}

Segui il modello di documentazione fornito e non modificare i collegamenti esistenti nel modello. Quando si includono nuovi collegamenti, leggere [Utilizzo dei collegamenti nella documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=it) nella guida per i collaboratori.

## Linee guida per il branding {#branding}

* AEP non è un termine pubblico approvato. Utilizza Adobe Experience Platform al primo utilizzo, quindi Experience Platform e infine Experience Platform.
   * **Non utilizzare**: prima di esportare i dati da AEP a YourDestination, assicurati di aver letto e completato questi prerequisiti.
   * **Utilizza**: prima di esportare dati da Adobe Experience Platform a YourDestination, assicurati di aver letto e completato questi prerequisiti.

## Immagini e schermate {#images-and-screenshots}

* Per informazioni su [come collegarsi alle immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=it#images), fare riferimento alla Guida per i collaboratori.
* Quando utilizzi le schermate, accertati che queste acquisiscano l’intera schermata dell’interfaccia utente di Experience Platform.
* Quando si marcano le immagini per evidenziare un determinato controllo o etichetta nella pagina, provare a seguire lo stile di markup utilizzato dal team di documentazione di Experience Platform. Osserva come la schermata basata sul profilo è evidenziata in [questa schermata](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Utilizzare immagini in formato `png`.
* Non utilizzare le schermate numerate come nomi di file. I nomi dei file immagine devono essere descrittivi.
   * **Non utilizzare**: `1.png`, `2.png`, `3.png`
   * **Usa**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Utilizza il testo alternativo per tutte le immagini aggiunte alla documentazione e utilizza la grammatica corretta nel testo alternativo.
   * **Non utilizzare**: dettagli della connessione di destinazione
   * **Usa**: immagine dell&#39;interfaccia utente di Experience Platform che mostra i dettagli della connessione di destinazione compilati.

## Processo {#process}

* Il [modello di documentazione](./self-service-template.md) viene aggiornato raramente, in base al feedback del partner. Prima di iniziare a creare la documentazione per la destinazione, assicurati di aver scaricato la [versione più recente del modello](../assets/docs-framework/yourdestination-template.zip).
* Crea la documentazione e crea la richiesta di pull della documentazione (PR) da un ramo nel fork *diverso dal ramo principale*. Consulta la sezione relativa alla destinazione di invio per la revisione durante la creazione nell&#39;interfaccia [GitHub](./use-github-interface-to-create-documentation.md#submit-review) o nell&#39;ambiente [locale](./work-in-local-environment.md#submit-review).
