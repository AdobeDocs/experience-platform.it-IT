---
title: Best practice di authoring
description: Scopri quali regole e suggerimenti devi seguire quando crei la pagina della documentazione di destinazione, per assicurarti che soddisfi gli standard di qualità della documentazione di Adobe Experience Platform.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: e239de97a26ea2ff36bb74390e249851a13d2e13
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Best practice di authoring

## Panoramica {#overview}

Questa pagina descrive le regole da seguire quando [creazione della documentazione di destinazione](./documentation-instructions.md) per garantire che soddisfi gli standard di qualità della documentazione di Adobe Experience Platform.

## Indicazioni generali {#general-guidance}

* Quando si riempie il [template](./self-service-template.md) per la documentazione sulla destinazione, consulta la guida per i collaboratori di Adobe per informazioni [collegamento](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en), [tabelle](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#tables), [sintassi markdown supportata](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en), [guida alla scrittura](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en)e altro ancora.
* Non includere osservazioni e stime nella documentazione del prodotto.
* Nella documentazione di Experience Platform, gli autori di Adobe utilizzano **formattazione grassetto** per fare riferimento ai controlli dell’interfaccia utente, come riportato di seguito:
   * Vai a **[!UICONTROL Connessioni]** > **[!UICONTROL Destinazioni]**, quindi seleziona la **[!UICONTROL Catalogo]** scheda . Visualizzare un esempio di come i controlli dell’interfaccia utente sono documentati in un [esercitazione sulle destinazioni](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#select-destination).

## Stile di scrittura

>[!IMPORTANT]
>
>Leggi [Indicazioni sulla scrittura per la documentazione di Adobe](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=en) prima di iniziare a creare la pagina della documentazione di destinazione.

* Mantieni le tue frasi brevi e arrivi al punto velocemente. Se la tua frase è lunga più di 20 parole o usa più virgole, considera la possibilità di suddividerla in frasi separate. Le frasi con più di 20 parole di lunghezza possono essere particolarmente impegnative per i lettori.
* Non essere eccessivamente educata. Evita di usare &quot;per favore&quot; o &quot;gentilmente fai ...&quot; nella documentazione tecnica.

## Collegamento {#linking}

Segui il modello di documentazione fornito e non modificare i collegamenti esistenti nel modello. Quando includi nuovi collegamenti, leggi [utilizzo dei collegamenti nella documentazione](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=en) nella guida per i collaboratori.

## Linee guida sul branding {#branding}

* AEP non è un termine approvato rivolto al pubblico. Utilizza Adobe Experience Platform al primo utilizzo, quindi Experience Platform, quindi Platform.
   * **Non utilizzare**: Prima di poter esportare i dati da AEP a YourDestination, assicurati di leggere e completare questi prerequisiti.
   * **Utilizzo**: Prima di esportare i dati da Adobe Experience Platform a YourDestination, verifica di aver letto e completato questi prerequisiti.

## Immagini e schermate {#images-and-screenshots}

* Per informazioni su [come collegare alle immagini](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=en#images), consulta la guida per i collaboratori .
* Quando utilizzi le schermate, accertati che la schermata acquisisca l’intera schermata dell’interfaccia utente di Platform.
* Quando contrassegni le immagini per evidenziare un determinato controllo o etichetta sulla pagina, prova a seguire lo stile di markup utilizzato dal team di documentazione di Experience Platform. Osserva come viene evidenziato in Basato su profilo [questa schermata](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency).
* Utilizzare `png` formattare le immagini.
* Non utilizzare schermate numerate come nomi di file. I nomi dei file immagine devono essere descrittivi.
   * **Non utilizzare**: `1.png`, `2.png`, `3.png`
   * **Utilizzare**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Utilizza il testo alt per tutte le immagini aggiunte alla documentazione e utilizza la grammatica appropriata nel testo alt.
   * **Non utilizzare**: Dettagli di connessione di destinazione
   * **Utilizzo**: Immagine dell’interfaccia utente di Platform, che mostra i dettagli della connessione di destinazione compilati.

## Processo {#process}

* La [modello di documentazione](./self-service-template.md) viene aggiornato di rado in base al feedback del partner. Prima di iniziare a creare la documentazione per la destinazione, assicurati di aver scaricato il [versione più recente del modello](../assets/docs-framework/yourdestination-template.zip).
* Crea la documentazione e crea la richiesta di pull della documentazione (PR) da un ramo del tuo fork *diversa dalla filiale principale*. Consulta la sezione invia destinazione per la revisione durante l’authoring in [Interfaccia GitHub](./use-github-interface-to-create-documentation.md#submit-review) o [ambiente locale](./work-in-local-environment.md#submit-review).
