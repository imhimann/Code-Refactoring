# How to Extract Methods
- Used to turn cod fragments into a method with a descriptive name
- Used to make code as readable

### Example 1

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
- Step 1
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

- Step 2
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

- Step 3
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

### Example 2
```java:
double average = 0.0;
double[] dashTimes {4.36, 4.59, 4.41};
for(int i=0; i < dashTimes.length; i++){
    totalDashTimes += dashTimes;
}
average = totalDashTimes / dashTimes.length;

```

- Solution:
```java:
double[] dashTimes {4.36, 4.59, 4.41};
double average = getAvgDashTime(dashTimes);

public static double getAvgDashTime(double[] dashTimes){
    double[] dashTimes {4.36, 4.59, 4.41};
for(int i=0; i < dashTimes.length; i++){
    totalDashTimes += dashTimes;
}
return totalDashTimes / dashTimes.length;
}

```

## When to NOT extract methods
- If the code is as clear as a method don't extract the method

### Example
```java:
String inTop15 = checkIFInTop15(avg40YdTime) ? " *Top 15\n : \n";

public boolean checkIfInTop15(double avg40YdTime){

    return avg40YdTime < 4.41;
}

String inTop15 = (avg40YdTime < 4.41) ? "*Top 15\n : \n";

```

## When to Get Rid of Temps
- The temp is used once and doesn't add to understanding
- The temp holds the value of an expression

### Example 1
```java:
double dashTime = 4.50;

double avg40YdDash = getAvgDashTime();

String dasgGrade = ((dashTime <= avg40YdDash) ? "Good":"Bad");

System.out.println("That was a " + dashGrade + " time" ); 
```

Solution
```java:
double dashTime = 4.50;

String dasgGrade = ((dashTime <= getAvgDashTime()) ? "Good":"Bad");

System.out.println("That was a " + dashGrade + " time" ); 
```

### Example 2
```java:
double avgDashTime = totalDashTime / totalDashes;

if(avgDashTime > 4.41){
    System.out.println ("Average time....");

    
}

```

Solution:
```java:

if(avgDashTime() > 4.41){ System.out.println ("Average time...."); }

double avgDashTime(){
    return totalDashTime / totalDashes;
}

```