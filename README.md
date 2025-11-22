# Boutique Diayma

## Flux d'exécution - Affichage des produits sur l'écran d'accueil

### EN résumé voici les étapes : 

L'application démarre avec **Program.Main()** qui appelle **BuildWebHost()** pour créer l'hôte web. La classe **Startup** configure les services dans **ConfigureServices()** (injection de dépendances pour ProductRepository, ProductService, LanguageService, etc.) et le pipeline HTTP dans **Configure()** avec la route par défaut vers Product/Index.

Lors de l'accès à la page d'accueil, le conteneur d'injection de dépendances instancie **ProductRepository** dont le constructeur appelle **GenerateProductData()** pour créer 9 produits. Ensuite, **ProductService** est cré avec les dépendances injectées, puis **ProductController** reçoit ProductService et LanguageService.

Le contrôleur exécute **ProductController.Index()** qui appelle **ProductService.GetAllProducts()**. Cette méthode délègue à **ProductRepository.GetAllProducts()** qui filtre les produits en stock, les trie par nom et retourne un tableau converti en List<Product>.

Le contrôleur passe cette liste à la vue **Index.cshtml** qui itère sur les produits avec @foreach et génère un tableau HTML affichant nom, description, prix et stock pour chaque produit, avec support de la localisation.

**Namespaces:** P2FixAnAppDotNetCode, P2FixAnAppDotNetCode.Controllers, P2FixAnAppDotNetCode.Models.Services, P2FixAnAppDotNetCode.Models.Repositories  
**Classes:** Program, Startup, ProductController, ProductService, ProductRepository  
**Méthodes clés:** Main(), BuildWebHost(), ConfigureServices(), Configure(), ProductRepository(), GenerateProductData(), Index(), GetAllProducts()
