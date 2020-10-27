# **Phaser 3 Scene change, Basic Physics and Spritesheet animation demo**

## **Code**

```javascript
var GameScene1 = new Phaser.Class({

    Extends: Phaser.Scene,
    initialize:

    function GameScene1 ()
    {
        Phaser.Scene.call(this, { key: 'GameScene1' });
    },

    preload: function ()
    {
        this.load.spritesheet('Girl', 'Girl.png',  {frameWidth: 256, frameHeight:256, endFrame: 12});
        this.load.spritesheet('Boy', 'Boy.png', {frameWidth: 64, frameHeight:64, endFrame: 36});
        this.load.image('Particle', 'Particle.png');
        this.load.image('Ground1', 'Ground1.png');
        this.load.image('Ground2', 'Ground2.jpg');
        this.load.image('Ground3', 'Ground3.jpg');
        this.load.image('PortalL', 'PortalL.png');
        this.load.image('PortalR', 'PortalR.png');
        this.load.image('Anthima', 'Anthima.png');
        this.load.image('Yashit', 'Yashit.png');
        this.load.image('Door', 'Door.png');
        this.load.image('Win', 'Win.png');
    },

    create: function ()
    {
        ground = this.add.sprite(300, 200, 'Ground1');
        ground.setScale(1.5);
        ground = this.add.sprite(300, 680, 'Ground1');
        ground.setScale(1.5);
        cursors = this.input.keyboard.createCursorKeys();

        this.anims.create({
            key: 'right',
            frames: this.anims.generateFrameNumbers('Boy', { start: 8, end: 15 }),
            frameRate: 10,
            repeat: -1
        });

        this.anims.create({
            key: 'left',
            frames: this.anims.generateFrameNumbers('Boy', { start: 24, end: 31 }),
            frameRate: 10,
            repeat: -1
        });

        this.anims.create({
            key: 'down',
            frames: this.anims.generateFrameNumbers('Boy', { start: 0, end: 7 }),
            frameRate: 10,
            repeat: -1
        });

        this.anims.create({
            key: 'up',
            frames: this.anims.generateFrameNumbers('Boy', { start: 16, end: 23 }),
            frameRate: 10,
            repeat: -1
        });

        this.anims.create({
            key: 'pause',
            frames: this.anims.generateFrameNumbers('Boy', { start: 16, end: 16 }),
            frameRate: 10,
            repeat: -1
        });
            
        Boy = this.add.sprite(200, 300, 'Boy');
        door = this.add.sprite(710, 510, 'Door');
        door.setScale(0.5);
        Boy.setScale(1.5);

    },

    update: function(){
        if (cursors.right.isDown)
        {
            if (Boy.x !=790)
            {
                Boy.anims.play('left', true);
                Boy.x += 2;
            }
        } 
        else if (cursors.left.isDown)
        {
            if (Boy.x !=20)
            {
                Boy.anims.play('right', true);
                Boy.x -= 2;
            }
        }
        else if (cursors.up.isDown)
        {
            if (Boy.y !=30)
            {
                Boy.anims.play('down', true);
                Boy.y -= 2;
            }
        }
        else if (cursors.down.isDown)
        {
            if (Boy.y !=570)
            {
                Boy.anims.play('up', true);
                Boy.y += 2;
            }
        }
        else if (Boy.y >= 450 && Boy.x >= 680)
        {
            door.setInteractive({ useHandCursor: true });
            door.setInteractive().on('pointerdown', function() {
                this.scene.scene.start('GameScene2');
                this.scene.scene.pause('GameScene1');
            });
        }
        else
        {
            Boy.anims.play('pause', true);
        }

    }
});

//create a scene with class
var GameScene2 = new Phaser.Class({
    Extends: Phaser.Scene,
    initialize:

    function GameScene ()
    {
        Phaser.Scene.call(this, { key: 'GameScene2' });
    },
    
    create: function ()
    {
        ground1 = this.add.sprite(400, 300, 'Ground2');
        ground1.setScale(1, 1.2);
        cursors = this.input.keyboard.createCursorKeys();

        this.anims.create({
            key: 'rightG',
            frames: this.anims.generateFrameNumbers('Girl', { start: 0, end: 5 }),
            frameRate: 10,
            repeat: -1
        });

        this.anims.create({
            key: 'leftG',
            frames: this.anims.generateFrameNumbers('Girl', { start: 6, end: 10 }),
            frameRate: 10,
            repeat: -1
        });

        this.anims.create({
            key: 'pauseG',
            frames: this.anims.generateFrameNumbers('Girl', { start: 4, end: 4 }),
            frameRate: 10,
            repeat: -1
        });

        
        portalL = this.add.sprite(50, 420, 'PortalL');
        portalL.setScale(0.1);
        portalR = this.add.sprite(750, 420, 'PortalR');
        portalR.setScale(0.1);
        Girl = this.add.sprite(300, 440, 'Girl');
        Girl.setScale(0.5);
    },

    update: function(){
        if (cursors.right.isDown)
        {
            if (Girl.x != 710)
            {
                Girl.anims.play('rightG', true);
                Girl.x += 2;
            }
        } 
        else if (cursors.left.isDown)
        {
            if (Girl.x != 80)
            {
                Girl.anims.play('leftG', true);
                Girl.x -= 2;
            }
        }
        else if (Girl.x <= 100)
        {
            portalL.setInteractive({ useHandCursor: true });
            portalL.setInteractive().on('pointerdown', function() {
                this.scene.scene.start('GameScene3');
                this.scene.scene.pause('GameScene2');
            });
        }
        else if (Girl.x >= 680)
        {
            portalR.setInteractive({ useHandCursor: true });
            portalR.setInteractive().on('pointerdown', function() {
                this.scene.scene.start('GameScene2');
            });
        }
        else
        {
            Girl.anims.play('pauseG', true);
        }

    }
});

var GameScene3 = new Phaser.Class({
    Extends: Phaser.Scene,
    initialize:

    function GameScene ()
    {
        Phaser.Scene.call(this, { key: 'GameScene3' });
    },
    
    create: function ()
    {
        ground2 = this.add.sprite(400, 320, 'Ground3');
        ground2.setScale(0.2);
        var txt5 = this.add.image(400, 100, 'Win');
        txt5.setInteractive({ useHandCursor: true });
        txt5.setInteractive().on('pointerdown', function() {
            this.scene.scene.start('GameScene1');
            this.scene.scene.pause('GameScene3');
        });

        var particles = this.add.particles('Particle');
        var emitter = particles.createEmitter({
            speed: 100,
            scale: { start: 0.05, end: 0 },
            blendMode: 'ADD'
        });

        var particles2 = this.add.particles('Particle');
        var emitter2 = particles2.createEmitter({
            speed: 100,
            scale: { start: 0.05, end: 0 },
            blendMode: 'ADD'
        });
            
        logo1 = this.physics.add.image(100, 100, 'Yashit');
        logo1.setScale(0.3);
        logo1.setVelocity(100, 0);
        logo1.setBounce(1, 1);
        logo1.setGravityY(300);
        logo1.setCollideWorldBounds(true);
        emitter.startFollow(logo1, -60, 30);

        logo2 = this.physics.add.image(500, 200, 'Anthima');
        logo2.setScale(0.3);
        logo2.setVelocity(100, 0);
        logo2.setBounce(1, 1);
        logo2.setGravityY(300);
        logo2.setCollideWorldBounds(true);
        emitter2.startFollow(logo2, 80, 10);
    }
});

//settings required to configure the game
var config = {
    type: Phaser.AUTO,   
    width: 800,
    height:  600,
    physics: {
        default: 'arcade',
        arcade: {
            gravity: 10,
        }
    },
    
    //set background color
    backgroundColor: 0x8080,
    scale: {
        //we place it in the middle of the page.
        autoCenter: Phaser.Scale.CENTER_BOTH
    },

    scene:[GameScene1, GameScene2, GameScene3]
};

var game = new Phaser.Game(config);
```

## What we are trying to do:
* In Phaser we have scene changing functions to help us navigate through our game.
* We are making 3 scenes in total. In 1st  scene we have to reach a door to navigate to the second scene, the 2nd  scene has a completely different Art type and not one but two portals which player should figure out which is the correct door to win the game.
* 3rd scene is radically different from other two scenes as it has physics components and particle effects, it is a Game win scene in a way.

![Image of Scene1](https://github.com/RedMonkWorks/Phaser3/blob/main/1.png)
### Elements in this scene
* Backdrop Image of grass, Door added as sprite and Character added as sprite and animated.
* Boy is animated which we will see further along with how we are changing scenes.
```javascript
Boy = this.add.sprite(200, 300, 'Boy');
door = this.add.sprite(710, 510, 'Door');
ground = this.add.sprite(300, 200, 'Ground1’);
```

![Image of Scene2](https://github.com/RedMonkWorks/Phaser3/blob/main/2.png)
### Elements in this scene
* Girl as a sprite, Backdrop picture as a sprite and two portals with same sprite.
* Girl is animated which we will see further along with how we are changing scenes.
```javascript
Boy = this.add.sprite(200, 300, 'Boy');
door = this.add.sprite(710, 510, 'Door');
ground = this.add.sprite(300, 200, 'Ground1’);
```

![Image of Scene3](https://github.com/RedMonkWorks/Phaser3/blob/main/3.png)
### Physics in this scene
* Code snippet for Particle effect
```javascript
var emitter = particles.createEmitter({
            speed: 100,
            scale: { start: 0.05, end: 0 },
            blendMode: 'ADD'
        });
```
* Code snippet for Bounce, gravity, setBounds and velocity
```javascript
logo1.setVelocity(100, 0);
        logo1.setBounce(1, 1);
        logo1.setGravityY(300);
        logo1.setCollideWorldBounds(true);
```

## Animation
```javascript
this.anims.create({
            key: 'right',
            frames: this.anims.generateFrameNumbers('Boy', { start: 8, end: 15 }),
            frameRate: 10,
            repeat: -1
        });
```
* This is an animation clip we have similar clips for left, up and down animation which we can see in the Rar file attached with work.
* This snippet sets speed of animation with frameRate and which frames are included in clip with frames.
* Usage, we use this snippet to activate the respective clip.
```javascript
if (cursors.left.isDown)
{
    if (Boy.x !=20)
    {
          Boy.anims.play('right', true);
          Boy.x -= 2;
    }
 }
```

## Scene Change
* This snippet takes us to Scene 2 from Scene 1.
```javascript
if (Boy.y >= 450 && Boy.x >= 680)
{
     door.setInteractive({ useHandCursor: true });
     door.setInteractive().on('pointerdown', function() 
     {
                this.scene.scene.start('GameScene2');
                this.scene.scene.pause('GameScene1');
     });
}
```
![RedMonk Logo](https://github.com/RedMonkWorks/Phaser3/blob/main/RedMonk.png)
