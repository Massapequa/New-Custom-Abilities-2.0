# New-Custom-Abilities-2.0
Custom Abilities for creatures in the ServUO Ultima Online emulator
//
Massapequa's Custom Abilities:
This is an attempt to make fun and cool custom abilities that are (relatively) easy
for others to implement into their server. Many of these abilities have modifiers that
allow you to change how they look for each mob that uses it. Each ability shows an example
of how it can be used within the code for the ability itself. In Addition, this comes with 
custom mobiles as examples to help you see how they work.


Also, be aware that all of these abilities are being tested on **ServUO-57.1**
At the time of writing this, there is a newer version released and these abilities should, for the most part, work with it.
However, if there are any conflicts with your version, feel free to post on the thread or direct message me on the ServUO forums.
I'd be happy to try and help with any issues you might be having. I want nothing more than for those reading this to have fun with the wrok I've created.
We've already solved a number of issues on the thread that people have had with 1.0, and maybe the solution to your issue is already there.

If you find anything you think may be a bug, feel free to post that as well and I'll be eager to fix it.
Anyway, on with the rest of the directions.


Single abilities can be called through: 	CustomAbility.CheckTrigger(caster, ability)
which should be placed in the OnThink Method.
Don't forget to add base.OnThink(); in your override method so the mod retains its inherited AI.
Example:

	BarrageOfBolts bob = new BarrageOfBolts();

	public override void OnThink()
	{
	    base.OnThink();

	    CustomAbility.CheckTrigger(this, bob);
	}

You can also use the CustomAbilityList if your creature is using multiple abilities at a time.

if you're using the CustomAbilityList, you have to add each ability to the list. 
The code could look something like this:

AbilityOne one = new AbilityOne();
AbilityTwo two = New AbilityTwo();
//where ability one and teo are any custom abilities you want to add//

CusstomAbilityList list;

	public override void OnThink()
	{
	    base.OnThink();

	    if( list == null)
	    {
 		list = new CustomAbilityList();
		list.Add(one);
		list.Add(two);
	    }
	    else
		list.CheckTrigger(this);
	}

The reason for placing this in the OnThink method is to make sure that the abilities are aviable any time the mob is in combat.
If the abilities are added in the constructor, the mobs won't use the abilities after the server has been restarted.

Here is a list of all of the abilities and their customizable attributes:

## Ability Attributes
<details>
<summary>
Click to reveal list of all of the abilities and their customizable attributes:
</summary>

### FlameStrikeTargeted
- **Type**: (Fire, Ice, Poison, Energy, Water, Steam, Necrotic, Holy)
- **Usage**: `ability.Type = FlameStrikeTargeted.StrikeType.` *Element goes here*
- **SetDamage**: 12 - 16 by default.

### Charge
- **SetDamage**: 12, 16 by default.

### FlameStrikeAoe
- **Type**: (Fire, Ice, Poison, Energy, Water, Steam, Necrotic, Holy)
- **Usage**: `ability.Type = FlameStrikeAoe.StrikeType.` *Element goes here*
- **Range**: 5 by default.
- **SetDamage**: 12, 18 by default.

### Firebolt
- **Type**: (Fire, Ice, Poison, Energy, Water, Steam, Necrotic, Holy)
- **Usage**: `ability.Type = Firebolt.BoltType.` *Element goes here*
- **SetDamage**: 8, 12 by default.

### Ambush
- **SetDamage**: 12, 24 by default.

### Geyser
- **Type**: (Fire, Ice, Poison, Energy, Water, Steam, Necrotic, Holy)
- **Usage**: `ability.Type = Geyser.GeyserType.` *Element goes here*
- **Message**: Message that's sent when a player is caught in the blast.
- **SetDamage**: 18, 24 by default.

### IcePrison
- **SetDamage**: 0 by default.

### WalkingBomb
- **SetDamage**: 18, 26 by default.

### MeteorStrike
- **Message**: Message that's sent when a player is struck.
- **SetDamage**: 18, 24 by default.

### MeteorShower
- **SetDamage**: 14, 18 by default.

### Thunderstorm
- **SetDamage**: 6, 10 by default.

### ThrowBoulder
- **SetDamage**: 12, 16 by default.

### Zap
- **SetDamage**: 8, 12 by default.

### ToxicRain
- **SetDamage**: 9, 18 by default.
- **Hue**: 64 by default.

### ToxicSpores
- **SetDamage**: 21, 28 by default.
- **Range**: 5 by default.

### ImpaleAoe
- **Range**: 5 by default.
- **ItemID**: Change the ItemID of the item that appears on the target. (A random stalagmite by default.)
- **SetDamage**: 12, 18 by default.

### FlameStrikeLine
- **Type**: (Fire, Ice, Poison, Energy, Water, Steam, Necrotic, Holy)
- **Usage**: `ability.Type = FlameStrikeLine.StrikeType.` *Element goes here*
- **Range**: 5 by default.
- **SetDamage**: 16, 20 by default.

### BarrageOfBolts
- **ItemID**: Change the ID of the projectiles.
- **Hue**: Change the hue of the projectiles.
- **Sound**: Fireball sound by default.
- **SetDamage**: 12, 18 by default.

### FlameStrikeCone
- **Type**: (Fire, Ice, Poison, Energy, Water, Steam, Necrotic, Holy)
- **Usage**: `ability.Type = FlameStrikeCone.StrikeType.` *Element goes here*
- **Range**: 5 by default.
- **SetDamage**: 16, 20 by default.

### Grapple
- **Emote**: Message that appears over the creature's head as it casts the ability.
- **Range**: 5 by default.
- **SetDamage**: 3, 8 by default.

### ThrowExplosives
- **Hue**: Change the hue of the projectile.
- **Duration**: Change the duration of the fire left on the ground after impact. (10 seconds by default.)
- **SetDamage**: 10, 20 by default.

### ThrowTimedExplosives
- **Message**: Message that displays when a player is hit by the blast.
- **ItemID**: ID of the projectile and item placed on the ground.
- **Sound**: Sound when the bomb detonates.
- **SetDamage**: 32, 40 by default.

### HealAllies
- *Note*: In order to make specific creatures healable allies, you must update the casting creature's IsFriend() method.
- **Range**: 12 by default.
- **SetHealing**: 10, 18 by default.

### FlameBurstAoe
- **Range**: 5 by default.
- **SetDamage**: 28, 34 by default.

### RagingTempest
- **SetDamage**: 8, 16 by default.

### Blizzard
- **SetDamage**: 12, 18 by default.

</details>


## Abilities

### Flame Strike Targeted
- **Description**: Casts a Flame strike on the target, with elemental customization options.

### Charge
- **Description**: The monster charges at the player from a distance, with customizable range.

### Flame Strike Aoe
- **Description**: Creates a circle of flame strikes around the monster, damaging all players and pets within. Customizable range and elemental effects.

### Firebolt
- **Description**: Fires a simple fireball at the target, with elemental customization.

### Ambush
- **Description**: Monster vanishes and reappears at the target's location to deliver a damaging attack.

### Geyser
- **Description**: Creates a swirling pool beneath the player, followed by a large geyser eruption. Players can avoid the blast by moving. Customizable elemental effects.

### Ice Prison
- **Description**: Traps the target in a block of ice for a short duration, with options to customize the hue and item ID.

### Walking Bomb
- **Description**: Marks a target before an explosion erupts, damaging nearby players. 

### Meteor Strike
- **Description**: Summons a shadow over a target player, followed by a crashing meteor. Players can avoid the damage by moving in time.

### Meteor Shower
- **Description**: Calls down a flurry of meteors at random locations near the target.

### Thunderstorm
- **Description**: Strikes all nearby targets with lightning.

### Throw Boulder
- **Description**: The creature hurls a large boulder at a target location, hitting and briefly knocking down any player in the area.

### Zap
- **Description**: Sends out a bolt of electricity that temporarily paralyzes the target.

### Toxic Rain
- **Description**: Douses the target in toxic rain, leaving pools of acid in their wake.

### Toxic Spores
- **Description**: Creates a circle of exploding mushrooms around the target, damaging anyone in the area and leaving pools of acid.

### Impale Aoe
- **Description**: Causes stalagmites to erupt from the ground, piercing anyone in the area and inflicting bleeding. Customize the hue and item ID of the stalagmites.



##Custom Abilities 2.0:

###New Abilities:

| Ability                | Description                                                                     |
|------------------------|---------------------------------------------------------------------------------|
| Flame Strike Line      | Sends out cascading flames in a direct line toward the target. All enemies in the way get damaged. |
| Barrage Of Bolts       | Sends a flurry of firebolts at a target. Any enemy caught in the location gets damaged. |
| Flame Strike Cone      | Creates a massive cone of fire in front of the creature that damages all nearby enemies. |
| Grapple                | The creature pulls the target towards them.                                  |
| Throw Explosives       | The creature throws a small explosive that hits the target and leaves a small fire behind. |
| Throw Timed Explosives | The creature throws an explosive barrel at the target that detonates after a short time and damages all nearby targets. |
| Heal Allies            | Heals nearby allies.                                                           |
| Flame Burst Aoe        | Creates a large area of effect blast at the creature's location and leaves behind flames in the blast zone. |
| Raging Tempest         | Creates a prolonged thunderstorm in an area by the target.                   |
| Blizzard               | Creates a massive storm at the creature's location.                          |

### Mobiles and their abilities

| Mobile                  | Abilities                                              |
|-------------------------|-------------------------------------------------------|
| Rebel Paladin           | Charge, Flame Strike Aoe (holy)                       |
| Rebel Archer            | Barrage of Bolts (arrow ItemID)                       |
| Rebel Priest            | Flame Strike Targeted (holy), Firebolt (holy), Heal Allies |
| Rebel Alchemist         | Throw Timed Explosives (Explosion potion ItemID), Flame Burst Aoe |
| Brigand Pillager        | Throw Explosives, Throw Timed Explosives              |
| Brigand Cutthroat       | Ambush, Barrage of Bolts                               |
| Brigand Occultist       | Walking Bomb, Toxic Rain, Heal Allies                  |
| Ice Imp                 | Firebolt (ice), Ice Prison                             |
| Fire Imp                | Meteor Strike, Firebolt                                |
| Shadow Imp              | Firebolt (necrotic), Toxic Rain                       |
| Swamp Hag               | Toxic Spores, Flame Strike Aoe (poison), Flame Strike Targeted (poison) |
| Sea Hag                 | Geyser, Flame Strike Aoe (water), Barrage of Bolts (water hued) |
| Winter Hag              | Blizzard, Flame Strike Aoe (ice), Geyser (steam)       |
| Reef Drake              | Flame Strike Line (water)                             |
| Reef Dragon             | Flame Strike Cone (water)                             |
| Shadow Drake            | Flame Strike Line (necrotic)                         |
| Shadow Dragon           | Flame Strike Cone (necrotic)                         |
| Blighted Vine           | Grapple, Geyser (poison), Firebolt (poison)           |
| Mountain Troll          | Throw boulder, Grapple                                 |
| Gem Elemental           | Throw Boulder, Impale Aoe, Barrage of Bolts (ore ItemID) |
| Lightning Elemental     | Thunderstorm, Zap, Raging Tempest                    |
| Firestorm               | Flame Burst Aoe, Meteor Shower, Barrage of Bolts      |
	
###Edits / Fixes:

	Toxic Rain: Tamed creatures will now use this on enemy creatures and the acid pools will no longer damage players when it's used by tamed creatures.
	Walking Bomb: Has more pronounced visual explosion and leaves flames on the gound in the area.
	Thunderstorm: No longer strikes allies. Non-tamed creatures using this ability will only strike players and pets, while tamed creatures will strike enemy NPCs.
	Meteor Shower: increased the default frequency that the meteors fall.
	Meteor Strike / Meteor Shower: Meteors now deal damage in a 2 tile range when they strike. (Updated from having to be direct on top of them).
	




