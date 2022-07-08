## Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions.
Abstractions should not depend on details. Details should depend on abstractions.

To understand high-level and low-level modules, see this example:

![high-and-low-modules.png](inkdrop://file:tU3nxptw1)

Taking a look at the Product module, the ProductCatalog depends on SQLProductRepository:

```java
public class SQLProductRepository {

    public List<String> getAllProductNames() {
        return Arrays.asList("soap", "toothpaste");
    }

}

public class ProductCatalog {
    
    public void getAllProductNames() {
        SQLProductRepository sqlProductRepository = new SQLProductRepository();

        List<String> allProductNames = sqlProductRepository.getAllProductNames();

        // display product names
    }
}
```

So refactoring it:

```java
public interface ProductRepository {

    public List<String> getAllProductNames();

}

public class ProductFactory {

    public static ProductRepository create() {
        return new SQLProductRepository();
    }

}

public class SQLProductRepository implements ProductRepository {

    public List<String> getAllProductNames() {
        return Arrays.asList("soap", "toothpaste");
    }

}

public class ProductCatalog {

    public void getAllProductNames() {
        ProductRepository productRepository = ProductFactory.create();

        List<String> allProductNames = productRepository.getAllProductNames();

        // display product names
    }
}
```

Applying dependency injection:

```java
public class ProductCatalog {
    
    private ProductRepository productRepository;
    
    public ProductCatalog(ProductRepository productRepository) {
        this.productRepository = productRepository;
    }

    public void getAllProductNames() {
        List<String> allProductNames = productRepository.getAllProductNames();
        // display product names
    }
}


public class ECommerceMainApplication {
    public static void main(String[] args) {
        ProductRepository productRepository = ProductFactory.create();
        
        ProductCatalog productCatalog = new ProductCatalog(productRepository);
        
        productCatalog.getAllProductNames();
    }
}
```
