# GuestList0.1
```
import java.util.*;

public class App {
    public static void main(String[] args)  {
        String[][] Guests = { {"john","1"},{"Bwar","30"},{}, {"jack","19"} };
        String[] Commands = {"list","stats","edit","stop"};
        Scanner input = new Scanner(System.in);  // Create a Scanner object
        boolean Run = true;
        while (Run) {
            //Checking for a vaild command
            System.out.println("Please Enter a Vaild Command: list, stats, edit, stop");
            String command = input.nextLine();  
            boolean IsACommand = Arrays.asList(Commands).contains(command);
            while (IsACommand == false){    
                System.out.println("Please Enter a Valid Command");
                command = input.nextLine(); 
                IsACommand = Arrays.asList(Commands).contains(command);
                }
                if (command.equals("list")){
                    for (int i = 0; i < Guests.length; i++) {
                        if(Guests[i].length == 0){
                            continue;
                        }
                        System.out.println("Guest "+(i+1)+", "+Arrays.deepToString(Guests[i]));
                    }
                }
                if (command.equals("stats")){

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
                System.out.println("Oldest person: "+Arrays.toString(YoungestPerson));
            }
            if (command.equals("edit")){

                boolean ActiveEdit = true;
                while (ActiveEdit) {
                    System.out.println("Please choose to: add, modify, remove, exit");
                    String EditList = input.nextLine();

                    //adding guests
                    if (EditList.equals("add")){

                        boolean ActiveAdd = true;
                        while (ActiveAdd) {
                            boolean PossibleAdd = false;
                            int SavedIndex = 0;
                            for (int i = 0; i < Guests.length; i++) {
                                if(Guests[i].length == 0){
                                    PossibleAdd = true;
                                    SavedIndex = i;
                                    break;
                                }
                            }
                            if (PossibleAdd){
                                System.out.println("Please enter the guests name");
                                String NewGuestName = input.nextLine() ;
                                System.out.println("Please enter the guests age");
                                String NewGuestAge = input.nextLine() ;

                                String[][] copy = new String[Guests.length][2];
                                for (int i = 0, j = 0; i < Guests.length; i++) {
                                    if (i != SavedIndex) {
                                        copy[j++] = Guests[i];
                                    }
                                }
                                copy[copy.length-1][0] = NewGuestName;
                                copy[copy.length-1][1] = NewGuestAge;

                                for (int i = 0, j = 0; i < copy.length; i++) {
                                    if (i != SavedIndex) {
                                        Guests[j++] = copy[i];
                                    }
                                }

                                System.out.println("Would you like to add more guests (yes/no)");
                                String MoreNewGuests = input.nextLine() ;
                                if(MoreNewGuests.equals("no")){
                                    ActiveAdd = false;
                                }
                            } else{
                                System.out.println("Guest List is full");
                                ActiveAdd = false;
                            }
                        }

                    }
                    //modifying Guests
                    if (EditList.equals("modify")){
                        boolean ActiveModify = true;
                        while (ActiveModify) {
                            System.out.println("What guest options do you want to modify: name, age, placement, exit");
                            String ModifyWhat = input.nextLine();

                            if(ModifyWhat.equals("name")){
                                boolean ActiveModifyName = true;
                                while (ActiveModifyName) {
                                    for (int i = 0; i < Guests.length; i++) {
                                        if(Guests[i].length == 0){
                                            continue;
                                        }
                                        System.out.println("Guest "+(i+1)+", "+Arrays.deepToString(Guests[i]));
                                    }
                                    int WhichGuest = -1;
                                    boolean VaildGuestNumber = false;
                                    while (!VaildGuestNumber) {
                                        try {
                                            System.out.println("\nWhich guest name would you like to modify (Use the Guest number)");
                                            WhichGuest = Integer.parseInt(input.nextLine());
                                            if(((WhichGuest >= 0) || (WhichGuest <= Guests.length)) && (Guests[WhichGuest-1].length >  0)){
                                                VaildGuestNumber = true;
                                            }else{
                                                System.out.println("Please Enter a Vaild Number");
                                            }
                                        } catch (Exception e) {
                                            System.out.println("Please Enter a Vaild Number");
                                        }
                                    }
                                            Boolean ModifyGuestSpecificName = true;
                                            while (ModifyGuestSpecificName) {
                                                System.out.println("Please enter the new name");
                                                String NewName = input.nextLine();
                                                Guests[WhichGuest-1][0] = NewName;
                                                System.out.println("The new name is "+NewName+" , Would you like to change the name again? (yes/no)");
                                                String ChangeSameName = input.nextLine();
                                                if (ChangeSameName.equals("no") || ChangeSameName.equals("yes") ) {
                                                    if(ChangeSameName.equals("no")){
                                                        ModifyGuestSpecificName = false;
                                                        break;
                                                    }
                                                } else {
                                                    System.out.println("Please enter yes/no");
                                                }
                                            }
                                            System.out.println("Would you like to change another guest name");
                                            Boolean ChangeNameBoolean = true;
                                            while (ChangeNameBoolean) {
                                                String ChangeName = input.nextLine();
                                                if (ChangeName.equals("no") || ChangeName.equals("yes") ) {
                                                    if(ChangeName.equals("no")){
                                                        ActiveModifyName = false;
                                                        break;
                                                    }
                                                    if(ChangeName.equals("yes")){
                                                        break;
                                                    }
                                                } else {
                                                    System.out.println("Please enter yes/no");
                                                }

                                        }

                                    }
                                }
                                if(ModifyWhat.equals("age")){
                                    boolean ActiveModifyAge = true;
                                    while (ActiveModifyAge) {
                                        for (int i = 0; i < Guests.length; i++) {
                                            if(Guests[i].length == 0){
                                                continue;
                                            }
                                            System.out.println("Guest "+(i+1)+", "+Arrays.deepToString(Guests[i]));
                                        }
                                        int WhichGuest = -1;
                                        boolean VaildGuestNumber = false;
                                        System.out.println("\nWhich guest age would you like to modify (Use the Guest number)");
                                        while (!VaildGuestNumber) {
                                            try {
                                                WhichGuest = Integer.parseInt(input.nextLine());
                                                if(((WhichGuest >= 0) || (WhichGuest <= Guests.length)) && (Guests[WhichGuest-1].length >  0)){
                                                    VaildGuestNumber = true;
                                                }else{
                                                    System.out.println("Please Enter a Valid Guest Number");
                                                }
                                            } catch (Exception e) {
                                                System.out.println("Please Enter a Valid Guest Number");
                                            }
                                        }
                                                Boolean ModifyGuestSpecificAge = true;
                                                while (ModifyGuestSpecificAge) {
                                                    boolean ValidAge = false;
                                                    String NewAge = "";
                                                    System.out.println("Please enter the new age");
                                                    while (!ValidAge){
                                                        try {
                                                        NewAge = input.nextLine();
                                                        int TestValidAge = Integer.parseInt(NewAge);
                                                        if (TestValidAge > 0) {
                                                            ValidAge = true;
                                                            break;
                                                        } else {
                                                            System.out.println("Please Enter a Valid Age");
                                                        }
                                                        } catch (Exception e) {
                                                            System.out.println("Please Enter a Valid Age");
                                                        }
                                                    }
                                                    Guests[WhichGuest-1][0] = NewAge;
                                                    System.out.println("The new age is "+NewAge+" , Would you like to change the age again? (yes/no)");
                                                    String ChangeSameAge = input.nextLine();
                                                    if (ChangeSameAge.equals("no") || ChangeSameAge.equals("yes") ) {
                                                        if(ChangeSameAge.equals("no")){
                                                            ModifyGuestSpecificAge = false;
                                                            break;
                                                        }
                                                    } else {
                                                        System.out.println("Please enter yes/no");
                                                    }
                                                }
                                                System.out.println("Would you like to change another guest age");
                                                Boolean ChangeAgeBoolean = true;
                                                while (ChangeAgeBoolean) {
                                                    String ChangeAge = input.nextLine();
                                                    if (ChangeAge.equals("no") || ChangeAge.equals("yes") ) {
                                                        if(ChangeAge.equals("no")){
                                                            ActiveModifyAge = false;
                                                            break;
                                                        }
                                                        if(ChangeAge.equals("yes")){
                                                            break;
                                                        }
                                                    } else {
                                                        System.out.println("Please enter yes/no");
                                                    }
    
                                            }
    
                                        }
                                    }
                                if(ModifyWhat.equals("placement")){
                                    boolean ActiveModifyPlacement = true;
                                    if (ActiveModifyPlacement) {
                                        for (int i = 0; i < Guests.length; i++) {
                                            System.out.println("Guest "+(i+1)+", "+Arrays.deepToString(Guests[i]));
                                        }
                                        int WhichGuest1 = -1;
                                        int WhichGuest2 = -1;
                                        boolean VaildGuestNumber1 = false;
                                        boolean VaildGuestNumber2 = false;
                                        while (!VaildGuestNumber1 || !VaildGuestNumber2 ) {
                                            try {
                                                System.out.println("\nWhich guest would you like to modify their placement (Use the Guest number)");
                                                WhichGuest1 = Integer.parseInt(input.nextLine());

                                                if((WhichGuest1 >= 0) || (WhichGuest1 <= Guests.length)){
                                                    VaildGuestNumber1 = true;
                                                }else{
                                                    System.out.println("Please Enter a Vaild Number");
                                                }
                                            } catch (Exception e) {
                                                System.out.println("Please Enter a Vaild Number");
                                            }
                                            try {
                                                System.out.println("\n With which Guest/place? (Use the Guest number)");
                                                WhichGuest2 = Integer.parseInt(input.nextLine());
                                                if((WhichGuest2 >= 0) || (WhichGuest2 <= Guests.length)){
                                                    VaildGuestNumber2 = true;
                                                }else{
                                                    System.out.println("Please Enter a Vaild Number");
                                                }
                                            } catch (Exception e) {
                                                System.out.println("Please Enter a Vaild Number");
                                            }
                                        }
                                        String[][] copy = new String[Guests.length][2];
                                for (int i = 0, j = 0; i < Guests.length; i++) {
                                    if (i == WhichGuest1-1 ) {
                                        copy[j++] = Guests[WhichGuest2-1];
                                    }else if(i == WhichGuest2-1){
                                        copy[j++] = Guests[WhichGuest1-1];
                                    }else{
                                        copy[j++] = Guests[i];
                                    }

                                }
                                    }

                            }

                            if(ModifyWhat.equals("exit")){
                                ActiveModify = false;
                        }
                    }
                    

                }

                if(EditList.equals("remove")){
                    boolean ActiveRemove = true;
                    while (ActiveRemove) {
                        boolean PossibleRemove = false;
                    int SavedIndex = 0;
                    for (int i = 0; i < Guests.length; i++) {
                        if(Guests[i].length != 0){
                            PossibleRemove = true;
                            SavedIndex = i;
                            break;
                        }
                    }
                    if (PossibleRemove){
                        for (int i = 0; i < Guests.length; i++) {
                            System.out.println("Guest "+(i+1)+", "+Arrays.deepToString(Guests[i]));
                        }

                        boolean VaildGuestNumber = false;
                        while (!VaildGuestNumber) {
                            try {
                                System.out.println("Please enter which guest to remove (Use the Guest number)");
                                int WhichGuest = Integer.parseInt(input.nextLine()); ;
                                if(((WhichGuest >= 0) || (WhichGuest <= Guests.length)) && (Guests[WhichGuest-1].length >  0)){
                                    VaildGuestNumber = true;
                                }else{
                                    System.out.println("Please Enter a Vaild Number");
                                }
                            } catch (Exception e) {
                                System.out.println("Please Enter a Vaild Number");
                            }
                        }

                        String[][] copy = new String[Guests.length][2];
                        String[][] Empty = {{}};
                        for (int i = 0, j = 0; i < Guests.length; i++) {
                            if (i == SavedIndex) {
                                copy[j++] = Empty[0];
                            }else{copy[j++] = Guests[i];}
                        }
                        for (int i = 0, j = 0; i < copy.length; i++) {
                                Guests[j++] = copy[i];
                        }

                        System.out.println("Would you like to remove more guests (yes/no)");
                        String MoreNewGuests = input.nextLine() ;
                        if(MoreNewGuests.equals("no")){
                            ActiveRemove = false;
                        }
                    } else{
                        System.out.println("Guest List is full");
                        ActiveRemove = false;
                    }
                    }
                    
                }

                if(EditList.equals("exit")){
                    ActiveEdit = false;
                }
            }

        }
        if (command.equals("stop")) {
            Run = false;
        }
    }
}

}
```
