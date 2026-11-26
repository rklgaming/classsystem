# The classes

[Back to the overview](../README.md)

Ten spells per class on slots `1`-`0` (slot 10 = key `0`), plus a quick ability on `G` for sixteen classes (all but the God, Demon, Merfolk and Werewolf; `B` before class core 3.2.9). Every class has
a passive that is always on, its own mana and ten ranks. The God and the Priest heal; every other class keeps only the HP it
gains by attacking.

| Class | Resource | `/setclass` name | Mana | Passive |
|---|---|---|---|---|
| [God](#god) | `rklgods` | `god` | Grace | Throne of Heaven |
| [Demon](#demon) | `rkldemon` | `demon` | Brimstone | Soul Pact |
| [Merfolk](#merfolk) | `rklmerfolk` | `merfolk` | Scales | Tidebound |
| [Vampire](#vampire) | `rklvampire` | `vampire` | Vitae | Nocturne |
| [Werewolf](#werewolf) | `rklwerewolf` | `werewolf` | Rage | Lunar Blood |
| [Fairy](#fairy) | `rklfairyspells` | `fairy` | Glamour | Bloomheart |
| [Witch](#witch) | `rklwitchspells` | `witch` | Malice | Hexweaver |
| [Elf](#elf) | `rklelf` | `elf` | Aether | Elemental Resonance |
| [Archer](#archer) | `rklarcher` | `archer` | Focus | Marksman's Rhythm |
| [Kitsune](#kitsune) | `rklkitsune` | `kitsune` | Spirit | Fox Trickery |
| [Priest](#priest) | `rklpriest` | `priest` | Faith | Afterglow |
| [Assassin](#assassin) | `rklassassin` | `assassin` | Cunning | Nightshade Edge |
| [Knight](#knight) | `rklknight` | `knight` | Valor | Steadfast Wall |
| [Oni](#oni) | `rkloni` | `oni` | Wrath | Bleeding Fury |
| [Samurai](#samurai) | `rklsamurai` | `samurai` | Resolve | Iai |
| [Shaman](#shaman) | `rklshaman` | `shaman` | Ancestry | Ancestral Chorus |
| [Alchemist](#alchemist) | `rklalchemist` | `alchemist` | Catalyst | Volatile Hands |
| [Dragonkin](#dragonkin) | `rkldragonkin` | `dragonkin` | Hoard | Dragon Scales |
| [Necromancer](#necromancer) | `rklnecromancer` | `necromancer` | Marrow | Grave Tithe |
| [Chronomancer](#chronomancer) | `rklchronomancer` | `chronomancer` | Sand | Tempo |

---

## God

*Throne of Heaven* · healer, guardian, ranged · holy and lightning. Every spell is a verdict that falls from the sky
onto the spot you marked, announced a heartbeat before it lands.

**Passive · Throne of Heaven**: stand still 1.5 s and a celestial throne rises under you: Grace flows back, you take
20 % less damage, and spells cast from the throne hit 15 % harder and reach 10 m further. One step breaks it.

| Slot | Spell | In short |
|---|---|---|
| 1 | Heaven's Verdict | a lance of light falls on your mark |
| 2 | Benediction | heals and blesses everyone inside (+15 % spell power, less spell damage taken) |
| 3 | Thunder of Olympus | a storm cloud, then bolts strike inside an 8 m circle |
| 4 | Heavenfall | burst up, hang as a star, dive like a comet onto your mark |
| 5 | Aegis of the Pantheon | three orbiting shields that swallow hits; `E` hurls one; ally shields |
| 6 | Blinding Radiance | a small sun detonates: whoever looks at it is blinded |
| 7 | Crown of Blades | six blades crown you; plant them and make them erupt |
| 8 | Hammer of the Heavens | a giant hammer crashes down with a knockdown shockwave |
| 9 | Rapture | a holy star on the ground lifts everyone still inside |
| 10 | Eye of Heaven | ultimate: a pillar of sunlight that follows your crosshair |

## Demon

*Bound by the Soul Pact* · burst, zone, ranged · hellfire, fire and shadow. It brands, binds and burns, takes your soul,
then spends that soul on something worse.

**Passive · Soul Pact**: spell hits tear souls out of enemies (up to 5, a ring of soul flames on the shoulders).
The demon is fire-proof and gains Brimstone standing in hellfire. Optional holy weapons and holy zones hurt it.

| Slot | Spell | In short |
|---|---|---|
| 1 | Twin Hellflame | two braided flames detonate where you aimed |
| 2 | Hellwhip | a whip of hellfire: three lashes, the third cracks and explodes |
| 3 | Infernal Leap | a comet arc to your mark that throws everyone back |
| 4 | Abyssal Ray | a soul-fire beam that ruptures into ground spears; souls make it stronger |
| 5 | Ring of Brimstone | a ring of fire that follows you: less damage, burns whoever crosses |
| 6 | Soul Covenant | spends souls on a soul ward, spell power and lifesteal for you and allies |
| 7 | Binding Pentagram | a pentagram rises; whoever is still inside is rooted and silenced |
| 8 | Doomfall | a giant skull drops a burning meteor |
| 9 | Abyssal Maw | a rift pulls everyone in, then erupts into a hellfire tornado |
| 10 | Ascension of the Demon Lord | ultimate: become the 3.5 m Demon Lord for 30 s (`E` fire breath, `G` stomp) |

## Merfolk

*Children of the Deep* · control, ranged, zone · water and ice. Every spell first draws a tide in, then lets it crash
back out.

**Passive · Tidebound**: hydration 0-100. Wet (water, rain, own spells): swim faster, never drown, mana recharges,
half-cost spells under water. Parched: slower, double cost.

| Slot | Spell | In short |
|---|---|---|
| 1 | Trident of the Deep | a water trident you hurl and recall |
| 2 | Abyssal Torrent | a high-pressure jet that follows where you look |
| 3 | Rimefang Wake | ice fangs crawl to the mark, then a crown of crystals bursts up (chill) |
| 4 | Abyssal Dive | dive into the ground and swim to the mark, then breach |
| 5 | Tidepearl Aegis | a pearl halo: cleanses and wards everyone around you |
| 6 | Maelstrom | a whirlpool drags everyone in, then erupts into a waterspout |
| 7 | Glacial Bulwark | a curved wall of ice and frost shields; shatter it into shards |
| 8 | Siren's Lament | a song that charms everyone in the cone |
| 9 | Kraken's Grasp | a kraken seizes everyone in the circle and slams them down |
| 10 | Leviathan Breach | ultimate: a spectral leviathan bursts out and crashes down |

## Vampire

*Nobility of the Night* · assassin, drain, melee · blood and shadow. A predator that drinks from what it hits.

**Passive · Nocturne**: by day in open sunlight the vampire smokes, then burns (cover, water, vehicles and shade
protect). By night spells hit harder, Vitae regenerates faster and Shadow Dash recovers sooner. Bloodlust heals the
vampire from the damage its spells really dealt.

| Slot | Spell | In short |
|---|---|---|
| G | Shadow Dash | turn to smoke and reappear up to 18 m away |
| 1 | Throw Spear | a blood-iron spear: knockdown and bleed |
| 2 | Blood Wave | a wave of blood that cuts, then bursts in a geyser |
| 3 | Blood Rain | crimson streaks fall on an 8 m circle |
| 4 | Blood Pull | yank a stunned target to you along a blood tether |
| 5 | Sword Circle | five blood blades orbit and cut |
| 6 | Blood Rush | speed and endless stamina |
| 7 | Summon Bats | a swarm of bats bites and blinds |
| 8 | Sword Dance | nine swords; `E` throws one, `G` throws all (no Shadow Dash while they wait) |
| 9 | Vampiric Embrace | a lunge and a real bite: stun and drain |
| 10 | Crimson Eruption | ultimate: a blood moon pulls everyone in, then erupts |

## Werewolf

*Cursed by the Moon* · melee, bruiser, summoner · beast and moon. It closes the gap, pins you and tears.

**Passive · Lunar Blood**: a Rage pool that fills when you fight. The server follows the real lunar phase: stronger at
night, much stronger under a full moon.

| Slot | Spell | In short |
|---|---|---|
| 1 | Rending Claws | three fast rakes toward where you look |
| 2 | Crescent Rend | three crescent waves of moonlight |
| 3 | Moonfall Pounce | leap in an arc and slam down |
| 4 | Ironpelt | iron fur: much less damage, ends in a shockwave |
| 5 | Call of the Pack | three spectral wolves that bite on command |
| 6 | Primal Rage | frenzy: faster, harder claws, lifesteal |
| 7 | Dread Howl | a roar that makes everyone in the cone cower |
| 8 | Moonsong | haste, power and a moon shield for every ally around you (any class) |
| 9 | Savage Maul | lunge, pin one target and tear |
| 10 | Blood Moon Ascendant | ultimate: transform into the beast for 45 s |

## Fairy

*Heart of the Bloom* · support, control, mobility · fae and nature. The Fae Gardener makes things grow: most spells are
planted and pay off on their own clock, and every delayed hit is telegraphed.

**Passive · Bloomheart**: a Bloom gauge that grows with every spell and on living ground. Blooming gives Glamour back;
Full Bloom makes the next spell cost half and hit harder.

| Slot | Spell | In short |
|---|---|---|
| G | Fae Step | a petal blink of 7 m |
| 1 | Bramble Bloom | a fae seed grows into a bursting bramble (knockdown, slow) |
| 2 | Petal Storm | a column of razor petals rolls away (blind) |
| 3 | Sporeling Trap | three mushroom traps that burst when someone comes near |
| 4 | Blossom Aegis | a blossom grove: ward for everyone inside |
| 5 | Entangling Roots | roots whip up and hold the target |
| 6 | Wildwood Barrage | hurl saplings that grow into trees where they land |
| 7 | Bramble Ward | thorny vines: ward and reflect |
| 8 | Faerie Ring | a fae ring that carries whoever steps in |
| 9 | Slumber Spores | a pollen cloud that puts people to sleep |
| 10 | Pixie Swarm | ultimate: nine pixies whirl over the mark |

## Witch

*Mistress of Curses* · curses, control, summoner · hex, shadow and nature. Her curses stack on enemies and feed her.

**Passive · Hexweaver**: every witch spell that lands adds Hex (up to 3, runes over the victim's head). A hit on a
doomed target sets off Malediction: damage, silence and mana burned. Half of every drain flows to the witch.

| Slot | Spell | In short |
|---|---|---|
| G | Hex Mirror | reflect spell damage for you or an ally |
| 1 | Murder of Crows | nine crows wheel over the mark |
| 2 | Witch's Mark | a brand: the target takes more from every class |
| 3 | Shadow Step | come apart into crows and reform up to 22 m away |
| 4 | Skull Barrage | five burning skulls fly at the mark |
| 5 | Hexfire Serpent | a serpent of green fire slithers to the mark and strikes |
| 6 | Cauldron Cataclysm | hurl your cauldron; it erupts |
| 7 | Hexed Effigy | a voodoo doll: damage, weaker spells and mana drain around it |
| 8 | Baleful Polymorph | turn enemies into critters |
| 9 | Smoke Form | become a cloud of black smoke and drift |
| 10 | Witching Hour | ultimate: a witch sigil, then hex lightning |

## Elf

*Elven Elementalist* · versatile, ranged, control · fire, water, ice, lightning, earth, wind, nature and moonlight.

**Passive · Elemental Resonance**: two different elements on one target within 4 s react: water + lightning = Shock,
fire + wind = Firestorm, ice + earth = Shatter, fire + ice = Steam.

| Slot | Spell | In short |
|---|---|---|
| G | Sylvan Veil | fade into leaves: faster, the next spell hits harder |
| 1 | Ember Lance | a spear of fire (burn) |
| 2 | Tidal Ring | a ring of water that shoves and soaks |
| 3 | Tempest Dance | glide 10 m on a whirlwind |
| 4 | Stone Grasp | rock bursts up and roots |
| 5 | Chain Spark | a bolt that jumps between targets |
| 6 | Frost Shards | a fan of ice spikes (chill) |
| 7 | Barkskin Ward | living bark on you or an ally |
| 8 | Gale Vortex | a whirlwind drags everyone in |
| 9 | Lunar Sanctuary | a moon ward dome |
| 10 | Elemental Convergence | ultimate: four elements at once |

## Archer

*Marksman of the Wilds* · marksman, ranged, mobility · physical (the Blast Arrow carries fire). Real bows and real
arrows: trick shots, nets, traps and arrow storms, no magic look.

**Passive · Marksman's Rhythm**: every 3 arrows that hit load a critical (+35 %). Standing still 1.5 s = steady aim:
+10 % range and no sway. The bow and quiver are worn on the back.

| Slot | Spell | In short |
|---|---|---|
| G | Roll Shot | a backward roll that looses one arrow |
| 1 | Piercing Shot | hold to draw: a heavy arrow through 2 bodies |
| 2 | Fan Volley | 5 arrows in a fan (slow) |
| 3 | Snare Shot | a net arrow that roots |
| 4 | Blast Arrow | sticks, burns its fuse, then bursts (knockdown) |
| 5 | Arrow Shower | three waves of arrows rain on a circle |
| 6 | Seeker Volley | six seekers curve onto different targets |
| 7 | Hunter's Trap | a hidden steel jaw trap (root, bleed) |
| 8 | Cyclone Shot | a spin and a ring of 12 arrows |
| 9 | Eagle Eye | longer range, no sway, arrows go through objects, mark the first target |
| 10 | Thousand Arrows | ultimate: a 4 s storm of arrows, then a heavy volley |

## Kitsune

*Foxfire Trickster* · trickster, burst, mobility · spirit and fire. Azure foxfire and illusion.

**Passive · Fox Trickery**: hits leave foxfire marks (up to 3); a hit on a full mark blooms into a bonus burn. After a
dash or a swap the next spell needs no cast time.

| Slot | Spell | In short |
|---|---|---|
| G | Spirit Fox Step | a foxfire dash of 8 m |
| 1 | Kitsune-bi | three homing foxfire wisps |
| 2 | Fox Mirage | three copies of herself run off; hitting one bursts it |
| 3 | Foxfire Lash | a fox-mask sigil fires 9 bolts in a fan |
| 4 | Moonlit Charm | a cone of petals that charms, then slows |
| 5 | Foxfire Veil | 9 orbiting wisps: a shield |
| 6 | Foxfire Rain | foxfire orbs fall over a circle |
| 7 | Spirit Fox | a spirit fox runs at the target and bites 3 times |
| 8 | Spirit Possession | a fox spirit weakens and slows an enemy |
| 9 | Trickster's Swap | swap places with a copy or a marked enemy |
| 10 | Ninefold Awakening | ultimate: nine foxfire flames, faster, every spell bursts |

## Priest

*Keeper of the Dawn* · healer, support, guardian · holy and light. A healer first, a giver of blessings second, with a
few strikes of holy light - and she raises the fallen with the **Rite of Resurrection** (`E` at a fallen player, 5 s),
through your own ambulance script ([how to wire it](integration.md#the-priests-rite-of-resurrection-revive--ambulance-systems)).

**Passive · Afterglow**: every heal she gives leaves a small shield of light; healing another player gives Faith back;
Smite and Holy Nova hits charge Zeal for a stronger Mending Light. Her heals are capped on the server (one heal at most
35; per player 70 HP per 10 s and 60 shield per 12 s across all priests).

| Slot | Spell | In short |
|---|---|---|
| G | Sacred Step | an 8 m glide-step of light |
| 1 | Mending Light | heals the ally under your aim (22 HP), or yourself |
| 2 | Smite | a lance of holy light at the foe under your aim |
| 3 | Aegis of Faith | a dome of light that absorbs 35 spell damage |
| 4 | Prayer of Renewal | a halo that heals 6 HP every 1.5 s |
| 5 | Purify | lifts roots, slows, chills, burns, bleeds and poison |
| 6 | Sanctuary | a circle of dawn runes that heals everyone inside |
| 7 | Holy Nova | strikes and binds foes around you, heals your allies |
| 8 | Blessing of Might | +15 % spell damage for an ally |
| 9 | Hymn of Haste | everyone around you moves 20 % faster |
| 10 | Miracle of Dawn | ultimate: heals, shields and frees your allies, pushes foes back |

## Assassin

*Nightshade Blade* · assassin, burst, mobility · venom, shadow and physical. A hooded blade of a nameless order: twin
daggers, alchemist poisons, ash smoke, a sigil, backstabs and an execute. No healing at all - her spells give Cunning
back, never health.

**Passive · Nightshade Edge**: hits from behind deal +35 % (the server decides from real positions); her daggers, knives
and vial stack Venom on a foe (up to 3, 2 HP a second per stack); a backstab gives Cunning back, a kill much more.

| Slot | Spell | In short |
|---|---|---|
| G | Shade Step | a 7 m low dash that keeps you hidden |
| 1 | Twin Fang | two quick stabs that add Venom; at 3 Venom the next stab ruptures it |
| 2 | Nightshade Knives | three throwing knives in a fan |
| 3 | Venom Vial | a poison cloud at your mark |
| 4 | Umbral Lunge | lunge behind the foe under your aim and stab |
| 5 | Black Mark | mark a foe: more damage, seen through walls, executes sooner |
| 6 | Nightshroud | fade for up to 6 s; the first strike out of it is an Ambush |
| 7 | Ashen Smoke | a smoke cloud that blocks sight, blinds and slows |
| 8 | Crippling Cut | a sweep at the legs that slows |
| 9 | Riposte | a 1 s guard; a blocked hit earns a counter-stab |
| 10 | Coup de Grace | ultimate: seize a foe from behind and strike; executes the weakened |

## Knight

*The Bulwark* · guardian, melee, control · physical. Where the knight plants his feet the line holds: an arming sword
in one hand, a tower shield on the other arm, walls of pavise shields raised out of the earth, a taunt that dares the
enemy to come at him and a chain that ties him to a friend's wounds. He heals no one; he simply does not break.

**Passive · Steadfast Wall**: while the shield is raised, hits from the front are blunted and knockdowns refused; every
blocked hit gives Valor back. Standing still behind it braces him: harder to move, more Valor per block.

| Slot | Spell | In short |
|---|---|---|
| G | Guard Step | a 3.5 m hop back behind the raised shield |
| 1 | Shield Bash | a step-in bash that staggers the foe in front of you |
| 2 | Cleaving Arc | a wide sweep that bites the two nearest foes in front of you |
| 3 | Shield Charge | drive forward behind the shield; the first foe in your lane is knocked down |
| 4 | Rally Banner | a banner at your mark: allies around it are warded and steadied, foes are challenged |
| 5 | Taunting Shout | foes in front of you are challenged and weakened; nearby NPCs turn on you |
| 6 | Iron Bulwark | kneel behind a steel shield wall: hits from the front are blunted, allies beside you are shielded |
| 7 | Pommel Break | a hilt jab to the head that silences one foe |
| 8 | Phalanx Line | a line of pavise shields rises at your mark and shoves back whoever touches it |
| 9 | Oathbound | a steel chain to an ally: part of their wounds come to you, and they are warded while it holds |
| 10 | Bastion of the Last Line | ultimate: a ring of pavises rises around you, then falls outward on your foes |

## Oni

*The Mountain Brute* · bruiser, melee, control · physical and earth. The brute of the old tales: a studded club, a
horned mask and a sake gourd on the hip. Slow and heavy, and the more he bleeds the harder he hits: he throws people by
the collar, cracks the earth into lanes, tears boulders out of the ground and splits a mountain in one blow.

**Passive · Bleeding Fury**: below 60 % health his club hits deal +15 %, below 30 % +30 % and he cannot be knocked
down. Wrath is a rage pool: it fills from damage taken and from club swings, never by itself.

| Slot | Spell | In short |
|---|---|---|
| G | Lumbering Leap | a heavy 6 m hop; the landing trips everyone close by |
| 1 | Crushing Swing | an overhead smash that cracks the ground; costs nothing and fills Wrath |
| 2 | Fissure Swing | a crack runs along your aim, dirt spikes lift everyone on it |
| 3 | Iron Grip | grab the foe in front of you by the collar and throw them along your aim |
| 4 | Gourd of Fury | a long drink: more power and haste, but you take more damage |
| 5 | Boulder Toss | rip a boulder from the ground and hurl it at your mark: a knockdown where it lands |
| 6 | Horned Rush | a bull-rush along your aim that knocks down everyone in your path |
| 7 | Earthshatter Spin | two sweeps of the club hit everyone around you twice and push them out |
| 8 | Wrathful Roar | foes in a cone are weakened and shoved back; NPCs flee |
| 9 | Blood Oath | cut your palm: lose health, gain Wrath; your next club hits bite deeper and bleed |
| 10 | Mountain Splitter | ultimate: the club comes down and a canyon splits open along your aim |

## Samurai

*The Still Blade* · melee, burst, mobility · physical and wind. A swordsman of stillness: the hand rests on the hilt
at the hip and nothing moves until it must. Then one draw-cut, a flash of silver, and the blade is home again. He parries
and answers, names a foe for a duel and ends a fight with a single cut.

**Passive · Iai**: every cut draws the blade for 4 s; sheathed for 2 s, the scabbard charges and the next Iaijutsu Draw
reaches farther and cuts deeper. Damage taken while the blade is sheathed gives Resolve back.

| Slot | Spell | In short |
|---|---|---|
| G | Wind Step | a low 7 m slide with the blade sheathed |
| 1 | Iaijutsu Draw | a draw-cut: everyone on the line in front of you is cut a heartbeat later |
| 2 | Rising Cut | an upward cut that lifts the foes in front of you off the ground |
| 3 | Blade Dance | three slides in a zigzag along your aim, a cut at every turn |
| 4 | Falling Petal | a downward cut; a lifted or airborne foe takes double and is knocked flat |
| 5 | Parry Stance | a short guard; the first hit from a foe close by is answered with a draw-cut and Resolve back |
| 6 | Mark of the Duel | name a foe: your cuts on them and their hits on you both bite harder |
| 7 | Hundred Cuts | eight cuts in a breath, fanning out in front of you |
| 8 | Severing Wind | a streak flies to your mark; a seam opens there and everyone on it is cut down |
| 9 | Zanshin | for a few seconds you cut harder and move faster, and every cut gives Resolve back |
| 10 | Moonless Night | ultimate: stand still, then one draw: everyone on a 12 m line falls together |

## Shaman

*The Totem Caller* · summoner, zone, support · earth and spirit. She plants carved totems that do the work - one burns,
one binds, one wards her kin, one throws the dust - links them with lines of spirit smoke, calls spirit bison out of the
ground and raises a great totem whose drum shakes the field. Any foe can break a totem; she simply plants another.

**Passive · Ancestral Chorus**: every totem she has standing beats a drum and makes her spells stronger; near her own
totem crowd control wears off sooner; a fallen totem gives Ancestry back. Up to 3 totems at once.

| Slot | Spell | In short |
|---|---|---|
| G | Spirit Stride | an 8 m run as a trail of ancestor smoke |
| 1 | Ember Totem | a totem that burns every foe around it |
| 2 | Spirit Link | smoke lines between your totems hurt and mark foes who cross, and hasten allies |
| 3 | Earthbind Totem | foes around it are slowed and cannot jump; the first to touch it is rooted |
| 4 | Totemic Recall | your totems tear out of the ground and plant themselves around you |
| 5 | Ancestor Totem | allies around it are warded and steadied |
| 6 | Mask of the Ancestor | half-seen and faster for a few seconds; every totem beats twice as fast |
| 7 | Gust Totem | every few seconds a dust wave shoves foes away |
| 8 | Ancestral Stampede | three spirit bison thunder down the lane and knock foes flat |
| 9 | Dust Devil | a whirling dust column hunts the nearest foes and lifts whoever it touches |
| 10 | Totem of the Great Spirit | ultimate: a 6 m totem whose drum pushes foes out and strengthens allies, then it falls |

## Alchemist

*The Flask Master* · zone, control, support · venom (acid), fire and ice. A brewer-engineer who turns the battlefield
into a lab: flasks whose puddles react where they meet, floors turned to ice, tar or coals, a brass still on her back, a
homunculus that drinks what she spills and a great work that turns a circle of the field to gold.

**Passive · Volatile Hands**: every third flask is unstable and splashes wider; her own puddles never hurt her; the still
on her back brews one free Elixir every 30 s. At most four puddles at once. Two puddle kinds that meet react: steam, a
flash-burn or a brittle crack.

| Slot | Spell | In short |
|---|---|---|
| G | Glass Slide | smash a frost flask and slide 7 m on the ice; the strip trips runners for a moment |
| 1 | Load Reagent | draw the next flask: acid, frost or ember (everyone sees which one you hold) |
| 2 | Flask Toss | the loaded flask shatters into a puddle of acid, frost or ember |
| 3 | Transmute Floor | a circle of ground turns to glass-ice, tar or coals, by the reagent you hold |
| 4 | Homunculus | a brass-and-glass creature walks to your foe, drinks a puddle on the way and bursts |
| 5 | Quicksilver Draught | a vial for an ally or yourself: faster, and spells cost less |
| 6 | Caustic Spray | a cone of acid mist that burns and weakens |
| 7 | Elixir of the Still | a glassy shield, and every slow, root and burn washed off; free when the still is ready |
| 8 | Transmute to Lead | a foe's weapon turns to lead: no guns or blades for a moment (spells still cast) |
| 9 | Alkahest Bomb | a big flask bursts, then every puddle of yours nearby bursts in a chain |
| 10 | Magnum Opus | ultimate: a circle turns to gold: foes inside stand as gilded statues, allies are shielded |

## Dragonkin

*The Drakeblood* · burst, mobility, zone · fire and wind. A human with dragon blood: no tail, no horns, the dragon shows
in the magic. She breathes cobalt fire, beats wings of blue flame that carry her up and over the field (every flight
ends back on the ground), hardens copper scales over her skin and hoards what she takes.

**Passive · Dragon Scales**: every 5 s without taking damage she grows a copper scale (up to 4); each one cuts the next
hit and is spent; with all four her Breath burns hotter. Hoard fills from the damage she deals.

| Slot | Spell | In short |
|---|---|---|
| G | Wingbeat | a flap 8 m forward and up; `G` again in the air flaps once more |
| 1 | Dragonfire Breath | a cone of cobalt fire you sweep with the camera; foes catch blue flame |
| 2 | Wing Buffet | wings of flame beat once and shove everyone near you back |
| 3 | Skyfall Talon | flap up toward your mark and dive: a burst, a knockdown, burning ground |
| 4 | Cobalt Comet | a blue fireball that bursts into scattering embers |
| 5 | Scale Armour | copper scales harden: less damage taken, fireproof |
| 6 | Dragon's Greed | a ring of coins slows the foes inside and fills your Hoard |
| 7 | Wyrm Wind | a wall of blue flame rolls along the ground and knocks foes down |
| 8 | Draconic Roar | a roar that silences the foes in front of you |
| 9 | Firestorm Ascent | climb on your wings and rain embers on the circle under you |
| 10 | Wrath of the Elder Wyrm | ultimate: rise inside a dragon's head and pour a river of fire down the field |

## Necromancer

*The Gravelord* · summoner, control, drain · shadow. She never fights alone: the dead climb out of the ground for her,
walls of rib and skull rise where she points, and every body on the field is hers to raise. She breathes out wraiths,
leashes souls, and when she plants her bone staff a legion answers.

**Passive · Grave Tithe**: anyone who dies near her leaves a grave mark for 20 s; raising on a grave is free and raises
two, and Corpse Burst can detonate one. Each servant costs Marrow while it stands; a servant that falls gives some back.

| Slot | Spell | In short |
|---|---|---|
| G | Wraithwalk | an 8 m glide, half-seen like a wraith |
| 1 | Bone Spear | a spear of bone down your aim: the first foe is struck and slowed |
| 2 | Raise Dead | a skeleton warrior climbs out at your mark and fights for you (on a grave: free, and two rise) |
| 3 | Corpse Burst | your servant or a grave near your mark bursts into bone shards |
| 4 | Wall of Bone | a 6 m wall of rib and skull; the slot again collapses it in a spray of shards |
| 5 | Soul Leash | a tether that drains the foe under your aim, feeding your Marrow and a little health |
| 6 | Wraith | a wraith drifts to the foe, wails until they flee in fear and haunts them |
| 7 | Grave Chill | a circle of grave-frost: foes inside are slowed, your servants strike harder |
| 8 | Legion Command | your servants run to your mark and strike the foe there together |
| 9 | Lich's Bargain | your servants crumble into bone armour; your next raise brings one more |
| 10 | Rise, My Legion | ultimate: a death circle bursts and a legion of the dead rises to fight |

## Chronomancer

*Keeper of the Hour* · control, support, mobility · arcane. She does not bend the world's time, only her own: she runs
back along her last breaths, writes a spell into the future so it strikes twice and freezes a circle in sand-glass while
the hours rise around it. Brass, sand and clock-glass.

**Passive · Tempo**: every cast fills the Tempo gauge; at 100 the next spell comes back at once. Under a third of her
health, once every 30 s, a shield of sand catches the blow.

| Slot | Spell | In short |
|---|---|---|
| G | Quickstep | a 7 m burst-run with three brass afterimages |
| 1 | Sand Bolt | a bolt of sand along your crosshair: damage and a slow |
| 2 | Rewind | run back along your own path of the last 4 seconds |
| 3 | Stasis Snare | a clock face at your mark; when its hands lock, everyone inside is frozen in sand-glass |
| 4 | Time Dilation | gear rings at your mark: your side moves faster inside, everyone else slower |
| 5 | Echo Cast | your next spell is written into the future: 2 s after it lands, an echo plays it again |
| 6 | Steal Time | a sand ribbon slows and silences a foe and speeds you up |
| 7 | Hourglass Ward | a shield for an ally (or yourself); when it ends, its sand bursts and slows foes nearby |
| 8 | Clockwork Sentinel | a brass turret at your mark fires sand bolts at the nearest foe |
| 9 | Age | the foe grows weak and slow, and one of their buffs falls away |
| 10 | Hour Zero | ultimate: twelve brass hours ring your mark; at twelve the circle freezes, then every shell shatters |
