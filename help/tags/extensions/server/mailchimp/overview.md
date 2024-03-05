---
title: Panoramica dell’estensione Mailchimp
description: Utilizza l’inoltro degli eventi per attivare le e-mail Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 4%

---

# Panoramica dell’estensione per l’inoltro di eventi Mailchimp

>[!NOTE]
>  
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) come riferimento consolidato delle modifiche terminologiche.

Il Mailchimp [inoltro eventi](../../../ui/event-forwarding/overview.md) L’estensione invia eventi all’API di marketing Mailchimp che possono attivare le e-mail per campagne di marketing, percorsi o transazioni di Mailchimp.

Questo documento illustra come impostare l’estensione e configurare le regole utilizzando l’azione Aggiungi evento.

## Prerequisiti

In questo documento si presuppone che tu abbia familiarità con i prodotti Mailchimp rilevanti utilizzati dall’estensione. Per ulteriori informazioni, consulta la guida di Mailchimp per [campagne](https://mailchimp.com/help/getting-started-with-campaigns/), [percorsi](https://mailchimp.com/help/about-customer-journeys/), e [transazioni](https://mailchimp.com/help/transactional/).

Per utilizzare questa estensione è necessario un account Mailchimp. È possibile registrarsi a un account [qui](https://login.mailchimp.com/signup/). Nel dashboard dell’account Mailchimp, annota i seguenti valori da utilizzare in questa guida:

- Prefisso del dominio Mailchimp
- Chiave API
- L’ID del pubblico
- L’indirizzo e-mail predefinito del mittente

A seconda del piano dell’account Mailchimp, puoi avere un accesso limitato agli strumenti di Percorso del cliente Mailchimp.

>[!TIP]
>  
>Se utilizzi automazioni Mailchimp come e-mail transazionali o Percorsi di clienti, i passaggi e le schermate potrebbero essere leggermente diversi da quelli elencati. Tuttavia, per utilizzare questa estensione ti servono ancora le stesse informazioni descritte in precedenza. Consulta la [Centro assistenza Mailchimp](https://mailchimp.com/help/) per informazioni dettagliate su ciascuno di questi valori per il tuo account e piano specifico.

### Prefisso dominio

Dopo aver effettuato l’accesso a Mailchimp e essere approdato nella vista Dashboard, la barra degli indirizzi del browser dovrebbe visualizzare un URL simile al seguente: `https://us11.admin.mailchimp.com` o semplicemente `us11.admin.mailchimp.com`. In questo esempio, il prefisso `us11` è solo un segnaposto e il valore sarà diverso. Registra l’URL con il prefisso per un passaggio successivo.

### Chiave API

Per trovare la chiave API per l’account, seleziona l’icona del profilo nell’interfaccia utente di Mailchimp, quindi seleziona **Profilo**. Dovresti visualizzare un URL come `https://us11.admin.mailchimp.com/account/profile/` ma con **tuo** prefisso invece di `us11`.

Seleziona **Funzionalità aggiuntive**, quindi **Chiavi API**:

![Menu Extra, collegamento alle chiavi API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Sotto **Le chiavi API**, puoi scegliere una chiave esistente o selezionare **Creare Una Chiave** per crearne uno nuovo. Puoi creare una nuova chiave da utilizzare specificamente con questa estensione. Copia la chiave API e salvala per un passaggio successivo. Per ulteriori dettagli, consulta la documentazione di Mailchimp su come [generare la chiave API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID pubblico e indirizzo mittente

Seleziona **Pubblico** nel menu di navigazione a sinistra, quindi **Dashboard del pubblico**. Quindi, seleziona il pubblico che intendi utilizzare con questa estensione. Per ulteriori informazioni, consulta il documento Mailchimp su [creazione di un pubblico](https://mailchimp.com/help/create-audience/).

Dopo aver creato e selezionato il pubblico, seleziona la **Gestisci pubblico** e scegli **Impostazioni**. Questa schermata mostra varie impostazioni per il pubblico.

Nella parte inferiore della schermata Settings (Impostazioni) dovresti vedere `Unique id for audience [audience name]` dove `[audience name]` è il nome del pubblico effettivo. Copia l’ID pubblico e salvalo per un passaggio successivo.

Seleziona **Nome pubblico e impostazioni predefinite** e confermare che **Indirizzo e-mail mittente predefinito** ha il valore corretto per le campagne. Tieni presente che anche l’ID pubblico è elencato nella parte superiore di questa pagina e corrisponde al valore copiato nell’ultimo passaggio.

## Automazioni Mailchimp

A seconda del piano Mailchimp e dell’utilizzo di e-mail transazionali, Percorsi di clienti o altre automazioni di Mailchimp, le impostazioni di percorso specifiche possono variare.

>[!IMPORTANT]
>  
>Il nome dell’evento scelto per attivare l’automazione o il percorso in Mailchimp è lo stesso nome che devi inviare con questa estensione. Prendi nota del nome dell’evento nell’automazione Mailchimp e salvalo per un passaggio successivo.

## Installazione e configurazione

In questa sezione sono elencati i passaggi per installare e configurare l’estensione. Per salvare in modo sicuro la chiave API Mailchimp, devi utilizzare l’inoltro degli eventi [segreti](../../../ui/event-forwarding/secrets.md).

### Creare un elemento segreto e dati

In una proprietà di inoltro degli eventi, [creare un [!UICONTROL Token] segreto](../../../ui/event-forwarding/secrets.md#token) ha chiamato `Mailchimp API Key`.

Avanti, [creare un elemento dati](../../../ui/managing-resources/data-elements.md#create-a-data-element) utilizzando [!UICONTROL Core] e un [!UICONTROL Segreto] tipo di elemento dati per fare riferimento a `Mailchimp API Key` segreto appena creato. Invio `Mailchimp Token` come nome dell’elemento dati.

### Installare e configurare l’estensione

Nella stessa proprietà di inoltro degli eventi, seleziona **[!UICONTROL Estensioni],** allora **[!UICONTROL Catalogo]** per visualizzare le estensioni disponibili per l&#39;installazione. Da qui, cerca l’estensione Mailchimp e seleziona **[!UICONTROL Installa]**.

![Installare l’estensione Mailchimp](../../../images/extensions/server/mailchimp/install.png)

Viene visualizzata la schermata di configurazione. Sotto **[!UICONTROL Nome dominio prefisso server Mailchimp]**, immetti il dominio copiato in precedenza dall&#39;account Mailchimp, incluso il prefisso di dominio univoco.

>[!IMPORTANT]
>
>Non includere `http://` o `https://` in questo campo.

![Configurazione dell&#39;estensione](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Sotto **[!UICONTROL Token Mailchimp]**, seleziona l’icona dell’elemento dati e scegli `Mailchimp Token` elemento dati creato in precedenza. Seleziona **[!UICONTROL Salva]** per salvare le modifiche.

L&#39;estensione è ora installata e configurata per l&#39;utilizzo nella proprietà.

## Raccolta dati

Quando utilizzi questa estensione in una [regola](../../../ui/managing-resources/rules.md), con ogni evento l’estensione invia a Mailchimp diversi valori di dati. Per un’implementazione tipica, puoi configurare il [Estensione Adobe Experience Platform Web SDK](../../client/web-sdk/overview.md) per inviare tali dati a [!DNL Platform Edge Network] da utilizzare dall’estensione nella proprietà di inoltro degli eventi.

I dati richiesti da questa estensione possono essere inviati da Web SDK come dati XDM (utilizzando [`xdm`](/help/web-sdk/commands/sendevent/xdm.md) oggetto ) o dati non XDM (utilizzando il [`data`](/help/web-sdk/commands/sendevent/data.md) oggetto ).

Ad esempio, se un cliente effettua un acquisto o si registra per un evento sul sito, puoi inviare un’e-mail di conferma tramite Mailchimp con questa estensione. Una volta inviate le informazioni richieste da Web SDK alla rete Edge, l’estensione attiva l’e-mail con Mailchimp.

![Aggiungi configurazione azione evento](../../../images/extensions/server/mailchimp/action-configurations.png)

### Elementi dati

La schermata nella sezione precedente mostra i dati che puoi inviare con ogni evento da questa estensione a Mailchimp. Una volta configurato Web SDK per inviare tali dati alla rete Edge, puoi creare elementi di dati nella proprietà di inoltro degli eventi in modo che l’estensione possa accedere a tali valori.

La tabella seguente fornisce maggiori dettagli per ciascun valore possibile.

| Nome | Percorso di esempio | Tipo | Descrizione | Obbligatorio | Limiti |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> o<br /> `arc.event.data._tenant.emailId` | Stringa | Indirizzo che riceve l’e-mail | **Sì** | Deve esistere nel pubblico Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> o<br /> `arc.event.data._tenant.listid` | Stringa | ID pubblico | **Sì** | Deve corrispondere a un ID pubblico esistente |
| `name` | `arc.event.xdm._tenant.name`<br /> o<br /> `arc.event.data._tenant.name` | Stringa | Nome dell’evento | **Sì** | 2-30 caratteri |
| `properties` | `arc.event.xdm._tenant.properties`<br /> o<br /> `arc.event.data._tenant.properties` | Oggetto | Un elenco facoltativo di proprietà in formato JSON con dettagli sull’evento | No |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> o<br /> `arc.event.data._tenant.isSyncing` | booleano | Eventi creati con `is_syncing` imposta su `true` **non** automazioni trigger | No |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> oppure `arc.event.data._tenant.occuredAt` | Stringa | Una marca temporale ISO 8601 del momento in cui si è verificato l’evento | No |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>Il **Percorso di esempio** i valori riportati sopra sono solo esempi. I nomi dei campi e [percorsi](../../../ui/event-forwarding/overview.md#data-element-path) Tali elementi dati possono fare riferimento a elementi diversi nella proprietà, a seconda di come è stato denominato e configurato Web SDK nei passaggi precedenti.

Nella proprietà di inoltro degli eventi, puoi creare un elemento dati per ciascuno dei campi descritti in precedenza. Una volta creati, puoi fare riferimento agli elementi dati nel [!UICONTROL Aggiungi evento] azione di questa estensione.

![Aggiungi configurazione azione evento](../../../images/extensions/server/mailchimp/action-configurations.png)

Ora puoi utilizzare questa estensione e l’azione Aggiungi evento per attivare le e-mail Mailchimp per i tipi di pubblico.

## Convalida dei dati

Quando si lavora con estensioni di inoltro eventi, il [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) è molto utile. Nella sezione Registri, in Registri Edge puoi visualizzare le richieste effettuate dalle regole di inoltro degli eventi dopo che sono state attivate. Le schermate seguenti mostrano una richiesta all’API Mailchimp da parte dell’estensione.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Nel dashboard Mailchimp, nella vista Feed attività del pubblico o del membro del pubblico, viene fornito un elenco di eventi per quel pubblico o membro del pubblico. Questo deve corrispondere agli eventi inviati dall&#39;estensione e mostrare tutti i dati facoltativi inviati, insieme all&#39;e-mail o alla campagna che hanno ricevuto. Consulta la [Guide per l&#39;automazione di Mailchimp](https://mailchimp.com/help/automation/) per ulteriori dettagli.
