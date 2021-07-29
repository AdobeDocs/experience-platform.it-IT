---
title: Guida introduttiva all’inoltro eventi
description: Segui questa esercitazione passo per iniziare a utilizzare l’inoltro eventi in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 46%

---

# Guida introduttiva all&#39;inoltro eventi

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Per utilizzare l’inoltro eventi in Adobe Experience Platform, i dati devono essere inviati a Adobe Experience Platform Edge Network utilizzando una o più delle tre opzioni seguenti:

* [Adobe Experience Platform Web SDK](../../extensions/web/sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [API server-to-server](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>L’SDK per web di Platform e l’SDK per dispositivi mobili di Platform non richiedono la distribuzione tramite tag in Adobe Experience Platform. Tuttavia, l&#39;utilizzo di tag per distribuire questi SDK è l&#39;approccio consigliato.

Dopo aver inviato i dati a Edge Network, è possibile attivare le soluzioni Adobe a cui inviare i dati. Per inviare dati a una soluzione non Adobe, impostala nell’inoltro degli eventi.

## Prerequisiti 

* Adobe Experience Platform Collection Enterprise (contatta il tuo account manager per informazioni sui prezzi)
* Inoltro di eventi in Adobe Experience Platform
* Adobe Experience Platform Web SDK o Mobile SDK, configurato per inviare i dati a Edge Network
* Mappa i dati su Experience Data Model (XDM) (Questa mappatura può essere effettuata utilizzando i tag)

## Creare uno schema XDM

Crea lo schema in Adobe Experience Platform.

1. Crea uno schema selezionando **[!UICONTROL Schemi]** > **[!UICONTROL Crea schemi]** e scegliendo l’opzione **[!UICONTROL XDM ExperienceEvent]**.

1. Assegna allo schema un nome e una breve descrizione.

1. Puoi aggiungere il gruppo di campi &quot;Dettagli web ExperienceEvent&quot; selezionando **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]**.

   >[!NOTE]
   >
   >Se necessario, è possibile aggiungere più gruppi di campi.

1. Salva lo schema e prendi nota del nome che gli hai assegnato.

Per ulteriori informazioni sugli schemi, consulta la [guida del sistema Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it).

## Creare una proprietà di inoltro eventi

Nell’interfaccia utente Raccolta dati creare una proprietà di tipo &quot;Edge&quot;.

1. Seleziona **[!UICONTROL Nuova proprietà]**.

1. Assegna un nome alla proprietà.

1. Scegli il tipo di piattaforma “Edge”.

1. Seleziona **[!UICONTROL Salva]**.

Dopo aver creato la proprietà, passa alla scheda **[!UICONTROL Ambienti]** per la nuova proprietà e annota
gli ID dell’ambiente. Se l’organizzazione Adobe utilizzata nel datastream è diversa dall’organizzazione Adobe utilizzata nell’inoltro degli eventi, puoi copiare l’ID ambiente dalla scheda **[!UICONTROL Ambienti]** e incollarlo durante la creazione di un datastream. In alternativa, è possibile selezionare l’ambiente da un menu a discesa.

## Creare un datastream

Per creare il datastream in Adobe Experience Platform, utilizza l’ID ambiente generato quando hai creato la proprietà di inoltro dell’evento.

1. Utilizza il collegamento nella barra a sinistra dell’interfaccia utente Raccolta dati per aprire l’interfaccia datastreams.

1. Selezionare **[!UICONTROL Datastreams]**.

1. Assegna un nome alla configurazione e fornisci una descrizione facoltativa.
La descrizione è utile per identificare le configurazioni, qualora ne siano elencate diverse.

1. Seleziona **[!UICONTROL Salva]**.



## Abilita inoltro eventi

Quindi, configura la rete Edge per l’invio di dati all’inoltro eventi e ad altri prodotti Adobe.

1. Nell’interfaccia utente dei datastreams, seleziona la proprietà creata.

1. Seleziona l&#39;ambiente di sviluppo, di produzione oppure di gestione temporanea.

   Oppure, per inviare dati a un ambiente di inoltro eventi al di fuori dell&#39;organizzazione Adobe, seleziona **[!UICONTROL Passa alla modalità avanzata]** e incolla un ID. L&#39;ID viene fornito quando crei una proprietà di inoltro eventi.

1. Attiva gli strumenti necessari e configura le opzioni in base alle tue esigenze.

   * Adobe Analytics richiede un ID della suite di rapporti.

   * L&#39;inoltro degli eventi in Adobe Experience Platform richiede un ID di proprietà e un ID ambiente. Percorso di pubblicazione per la proprietà di inoltro eventi.

Dopo la configurazione, annota gli ID ambiente per la nuova proprietà.

## Configura l’estensione tag Web SDK per inviare dati al datastream creato in precedenza

Crea la proprietà nell’interfaccia utente di raccolta dati, quindi utilizza l’estensione Adobe Experience Platform Web SDK per configurarla.

1. Assegna un nome alla proprietà.

   Puoi avere più istanze di Alloy. Ad esempio, potresti avere diverse proprietà di tracciamento prima e dopo il paywall.

1. Seleziona l&#39;ID dell’organizzazione.

1. Seleziona il dominio Edge.

Per ulteriori opzioni di configurazione, consulta la [documentazione dell&#39;estensione SDK Web](../../extensions/web/sdk/overview.md).

## Creare una regola di tag per inviare dati all’SDK per web di Platform

Dopo aver implementato quanto sopra, crea definizioni di dati, regole e così via, che utilizzano l’inoltro eventi e i tag, ma che richiedono una sola richiesta dalla pagina.

Crea una regola di caricamento della pagina utilizzando l’estensione Platform Web SDK e il tipo di azione &quot;Invia evento&quot;:

1. Apri la scheda **[!UICONTROL Regole]**, quindi seleziona **[!UICONTROL Crea nuova regola]**.

1. Denomina la regola.

1. Seleziona **[!UICONTROL Eventi Aggiungi]**.

1. Aggiungi un evento scegliendo un&#39;estensione e uno dei tipi di evento disponibili per tale estensione, quindi configura le impostazioni dell&#39;evento. Ad esempio, seleziona **[!UICONTROL Core - Window Loaded]**.

1. Aggiungi un&#39;azione utilizzando l&#39;estensione Platform SDK Web. Seleziona **[!UICONTROL Invia evento]** dall&#39;elenco **[!UICONTROL Tipo di azione]**, scegli l’istanza desiderata (istanza di Alloy già configurata in precedenza), quindi seleziona un elemento dati da aggiungere al blocco dati XDM all’interno del riscontro di Alloy.

1. Lascia le altre impostazioni predefinite per questo esempio, quindi seleziona **[!UICONTROL Salva]**.

Per un altro esempio, potresti creare una regola che invia il livello dati a Edge se l&#39;utente passa il mouse su un pulsante specifico.

## Riepilogo

Con quanto segue, ora puoi creare regole di inoltro eventi per inoltrare i dati a destinazioni non Adobi.

* Schema Experience Data Model (prendi nota del nome che gli hai assegnato).
* Proprietà di inoltro eventi (tieni traccia degli ID proprietà e degli ID ambiente).
* Un datastream (prendi nota dell’ID ambiente, da non confondere con l’ID ambiente dall’inoltro degli eventi).
* Proprietà tag
