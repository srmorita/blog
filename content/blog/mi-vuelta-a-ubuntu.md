+++
date = '2025-11-28T16:18:15-03:00'
draft = true
slug = 'mi-vuelta-a-ubuntu'
title = 'Mi vuelta a Ubuntu'
description = "He vuelto a Ubuntu en su versión 24.04.3"
keywords = ['ubuntu', 'gnu', 'linux']
+++
### Contexto

Hace unos meses en mi lugar de trabajo cambiamos el framework con el cual automatizamos pruebas, estabamos usando [WebdriverIO](https://webdriver.io/ 'WebdriverIO website') y en su lugar pasamos a usar [Playwright](https://playwright.dev/ 'Playwright website'), todo esto enmarcado en una migración hacia productos __Microsoft__ y como es algo laboral no tengo mayor injerencia en la toma de decisiones.

Esto provocó algo que no tenia pensado, volver a [Ubuntu](https://ubuntu.com/ 'Ubuntu website') y dejar mi zona de confort en __Archlinux__, te preguntarás por qué tuve que hacerlo, pues la razón es muy sencilla y a la vez me hace odiar más los productos del tio __Bill__.

_Playwright_ no tiene soporte a distribuciones distintas a _Debian_ y _Ubuntu_, fin del comunicado. Bueno no tan así tampoco, en _Debian_ incluso falla al instalar las dependencias necesarias para la gestión automatica de los browser y en Ubuntu tengo cero fallos de dependencias.

En _Archlinux_ es imposible instalar las dependencias, [algo ya documentado en el github](https://github.com/microsoft/playwright/issues/8100 'Playwright issue en github') y sin planes para soportar esta distro. __Playwright__ intenta instalarlas basandose en __APT__, intenté lo descrito en el blog de [Nicoandres](https://blog.nicoandres.dev/use-playwright-in-arch-linux/ 'Blog con posible solución a Plauwright en Archlinux') pero tira de AUR, lo cual, no utilizo porque no me gusta agregar paquetes que puedan ser inestables en algún momento.

![Playwright error deps]( /img/playwright_error.png "Playwright error deps")

### ¿Por qué Ubuntu?

Pues _Ubuntu_ fué mi segunda distro al comenzar a usar __GNU/linux__ por allá en el año 2010 si mal no recuerdo. utilicé el [programa de envíos de Ubuntu](https://ubuntu.com/blog/keeping-ubuntu-cds-available 'ShipIt program Ubuntu') y me llegaban los CD's a mi casa para probar esta distribución y por eso le tengo un especial cariño.

Otra razón importante fue entender de primera fuente si los los comentarios infundados en ciertos lugares eran ciertos, comentarios tales como:

1. Ubuntu ya no es para seres humanos.
2. Snap es basura y lento.
3. Cualquier cosa que haga _Canonical_ es malo para el mundo linuxero.

Y debo decirte que nada de eso es cierto.

### Mis impresiones al trabajar en Ubuntu como estación de trabajo

En primer lugar quiero aclarar este punto. No uso __GNU/Linux__ para gaming, ni distrohopping. Necesito algo que me permita instalar y usar para trabajar. Agradezco por lo menos tener la opción de ocupar el sistema operativo de mi preferencia en el trabajo.

#### Instalación

En este punto Ubuntu va como la seda, en menos de 10 minutos ya tenia instalado el sistema, _UEFI_ y _Secure Boot_ habilitados en mi __BIOS__. Particionado manual, ya que, tengo una partición _/data_ aparte y sin partición _SWAP_, acá ubuntu se hace cargo automáticamente con _ZRAM_ o swap sobre tu memoria ram.

Mi gráfica es AMD (fuck you nvidia!!!), interfaz de audio __Audient ID 14 MkII__ reconocida desde el principio.

#### Aplicaciones

_Slack_ para el trabajo en formato snap funcionando sin problemas. Esta es la aplicación para coordinación así que era inevitable su instalación. No comento otras aplicaciones de desarrollo comunes por que funcionan bien en cualquier distro.

Debo si comentar acá un problemilla con la __Snap Store__ que no se actualiza con un simple `apt update` y hay que tirar de consola.

```bash
sudo killall snap-store
sudo snap refresh snap-store
```

#### Uso diario

Llevo más de un mes con Uuntu. Enciendo mi equipo temprano, trabajo, lo apago al final de mi jornada sin problemas. Es aburrido de lo bien que va Ubuntu. Cero congelamientos, cero kernel panics, nada que decir.

### Conclusiones

Después de tantos años sin utilizar Ubuntu de forma profesional/laboral me ha dejado sorprendido su rendimiento y lo bien que se siente su uso.

Ahora con el fin de soporte de _Ventanas 10__, Ubuntu sin lugar a dudas es una gran opción para quien busca una distro llegar y usar.

¿Volveré a __Archlinux__? por el momento no. Ubuntu es mi casa para el trabajo por ahora.

EOF.
