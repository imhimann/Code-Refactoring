# How to Extract Methods
- Used to turn cod fragments into a method with a descriptive name
- Used to make code as readable

### Example

Problem:
```java:
public class FootballPlayer40YardDashInfo {

    ArrayList<FootballPlayer> players = new ArrayList<FootballPlayer>();

    publoic void addFootballPlayer(FootballPlayer player){
        players.add(player);
    }

    public void printPlayerInfo(){
        double avg40YdTime = 0.0;
        System.out.printf("%-15s %15s", "Name", "Avg 40 Time\n");
        
        //Print dashes
        for(int i = 0; i < 30; i++ ){System.out.print("_");}
        System.out.println();

        for(FootballPlayer player : players){
            System.out.printf("%-19s", player.getName());

            double total40YdDashTimes = 0.0;
            double[] fortyYardDashTimes = player.get40YardDashTimes();

            for(int i = 0; i < player.get40YardDashTimes().length; i++){
                total40YdDashTimes += fortyYardDashTimes[i];
            }

            avg40YdTime = total40YdDashTimes / player.get40YardDashTimes().length;
            
            System.out.printf("%1$.2f", avg40YdTime);
            System.out.println();
        }
    }

    //Main Method//
}

```

Solution:
- Method 1
```java:
public class FootballPlayer40YardDashInfo {

    ArrayList<FootballPlayer> players = new ArrayList<FootballPlayer>();

    publoic void addFootballPlayer(FootballPlayer player){
        players.add(player);
    }

    public void printPlayerInfo(){
        double avg40YdTime = 0.0;

        printTitles();   // Add printTitles method back
        
        for(FootballPlayer player : players){
            System.out.printf("%-19s", player.getName());

            double total40YdDashTimes = 0.0;
            double[] fortyYardDashTimes = player.get40YardDashTimes();

            for(int i = 0; i < player.get40YardDashTimes().length; i++){
                total40YdDashTimes += fortyYardDashTimes[i];
            }

            avg40YdTime = total40YdDashTimes / player.get40YardDashTimes().length;
            
            System.out.printf("%1$.2f", avg40YdTime);
            System.out.println();
        }
    }

    public void printTitles(){
        
        System.out.printf("%-15s %15s", "Name", "Avg 40 Time\n");
        
        //Print dashes
        for(int i = 0; i < 30; i++ ){System.out.print("_");}
        System.out.println();

    }

    //Main Method//
}
```

- Method 2
```java:
public class FootballPlayer40YardDashInfo {

    ArrayList<FootballPlayer> players = new ArrayList<FootballPlayer>();

    publoic void addFootballPlayer(FootballPlayer player){
        players.add(player);
    }

    public void printPlayerInfo(){

        printTitles();   

        printPlayersWith40Avg(); // Extract to a method
        
        
    }

    public void printTitles(){
        
        System.out.printf("%-15s %15s", "Name", "Avg 40 Time\n");
        
        //Print dashes
        for(int i = 0; i < 30; i++ ){System.out.print("_");}
        System.out.println();

    }

    public void printPlayersWith40Avg(){

        for(FootballPlayer player : players){
            System.out.printf("%-19s", player.getName());

            double total40YdDashTimes = 0.0;
            double[] fortyYardDashTimes = player.get40YardDashTimes();

            for(int i = 0; i < player.get40YardDashTimes().length; i++){
                total40YdDashTimes += fortyYardDashTimes[i];
            }

            double avg40YdTime = total40YdDashTimes / player.get40YardDashTimes().length;
            
            System.out.printf("%1$.2f", avg40YdTime);
            System.out.println();
        }

    }

    //Main Method//
}
```

- Method 3
```java:
public class FootballPlayer40YardDashInfo {

    ArrayList<FootballPlayer> players = new ArrayList<FootballPlayer>();

    publoic void addFootballPlayer(FootballPlayer player){
        players.add(player);
    }

    public void printPlayerInfo(){

        printTitles();  

        printPlayersWith40Avg();
        
        
    }

    public void printTitles(){
        
        System.out.printf("%-15s %15s", "Name", "Avg 40 Time\n");
        
        //Print dashes
        printCharMultTimes("_", 30);  //Extract to a method of itself


    }

    public void printCharMultTimes(char charToPrint, int howManyTimes){
        
        for(int i = 0; i < howManyTimes; i++ ){System.out.print(charToPrint);}
        System.out.println();
    }

    public void printPlayersWith40Avg(){

        for(FootballPlayer player : players){
            System.out.printf("%-19s", player.getName());

            double total40YdDashTimes = 0.0;
            double[] fortyYardDashTimes = player.get40YardDashTimes();

            for(int i = 0; i < player.get40YardDashTimes().length; i++){
                total40YdDashTimes += fortyYardDashTimes[i];
            }

            double avg40YdTime = total40YdDashTimes / player.get40YardDashTimes().length;
            
            System.out.printf("%1$.2f", avg40YdTime);
            System.out.println();
        }

    }

    //Main Method//
}
```