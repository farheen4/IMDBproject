# IMDBproject
 To download the IMDBProject > Go to Code > Download Zip >Select IBMDProject.
Below is the code for the project from Pycharm

First step : Go to the IMDB movie ratings, you can check out the html code to get the clear idea about this project. 
Second step : Download relevant python libraries : Like Requests, BeautifulSoup and Openpyxl from python libraries. 
Third step : Copy the web link in order to request in pycharm from Beautifulsoup.
Fourth step : Code the Movie ratings and then the last step will be sheets and exporting to excel. 
Fivth step : Here the first volume of code is the raw data and the second volume of code will be rough code which will make you under clearly. 

Note: Here the second volume consists of rough code where the comment down sections are done before the coding. 

[VOLUME 1]
from bs4 import BeautifulSoup
import requests,openpyxl

excel=openpyxl.Workbook()
print(excel.sheetnames)
sheet=excel.active
sheet.title='Top Rated Movies'
print(excel.sheetnames)
sheet.append(['Movie Rank','Movie Name','Year of release','IMBD Rating'])



try:
    source=requests.get('https://www.imdb.com/chart/top/')
    source.raise_for_status()

    soup=BeautifulSoup(source.text,'html.parser')
    

    movies=soup.find('tbody',class_='lister-list').find_all('tr')

    for movie in movies:

        name=movie.find('td',class_='titleColumn').a.text #this is how you extract the particular name of the movie or tag
        rank=movie.find('td',class_='titleColumn').get_text(strip=True).split('.')[0] #strip will basically delete all the spaces and unknown characters.
       
        year=movie.find('td',class_='titleColumn').span.text.strip('()') #stripping where if you mention something it will remove that
        rating=movie.find('td',class_='ratingColumn imdbRating').strong.text
       
        print(rank,name,year,rating)
        sheet.append([rank,name,year,rating])


except Exception as e:
    print(e)

excel.save('IMBD Movie Rating doc.xlsx')




[VOLUME 2] This is the rough code with notes. 
from bs4 import BeautifulSoup
import requests,openpyxl

excel=openpyxl.Workbook()
print(excel.sheetnames)
sheet=excel.active
sheet.title='Top Rated Movies'
print(excel.sheetnames)
sheet.append(['Movie Rank','Movie Name','Year of release','IMBD Rating'])


# source=requests.get('https://www.imdb.com/chart/top/') #put in some label whenever you use request model like (source) because then it will show error.
# source.raise_for_status() #this raise for status will throw an error if the above URL is having some issues.

try:
    source=requests.get('https://www.imdb.com/chart/top/')
    source.raise_for_status()

    soup=BeautifulSoup(source.text,'html.parser')
    #print(soup)

    movies=soup.find('tbody',class_='lister-list').find_all('tr')
#print(len(movies)) #basically with this tbody we access the body of those movies not the insides.
#Here the beautiful soup will extract the html code and put it in the source object
#Here source is our response object and in order to use html code we should write source.text,

    for movie in movies:

        name=movie.find('td',class_='titleColumn').a.text #this is how you extract the particular name of the movie or tag
        rank=movie.find('td',class_='titleColumn').get_text(strip=True).split('.')[0] #strip will basically delete all the spaces and unknown characters.
        #if you use split then it will use quotes and listing brackets and [0] it will only show 1 not the title
        year=movie.find('td',class_='titleColumn').span.text.strip('()') #stripping where if you mention something it will remove that
        rating=movie.find('td',class_='ratingColumn imdbRating').strong.text
        # print(name)
        # print(rank) #The following coding above has been extracted from website>rightclick>inspect>html oc
        # print(year)
        # print(rating)
        print(rank,name,year,rating)
        sheet.append([rank,name,year,rating])


except Exception as e:
    print(e)

excel.save('IMBD Movie Rating doc.xlsx')

#if we use break at the end then it show the values which are how many time coded
#if we dont use break it will show all the 250 values nonstop




