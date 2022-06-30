## Open-Closed Principle (OCP)
Software components must be closed for modification, but open to extension. <br/>
Closed for modifications means that new features getting added to the software component, should not have to modify existing code. <br/>
Open for extensions means that a software component should be extentable to add a new feature or new behavior to it. <br/>

The fist example is a company that cares your health, and calculate your discount if you are a loyal costumer:

```java
public class HealthInsuranceCostumerProfile {
    public boolean isLoyalCostumer() {
        return true; // or false
    }   
}

public class InsurancePremiumDiscountCalculator {

    public int calculatePremiumDiscountPercent(HealthInsuranceCostumerProfile costumer) {
        if(costumer.isLoyalCostumer()) {
            return 20;
        }
        return 0;
    }

}

```

Now supose that company now cares your car too:

```java
public class VehicleInsuranceCostumerProfile {
    public boolean isLoyalCostumer() {
        return true; // or false
    }   
}
```

InsurancePremiumDiscountCalculator class must be closed for modifications, so refactoring it, the first step is use a interface:

```java
public interface CostumerProfile {
    public boolean isLoyalCostumer();
}
```

Now the two costumers profile implements this interface:

```java
public class VehicleInsuranceCostumerProfile implements CostumerProfile {
  
  @Override  
  public boolean isLoyalCostumer() {
        return true; // or false
    }   
}

public class HealthInsuranceCostumerProfile implements CostumerProfile {
    
  @Override
  public boolean isLoyalCostumer() {
        return true; // or false
    }   
}
```

And the calculator don't recive more a class, but the interface:

```java
public class InsurancePremiumDiscountCalculator {

    public int calculatePremiumDiscountPercent(CostumerProfile costumer) {
        if(costumer.isLoyalCostumer()) {
            return 20;
        }
        return 0;
    }

}
```
