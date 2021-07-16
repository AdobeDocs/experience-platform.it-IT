---
title: Host SFTP
description: Scopri come configurare i tag in Adobe Experience Platform per distribuire build della libreria a un server SFTP protetto e self-hosting.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 48%

---

# Host SFTP

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Se non vuoi che le librerie ospitate vengano gestite da Adobe, puoi fare sì che Adobe Experience Platform distribuisca le build a un tuo server SFTP protetto.

Platform si collega al tuo sito SFTP utilizzando una chiave crittografata. Sono disponibili alcuni passaggi per eseguire correttamente la configurazione:

1. Sul server SFTP deve essere installata una coppia di chiave pubblica/privata. Puoi generare queste chiavi sul tuo server o generarle in un altro punto e installarle sul tuo server. Per ulteriori informazioni, consulta la documentazione GitHub relativa a [come generare chiavi SSH](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#generating-a-new-ssh-key) .
1. La chiave privata viene utilizzata per crittografare la chiave GPG pubblica. Dovrai fornire la tua chiave privata durante il processo di creazione dell’host SFTP. Per istruzioni sulla crittografia delle chiavi GPG pubbliche, consulta la sezione [Cifra valori](https://developer.adobelaunch.com/api/guides/encrypting_values/) nella documentazione API del reattore . Utilizza la chiave GPG dell’ambiente di produzione a meno che tu non sappia di aver bisogno di una chiave specifica. Infine, puoi crittografare la tua chiave privata da qualsiasi computer, per cui non devi installare GPG sul server per completare questo passaggio.
1. Potrebbe essere necessario approvare gli indirizzi IP utilizzati con il firewall aziendale per consentire a Platform di raggiungere il server SFTP e connettersi ad esso. Gli indirizzi IP sono:
   * `184.72.239.68`
   * `23.20.85.113`
   * `54.226.193.184`

>[!NOTE]
>
>La struttura delle build dei tag è cambiata nel tempo. Utilizzano internamente dei collegamenti simbolici (symlink) per mantenere la compatibilità con le versioni precedenti, affinché i codici precedentemente incorporati possano continuare a funzionare anche con la struttura di build più recente. Per poter essere utilizzato come destinazione valida per le build dei tag, il server SFTP deve supportare l’utilizzo di symlink.

Per informazioni più dettagliate, consulta il seguente articolo Media su [come configurare i server SFTP per distribuire una build](https://medium.com/launch-by-adobe/configuring-an-sftp-server-for-use-with-adobe-launch-bc626027e5a6).

## Creare un host SFTP

1. Apri la scheda [!UICONTROL Host].
1. Crea il nuovo host.
1. Assegna un nome all&#39;host.
1. Seleziona **[!UICONTROL SFTP]** come tipo di host.
1. Immetti l’host, il percorso, la porta, il nome utente e la chiave privata crittografata.

   Per la porta, scegli una delle seguenti possibilità:

   * 21
   * 22
   * 80
   * 200-299
   * 443
   * 2000-2999
   * 4343
   * 8080
   * 8888

   >[!NOTE]
   >
   >Come best practice per la sicurezza, Adobe limita il numero di porte che possono essere utilizzate per il traffico in uscita. Le porte selezionate sono solitamente consentite dai firewall aziendali e includono alcuni intervalli per garantire flessibilità.

1. Seleziona **[!UICONTROL Salva]**.

Quando selezioni **[!UICONTROL Salva]**, viene verificata la connessione e la capacità di consegnare i file al server SFTP. Platform crea una cartella, scrive un file all’interno di tale cartella, verifica che il file sia presente, quindi si ripulisce da solo. Se l’account utente sul server SFTP (quello associato al certificato protetto fornito a Platform) non dispone delle autorizzazioni necessarie per eseguire questa azione, l’host passa a uno stato &quot;Non riuscito&quot;.
