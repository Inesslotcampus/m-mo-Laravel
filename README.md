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

### Créer un controller

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

### View

- page view : txt php
- page controller 

(ex)function cart(){
        return view("cart");
    }


## Formulaire

__2 view, un avec le formulaire et un avec la réponse.__


CSRF=

### -view formulaire : @extends('template')

@section('content')

(formulaire html )
{{ csrf_field() }} //obligatoir sinon ça marche pas. protection

@endsection


### -réponse : (ex)

 @extends('template')

@section('content')

<h3>Firstname</h3>

            <p>valeur : <b>{{ $user['firstname'] }}</b></p>
            

@endsection

## Controller (ex) 

  public function store(Request $request)
    {
        $data = [
            'user' => [
                'firstname' => $request->input('firstname'),
                'lastname' => $request->input('lastname'),
                
            ],
        ];

        return view('user.result', $data);

    }

## Model

- Création model:

__php artisan make:model Table__
(maj pour la table)

- database migration:

__php artisan make:model Table --migration__

- primary key

__protected $primaryKey = 'table_id';__


- Building Queries

__$productcs = Products::where('champ', valeurQueTuVeux)

               ->orderBy('name')
               
               ->take(10)
               
               ->get();
