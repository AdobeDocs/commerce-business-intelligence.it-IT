---
title: Connessione di MySQL tramite una connessione diretta
description: Scopri come connetterti [!DNL MongoDB] tramite connessione diretta.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Connetti [!DNL MongoDB] tramite connessione diretta

## In questo articolo

* [Consenti accesso a [!DNL MBI] Indirizzo IP](#allowlist)
* [Creare un ](#steptwo)
* [Immetti le informazioni di connessione in [!DNL MBI]](#stepthree)

## Passa a

* [&#39;MySQL tramite tunnel SSH&#39;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&quot;MySQL via cPanel&quot;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>L’Adobe consiglia di utilizzare [SSH](../integrations/mysql-via-ssh-tunnel.md) o un&#39;altra forma di crittografia per proteggere i dati. Se questa non è un&#39;opzione, è comunque possibile connettersi direttamente [!DNL MBI] nel database seguendo le istruzioni riportate in questo articolo.

Questo articolo illustra come collegare direttamente il database MySQL a [!DNL MBI]. Queste impostazioni possono essere utilizzate anche con Commerce o altri database di eCommerce che utilizzano MySQL.

## Consenti accesso a [!DNL MBI] Indirizzi IP {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma si trova anche nella pagina Credenziali MySQL:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creare un utente MySQL per [!DNL MBI]

Il modo più semplice per creare un’ `MySQL` utente per [!DNL MBI] : per eseguire la seguente query quando si accede a `MySQL` con `GRANT` privilegi. Sostituisci `MBI IP Address` con [!DNL MBI] Indirizzo IP e sostituzione `secure password` con una password sicura a tua scelta:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Per impedire all&#39;utente di accedere ai dati in database, tabelle o colonne specifici, è possibile eseguire `GRANT` query che consentono solo l&#39;accesso ai dati consentiti.

**Eseguire nuovamente la query GRANT per tutti gli IP richiesti utilizzando lo stesso utente e la stessa password.**

## Immetti le informazioni di connessione in MBI

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL MBI]. La pagina Credenziali MySQL è stata lasciata aperta? In caso contrario, vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi l&#39;icona MySQL. Non dimenticare di modificare il `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, iniziando da `Database Connection` sezione:

* `Connection Nickname`: immetti un nome per l’integrazione (ad esempio, Archivio e-commerce)
* `Username`: nome utente per [!DNL MBI] Utente MySQL
* `Password`: password per [!DNL MBI] Utente MySQL
* `Port`: porta MySQL sul server (`3306` per impostazione predefinita)
* `Host`: per impostazione predefinita, è localhost. In generale, si tratta del valore bind-address per il server MySQL, che per impostazione predefinita è `127.0.0.1 (localhost)`, ma potrebbe anche essere un indirizzo di rete locale (ad esempio, `192.168.0.1`) o l&#39;indirizzo IP pubblico del server.

   Il valore si trova nella `my.cnf` file (che si trova in `/etc/my.cnf`) sotto la riga che recita `\[mysqld\]`. Se la riga dell&#39;indirizzo di associazione viene inserita come commento in tale file, il server viene protetto dai tentativi di connessione esterni.

Tutto qui! Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Documentazione correlata

* [Reautenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
