# mémo-Laravel

schéma Laravel: https://miro.medium.com/max/1400/1*Vu2ThQPxr72UEOP0LMo4hA.jpeg

GET
La méthode GET demande une représentation de la ressource spécifiée. Les requêtes GET doivent uniquement être utilisées afin de récupérer des données.

POST
La méthode POST est utilisée pour envoyer une entité vers la ressource indiquée. Cela entraîne généralement un changement d'état ou des effets de bord sur le serveur.

PUT
La méthode PUT remplace toutes les représentations actuelles de la ressource visée par le contenu de la requête.

DELETE
La méthode DELETE supprime la ressource indiquée.

## Routage 
__ Déclarer une route permet de lier une URI (identifiant de ressource uniforme, autrement dit la partie de l’adresse qui suit le nom de domaine) à un code à exécuter. Le routage est un moyen de créer une URL de requête pour votre application. (A faire dans route/web.php)__
__URI: L'URI est un identifiant.__

__URL: L'URL fournit des informations sur l'obtention d'une ressource..__



### Routage :Relier un texte à une URL:

- Route::get('/', function () {
    return 'Homepage';
    //affiche dans localhost "homepage"
}); 

- Relier un texte avec l'id à une URL:

Route::get('/user/{id}', function ($id) {
    return 'User '.$id;
});

- Route::ressources mix de plusieurs actions
    - Get -> index
    - Get -> create
    - post -> store
    - Get -> show 
    - Get -> edit
    - put/patch -> update 
    - delete -> destroy 

Route::resource('photos', PhotoController::class);



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

protected $table="product";


- Building Queries

- Dans controller
- 
__$productcs = Products::where('champ', valeurQueTuVeux)

               ->orderBy('name')
               
               ->take(10)
               
               ->get();
               
               
               
               
### Step 6 : création d'une selection entre l'ordre croissant des prix et de noms

-Route:

Route::post('/product/sort', [ProductController::class,"store"]);

-controller: 

 public function store(Request $request)
    {
        
        if ($request->input('product'//nom de mon select) == 'name') {
            $product = Product::where('available', 1)

                ->orderBy('name')
                ->get();


            return view('product-list', ['products' => $product]);
        } else {
            $product = Product::where('available', 1)

                ->orderBy('price')
                ->get();


            return view('product-list', ['products' => $product]);
        }
    }
}
