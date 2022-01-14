# WGET Headers

So, we begin with the full string from the solution to picoCTF's "Who are you?" challange:

    wget http://mercury.picoctf.net:46199/ -U PicoBrowser --header='Referer: http://mercury.picoctf.net:46199/' --header='Date: 2018' --header='X-Forwarded-For: 80.80.28.16' --header='DNT: dnt' --header='Accept-language: sv'

### wherein:

    wget http://mercury.picoctf.net:46199/ 
is the standard command to which we add the headers:

    -U PicoBrowser

to give us our **UserAgent** as '*PicoBrowser*'

    --header='Referer: http://mercury.picoctf.net:46199/' 

To set our **Referer** back to the same page we are WGET-ing

    --header='Date: 2018' 

asks for the site from 2018

    --header='X-Forwarded-For: 80.80.28.16' 

gives our our country by IP. This one is for Sweeden as per the challange, but you can Google "*IPs in Whateverastan*" for similar results.

    --header='DNT: dnt' 

is the **Do Not Track** header, and

    --header='Accept-language: sv'

Sets the user's language, in this case to Sweedish
