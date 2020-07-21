---
title: Esercitazione Implementare i tag del sito Web con Adobe Launch
seo-title: Implementare i tag dei siti Web con Adobe Launch
description: Utilizzo di Adobe Launch per implementare i tag del sito Web in  Adobe Experience Platform
seo-description: Utilizzo di Adobe Launch per implementare i tag del sito Web in  Adobe Experience Platform
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 7%

---


# Esercitazione: Implementare i tag dei siti Web con Adobe Launch

Questa esercitazione spiega come implementare i tag del sito Web per inviare dati al Adobe Experience Platform  tramite Adobe Launch.

## Prerequisiti

* Lo schema e il dataset necessari vengono creati in [!DNL Platform].
* La configurazione necessaria è stata implementata in [!DNL Experience Edge] e ha l&#39;ID di configurazione e il [!DNL Edge] dominio corrispondenti.
* La società CMS è già stata configurata per fornire un oggetto JavaScript su ciascuna pagina con i dati a cui è necessario inviare [!DNL Platform].

## Passaggi

Questa esercitazione contiene i passaggi seguenti:

1. Installate l’ [!DNL Web SDK] estensione  Adobe Experience Platform.
1. Crea una regola per indicare [!DNL Launch] quali dati inviare.
1. Create un bundle dell&#39;estensione e della regola in una libreria.

## Installare l&#39;estensione  Adobe Experience Platform [!DNL Web SDK]

Innanzitutto, installate l&#39; [!DNL Web SDK] estensione  Adobe Experience Platform.

1. In [!DNL Launch], open the **[!UICONTROL Extensions]** tab.

   ![immagine](assets/launch-overview.png)

1. Selezionate l’estensione SDK Web  Adobe Experience Platform dall’ [!DNL Launch] estensione [!DNL Catalog]Viene visualizzata la schermata di configurazione.

   ![immagine](assets/launch-extension-install.png)

   Per ulteriori informazioni, consulta [Estensioni](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) nella [!DNL Launch] documentazione.

1. Configura l&#39;estensione.

   Le uniche impostazioni necessarie al momento sono:

   * **ID configurazione:** Specificate l&#39;ID di configurazione ricevuto dal rappresentante Adobe.
   * **Dominio Edge:** Specificate il dominio periferico ricevuto dal rappresentante Adobe.

1. Fate clic **[!UICONTROL Save]** e continuate con il passaggio successivo.

## Crea una regola per indicare [!DNL Launch] quali dati inviare

Quindi, create una regola per comunicare [!DNL Launch] quali dati inviare al Adobe Experience Platform  e quando inviarlo.

1. Sotto la **[!UICONTROL Rules]** scheda, configurate un evento che verrà attivato su ogni nuova pagina del sito Web al caricamento della [!DNL Launch] libreria.

   ![immagine](assets/launch-make-a-rule.png)

1. Aggiungi un&#39;azione.

   Per configurare l’azione, indicate [!DNL Launch] dove trovare il livello dati. Il livello dati è un oggetto JavaScript esistente sulla pagina, che viene distribuito dallo stesso CMS che esegue il rendering della pagina Web. Fornire il percorso JavaScript all&#39;oggetto dati.

   ![immagine](assets/launch-add-aep-action.png)

   L&#39;oggetto dati inviato deve essere un XDM valido che trasmette la convalida rispetto allo schema utilizzato dal set di dati connesso all&#39;ID di configurazione.

1. Fai clic su **[!UICONTROL Keep Changes]**.

Per ulteriori informazioni, consulta [Regole](https://docs.adobe.com/content/help/it-IT/launch/using/reference/manage-resources/rules.html) nella [!DNL Launch] documentazione.

## Eseguire il bundle dell&#39;estensione e della regola in una libreria

Quindi, [raggruppate l&#39;estensione](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) e la nuova regola in una libreria e verificate le modifiche in un ambiente di sviluppo.

![immagine](assets/launch-add-changes-to-library.png)

Dopo aver completato il test, promuovi la libreria attraverso il flusso di lavoro in modo che possa essere distribuita sul sito Produzione. I dati ora scorrono da ogni singolo utente a  Adobe Experience Platform.

![immagine](assets/launch-promote-library.png)

Per ulteriori informazioni, consulta [Librerie](https://docs.adobe.com/content/help/it-IT/launch/using/reference/publish/libraries.html) nella [!DNL Launch] documentazione.