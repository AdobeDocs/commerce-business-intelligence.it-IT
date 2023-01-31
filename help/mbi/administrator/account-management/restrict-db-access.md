---
title: Limitazione dell'accesso al database
description: Scopri come limitare l’accesso, limitare l’accesso al server che ospita il database.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Accesso limitato

Quando creiamo un tunnel SSH per il tuo server, non è necessario [!DNL MBI] avere accesso a qualsiasi cosa tranne il database. Se non vuoi [!DNL MBI] per avere pieno accesso al server che ospita il database, è possibile limitare l&#39;accesso forzando il [!DNL MBI Linux] in un [conchiglia bash limitata](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Si può avere indovinato dal nome, ma una shell bash limitata viene utilizzata per impostare un ambiente più controllato della shell standard. La cosa importante di questo tipo di shell è che gli utenti con shell limitate non possono accedere alle funzioni del sistema o apportare qualsiasi tipo di modifica.

Per limitare [!DNL MBI Linux] utente, è necessario eseguire due operazioni:

1. Cambia la variabile di ambiente PATH in stringa vuota. Ciò significa che l&#39;utente non sarà in grado di accedere ai file eseguibili del sistema.

1. Assicurati che la shell eseguita sia `bash -r`

Entrambi possono essere eseguiti all&#39;interno della `authorized_keys` file nella home dell&#39;utente `dir/.ssh` come parte del comando eseguito quando l&#39;utente effettua l&#39;accesso. Avrà un aspetto simile a questo:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Una volta completato, l&#39;utente creato per [!DNL MBI] non sarà in grado di apportare modifiche al sistema.
