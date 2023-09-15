#%%
import time
import requests as req
import pandas as pd
from  bs4 import BeautifulSoup
import base64
from datetime import datetime
import pytz

url = 'https://liquipedia.net/counterstrike/Main_Page'

html = req.get(url)

bs_obj = BeautifulSoup(html.text, 'lxml')



match_Time = [i.text.split() for i in bs_obj.find('tbody').find_all_next('td', class_='match-filler')]
match_Teams_Left = [i.text.replace(' \n', ' ') for i in bs_obj.find('tbody').find_all_next('td', class_='team-left')]
match_Teams_Right = [i.text.replace('\n', ' ') for i in bs_obj.find('tbody').find_all_next('td', class_='team-right')]

hr = []

horarios = []

if match_Teams_Right:
    for i in match_Time:
        horarios.append(i[4])

    df = pd.DataFrame( {"Time Left": match_Teams_Left,"x":'x',
                    "Time Right": match_Teams_Right,
                    "Horário": horarios,
                    })
##

htc = []
for ia in horarios:
    htc.append(ia)


df['Horário'] = pd.to_datetime(df['Horário'], format='%H:%M')

brasil_timezone = pytz.timezone('America/Sao_Paulo')
df['Horario_fuso'] = df['Horário'].dt.tz_localize(brasil_timezone)
df['Horário'] = df['Horário'].dt.strftime('%H:%M')


df.head(30)

##with pd.ExcelWriter('Match_Games_CS.xlsx',
##                    mode='a', if_sheet_exists="new") as writer:  
##    df.to_excel(writer, sheet_name='Sheet1')
##df.to_excel('Match_Games_CS.xlsx')
# %%
