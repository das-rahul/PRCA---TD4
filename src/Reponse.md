#Exercice 1

* Q.1 :

Plusieurs threads peuvent exécuter en parallèle la fonction request(m) et release(m) et donc leur
actions seront entrelacées. Ce qui fait que malgrès qu'il n'y ai plus qu'un exemplaire
disponible à un moment donné, les deux threads peuvent l'utiliser.

Pour remédier à ceci, on peut utiliser l'exclusion mutuelle et donc de faire de la méthode
request(m) et release(m) des sections critiques, c'est-à-dire un code partagé qui ne peut être utilisé par un
seul thread à la fois.

=> Nous modifions de façon incohérente la ressource. Si deux threads s'exécutent 
en parallèle mais que le premier qui utilise la ressource s'interrompt avant la modification
de la ressource, la ressource reste inaccessible mais le deuxième thread ne le sait pas.



* Q.2 :

1.

    ````
    Mettre toute la tâche en synchronized
    ````
   
   => Si nous avons 5 ressources max et que le thread1 a besoin de 2 ressources et le thread2 de 2 ressources également, ils doivent quand même s'attendre, 
   l'exécution ne se fait pas en parallèle même s'il y a assez de ressources.

2. 
    ````
    Synchronized Procédure request(m){
        Tant que (NbRessDisponibles < m) faire attendre le processus appelant;
        NbRessDisponibles = NbRessDisponibles - 1 ;
    }
    
    Synchronized Procédure release(entier m) {
     NbRessDisponibles = NbRessDisponibles + m ;
     }
   
    Tant que (true){
        request(m);
        utiliser ressource m
        release(m);
    }
    ````
   
   => Incohérence, si deux threads veulent accèder à la ressource en même temps (admettons nous avons 50 ressources) et les deux demandent 25 ressources, normalement on devrait
   avoir 0 ressources au final mais vu qu'ils s'exécutent en même temps il restera 25 (alors qu'il n'y a 0 normalement).
   
   => Si jamais on a plusieurs requests => Famine : Des Threads peuvent ne jamais avoir accès à la ressource (car ordonnancement). Si nous faisons plusieurs request dans une même méthodes, et qu'il y a plusieurs
   Threads qui font la même chose que nous, nous pouvons arriver à un stade où on request une ressource avant de release et qu'on reste bloqué.
   
   
   ***
   
 ##Exercice 2
 
 
