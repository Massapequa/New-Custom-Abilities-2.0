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

FlameStrikeTargeted
	Type: (Fire, Ice, Posion, Energy, Water, Steam, Necrotic, Holy) Usage: ability.Type = FlameStrikeTargeted.StrikeType.**Element goes here**
	SetDamage: 12 - 16 by default.


Charge
	SetDamage: 12, 16 by default


FlameStrikeAoe
	Type: (Fire, Ice, Posion, Energy, Water, Steam, Necrotic, Holy) Usage: ability.Type = FlameStrikeAoe.StrikeType.**Element goes here**
	Range: 5 by default
	SetDamage: 12, 18 by default


Firebolt
	Type: (Fire, Ice, Posion, Energy, Water, Steam, Necrotic, Holy) Usage: ability.Type = Firebolt.BoltType.**Element goes here**
	SetDamage: 8, 12 by default


Ambush
	SetDamage: 12, 24 by default


Geyser
	Type: (Fire, Ice, Posion, Energy, Water, Steam, Necrotic, Holy) Usage: ability.Type = Geyser.GeyserType.**Element goes here**
	Message: message that's sent when player is caught in the blast
	SetDamage: 18, 24 by default


IcePrison
	SetDamage: 0 by default


WalkingBomb
	SetDamage: 18, 26 by default


MeteorStrike
	Message: message that's sent when player is struck
	SetDamage: 18, 24 by default


MeteorShower
	SetDamage: 14, 18 by default


Thunderstorm
	SetDamage: 6, 10 by default


ThrowBoulder
	SetDamage: 12, 16 by default


Zap
	SetDamage: 8, 12 by default


ToxicRain
	SetDamage: 9, 18 by default
	Hue: 64 by defult 


ToxicSpores
	SetDamage: 21, 28 by default
	Range: 5 by default.


ImpaleAoe
	Range: 5 by default
	ItemID: change the ItemID of the item that appears on the target. a random stalagmite by default. 
	SetDamage: 12, 18 by default.


FlameStrikeLine
	Type: (Fire, Ice, Posion, Energy, Water, Steam, Necrotic, Holy) Usage: ability.Type = FlameStrikeLine.StrikeType.**Element goes here**
	Range: 5 by default
	SetDamage: 16, 20 by default.


BarrageOfBolts
	ItemID: change the ID of the projectiles.
	Hue: change the hue of the projectiles.
	Sound: fireball sound by default. 
	SetDamage: 12, 18 by default.


FlameStrikeCone
	Type: (Fire, Ice, Posion, Energy, Water, Steam, Necrotic, Holy) Usage: ability.Type = FlameStrikeCone.StrikeType.**Element goes here**
	Range: 5 by default
	SetDamage: 16, 20 by default.


Grapple
	Emote: Message that appears over creature's head as it casts the ability.
	Range: 5 by default.
	SetDamage: 3, 8 by default.


ThrowExplosives
	Hue: change the hue of teh projectile.
	Duration: change the duration of the fire that's left on the ground after impact. 10 seconds by default.
	SetDamage: 10, 20 by default


ThrowTimedExplosives
	Message: message that displays when player is hit by the blast.
	ItemID: ID of the projectile and item that's placed on the ground.
	Sound: when the bomb detonates. 
	SetDamage: 32, 40 by default


HealAllies- *note: in order to make specific creatures healable allies, you must update the casting creature's IsFriend() method.*
	Range: 12 by default
	SetHealing: 10, 18 by default.


FlameBurstAoe
	Range: 5 by default.
	SetDamage: 28, 34 by default.


RagingTempest
	SetDamage: 8, 16 by default.


Blizzard
	SetDamage: 12, 18 by default.

Abilities:
Flame Strike Targeted: Casts a Flame strike on the target. simple and straight forward. has elemental customization options.

Charge: The monster charges at the player from a distance. The range can be altered on this skill.

Flame Strike Aoe: Creates a circle of flame strikes around the monster and damages all players and pets within. Has range and elemental customization.

Firebolt: Fires a simple fireball at the target. Also has elemental customization.

Ambush: Monster vanishes and reappears at the target's location to deliver a damaging attack.

Geyser: A swirling pool is created beneath the player, and after a short duration, a large geyser erupts from that spot. If the player moves out of the way in time, they can avoid the blast. This has elemental customization options.

Ice Prison: The target is trapped in a block of ice for a short duration. The hue and item id of the prison can be changed.

Walking Bomb: A target is marked for a short duration before an explosion erupts on top of them. Any nearby player is damaged by the blast as well.

Meteor Strike: A shadow appears over a target player, and after a short duration a meteor comes crashing down and damages anyone standing in that location. If the player moves out of the way in time, they can avoid the damage.

Meteor Shower: The enemy calls down a flurry of meteors at random locations nearby the target.

Thunderstorm: All nearly targets are stuck by lightning.

Throw Boulder: The creature throws a large boulder at a target location. Any player that is caught in the area is hit and knocked down for a short duration.

Zap: Sends out a bolt of electricity that temporarily paralyses the target

Toxic Rain: The target is doused in toxic rain for a short duration, leaving pools of acid wherever they step.

Toxic Spores: Creates a circle of exploding mushrooms around the target, damaging anyone in the area and leaving pools of acid in the area that damage anyone who dares to step in it.

Impale Aoe: Stalagmites erupt from the ground and pierce anyone in the area. Anyone caught in the aoe will start bleeding. The hue item ID of the stalagmites can be changed to anything you want.

Custom Abilities 2.0:

New Abilities:
Flame Strike Line - Sends out cascading flames in a direct line toward the target. All enemies in the way get damaged.

Barrage Of Bolts - sends a flurry of firebolts at a target. Any enemy caught in the location gets damaged.

Flame Strike Cone - Creates a massive cone of fire in front of the creature that damages all nearby enemies.

Grapple - The creature pulls the target towards them.

Throw Explosives - The creature throws a small explosive that hits teh target and leaves a small fire behind.

Throw Timed Explosives - The creature throws an explosive barrel at the target that detonates after a short time and damages all nearby targets.

Heal Allies - Heals nearby allies.

Flame Burst Aoe - Creates a large area of effect blast at the creature's location and leaves behind flames in the blast zone.

Raging Tempest - Creates a prolonged thunderstorm in an area by the target.

Blizzard - Creates a massive storm at the creature's location.

Edits / Fixes:

	Toxic Rain: Tamed creatures will now use this on enemy creatures and the acid pools will no longer damage players when it's used by tamed creatures.
	Walking Bomb: Has more pronounced visual explosion and leaves flames on the gound in the area.
	Thunderstorm: No longer strikes allies. Non-tamed creatures using this ability will only strike players and pets, while tamed creatures will strike enemy NPCs.
	Meteor Shower: increased the default frequency that the meteors fall.
	Meteor Strike / Meteor Shower: Meteors now deal damage in a 2 tile range when they strike. (Updated from having to be direct on top of them).
	


Mobiles and their abilities:

	Rebel Paladin: Charge, Flame Strike Aoe(holy)
	Rebel Archer: Barrage of Bolts(arrrow ItemID)
	Rebel Priest: Flame Strike Targeted(holy), Firebolt(holy), Heal Allies
	Rebel Alchemist: Throw Timed Explosives (Explosion potion ItemID), Flame Burst Aoe

	Brigand Pillager: Throw Explosives, Throw Timed Explosives
	Brigand Cutthroat: Ambush, Barrage of Bolts
	Brigand Occultist: Walking Bomb, Toxic Rain, Heal Allies

	Ice Imp: Firebolt(ice), Ice Prison
	Fire Imp: Meteor Strike, Firebolt
	Shadow Imp: Firebolt(necrotic), Toxic Rain

	Swamp Hag:Toxic Spores, Flame Strike Aoe(poison), Flame Strike Targeted(poison)
	Sea Hag: Geyser, FlameStrike Aoe(water), Barrage of Bolts(water hued)
	Winter Hag: Blizzard, Flame Strike Aoe(ice), Geyser(steam)

	Reef Drake: Flame Strike Line(water)
	Reef Dragon: Flame Strike Cone(water)
	Shadow Drake: Flame Strike Line(necrotic)
	Shadow Dragon: Flame Strike Cone(necrotic)

	Blighted Vine: Grapple, Geyser(poison), Firebolt(poison)
	Mountain Troll: Throw boulder, Grapple

	Gem Elemental: Throw Boulder, Impale Aoe, Barrage of Bolts(ore ItemID)
	Lightning Elemental: Thunderstorm, Zap, Raging Tempest
	Firestorm: Flame Burst Aoe, Meteor Shower, Barrage of Bolts

	

