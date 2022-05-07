# Replacing Constructors with Factory Methods and More

### Challenge Prompt:
+ Create a class called Athlete with subclasses Gold, Silver & Bronze winners
+ Make it so once an Athlete receives a medal no other Athletes can be assigned to that medals subclass
+ THe program isn't allowed to contain conditional statements

```java:
public abstract class Customer2{
     
    private String custRating;
    static final int PREMIER = 2;
    static final int VALUED = 1;
    static final int DEADBEAT = 0;

    public void getCustRating(){
        return custRating;
    }
    public void setCustRating(String custRating){
        this.custRating = custRating;
    }

    public static void main(String[] args){
        CustomerFactory customerFactory = new CustomerFactory();

        Customer2 goodCustomer = customerFactory.getCustomer(PREMIER);

        System.out.println("Customer Rating: " + goodCustomer.getCustRating());
    }

}

class Premier extends Customer2{

     Premier(){

         setCustRating("Premier Customer");
     }
}

class Valued extends Customer2{

     Valued(){

         setCustRating("Valued Customer");
     }
}

class Deadbeat extends Customer2{

     Deadbeat(){

         setCustRating("Deadbeat Customer");
     }
}

class CustomerFactory{
    public Customer2 getCustomer(int custType){

        switch(custType){

            case 2:
                return new Premier();
            case 1:
                return new Valued();
            case 0:
                return new Deadbeat();
            default:
                throw new IllegalArgumentException("Invalid Customer type");
        }
    }

}
```

Output:
```
Customer Rating: Premier Customer
```

### Refacored:
```java:
public abstract class Customer2{
     
    private String custRating;
    static final int PREMIER = 2;
    static final int VALUED = 1;
    static final int DEADBEAT = 0;

    public void getCustRating(){
        return custRating;
    }
    public void setCustRating(String custRating){
        this.custRating = custRating;
    }

    public static void main(String[] args){
        CustomerFactory customerFactory = new CustomerFactory();

        Customer2 goodCustomer = customerFactory.getCustomer("Premier");

        System.out.println("Customer Rating: " + goodCustomer.getCustRating());
    }

}

class Premier extends Customer2{

     Premier(){

         setCustRating("Premier Customer");
     }
}

class Valued extends Customer2{

     Valued(){

         setCustRating("Valued Customer");
     }
}

class Deadbeat extends Customer2{

     Deadbeat(){

         setCustRating("Deadbeat Customer");
     }
}

class CustomerFactory{
    public Customer2 getCustomer(String custName){

        try{
           
            return(Customer2) Class.forName(custName).newInstance();

        }
        catch(Exception e){

            System.out.println("Invalid Customer Type");

        }
    }

}
```
Output:
```
Customer Rating: Premier Customer
```



## Challenge:
```java:
public class Athlete{
    
    private String athleteName = "";

    public String getAthleteName(){
        return athleteName;
    }

    public void setAthleteName(String athleteName){
        this.athleteName = athleteName;
    }

    public static Athlete getInstance(){
        return null;
    }
}

class GoldWinner extends Athlete{
    private static GoldWinner goldAthlete = null;

    private GoldWinner(String athlete){
        setAthlete(athleteName);
    }

    public static GoldWinner getInstance(String athleteName){
        if(goldAthlete == null){

            goldAthlete = new GoldWinner(athleteName);
        }

        return goldAthlete;
    }

    
}

class SilverWinner extends Athlete{
    private static SilverWinner silverAthlete = null;

    private GoldWinner(String athlete){
        setAthlete(athleteName);
    }

    public static SilverWinner getInstance(String athleteName){
        if(silverAthlete == null){

            silverAthlete = new SilverWinner(athleteName);
        }

        return silverAthlete;
    }

    
}

class BronzeWinner extends Athlete{
    private static BronzeWinner bronzeAthlete = null;

    private BronzeWinner(String athlete){
        setAthlete(athleteName);
    }

    public static BronzeWinner getInstance(String athleteName){
        if(bronzeAthlete == null){

            bronzeAthlete = new BronzeWinner(athleteName);
        }

        return bronzeAthlete;
    }

    
}

class MedalFactory{

    public Athlete getMedal(String medalType, String athleteName){

        try{
            Class[] athleteNameParamete = new Class[]{String.class};

            Method getInstanceMethod = Class.forName(medalType).getMethod("getInstance", athleteNameParameter);

            Object[] params = new Object[]{ new String(athleteName) };

            return (Athlete) getInstanceMethod.invoke(null, params);
        }

        catch(Exception e){

            throw new IllegalArgumentException("Invalid Athlete Type");
        }
    }

}

class testMedalWinner{
    public static void main(String[] args){

        MedalFactory medalFactory = new MedalFactory();

        Athlete goldWinner = medalFactory.getMedal("GoldWinner", "D T");
        Athlete silverWinner = medalFactory.getMedal("SilverWinner", "T D");
        Athlete bronzeWinner = medalFactory.getMedal("BronzeWinner", "M M");
        
    }
}
```