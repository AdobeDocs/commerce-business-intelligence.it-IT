---
title: Connessione di MySQL tramite una connessione diretta
description: Scopri come connettersi [!DNL MongoDB] tramite connessione diretta.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Connetti [!DNL MongoDB] tramite connessione diretta

## In questo articolo

* [Consenti accesso al [!DNL MBI] Indirizzo IP](#allowlist)
* [Crea un ](#steptwo)
* [Immetti le informazioni di connessione in [!DNL MBI]](#stepthree)

## Passa a

* [`MySQL tramite tunnel SSH`](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [`MySQL tramite cPanel`](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Si consiglia vivamente di utilizzare [SSH](../integrations/mysql-via-ssh-tunnel.md) o qualche altra forma di crittografia per proteggere i tuoi dati! Se questa non è un&#39;opzione, è comunque possibile connettersi direttamente [!DNL MBI] al database utilizzando le istruzioni contenute in questo articolo.

In questo articolo viene descritto come collegare direttamente il database MySQL a [!DNL MBI]. Queste impostazioni possono essere utilizzate anche con Commerce o altri database eCommerce che utilizzano MySQL.

## Consenti accesso al [!DNL MBI] Indirizzi IP {#allowlist}

Affinché la connessione abbia successo, devi configurare il firewall per consentire l’accesso dai nostri indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma si trova anche nella pagina delle credenziali MySQL:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Creare un utente MySQL per [!DNL MBI]

Il modo più semplice per creare un `MySQL` utente per [!DNL MBI] deve eseguire la seguente query al momento dell&#39;accesso `MySQL` con `GRANT` privilegi. Sostituisci `MBI IP Address` con [!DNL MBI] Indirizzo IP e sostituzione `secure password` con una password sicura a tua scelta:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Per impedire all&#39;utente di accedere ai dati in database, tabelle o colonne specifici, è invece possibile eseguire `GRANT` query che consentono solo l’accesso ai dati consentiti.

**Esegui nuovamente la query GRANT per tutti gli IP richiesti utilizzando lo stesso utente e la stessa password.**

## Immettere le informazioni di connessione in MBI

Per concludere, dobbiamo inserire la connessione e le informazioni utente in [!DNL MBI]. Hai lasciato aperta la pagina delle credenziali MySQL? In caso contrario, vai a **[!UICONTROL Data** > **Connections]** e fai clic su **[!UICONTROL Add New Data Source]**, quindi l&#39;icona MySQL. Non dimenticare di modificare le `Encrypted` passa a `Yes`.

Immetti le seguenti informazioni in questa pagina, a partire dal `Database Connection` sezione:

* `Connection Nickname`: Immetti un nome per l’integrazione (ad esempio, Ecommerce Store)
* `Username`: Il nome utente per il [!DNL MBI] Utente MySQL
* `Password`: La password per [!DNL MBI] Utente MySQL
* `Port`: Porta di MySQL sul server (`3306` per impostazione predefinita)
* `Host`: Per impostazione predefinita, è localhost. In generale, sarà il valore bind-address per il server MySQL, che per impostazione predefinita è `127.0.0.1 (localhost)`, ma potrebbe anche essere un indirizzo di rete locale (ad esempio, `192.168.0.1`) o l&#39;indirizzo IP pubblico del server.

   Il valore si trova nella `my.cnf` file (di solito si trova in `/etc/my.cnf`) sotto la riga che legge `\[mysqld\]`. Se nel file viene commentata la riga dell&#39;indirizzo di binding, il server viene protetto da tentativi di connessione esterni.

Tutto qui! Al termine, fai clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Documentazione correlata

* [Riautenticazione delle integrazioni](https://support.magento.com/hc/en-us/articles/360016733151)
