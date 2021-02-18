---
title: Estensione di Adobe Experience Platform Web SDK Panoramica
description: Ulteriori informazioni sull'estensione Adobe Experience Platform Web SDK per  Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 88%

---


# Panoramica dell’estensione Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK Extension invia i dati all’Adobe Experience Cloud dalle proprietà Web tramite Adobe Experience Platform Edge Network. L&#39;estensione Adobe Experience Platform Web SDK consente lo streaming dei dati nella piattaforma, la sincronizzazione delle identità, il consenso e la raccolta automatica dei dati contestuali.

## Configurare l&#39;estensione AEP Web SDK

Questa sezione fornisce un riferimento per le opzioni disponibili durante la configurazione dell&#39;estensione Adobe Experience Platform Web SDK.

Se l&#39;estensione Adobe Experience Platform Web SDK non è ancora stata installata, apri la proprietà, quindi seleziona **[!UICONTROL Extensions > Catalog]**, passa il mouse sull&#39;estensione Adobe Experience Platform Web SDK e fai clic su **[!UICONTROL Install]**.

Per configurare l&#39;estensione, apri la scheda **[!UICONTROL Extensions]**, passa il puntatore del mouse sull&#39;estensione e fai clic su **[!UICONTROL Configure]**.

![](./assets/ext-aep-config.png)

### Nome istanza

L’estensione Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Viene utilizzato per inviare dati a più organizzazioni con una singola configurazione di Adobe Experience Platform Launch. Il **[!UICONTROL Name]** predefinito è alloy. Tuttavia, è possibile modificare il nome dell&#39;istanza e inserire un nome oggetto JavaScript valido. L&#39;estensione Adobe Experience Platform richiede che ogni istanza abbia un **[!UICONTROL Config ID]** e un **[!UICONTROL Organization ID]** diversi.

## **[!UICONTROL Config ID]**

L&#39;**[!UICONTROL Config ID]** è ciò che indica ad Adobe Experience Platform dove i dati dovrebbero essere instradati e quali configurazioni dovrebbero essere utilizzate sul server. Questa impostazione è necessaria per il funzionamento dell&#39;estensione Adobe Experience Platform. Puoi ottenere un ID di configurazione contattando l&#39;assistenza clienti.


### **[!UICONTROL Organization ID]**

L&#39;**[!UICONTROL Organization ID]** è l&#39;organizzazione a cui si desidera inviare i dati in Adobe. Nella maggior parte dei casi, si consiglia di utilizzare il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, è necessario compilare il modulo con il valore della seconda organizzazione a cui si desidera inviare i dati.

### **[!UICONTROL Edge Domain]**

**[!UICONTROL Edge Domain]** è il dominio da cui l’estensione Adobe Experience Platform invia e riceve i dati. L&#39;estensione richiede l&#39;utilizzo di un first party CNAME per il traffico di produzione. Il dominio predefinito di terze parti funziona per gli ambienti di sviluppo ma non è adatto per gli ambienti di produzione. Le istruzioni su come impostare un first party CNAME sono disponibili [qui](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html).

### **[!UICONTROL Enable Errors]**

Per impostazione predefinita, se si verifica un errore con l&#39;estensione, l&#39;errore viene registrato nella console. Se desideri nascondere gli errori in un ambiente di produzione, puoi deselezionare la casella **[!UICONTROL Enable Errors]**. Gli errori vengono comunque stampati quando il debug viene attivato in Platform Launch.

### **[!UICONTROL Enable Opt-in]**

Se **[!UICONTROL Enable Opt-in]** è abilitata, l&#39;estensione AEP Web SDK può contenere riscontri fino alla ricezione del consenso. L&#39;estensione presenta un&#39;azione per impostare le preferenze di consenso.

### **[!UICONTROL Enable Migrate ECID]**

L&#39;estensione AEP Web SDK utilizza un nuovo cookie per memorizzare l&#39;ECID. Questa impostazione rende compatibili il nuovo cookie e il vecchio cookie a scopo di migrazione. Adobe consiglia vivamente di attivarlo, a meno che non siano presenti visitatori con un ECID.

### **[!UICONTROL Use 3rd Party Cookies]**

Adobe Experience Platform memorizzerà sempre un cookie nel dominio di prime parti. Questa opzione consente di utilizzare un cookie di terze parti impostato su demdex.net in aggiunta al cookie del dominio di prime parti. Questa funzione può essere utile quando gli utenti si spostano tra più domini. In questo modo verranno disattivate le chiamate a demdex.net.

### **[!UICONTROL Context]**

L&#39;estensione raccoglie automaticamente informazioni sul contesto della richiesta (ad esempio, dettagli sull&#39;URL e sul browser). Per disattivarlo, deselezionare contesti specifici.

- **[!UICONTROL web]** - Dettagli sulla pagina Web come url, referrer, ecc.
- **[!UICONTROL device]** - Dettagli sul dispositivo quali l&#39;orientamento dello schermo, l&#39;altezza dello schermo e la larghezza dello schermo.
- **[!UICONTROL environment]** - Informazioni sull&#39;ambiente informatico (browser, connessione, ecc.)
- **[!UICONTROL location]** - Informazioni limitate sulla posizione dell&#39;utente

## Ulteriori informazioni

1. Impostare [tipi di azione](action-types.md).
2. Impostare i tipi di elementi di dati [](data-element-types.md).
