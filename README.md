# mémo-Laravel


## Routage 
__ Déclarer une route permet de lier une URI (identifiant de ressource uniforme, autrement dit la partie de l’adresse qui suit le nom de domaine) à un code à exécuter. Le routage est un moyen de créer une URL de requête pour votre application. (A faire dans route/web.php)__

### Relier un texte à une URL:

Route::get('/', function () {
    return 'Homepage';
    //affiche dans localhost "homepage"
}); 

### Relier un texte avec l'id à une URL:

Route::get('/user/{id}', function ($id) {
    return 'User '.$id;
});

## Créer un controller

__Aller sur la commande de vs code__

php artisan make:controller (nm controlleur)

-sur page controller: 

(ex) class CartController extends Controller
{
    //
    function cart(){
        return "Panier";
    }
}

-sur web.php:

(ex) Route::get('/home', [HomeController::class,"home"] );

##view

- page view : txt php
- page controller 

(ex)function cart(){
        return view("cart");
    }


