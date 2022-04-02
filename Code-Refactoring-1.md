# The Bad Smells

- Duplicated Code
- Long Methods
- Complex Conditional Statements
- Primitive Obsession
- Indecent Exposure
- Solution Sprawl
- ALternative Classes with Different Interfaces
- Lazy Classes
- Large Classes
- Switch Statements
- Combinatorial Explosions
- Oddball Solutions

# Creation Problems
- Replace Constructors with Creation Methods
    - Which constructor should be called?
    - Wish constructors had descriptive names?
    - Constructors can't have the same attribute signatures

### Example
Problem:
```java:
//Demonstrate the Creation Method replacement of Constructors

public class FootballPlayer{

    private double passerRating; 
    private int rushingYards; 
    private int receivingYards; 
    private int totalTackles;
    private int interceptions;
    private int fieldGoals;
    private double avgPunt;
    private double avgKickoffReturn;
    private double avgPuntReturn;

    FootballPlayer(double passerRating, int rushingYard){
        this.passerRating = passerRating;
        this.rushingYards = rushingYards;
    }

    FootballPlayer(int rushingYards){
        this.rushingYards = rushingYards;
    }

    FootballPlayer(int receivingYards){
        this.receivingYards = receivingYards;
    }

}
```

Solution:
```java:
//Demonstrate the Creation Method replacement of Constructors

public class FootballPlayer{

    private double passerRating; 
    private int rushingYards; 
    private int receivingYards; 
    private int totalTackles;
    private int interceptions;
    private int fieldGoals;
    private double avgPunt;
    private double avgKickoffReturn;
    private double avgPuntReturn;

    private FootballPlayer(double passerRating, int rushingYards, int receivngYards, int totalTackles, int interceptions, int fieldGoals, double avgPunt, double avgKickoffReturn, double avgPuntReturn){

        this.passerRating = passerRating;
        this.rushingYards = rushingYards;
        this.totalTackles = totalTackles;
        this.interceptions = interceptions;
        this.avgPunt = avgPunt;
        this.avgKickoffReturn = avgKickoffReturn;
        this.avgPuntReturn = avgPuntReturn;
    }

    public static FootballPlayer createQB(double passerRating, int rushingYards){
        return new FootballPlayer(passerRating, rushingYards, 0, 0, 0, 0, 0, 0, 0);

    }
    

}
```

## Avoid Duplication & Chain Constructors
- More constructors, More problems
- General purpose constructors save the day

Problem:
```java:
public class FootballPlayer2 {
    private String playerName = "";
    private String college = "";
    private double fortyYardDash = 0.0;
    private int repsBenchPress = 0;
    private double sixtyYardDash = 0.0;

    public FootballPlayer2(String playerName, String college, double fortyYardDash, double sixtyYardDash){
        this.playerName = playerName;
        this.college = college;
        this.fortyYardDash = fortyYardDash;
        this.sixtyYardDash = sixtyYardDash;
    }

    public FootballPlayer2(String playerName, String college, double fortyYardDash, int repsBenchPress){
        this.playerName = playerName;
        this.college = college;
        this.fortyYardDash = fortyYardDash;
        this.repsBenchPress = repsBenchPress;
    }

    public FootballPlayer2(String playerName, String college, double fortyYardDash, int repsBenchPress, double sixtyYardDash){
        this.playerName = playerName;
        this.college = college;
        this.fortyYardDash = fortyYardDash;
        this.repsBenchPress = repsBenchPress;
        this.sixtyYardDash = sixtyYardDash;
    }
    
}

```

Solution:
```java:
public class FootballPlayer2 {
    private String playerName = "";
    private String college = "";
    private double fortyYardDash = 0.0;
    private int repsBenchPress = 0;
    private double sixtyYardDash = 0.0;

    public FootballPlayer2(String playerName, String college, double fortyYardDash, int repsBenchPress, double sixtyYardDash){
        this.playerName = playerName;
        this.college = college;
        this.fortyYardDash = fortyYardDash;
        this.repsBenchPress = repsBenchPress;
        this.sixtyYardDash = sixtyYardDash;
    }

    public FootballPlayer2(String playerName, String college, double fortyYardDash, int repsBenchPress){
        this(playerName, college, fortyYardDash, repsBenchPress, 0.0);

    }

    public FootballPlayer2(String playerName, String college, double fortyYardDash, double sixtyYardDash){
        this(playerName, college, fortyYardDash, 0, sixtyYardDash);

    }

    
}

```