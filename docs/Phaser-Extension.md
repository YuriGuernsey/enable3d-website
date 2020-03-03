## Using Enable3d as a 3d objects and physics extension for Phaser

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="/lib/three.min.js"></script>
    <script src="/lib/enable3d.phaserGame"></script>
  </head>

  <body>
    <script>
      const { enable3d, Scene3D, Canvas } = ENABLE3D

      class MainScene extends Scene3D {
        constructor() {
          super({ key: 'MainScene' })
        }

        init() {
          this.requestThirdDimension()
        }

        create() {
          this.accessThirdDimension()

          // add a demo scene
          this.third.warpSpeed()

          // add blue box
          this.third.physics.add.box({ y: 2 }, { lambert: { color: 0x2194ce } })
        }
      }

      const config = {
        // use Phaser.WEBGL
        type: Phaser.WEBGL,
        scale: {
          mode: Phaser.Scale.FIT,
          autoCenter: Phaser.Scale.CENTER_BOTH,
          width: window.innerWidth * Math.max(1, window.devicePixelRatio / 2),
          height: window.innerHeight * Math.max(1, window.devicePixelRatio / 2)
        },
        scene: [MainScene],
        // add a custom canvas
        ...Canvas()
      }

      window.addEventListener('load', () => {
        // wrap enable3d around your Phaser game and load ammo from the /lib folder
        enable3d(() => new Phaser.Game(config)).withPhysics('/lib')
      })
    </script>
  </body>
</html>
```
