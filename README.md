

### Hoggax Rive Integration   
Here is a simple code test for rive integration to hoggax front end app
[Rive Page](https://rive.app/runtimes/)  
  



### Vainilla Integration  
For a Simple and Vainilla integration It's neccesary to import this script in the html:


```<script src="assets/rive.min.js"></script>```

**Then** 
Use a canvas html tag for animation DOM holding

```<canvas id="05_oficina" width="900" height="900"></canvas>```

(Look at the name "05_oficina", it's the anme of one animation listed later)

**Finally** You only need to exec this script at the bottom of the html
```
<script type="text/javascript">
    var items2Check = [
      '01_hero_image',
      'pajaro_ultimo2',
      '02_translado_city',
      '02_translado_fondo',
      '03_online',
      '04_reporteAprobado',
      '05_oficina'
    ];
    var rivePlayers = [];

    function startAnim(animName) {
        var heroAnim = new rive.Rive({
          src: "assets/animaciones/" + animName + ".riv",
          canvas: document.getElementById(animName),
          autoplay: true,
        });
      return heroAnim;
    }

    function startAll() {
      items2Check.forEach((value) => {
        rivePlayers.push(startAnim(value));
      });
    }

    function checkItemsInsideViewport() {
      function check(id) {
        var myElement = document.getElementById(id);
        var offsetY = Number(myElement.getAttribute("offsetY")) | 0;
        var bounding = myElement.getBoundingClientRect();

        var r = (
          bounding.top + offsetY >= 0 &&
          bounding.left >= 0 &&
          bounding.right <= window.innerWidth &&
          bounding.bottom - offsetY <= window.innerHeight
        );

        if (myElement.getAttribute("data-in-viewport") == "true" && !r) {
          myElement.setAttribute("data-in-viewport", "false");
        } else if (myElement.getAttribute("data-in-viewport") == "true" && r) {
          r = false;
        } else if (r) myElement.setAttribute("data-in-viewport", "true");
        return r
      }

      for (let index = 0; index < items2Check.length; index++) {
        if (check(items2Check[index])) {
          if (items2Check[index] == "04_reporteAprobado") {
            rivePlayers[index].reset();
            rivePlayers[index].play();
          } else rivePlayers[index].play("pop up");
        }
      }
    }

    window.onload = function () {
      window.addEventListener('scroll', checkItemsInsideViewport);
      startAll();
      checkItemsInsideViewport();
    }
  </script>
```

**Some hints**: 

The fn **startAll** will iterate and create one riveRuntimeApp for each element inside  *items2Check* List.

The fn **checkItemsInsideViewport** will  check if the animation is in the screen to trigger the PopUp Animation applied. This only works if the animation has "pop up" animation in it.


**For more information**: 

[Wiki](https://help.rive.app/runtimes/overview/web-js)

[GitHub](https://github.com/rive-app/rive-wasm)  
  



### React Integration  
Please read the following instructions

[Wiki](https://help.rive.app/runtimes/overview/react)

[GitHub](https://github.com/rive-app/rive-react)  
  



### Mock Dev Server  
In this repository there is a few index.html with a mocked version of the site with all the animations. To run this server you only need to have *static-server* node app installed globaly:

```npm install static-server -g```

To finally run:

```static-server .``` in this repository :)

Clicking in the page will go forwards in the next mocked page  
  



### Contact and Information  
If you need some help, please contact juanmartin.cerruti@gmail.com or leave some comment in this github project.

Greetings,
Barto
:)   

<br />

----
<div align="center">Generated using <a href="https://profilinator.rishav.dev/" target="_blank">Github Profilinator</a></div>