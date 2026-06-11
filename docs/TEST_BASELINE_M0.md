# M0 Test Baseline

Policy: make check is not a blocking M0 gate; from M1 onward, no new failure may be introduced relative to this baseline.

- Command: timeout 45m make -j2 check, with output captured in docs/build_log_m0ter_check.txt.
- Result: completed before timeout; make check exited non-zero.
- Failure baseline count: 125 total runner failures = 118 FAIL + 6 INVALID + 1 ERROR.
- Runner summary: FAILED 125, KNOWN_FAILING 10, ASSUMPTIONS_FAILED 72, TO_DO 625, EXPECT_FAILING 6, PASSED 4373, TOTAL 5211.

## FAIL (118)

1. Capture: Missing badge malus apply correcly in gen 9 1/9
2. Gem boosted Damage calculation 1/16
3. Punching Glove vs Muscle Band Damage calculation 1/16
4. Cheek Pouch doesn't activate under Heal Block's effect
5. Color Change changes the type when a Pokemon is hit by Doom Desire
6. Color Change changes the type when a Pokemon is hit by Future Sight
7. Costar copies an ally's Focus Energy critical hit boost (2/2)
8. Dancer-called attacks do not trigger Life Orb if target is immune
9. Spread Moves: AOE move vs Eiscue and Mimikyu (Based on vanilla games)
10. Trainer Slide: Doubles: Last Switchin
11. Trainer Slide: Doubles: Enemy Mon Unaffected
12. Trainer Slide: Singles: Last Switchin
13. Trainer Slide: Singles: Enemy Mon Unaffected
14. Forewarn does not trigger if a mon switches in while the opposing field is empty
15. Beads of Ruin increases damage taken by physical moves in Wonder Room 4/4
16. Beast Boost considers Wonder Room
17. (Gulp Missile) Cramorant in Gorging damages an electric type without paralysing
18. Illusion does not break if the attacker faints without taking damage
19. Intimidate is not going to trigger if a mon switches out through u-turn and the opposing field is empty
20. Lightning Rod redirects an ally's attack
21. Dragonize boosts power of affected moves by 20% (Gen7+) or 30% (Gen1-6) 4/4
22. Orichalcum Pulse sets up sun for 8 turns with Heat Rock
23. Pixilate boosts power of affected moves by 20% (Gen7+) or 30% (Gen1-6) 4/4
24. Shield Dust does or does not block Sparkling Aria depending on number of targets hit 1/2
25. Sword of Ruin increases damage taken by special moves in Wonder Room 4/4
26. Wind Power sets up Charge for opponent when hit by a wind move 2/2
27. Electromorphosis triggers on each multistrike hit but Charge does not stack
28. Electromorphosis sets up Charge when hit by any move 1/2
29. AI stays choice locked into moves in spite of the player's ability disabling them 5/5
30. Hadron Engine boosts the Pokemon's Special Attack on Electric Terrain even if not grounded 4/4
31. Hunger Switch does not switch a mon transformed into Morpeko's form
32. Infiltrator doesn't ignore a battler's Substitute when using Transform or Sky Drop 1/4
33. AI sees corresponding absorbing abilities on partners 2/11
34. Magic Bounce bounces back moves hitting foes field 1/2
35. Mega Sol ignores Snow's Ice-type Defense boost
36. Neutralizing Gas is active until the last Dragon Darts hit even if Neutralizing Gas is no longer on the field
37. Orichalcum Pulse sets up sun for 5 turns
38. Protosynthesis uses Wonder Room swapped defenses when choosing boosted stat
39. Quark Drive uses Wonder Room swapped defenses when choosing boosted stat
40. Switch AI: Palafin hard switches into absorb abilities instead of Flip Turn (Single) 1/3
41. AI_FLAG_SMART_SWITCHING: AI will switch out if all moves deal zero damage (absorbing ability) (1/?)
42. Spicy Spray burns the attacker even if the defender behind a Substitute takes damage
43. Wind Power sets up Charge for player when hit by a wind move 2/2
44. AI can use all moves, 201-300 49/69
45. Imposter doesn't apply the heroic transformation message when copying Palafin
46. AI will see 2HKOs through resist berries
47. AI recognizes Volt Absorb received from Trace
48. AI will choose Beat Up on an ally with Justified if it will benefit the ally 2/4
49. Covert Cloak does or does not block Sparkling Aria depending on number of targets hit 1/2
50. Enigma Berry does nothing if Heal Block applies
51. AI_FLAG_SMART_SWITCHING: AI will consider player's endure effects when evaluating switchin candidates 2/2
52. Switch AI: Palafin hard switches into absorb abilities instead of Flip Turn (Doubles) 1/3
53. White Herb wont have time to activate if Magician steals it
54. White Herb wont have time to activate if it is knocked off or stolen by Thief 1/2
55. AI sees Loaded Dice damage increase from multi hit moves
56. Beat Up's damage doesn't consider STAB
57. Beat Up's damage is Dark-typed (Gen5+) 2/2
58. Chilly Reception fails if it can't switch the user out or change the weather
59. Conversion 2's type change fails targeting Struggle (Gen 5+)
60. Conversion 2's type change considers status moves (Gen 5+)
61. Defog removes Toxic Spikes from target's side 2/2
62. Defog removes Stealth Rock and Sticky Web from target's side 2/2
63. Embargo doesn't block held item effects that affect effort values
64. Encore forces the last move used while asleep
65. Final Gambit does not faint user if target is immune
66. Final Gambit does not faint user if target protects
67. Final Gambit faints the user, and the target receives damage equal to the user's HP 1/2
68. Fling - Mental Herb effect should not remove the target's held item
69. AI can use all moves, 101-200 46/64
70. Focus Punch does not activate when Focus Band/Focus Sash/Sturdy prevent getting one-shot by an attack 1/3
71. Future Sight uses Sp. Atk stat of the original user without modifiers 1/2
72. Magic Coat reflects hazards regardless of the user's position 1/2
73. Multi Hit moves will not disrupt Destiny Bond flag 1/2
74. Air Balloon pops when Disguise is broken 1/2
75. Leftovers does nothing if Heal Block applies
76. Rapid Spin doesn't blow away Wrap, hazards or raise Speed when Sheer Force boosted (Gen 9+)
77. Beat Up's damage is determined by each striking Pokémon's base attack and level and the target's defense
78. Semi-invulnerable moves don't need to charge with Power Herb 1/6
79. Charge's effect does not stack with Electromorphosis or Wind Power 1/2
80. Chilly Reception switches the user out even if it can't change the weather
81. Conversion 2 fails if the move used is of typeless damage (Gen 5+)
82. Conversion 2's type change considers move types changed by Normalize and Electrify
83. Conversion 2 randomly changes the type of the user to a type that resists the last used target's move (Gen 5+)
84. Curse applies to the user if used with Protean/Libero 1/2
85. Defog removes Spikes from target's side 2/2
86. Embargo can be reflected by Magic Coat
87. Toxic cannot miss if used by a Poison-type (Gen6+) 4/4
88. Transform fails on target behind substitute in Gen5+ 2/2
89. Fling - Item does not get blocked by Unnerve if it isn't a berry
90. Skull Bash needs a charging turn
91. Razor Wind doesn't need to charge with Power Herb
92. Uproar status causes sleeping Pokémon to wake up during an attack (2/2)
93. Foresight causes moves against the target to ignore positive evasion stat stages (2/2)
94. Future Sight flying type attacker in party receives no boost from Psychic Terrain 4/4
95. Future Sight doesn't ignore Wonder Guard (Gen 5+)
96. Future Sight is affected by type effectiveness (Gen 5+)
97. Future Sight receives STAB from party mon (Gen 5+)
98. Gravity cancels Fly and Sky Drop if they are in the air
99. Wake-Up Slap does not cure paralyzed pokemons behind substitutes or get increased power 2/2
100. Smelling Salts does not cure paralyzed pokemons behind substitutes or get increased power 2/2
101. Axe Kick still deals crash damage when boosted by Sheer Force 1/2
102. Knock Off does not remove item when used by Wild Pokemon (Gen 5+)
103. Frostbite is healed if hit with a thawing move 1/5
104. Thunder Wave prints an avoided attack message when it misses
105. Magic Coat reflection doesn't activate Protean/Libero 1/2
106. Magic Room: An item that can activate will activate once Magic Room is over
107. Sheer Cold doesn't affect Ice-type Pokémon (Gen7+)
108. Psychic Terrain doesn't block priority moves against semi-invulnerable targets 2/2
109. Recoil if miss: Supercell Slam causes recoil if it is absorbed
110. Reflect Damage: Counter is affected by Protect effects if it was damaged by that battler 2/4
111. Semi-invulnerable moves make the user semi-invulnerable turn 1, then strike turn 2 2/6
112. Sky Drop does no damage to Flying type Pokémon
113. Spit Up's Stockpile's are romoved if move is absorbed
114. Transform returns the user to normal at the end of the battle after fainting
115. Sky Attack doesn't need to charge with Power Herb
116. Skull Bash doesn't need to charge with Power Herb
117. Razor Wind successfully KOs both opponents
118. Frostbite reduces the special attack by 50 percent

## INVALID (6)

1. AI_FLAG_SMART_SWITCHING: AI will consider player's endure effects when evaluating Bad Odds 1v1 (1/?)
2. AI uses Final Gambit
3. Psychic Terrain protects grounded battlers from priority moves in doubles - Right
4. Recoil if miss: Jump Kick's recoil happens after Spiky Shield damage and Pokemon can faint from either of these 1/3
5. Final Gambit faints user and target
6. Psychic Terrain protects grounded battlers from priority moves in doubles - Left

## ERROR (1)

1. Dancer can still copy a move even if it's being forced into a different move - Encore

## Assumption Failures (72)

1. givemon respects perfectIVCount but does overwrite fixed IVs (1)
2. givemon respects perfectIVCount but does overwrite fixed IVs (2)
3. givemon respects perfectIVCount
4. Damage calculation matches Gen5+ (Marshadow vs Mawile)
5. Comatose boosts Dream Ball's multiplier
6. Sleep Clause: Sleep clause is deactivated when a sleeping mon is woken up with Aromatherapy / Heal Bell / Sparkly Swirl
7. Sleep Clause: Sleep clause is deactivated when a sleeping mon wakes up
8. Trainer Class Balls apply to the entire party
9. Filter reduces damage to Super Effective moves by 0.75
10. Flower Gift transforms Cherrim back when it switches out
11. Flower Gift transforms Cherrim back to normal when its ability is suppressed
12. Forecast transforms Castform back when it uses a move that forces it to switch out
13. Forecast transforms Castform back when it switches out
14. Forewarn randomly chooses between opponents with same-power moves
15. Flower Gift does not transform Cherrim back to normal when suppressed if Cherrim is Dynamaxed
16. Flower Gift transforms Cherrim back when it uses a move that forces it to switch out
17. Forecast transforms Castform back to normal when its ability is suppressed
18. Forewarn randomly chooses between same-power moves on one opponent
19. AI won't use Solar Beam if there is no Sun up or the user is not holding Power Herb
20. AI prefers moves which deal more damage instead of moves which are super-effective but deal less damage
21. AI prefers Water Gun over Bubble if it knows that foe has Contrary
22. AI prefers Bubble over Water Gun if it's slower
23. Gulp Missile: If Cramorant loses Gulp Missile, it cannot spit out its prey
24. Gulp Missile only changes forms for Cramorant
25. HasMoveThatChangesKOThreshold - AI should not see self-targeted speed drops as preventing setup moves in 2hko cases
26. AI sees increased base power of Smelling Salt
27. AI uses Trick Room intelligently
28. Mega Sol: Growth increases Attack and Sp. Atk by 2 stages under Mega Sol (Gen 5+)
29. AI_FLAG_RISKY: Mid-battle switches prioritize offensive options
30. Pickpocket checks contact/effect per target for spread moves
31. AI_FLAG_SMART_TERA: AI will not tera if it gets outsped and ko'd
32. AI_FLAG_SMART_SWITCHING: AI will stay in if Encore'd into super effective move
33. AI calculates guaranteed criticals and detects critical immunity
34. AI prefers a weaker move over a one with a downside effect if both require the same number of hits to ko
35. AI can choose Counter or Mirror Coat if the predicted move split is correct and user doesn't faint
36. AI sees increased base power of Wake Up Slap
37. AI uses After You to set up Trick Room
38. (TERA) Revelation Dance uses a Terastallized Pokemon's Tera Type
39. (Z-MOVE) Z_EFFECT_CURSE activates Z_EFFECT_RECOVER_HP or Z_EFFECT_ATK_UP_1 depending on the type of the battler
40. AI_FLAG_SMART_MON_CHOICES: AI will properly consider immunities when determining switchin type matchup
41. Throat Spray activates when a sound move is used
42. AI_FLAG_SMART_SWITCHING: AI will switch out if it has been Toxic'd for at least two turns 50% of the time with more than 1/3 HP remaining with good switchin
43. Absorb fails if Heal Block applies
44. Howl does not work on partner if it has Soundproof
45. Dark Void inflicts 1-3 turns of sleep
46. Dream Eater fails if Heal Block applies
47. Dynamax: Dynamaxed Pokemon can have base moves disabled on their first turn
48. (TERA) Revelation Dance uses a Stellar-type Pokemon's base type
49. Life Orb does not activate if using status move on a Substitute
50. Rest fails if the user is protected by Leaf Guard
51. Revelation Dance becomes Normal type if used by a Typeless Pokemon due to Roost
52. Howl raises user's and partner's Attack by 1 stage
53. Hypnosis inflicts 1-3 turns of sleep
54. Snatch does not steal a move that was already snatched this turn (Gen 5+)
55. Tail Glow drastically raises Special Attack
56. Speed Down: Cotton Spore does not fail if it is blocked by one target
57. Dark Void inflicts 1-3 turns of sleep
58. Upper Hand fails if the target has attempted to act even if previously successful
59. Upper Hand is boosted by Sheer Force
60. Upper Hand fails if the target moves first
61. Upper Hand succeeds if the target is using a priority attacking move and causes it to flinch
62. AI won't use status moves if the player's best attacking move is Focus Punch
63. Sparkling Aria cures burns from all Pokemon on the field and behind substitutes
64. Thrash confuses the user if it is canceled on turn 3 of 3, Protect
65. Sheer Cold doesn't affect Ice-type Pokémon (Gen7+)
66. Revelation Dance becomes Normal type if used by a Typeless Pokemon due to Roost
67. Hypnosis inflicts 1-3 turns of sleep
68. Strength Sap fails if Heal Block applies
69. Upper Hand succeeds if the target's move is boosted in priority by an Ability
70. Uproar wakes up other pokemon on field
71. Thrash confuses the user if it is canceled on turn 3 of 3, Immunity
72. Sheer Cold does affect Ice-type Pokémon (Gen3-6)

## Known Failing (10)

1. Pokémon level up learnsets fit within MAX_LEVEL_UP_MOVES and MAX_RELEARNER_MOVES
2. Anticipation treats Hidden Power as its dynamic type (Gen6+)
3. Sleep Clause: Sleep clause is deactivated when a sleeping mon is sent out and transforms into a mon with Insomnia / Vital spirit
4. Mirror Armor lowers Speed of the partner Pokemon after Court Change was used by the opponent after it set up Sticky Web
5. AI_SMART_MON_CHOICES: AI sees its own terrain setting ability's effect on failed moves when considering switchin candidates
6. AI uses Helping Hand if the ally does notably more damage
7. Embargo blocks an affected Pokémon's trainer from using items
8. AI uses Dynamax -- AI does not dynamax before using a utility move
9. AI uses Dynamax -- Max Moves are scored based on max move effects, not base effects
10. Roost recovers 50% of the user's Max HP
