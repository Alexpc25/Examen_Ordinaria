# Examen_Ordinaria
Ej 1 de tweeter


#clase UserAccount
 ```
 from datetime import datetime as date
from Tweet import Tweet
from Email import Email  


class UserAccount():

    id = 0
    #he añadido un atributo estático que sirva como contador de cuentas cuentas existen 

    def __init__(self,alias,email, tweets):
        self.__alias = alias
        #nombre únivoco de la cuenta, un str

        self.__email = email
        #correo asociado a la cuenta

        if type(email) != Email:
            raise TypeError("Tipo invalido para email")
        #puesto que la clase Email ya existe según el enunciado, se crea un aviso de error en caso de que el email introducido al instanciar la cuenta no sea de calse Email

        self.__tweets = tweets
        #tweets almancena todos los tweets publicados por la cuenta

        if type(tweets) != Tweet:
            raise TypeError("Tipo invalido para tweets")
        #puesto que la clase Tweet ya existe según el enunciado, se crea un aviso de error en caso de que el tweets introducido al instanciar la cuenta no sea de calse Tweet

        self.__followers = []
        #followers es una lista que no se pasa al instanciar un usuario, si no que se van añadiendo followers segun se utilize la función follow

        self.__timeline = []
        #el timeline almaneca los tweets que se publican las cuantas a las que sigue el usuario
        
        self.__direct_message = {}
        #cumple una función similar al timeline, pero perimite la comunicación privida entre 2 usuarios. 
        #lleva estrutura de diccionario, porque voy a almacenar como clave el usuario que manda el mensaje y como valor el mensaje

        UserAccount.id += 1

    
    def get_alias(self): 
        return self.__alias

    def get_email(self): 
        return self.__email

    def get_followers(self): 
        return self.__followers

    def get_timeline(self): 
        return self.__timeline


    #ninguno de los atributos debería ser modificado desde fuera por eso no hay setters, y los direct message son privados por eso no hay getter. 


    def follow(self, user2):
        user2.followers.append(self.__alias)
        #el usiar pasa a ser follower de user2

    def num_followers(self): 
        return len(self.__followers)
        #metodo que lleva el conteo de cuantos seguidores tiene una cuenta


    def tweet(self, tweet1):
        self.__tweets.append(tweet1)

        for elemento in self.__followers:
            elemento.timeline.append(tweet1)
        #se añande el tweet publicado por el usuario al timeline de sus followers


    def use_direct_message(self, mensaje): 
        self.__direct_message[self.__alias] = [mensaje,date.now()]
        #por cada llamada a este método, se cra una entrada en el diccionario con el alias como clave y una dupla (mensaje y la hora del mensaje) como valor. 
   ```
   
   #Clase Tweet
```
from datetime import datetime as date
from examen_ej1 import UserAccount



class Tweet():

    registro_tweets = []

    def __init__(self,message, sender): 
        self.__sender = sender

        if type(sender) != UserAccount:
            raise TypeError("Tipo invalido para email")
        #Sender tiene que pertenecer a la clasze UserAccount

        self.__tweet_hora = [message, date.now()]

        Tweet.registro_tweets.append({self.__sender : self.tweet_hora})

        #se registran todos los tweets que se han hecho y quien los ha hecho

```

#clase Retweet
```
from examen_ej1 import UserAccount
from Tweet import Tweet
from datetime import datetime as date

class Retweet(Tweet): 
    def __init__(self, message):
        self.__message = message

    def retweetear(self, user2):
        retweet = {Tweet.__tweet_hora : [self.__message, date.now()]}

        user2.__timeline.append(retweet)

        #cuando se llama a esta función, se crea un diccionario, donde la clave es el mensaje original y el valor el mensaje retweeteado
        #luego se añade este retweet al timeline del user2
  ```

