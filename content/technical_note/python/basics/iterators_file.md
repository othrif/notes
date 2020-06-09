---
title: "Load data in chunks"
date: 2020-04-12T14:41:32+02:00
author: "Othmane Rifki"
type: technical_note
draft: false
---
### Loading data in chunks
the data we have to process reaches a size that is too much for a computer's memory to handle. A solution to this is to process an entire data source chunk by chunk, instead of a single go all at once.


```python
import pandas as pd
counts_dict = {}
csv_url='../datasets/tweets.csv'
pd.set_option('display.max_colwidth',-1)
# Iterate over the file chunk by chunk
for chunk in pd.read_csv(csv_url, chunksize=10):
    print(chunk['text'])
    # Iterate over the column in DataFrame
    for entry in chunk['lang']:
        if entry in counts_dict.keys():
            counts_dict[entry] += 1
        else:
            counts_dict[entry] = 1

# Print the populated dictionary
print(counts_dict)

```

    0    RT @bpolitics: .@krollbondrating's Christopher Whalen says Clinton is the weakest Dem candidate in 50 years https://t.co/pLk7rvoRSn https:/…
    1    RT @HeidiAlpine: @dmartosko Cruz video found.....racing from the scene.... #cruzsexscandal https://t.co/zuAPZfQDk3                          
    2    Njihuni me Zonjën Trump !!! | Ekskluzive https://t.co/4KmsQi47VD                                                                            
    3    Your an idiot she shouldn't have tried to grab trump after the fact she's an idiot https://t.co/lpASyeNVpG                                  
    4    RT @AlanLohner: The anti-American D.C. elites despise Trump for his America-first foreign policy. Trump threatens their gravy train. https:…
    5    RT @BIackPplTweets: Young Donald trump meets his neighbor  https://t.co/RFlu17Z1eE                                                          
    6    RT @trumpresearch: @WaitingInBagdad @thehill Trump supporters have selective amnisia.                                                       
    7    RT @HouseCracka: 29,000+ PEOPLE WATCHING TRUMP LIVE ON ONE STREAM!!!\n\nhttps://t.co/7QCFz9ehNe                                             
    8    RT @urfavandtrump: RT for Brendon Urie\nFav for Donald Trump https://t.co/PZ5vS94lOg                                                        
    9    RT @trapgrampa: This is how I see #Trump every time he speaks. https://t.co/fYSiHNS0nT                                                      
    Name: text, dtype: object
    10    RT @trumpresearch: @WaitingInBagdad @thehill Trump supporters have selective amnisia.                                                        
    11    RT @Pjw20161951: NO KIDDING: #SleazyDonald just attacked Scott Walker for NOT RAISING TAXES in WI! #LyinTrump\n#NeverTrump  #CruzCrew  https…
    12    RT @urfavandtrump: RT for Brendon Urie\nFav for Donald Trump https://t.co/PZ5vS94lOg                                                         
    13    RT @ggreenwald: The media spent all day claiming @SusanSarandon said she might vote for Trump. A total fabrication, but whatever... https:/… 
    14    RT @Pjw20161951: NO KIDDING: #SleazyDonald just attacked Scott Walker for NOT RAISING TAXES in WI! #LyinTrump\n#NeverTrump  #CruzCrew  https…
    15    RT @trapgrampa: This is how I see #Trump every time he speaks. https://t.co/fYSiHNS0nT                                                       
    16    RT @mitchellvii: So let me get this straight.  Any reporter can assault Mr Trump at any time and Corey can do nothing?  Michelle is clearly… 
    17    Your an idiot she shouldn't have tried to grab trump after the fact she's an idiot https://t.co/lpASyeNVpG                                   
    18    RT @paulbenedict7: How #Trump Sacks RINO Strongholds by Hitting Positions Held by Dems and GOP https://t.co/D7ulnAJhis   #tcot #PJNET https… 
    19    RT @DRUDGE_REPORT: VIDEO:  Trump emotional moment with Former Miss Wisconsin who has terminal illness... https://t.co/qt06aG9inT             
    Name: text, dtype: object
    20    #HillYes #ImWithHer #RollHillary @HillaryClinton  https://t.co/OwYXKIalyn                                                                   
    21    RT @ggreenwald: The media spent all day claiming @SusanSarandon said she might vote for Trump. A total fabrication, but whatever... https:/…
    22    RT @DennisApgar: Thank God I seen Trump at first stop in Wisconsin media doesn't know how great he is, advice watch live streaming https://…
    23    RT @paulbenedict7: How #Trump Sacks RINO Strongholds by Hitting Positions Held by Dems and GOP https://t.co/D7ulnAJhis   #tcot #PJNET https…
    24    RT @DRUDGE_REPORT: VIDEO:  Trump emotional moment with Former Miss Wisconsin who has terminal illness... https://t.co/qt06aG9inT            
    25    RT @DennisApgar: Thank God I seen Trump at first stop in Wisconsin media doesn't know how great he is, advice watch live streaming https://…
    26    RT @mitchellvii: So let me get this straight.  Any reporter can assault Mr Trump at any time and Corey can do nothing?  Michelle is clearly…
    27    Trump won't do a yes ma'am for this.  https://t.co/r3WkGZDjPH                                                                               
    28    RT @sciam: Trump's idiosyncratic patterns of speech are why people tend either to love or hate him https://t.co/QXwquVgs3c https://t.co/P9N…
    29    #HillYes #ImWithHer #RollHillary @HillaryClinton  https://t.co/OwYXKIalyn                                                                   
    Name: text, dtype: object
    30    RT @Norsu2: Nightmare WI poll for Ted Cruz has Kasich surging: Trump 29, Kasich 27, Cruz 25. https://t.co/lJsgbLYY1P #NeverTrump                
    31    RT @thehill: WATCH: Protester pepper-sprayed point blank at Trump rally https://t.co/B5f65Al9ld https://t.co/skAfByXuQc                         
    32    RT @sciam: Trump's idiosyncratic patterns of speech are why people tend either to love or hate him https://t.co/QXwquVgs3c https://t.co/P9N…    
    33    RT @ggreenwald: The media spent all day claiming @SusanSarandon said she might vote for Trump. A total fabrication, but whatever... https:/…    
    34    Opinion: The big story is -- Sanders https://t.co/9Z9ZVnZ1Zi                                                                                    
    35    GOP speechwriter: By November, Ivanka will be voting for Clinton | TheHill https://t.co/tUT7LpEHak                                              
    36    This dude must have some serious issues  https://t.co/ojYaDpnSoe                                                                                
    37    RT @DebbieStout5: Wow! Last I checked it was just 12 points &amp; that wasn't more than a day ago. Oh boy Trump ppl might want to rethink🤔 http…
    38    RT @tyleroakley: i'm a messy bitch, but at least i'm not voting for trump                                                                       
    39    RT @vandives: Trump supporters r tired of justice NOT being served. There's no justice anymore. Hardworking Americans get screwed. That's n…    
    Name: text, dtype: object
    40    Opinion: The big story is -- Sanders https://t.co/9Z9ZVnZ1Zi                                                                                  
    41    RT @AP: BREAKING: Trump vows to stand by campaign manager charged with battery, says he does not discard people.                              
    42    It Cometh from the Pit. And Hath a Knout https://t.co/iyF5HPDJNU\n#Trump\n#Election2016 https://t.co/W4ZXQfUHi8                               
    43    RT @AP: BREAKING: Trump vows to stand by campaign manager charged with battery, says he does not discard people.                              
    44    @footlooseracer @hautedamn @z0mgItsHutch So much sadness and pure stupidity from the people who support Trump. Very sad.                      
    45    RT @urfavandtrump: RT for Jerrie (Little Mix)\nFav for Donald Trump https://t.co/nEVxElW6iG                                                   
    46    RT @urfavandtrump: RT for Jerrie (Little Mix)\nFav for Donald Trump https://t.co/nEVxElW6iG                                                   
    47    PSA: @piersmorgan is a asshole. https://t.co/2Gjp2NPo0w                                                                                       
    48    RT @NoahCRothman: When Walker was fighting for reforms, Trump was defending unions and collective bargaining privileges https://t.co/e1UWNN…  
    49    RT @RedheadAndRight: Report: Secret Service Says Michelle Fields Touched Trump https://t.co/c5c2sD8VO2\n\nThis is the only article you will n…
    Name: text, dtype: object
    50    Me listening to DONALD TRUMP saying that he has no small hands ( allegedly ) https://t.co/LhUYdi8Vgf https://t.co/IwD9Lg84HY                  
    51    RT @AIIAmericanGirI: VIDEO=&gt; Anti-Trump Protester SLUGS Elderly Trump Supporter in the Face\nhttps://t.co/GeEryMDuDY                       
    52    RT @NoahCRothman: When Walker was fighting for reforms, Trump was defending unions and collective bargaining privileges https://t.co/e1UWNN…  
    53    PSA: @piersmorgan is a asshole. https://t.co/2Gjp2NPo0w                                                                                       
    54    RT @JusticeRanger1: @realDonaldTrump @Pudingtane @DanScavino @GOP @infowars @EricTrump \nURGENT PUBLIC TRUMP ALERT:\nCOVERT KILL MEANS https:…
    55    RT @AIIAmericanGirI: VIDEO=&gt; Anti-Trump Protester SLUGS Elderly Trump Supporter in the Face\nhttps://t.co/GeEryMDuDY                       
    56    Susan Sarandon Shares Interesting Opinion on Donald Trump https://t.co/Gjzkpr5mrH                                                             
    57    RT @RedheadAndRight: Report: Secret Service Says Michelle Fields Touched Trump https://t.co/c5c2sD8VO2\n\nThis is the only article you will n…
    58    @jbrading dude you are annoying af. Deion sanders fucking hates you guys.                                                                     
    59    RT @JusticeRanger1: @realDonaldTrump @Pudingtane @DanScavino @GOP @infowars @EricTrump \nURGENT PUBLIC TRUMP ALERT:\nCOVERT KILL MEANS https:…
    Name: text, dtype: object
    60    RT @Schneider_CM: Trump says nobody had ever heard of executive orders before Obama started signing them. Never heard of the Emancipation P…
    61    RT @RonBasler1: @DavidWhitDennis @realDonaldTrump @tedcruz \n\nCRUZ SCREWS HOOKERS\n\nCRUZ / CLINTON                                        
    62    Susan Sarandon Shares Interesting Opinion on Donald Trump https://t.co/Gjzkpr5mrH                                                           
    63    @realDonaldTrump Its too bad Cruz doesn't have enough brains to realize he's being led down the primrose lane to be neutered by the Elites!!
    64    RT @DonaldsAngel: Former Ms. WI just said that she is terminally ill but because of Trump pageant, her 7 yr. old son has his college educat…
    65    Photo: #Donald #Trump #Protest in #Milwaukee ahead of CNN GOP #Town #Hall with #Trump, Ted #Cruz, ... https://t.co/8NOguZUSCK               
    66    RT @Schneider_CM: Trump says nobody had ever heard of executive orders before Obama started signing them. Never heard of the Emancipation P…
    67    @jbrading dude you are annoying af. Deion sanders fucking hates you guys.                                                                   
    68    RT @DonaldsAngel: Former Ms. WI just said that she is terminally ill but because of Trump pageant, her 7 yr. old son has his college educat…
    69    Photo: #Donald #Trump #Protest in #Milwaukee ahead of CNN GOP #Town #Hall with #Trump, Ted #Cruz, ... https://t.co/8NOguZUSCK               
    Name: text, dtype: object
    70    RT @Dodarey: @DR8801 @SykesCharlie Charlie, let's see you get a straight "yes" or "no" answer from Cruz a/b being unfaithful to his wife @T… 
    71    RT @RonBasler1: @DavidWhitDennis @realDonaldTrump @tedcruz \n\nCRUZ SCREWS HOOKERS\n\nCRUZ / CLINTON                                         
    72    RT @RockCliffOne: Remember when the idea of a diabolical moron holding the world hostage was an idea for a funny movie? #Trump #GOP https:/… 
    73    RT @HillaryClinton: "Every day, another Republican bemoans the rise of Donald Trump... but [he] didn’t come out of nowhere." —Hillary\nhttps…
    74    @realDonaldTrump @MELANIATRUMP Get Them Good Mr.Trump ,Great Picture of You and The First Lady                                               
    75    @realDonaldTrump Its too bad Cruz doesn't have enough brains to realize he's being led down the primrose lane to be neutered by the Elites!! 
    76    I just saw this. I'm speechless.  https://t.co/cmUYxtrX0Y                                                                                    
    77    RT @Dodarey: @DR8801 @SykesCharlie Charlie, let's see you get a straight "yes" or "no" answer from Cruz a/b being unfaithful to his wife @T… 
    78    I just saw this. I'm speechless.  https://t.co/cmUYxtrX0Y                                                                                    
    79    Trump campaign chief charged with battery https://t.co/SpIukqj3Rb                                                                            
    Name: text, dtype: object
    80    RT @HillaryClinton: "Every day, another Republican bemoans the rise of Donald Trump... but [he] didn’t come out of nowhere." —Hillary\nhttps…
    81    @realDonaldTrump @MELANIATRUMP Get Them Good Mr.Trump ,Great Picture of You and The First Lady                                               
    82    RT @RockCliffOne: Remember when the idea of a diabolical moron holding the world hostage was an idea for a funny movie? #Trump #GOP https:/… 
    83    RT @immigrant4trump: @immigrant4trump msm, cable news attacking trump all day, from 8am to 10pm today, then the reruns come on, repeating t… 
    84    @ErinBurnett @Bakari_Sellers @benfergusonshow @BernieSanders Again @CNN allows Jeff Lord far too much time to spin wacky Trump.              
    85    RT @immigrant4trump: @immigrant4trump msm, cable news attacking trump all day, from 8am to 10pm today, then the reruns come on, repeating t… 
    86    @ErinBurnett @Bakari_Sellers @benfergusonshow @BernieSanders Again @CNN allows Jeff Lord far too much time to spin wacky Trump.              
    87    @noreallyhowcome @TVineberg Learn about Bernie https://t.co/bhaUnQ4jrr Learn about Hillary https://t.co/eAbfWrAG4G https://t.co/W53JJCkDFv   
    88    RT @GlendaJazzey: Donald Trump’s Campaign Financing Dodge, @rrotunda https://t.co/L8flI4lswG via @VerdictJustia                              
    89    Trump who prides himself on the ability to spot a good deal missed out on a big one in Louisiana. C'est la vie.  https://t.co/MZrvWwTWZV     
    Name: text, dtype: object
    90    Judicial Watch: Obama Administration Withholds Draft Whitewater Indictment of Hillary Clinton https://t.co/EuW9J1WVm1                       
    91    I don't understand how anyone can support a hateful person like @realDonaldTrump  https://t.co/BbYMxRWadC                                   
    92    RT @TUSK81: LOUDER FOR THE PEOPLE IN THE BACK https://t.co/hlPVyNLXzx                                                                       
    93    RT @loopzoop: Well...put it back https://t.co/8Yb7BDT5VM                                                                                    
    94    Donald Trump: Victim. https://t.co/qvK17ZnUTZ                                                                                               
    95    RT @claytoncubitt: Stop asking Bernie supporters if they’ll vote for Hillary against Trump. We got a plan to beat Trump already. Called Ber…
    96    Kasich is gonna fuck this up for Ted Cruz  https://t.co/JYYok5qx7R                                                                          
    97    RT @akaMaude13: Seriously can't make this up. What a joke. #NeverTrump  https://t.co/JkTx6mdRgC                                             
    98    Kasich is gonna fuck this up for Ted Cruz  https://t.co/JYYok5qx7R                                                                          
    99    @marklevinshow try reporting this truth. https://t.co/z76fZzCRK3                                                                            
    Name: text, dtype: object
    {'en': 97, 'et': 1, 'und': 2}


    /Users/othmanerifki/Library/Python/3.7/lib/python/site-packages/ipykernel_launcher.py:4: FutureWarning: Passing a negative integer is deprecated in version 1.0 and will not be supported in future version. Instead, use None to not limit the column width.
      after removing the cwd from sys.path.



```python

```
