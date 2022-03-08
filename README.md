# mémo-Laravel


##Routage 
__ Déclarer une route permet de lier une URI (identifiant de ressource uniforme, autrement dit la partie de l’adresse qui suit le nom de domaine) à un code à exécuter. Le routage est un moyen de créer une URL de requête pour votre application.__

##Relier un texte à une URL:

Route::get('/', function () {
    return 'Homepage';
    //affiche dans localhost "homepage"
}); 
