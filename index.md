### DSC 80 Project
***By Katelyn Abille and Aneesh Pamula*** <br> <br>
Curated by students of DSC 80, this academic project is a continuation of our previous exploratory data analysis performed on League of Legends 2022 competitive matche data. Our website stands as a holistic report of our findings, demonstrating the process of ...
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
League of Legends is a game that features a very diverse cast of over 160 characters, or champions, who each have their own unique playstyle. Certain champions do have similar playstles though, and they are grouped into groups called **classes**. 

League features six main classes for its characters, each with its own unique strengths and weaknesses:

#### **Tanks**

<img src="assets/img/tank_clip.gif" alt="clip of tank gameplay" width="600" height="338">

Tanks are very difficult to kill and excel at disrupting enemies and forcing attention to themselves, but they often don't deal a lot of damage (i.e. Shen shown above)

#### **Fighters**

<img src="assets/img/fighter_clip.gif" alt="clip of fighter gameplay" width="600" height="338">

Fighters are great at taking long fights with enemies due to their consistent damage and resistances, but often lack the ability to deal with long-ranged opponents.

#### **Assassins**

<img src="assets/img/assassin_clip.gif" alt="clip of assassin gameplay" width="600" height="338">

like Akali and Yone, can deal a huge burst of damage to a single target in a short time and have great mobility, but they often lack defenses and lack sustained damage after the initial burst.

#### **Mages**

<img src="assets/img/mage_clip.gif" alt="clip of mage gameplay" width="600" height="338">

like Lux and Viktor, can damage enemies from a distance with area-of-effect abilities that can hit multiple targets, but these abilities can be dodged by champions with high mobility and must take time to recharge before being used again.

#### **Marksmen**

<img src="assets/img/mage_clip.gif" alt="clip of mage gameplay" width="600" height="338">

like Caitlyn and Jinx, pressure enemies from a distance with their long range and sustained damage, but often die very quickly once enemies get within reach of them.

#### **Supports**

<img src="assets/img/supp_clip.gif" alt="clip of support gameplay" width="600" height="338">

like Sona and Janna, can offer a wide range of utility such as stuns, healing, and damage buffs, but they do not do very much damage and are often very weak without a teammate alongisde them.

<br>
<br>

Due to different classes having different affinities, the distributions of their post-game stats also tends to be quite different. For example, assassins and marksmen may have a very high number of kills, while supports may tend to have more assists. In this notebook, we will look to create a model that predicts which class of champion a player was playing, given their post-game stats.

### **Description of Columns** <a name="col_desc"></a>

## **Baseline Model** <a name="baseline_model"></a>

## **Final Model** <a name="final_model"></a>

## **Fairness Analysis** <a name="fairness"></a>

