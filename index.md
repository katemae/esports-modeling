## DSC 80 Project
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

<br>

## **Framing the Problem** <a name="frame_problem"></a>
League of Legends is a game that features a very diverse cast of over 160 characters, or champions, who each have their own unique abilities and techniques. Nonetheless, with over 160 champions, some will have similar playstyles and are thus grouped into **classes**. 

League features six main classes for its champions, each with its own unique strengths and weaknesses:

#### **Tanks**

<img src="assets/img/tank_clip.gif" alt="clip of tank gameplay" width="600" height="338" class="clip">

Tanks, like Shen (shown above), are very difficult to kill and excel at disrupting enemies and forcing attention to themselves, but they often do not deal a lot of damage.

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

Due to different classes having different affinities, the distributions of their post-game statistics also tends to be quite different. For example, assassins and marksmen may have a very high number of kills, while supports may tend to have more assists. **Because of this, we have chosen for our report to create a model that predicts which class of champion a player was playing given their post-game statistics. To do so, we have chosen to use a multiclass classification.**

### **Description of Columns** <a name="col_desc"></a>

Because we are predicting class based on *post-game* statistics, we have free reign on all columns since they are within the *"time of prediciton"*. The post-game data that we will be using are the following:

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

Thus, we will keep all the above columns in our dataset, along with the column corresponding to a champion's class to test our model on.

<br>

Before we proceed, however, we must first address some of the missing values in our dataset. The vast majority of the missing values are missing by design (MD) because certain leagues do not keep track of certain statistics. For example, leagues like LPL and LDL do not keep track of statistics like gold difference at 15 minutes, or damage mitigated per minute. These statistics are essential to make our predictions, since sometimes getting an early lead over the opponent or mitigating damage is a key part of the playstle of a class as described earlier. 

Because of this, we will be removing the rows corresponding to leagues that do not store the data we require in the dataset used for our model. Specifically, leagues 'LPL', 'LDL', 'WLDs', and 'DCup' have been completely removed from our data.

<br>

| class    |   gamelength | position   |   kills |   deaths |   assists |   doublekills |   triplekills |   quadrakills |   pentakills |     dpm |   damagetakenperminute |   damagemitigatedperminute |    wpm |   wcpm |   controlwardsbought |   vspm |   minionkills |   monsterkills |   goldat15 |   xpat15 |   csat15 |   golddiffat15 |   xpdiffat15 |   csdiffat15 |   killsat15 |   assistsat15 |   deathsat15 |
|:---------|-------------:|:-----------|--------:|---------:|----------:|--------------:|--------------:|--------------:|-------------:|--------:|-----------------------:|---------------------------:|-------:|-------:|---------------------:|-------:|--------------:|---------------:|-----------:|---------:|---------:|---------------:|-------------:|-------------:|------------:|--------------:|-------------:|
| Fighter  |         1713 | top        |       2 |        3 |         2 |             0 |             0 |             0 |            0 | 552.294 |               1072.4   |                    777.793 | 0.2802 | 0.2102 |                    5 | 0.9107 |           220 |             11 |       5025 |     7560 |      135 |            391 |          345 |           14 |           0 |             1 |            0 |
| Fighter  |         1713 | jng        |       2 |        5 |         6 |             0 |             0 |             0 |            0 | 412.084 |                944.273 |                    650.158 | 0.2102 | 0.6305 |                    6 | 1.6813 |            33 |            115 |       5366 |     5320 |       89 |            541 |         -275 |          -11 |           2 |             3 |            2 |
| Assassin |         1713 | mid        |       2 |        2 |         3 |             0 |             0 |             0 |            0 | 499.405 |                581.646 |                    227.776 | 0.6655 | 0.2452 |                    7 | 1.0158 |           177 |             16 |       5118 |     6942 |      120 |           -475 |          153 |            1 |           0 |             3 |            0 |
| Marksman |         1713 | bot        |       2 |        4 |         2 |             0 |             0 |             0 |            0 | 389.002 |                463.853 |                    218.879 | 0.4203 | 0.2102 |                    4 | 0.8757 |           208 |             18 |       5461 |     4591 |      115 |           -793 |        -1343 |          -34 |           2 |             1 |            2 |
| Tank     |         1713 | sup        |       1 |        5 |         6 |             0 |             0 |             0 |            0 | 128.301 |                475.026 |                    490.123 | 1.0158 | 0.4904 |                   11 | 2.4168 |            42 |              0 |       3836 |     3588 |       28 |            443 |         -497 |            7 |           1 |             2 |            2 |
| ...      |          ... | ...        |     ... |      ... |       ... |           ... |           ... |           ... |          ... |     ... |                    ... |                        ... |    ... |    ... |                  ... |    ... |           ... |            ... |        ... |      ... |      ... |            ... |          ... |          ... |         ... |           ... |          ... |
| Tank     |         1680 | top        |       3 |        5 |         0 |             1 |             0 |             0 |            0 | 259.964 |                864.286 |                   1027.04  | 0.3214 | 0.1786 |                    1 | 0.8571 |           162 |              0 |       4948 |     6973 |      108 |          -1537 |         -645 |          -15 |           2 |             0 |            1 |
| Fighter  |         1680 | jng        |       2 |        8 |         4 |             0 |             0 |             0 |            0 | 273.857 |                992.321 |                    948.286 | 0.6429 | 0.1071 |                   11 | 1.2143 |            18 |            124 |       4798 |     5504 |       93 |           -403 |          706 |           13 |           1 |             4 |            3 |
| Assassin |         1680 | mid        |       2 |        3 |         3 |             0 |             0 |             0 |            0 | 424.107 |                835.857 |                    580.75  | 0.3571 | 0.1071 |                    5 | 1      |           231 |              8 |       5283 |     7347 |      122 |            342 |          270 |           -4 |           1 |             2 |            0 |
| Marksman |         1680 | bot        |       2 |        1 |         3 |             0 |             0 |             0 |            0 | 386.321 |                332.643 |                    199.143 | 0.4643 | 0.2143 |                    5 | 1.0357 |           224 |             12 |       5012 |     5012 |      114 |           -475 |         -866 |          -11 |           1 |             1 |            0 |
| Mage     |         1680 | sup        |       0 |        5 |         4 |             0 |             0 |             0 |            0 | 243.964 |                553.964 |                    386.679 | 0.8929 | 0.2143 |                    8 | 2.1786 |            16 |              0 |       3192 |     3586 |        2 |           -140 |           19 |           -1 |           0 |             3 |            2 |

Now our data is ready for predictive modeling!

## **Baseline Model** <a name="baseline_model"></a>

Before working with all our columns, let's begin by creating a baseline model using only five columns from our dataset to predict the champion class: `'gamelength'`, `'kills'`, `'deaths'`, `'assists'`, and `'position'`. These statistics are fairly easy to explain to someone who does not know much about League of Legends in contrast to statistics like gold and experience difference. Additionally, these five are a great baseline since they are likely correlated with the class of a champion and are basic statistics easily found for all matches, not just competitive games.

* `'position'`: We include this **nominal** bacause each position has certain characteristics that make some classes stronger in those position than others. For example, fighters are often played in the top lane because they are more self sufficient and do not need the help of their teammates, who are spread throughout the rest of the map. Meanwhile, assassins are often played in the jungle because their high mobility allows them to get around the map faster. 

* `'gamelength'`: We include this **quantitative** feature because different classes tend to be stronger at different levels of the game. For example, a fighter or assassin may contribute the majority of their team's damage in a short (around 25 minutes or less) game, while a marksman will likely contribute the majority of their team's damage in longer games.

* `'kills'`, `'deaths'`, and `'assists'`:  We include these **quantitative** features because some classes prioritize aiding their teammates in killing an enemy, while other classes want to be the ones to score those kills. For example, a support or tank champion may focus more on setting up kills for their assassin or marksman teammates rather than actually going for the kills themselves, leading to a low number of kills but high number of assists. Classes who take on more fights are also more prone to deaths.

## **Final Model** <a name="final_model"></a>

## **Fairness Analysis** <a name="fairness"></a>

