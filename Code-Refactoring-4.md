```java:
public class Customer{

    private String firstName = "";
    private String lastName = "";
    private String street = "";
    private String city = "";
    private String state = "";
    private int postalCode = 0;
    private String birthDay = "";

    public Customer(String firstName, String lastName, String street, String city, String state, int postalCode, String birthDay) {
        super();
        this.firstName = firstName;
        this.lastName = lastName;
        this.street = street;
        this.city = city;
        this.state = state;
        this.postalCode = postalCode;
        this.birthDay = birthDay;
    }
    
}

```
==========================================
```java:
public class Customer{

    private String firstName = "";
    private String lastName = "";
    private String birthDay = "";

    private Address address = null;

    public Customer(String firstName, String lastName, String birthDay, Address address) {
        super();
        this.firstName = firstName;
        this.lastName = lastName;
        this.birthDay = birthDay;
        this.address = address;
    }

    public static void main(String[] args){
        Address sallySmithAddress = new Address("", "", "", 12345);

        Customer sallySmith = new Customer("", "", "", sallySmithAddress);

        System.out.print("Customer: " + sallySmith.getFirstName + ... );
        System.out.print("Customer address: " + sallySmith.address);
    }
    
}

class Address {
    private String street = "";
    private String city = "";
    private String state = "";
    private int postalCode = 0;


    public Address(String street, String city, String state, int pastalCode) {

        this.street = street;
        this.city = city;
        this.state = state;
        this.postalCode = postalCode;
    }

    public String toString(){
        return getStreet() + " " + getCity() + " " + getState() + " " + getPostalCode();
    }

}   

```
==========================================
```java:
public class Customer{

    private String firstName = "";
    private String lastName = "";
    private String birthDay = "";

    private Address address = null;
    private Birthday birthDay = null;

    public Customer(String firstName, String lastName, Birthday birthDay, Address address) {
        super();
        this.firstName = firstName;
        this.lastName = lastName;
        this.birthDay = birthDay;
        this.address = address;
    }

    public static void main(String[] args){
        Address sallySmithAddress = new Address("", "", "", 12345);
        Birthday sallySmithBirthday = new Birthday(1,1,1);

        Customer sallySmith = new Customer("", "", "", sallySmithAddress);

        System.out.print("Customer: " + sallySmith.getFirstName + ... );
        System.out.print("Customer address: " + sallySmith.address);
        System.out.print("Customer Birthday: " + sallySmith.birthday);
    }
    
}

class Address {
    private String street = "";
    private String city = "";
    private String state = "";
    private int postalCode = 0;


    public Address(String street, String city, String state, int pastalCode) {

        this.street = street;
        this.city = city;
        this.state = state;
        this.postalCode = postalCode;
    }

    public String toString(){
        return getStreet() + " " + getCity() + " " + getState() + " " + getPostalCode();
    }

}   

class Birthday{
    private int day;
    private int month;
    private int year;

    public Birthday(int day, int month, int year){
        this.day = day;
        this.month = month;
        this.year = year;
    }

    public String getBirthDate() {
        return getDay() + "/" + getMonth() + "/" + getYear();
    }
}

```