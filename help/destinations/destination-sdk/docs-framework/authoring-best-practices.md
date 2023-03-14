---
title: Best practice di authoring
description: Scopri le regole e i suggerimenti da seguire per creare la pagina della documentazione di destinazione in modo che soddisfi gli standard di qualità della documentazione di Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: 0b9b724c2530e43ce681011d12fc1341148ddbf5
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Best practice di authoring

## Panoramica {#overview}

Questa pagina descrive le regole da seguire quando [authoring della documentazione di destinazione](./documentation-instructions.md) per garantire che soddisfi gli standard di qualità della documentazione Adobe Experience Platform.

## Indicazioni generali {#general-guidance}

* Durante la compilazione del [modello](./self-service-template.md) per informazioni sulla documentazione di destinazione, consulta l’Adobe guida per i collaboratori [collegamento](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tabelle](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), il [sintassi markdown supportata](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [istruzioni per la scrittura](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en), e altro ancora.
* Non includere osservazioni e stime nella documentazione del prodotto.
* Nella documentazione di Experience Platform, gli autori di Adobi utilizzano **grassetto** per fare riferimento ai controlli dell’interfaccia utente, come segue:
   * Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]**, e seleziona la **[!UICONTROL Catalogo]** scheda. Visualizza un esempio della documentazione dei controlli dell’interfaccia utente in una [tutorial sulle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Stile scrittura

>[!IMPORTANT]
>
>Letto [Indicazioni sulla scrittura per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) prima di iniziare a creare la pagina della documentazione di destinazione.

* Mantieni le tue frasi brevi e arriva rapidamente al punto. Se la tua frase è lunga più di 20 parole o utilizza più virgole, prendi in considerazione di suddividerla in frasi separate. Frasi di lunghezza superiore a 20 parole possono essere particolarmente difficili per i lettori.
* Non siate eccessivamente educate. Evita di utilizzare &quot;per favore&quot; o &quot;gentilmente fare ...&quot; nella documentazione tecnica.

## Collegamento {#linking}

Segui il modello di documentazione fornito e non modificare i collegamenti esistenti nel modello. Quando includi nuovi collegamenti, leggi [utilizzo dei collegamenti nella documentazione di](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) nella guida per i collaboratori.

## Linee guida per il branding {#branding}

* AEP non è un termine approvato rivolto al pubblico. Utilizza Adobe Experience Platform al primo utilizzo, quindi Experience Platform e infine Platform.
   * **Non utilizzare**: prima di poter esportare dati da AEP a YourDestination, assicurati di aver letto e completato questi prerequisiti.
   * **Utilizzare**: prima di esportare i dati da Adobe Experience Platform a YourDestination, assicurati di aver letto e completato questi prerequisiti.

## Immagini e schermate {#images-and-screenshots}

* Per informazioni su [come collegare immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), consulta la guida per i collaboratori.
* Quando utilizzi le schermate, accertati che queste acquisiscano l’intera schermata dell’interfaccia utente di Platform.
* Quando si marcano le immagini per evidenziare un determinato controllo o etichetta nella pagina, provare a seguire lo stile di markup utilizzato dal team di documentazione di Experience Platform. Nota come le opzioni basate sul profilo sono evidenziate in [questa schermata](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Utilizza `png` formattare le immagini.
* Non utilizzare le schermate numerate come nomi di file. I nomi dei file immagine devono essere descrittivi.
   * **Non utilizzare**: `1.png`, `2.png`, `3.png`
   * **Utilizzare**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Utilizza il testo alternativo per tutte le immagini aggiunte alla documentazione e utilizza la grammatica corretta nel testo alternativo.
   * **Non utilizzare**: dettagli della connessione di destinazione
   * **Utilizzare**: immagine dell’interfaccia utente di Platform che mostra i dettagli della connessione di destinazione compilati.

## Processo {#process}

* Il [modello di documentazione](./self-service-template.md) viene aggiornato raramente, in base al feedback ricevuto dai partner. Prima di iniziare a creare la documentazione per la destinazione, assicurati di aver scaricato [versione più recente del modello](/help/destinations/destination-sdk/docs-framework/assets/yourdestination-template.zip).
* Crea la documentazione e la richiesta di pull della documentazione (PR) da un ramo nel fork *diverse dalla filiale principale*. Consulta la sezione relativa alla destinazione di invio per la revisione durante la creazione di in [Interfaccia GitHub](./use-github-interface-to-create-documentation.md#submit-review) o in [ambiente locale](./work-in-local-environment.md#submit-review).
