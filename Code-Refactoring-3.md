
## Example 1
### Bad Code
```java:
public class Product {
    private String name = "";
    private double price = 0.0;
    private double shippingCost = 0.0;
    private int quantity = 0;

    Product(String name, double price, double shippingCost, int quantity){

        this.name = name;
        this.price = price;
        this.shippingCost = shippingCost;
        this.quantity = quantity;

    }

    public double getTotalCost(){

        double quantityDiscount = 0.0;

        if((quantity>50) || ((quantity*price)>500)){
            quantityDiscount = .10;
        } else if ((quantity>25) || ((quantity*price)>100)){
            quantityDiscount = .07;
        } else if ((quantity>=10) || ((quantity*price)>50)){
            quantityDiscount = .05;
        }

        double discount = ((quantity-1)*quantityDiscount)*price;
    }

}
```

### Solution
```java:
public class Product {
    private String name = "";
    private double price = 0.0;
    private double shippingCost = 0.0;
    private int quantity = 0;

    Product(String name, double price, double shippingCost, int quantity){

        this.name = name;
        this.price = price;
        this.shippingCost = shippingCost;
        this.quantity = quantity;

    }

    public double getTotalCost(){

        double quantityDiscount = 0.0;


        //Creating Finals
        final boolean over50Products = (quantity>50) || ((quantity*price)>500);
        final boolean over25Products = (quantity>25) || ((quantity*price)>100);
        final boolean over10Products = ((quantity>=10) || ((quantity*price)>50);

        if(over50products){
            
            quantityDiscount = .10;

        } else if(over25products){
            
            quantityDiscount = .07;

        } else if(over10products){
            
            quantityDiscount = .05;

        }

    }
}

```



## Example 2

### Bad Code
```java:
public class Store{
    public ArrayList<Product> theProducts = new ArrayList<Product>();

    public void addAProduct(Product newProduct){
        theProducts.add(newProduct);
    }

    public void getCostOfProducts(){

        for(Product product : theProducts){

            System.out.println("Total cost for " + product.getQuantity() + " " + product.getName() + "s is $" + product.getTotalCost());

            System.out.println("Cost per product " + product.getTotalCost() / product.getQuantity() );

            System.out.println("Savings per product " + ((product.getPrice() + product.getShipping()) - (product.getTotalCostr() / product.getQuantity())) + "\n"); 

            
        }
    }
}

```

### Solution
```java:
public class Store{
    public ArrayList<Product> theProducts = new ArrayList<Product>();

    public void addAProduct(Product newProduct){
        theProducts.add(newProduct);
    }

    public void getCostOfProducts(){

        for(Product product : theProducts){

            //Creating Finals
            final int numOfProducts = product.getQuantity();
            final String prodName = product.getName();
            final double cost = product.getTotalCost();

            final double costWithDiscount = product.getTotalCost() / product.getQuantity();
            final double costWithoutDiscount = product.getPrice() + product.getShipping();

            System.out.println("Total cost for " + numOfProducts + " " + prodName + "s is $" + cost);

            System.out.println("Cost per product " + costWithDiscount );

            System.out.println("Savings per product " + ((costWithoutDiscount) - (costWithDiscount)) + "\n"); 

            
        }
    }
}

```