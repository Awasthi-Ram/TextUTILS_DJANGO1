# TextUTILS_DJANGO1

link of all the notes
https://www.codewithharry.com/videos/python-django-tutorials-hindi-2/

python - to check the version of python

pip install django - install in the coresponding

python -m pip install django -  to install django current working python only

python -m django --version - to know the version of the the python

django----




django-admin - to see all admin command

django-admin startproject nameofproject
 create the project with django file 

 above file mysite can be any thing and the inner mysite is the python package or our project

 manage.py - command line utility use to interrract with the django project

 __init__.py - python package 

 setting.py - all setting are there
 of django

 urls.py - url declar and mapping is done here

 wsgi.py (web server gateway interface)


 python manage.py runserver - to start the server of the project default server http://127.0.0.1:8000/

python manage.py runserver 7000 - to give own local host server http://127.0.0.1:7000/

front-end - html ,css,javascript
backend -code on server for dynamic change in the server


create views.py 
from django.urls import path
import views in url.py from . import views;

urlpatterns = [
    path('admin/', admin.site.urls),
    path("",views.index,name='index')
]

views.py 
# if not given request
#index() takes 0 positional arguments but 1 was given
"""def index():
    return "hello"
    """
# to solve request argument
# still give error 'str' object has no attribute 'get'
"""def index(request):
    return "hello"
    """
# solve
from django.http import HttpResponse;

def index(request):
    return HttpResponse("hello")


with back url

def removepun(request):
    return HttpResponse('''<h1>removepun</h1> <a href="/">back</a>''')
def capital(request):
    return HttpResponse("<h1>capital</h1> <a href="/">back</a>")

def spaceremover(request):
    return HttpResponse("<h1>space remover</h1> <a href="/">back</a>")
def newlineremove(request):
    return HttpResponse("<h1>newlineremove</h1> <a href="/">back</a>")
def charcount(request):
    return HttpResponse("<h1>charcount</h1> <a href="/">back</a>")


#############use of templates

 'DIRS': ['templates'],

create templates
in the same director where manage.py exist

from django.shortcuts import render;


def index(request):
    return render(request,'index.html')

to asses variable in the index.html

param = {'name':'ram','place':'earth'}

{{}}

 def index(request):
#     param = {'name':'ram','place':'earth'}
#     return render(request,'index.html',param)
#     #return HttpResponse("hello")

 <h1> i am templates {{name}} is from{{place}}</h1>

<form action="removepun" method="get"> here removepun path url hai
to get the eleemnt of html
 print(request.GET.get('textarea','default')) - to get the emelent of html

 djtext = request.GET.get('textarea','default')
 print(djtext)

def analyze(request):
    text = request.GET.get('textarea','default')
    CHECKBOX = request.GET.get('checkbox','off')
    print(CHECKBOX)
    print(text)
   # correct = text
    punctuations = '''!()-[]{};:'"\,<>./?@#$%^&*_~'''
    correct = ""
    if CHECKBOX == "on":
        for char in text:
            if char not in punctuations:
                correct = correct + char
        param = {'purpose':'remove punctuation','analyed_text':correct,"check":CHECKBOX}
        return render(request, 'analyze.html',param)
    else:
        return HttpResponse("error no punctuatio remove")

def analyze(request):
    # get the text
    text = request.GET.get('textarea','default')

    # getting the checkbox
    CHECKBOX = request.GET.get('checkbox','off')
    fullcaps = request.GET.get('fullcaps','off')
    newlineremove = request.GET.get('newlineremover','off')
    spaceremover = request.GET.get('spaceremover','off')

    # print(CHECKBOX)
    # print(text)
   # correct = text
    punctuations = '''!()-[]{};:'"\,<>./?@#$%^&*_~'''
    correct = ""
    if CHECKBOX == "on":
        for char in text:
            if char not in punctuations:
                correct = correct + char
        param = {'purpose':'remove punctuation','analyed_text':correct,"check":CHECKBOX}
        return render(request, 'analyze.html',param)
    elif(fullcaps == 'on'):
        analyze = ""
        for char in text:
            analyze = analyze + char.upper()
        param = {'purpose':'change to upper case','analyed_text':analyze,"check":CHECKBOX}
        return render(request, 'analyze.html',param)
    elif(newlineremove == 'on'):
        analyze = ""
        for char in text:
            if char!= '\n':
                analyze = analyze + char
        param = {'purpose':'remove new line','analyed_text':analyze,"check":CHECKBOX}
        return render(request, 'analyze.html',param)
    elif(spaceremover == "on"):
        analyze = ""
        for index, char in enumerate(text):
            if text[index] == ' ' and text[index + 1] == " ":
                pass
            else:
                analyze = analyze + char
        param = {'purpose':'remove new line','analyed_text':analyze,"check":CHECKBOX}
        return render(request, 'analyze.html',param)
    else:
        return HttpResponse("error no punctuatio remove")

        #####################################
        #######################################

         <pre>{{ analyed_text}} </pre> 
         to get the asitize answer of string

         #########################
         get request send data with the urls
         nad the length of url have limit - because of server limit

         #############post method send data with post request

         ################################################
         django provite protection angaist csrf -Cross-site Request Forgery

         from example jo hama html form hota hai wo user side me avalable hota hai or agar user form action="khuch or kaede exampe delete
         kar de or delete method exist karti ho to hama account delete ho jat=ye ga to usse bachane ke liye hai csrf token

         ----security loop hool

         --- csrf token - promise that the request is coming from your website only

         to fix
         <form action="analyze" method="post">
            {% csrf_token %}

data featching in post method
        text = request.POST.get('textarea','default')

    # getting the checkbox
    CHECKBOX = request.POST.get('checkbox','off')
    fullcaps = request.POST.get('fullcaps','off')
    newlineremove = request.POST.get('newlineremover','off')
    spaceremover = request.POST.get('spaceremover','off')

 in a  net work to remove new line \n and \r both is used
if char!= '\n' and char!= '\r':


    # get the text

    ################get form#######
    # text = request.GET.get('textarea','default')

    # # getting the checkbox
    # CHECKBOX = request.GET.get('checkbox','off')
    # fullcaps = request.GET.get('fullcaps','off')
    # newlineremove = request.GET.get('newlineremover','off')
    # spaceremover = request.GET.get('spaceremover','off')
#################post form##########
    text = request.POST.get('textarea','default')

    # getting the checkbox
    CHECKBOX = request.POST.get('checkbox','off')
    fullcaps = request.POST.get('fullcaps','off')
    newlineremove = request.POST.get('newlineremover','off')
    spaceremover = request.POST.get('spaceremover','off')

    # print(CHECKBOX)
    # print(text)
   # correct = text
    punctuations = '''!()-[]{};:'"\,<>./?@#$%^&*_~'''
    correct = ""
    if CHECKBOX == "on":
        for char in text:
            if char not in punctuations:
                correct = correct + char
        param = {'purpose':'remove punctuation','analyed_text':correct,"check":CHECKBOX}
        text = correct
        #return render(request, 'analyze.html',param)
    if(fullcaps == 'on'):
        analyze = ""
        for char in text:
            analyze = analyze + char.upper()
        param = {'purpose':'change to upper case','analyed_text':analyze,"check":CHECKBOX}
        text = analyze
        #return render(request, 'analyze.html',param)
    if(newlineremove == 'on'):
        analyze = ""
        for char in text:
            if char!= '\n' and char!= '\r':
                analyze = analyze + char
        param = {'purpose':'remove new line','analyed_text':analyze,"check":CHECKBOX}
        text = analyze
       # return render(request, 'analyze.html',param)
    if(spaceremover == "on"):
        analyze = ""
        for index, char in enumerate(text):
            if text[index] == ' ' and text[index + 1] == " ":
                pass
            else:
                analyze = analyze + char
        param = {'purpose':'remove new line','analyed_text':analyze,"check":CHECKBOX}
        text = analyze
       # return render(request, 'analyze.html',param)
    #else:
     #   return HttpResponse("error no punctuatio remove")
    if(spaceremover == 'off' and newlineremove == "off" and fullcaps == "off" and CHECKBOX =="off"):
        return HttpResponse("nother happen")
    return render(request, 'analyze.html',param)
