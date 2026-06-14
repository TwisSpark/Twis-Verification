## ⚙️ Configuración del "$onInteraction"

Antes de usar el sistema, debes configurar el ID del rol de verificación.

Busca esta línea dentro del código:

```
$var[rol_id;1515560567815802920] $c[← Cambia esta ID por el rol que quieres dar a los usuarios cuando completen la verificación]`
```

## 📌 ¿Por qué debes cambiarla?

Esa ID es solo un ejemplo.

Si no cambias la ID:

- El sistema no podrá dar el rol correctamente.
- Los usuarios no serán verificados.
- El CAPTCHA parecerá funcionar, pero no dará acceso al servidor.

---

## ✅ Cómo obtener la ID del rol

1. Activa el modo desarrollador en Discord.
2. Haz clic derecho sobre el rol de verificación.
3. Pulsa en "Copiar ID".
4. Reemplaza la ID del ejemplo por la tuya.

---

## ⚠️ Importante

- No elimines **"$var[rol_id;]"**
- Solo cambia los números de la ID.
- Asegúrate de que el bot tenga permisos para dar roles.
- El rol del bot debe estar arriba del rol de verificación en la lista de roles de Discord.

---

## 💡 Consejo

Muchos errores pasan porque las personas:

- No copian el "$onInteraction"
- No cambian la ID del rol
- O copian el sistema incompleto

Si algo no funciona, revisa eso primero antes de decir que el sistema está roto.

--

```
$onlyIf[$checkContains[$customID;TwisCaptchaSelect;TwismenúVerify]==true;]
$var[rol_id;1515560567815802920] $c[← Cambia esta ID por el rol que quieres dar a los usuarios cuando completen la verificación]

$if[$customID==TwisCaptchaSelect]
$if[$hasRole[$authorID;$var[rol_id]]==false]
$httpGet[https://akiomae.xyz/api/others/captcha.php]
$ephemeral 
$addContainer[TwisCaptchaSelect;#673ab7]
$addTextDisplay[## 🧩 Elije el código del CAPTCHA;TwisCaptchaSelect]
$addSeparator[true;large;TwisCaptchaSelect]
$addTextDisplay[Selecciona el código correcto para completar la verificación y acceder al servidor.;TwisCaptchaSelect]
$addSeparator[false;large;TwisCaptchaSelect]
$addMediaGallery[imagen;TwisCaptchaSelect]
$addMediaGalleryItem[$httpResult[api_response;url];;false;imagen]
$addSeparator[true;large;TwisCaptchaSelect]
$addActionRow[menú;TwisCaptchaSelect]
$addStringSelect[TwismenúVerify;Elige alguna opción;1;1;false;menú]
$addStringSelectOption[$httpResult[generated_codes;code1];TwisVerify-$httpResult[generated_codes;code1]==$httpResult[api_response;code];;;false;TwismenúVerify]
$addStringSelectOption[$httpResult[generated_codes;code2];TwisVerify-$httpResult[generated_codes;code2]==$httpResult[api_response;code];;;false;TwismenúVerify]
$addStringSelectOption[$httpResult[generated_codes;code3];TwisVerify-$httpResult[generated_codes;code3]==$httpResult[api_response;code];;;false;TwismenúVerify]
$addStringSelectOption[$httpResult[generated_codes;code4];TwisVerify-$httpResult[generated_codes;code4]==$httpResult[api_response;code];;;false;TwismenúVerify]
$addStringSelectOption[$httpResult[generated_codes;code5];TwisVerify-$httpResult[generated_codes;code5]==$httpResult[api_response;code];;;false;TwismenúVerify]
$else
$ephemeral
$addContainer[TwisAlreadyVerified;#2196f3]
$addTextDisplay[✅ Ya estás verificado;TwisAlreadyVerified]
$addSeparator[true;large;TwisAlreadyVerified]
$addTextDisplay[No puedes volver a verificarte porque ya tienes el rol de verificación en este servidor.;TwisAlreadyVerified] 
$endif 
$endif 

$if[$checkContains[$customID;TwismenúVerify]==true]
$textSplit[$message;-]
$if[$splitText[2]]
$addContainer[TwisVerificationSuccess;#4caf50]
$addTextDisplay[## ✅ Verificación completada;TwisVerificationSuccess]
$addSeparator[true;large;TwisVerificationSuccess]
$addTextDisplay[Has sido verificado correctamente. Ya puedes acceder al servidor y disfrutar de todas las funciones.;TwisVerificationSuccess]
$try$roleGrant[$authorID;+$var[rol_id]]$endtry

$else  
$addContainer[TwisVerificationError;#f44336]
$addTextDisplay[## ❌ CAPTCHA incorrecto;TwisVerificationError]
$addSeparator[true;large;TwisVerificationError]
$addTextDisplay[Ese no era el CAPTCHA correcto. Vuelve a pulsar el botón e inténtalo otra vez.;TwisVerificationError]
$endif 
$endif 

```




