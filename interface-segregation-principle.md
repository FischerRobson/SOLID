## Interface Segregation Principle (ISP)

No client should be force to depend on methods it does not use.

Violations of ISP:
* Fat interfaces
* Interfaces with low cohesion
* Empty method implementations

An example, imagine you create a interface with all operations that a printer can make.

```java
public interface IMultiFunction {
    public void print();

    public void getPrintSpoolDetail();

    public void scan();

    public void scanPhoto();

    public void fax();

    public void internetFax();
}
```

Then you have a XeroxWorkCenter class, a multi functional printer that make all those functions:

```java
public class XeroxWorkCenter implements IMultiFunction {

    @Override
    public void print() {
        // real code
    }

    @Override
    public void getPrintSpoolDetail() {
        // real code
    }

    @Override
    public void scan() {
        // real code
    }

    @Override
    public void scanPhoto() {
        // real code
    }

    @Override
    public void fax() {
        // real code
    }

    @Override
    public void internetFax() {
        // real code
    }
}
```

But you have a simple printer that just prints and scan, it does not send fax:

```java
public class HPPrinterScanner implements IMultiFunction {

    @Override
    public void print() {
        // real code
    }

    @Override
    public void getPrintSpoolDetail() {
        // real code
    }

    @Override
    public void scan() {
        // real code
    }

    @Override
    public void scanPhoto() {
        // real code
    }

    @Override
    public void fax() {
        
    }

    @Override
    public void internetFax() {
        
    }
}
```

And you have another printer, thats just print:

```java
public class CanonPrinter implements IMultiFunction {

    @Override
    public void print() {
        // real code
    }

    @Override
    public void getPrintSpoolDetail() {
        // real code
    }

    @Override
    public void scan() {
        
    }

    @Override
    public void scanPhoto() {
        
    }

    @Override
    public void fax() {
        
    }

    @Override
    public void internetFax() {
        
    }
}
```

So the correct way to do this, is split the interface:

```java
public interface IPrint {
    public void print();

    public void getPrintSpoolDetail();
}

public interface IScan {
    public void scan();

    public void scanPhoto();
}

public interface IFax {
    public void fax();

    public void internetFax();
}
```

Now the classes implementations is this:

```java
public class XeroxWorkCenter implements IPrint, IScan, IFax {

    @Override
    public void print() {
        // real code
    }

    @Override
    public void getPrintSpoolDetail() {
        // real code
    }

    @Override
    public void scan() {
        // real code
    }

    @Override
    public void scanPhoto() {
        // real code
    }

    @Override
    public void fax() {
        // real code
    }

    @Override
    public void internetFax() {
        // real code
    }
}

public class HPPrinterScanner implements IPrint, IScan {

    @Override
    public void print() {
        // real code
    }

    @Override
    public void getPrintSpoolDetail() {
        // real code
    }

    @Override
    public void scan() {
        // real code
    }

    @Override
    public void scanPhoto() {
        // real code
    }
}

public class CanonPrinter implements IPrint {

    @Override
    public void print() {
        // real code
    }

    @Override
    public void getPrintSpoolDetail() {
        // real code
    }
}
```
