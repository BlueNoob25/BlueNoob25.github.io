# The Shield Mod github page!

## Code for the mod (if you are too lazy to go to the official page)
### World Code

```js
//These are all the main variables used. Change them however you like! :D//
var shieldItem = "Pine Door";
var minHearts = 100;
var effectName = "critical_hit";
var shieldProt = 15;
var knockbackResLvl = 15;

// Shield function and node attachments
function tick() {
  for (let playerId of api.getPlayerIds()) {
    let hearts = api.getHealth(playerId);
    let heldItem = api.getHeldItem(playerId);
    
      if (api.getHealth(playerId)) {
      if (heldItem && heldItem.name === shieldItem) {
      if (hearts < minHearts) {
        api.setShieldAmount(playerId, shieldProt);
        api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0.7, meshOffset: [0, 0, 0] },[0.3, 0.3, 0.3], [0, 3.1, 0]);
    } else {
            api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0.7, meshOffset: [0, 0, 0] },[0.5, 0.2, 0], [0, 1.5, 0]);
      }
            api.setShieldAmount(playerId, 0);
    } else {
          api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0, meshOffset: [0, 0, 0] },[0, 0, 0], [0, 0, 0]);
      }
    }
  }
}

// Particle effect settings
function particle(x, y, z){
        y += 1
        api.playParticleEffect({
          dir1: [-1, -1, -1],
          dir2: [1, 1, 1],
          pos1: [x, y, z],
          pos2: [x + 1, y + 1, z + 1],
          texture: effectName,
          minLifeTime: 0.2,
          maxLifeTime: 0.6,
          minEmitPower: 2,
          maxEmitPower: 2,
          minSize: 0.25,
          maxSize: 0.35,
          manualEmitCount: 5,
          gravity: [0, -10, 0],
          colorGradients: [
           {
               timeFraction: 0,
               minColor: [60, 60, 150, 1],
               maxColor: [200, 200, 255, 1],
           },
          ],
          velocityGradients: [
           {
               timeFraction: 0,
               factor: 1,
               factor2: 1,
           },
          ],
          blendMode: 1,
})
}

// Effects code
onPlayerDamagingOtherPlayer = (attacker, victim, dmg, weaponName) => {

    let hearts = api.getHealth(victim);
    let heldItem = api.getHeldItem(victim);

      if (heldItem && heldItem.name === shieldItem) {
      if (hearts < minHearts + 1) {
        api.applyEffect(victim, "Slowness", 100, {inbuiltLevel:knockbackResLvl})
        let [x, y, z] = api.getPosition(victim);
        particle(x, y, z);
    }
  }
}

onMobDamagingPlayer = (attacker, victim, dmg, weaponName) => {

    let hearts = api.getHealth(victim);
    let heldItem = api.getHeldItem(victim);

      if (heldItem && heldItem.name === shieldItem) {
      if (hearts < minHearts + 1) {
        api.applyEffect(victim, "Slowness", 100, {inbuiltLevel:knockbackResLvl})
        let [x, y, z] = api.getPosition(victim);
        particle(x, y, z);
    }
  }
}
```

### Code Block code

```js
api.giveItem(myId, shieldItem, 1, {
   customDisplayName: "Simple Shield", customDescription: "Hold me to protect yourself :D"
   }
)
```

How the updates work:

   Every update here is what I have put into the code since the last version listed. So, if, hypothetically, I were to make the shield real large (which I have not done and I don’t plan to do so) and then update the code to include the larger shield, that would be an update, maybe not on its own, since it wasn’t too big of a change, and then the very next time I worked on the mod I were to add something else, then input the new code, that would (maybe idk) be a separate update listed than the one that made the shield larger.

   The first decimal point is the bigger, 'Parent' update. It might’ve set the stage for some of the smaller updates that go next.

   The second decimal point is for the updates that follow that introduce stuff similar to the features the Parent updates introduced. “Smaller updates" isn’t a good name to call it, however, because the update might introduce more features than the parent update. Anyways, since if the small updates don’t introduce anything similar to the update(s) before, it technically stands out by itself, so it's an independent update that only has the first decimal point.


Developer Changelog:

v1.0: the mod only gave the protection when it was first created. There were no cool visuals, nothing but the protection, which was the main part. Also there was no need for any excess organization since the code at the time was small enough that you could see everything all at once and it was easy to spot the things to change/customize.

v1.1: added a cool shield visual when activated. The player’s shield will cover their body when used. Also new screenshots that visually describe the shield better than the old ones!

v1.1.1: added different shield visuals depending on the state of the player. When the player is at or over the minimum required health limit the shield will be put down, and also the shield visuals will be turned off completely now when none of the requirements are met, so no more shield covering your body for literally your whole gaming session just because of that one pvp battle!

v1.2: made customization improvements; instead of finding every instance of 'Pine Door' to change you can just change the "shieldItem" variable directly! Having trouble looking for the spot to change shield protection? Now just go change the "shieldProt" variable! It is also even easier to change the required maximum health limit with the easily-accessible “maxHearts” variable! ;D


Team: (1 Staff member, not hiring)

(Creator) Ethan Jamison
Social Media: @BlueNoob - Bloxdhub.com, Thegreatestgamer_ev - Bloxd.io, u/ZestyClose_Job_5735 - Reddit.com


Licensing:
Licensing info can be found on the link: https://bloxdhub.com/mod/439
It should be CC by 4.0 or similar licenses.

By using the mod, you agree to the licensing information and understand we have the ability to  report you on bloxdhub.com if found using the mod without credit.



# Breakdown
Understanding the mod can allow one to mold the mod into whatever they wish!

## Setting the variables
```
var shieldItem = "Pine Door";
var minHearts = 100;
var effectName = "critical_hit";
var shieldProt = 15;
var knockbackResLvl = 15;
```
These variables control the main parts of the shield. Like the code offers, you may change them to however you like!
These variables are very straightfoward, and they are there for convenience. They were added back in v1.2 to avoid confusion and make customizing the mod much less time-wasting.

For example:

Change the shield to absorb 55 hp and activate when hp is below 30:
```
var minHearts = 30;
---
var shieldProt = 55;
```
Change the shield to become a maple door and let the attack particles become bubble particles:
```
var shieldItem = "Maple Door";
---
var effectName = "bubble";
```

## The Function and Node Attachments
```
function tick() {
  for (let playerId of api.getPlayerIds()) {
    let hearts = api.getHealth(playerId);
    let heldItem = api.getHeldItem(playerId);
    
      if (api.getHealth(playerId)) {
      if (heldItem && heldItem.name === shieldItem) {
      if (hearts < minHearts) {
        api.setShieldAmount(playerId, shieldProt);
        api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0.7, meshOffset: [0, 0, 0] },[0.3, 0.3, 0.3], [0, 3.1, 0]);
    } else {
            api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0.7, meshOffset: [0, 0, 0] },[0.5, 0.2, 0], [0, 1.5, 0]);
      }
            api.setShieldAmount(playerId, 0);
    } else {
          api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0, meshOffset: [0, 0, 0] },[0, 0, 0], [0, 0, 0]);
      }
    }
  }
}
```
This is the main part of the shield, controlling the main function of the shield, the protection, along with the mesh nde attachments. As you can see, it all happens in a tick, which is how the game checks and activates the shield when nessesary. 


```
let hearts = api.getHealth(playerId);
let heldItem = api.getHeldItem(playerId);
```
These variables may NOT be touched, they check the item and hp of the player, which can be inferred by their names.

```
if (api.getHealth(playerId)) {
      if (heldItem && heldItem.name === shieldItem) {
      if (hearts < minHearts) {
```
These are the "if" statements, which determines the state of the shield and whether it should be active or not. It is up to you to change the comparison and requirements, however note that the statements are dependent on the variables discussed, so you may want to consider changing those variables when changing the comparison.

```
api.setShieldAmount(playerId, shieldProt);
```
This sets the protection, once EVERY statement has been fulfilled. What follows is the visual attachments:
```
            api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0.7, meshOffset: [0, 0, 0] },[0.3, 0.3, 0.3], [0, 3.1, 0]);
    } else {
            api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0.7, meshOffset: [0, 0, 0] },[0.5, 0.2, 0], [0, 1.5, 0]);
      }
            api.setShieldAmount(playerId, 0);
    } else {
          api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 0, meshOffset: [0, 0, 0] },[0, 0, 0], [0, 0, 0]);
```
You may edit the way the visuals are presented. For example:

Change the "active" state to have an enormous shield:
```
api.updateEntityNodeMeshAttachment(playerId, "TorsoNode", "BloxdBlock",{ blockName: shieldItem, size: 1.0, meshOffset: [0, 0, 0] },[1, 1, 1], [0, 3.1, 0]);
```

## Particle Effect Settings
```
function particle(x, y, z){
        y += 1
        api.playParticleEffect({
          dir1: [-1, -1, -1],
          dir2: [1, 1, 1],
          pos1: [x, y, z],
          pos2: [x + 1, y + 1, z + 1],
          texture: effectName,
          minLifeTime: 0.2,
          maxLifeTime: 0.6,
          minEmitPower: 2,
          maxEmitPower: 2,
          minSize: 0.25,
          maxSize: 0.35,
          manualEmitCount: 5,
          gravity: [0, -10, 0],
          colorGradients: [
           {
               timeFraction: 0,
               minColor: [60, 60, 150, 1],
               maxColor: [200, 200, 255, 1],
           },
          ],
          velocityGradients: [
           {
               timeFraction: 0,
               factor: 1,
               factor2: 1,
           },
          ],
          blendMode: 1,
})
}
```
This is a custom function that plays the particle effect according to the settings. While the main setting, the effect texture, can easily be changed at the top, The other settings, which the player may want to also change depending on their view of the current default settings.

Examples:

Change the amount of particles that play at a time:
```
manualEmitCount: 20,
```

Change the range of time it takes for the particles to play:
```
minLifeTime: 0.1,
maxLifeTime: 1.0,
```

Change the range of size of the particles, with the amount of gravitational force being applied:
```
minSize: 0.05,
maxSize: 0.05,
---
gravity: [0, -15, 0],
```

## Playing the effects
NOTE: The following script appears TWICE in the code, so any changes to either copy should be applied to the other copy, unless you want it different depending on what's damaging the player

```
    let hearts = api.getHealth(victim);
    let heldItem = api.getHeldItem(victim);

      if (heldItem && heldItem.name === shieldItem) {
      if (hearts < minHearts + 1) {
        api.applyEffect(victim, "Slowness", 100, {inbuiltLevel:knockbackResLvl})
        let [x, y, z] = api.getPosition(victim);
        particle(x, y, z);
    }
  }
}
```

AGAIN, the variables here may NOT be changed!

The "if" statements:
```
if (heldItem && heldItem.name === shieldItem) {
if (hearts < minHearts + 1) {
```

The first statement determines if the player is holding the correct item. The second determines whether the hp reaches the requirements for the shield to activate (do not question or change the "+ 1", by changing it you are essentially changing the limit of the minimum hp required without changing the ```"minhearts"``` variable, which may become tricky to find and change back, even harder because the code is repeated.)

```
api.applyEffect(victim, "Slowness", 100, {inbuiltLevel:knockbackResLvl})
```
This handles the knockback, and you may change the settings, but it is not recomended to change the effect being applied, unless you want the player to actually get knocked back harder if changed to speed, or unless you want the player to get poisoned when hit. I really wouldn't care actually if you changed the effect to something obscure as I'm sure that would make the gameplay VERY interesting... :) Best to just change the amount of time the effect lasts, maybe to control and help figure out the slowness, but really the main thing to change is the ```knockbackResLvl``` variable, which basically explains itself.

```
let [x, y, z] = api.getPosition(victim);
particle(x, y, z);
```

This runs the particle effects from earlier. DO NOT CHANGE THESE LINES, ANY CHANGES TO THE PARTICLES GO TO THE FUNCTION CODE FROM EARLIER.

Why are these lines of code being repeated? Well, It can be found under the ```onPlayerDamagingOtherPlayer``` and ```onMobDamagingPlayer``` callbacks, which happens when a player attacks another player, or when a mod attacks another player. While it is recommended to apply any changes from one copy to the other, if you really want to make changes depending on what is attacking the player you may.


Finally,
# The Code Block Code Breakdown
```
api.giveItem(myId, shieldItem, 1, {
   customDisplayName: "Simple Shield", customDescription: "Hold me to protect yourself :D"
   }
)
```
This is the code that gives the shield along with a custom name and description. You may change the name and description, and it will not affect any of the code.

Examples:

```
customDisplayName: "The greatest shield you'll ever use", customDescription: "I will protect you no matter the cost..."
```
```
customDisplayName: "Weak Shield", customDescription: "A tattered shield, worn out and used by many peasants before you."
```

I call this one, "Unoriginal"
```
customDisplayName: "Name", customDescription: "Description"
```



And thats the explanation for all the code, working for version v1.5! Have fun with this cool weapon :3
