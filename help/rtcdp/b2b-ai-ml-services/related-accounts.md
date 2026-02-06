---
title: Account correlati in Real-Time CDP B2B edition
type: Documentation
description: Panoramica e ulteriori informazioni sulla funzione account correlati in Experience Platform Real-Time CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it#rtcdp-editions" newtab=true
exl-id: 37fd2cdb-87c0-4e5e-9599-ad4f397f7c28
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 5%

---

# Account correlati in Real-Time CDP B2B edition

## Panoramica {#overview}

Le aziende B2B spesso dispongono di informazioni sui propri clienti archiviate in più sistemi, ciascuno dei quali include solo dati parziali o addirittura in conflitto per la stessa entità aziendale reale. Questo crea una sfida enorme: ottenere una visione accurata dei propri clienti, riducendo l&#39;efficienza e l&#39;efficacia delle attività di marketing e vendita B2B.

| ID | Nome | Sito web | Settore | Stato | Telefono | Ha un&#39;opportunità aperta con importo > `$1 million` |
|---|---|---|---|---|---|---|
| 1 | Acme | acme.com | Software | CA | (408)536-6000 |   |
| 2 | Acme | acm.com | Software | CA | 4085366000 | x |
| 3 | Acme Inc. |   |   | CA | (408)5366000 |   |
| 4 | Servizio di consulenza Acme | `http://www.acme.com/consulting` | Consulenza tecnologica | NY | (212) 471-0904 | x |
| 5 | Acme IT |   |   | CA |   |   |

{style="table-layout:auto"}

Con gli account correlati, [!DNL Real-Time CDP B2B] ora mostra un elenco di account simili a quelli che stai esplorando.

![Schermata che mostra gli account correlati nell&#39;interfaccia utente di Experience Platform.](/help/rtcdp/b2b-ai-ml-services/assets/related-accounts-in-ui.png)

Utilizza questa funzione per visualizzare i profili account correlati per un profilo account nell’interfaccia utente di Experience Platform e quindi includere gli account correlati nelle definizioni dei segmenti per ampliare la portata o applicare criteri più ampi ai tipi di pubblico.

## Abilita il servizio account correlati {#enable}

Per abilitare il servizio, selezionare **[!UICONTROL Profiles]** nella barra laterale seguito da **[!UICONTROL Settings]**.

![Interfaccia utente di Experience Platform che evidenzia profili e impostazioni.](../assets/../b2b-ai-ml-services/assets/related-account-settings.png)

Selezionare l&#39;interruttore accanto a [!UICONTROL Enable related accounts] per abilitare il servizio, quindi selezionare **[!UICONTROL Save]**.

![Nella schermata delle impostazioni account è evidenziata l&#39;opzione di attivazione/disattivazione e salvataggio.](../assets/../b2b-ai-ml-services/assets/related-account-toggle.png)

## Come funziona {#how-it-works}

I processi di apprendimento automatico giornalieri utilizzano un algoritmo gerarchico per raggruppare profili di account simili in gruppi sulla base di tre fattori:

* Collegamento account principale
* Dominio web
* Nome account

In seguito al completamento di un processo di elaborazione, a ogni membro del gruppo di profili di account viene assegnato il tag relativo all&#39;elenco Account correlati. Puoi visualizzare l&#39;elenco nella scheda **Account correlati** della pagina Profilo account e utilizzare gli account correlati nelle definizioni dei segmenti.

Consulta la documentazione per ulteriori informazioni sui [processi di account correlati all&#39;arricchimento dei profili](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).

## Come visualizzare gli account correlati {#how-to-view}

Puoi visualizzare gli account correlati per un account che stai esplorando nell’interfaccia utente di Experience Platform.

Per ulteriori informazioni su [come trovare account correlati nell&#39;interfaccia utente](/help/rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab), vedere la documentazione.

## Come utilizzare gli account correlati {#how-to-use}

Puoi utilizzare gli account e gli account correlati nella segmentazione. La decisione se utilizzare o meno account correlati nelle definizioni dei segmenti dipende dal caso di utilizzo di marketing. Ad esempio, puoi utilizzare account correlati per campagne di e-mail marketing o pubblicitarie, in cui puoi accettare una precisione inferiore in cambio di una portata più ampia.

Vedi un [esempio di segmentazione](/help/rtcdp/segmentation/b2b.md#related-accounts) che utilizza account correlati.
