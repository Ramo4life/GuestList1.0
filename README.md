import java.util.*;

public class App {
    static Scanner input = new Scanner(System.in);  // Create a Scanner object
    static void Listprint(String[][] Guests){
        for (int i = 0; i < Guests.length; i++) {
            for (int j = 0; j < 2; j++) {
                if(Guests[i].length == 0){
                    continue;
                }
                if (j == 0){
                    System.out.print("Guest "+(i+1)+", "+ "name: " + Guests[i][j]);
                }else{
                    System.out.println(" age: " + Guests[i][j]);
                }
                
            }
        }
    }
    static void Stats(String[][] Guests){
        int NumberOfGuests = Guests.length;
        int NumberOfAdults = 0;
        int NumberOfChildren = 0;
        String[] OldestPerson = Guests[0];
        String[] YoungestPerson = Guests[0];

        //number of Guests
        for (int i = 0; i < Guests.length; i++) {
            if(Guests[i].length == 0){
                NumberOfGuests--;
            }
        }

        //Number of Adults and Children
        for (int i = 0; i < Guests.length; i++) {
            if(Guests[i].length == 0){
                continue;
            }
            if (Integer.parseInt(Guests[i][1]) > 13) {
                NumberOfAdults++;
                continue;
            }
            else{
                NumberOfChildren++;
                continue;
            }                       
    }
        //Oldest person
        for (int j = 0; j < (Guests.length-1); j++) {
            if((Guests[j].length == 0)|| (Guests[j+1].length == 0)){
            continue;
        }
        if (Integer.parseInt(Guests[j+1][1]) > Integer.parseInt(Guests[j][1])) {
            OldestPerson = Guests[j+1];
            }
        }

        //Youngest person
        for (int j = 0; j < (Guests.length-1); j++) {
            if((Guests[j].length == 0)|| (Guests[j+1].length == 0)){
            continue;
        }
        if (Integer.parseInt(Guests[j+1][1]) < Integer.parseInt(Guests[j][1])) {
            OldestPerson = Guests[j+1];
            }
        }

    System.out.println("Number of Guests: "+NumberOfGuests);
    System.out.println("Number of Adults: "+NumberOfAdults);
    System.out.println("Number of Children: "+NumberOfChildren);
    System.out.println("Oldest person: "+Arrays.toString(OldestPerson));
    System.out.println("Youngest person: "+Arrays.toString(YoungestPerson));
    }
    static int CheckForAdd(String[][] Guests){
        for (int i = 0; i < Guests.length; i++) {
            if(Guests[i].length == 0){
                return i; //returns the empty spot
            }
    } return -1;
}
    static String[][] AddGuest(String[][] Guests,int freeSpot){
        System.out.print("Please enter the guests name: ");
            String NewGuestName = input.nextLine() ;
            System.out.print("Please enter the guests age: ");
            String NewGuestAge = input.nextLine() ;
            String[][] copy = new String[Guests.length][2];
                for (int i = 0, j = 0; i < Guests.length; i++) {
                    if (i != freeSpot) {
                        copy[j++] = Guests[i];
                    }else{
                        copy[j][0] = NewGuestName;
                        copy[j][1] = NewGuestAge;
                        j++;
                    }
                }
                return copy;         
}
    static int VaildGuestNum(String[][] Guests){
        int WhichGuest = -1;
        boolean VaildGuestNumber = false;
        while (!VaildGuestNumber) {
            try {
                System.out.println("\nPlease enter which guest (Use the Guest number, type '0' to exit)");
                WhichGuest = Integer.parseInt(input.nextLine())-1; ;
                if((WhichGuest == -1)){
                    return -1;
                }else if((WhichGuest >= 0 || WhichGuest <= Guests.length) && (Guests[WhichGuest].length >  0)){
                    VaildGuestNumber = true;
                }
                else{
                    System.out.println("Please Enter a Vaild Number");
                }
            } catch (Exception e) {
                System.out.println("Please Enter a Vaild Number");
            }
        }
        return WhichGuest;
    }
    static int VaildGuestNumC(String[][] Guests){
        int WhichGuest = -1;
        boolean VaildGuestNumber = false;
        while (!VaildGuestNumber) {
            try {
                System.out.println("\nPlease enter which guest (Use the Guest number, type '0' to exit)");
                WhichGuest = Integer.parseInt(input.nextLine())-1; ;
                if((WhichGuest == -1)){
                    return -1;
                }else if(WhichGuest >= 0 || WhichGuest <= Guests.length){
                    VaildGuestNumber = true;
                }
                else{
                    System.out.println("Please Enter a Vaild Number");
                }
            } catch (Exception e) {
                System.out.println("Please Enter a Vaild Number");
            }
        }
        return WhichGuest;
    }
    static boolean CheckForRemove(String[][] Guests){
            for (int i = 0; i < Guests.length; i++) {
                if(Guests[i].length != 0){
                    return true;
                        }
    }return false;
}
    static String[][] RemoveGuest(String[][] Guests){
        Listprint(Guests);
        int GuestNum = VaildGuestNum(Guests);

        String[][] copy = new String[Guests.length][2];
        String[][] Empty = {{}};
        for (int i = 0, j = 0; i < Guests.length; i++) {
            if (i == GuestNum) {
                copy[j++] = Empty[0];
            }else{copy[j++] = Guests[i];}
        }
        return copy;
    }
    static String[][] ChangeGuestName(String[][] Guests){
        
        int GuestNum = VaildGuestNum(Guests);
        if (GuestNum == -1){
            return Guests;
        }
        boolean isNumber = true;
        while (isNumber) {
            try {
                System.out.println("Please enter the new name");
                Guests[GuestNum][1] = input.nextLine();  
                Integer.parseInt(Guests[GuestNum][1]);
                System.out.println("Please enter a valid name\n");
                } catch (Exception e) {
                    isNumber = false;
                }
        }
        System.out.println("Please enter the new name");
        Guests[GuestNum][0] = input.nextLine();
        String CorrectName = "no";
        while (!CorrectName.equals("yes")){
            System.out.println("The new name is "+Guests[GuestNum][0]+" , Is that correct? (yes/no)");
            CorrectName = input.nextLine();
        }
        return Guests;
    }
    static String[][] ChangeGuestAge(String[][] Guests){
        int GuestNum = VaildGuestNum(Guests);
        if (GuestNum == -1){
            return Guests;
        }
        boolean isNumber = false;
        while (!isNumber) {
            try {
                System.out.print("Please enter the new age: ");
                Guests[GuestNum][1] = input.nextLine();  
                Integer.parseInt(Guests[GuestNum][1]);
                isNumber = true;
            } catch (Exception e) {
                System.out.println("Please enter a valid age\n");
            }

        }
        String CorrectName = "no";
        while (!CorrectName.equals("yes")){
            System.out.print("The new age is "+Guests[GuestNum][1]+" , Is that correct? (yes/no): ");
            CorrectName = input.nextLine();
        }
        return Guests;
    }
    static String[][] ChangePlace(String[][] Guests){
        int GuestNum1 = VaildGuestNumC(Guests);
        int GuestNum2 = VaildGuestNumC(Guests);
        if (GuestNum1 == -1 || GuestNum2 == -1){
            return Guests;
        }
        String[] GuestNum2Holder = Guests[GuestNum2];
        Guests[GuestNum2] = Guests[GuestNum1];
        Guests[GuestNum1] = GuestNum2Holder;
        return Guests;
    }
    public static void main(String[] args) throws Exception {
    boolean active = true;
    String[][] Guests = {{"john","1"},{"Bwar","30"}, {"jack","19"},{} };
    while (active){
        System.out.println("Commands: list, stats, add, remove, change-name, change-age,change-place,stop");
        System.out.print("input please: ");
        String x = input.nextLine();
        if(x.equals("list")){
            Listprint(Guests);
        }
        if(x.equals("stats")){
            Stats(Guests);
        }
        if(x.equals("add")){
            int check = CheckForAdd(Guests);
            if(check == -1){
                System.out.println("No more room in guest list");
            }else{
                Guests = AddGuest(Guests,CheckForAdd(Guests));
            }
        }
        if(x.equals("remove")){
            if(CheckForRemove(Guests)){
                Guests = RemoveGuest(Guests);
            }else{
                System.out.println("No guests exist");
            }
        }
        if(x.equals("change-name")){
            Listprint(Guests);
            Guests = ChangeGuestName(Guests);
        }
        if(x.equals("change-age")){
            Listprint(Guests);
            Guests = ChangeGuestAge(Guests);
        }
        if(x.equals("change-place")){
            Listprint(Guests);
            Guests = ChangePlace(Guests);
        }
        if(x.equals("stop")){
            active = false;
        }
    }
}
}

