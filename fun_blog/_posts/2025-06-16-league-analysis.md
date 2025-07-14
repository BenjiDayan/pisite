---
layout: post
title:  "League analysis"
date:   2025-06-15 20:57:00 -0800
categories: fun_blog videogames
---


## Introduction

League is a surprisingly rich game, inspiring players to descend time and again onto the pretty much exact same summoner's rift map for 30-40 minute matches. There are many ways to derive entertainment and enjoyment from this experience, if those are indeed the right adjectives; players sink hours into diverse avenues such as "sadistically leading enemies on a poisnous wild goose chase" (Singed top lane), "bright and positive zappy laser girl" (Lux), and "meticulous criminal psychopath who believes murder is art" (Jhin) - that last one is actually literally the league wiki quote on the champion. I believe that the engine that keeps league going is the fulfillment of myriad player fantasies. I've had my share of champion fantasies (fyi the champion I've the most games on is Ezreal) [^1], however another source of obsession and fantasy that I've persisted, even since long having ceased to play at all consistently, is in theory crafting item combinations / synergies, and how champions scale with them.

[^1]: I found this website which ranks champions by % mained and % one-tricked. E.g. Warwick is the top one-tricked champion: Awooooo!

The genesis of this post was a conviction/fixation that Thresh could be a wildly strong champion, breaking from his traditional supportive role. In order to explain how, I will actually dive deeper into wider and more interesting topics, bringing a mathematical and analytical lens. Given League's popularity I'm sure there exists similar analyses elsewhere on the internet, however I'm doing mine mostly from scratch and through reference to <https://wiki.leagueoflegends.com/en-us/>. TBD how much interest/diversion this post will inspire to League non-afficionados - we'll see!

Much of the phenomena explained by my analysis will be intuitively obvious / already known to people who've played league or other similar games. I hope that nonetheless my explanations may still provide some interesting nuggets of insight!

## The basics - defense vs offense

To reap rewarding insights, we must first lay a foundation of understanding in the fundamental game mechanic of attack and defense. 

<figure class="image-with-caption" style="float:right;">
    <img src="/assets/images/jhin_vs_leona.png" width="300">
    <figcaption><em>Atrocious gemini effort for Jhin vs Leona, A vs D</em></figcaption>
</figure>

An essential component of league, that we will study in idealised and simplified format, is the fight to death between your player controlled character and an enemy's. Whoever's health bar is first depleted perishes, leaving the survivor as victor. A grim tale as old as time.

We will immediately reduce all nuance and beauty by modelling the situation as the interaction of a few key values.

<figure class="image-with-caption" style="float:left;">
    <img src="/assets/images/ezreal_before.png" width="300">
    <figcaption><em>Ezreal Base Stats</em></figcaption>
</figure>

<!-- <figure class="image-**with**-caption" style="float:right;">
    <img src="/assets/images/**ezreal_after**.png" width="300">
    <figcaption><em>Atrocious gemini effort for Jhin vs Leona, A vs D</em></figcaption>
</figure> -->

Shown in this complicated are the various "stat values" of the champion Ezreal at level 9. To get easier math, we will simplify these numbers even more and say he has 1200 **Health**, 50 **Armour**, 100 **Attack Damage (AD)**, and a slovenly 0.6 **Attack Speed / Attacks per Second (AS)**.

We will of course pit poor Ez against his mirror image in a 1v1 to the death. We can calculate his **Damage Per Second (DPS)** as $$100 \times 0.6 = 60$$, meaning his **Time to Kill (TTK)** his dark alter-ego is $$TTK = \frac{HP}{DPS} = \frac{1200}{60} = 20 \;\text{seconds}$$. But wait - how do we take into account armour?!

### Armour

The simple calculation of the effect of armour is as modifying his (true) 1000 Health to become **Effective Health**. In this case Ezreal has $$1000 \times \frac{100 + 50}{100} = 1500$$ Effective Health. 50 Armour implies an extra 50% Effective Health! Thus in reality the duel would take an even more pain-staking 30 seconds till one Ezreal bites the dust [^2]. We'll use the slightly more revealing viewpoint of 50 armour providing a 1.5x **Defense Multiplier (DM)**. In reality armour provides rather a form of damage reduction, multiplying incoming damage by $$\frac{100}{100 + 50}$$. But we'll see that the positive multiplier will be more revealing in analsyis to come.

[^2]: Ezreal mains know too well his catch-phrase "You belong in a museum"! His persona is some kind of spunky kid Indiana Jones shooting mystic energy projectiles.


## TTK 1v1 Equation

Putting this all together, the central equation to determine 1v1 outcome is

\\[
\text{TimeToKill (enemy)} = \frac{\text{(opponent's)}\; HP \times Armour}{\text{(your)}\; AD \times AS}
\\]

If your TTK is smaller than your opponent's, you win the fight.

<!-- When things are nice and symmetric -->




<!-- Ezreal's base 50 armour actually provides a 1.5x defense multiplier. This 50% increase in his defense gives a direct 50% extra lifetime under constant DPS by enemy Ezreal (20 seconds -> 30 seconds). This multiplicative framework is great for comparing apples to apples, as it's then clear that for the enemy ezreal to cancel this out, they need either a 50% increase in either AD or AS.

\\[
\text{TimeToKill} = \frac{HP \times \text{DefMult}}{DPS} = \frac{HP \times \text{DefMult}}{AD \times AS}
\\]

Once you start thinking in multipliers, things become a lot clearer. -->

### Buying stats

Why does all this math matter? Because a key gameplay loop in league is spending gold on items that buff your champion (increasing their attack / defense). You use this to more effectively defeat your enemies, gaining more gold, in a virtuous cycle.

But how do we decide which items to buy? League has all sorts of interesting items, but we'll start with just the very basic ones - a simple exchange of gold for singular stat increase. Sword = AD, Dagger = AS, Ruby Crystal = HP etc.

<!-- <figure class="image-with-caption">
    <img src="/assets/images/league_gold_basic_items.png"
    style="width:100%; height:auto;"
     ">
    <figcaption><em>Basic Items</em></figcaption>
</figure> -->

<!-- <figure class="image-with-caption" style="float:left;">
    <img src="/assets/images/ezreal_before.png" width="300">
    <figcaption><em>Ezreal Base Stats</em></figcaption>
</figure> -->

<figure class="image-with-caption" style="width:100%;">
    <img src="/assets/images/league_gold_basic_items.png">
    <figcaption><em>Ezreal Base Stats</em></figcaption>
</figure>

Let's say that we've decided to invest in more defense. Let's say we have just 400 gold, and want to spend 300 gold on 15 more armour, or 400 gold on 150 HP. Presumably the higher cost 150 HP will be more valuable - and the way to verify this is through working out the percentage / multiplier effect. 1200 -> 1350 HP vs 1.5x -> 1.65x armour defense multiplier. It's simplest to convert the HP difference into a ratio as well: 1.2 -> 1.35 (also a +0.15, but from a lower base) - which is then clearly a bigger boost.

### The 1v1 stat efficiency viewpoint: diminishing returns

The simple upshot is that when taking marginal decisions like "should I buy more health or more armour", the simple optimal answer is to strike a rough balance of both. An additional 150 HP will make a tiny 1.03x difference to your total defense if you already have 5000 HP, however 15 extra armour from a base of 50 yields a 1.65/1.5 = 1.1x defense boost.

In the symmetric 1v1 between two identical champions who have bought a different bag of bonus stat items, we can figure out who wins by comparing the multiplicative boosts of all their stats.

Call the total **Defense Multiplier** and total **Attack multiplier** 

\\[
DM = \frac{HP + HP^+}{HP} \times \frac{Armour + Armour^+}{Armour} \quad AM = \frac{AD + AD^+}{AD} \frac{AS + AS^+}{AS}
\\]

<!-- $$DM = \frac{HP + HP^+}{HP} \times \frac{Armour + Armour^+}{Armour}$$, and likewise the total **Attack Multiplier** $$AM = \frac{AD + AD^+}{AD} \frac{AS + AS^+}{AS}$$,  -->

Where here $$X^+$$ denotes the amount of bonus stat bought. We can denote the ratio $$\frac{HP + HP^+}{HP} =: HP^*$$, the multiplier boost, so that more simply

\\[
DM = HP^* \times Armour^* \quad AM = AD^* \times AS^*
\\]

Then to figure out who wins the 1v1, we can more simply compare just the ratio

\\[
    \frac{TTK_0}{TTK_1} = \frac{DM_1 \times AM_1}{DM_0 \times AM_0}
\\]

I.e. it all ends up as the ratio between each of your $$HP^* \times Armour^* \times AD^* \times AS^*$$! Everything is a simple multiplication...

Now every comparison becomes brutally simple. In a simple world where the baseline stats are 1000 HP, 0 Armour, 100 AD and 1.0 AS, if you choose to buy 10 more AD, and your opponent buys 100 more HP, their $$DM_1$$ increases by 1.1x as does your $$AM_0$$, so it's a wash and complete draw. With twice as much gold however, the optimal strategy is to buy 10 AD and 100 HP, as this will beat both 20 bonus AD, and 200 bonus HP, for the combined multiplier of $$1.1 \times 1.1 = 1.21 > 1.2$$.

Again we see the concept of **diminishing returns**. Every additional 10 AD increases your AM by a smaller and smaller percentage - $$1.1/1 = 10\%,\; 1.2/1.1 = 9.1\%,\; 1.3/1.2 = 8.3\% ...$$.

<!-- We saw in [#Multipliers as the key to victory](#multipliers-as-the-key-to-victory) that in the simple 1v1 fight to the death, you could cancel out exactly the benefit of a 1.5x defense multiplier with a 1.5x attack multiplier - either increasing your AD by 50%, or your AS by 50%. -->

<!-- Let's start in the simplified world of 0 armour, 1000 HP, 100 AD and 1.0 AS. TTK is simply $$1000 / (100 \times 1.0) = 10$$ seconds. Let's say you're choosing to spend an equivalent sum of gold to buy either 10 AD or 100 HP. If you choose 10 AD, and your opponent chooses 100 HP, these will perfectly cancel out. Neither of your TTKs change. Your 10% attack modifier is perfectly cancelled out by their 10% defense modifier.

Start again with twice the gold. If you buy 20 AD and they 200 HP, again it's a stalemate. However if you decide sneakily to buy instead 10 AD and 100 HP, who wins?

>! Your attack defense balance beats the pure defense!

The intuition should be simple - the additional purchase of 100+100 HP does increase the enemy's defense multiplier to 20%, however this is actually a **diminishing return** (in percentage terms) - $$1.2 < 1.1 \times 1.1 = 1.21$$, which is your combined 1.1 AM (**Attack Multiplier**) and 1.1 DM. Every additional 10 AD increases your AM by a smaller and smaller percentage - $$11/10 = 10\%,\; 12/11 = 9.1\%,\; 13/12 = 8.3\% ...$$.

A champion's idealised "1v1 score" is $$AM \times DM$$, the product of their attack modifier and defense modifier. -->

#### Optimal stat balance; Bruisers rule 1v1s

<!-- We can break down AM as $$\text{ADmult} \times \text{ASmult}$$ and DM as $$\text{HPmult} \times \text{ArmourMult}$$. Because of these **cross-multiplication** (AD with AS and HP with armour), the truly optimal (assuming equal gold efficiency) allocation of resources to buy bonus stats is an equal balance of bonus AD, AS, HP and Armour.  -->

<!-- The 

#### Bruisers rule 1v1s -->

The simple conclusion of this idealised analysis is that in a 1v1 fight to the death, optimal gold allocation actually balances perfectly between bonus attack and bonus defense, DM and AM, and actually because each is again a simple product, between every single bonus stat multiplier, $$HP^*, Armour^*, AD^*, AS^*$$.

<!-- 
. Every gold expenditure should consider the marginal multiplier benefit, along the lines of "I have too much bonus HP, buying more would increase my total defense by a small percentage. My gold would be better spent increasing my small amount of AD, for a large multiplying benefit". -->

Our analysis isn't just hypothetical, it really reflects the reality. When an **ADC (attack damage carry)** (glass cannon ranged champion building only damage and no defense) is forced to fight 1v1 with a **bruiser** (shorter ranged / melee champion building a balance of offense and defense), the ADC will generally lose. The same goes for a full **tank** (champion building only defense) against the bruiser! 

### 2v2 and the evolution of role assignment

Why then do these long-ranged **ADCs** build only damage? Should all champions not just converge to the **bruiser** ideal?

I'll show **two** good reasons, and multipliers will feature again in one! They both emerge in a more complex **teamfight** 2v2 and nvn settings. League is actually normally a game of two teams of 5 champions (each controlled by one human player). Crucial in winning a game will be the occurence of multiple such teamfights.

#### Champion heterogeneity incentivises specialisation

You may have heard of the Adam Smith / David Ricardo theory of international trade - with the concept of specialisation due to [comparative advantage](https://en.wikipedia.org/wiki/Comparative_advantage).

Somewhat analagously, champions in league are all unique, and have their own comparative advantages. A primary differentiator is between long-ranged and shorter-ranged (often melee) champions. In a 2v2 teamfight setting where both sides have one ranged and one melee champion, by the laws of geometry, the melee champions will clash in the middle and bear the brunt of enemy firepower, while the ranged champions will dish out DPS from afar while taking little damage themselves. It's already clear that the roles of **tank** and **ADC** should come about!

The comparative disadvantage of the melee champion of being first to the line of fire means their investing in offensive power will be less useful than into defense. The simple reason being that
1. They will die before their long-ranged ally. Additional DPS is useless when dead! This gets worse the bigger the teamfight (nvn) - more enemy firepower concentrated on the first frontline target
2. More subtly, being melee inherently makes it harder to actually apply DPS (think multiple rounds of shot arrows before the swordsman can close the distance)

The vast simplification of the 2v2 fight is that both frontline melee champs take 100% of the enemy team's DPS. Whichever melee expires first will cease to output DPS, and the opposing team's DPS will immediately redirect to the long-ranged champion behind. We call this style of fighting **front-to-back**.

In this oversimplified framework and restricting to buying just HP vs AD, optimal stat allocation will solely put bonus offense to the ranged, and bonus defense to the melee. The fight is lost when your whole team's collective HP is 0, so on a defense viewpoint allocating to either character is equivalent, however it's better placed on the melee as this will prolong the melee's DPSing window before they die. Similarly given that they will die before the ranged champion, any bonus AD should go solely on the ranged to not be wasted.

Hence our 1v1 "balanced bonus offense and defense is optimal" becomes in the 2v2 setting rather "balanced bonus offense and defense, cleanly split to the damage dealer and tank roles".


#### Multipliers be multiplying

An extreme sharpening of comparative advantage is the presence of **cross-multipliers** which actually compound advantages to be more pronounced. Consider two champions X and Y who are otherwise identical, except that
- champ X has a 2x AD multiplier (200 AD, 1000 HP)
- champ Y has a 2x HP multiplier (100 AD, 2000 HP)

Consider buying a flat 10% extra AS, and assigning this to either X or Y. If they had to 1v1, this would equally tip the balance in favour of the buffed side - the $$TTK_0/TTK_1$$ ratio doesn't care, it's a 1.1x multiplier either way.
However when champ X and champ Y form a team together, it really matters that the 10% extra AS is an extra 20 DPS on champ X rather than 10 DPS on champ Y. Logically the buff is more optimal on X than Y.
Similarly if we're considering who to give a bonus 10 Armour, it should go to Y not X.

This means that the more specialised a champion gets into the offense or defense tree, because of the existence of cross-multipliers, the more they should continue to invest - however in a smart fashion: an equal balance between bonus AD and AS, so as to maximise the total multiplier $$AD^* \times AS^*$$ still holds as more efficient than biasing to any one stat value; the same goes for bonus HP and Armour.






<!-- A further powerful incentive for specialisation in the 2v2 setting is that once roles are assigned,



is that the power of diminishing returns evinced in [1v1 scenario](#bruisers-rule-1v1s) is flipped on its head by the presence of **multiplicative-multipliers**.

We already saw these in our [TTK equation derivation](#multipliers-as-the-key-to-victory). On the defense side we had $$HP \times (1+ \text{Armour})$$, and on the offense side $$AD \times AS$$. -->


### Upshot & Perverse Incentives / Outcomes

Putting this all together, in a teamfight scenario, some champions have comparative advantage to be tanks, and some as damage dealers, and once they start investing in increasing one side of offense or defense, by the laws of **cross-multipliers**, they are ever more encouraged to specialise more intensely.

Having understood these concepts, we can identify and explain common areas of confusion and frustration in league games.

- ADC angry at getting destroyed by bruiser in 1v1: we covered this - the role of ADC only makes sense for teamfighting
- Bruiser feels useless in teamfights / late game: early in the game generally has more 1v1s where bruisers shine, and later in the game teamfights become more important, where bruisers are generally inferior to pure tanks
- Tank player gets flamed for not dutifully protecting the ADC; teammates blame ADC for recklessly overstepping and getting one-shot by the enemy team: now we understand the dominant optimal way of playing a 2v2 or nvn team fight is front-to-back, sadly indeed straying from the optimal formula can lead to disaster.

This all feels slightly constraining. League is meant to be a fun game after all! But people do play to win, and the way the game is currently designed, the best way to achieve this is by playing your part, fitting into a set of roles. And after all no one role / champion can feel too strong, otherwise all interactions with them would be overly negative to the opposing team. For example, bruisers will often be stronger in the early game due to the pre-dominance of 1v1s there, so maybe it's only right that they should feel quite weak in late game team fights. And as we'll see in the next section, ADCs very much feel stronger in the late game team fights, and as some recompense they spend the early game with lower agency and impact, forced to just try and farm gold with minimal risk.

More could still be done to let everyone eat more cake though! For example having more smaller scale objectives around the map that add up to a large advantage, would give bruiser 1v1 specialists more to do in the late game, as opposed to the current map having mainly large objectives in the late game which encourage team  fights to contest them.


## Hyperscaling laws

If you're familiar with league and have been following the math closely, you may have found the [description of theoretically optimal 1v1](#optimal-stat-balance-bruisers-rule-1v1s) strange: we showed that defense and offense have equal importance! In fact (though it's not immediately obivous), even in our perfect 2v2 setting, again in a face-off between two teams with equal but opposite bonus stats:
- Team 1: (AM = 1x, DM = 1x), (AM = 1x, DM = 2x) i.e. a buffed tank
- Team 2: (AM = 2x, DM = 1x), (AM = 1x, DM = 1x) i.e. a buffed damage dealer 

Again, the teamfight will be a perfect draw (even though Team 2's front liner will fall first, diminishing their DPS early, Team 2 will still catch up in the end due to their consistently high DPS). But every league player worth their salt knows that excess team gold should be channeled to the ADC so they can buy more offensive stats. What's going on?

### Superior exponential scaling of damage dealers vs tanks

[Multipliers be multiplying](#multipliers-be-multiplying) means that you can expontentially scale bonus offensive / defensive statistics by hitting multiple bases. A 1.5x AD bonus and a 1.5x AS bonus collectively makes a 2.25x total attack modifier! The more multiplications we can get in there, the total scaling balloons exponentially larger.

<figure class="image-with-caption" style="float:left;">
    <img src="/assets/images/infinity_edge.png" width="310">
    <figcaption><em>An exodia item - 2nd most expensive in the game</em></figcaption>
</figure>

The way league is designed, there are just more multipliers available to the ADC than the tank. So far we covered just the two each: HP x Armour vs AD x AS. However ADCs have another key stat boost: **Crit% (critical strike chance)**. A critical strike deals 175% damage, and occurs (semi)-randomly at a rate of Crit% of the time. You can buy more Crit%, up to a cap of 100% (well, you could go over, but this won't help you...). If you have 100 Crit%, that would be a 1.75x offensive multiplier, that scales multiplicatively with the other AD and AS ones. In expectation, Crit% thus yields a (1 + 0.75 x Crit%)x multiplier. To add fuel to this fire is the item **Infinity Edge**, which increases that to a (1 + 1.15 x Crit%)x (i.e. critical strikes deal 215% damage). NB that the optimal time to buy Infinity Edge as an ADC then is only after having already accrued a decent amount of Crit%.

<figure class="image-with-caption" style="float:right;">
    <img src="/assets/images/mundo_cleaver.png" width="330">
    <figcaption><em>This ability deals 30% (current) health damage</em></figcaption>
</figure>

Tanks in league also have another multiplier source - **Magic Resist (MR)**! This is no boon, however, quite the opposite. Rather tanks must contend with a second main damage type: **Magic Damage**, against which armour is useless, and MR takes its place. Poor tanks must therefore split their HP cross multiplying gold budget between MR and Armour. At least investing in HP will work for all types of damage. Wait - some damaging abilities/attacks deal **%Health Damage**! This type of damage effectively ignores a tank's bonus HP defense multiplier. If you have 2x HP, well now %Health damage is also 2x'd! In a similar vein, some abilities deal **True Damage**, which ignores both Armour and MR!

Just when you thought tanks couldn't catch a break, typically after an ADC has invested in a decent amount of bonus AD, AS, and Crit%, they will buy an item like **Lord Dominik's Regards** that gives 40% **Armour penetration**. This actually means, in the limit of a tank with armour approaching infinity, a 1/0.6 = 1.66x multiplier (!). For heavy tanks of 2x or 3x armour multipliers this is more like 1.36x - 1.43x.

I've painted a pretty grim view for tanks, but in reality it's not all so extreme - the game developers balance things so that everyone gets to feel relevant at some point, and as mentioned before ADCs scale from a lower, weaker base in the early game, to a pretty strong point in the late game. There are also a few tank items that help to increase defense multipliers too. However it is true though that as the game goes on and players amass more item purchases, ADCs start to pull ahead with large multipliers - think around a 2x AD, 2x AS, 2x Crit (with Infinity Edge) and 1.4x armour penetration yielding 11.2x total, more than what they would have been doing with no items.

<!-- It would be unfair for ADCs to have all the fun/status, so the game devs explicitly balance things by making ADCs quite weak early in the game when they have few items. -->

In league this concept is called **Scaling** - and it's the games equivalent of an inevitable force of the world, like death and taxes. As the game goes on, different champions scale to different degrees, changing in relevance. A team without any champion who's able to effectively harness a chain of such multipliers will have an inferior source of scaling power to a better balanced opposing team. They will be forced to either seize control of the match and "snowball" in the early game, or risk being scaled into irrelevance in the late game.

Although in theory any champion can build a nice multiplicative set of damage items, most short ranged, melee champions lack both the complementary abilities to best harness these, and crucially the luxury of being able to dish out damage from a safe distance - they would have to expose themselves to enemy fire and get quickly blown up due to lacking any defensive stats.

Personally I do feel like giving characters in roles than ADCs the option to scale well into the late game, at the price of a weaker earlier game, sounds like it could be a net fun idea! Maybe though I just hate the feeling of playing a tank and getting melted in a late game teamfight, despite my best efforts and item purchases...


## Thresh - infinite scaling??

Finally to the more esoteric topic that sparked this whole blog post in the first place. This may be less appealing to a general audience than to a subset of league fans, so I will also give less background detail!

The powers of scaling are highly enticing - to have the fantasy of wielding ever greater powers with which to smite your enemies. However most scaling in league is capped out by the item inventory limit of 6 items. A smaller subset of champions do possess special abilities which allow them to scale infinitely! And none more so than... Thresh?!

<figure class="image-with-caption" style="float:left; width: 350px">
    <img src="/assets/images/Thresh.jpg">
    <figcaption><em>The spooky skeleton himself. Reminds me of the children's book character Skulduggery Pleasant</em></figcaption>
</figure>

Thresh is some kind of soul-devouring demon that can harvest souls from the corpses of vanquished foes (and smaller monsters and minions). Each soul increases his stats, an eye-popping 3 different ones: **Ability Power (AP)**, Armour, and his own special **On-hit Dmg**. AP is the equivalent to AD, but for magic damage dealing abilities (champions in league have abilities/spells which they can cast). 1 soul gives Thresh an extra 1 AP, 1 armour point, and 1.7 On-hit Dmg, with no upper limit! 1 AP is worth about 0.57 AD, and 1.7 On-hit Dmg is worth about 1.05 AD (by converting the stats of base items).

Most champions that have infinite scaling only really do in one dimension, e.g. Veigar gets only bonus AP. But Thresh has 3! His scaling powers are even more surprising given that 95% of the time that you see Thresh played, it is in the support role (neither tank nor damage dealer, rather a less directly useful role that eschews collecting gold, and has duties like scouting out the enemy team's positions, and sacrificing their lives to beneficially engage teamfights). Yet a careful Thresh player will have over 100 souls collected by mid to late-game - that's 2-3 items of pure value from additional stats! 

### Why Thresh isn't the hyper carry we dreamed of - but can still be strong!

Before we get too carried away, despite the indeed huge stat boosts Thresh can accrue, his kit is distinctly poorly designed to benefit from it, as I will explain. We can still theorycraft how best to leverage his powers, and end up with semi-decent scaling bruiser top viability.

#### Thresh is too short-ranged and immobile to solely be a damage dealer

We saw in [2v2 short vs long range role assignment](#2v2-and-the-evolution-of-role-assignment) that short-ranged champions just aren't good at building exclusively damage - they will get quickly blown up in a teamfight wasting their damage potential. The exception to this rule is actually assassins - if you're sneaky and mobile enough you can bypass the enemy frontline to quickly take out their backline, and maybe even escape afterwards too. Thresh is however both quite short ranged and immobile. The exception is Thresh's Q - it's long ranged, and actually offers some mobility as if you hit something you can grappling hook to it. However it's still single target damage, easy to dodge, and you actually CC yourself (Crowd Control - unable to move) while casting it, endangering yourself.

As an ADC, Thresh has a short range: 450 vs even short ranged ADCs like Sivir, Lucian with 500. He has a very high **Windup%** of 24% vs their 12%, 15% - comparable to clunky big melee attacking champions like Sion (25%) & Nautilus (30%). This makes him inefficient at stutter stepping (interspacing moving and attacking to DPS while retaining mobility). He is further uniquely sandbagged by a **Windup-modifier** of 0.25 - I think the only other champion in the game with one is Kalista at 0.75 - it means that his attack windup time is decreased at 25% efficiency by increased AS - meaning I believe that building AS actually makes his windup (immobile) time take an ever larger portion of his total attack animation. This feels terrible if you're used to normal ADCs, and at high AS to achieve good DPS he basically has to stand still while attacking.


#### Bruiser Toplane Thresh build

Thus Thresh is best built at least somewhat tanky. However with his inherent soul based bonus offense powers, and lacking the tool kit of a true tank, I argue he's best built as a bruuiser top-laner - mix of offense and defense! With all of his free on-hit damage, building a little AS is important. I generally take the Legend AS rune in the Precision rune tree, and avoid building any AS items early - they become more effective later in the game when he he's stacked more souls. To scale with this bonus AS, a bit of AD is important too. Thresh's E additionally gives a strong 210% bonus AD magic damage on your first attack, whereas the 1.7/soul on-hit magic damage applies to every auto attack.

<figure class="image-with-caption" style="width:95%; float:none; text-align: center; margin:0 auto;">
    <img src="/assets/images/Thresh_E.png" style="max-width:100%;height:auto;">
    <figcaption><em>Soul and AD scaling on-hit magic damage</em></figcaption>
</figure>

Finally, Thresh should build mostly HP and MR, and only a little Armour in the early game, before his soul scaling makes extra marginal armour quite useless (likewise bonus AP should be avoided). 

Putting this all together, I like to rush Heartsteel first item for its stacking HP (doubling down on the scaling fantasy). Next, Thresh really lacks good wave clear (his E active is ok, but also his only disengage so risky to use), so either Hollow Radiance (HP, MR) or Titanic Hydra (HP, AD) give a helping hand. Early steelcap boots for a bit of Armour and no more Armour items (maybe except Randuins lategame against heavy enemy crit). Third item I like Terminus - I think it might be optimal to maximise Thresh's hybrid magic and physical damage output, as well as giving some AS and AD. Guinsoo's rageblade is also very good for the AS and double on-hit dmg proc, possibly better than Terminus against enemies with lower resistances. Other items to consider are also Stattik Shiv (AD, AS, waveclear), Hullbreaker (AD, HP, split-push power), and Overlord's Bloodmail (HP, AD; AD scaling with bonus HP).

For runes I think press the attack and hail of blades are both good. Lethal tempo does give AS, but it's less efficient on Thresh than longer range ADCs - it may still good for long 1v1s in the toplane. Grasp has now been heavily nerfed for ranged champions so is inadvisable.

General tips when playing scaling bruiser Thresh toplane:
- like any ranged top, you're weak early before soul scaling builds up. Abuse your range to poke, but be careful of getting all-inned!
- souls are pretty valuable. Think of them like cannon minions (similar gold value!) - you don't want to miss one. You can throw your W lantern to pick them up from afar if in danger. Jungle camps also give souls so get some free stacks when your jungler is taking krugs/gromp (krugs especially good)

Jungle Thresh isn't great - his clear speed early is quite bad, and minion waves dropping souls when you're nearby is a little early warning sign to enemy laners! Spiderman Q-ing jungle camps over walls does feel good though, and his engage kit is still a strong ganking tool!


#### Some tweak ideas that could make Toplane / Jungle Thresh feel better
(Or even scaling botlane Thresh with co-carry suports like Senna (?))

1. Thresh's strange windup modifier just feels annoying when trying to stutter step, making utilising bonus AD and AS feel a little bad. I do get that it's meant to make his "not a projectile flay auto-attack" feel unique/realistic. I would actually propose making the longer windup% / modifier only apply on a fully charged E-passive attack (scaling with degree of charge) - so the extra clunkiness only comes at this first auto attack, and feels like a correlate of the nice bonus AD scaling damage; subsequent attacks could then be "normal".

2. I haven't confirmed, but I believe that if Thresh's Q one-shots the target (e.g. a ranged creep when he has a lot of souls lategame), he can't then spiderman grapple hook over to the dead corpse. Niche, but allowing an instant recast before hit to still grapple over could help in some escape situations

3. Thresh can't auto-attack after his Q connects (makes sense - his chain scythe thing is used for both). This can however feel frustrating when you're building on-hit Thresh. Perhaps a new auto-attack command during Q could automatically cancel the shackle stun/tug.

An aside general issue is that the league item system has scant support for scaling hybrid (magic and physical) damaging champions (Thresh being an example with his magic AP scaling abilities and magic on-hit damage). Terminus and Rageblade are the only two items, and both focus on the on-hit hybrid. Terminus is a blessing, as it gives a "buy 1 get 1 free" on Armour/MR resistance penetration (though the counterfactual is if hybrid champions were forced to buy 2 separate penetration items while most damage dealers only need the 1), but has to be slowly stacked up by auto attack on enemy champions. The item is rarely bought, and perhaps the chief mainstream usecase is on Kalista who doesn't even have any inherent magic damage in their kit... I believe that the game devs, noting the difficulty of balancing hybrid champions, decided to mostly discourage hybrid builds, leading to the removal of items like hextech gunblade.


## Thanks for reading!

Acknowledgements to all of my poor teammates who had to play with me as Thresh top. My peak rank in league was silver - trust my modelling and analysis skills rather than my gameplay!

<figure class="image-with-caption" style="width:95%; float:none; text-align: center; margin:0 auto;">
    <img src="/assets/images/Thresh_9_game_loss_streak.png" style="max-width:100%;height:auto;">
    <figcaption><em>Yes that is a 9 game loss streak. I'm conjecturing, but I think league thinks Thresh top is in fact support, gives good play grades even for poor performance (S, A etc.), and hence increases your ELO notwithstanding consecutive losses?</em></figcaption>
</figure>


<!-- First off, Thresh's abilities are piss poor at dealing consistent damage like conventional mages. All of his abilities are short range, and even worse his Q forces him to stand still while casting, making him a sitting duck. Thus, despite his built in AP generation, he'll never be a good mage. His abilities will hit a bit harder as he gains more souls, but it's not going to be a massive deal.

On the ADC front, Thresh is equally sandbagged. His attack range is 450, shorter than the shortest ranged ADCs like Sivir and Lucian with 500 range). He has a very high **Windup %** of 24% - the amount of time at the beginning of his attack he must stand still while attacking - movement commands during this window cancel the auto attack. This windup makes stutter stepping less effective on him - feeling slow and clunky on him. For comparison Sivir's is 12% and Lucian is 15%. 24% is higher even than non ADCs with clunky feeling auto attacks like Anivia. Very clunky melee attackers like Nautilus 30% and Sion 25% are still worse though! Actually the only ADC comparable is Nilah, who has 350 range with her Formless Blade Q procced, and a 22% windup. For Nilah and Thresh are near unique in being "ranged" but with a projectile-less auto attack animation - Nilah's whip and Thresh's flay - hence the long windup. Nonetheless, Nilah, unlike Thresh, has better mobility and self-protection granting abilities.

The nail in the coffin for ADC Thresh though is a mechanic which I think is unique to him - he has a **Windup modifier** of 0.25 (not present on other champions). This means that even if he builds attack speed, it will affect his windup time with only 1/4 effectiveness - normally champions building AS feel more fluid and better at stutter stepping with increased AS, whereas Thresh is kind of the opposite - and in order to maximise DPS effectively has to stand still.

Hence Thresh's bonus AP is maybe only 1/3 as useful as on mages, and his on-hit damage maybe a little less than 1/2 as useful as on an ADC. What's more his soul armour scaling is somewhat offset by another unique situation for him of having no built in armour scaling with levels (he has to get it all through souls). Thus 100 soul thresh is only maybe getting ~1+ item of bonus utility after all. 

Therefore, with his short range and bonus armour from souls, Thresh is destined to be a bruiser, though still able to get some good damage out from his infinite scalings. Carry thresh thus naturally lives in top lane, and excels at abusing his range advantage in early laning, pushing down towers, and winning 1v1s on the splitpush in the later game having scaled up offense and defense through his souls and item purchases.


On items to purchase, with large built in armour and 

Despite this, with his built in on-hit damage, investing in a little bonus AS is still worthwhile. Thresh's E also grants a first-auto-attack-hit large damage boost scaling with AD, so building complementary AD is also beneficial. But with the addition of all the free armour, carry Thresh is thus best played as a bruiser in top lane. Lacking the range to be a true ADC 



...

Thresh should by no means be built as a pure APC or ADC. In fact this would be counter to all that we've learnt. -->



<!-- First to explain the supposedly "faulty" math intuition why defense > offense in 2v2, if we pit two teams against each other:
- Team 1: (1x off, 1x def), (1x off, 2x def) i.e. a buffed tank
- Team : (2x off, 1x def), (1x off, 1x def) i.e. a buffed damage dealer 
Then viewed as a collective homogeneous teamwide health bar and DPS, the defensive team has e.g. 1000 + 2000 = 3000 HP and only 100 + 100 = 200 AD, whereas the offensive team has 1000 + 1000 = 2000 HP, and 200 + 100 = 300 AD. In the 1v1 case this was a complete draw, but now in the 2v2 case, because the offensive team's frontline champion will die first, they will actually suffer a DPS loss (of 100 AD). Yes, once the super 2000 HP tank on the defensive team dies a period of time later, 

#### Hybrid champs suck

You can't really access scalings. Terminus is nice but ehhh...
Also why does terminus give resists. And only works on attacks.

There is no corresponding "defense attack" tradeoff that means that building hybrid makes sense.
Thresh is different - he does hybrid damage, but doesn't build AP and AD. Maybe only a little AD even!



The slightly more opaque viewpoint is of 50 armour as providing (physical) damage reduction at a rate of $$\frac{100}{100 + 50}$$ - thus if an enemy baby level 1 Ezreal with 60 AD attacks us, we will only take two thirds of that, 40 damage to our 1000 HP bar.

However for our calculations it will be more revealing to take the traditional "damage reduction" point of view - that 50 armour means Ezreal takes $$


To avoid this symmetrical duel ending in death on both sides, we clearly need to tweak the stats a little. Luckily, buying items which grant bonus Attack Damage, Health, Armour and more, is part of League's bread and butter. 


When I played league, I would always obssess about 

I barely even play league anymore, however still now, as when I used to, I sometimes find myself obssessively fantasising and theory crafting about certain 

- 1v1 analysis
- 2v2 analysis
- try to calculate winner for n v n with vectors of health and dps
- stats basics: ad, as, health, armour etc.
- try to do scaling analyses
- dive into some fun champs like thresh, tahm kench
-  -->

<br>
----------------------------------