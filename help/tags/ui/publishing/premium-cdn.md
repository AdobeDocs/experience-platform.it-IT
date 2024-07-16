---
title: Tag Experience Platform (Cina)
description: Scopri la funzione Tag Experience Platform (Cina) per i tag e come utilizzarla per distribuire i contenuti in più aree geografiche.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Tag Experience Platform (Cina)

Quando si utilizza un [host gestito da Adobe](./hosts/managed-by-adobe-host.md) per distribuire le risorse dei tag Adobe Experience Platform sul sito Web, queste risorse vengono distribuite tra varie reti CDN (Content Delivery Network) in tutto il mondo per offrire la velocità di download più elevata. Tuttavia, alcune aree richiedono che tutte le risorse del sito web vengano replicate e ospitate su un server all’interno di tale area.

Per tenere conto di ciò, i tag in Experience Platform forniscono una funzione Experience Platform di Tag (Cina) che consente di distribuire contenuto a queste aree speciali.

Il supporto per i tag Experience Platform (Cina) è una funzione a pagamento e deve essere acquistato dalla tua organizzazione per abilitarla e utilizzarla. Questa guida illustra come configurare e utilizzare questa funzione nell’interfaccia utente di Experience Platform o di Data Collection dopo l’acquisto.

## Abilitare i tag Experience Platform (Cina) per la tua organizzazione

L’opzione Tag Experience Platform (Cina) è abilitata a livello aziendale. Dopo che la tua organizzazione ha acquistato la funzione Tag Experienci Platform (Cina), un amministratore di Adobi la abiliterà nell’interfaccia utente della tua azienda.

## Rigenera e installa le librerie di tag con codici di incorporamento aggiornati

Una volta abilitati i tag di Experience Platform (Cina), ciò non significa che le risorse tag vengano immediatamente replicate e pronte per l’uso nelle nuove aree geografiche. Significa solo che ora puoi scegliere quando dare il consenso a questa funzionalità.

>[!IMPORTANT]
>
>Le librerie create prima di abilitare i tag in Cina continueranno a funzionare così come sono oggi. Questo vale anche per le librerie non gestite da Adobe, in quanto [gli ambienti archiviati](./environments.md#archive) utilizzano solo URL relativi per i percorsi delle risorse. Tieni presente che dopo aver abilitato Experience Platform Tags (Cina), tutte le librerie create che non sono gestite da Adobe si comportano come se la funzione Tag in Cina non fosse abilitata.

Dopo aver abilitato i tag in Cina e ricostruito le librerie che desideri utilizzare dalle nuove aree di hosting, puoi recuperare i nuovi codici di incorporamento delle aree di hosting da aggiungere ai siti web.

>[!NOTE]
>
>Il codice di incorporamento della libreria elencato nell&#39;area di hosting [!UICONTROL Standard] continuerà a funzionare così com&#39;è, così come qualsiasi codice di incorporamento Page Top (Inizio pagina) o Page Bottom (Fine pagina) già presente nei tuoi siti Web.

Visita la pagina **[!UICONTROL Ambienti]** o visualizza le istruzioni di installazione dell&#39;ambiente dalla schermata di modifica della libreria per trovare i nuovi codici da incorporare. Ogni nuova area di hosting supportata viene visualizzata dopo l&#39;area di hosting [!UICONTROL Standard] (utilizzata per le aree del mondo che sono supportate senza tag Experience Platform (Cina)). La schermata seguente mostra un codice di incorporamento per l&#39;area geografica Cina, che utilizza `.cn` come dominio di primo livello (TLD).

![Codice di incorporamento per l&#39;area geografica Cina](../../images/ui/publishing/premium-cdn/embed-codes.png)

Scegliere il codice di incorporamento appropriato per la pagina Web e incollarlo nel tag `<head>` del documento. Per ulteriori informazioni sull&#39;utilizzo dei codici di incorporamento per installare le librerie di tag, consulta la [guida dell&#39;interfaccia utente degli ambienti](./environments.md#installation).

## Passaggi successivi

Questa guida illustra come abilitare e installare la funzione Tag Experienci Platform (Cina) per l’implementazione dei tag. Per ulteriori informazioni sull&#39;installazione e la verifica delle librerie di tag nelle proprietà Web e mobile, consulta la [panoramica sulla pubblicazione](./overview.md).
