---
title: Supporto CDN Premium per i tag
description: Scopri la funzione CDN Premium per i tag e come utilizzarla per distribuire i contenuti in più aree geografiche.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Supporto CDN Premium per i tag (Beta)

>[!IMPORTANT]
>
>La funzione CDN Premium per i tag è attualmente in versione beta e la tua organizzazione potrebbe non averne ancora accesso. Questa documentazione è soggetta a modifiche.

Quando si utilizza un’ [Host gestito da Adobe](./hosts/managed-by-adobe-host.md) per distribuire le risorse dei tag Adobe Experience Platform sul sito web, queste risorse vengono distribuite tra varie reti CDN (content delivery network) in tutto il mondo per offrire la velocità di download più rapida. Tuttavia, alcune aree richiedono che tutte le risorse del sito web vengano replicate e ospitate su un server all’interno di tale area.

Per tenere conto di questo, i tag in Experience Platform forniscono una funzione CDN Premium che consente di distribuire contenuti a queste aree speciali.

Il supporto CDN Premium è una funzione a pagamento e deve essere acquistato dall’organizzazione per abilitarlo e utilizzarlo. Questa guida illustra come configurare e utilizzare questa funzione nell’interfaccia utente di Experience Platform o di Data Collection dopo l’acquisto.

## Abilita CDN premium per la tua organizzazione

La rete CDN Premium è abilitata a livello aziendale. Dopo che la tua organizzazione ha acquistato la funzione CDN Premium, un amministratore di Adobe la abiliterà nell’interfaccia utente della tua azienda.

## Rigenera e installa le librerie di tag con codici di incorporamento aggiornati

Una volta abilitata la rete CDN Premium, ciò non significa che le risorse tag vengano immediatamente replicate e pronte per l’uso nelle nuove aree geografiche. Significa solo che ora puoi scegliere quando dare il consenso a questa funzionalità.

>[!IMPORTANT]
>
>Le librerie create prima di abilitare la rete CDN Premium continueranno a funzionare così come sono. Questo vale anche per le librerie non gestite da Adobe, in quanto [ambienti archiviati](./environments.md#archive) utilizza solo URL relativi per i percorsi delle risorse. Dopo aver abilitato la rete CDN Premium, tutte le librerie create e non gestite da Adobe si comportano come se la funzione CDN Premium non fosse abilitata.

Dopo aver attivato la rete CDN Premium e ricostruito le librerie che desideri utilizzare dalle nuove aree di hosting, puoi recuperare i nuovi codici di incorporamento delle aree di hosting da aggiungere ai siti web.

>[!NOTE]
>
>Il codice di incorporamento della libreria elencato in [!UICONTROL Standard] l&#39;area di hosting continuerà a funzionare così come è, così come eventuali codici di incorporamento Page Top (Inizio pagina) o Page Bottom (Fine pagina) già presenti sui tuoi siti web.

Visita il **[!UICONTROL Ambienti]** o visualizzare le istruzioni di installazione dell’ambiente dalla schermata modifica libreria per trovare i nuovi codici da incorporare. Ogni nuova area di hosting supportata viene visualizzata dopo il [!UICONTROL Standard] area di hosting (utilizzata per aree del mondo che sono supportate senza CDN Premium). La schermata seguente mostra un codice da incorporare per l’area geografica Cina, che utilizza `.cn` come dominio di primo livello (TLD).

![Codice di incorporamento per l’area geografica Cina](../../images/ui/publishing/premium-cdn/embed-codes.png)

Scegli il codice di incorporamento appropriato per la pagina web e incollalo all’interno del `<head>` del documento. Per ulteriori informazioni sull’utilizzo dei codici di incorporamento per installare le librerie di tag, consulta [guida all’interfaccia utente degli ambienti](./environments.md#installation).

## Passaggi successivi

Questa guida illustra come abilitare e installare la funzione CDN Premium per l’implementazione dei tag. Per ulteriori informazioni sull’installazione e il test delle librerie di tag nelle proprietà web e mobili, consulta [panoramica sulla pubblicazione](./overview.md).
