# HW_4_2

#!/usr/bin/env python3
# -*- coding: utf-8 -*-
"""
Created on Wed Feb 28 15:29:12 2024

@author: fredpvellla
"""

# main-1.py ###################

'''
CSC-103 - Homework 4_2 professor Auerbeck Fred P Vella
For this assignment, we will create a script what will 
generate a random team of six pokemon and how many versions
they appeared in. In the graph, they will be represented by 
Their actual names. 
'''

# First, we import all relevent functions and libraries. 

import pandas as pd
import seaborn as sb
import matplotlib.pyplot as plt

Pok = pd.read_csv("data/poke_by_game.csv")

print(Pok)

print(Pok.loc[Pok['pokemon_id']==1])

print(Pok.loc[Pok['pokemon_id']==1].groupby('pokemon_id').count())


print(Pok.loc[Pok['pokemon_id']==1,['pokemon_id','version_id']].groupby('pokemon_id').count().reset_index())

bulba = Pok.loc[Pok['pokemon_id']==1,['pokemon_id','version_id']].groupby('pokemon_id').count().reset_index()

print(bulba)

sb.barplot(data=bulba,x='pokemon_id',y='version_id')

plt.xlabel("Pokemon",weight='bold')
plt.ylabel("Version Count",weight='bold')
plt.title("Pokemon Appearences",fontsize=20)

plt.show()

morepoke = (Pok.sample(4)),[['pokemon_id','version_id']] .groupby('pokemon_id').count().reset_index()

# print(morepoke)

#sb.barplot(data=morepoke,x='pokemon_id',y='version_id')
sb.barplot(data=morepoke,x=morepoke.index,y='version_id')


# Main-2.py #########################

# Next, we will create a python script that will ask for 
# A pokemon by name. And we will create a graph to illustrate
# Our findings. 

import pandas as pd
import seaborn as sb
import matplotlib.pyplot as pl

import warnings
warnings.filterwarnings("ignore", "use_inf_as_na")

pok = pd.read_csv("data/pokemon.csv")
pokspe = pd.read_csv("data/pokemon_species.csv")
exp = pd.read_csv("data/experience.csv")

ids = pokspe.sample(1)['identifier']

Pokemon1 = (pokspe.merge(exp, how='left', left_on='growth_rate_id', 
              right_on='growth_rate_id', 
              suffixes=('_spec','_exp')))

Pokemon1 = Pokemon1[['identifier','level','species_id']]

bulbasar1 = Pokemon1['identifier'].isin(ids)

squirtle1 = Pokemon1[bulbasar1][['identifier','level','species_id']]

sb.lineplot(data = squirtle1 ,x='level',y='experience')

pl.ticklabel_format(style='plain', axis='y')

fig, ax = plt.subplots()
ids=['charmander','bulbasaur','mewtwo']

for i in ids:
    chk=Pokemon1['identifier'].isin([i])
    newdat=Pokemon1[bulbasar1][['identifier','level','species_id']]
    (sb.lineplot(data=newdat,x='level',y='experience',
                 legend='brief',label=str(i)))

pl.ticklabel_format(style='plain', axis='y')

fig, ax = pl.subplots(1, 3)
ids=['charmander','bulbasaur','mewtwo']

a=0
for i in ids:
    morepoke=(pok.loc[pok['identifier'].isin([i]),
                    ['identifier','base_experience']])
    (sb.barplot(ax=ax[a],data=morepoke,x='identifier',
                y='base_experience'))
    a+=1

fig, ax = pl.subplots(1, 3, sharey=True)
a=0
for i in ids:
    morepoke=pok.loc[pok['identifier'].isin([i]),['identifier','base_experience']]
    sb.barplot(ax=ax[a],data=morepoke,x='identifier',y='base_experience')
    a+=1

# Main-3.py ################

# Currently, we will create a list for pokemon and it will be 
# illustrated in a bargraph. 
# Each team member will be given a name and grade assigned to 
# Them and their respective part in the game. 

import pandas as pd
import seaborn as sb
import matplotlib.pyplot as plt

# Pok = pd.read_csv("data/poke_by_game.csv")

pokelist = pd.read_csv("data/pokemon.csv")

print(pokelist)

print(pokelist.loc[pokelist['base_experience']==1])

print(pokelist.loc[pokelist['base_experience']==1].groupby('identifier').count())


print(pokelist.loc[pokelist['base_experience']==1,['identifier','base_experience']].groupby('identifier').count().reset_index())

bulba = pokelist.loc[pokelist['base_experience']==1,['identifier','base_experience']].groupby('identifier').count().reset_index()

print(bulba)

sb.barplot(data=bulba,x='identifier',y='base_experience')

plt.xlabel("Team Member Name",weight='thin')
plt.ylabel("Team Member Grade",weight='thin')
plt.title("Pokemon Teams",fontsize=10)

plt.show()

pokevariables = (pokelist.sample(4)),[['base_experience','identifier']] .groupby('identifier').count().reset_index()
