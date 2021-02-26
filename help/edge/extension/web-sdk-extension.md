---
title: Estensione di Adobe Experience Platform Web SDK Panoramica
description: Ulteriori informazioni sull'estensione Adobe Experience Platform Web SDK per  Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 18e511337eaa8b6eb7785b1ee5f1ce2366ddd7c7
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 24%

---


# Panoramica dell’estensione Adobe Experience Platform Web SDK

L’estensione Adobe Experience Platform Web SDK invia dati ad Adobe Experience Cloud da proprietà Web tramite Adobe Experience Platform Edge Network. L&#39;estensione consente di trasmettere dati in streaming alla piattaforma, sincronizzare identità, elaborare i segnali di consenso dei clienti e raccogliere automaticamente i dati contestuali.

In questo documento viene illustrato come configurare l’estensione nell’interfaccia utente  Adobe Experience Platform Launch.

## Configura l&#39;estensione

Se l&#39;estensione SDK Web della piattaforma è già stata installata per una proprietà, aprite la proprietà nell&#39;interfaccia utente del Platform launch e selezionate la scheda **[!UICONTROL Extensions]**. In Platform Web SDK, selezionate **[!UICONTROL Configure]**.

![](../images/extension/overview/configure.png)

Se non avete ancora installato l&#39;estensione, selezionate la scheda **[!UICONTROL Catalog]**. Nell&#39;elenco delle estensioni disponibili, individua l&#39;estensione SDK Web della piattaforma e seleziona **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

In entrambi i casi, arrivate alla pagina di configurazione per l’SDK Web della piattaforma. Le sezioni seguenti illustrano le opzioni di configurazione dell&#39;estensione.

![](../images/extension/overview/config-screen.png)

## Opzioni di configurazione generali

Le opzioni di configurazione nella parte superiore della pagina indicano ad Adobe Experience Platform dove indirizzare i dati e quali configurazioni utilizzare sul server.

### [!UICONTROL Name]

L’estensione Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Viene utilizzato per inviare dati a più organizzazioni con una singola configurazione di Platform Launch.

Per impostazione predefinita, il nome dell&#39;estensione è &quot;[!DNL alloy]&quot;. Tuttavia, è possibile modificare il nome dell&#39;istanza e inserire un nome oggetto JavaScript valido.

### **[!UICONTROL IMS Organization ID]**

L&#39;[!UICONTROL IMS Organization ID] è l&#39;organizzazione a cui si desidera inviare i dati in Adobe. Nella maggior parte dei casi, si consiglia di utilizzare il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, compilare il campo con il valore della seconda organizzazione a cui si desidera inviare i dati.

### **[!UICONTROL Edge Domain]**

[!UICONTROL Edge Domain] è il dominio da cui l’estensione Adobe Experience Platform invia e riceve i dati. L&#39;estensione richiede l&#39;utilizzo di un first party CNAME per il traffico di produzione. Il dominio predefinito di terze parti funziona per gli ambienti di sviluppo ma non è adatto per gli ambienti di produzione. Le istruzioni su come impostare un first party CNAME sono disponibili [qui](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Edge Configurations]

Quando una richiesta viene inviata ad Adobe Experience Platform Edge Network, viene utilizzato un ID di configurazione periferico per fare riferimento alla configurazione lato server. Questo consente di aggiornare la configurazione senza dover apportare modifiche al codice sul sito Web.

Per ulteriori informazioni, vedere la guida sulle [configurazioni dei bordi](../fundamentals/edge-configuration.md).

## [!UICONTROL Privacy]

La sezione [!UICONTROL Privacy] consente di configurare il modo in cui l&#39;SDK gestisce i segnali di consenso dei clienti dal sito Web. Nello specifico, consente di selezionare il livello predefinito di consenso che si presume di un cliente se non è stata fornita alcuna altra preferenza esplicita per il consenso. La tabella seguente riassume il contenuto di ogni opzione:

| [!UICONTROL Default Consent Level] | Descrizione |
| --- | --- |
| [!UICONTROL In] | Consenso. Utilizzate questa opzione se per impostazione predefinita si assume il consenso del cliente e si rispettano solo i segnali di rinuncia. |
| [!UICONTROL Pending] | Si presume che i clienti con il consenso &quot;in sospeso&quot; siano esclusi fino all&#39;invio di un segnale di consenso. Utilizzate questa opzione se richiedete un consenso esplicito da parte del cliente per le operazioni aziendali. |
| [!UICONTROL Provided by data element] | Il livello di consenso predefinito è determinato da un elemento dati separato definito dall&#39;utente. Quando si utilizza questa opzione, è necessario specificare l&#39;elemento dati utilizzando il menu a discesa fornito. |