**Mobile apps Analyis for Android and IOS**

*we're working as data analysts for a company that builds Android and iOS mobile apps. We make our apps available on Google Play and the App Store.*

*Our goal for this project is to analyze data to help our developers understand what type of apps are likely to attract more users,We only build apps that are free to download and install, and our main source of revenue consists of in-app ads. This means our revenue for any given app is mostly influenced by the number of users who use our app — the more users that see and engage with the ads, the better.*



```python
from csv import reader

# The App Store data set
opened_file = open('AppleStore.csv')
read_file = reader(opened_file)
ios = list(read_file)
apple_head = ios[0]
apple = ios[1:]

#The Google Play data set #
opened_file = open('googleplaystore.csv')
read_file = reader(opened_file)
droid = list(read_file)
android_head = droid[0]
android = droid[1:]
```


```python
#function created to access dataset
def explore_data(dataset, start, end, rows_and_columns=False):
    dataset_slice = dataset[start:end]    
    for row in dataset_slice:
            print(row)
            print('\n') # adds a new (empty) line between rows
        
    if rows_and_columns:
            print('Number of rows:', len(dataset))
            print('Number of columns:', len(dataset[0]))
 
```


```python
                             
print(apple_head,'\n')            
explore_data(apple,0,3,True)
#printing the column names that can help with analysis,'App', 'Category', 'Reviews', 'Installs', 'Type', 'Price', and 'Genres'..
```

    ['id', 'track_name', 'size_bytes', 'currency', 'price', 'rating_count_tot', 'rating_count_ver', 'user_rating', 'user_rating_ver', 'ver', 'cont_rating', 'prime_genre', 'sup_devices.num', 'ipadSc_urls.num', 'lang.num', 'vpp_lic'] 
    
    ['284882215', 'Facebook', '389879808', 'USD', '0.0', '2974676', '212', '3.5', '3.5', '95.0', '4+', 'Social Networking', '37', '1', '29', '1']
    
    
    ['389801252', 'Instagram', '113954816', 'USD', '0.0', '2161558', '1289', '4.5', '4.0', '10.23', '12+', 'Photo & Video', '37', '0', '29', '1']
    
    
    ['529479190', 'Clash of Clans', '116476928', 'USD', '0.0', '2130805', '579', '4.5', '4.5', '9.24.12', '9+', 'Games', '38', '5', '18', '1']
    
    
    Number of rows: 7197
    Number of columns: 16



```python
print(android_head,'\n')
explore_data(android, 0, 3, True)
#printing the column names that can help with analysis,'App', 'Category', 'Reviews', 'Installs', 'Type', 'Price', and 'Genres'..
```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver'] 
    
    ['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']
    
    
    ['Coloring book moana', 'ART_AND_DESIGN', '3.9', '967', '14M', '500,000+', 'Free', '0', 'Everyone', 'Art & Design;Pretend Play', 'January 15, 2018', '2.0.0', '4.0.3 and up']
    
    
    ['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']
    
    
    Number of rows: 10841
    Number of columns: 13



```python
#incorrect header row,@ in 3, rating is 19 in index 10472
print (android_head[0:],'\n')#for visualization
print(len(android))
del (android[10472])#del in error index 10472, run once.
print(len(android))

```

    ['App', 'Category', 'Rating', 'Reviews', 'Size', 'Installs', 'Type', 'Price', 'Content Rating', 'Genres', 'Last Updated', 'Current Ver', 'Android Ver'] 
    
    10841
    10840



```python
app_names = ['Instagram']

print('Instagram' in app_names)
print('Twitter' in app_names)
print(232 in app_names)
print('Facebook' in app_names)
```

    True
    False
    False
    False



```python
for app in android:#serching for dupliclate apps
    name = app[0]
    if name == 'Instagram':
        print('duplicate apps'+'\n')
        print(app)
```

    duplicate apps
    
    ['Instagram', 'SOCIAL', '4.5', '66577313', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
    duplicate apps
    
    ['Instagram', 'SOCIAL', '4.5', '66577446', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
    duplicate apps
    
    ['Instagram', 'SOCIAL', '4.5', '66577313', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']
    duplicate apps
    
    ['Instagram', 'SOCIAL', '4.5', '66509917', 'Varies with device', '1,000,000,000+', 'Free', '0', 'Teen', 'Social', 'July 31, 2018', 'Varies with device', 'Varies with device']


The main difference of in the duplicates is in the fourth row, that corresponds with the number of reviews The data was collected at different times and the most the most recent would be the latest update with the highest review.


```python
#Identifying duplicate apps
duplicate_apps = []
unique_apps = []

for app in android:
    name = app[0]
    if name in unique_apps:
        duplicate_apps.append(name)
    else:
        unique_apps.append(name)
print('Number of duplicate apps:',len(duplicate_apps))
print('\n')
print('Examples of duplicate apps:',duplicate_apps[:15])
```

    Number of duplicate apps: 1181
    
    
    Examples of duplicate apps: ['Quick PDF Scanner + OCR FREE', 'Box', 'Google My Business', 'ZOOM Cloud Meetings', 'join.me - Simple Meetings', 'Box', 'Zenefits', 'Google Ads', 'Google My Business', 'Slack', 'FreshBooks Classic', 'Insightly CRM', 'QuickBooks Accounting: Invoicing & Expenses', 'HipChat - Chat Built for Teams', 'Xero Accounting Software']



```python
#removing duplicate entries.
reviews_max = {}

for app in android:
    name = app[0]
    n_reviews = float(app[3])

    if name in reviews_max and reviews_max[name] < n_reviews:
        reviews_max[name] = n_reviews
    
    elif name not in reviews_max:
        reviews_max[name] = n_reviews
    
#inspecting the dictionary;length should be 9,659

```


```python
#Total number of apps without duplicates.
print('Expected length:',len(android) - 1181)
print('actual length:',len(reviews_max))
```

    Expected length: 9659
    actual length: 9659



```python

```


```python
#removing duplicate rows, empty lists will store duplicate apps
android_clean = [] 
already_added = []

for app in android:
    name = app[0]
    n_reviews = float(app[3])

    if (n_reviews == reviews_max[name]) and (name not in already_added):
        android_clean.append(app)
        already_added.append(name)
        
        
        
```


```python
#Explore the android_clean data set to ensure everything went as expected. 
#The data set should have 9,659 rows.
explore_data(android_clean, 0, 2, True)
```

    ['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']
    
    
    ['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']
    
    
    Number of rows: 9659
    Number of columns: 13



```python
#identifying non english apps to remove for dataset.
print(apple[813][1])
print(apple[6731][1])
print('\n')
print(android_clean[4412][0])
print(android_clean[7940][0])
```

    爱奇艺PPS -《欢乐颂2》电视剧热播
    【脱出ゲーム】絶対に最後までプレイしないで 〜謎解き＆ブロックパズル〜
    
    
    中国語 AQリスニング
    لعبة تقدر تربح DZ



```python
#in order to remove non english apps, we search for app names greater than unicode 127
def eng_charac(english):
    for non_eng  in english:
        if ord(non_eng) > 127:
            return False
        
    return True

```


```python
#checking for english and non english apps
print(eng_charac('Instagram'))
print(eng_charac('爱奇艺PPS -《欢乐颂2》电视剧热播'))
print(eng_charac('Docs To Go™ Free Office Suite'))
print(eng_charac('Docs To Go™ Free Office Suite'
))

#note special characters are not recognized as english characters, as they are out of ASCII range
#using function created could remove useful data.
```

    True
    False
    False
    False


We'll only remove an app if its name has more than three characters with corresponding numbers falling outside the ASCII range.



```python
def eng_charac(string):
    non_ascii = 0
    
    for non_eng_charac in string:
        if ord(non_eng_charac) > 127:
            non_ascii += 1
            
    if non_ascii > 3:
        return False
    else:
        return True

print(eng_charac('Docs To Go™ Free Office Suite'))
print(eng_charac('Instachat 😜'))



```

    True
    True


Below, we use the is_english() function to filter out the non-English apps for both data sets:


```python
android_english = []
apple_english = []

for app in android_clean:
    name = app[0]
    if eng_charac(name):
        android_english.append(app)


for app in apple:
    name = app[1]
    if eng_charac(name):
        apple_english.append(app)

explore_data(android_english, 0, 3, True)
print('\n')
explore_data(apple_english, 0, 3, True)
```

    ['Photo Editor & Candy Camera & Grid & ScrapBook', 'ART_AND_DESIGN', '4.1', '159', '19M', '10,000+', 'Free', '0', 'Everyone', 'Art & Design', 'January 7, 2018', '1.0.0', '4.0.3 and up']
    
    
    ['U Launcher Lite – FREE Live Cool Themes, Hide Apps', 'ART_AND_DESIGN', '4.7', '87510', '8.7M', '5,000,000+', 'Free', '0', 'Everyone', 'Art & Design', 'August 1, 2018', '1.2.4', '4.0.3 and up']
    
    
    ['Sketch - Draw & Paint', 'ART_AND_DESIGN', '4.5', '215644', '25M', '50,000,000+', 'Free', '0', 'Teen', 'Art & Design', 'June 8, 2018', 'Varies with device', '4.2 and up']
    
    
    Number of rows: 9614
    Number of columns: 13
    
    
    ['284882215', 'Facebook', '389879808', 'USD', '0.0', '2974676', '212', '3.5', '3.5', '95.0', '4+', 'Social Networking', '37', '1', '29', '1']
    
    
    ['389801252', 'Instagram', '113954816', 'USD', '0.0', '2161558', '1289', '4.5', '4.0', '10.23', '12+', 'Photo & Video', '37', '0', '29', '1']
    
    
    ['529479190', 'Clash of Clans', '116476928', 'USD', '0.0', '2130805', '579', '4.5', '4.5', '9.24.12', '9+', 'Games', '38', '5', '18', '1']
    
    
    Number of rows: 6183
    Number of columns: 16


We're now left with 9164 Android apps and 6183 IOS apps.

we only build apps that are free to download and install, and our main source of revenue consists of in-app ads. Our data sets contain both free and non-free apps; we'll need to isolate only the free apps for our analysis.




```python
android_free = []
ios_free = []

for app in android_english:
    price = app[7]
    if price == '0':
        android_free.append(app)
        
for app in apple_english:
        price = app[4]
        if price == '0.0':
            ios_free.append(app)

print(len(android_free))
print(len(ios_free))
```

    8864
    3222



Removed inaccurate data
Removed duplicate app entries
Removed non-English apps
Isolated the free apps

 **So far, we:**
- Removed inaccurate data
- Removed duplicate app entries
- Removed non-English apps
- Isolated the free apps




We want to find an app profile that fits both the App Store and Google Play, because our aim is to determine the kinds of apps that are likely to attract more users, due to the fact that our revenue is highly influenced by the number of people using our apps.

Now we will inspect both data sets and identify the columns you could use to generate frequency tables to find out what are the most common genres in each market.

**We'll build two functions we can use to analyze the frequency tables:**

- One function to generate frequency tables that show percentages

- Another function that we can use to display the percentages in a descending order


```python
# function to generate frequency tables that show percentages
def freq_table(dataset, index):
    table = {}
    total = 0
    
    for row in dataset:
        total += 1
        value = row[index]
        if value in table:
            table[value] += 1
        else:
            table[value] = 1
    
    table_percentages = {}
    for key in table:
        percentage = (table[key] / total) * 100
        table_percentages[key] = percentage 
    
    return table_percentages



#Another function that we can use to display the percentages in a descending order
def display_table(dataset, index):
    table = freq_table(dataset, index)
    table_display = []
    for key in table:
        key_val_as_tuple = (table[key], key)
        table_display.append(key_val_as_tuple)
        
    table_sorted = sorted(table_display, reverse = True)
    for entry in table_sorted:
        print(entry[1], ':', entry[0])
```

We can now examine the frequency the table for prime_genre columun of the Applestore dataset.


```python
display_table(ios_free, -5)
```

    Games : 58.16263190564867
    Entertainment : 7.883302296710118
    Photo & Video : 4.9658597144630665
    Education : 3.662321539416512
    Social Networking : 3.2898820608317814
    Shopping : 2.60707635009311
    Utilities : 2.5139664804469275
    Sports : 2.1415270018621975
    Music : 2.0484171322160147
    Health & Fitness : 2.0173805090006205
    Productivity : 1.7380509000620732
    Lifestyle : 1.5828677839851024
    News : 1.3345747982619491
    Travel : 1.2414649286157666
    Finance : 1.1173184357541899
    Weather : 0.8690254500310366
    Food & Drink : 0.8069522036002483
    Reference : 0.5586592178770949
    Business : 0.5276225946617008
    Book : 0.4345127250155183
    Navigation : 0.186219739292365
    Medical : 0.186219739292365
    Catalogs : 0.12414649286157665


We can see that among the free English apps, more than a half (58.16%) are games. Entertainment apps are close to 8%, followed by photo and video apps, which are close to 5%. Only 3.66% of the apps are designed for education, followed by social networking apps which amount for 3.29% of the apps in our data set.

The general impression is that App Store (at least the part containing free English apps) is dominated by apps that are designed for fun (games, entertainment, photo and video, social networking, sports, music, etc.), while apps with practical purposes (education, shopping, utilities, productivity, lifestyle, etc.) are more rare. However, the fact that fun apps are the most numerous doesn't also imply that they also have the greatest number of users — the demand might not be the same as the offer.

Below we can now examine the Goople playstore.


```python
display_table(android_english, -4) # Category

```

    Tools : 8.602038693571874
    Entertainment : 5.793634283336801
    Education : 5.231953401289786
    Business : 4.358227584772207
    Medical : 4.108591637195756
    Personalization : 3.900561680882047
    Productivity : 3.879758685250676
    Lifestyle : 3.775743707093822
    Finance : 3.588516746411483
    Sports : 3.442895776991887
    Communication : 3.2660703141252343
    Action : 3.110047846889952
    Health & Fitness : 2.995631370917412
    Photography : 2.9124193883919283
    News & Magazines : 2.600374453921365
    Social : 2.485957977948825
    Travel & Local : 2.26752652381943
    Books & Reference : 2.26752652381943
    Shopping : 2.090701060952777
    Simulation : 1.9762845849802373
    Arcade : 1.9138755980861244
    Dating : 1.768254628666528
    Casual : 1.7162471395881007
    Video Players & Editors : 1.674641148325359
    Maps & Navigation : 1.3417932182234242
    Puzzle : 1.2377782400665696
    Food & Drink : 1.1649677553567712
    Role Playing : 1.0817557728312877
    Strategy : 0.9777407946744331
    Racing : 0.9465363012273768
    Libraries & Demo : 0.8737258165175785
    Auto & Vehicles : 0.8737258165175785
    Weather : 0.8217183274391513
    House & Home : 0.7593093405450385
    Adventure : 0.748907842729353
    Events : 0.6656958602038693
    Art & Design : 0.5824838776783856
    Comics : 0.5616808820470147
    Beauty : 0.5512793842313293
    Card : 0.48887039733721654
    Parenting : 0.4784688995215311
    Board : 0.43686290825878926
    Casino : 0.40565841481173287
    Educational;Education : 0.3952569169960474
    Trivia : 0.384855419180362
    Educational : 0.384855419180362
    Education;Education : 0.36405242354899103
    Casual;Pretend Play : 0.26003744539213647
    Word : 0.23923444976076555
    Music : 0.1976284584980237
    Puzzle;Brain Games : 0.1768254628666528
    Education;Pretend Play : 0.1768254628666528
    Racing;Action & Adventure : 0.16642396505096732
    Entertainment;Music & Video : 0.15602246723528188
    Board;Brain Games : 0.1456209694195964
    Arcade;Action & Adventure : 0.1456209694195964
    Educational;Pretend Play : 0.13521947160391096
    Casual;Action & Adventure : 0.13521947160391096
    Casual;Brain Games : 0.1248179737882255
    Action;Action & Adventure : 0.1248179737882255
    Simulation;Action & Adventure : 0.0728104847097982
    Parenting;Education : 0.0728104847097982
    Entertainment;Brain Games : 0.0728104847097982
    Parenting;Music & Video : 0.06240898689411275
    Educational;Brain Games : 0.06240898689411275
    Education;Creativity : 0.06240898689411275
    Casual;Creativity : 0.06240898689411275
    Art & Design;Creativity : 0.06240898689411275
    Educational;Creativity : 0.052007489078427296
    Adventure;Action & Adventure : 0.052007489078427296
    Sports;Action & Adventure : 0.04160599126274183
    Role Playing;Pretend Play : 0.04160599126274183
    Role Playing;Action & Adventure : 0.04160599126274183
    Education;Brain Games : 0.04160599126274183
    Education;Action & Adventure : 0.04160599126274183
    Simulation;Pretend Play : 0.031204493447056374
    Simulation;Education : 0.031204493447056374
    Puzzle;Action & Adventure : 0.031204493447056374
    Music;Music & Video : 0.031204493447056374
    Entertainment;Creativity : 0.031204493447056374
    Entertainment;Action & Adventure : 0.031204493447056374
    Educational;Action & Adventure : 0.031204493447056374
    Education;Music & Video : 0.031204493447056374
    Casual;Education : 0.031204493447056374
    Board;Action & Adventure : 0.031204493447056374
    Video Players & Editors;Music & Video : 0.020802995631370915
    Strategy;Action & Adventure : 0.020802995631370915
    Puzzle;Creativity : 0.020802995631370915
    Entertainment;Pretend Play : 0.020802995631370915
    Card;Action & Adventure : 0.020802995631370915
    Books & Reference;Education : 0.020802995631370915
    Video Players & Editors;Creativity : 0.010401497815685458
    Trivia;Education : 0.010401497815685458
    Travel & Local;Action & Adventure : 0.010401497815685458
    Tools;Education : 0.010401497815685458
    Strategy;Education : 0.010401497815685458
    Strategy;Creativity : 0.010401497815685458
    Role Playing;Education : 0.010401497815685458
    Role Playing;Brain Games : 0.010401497815685458
    Racing;Pretend Play : 0.010401497815685458
    Puzzle;Education : 0.010401497815685458
    Parenting;Brain Games : 0.010401497815685458
    Music & Audio;Music & Video : 0.010401497815685458
    Lifestyle;Pretend Play : 0.010401497815685458
    Lifestyle;Education : 0.010401497815685458
    Health & Fitness;Education : 0.010401497815685458
    Health & Fitness;Action & Adventure : 0.010401497815685458
    Entertainment;Education : 0.010401497815685458
    Communication;Creativity : 0.010401497815685458
    Comics;Creativity : 0.010401497815685458
    Casual;Music & Video : 0.010401497815685458
    Books & Reference;Creativity : 0.010401497815685458
    Board;Pretend Play : 0.010401497815685458
    Art & Design;Pretend Play : 0.010401497815685458
    Art & Design;Action & Adventure : 0.010401497815685458
    Arcade;Pretend Play : 0.010401497815685458
    Adventure;Education : 0.010401497815685458
    Adventure;Brain Games : 0.010401497815685458


The landscape seems significantly different on Google Play: there are not that many apps designed for fun, and it seems that a good number of apps are designed for practical purposes (family, tools, business, lifestyle, productivity, etc.). However, if we investigate this further, we can see that the family category (which accounts for almost 19% of the apps) means mostly games for kids.



### Now will find out the most popular apps by genre App Store.

One way to find out what genres are the most popular (have the most users) is to calculate the average number of installs for each app genre. For the Google Play data set, we can find this information in the Installs column, but for the App Store data set this information is missing. As a workaround, we'll take the total number of user ratings as a proxy, which we can find in the rating_count_tot app.

Below, we calculate the average number of user ratings per app genre on the App Store:


```python
#12
genres_ios = freq_table(ios_free, -5)

for genre in genres_ios:
    total = 0
    len_genre = 0
    for app in ios_free:
        genre_app = app[-5]
        if genre_app == genre:
            n_ratings = float(app[5])
            total += n_ratings
            len_genre += 1
    avg_n_ratings = total / len_genre
    print(genre, ':', avg_n_ratings)
```

    Social Networking : 71548.34905660378
    Photo & Video : 28441.54375
    Games : 22788.6696905016
    Music : 57326.530303030304
    Reference : 74942.11111111111
    Health & Fitness : 23298.015384615384
    Weather : 52279.892857142855
    Utilities : 18684.456790123455
    Travel : 28243.8
    Shopping : 26919.690476190477
    News : 21248.023255813954
    Navigation : 86090.33333333333
    Lifestyle : 16485.764705882353
    Entertainment : 14029.830708661417
    Food & Drink : 33333.92307692308
    Sports : 23008.898550724636
    Book : 39758.5
    Finance : 31467.944444444445
    Education : 7003.983050847458
    Productivity : 21028.410714285714
    Business : 7491.117647058823
    Catalogs : 4004.0
    Medical : 612.0



```python
for app in ios_free:
    if app[-5] == 'Navigation':
        print(app[1], ':', app[5]) # print name and number of ratings        
```

    Waze - GPS Navigation, Maps & Real-time Traffic : 345046
    Google Maps - Navigation & Transit : 154911
    Geocaching® : 12811
    CoPilot GPS – Car Navigation & Offline Maps : 3582
    ImmobilienScout24: Real Estate Search in Germany : 187
    Railway Route Search : 5


On average, navigation apps have the highest number of user reviews, but this figure is heavily influenced by Waze and Google Maps, which have close to half a million user reviews together:

The same pattern applies to social networking apps, where the average number is heavily influenced by a few giants like Facebook, Pinterest, Skype, etc. Same applies to music apps, where a few big players like Pandora, Spotify, and Shazam heavily influence the average number.




```python
for app in ios_free:
    if app[-5] == 'Reference':
        print(app[1], ':', app[5])
```

    Bible : 985920
    Dictionary.com Dictionary & Thesaurus : 200047
    Dictionary.com Dictionary & Thesaurus for iPad : 54175
    Google Translate : 26786
    Muslim Pro: Ramadan 2017 Prayer Times, Azan, Quran : 18418
    New Furniture Mods - Pocket Wiki & Game Tools for Minecraft PC Edition : 17588
    Merriam-Webster Dictionary : 16849
    Night Sky : 12122
    City Maps for Minecraft PE - The Best Maps for Minecraft Pocket Edition (MCPE) : 8535
    LUCKY BLOCK MOD ™ for Minecraft PC Edition - The Best Pocket Wiki & Mods Installer Tools : 4693
    GUNS MODS for Minecraft PC Edition - Mods Tools : 1497
    Guides for Pokémon GO - Pokemon GO News and Cheats : 826
    WWDC : 762
    Horror Maps for Minecraft PE - Download The Scariest Maps for Minecraft Pocket Edition (MCPE) Free : 718
    VPN Express : 14
    Real Bike Traffic Rider Virtual Reality Glasses : 8
    教えて!goo : 0
    Jishokun-Japanese English Dictionary & Translator : 0



However, this niche seems to show some potential. One thing we could do is take another popular book and turn it into an app where we could add different features besides the raw version of the book. This might include daily quotes from the book, an audio version of the book, quizzes about the book, etc. On top of that, we could also embed a dictionary within the app, so users don't need to exit our app to look up words in an external app.

This idea seems to fit well with the fact that the App Store is dominated by for-fun apps. This suggests the market might be a bit saturated with for-fun apps, which means a practical app might have more of a chance to stand out among the huge number of apps on the App Store.

Other genres that seem popular include weather, book, food and drink, or finance. The book genre seem to overlap a bit with the app idea we described above, but the other genres don't seem too interesting to us:

- Weather apps — people generally don't spend too much time in-app, and the chances of making profit from in-app adds are low. Also, getting reliable live weather data may require us to connect our apps to non-free APIs.

- Food and drink — examples here include Starbucks, Dunkin' Donuts, McDonald's, etc. So making a popular food and drink app requires actual cooking and a delivery service, which is outside the scope of our company.

- Finance apps — these apps involve banking, paying bills, money transfer, etc. Building a finance app requires domain knowledge, and we don't want to hire a finance expert just to build an app.

### Most Popular Apps by Genre on Google Play


```python
display_table(android_free, 5)#the installs colums
```

    1,000,000+ : 15.726534296028879
    100,000+ : 11.552346570397113
    10,000,000+ : 10.548285198555957
    10,000+ : 10.198555956678701
    1,000+ : 8.393501805054152
    100+ : 6.915613718411552
    5,000,000+ : 6.825361010830325
    500,000+ : 5.561823104693141
    50,000+ : 4.7721119133574
    5,000+ : 4.512635379061372
    10+ : 3.5424187725631766
    500+ : 3.2490974729241873
    50,000,000+ : 2.3014440433213
    100,000,000+ : 2.1322202166064983
    50+ : 1.917870036101083
    5+ : 0.78971119133574
    1+ : 0.5076714801444043
    500,000,000+ : 0.2707581227436823
    1,000,000,000+ : 0.22563176895306858
    0+ : 0.04512635379061372
    0 : 0.01128158844765343


One problem with this data is that is not precise. For instance, we don't know whether an app with 100,000+ installs has 100,000 installs, 200,000, or 350,000. However, we don't need very precise data for our purposes — we only want to get an idea which app genres attract the most users, and we don't need perfect precision with respect to the number of users.


We're going to leave the numbers as they are, which means that we'll consider that an app with 100,000+ installs has 100,000 installs, and an app with 1,000,000+ installs has 1,000,000 installs, and so on.

To perform computations, however, we'll need to convert each install number to float — this means that we need to remove the commas and the plus characters, otherwise the conversion will fail and raise an error. We'll do this directly in the loop below, where we also compute the average number of installs for each genre (category).





```python
categories_android = freq_table(android_free,1)

for category in categories_android:
    total = 0
    len_category = 0
    for app in android_free:
        category_app = app[1]
        if category_app == category:
            n_installs = app[5]
            n_installs = n_installs.replace(',','')
            n_installs = n_installs.replace('+','')
            total += float(n_installs)
            len_category += 1
    avg_n_installs = total / len_category
    print(category,':', avg_n_installs)
```

    ART_AND_DESIGN : 1986335.0877192982
    AUTO_AND_VEHICLES : 647317.8170731707
    BEAUTY : 513151.88679245283
    BOOKS_AND_REFERENCE : 8767811.894736841
    BUSINESS : 1712290.1474201474
    COMICS : 817657.2727272727
    COMMUNICATION : 38456119.167247385
    DATING : 854028.8303030303
    EDUCATION : 1833495.145631068
    ENTERTAINMENT : 11640705.88235294
    EVENTS : 253542.22222222222
    FINANCE : 1387692.475609756
    FOOD_AND_DRINK : 1924897.7363636363
    HEALTH_AND_FITNESS : 4188821.9853479853
    HOUSE_AND_HOME : 1331540.5616438356
    LIBRARIES_AND_DEMO : 638503.734939759
    LIFESTYLE : 1437816.2687861272
    GAME : 15588015.603248259
    FAMILY : 3695641.8198090694
    MEDICAL : 120550.61980830671
    SOCIAL : 23253652.127118643
    SHOPPING : 7036877.311557789
    PHOTOGRAPHY : 17840110.40229885
    SPORTS : 3638640.1428571427
    TRAVEL_AND_LOCAL : 13984077.710144928
    TOOLS : 10801391.298666667
    PERSONALIZATION : 5201482.6122448975
    PRODUCTIVITY : 16787331.344927534
    PARENTING : 542603.6206896552
    WEATHER : 5074486.197183099
    VIDEO_PLAYERS : 24727872.452830188
    NEWS_AND_MAGAZINES : 9549178.467741935
    MAPS_AND_NAVIGATION : 4056941.7741935486


Our aim is to recommend an app genre that shows potential for being profitable on both the App Store and Google Play. 


```python
for app in android_free:
    if app[1] == 'COMMUNICATION' and (app[5] == '1,000,000+'
                                     or app[5] == '500,000,000+'
                                     or app[5] == '100,000,000+'):
        print(app[0], ':' , app[5])
```

    imo beta free calls and text : 100,000,000+
    TracFone My Account : 1,000,000+
    My magenta : 1,000,000+
    Android Messages : 100,000,000+
    Google Duo - High Quality Video Calls : 500,000,000+
    Seznam.cz : 1,000,000+
    imo free video calls and chat : 500,000,000+
    Who : 100,000,000+
    GO SMS Pro - Messenger, Free Themes, Emoji : 100,000,000+
    Messaging+ SMS, MMS Free : 1,000,000+
    LINE: Free Calls & Messages : 500,000,000+
    mysms SMS Text Messaging Sync : 1,000,000+
    2ndLine - Second Phone Number : 1,000,000+
    Firefox Browser fast & private : 100,000,000+
    Ninesky Browser : 1,000,000+
    UC Browser - Fast Download Private & Secure : 500,000,000+
    Ghostery Privacy Browser : 1,000,000+
    InBrowser - Incognito Browsing : 1,000,000+
    PHONE for Google Voice & GTalk : 1,000,000+
    Safest Call Blocker : 1,000,000+
    Should I Answer? : 1,000,000+
    RocketDial Dialer & Contacts : 1,000,000+
    True Contact - Real Caller ID : 1,000,000+
    Video Caller Id : 1,000,000+
    Burner - Free Phone Number : 1,000,000+
    Caller ID + : 1,000,000+
    Email TypeApp - Mail App : 1,000,000+
    All Email Providers : 1,000,000+
    Newton Mail - Email App for Gmail, Outlook, IMAP : 1,000,000+
    mail.com mail : 1,000,000+
    Vonage Mobile® Call Video Text : 1,000,000+
    Messenger Lite: Free Calls & Messages : 100,000,000+
    AntennaPict β : 1,000,000+
    Kik : 100,000,000+
    KakaoTalk: Free Calls & Text : 100,000,000+
    Opera Mini - fast web browser : 100,000,000+
    Opera Browser: Fast and Secure : 100,000,000+
    Telegram : 100,000,000+
    AT&T Messages for Tablet : 1,000,000+
    Truecaller: Caller ID, SMS spam blocking & Dialer : 100,000,000+
    UC Browser Mini -Tiny Fast Private & Secure : 100,000,000+
    Viber Messenger : 500,000,000+
    WeChat : 100,000,000+
    Yahoo Mail – Stay Organized : 100,000,000+
    Adblock Plus for Samsung Internet - Browse safe. : 1,000,000+
    AW - free video calls and chat : 1,000,000+
    BBM - Free Calls & Messages : 100,000,000+
    BBMoji - Your personalized BBM Stickers : 1,000,000+
    SW-100.tch by Callstel : 1,000,000+
    Tiny Call Confirm : 1,000,000+
    CB Radio Chat - for friends! : 1,000,000+
    Virtual Walkie Talkie : 1,000,000+
    ClanPlay: Community and Tools for Gamers : 1,000,000+
    My Vodafone (GR) : 1,000,000+
    DW Contacts & Phone & Dialer : 1,000,000+
    Call Blocker - Blacklist, SMS Blocker : 1,000,000+
    Web Browser for Android : 1,000,000+
    Lite for Facebook Messenger : 1,000,000+
    Wi-Fi Auto-connect : 1,000,000+
    WeFi - Free Fast WiFi Connect & Find Wi-Fi Map : 1,000,000+
    Firefox Focus: The privacy browser : 1,000,000+


If we removed all the communication apps that have over 100 million installs, the average would be reduced roughly ten times:


```python
under_100_m = []

for app in android_free:
    n_installs = app[5]
    n_installs = n_installs.replace(',','')
    n_installs = n_installs.replace('+','')
    if app[1] == 'COMMUNICATION' and ( float(n_installs) < 100000000):
        under_100_m.append(float(n_installs))
        
sum(under_100_m) / len (under_100_m)
```




    3603485.3884615386



We see the same pattern for the video players category, which is the runner-up with 24,727,872 installs. The market is dominated by apps like Youtube, Google Play Movies & TV, or MX Player. The pattern is repeated for social apps (where we have giants like Facebook, Instagram, Google+, etc.), photography apps (Google Photos and other popular photo editors), or productivity apps (Microsoft Word, Dropbox, Google Calendar, Evernote, etc.).
