---
title: Estensione di Adobe Experience Platform Web SDK Panoramica
description: Scopri l’estensione Adobe Experience Platform Web SDK per Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 18%

---


# Panoramica dell&#39;estensione Adobe Experience Platform Web SDK

L’estensione Adobe Experience Platform Web SDK invia i dati a Adobe Experience Cloud dalle proprietà web tramite Adobe Experience Platform Edge Network. L’estensione ti consente di inviare dati in streaming a Platform, sincronizzare le identità, elaborare i segnali di consenso dei clienti e raccogliere automaticamente i dati contestuali.

Questo documento illustra come configurare l&#39;estensione nell&#39;interfaccia utente di Adobe Experience Platform Launch.

## Configura l&#39;estensione

Se l’estensione Platform Web SDK è già stata installata per una proprietà, apri la proprietà nell’interfaccia utente del Platform launch e seleziona la scheda **[!UICONTROL Extensions]** . In Platform Web SDK, seleziona **[!UICONTROL Configure]**.

![](../images/extension/overview/configure.png)

Se non hai ancora installato l&#39;estensione, seleziona la scheda **[!UICONTROL Catalog]** . Dall’elenco delle estensioni disponibili, trova l’estensione Platform Web SDK e seleziona **[!UICONTROL Install]**.

![](../images/extension/overview/install.png)

In entrambi i casi, arrivi alla pagina di configurazione dell’SDK per web di Platform. Le sezioni seguenti illustrano le opzioni di configurazione dell&#39;estensione.

![](../images/extension/overview/config-screen.png)

## Opzioni di configurazione generali

Le opzioni di configurazione nella parte superiore della pagina indicano a Adobe Experience Platform dove indirizzare i dati e quali configurazioni utilizzare sul server.

### [!UICONTROL Name]

L&#39;estensione Adobe Experience Platform Web SDK supporta più istanze sulla pagina. Il nome viene utilizzato per inviare dati a più organizzazioni con una singola configurazione di Platform launch.

Il nome dell&#39;estensione viene impostato automaticamente su &quot;[!DNL alloy]&quot;. Tuttavia, è possibile modificare il nome dell&#39;istanza e inserire un nome oggetto JavaScript valido.

### **[!UICONTROL IMS Organization ID]**

L&#39;[!UICONTROL IMS Organization ID] è l&#39;organizzazione a cui si desidera inviare i dati in Adobe. Nella maggior parte dei casi, utilizza il valore predefinito compilato automaticamente. Se sulla pagina sono presenti più istanze, compila questo campo con il valore della seconda organizzazione a cui desideri inviare i dati.

### **[!UICONTROL Edge Domain]**

[!UICONTROL Edge Domain] è il dominio da cui l’estensione Adobe Experience Platform invia e riceve i dati. L&#39;estensione richiede l&#39;utilizzo di un first party CNAME per il traffico di produzione. Il dominio predefinito di terze parti funziona per gli ambienti di sviluppo ma non è adatto per gli ambienti di produzione. Le istruzioni su come impostare un first party CNAME sono disponibili [qui](https://docs.adobe.com/content/help/it-IT/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Edge Configurations]

Quando una richiesta viene inviata ad Adobe Experience Platform Edge Network, viene utilizzato un ID di configurazione perimetrale per fare riferimento alla configurazione lato server. Puoi aggiornare la configurazione senza dover apportare modifiche al codice sul sito web.

Per ulteriori informazioni, consulta la guida sulle [configurazioni edge](../fundamentals/edge-configuration.md) .

## [!UICONTROL Privacy]

La sezione [!UICONTROL Privacy] ti consente di configurare in che modo l’SDK gestisce i segnali di consenso degli utenti provenienti dal tuo sito web. Nello specifico, ti consente di selezionare il livello di consenso predefinito che si presume di un utente se non è stata fornita alcuna altra preferenza di consenso esplicito. Il livello di consenso predefinito non viene salvato nel profilo dell’utente. La tabella seguente suddivide ciò che ogni opzione comporta:

| [!UICONTROL Default Consent Level] | Descrizione |
| --- | --- |
| [!UICONTROL In] | Raccogliere eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL Out] | Elimina gli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. |
| [!UICONTROL Pending] | Eseguire la coda degli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. Quando vengono fornite le preferenze di consenso, gli eventi vengono raccolti o scartati a seconda delle preferenze fornite. |
| [!UICONTROL Provided by data element] | Il livello di consenso predefinito è determinato da un elemento dati separato definito dall’utente. Quando utilizzi questa opzione, devi specificare l’elemento dati utilizzando il menu a discesa fornito. |

Utilizzare Out o Pending se si richiede un consenso esplicito dell’utente per le operazioni aziendali.