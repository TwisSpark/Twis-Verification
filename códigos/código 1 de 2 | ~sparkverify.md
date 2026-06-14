### ⚠️ Asegúrate de copiar el código completo del comando "sparkverify".
---
Después de agregar el comando a tu bot, ve también al código "2 | $onInteraction" y cópialo completo.

Si falta una parte del sistema, la verificación no funcionará correctamente.
--

```
$deletecommand
$allowUserMentions[]
$addContainer[TwisVerification;#673ab7]
$addTextDisplay[## 👋 Bienvenido a $serverName[$guildID];TwisVerification]
$addSeparator[true;large;TwisVerification]
$addTextDisplay[Pulsa en el botón y completa el CAPTCHA para verificarte en este servidor.;TwisVerification]
$addActionRow[botones;TwisVerification]
$addButtonCV2[TwisCaptchaSelect;Verificarme Ahora;Secondary;false;📝;botones]

```
