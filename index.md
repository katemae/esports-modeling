### DSC 80 Project
***By Katelyn Abille and Aneesh Pamula*** <br> <br>
Curated by students of DSC 80, this academic project is a continuation of our previous exploratory data analysis performed on League of Legends 2022 competitive matche data. Our website stands as a holistic report of our findings, demonstrating the process of cleaning, transforming, and fitting our data for a prediction model, as well as assessing the fairness of our model.
> Our exploratory data analysis on this dataset can be found here:
> <br> [An Analysis of Renekton's Presence During the 2022 Season of Professional League of Legends](https://katemae.github.io/esports-data-report/).

<br>

### Table of contents
1. [Framing the Problem](#frame_problem) <br>
    a. [Description of Columns](#col_desc)
2. [Baseline Model](#baseline_model) <br>
3. [Final Model](#final_model) <br>
4. [Fairness Analysis](#fairness)<br>

## **Framing the Problem** <a name="frame_problem"></a>
League of Legends is a game that features a very diverse cast of over 160 characters, or champions, who each have their own unique abilities and techniques. Nonetheless, with over 160 champions, some will have similar playstyles and are thus grouped into **classes**. 

League features six main classes for its champions, each with its own unique strengths and weaknesses:

#### **Tanks**

<img src="assets/img/tank_clip.gif" alt="clip of tank gameplay" width="600" height="338" class="clip">

Tanks, like Shen (shown above), are very difficult to kill and excel at disrupting enemies and forcing attention to themselves, but they often don't deal a lot of damage.

#### **Fighters**

<img src="assets/img/fighter_clip.gif" alt="clip of fighter gameplay" width="600" height="338" class="clip">

Fighters, like Renekton (shown above), are great at taking long fights with enemies due to their consistent damage and resistances, but often lack the ability to deal with long-ranged opponents.

#### **Assassins**

<img src="assets/img/assassin_clip.gif" alt="clip of assassin gameplay" width="600" height="338" class="clip">

Assassins, like Kayn (shown above), can deal a huge burst of damage to a single target in a short time and have great mobility, but they often lack defenses and lack sustained damage after the initial burst.

#### **Mages**

<img src="assets/img/mage_clip.gif" alt="clip of mage gameplay" width="600" height="409" class="clip">

Mages, like Lux (shown above), can damage enemies from a distance with area-of-effect abilities that can hit multiple targets, but these abilities can be dodged by champions with high mobility and must take time to recharge before being used again.

#### **Marksmen**

<img src="assets/img/mark_clip.gif" alt="clip of marksmen gameplay" width="600" height="409" class="clip">

Marksmen, like Jinx (shown above), pressure enemies from a distance with their long range and sustained damage, but often die very quickly once enemies get within reach of them.

#### **Supports**

<img src="assets/img/supp_clip.gif" alt="clip of support gameplay" width="600" height="409" class="clip">

Supports, like Lulu (shown above), can offer a wide range of utility such as stuns, healing, and damage buffs, but they do not do very much damage and are often very weak without a teammate alongside them.

<br>

Due to different classes having different affinities, the distributions of their post-game statistics also tends to be quite different. For example, assassins and marksmen may have a very high number of kills, while supports may tend to have more assists. In this notebook, we will look to create a model that predicts which class of champion a player was playing given their post-game statistics.

### **Description of Columns** <a name="col_desc"></a>

The post-game statistics that we will be using are the following:

* `'position'`: The position that the champion was played in. This could be top, jungle (abbreviated to jng), middle (abbreviated to mid), bottom, (abbreviated to bot), and support (abbreviated to sup).

* `'gamelength'`: The length of the game in seconds.

* `'kills'`, `'deaths'`, and `'assists'`: `'kills'` represents the number of times the player scored a kill on an opponent, while `'deaths'` represents the number of times the player died. `'assists'` represents the number of times the player aided their teammates in killing another opponent without actually scoring the kill themselves.

* `'doublekills'`, `'triplekills'`, `'quadrakills'`, and `'pentakills'`: The number of times a player killed two, three, four or five (respectively) players in quick succession.

* `'dpm'`, `'damagetakenperminute'`, and `'damagemitigatedperminute'`: The amount of damage dealt, taken, and mitigated (that is, reduced with shields, healing, armor, etc.), all averaged over the length of the game in minutes.

* `'wpm'`, `'wcpm'`, `'controlwardsbought'`, and `'vspm'`: The number of wards (objects that grant vision) placed and destroyed, averaged over the length of the game in minutes, and the number of control wards (a stronger version of wards) bought. `'vspm'` is the vision score (a number that reflects how much a player granted vision to their team and denied it from the opponent) averaged over the length of the game in minutes.

* `'minionkills'` and `'monsterkills'`: The number of minions and monsters killed by the player. Minions spawn in the top, middle, and bottom lanes, while monsters spawn in the jungle.

* `'goldat15'`, `'xpat15'`, `'csat15'`,`'killsat15'`, `'assistsat15'`, and `'deathsat15'`: Various statistics at the 15 minute mark of the game. Gold is a resource that allows players to buy items, and experience (abbreviated to xp here) allows champions to strengthen their abilities and grow more powerful. CS is a statistic that reflects the number of minions and monsters a player has killed.

* `'golddiffat15'`, `'xpdiffat15'`, `'csdiffat15'`: The difference between the player's gold and their lane opponent's gold, experience, and CS at the 15 minute mark.

It is also important to note that `'kills'`, `'deaths'`, and `'assists'` vary from `'killsat15'`, `'assistsat15'`, and `'deathsat15'`. Statistics within the first 15 minutes of a game are vital to our predictions and to a game's overall outcome, as some champions have different early game strategies.

Thus, we will keep all the above columns in our dataset, along with the column corresponding to the champion class to test our model on.

<br>

Before we proceed, however, we must first address some of the missing values in our dataset. The vast majority of the missing values are missing by design (MD) because certain leagues do not keep track of certain statistics. For example, leagues like LPL and LDL do not keep track of statistics like gold difference at 15 minutes, or damage mitigated per minute. These statistics are essential to make our predictions, since sometimes getting an early lead over the opponent or mitigating damage is a key part of the playstle of a class. 

Because of this, we will be removing the rows corresponding to leagues that do not store the data we require in the dataset used for our model. Specifically, leagues 'LPL', 'LDL', 'WLDs', and 'DCup' have been completely removed from our data.

## **Baseline Model** <a name="baseline_model"></a>

## **Final Model** <a name="final_model"></a>

## **Fairness Analysis** <a name="fairness"></a>

