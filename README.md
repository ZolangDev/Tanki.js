# shizoval

Discord: **солевой#4769**

## Usage

There are two ways to use the cheat:

**1.** [Site with built-in cheat](https://shizoval-site.vercel.app/) (Advantage - no need to install anything)

**2.** Installing the script (Benefit - more stable operation)

## Installation

**1.** Install [Tampermonkey](https://www.tampermonkey.net/)

**2.** Install [script](https://github.com/sheezzmee/shizoval/raw/main/release/shizoval.user.js)

## Keys

`INSERT`, `NumPad 0`, `/` - Open menu

## Customization reads

  In version **0.64.3**, the ability to customize the cheat has been added, namely, full access to the cheat API and all internal functions has been opened.
  
  **Global variables created for you**
  
      I'm too lazy to explain what and how, so your browser console will do it for you
      utils
      gameObjects
      storeOpener
      config
      removeMines
      airBreak
      cameraHack
      menu
      cImGui
      ImGui
      other
      stick
      clicker
      sync
      consoleLog
      wallhack
      filters
      packetControl
      striker
      
  ![](https://github.com/sheezzmee/shizoval/blob/main/img/exampleScript.jpg?raw=true)
 
  A couple of examples (write these scripts into the console or at the end of the script): 
  
```js
/*  SHIZOVAL
*  Code creator: sheezzmee
*  Name: Legit FPS hack
*  Description: Remove mine positions that are the same as others
*  Activation: Digit0
*/
   
const checkMine = mine => {
    if (!mine.removeMine_0)
        return;

    const mines = gameObjects.world.triggers_0.triggers_0.array;
    
    for (const element of mines) {
        if (!element.removeMine_0 || element.id === mine.id)
            continue;
    
        if (element.position.distance_ry1qwf$(mine.position) <= 10)
            element.removeMine_0();
    }
}

document.addEventListener('keyup', (e) => {
    if (utils.isChatOpen() || e.code !== 'Digit0') 
        return;

    const mines = gameObjects.world?.triggers_0?.triggers_0?.array;

    if (!utils.isArrayValid(mines))
        return;

    for (const element of mines)
        checkMine(element);
})
```

```js
/*  SHIZOVAL
*  Code creator: sheezzmee
*  Name: Box Teleport
*  Description: Teleports the tank to bonus crates
*  Activation: B (hold)
*/

requestAnimationFrame(function boxTeleport() {
    requestAnimationFrame(boxTeleport);

    if (!utils.getKeyState('KeyB'))
        return;

    const world = gameObjects.world,
        tank = gameObjects.localTank,
        physics = tank?.['TankPhysicsComponent'];

    if (!world || !physics)
        return;

    const boxes = gameObjects.world?.triggers_0?.triggers_0?.array;

    if (!utils.isArrayValid(boxes))
        return;

    for (const box of boxes) {
        const object3d = box.bonus_0?.bonusMesh?.object3d;

        if (!object3d)
            continue;

        physics.body.state.position.init_ry1qwf$(object3d.aabb.center);
    }
})
```

If you want me to put your script here (authorship will be indicated), then send it to me in ds (there above) 

## Cloning a project

```bash
# Cloning a repository
git clone https://github.com/sheezzmee/shizoval.git
# Go to repository folder
cd shizoval
# Install dependencies
npm i
# Project Compilation
npx gulp
```

## List of changes

* 0.64.3:

      - Cut Features: BoxTeleport, FlagTeleport, DeSync, Box WallHack, Anti-Crash, Gravity, No-Knockback
      
      - Improved AimBot function
      
      - Added Packet Control function (clicker only)
          * allows you to control the state of the server (if there is a large ping, then the speed of the clicker decreases)
          * automatic activation
          
      - Added PPS (Packets Per Second) function
          * displays the number of packets sent to the server (including packets sent by the game itself)
          * automatic activation
      
      - Optimized Sync block
      
      - Improved Rapid Update
          * packets are not sent if the tank state does not change
          * packets are not sent if the tank is dead or not spawned (included in the battle)

      - Disabled sendChassisControl function (sending movement packets)

      - Fixed fps bug

      - Added ConsoleLog function
          * logs messages, kills, exits, self-destructs to the console
    ![](https://github.com/sheezzmee/shizoval/blob/main/img/consoleLog.jpg?raw=true)
       
      - Improved clicker
          * packets are not sent if the tank is dead or not spawned (included in the battle)
          * packets are not sent if the server is not responding
          * changed loop to setInterval (faster operation)
   
      - Added the ability to customize the cheat
        
      - Striker self-destruction unlocked

      - WallHack, Remove mines, Freeze tanks now activate before the local tank spawns

      - Optimized menu (less load)

      - Optimized striker hack

      - Fixed GTA Camera feature

      - Fixed a bug when the camera freezes in one place

      - Improved collision disable function
          * now tanks are completely ignored (previously, the collision of tank turrets was not disabled)
