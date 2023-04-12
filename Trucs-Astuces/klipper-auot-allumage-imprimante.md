## Démarrer / redémarrer Klipper à l'allumage de l'imprimante

L'imprimante a été éteinte mais le Sonic Pad est resté allumé.

Procrastinateur né, vous trouvez trop fatiguant de devoir appuyer sur 'Redémarrer Klipper' à chaque allumage de l'imprimante ?

>  Un accès root est obligatoire pour pouvoir réaliser cette manipulation.

Suivre ce qui suit pour que klipper redémarre automatiquement lorsque l'imprimante est rallumée.

**[RAPPEL] manipulations à réaliser en tant qu'utilisateur «root»**

Créer une régle UDEV `/etc/udev/rules.d/98-klipper.rules` avec le contenu:

```
SUBSYSTEM=="usb", ATTRS{idVendor}=="1a86", ATTRS{idProduct}=="7523", ACTION=="add", RUN+="/bin/sh -c 'echo RESTART > /tmp/printer'"
```

puis modifier les droits (exécution) de cette règle et mettre à jour la base UDEV :

```
chmod +x /etc/udev/rules.d/98-klipper.rules
udevadm control --reload (ou redémarrer le Sonic Pad)
```

Sources:
- [Github Klipper](https://github.com/Klipper3d/klipper/issues/835)