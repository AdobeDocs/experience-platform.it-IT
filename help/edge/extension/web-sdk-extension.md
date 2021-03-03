---
title: Estensione di Adobe Experience Platform Web SDK Panoramica
description: Scopri l’estensione Adobe Experience Platform Web SDK per Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 19%

---


# Panoramica dell’estensione dell’SDK per web di Adobe Experience Platform

L’estensione Adobe Experience Platform Web SDK invia i dati ad Adobe Experience Cloud dalle proprietà web tramite Adobe Experience Platform Edge Network. L’estensione ti consente di inviare dati in streaming a Platform, sincronizzare le identità, elaborare i segnali di consenso dei clienti e raccogliere automaticamente i dati contestuali.

Questo documento illustra come configurare l’estensione nell’interfaccia utente di Adobe Experience Platform Launch.

## Configura l&#39;estensione

Se l’estensione Platform Web SDK è già stata installata per una proprietà, apri la proprietà nell’interfaccia utente di Platform Launch e seleziona la scheda **[!UICONTROL Extensions]** . In Platform Web SDK, seleziona **[!UICONTROL Configure]**.

![](../images/extension/overview/configure.png)

Se non hai ancora installato l&#39;estensione, seleziona la scheda **[!UICONTROL Catalog]** . Dall’elenco delle estensioni disponibili, trova l’estensione Platform Web SDK e seleziona **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

In entrambi i casi, arrivi alla pagina di configurazione dell’SDK per web di Platform. Le sezioni seguenti illustrano le opzioni di configurazione dell&#39;estensione.

![](../images/extension/overview/config-screen.png)

## Opzioni di configurazione generali

Le opzioni di configurazione nella parte superiore della pagina indicano ad Adobe Experience Platform dove indirizzare i dati e quali configurazioni utilizzare sul server.

### [!UICONTROL Name]

L’estensione Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Il nome viene utilizzato per inviare dati a più organizzazioni con una singola configurazione di Platform Launch.

Il nome dell&#39;estensione viene impostato automaticamente su &quot;[!DNL alloy]&quot;. Tuttavia, è possibile modificare il nome dell&#39;istanza e inserire un nome oggetto JavaScript valido.

### **[!UICONTROL IMS Organization ID]**

L&#39;[!UICONTROL IMS Organization ID] è l&#39;organizzazione a cui si desidera inviare i dati in Adobe. Nella maggior parte dei casi, utilizza il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, compila questo campo con il valore della seconda organizzazione a cui desideri inviare i dati.

### **[!UICONTROL Edge Domain]**

[!UICONTROL Edge Domain] è il dominio da cui l’estensione Adobe Experience Platform invia e riceve i dati. L&#39;estensione richiede l&#39;utilizzo di un first party CNAME per il traffico di produzione. Il dominio predefinito di terze parti funziona per gli ambienti di sviluppo ma non è adatto per gli ambienti di produzione. Le istruzioni su come impostare un first party CNAME sono disponibili [qui](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Edge Configurations]

Quando viene inviata una richiesta ad Adobe Experience Platform Edge Network, viene utilizzato un ID di configurazione perimetrale per fare riferimento alla configurazione lato server. Puoi aggiornare la configurazione senza dover apportare modifiche al codice sul sito web.

Per ulteriori informazioni, consulta la guida sulle [configurazioni edge](../fundamentals/edge-configuration.md) .

## [!UICONTROL Privacy]

La sezione [!UICONTROL Privacy] ti consente di configurare in che modo l’SDK gestisce i segnali di consenso dei clienti provenienti dal tuo sito web. Nello specifico, ti consente di selezionare il livello di consenso predefinito che si presume di un cliente se non è stata fornita alcuna altra preferenza di consenso esplicito. La tabella seguente suddivide ciò che ogni opzione comporta:

| [!UICONTROL Default Consent Level] | Descrizione |
| --- | --- |
| [!UICONTROL In] | Opt-in. Utilizza questa opzione se supponi il consenso del cliente per impostazione predefinita e rispetta solo i segnali di rinuncia. |
| [!UICONTROL Pending] | I clienti con consenso &quot;in sospeso&quot; vengono esclusi finché non viene inviato un segnale di consenso. Utilizza questa opzione se richiedi il consenso esplicito del cliente per le operazioni aziendali. |
| [!UICONTROL Provided by data element] | Il livello di consenso predefinito è determinato da un elemento dati separato definito dall’utente. Quando utilizzi questa opzione, devi specificare l’elemento dati utilizzando il menu a discesa fornito. |