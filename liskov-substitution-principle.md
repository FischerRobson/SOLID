## Liskov Substitution Principle (LSP)

Objects should be replaceable with ther subtypes without affecting the correctness of the program. <br/>
If it looks like a duck and quack like a duck but it need batteries, you probably have the wrong asbtraction. <br/>
Break the hierarchy if it fails the substitution test. <br/>


```java
public class Bird {
    public void fly() {
        // fly high
    }
}

public class Ostrich extends Bird {

    @Override
    public void fly() {
        throw new RuntimeException(); // Ostrich dont fly
    }
}
```

As you see, Ostrich can't substitute Bird cause it don't fly.

```java
public class Car {
    public double getCabinWidth() {
        // return cabin width
    }
}

public class RacingCar extends Car {
    
  @Override
    public double getCabinWidth() {
        // UNIMPLEMENTED
    }
    
    public double getCockpitWidth() {
        // return cockpit width
    }
}

public class CarUtils {
    public static main(String[] args) {
        Car first = new Car();
        Car second = new Car();
        Car third = new RacingCar();

        List<Car> myCars = new ArrayList<>();
        myCars.add(first);
        myCars.add(second);
        myCars.add(third);

        for (Car car: myCars) {
            System.out.println(car.getCabinWidth());
        }
    }
}
```

When thrid car be itareted, an Exception will be throwed. <br />
So refactoring it, both Car and RacingCar will be extensions of a new generic class Vehicle:

```java
public class Vehicle {
    public double getInteriorWidth() {
        // return interior width
    }
}

public class Car extends Vehicle {

    @Override
    public double getInteriorWidth() {
        return this.getCabinWidth();
    }

    public double getCabinWidth() {
        // return cabin width
    }
}

public class RacingCar extends Vehicle {

    @Override
    public double getInteriorWidth() {
        return this.getCockpitWidth();
    }

    public double getCockpitWidth() {
        // return cockpit width
    }
}

public class VehicleUtils {
    public static main(String[] args) {
        Vehicle first = new Car();
        Vehicle second = new Car();
        Vehicle third = new RacingCar();

        List<Vehicle> myVehicles = new ArrayList<>();
        myVehicles.add(first);
        myVehicles.add(second);
        myVehicles.add(third);

        for (Vehicle vehicle: myVehicles) {
            System.out.println(vehicle.getInteriorWidth());
        }
    }
}
```
