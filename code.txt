package sample;

import javafx.fxml.FXML;
import javafx.scene.control.Label;
import javafx.scene.control.ListView;
import javafx.scene.control.TextField;

import java.util.ArrayList;


public class Controller {
    //all labels, text fields, and listviews declared.
    @FXML
    Label lbl1A, lbl1B, lbl2A, lbl2B, lbl3A, lbl3B, lbl4, lbl5A, lbl5B, lbl5C, lbl6, lbl9;
    @FXML
    TextField txtInput1, txtInput3A, txtInput3B, txtInput4A, txtInput4B, txtInput6, txtInput7, txtInput8, txtInput9;
    @FXML
    ListView<String> lstView4, lstView7, lstView8;
    //"total" string used throughout my program.
    String total = "";
    @FXML
    //first method.
    private void handleClick1(){
        //variables consisting of an integer array 25 integers long, the integer "numOfFinds" for the number of times it finds the wanted number, and the integer "num", which is the number the user inputs and wants to find.
        int[] array = new int [25];
        int numOfFinds = 0;
        int num = Integer.parseInt(txtInput1.getText());
        //this basically runs the array through the randomArray function. in this function, you type in the array, the maximum and the minimum, and how many numbers you want it to generate as parameters, and it will generate random numbers for that many number of positions in the array.
        array = randomArray(array, 25, 25, -25);
        //sets the first label to the original array, using the printArray function.
        lbl1A.setText(printIntArray(array, "Array: "));
        //loop that runs 25 times, for each of the numbers in the array.
        for (int i=0; i<25; i++){
            //if the number in the array is equal to the number wanted to be found, it will add 1 to numOfFinds, and add that position to the total variable.
            if (array[i] == num){
                numOfFinds++;
                total += i+1 + ", ";
            }
        }
        //if the number was found 0 times, it will print that no instances of the number were found.
        if (numOfFinds == 0){
            lbl1B.setText("No instances of " + num + " were found.");
        //if the number was found once, it will print that 1 instance of the number was found as well as the positions of the number (the substringCalc method basically just takes the substring of a string to prevent there being extra unwanted characters at the end, such as a comma).
        } else if (numOfFinds == 1){
            lbl1B.setText("There was 1 instance of " + num + ", at position " + substringCalc(total, 2));
        //if the number was found multiple times, it will print those instances that the number was found at as well as the positions of the numbers.
        } else {
            lbl1B.setText("There were " + numOfFinds + " instances of " + num + ", at positions " + substringCalc(total, 2));
        }
        //function resetTotal to reset the "total" string for other uses of it in the program.
        resetTotal();
    }
    @FXML
    //second method.
    private void handleClick2(){
        //variables consisting of an integer array 25 integers long, the maximum and minimum integers, and the average double.
        int[] array = new int [25];
        //the maximum and minimum variables are set to the opposites at the start, because you need to start at the lowest/highest, and work your way to find the maximum and minimum.
        int max = -25;
        int min = 25;
        double average = 0;
        //this runs the array through the random number array again, filling the array with random numbers.
        array = randomArray(array, 25, 25, -25);
        //prints the first array in the first label.
        lbl2A.setText(printIntArray(array, "Array: "));
        //runs a loop 25 times, and sees if the number is either greater than the max or less than the minimum, to eventually find the maximum and minimum numbers.
        for (int i=0; i<25; i++){
            //sets max to the number in the array if that number is greater than the current max.
            if (array[i] > max){
                max = array[i];
            }
            //sets min to the number in the array if that number is less than the current min.
            if (array[i]<min){
                min = array[i];
            }
            //adds number to average every time.
            average+=array[i];
        }
        //divides the average by 25, for the 25 numbers in the array.
        average /= 25;
        //sets the second label to the maximum, minimum, and average numbers.
        lbl2B.setText("Maximum number: " + max + ", Minimum number: " + min + ", Average: " + average);
        //resets the total string.
        resetTotal();
    }
    //sorry, for this problem, I did it the harder way accidentally. I think you were supposed to code it so that you can add one item, but I coded it so that you can add as many items as you want, which is why it looks much more complex. You said it was okay if i turned it in, so here it is.
    //global variables for the problem 3 arrays, and a counter for the length of the array (global because it is used in multiple functions).
    int[] problem3Array = new int [500];
    String[]problem3Array2 = new String[500];
    int prob3Counter = 20;
    @FXML
    //third method (next 3 functions).
    //this function generates the array that needs to be used.
    private void handleClick3A(){
        //20 random numbers are placed into the first 20 positions of the array. the arrays have a length of 500, because multiple numbers need to be able to be added.
        problem3Array = randomArray(problem3Array, 20, 25, -25);
        //puts the same numbers from the integer array into the string array.
        for (int i=0; i<20; i++){
            problem3Array2[i] = Integer.toString(problem3Array[i]);
        }
        //sets the rest of the positions in the string array to "", so that null is not displayed when the entire array is printed.
        for (int i=25; i<problem3Array.length; i++){
            problem3Array2[i] = "";
        }
        //sets the first label to print the string array.
        lbl3A.setText(printStringArray(problem3Array2, 20, "Original Array: "));
        //resets the total string.
        resetTotal();
    }
    @FXML
    //this function adds a number at any given position.
    private void handleClick3B(){
        //adds 1 to the counter everytime, which is used later on.
        prob3Counter++;
        //variables to get the text inputs for the position and the number wanted to be entered.
        int pos = Integer.parseInt(txtInput3A.getText());
        int num = Integer.parseInt(txtInput3B.getText());
        //sets the position to the number inputted.
        problem3Array2[pos] = Integer.toString(num);
        //loop that sets the string array to the values in the integer array, after adding the number.
        for (int i=pos+1;i<prob3Counter;i++){
            problem3Array2[i] = Integer.toString(problem3Array[i-1]);
        }
        //displays the string array for only the length of counter, so that nothing else is shown.
        lbl3B.setText(printStringArray(problem3Array2, prob3Counter, "Modified Array: "));
        //this just sets the integer array to the values of the string array, so that they are matching at the end.
        for (int i=0; i<prob3Counter; i++){
            problem3Array[i] = Integer.parseInt(problem3Array2[i]);
        }
        //resets the total string.
        resetTotal();
    }
    @FXML
    //this function replaces the number at any given position.
    private void handleClick3C(){
        //variables to get the text inputs for the position and the number wanted to be entered.
        int pos = Integer.parseInt(txtInput3A.getText());
        int num = Integer.parseInt(txtInput3B.getText());
        //replaces the number in the position with the new number.
        problem3Array2[pos] = Integer.toString(num);
        //prints the new string array.
        lbl3B.setText(printStringArray(problem3Array2, 20, "Modified Array: "));
        //resets the total string.
        resetTotal();
    }
    @FXML
    //fourth method.
    private void handleClick4(){
        //integers to get the number of dice, the amount of rolls the user wants, and the roll variable, for the results.
        int dice = Integer.parseInt(txtInput4A.getText());
        int times = Integer.parseInt(txtInput4B.getText());
        int roll = 0;
        //arraylist for the sums.
        ArrayList<Integer> arr = new ArrayList<>();
        //clears the listview everytime, to prevent repetition.
        lstView4.getItems().clear();
        //loop that runs for the amount of times the user wanted the dice to be rolled.
        for (int i=0; i<times; i++){
            //secondary loop that runs for the amount of dice there are, to get the sum of those.
            for (int j=0; j<dice; j++){
                roll += (int)((Math.random()*(6)) + 1);
            }
            //adds the sum to the array list.
            arr.add(roll);
            //resets roll.
            roll = 0;
        }
        //prints the roll sums which are in the array list.
        lbl4.setText(printArrayList(arr, "Roll Sums: "));
        //loop that runs for each possible sum result of the dice rolled.
        for (int i=dice; i<=dice*6; i++){
            //another loop that runs to find the amount of times the number was in the sums array.
            for (int j=0; j<times; j++) {
                //if the number is in the array, 1 is added to roll.
                if (arr.get(j) == i){
                    roll+=1;
                }
            }
            //if roll is 1, then it will print that there is 1 instance of i, the possible sum.
            if (roll == 1) {
                lstView4.getItems().add("There was 1 instance of " + i);
            } else {
            //if roll is more than 1, then it will print that there is roll instances of i, the possible sum.
                lstView4.getItems().add("There were " + roll + " instances of " + i);
            }
            //resets roll.
            roll = 0;
        }
    }
    //global array list and array, since multiple functions are used for this.
    ArrayList<Integer> p5ArrList = new ArrayList<>();
    int[] p5Arr = new int [20];
    @FXML
    //fifth method (next 3 functions).
    //this function creates the array.
    private void handleClick5A(){
        //clears the array list in case there are any integers in it.
        p5ArrList.clear();
        //adds 20 random numbers to the array list.
        for (int i=0; i<20; i++){
            p5ArrList.add((int)(Math.random() * (41)) - 20);
        }
        //prints the array list.
        lbl5A.setText(printArrayList(p5ArrList, "Original Array: "));
    }
    @FXML
    //this function shuffles the array the first way.
    private void handleClick5B(){
        //a temp array list is created, and the original array list is copied into it.
        ArrayList<Integer> temp = new ArrayList<>(p5ArrList);
        //runs a shuffle function, which essentially takes numbers in random positions in the temp array, and puts those in the original array, resulting in a shuffled original array.
        p5Shuffle(temp);
        //prints the shuffled array.
        lbl5B.setText(printIntArray(p5Arr, "Shuffled Array #1: "));
    }
    @FXML
    //this function shuffles the array the second way.
    private void handleClick5C(){
        //a temp array list is created.
        ArrayList<Integer> temp = new ArrayList<>();
        //counter is created as a reasonable random number.
        int counter = (int)(Math.random()*(18)) + 1;
        //loop that runs 20 times, and it adds the values in the original array to temp from the point counter was at (for example, if the array is [0,1,2,3,4], and counter is 2, temp will then be [2,3,4,0,1]. this just provides an extra layer of shuffling).
        for (int i=0; i<20; i++){
            //adds the position corresponding to counter to the temp array list.
            temp.add(p5ArrList.get(counter));
            //if counter is 19, which is the max length of the array, it resets it to -1 (counter++ appears later in the loop, so counter will be reset to 0 then).
            if (counter == 19){
                counter = -1;
            }
            //adds 1 to counter.
            counter++;
        }
        //now, the shuffle function is ran again, but we shuffled the array a little more earlier in the function, so the two shuffled arrays will be different.
        p5Shuffle(temp);
        //prints the shuffled array.
        lbl5C.setText(printIntArray(p5Arr, "Shuffled Array #2: "));
    }
    @FXML
    //sixth method.
    private void handleClick6(){
        //character arrays, integers for the counter, and the num for the number of positions the user wants to translate the alphabet.
        char[] arr = new char[26];
        char[] arr2 = new char[26];
        int counter = 0;
        int num = Integer.parseInt(txtInput6.getText());
        //loop that creates the alphabet array, adding characters a through z to it.
        for (char i='a';i<='z';i++){
            arr[counter] = i;
            counter++;
        }
        //loop that adds the num position in the first array to the second array, as num constantly increases, resulting in a translated array.
        for (int i=0; i<26; i++){
            arr2[i] = arr[num];
            //if num is 25, or the max position in the array, it resets it to -1 (num++ appears later in the loop, so num will be reset to 0 then).
            if (num == 25){
                num = -1;
            }
            //adds 1 to num.
            num++;
        }
        //adds the characters in the array to the total variable.
        for (int i=0; i<26; i++){
            total+=arr2[i] + ", ";
        }
        //prints the translated alphabet
        lbl6.setText("The translated alphabet is [" + substringCalc(total, 2) + "]");
        //resets the total string.
        resetTotal();
    }
    @FXML
    //seventh method.
    private void handleClick7(){
        //integers for the runs variable, which is the amount of rows the user wants to print, and the row variable, corresponding to which row is being printed at the current time.
        int runs = Integer.parseInt(txtInput7.getText());
        int row = 3;
        //first array list.
        ArrayList<Integer> arr1 = new ArrayList<>();
        //1 is added to it, as it is the first row.
        arr1.add(1);
        //second array list.
        ArrayList<Integer> arr2 = new ArrayList<>();
        //1 and 1 are added to it, as it is the second row.
        arr2.add(1);arr2.add(1);
        //the first 2 rows are printed because you cannot really incorporate those rows into the loop, as they are too small to do the addition and make rows.
        //clears the listview, in case it had values in it.
        lstView7.getItems().clear();
        //prints the first row using the arrayListSimplifier method, which basically makes it easier to print just the spaced out numbers in the array.
        if (runs>0) {
            lstView7.getItems().add(arrayListSimplifier(arr1));
        }
        //prints the first row using the arrayListSimplifier method.
        if (runs>1) {
            lstView7.getItems().add(arrayListSimplifier(arr2));
        }
        //loop that runs runs-2 times, for the amount of rows, since we want to print 2 less rows than the user input because we have already added the first 2 rows.
        for (int i = 0; i < runs-2; i++) {
            //clears arr1.
            arr1.clear();
            //copies arr2 values into arr1.
            arr1.addAll(arr2);
            //clears arr2, which will now be the new row.
            arr2.clear();
            //adds 1 to arr2, since every row starts with a 1.
            arr2.add(1);
            //runs a loop for the row-2 times, since we need that many positions to be calculated (row 3 is 1,2,1, but we only need to find 2, so 3-2 = 1 number to find).
            for (int j = 0; j<row-2; j++){
                //adds the last 2 numbers that were "above" that position in the triangle.
                arr2.add(arr1.get(j) + arr1.get(j+1));
            }
            //adds 1 to arr2, since every row ends with a 1 as well.
            arr2.add(1);
            //sets the listview to the spaced out arr2 using the arrayListSimplifier method.
            lstView7.getItems().add(arrayListSimplifier(arr2));
            //adds 1 to row.
            row++;
        }
    }
    //eighth method
    //global string array used for method 8, since there are multiple functions needed.
    String[] num8Arr = new String[10];
    @FXML
    //this function just sets all the values in the array to random fruits, which are what I used.
    private void handleClick8A(){
        //10 positions set to 10 fruits.
        num8Arr[0] = "apple";
        num8Arr[1] = "banana";
        num8Arr[2] = "cherry";
        num8Arr[3] = "grape";
        num8Arr[4] = "mango";
        num8Arr[5] = "orange";
        num8Arr[6] = "pear";
        num8Arr[7] = "pineapple";
        num8Arr[8] = "strawberry";
        num8Arr[9] = "watermelon";
        //clears listview, in case anything was there previously.
        lstView8.getItems().clear();
        //loop that moves all the items from the array into the listview.
        for (int i=0; i<num8Arr.length; i++){
            lstView8.getItems().add(num8Arr[i]);
        }
    }
    @FXML
    //this function is ran when a new letter is typed or removed, and finds all the fruits that have those letter(s) in them.
    private void handleClick8B(){
        //variables consisting of the input string, which is the input from the user, and the inputLength, which is the length of the user input.
        String input = txtInput8.getText();
        int inputLength = input.length();
        //clears the listview, so that old values are not displayed.
        lstView8.getItems().clear();
        //loop that runs for the amount of words there are in the array, so it can check each word for possible matches.
        for (int i=0; i<num8Arr.length; i++){
            //second loop that searches through each word, or the "i" position in the array, a certain amount of times based on the input length.
            for (int j=0; j<num8Arr[i].length()-inputLength+1; j++){
                //if the user input is equal to any of the substrings in the word equal to the length of the user input, it will add the word to the listview, since it is a match.
                if (input.equals(num8Arr[i].substring(j, j+inputLength))){
                    //adds word to listview.
                    lstView8.getItems().add(num8Arr[i]);
                    //sets j to the length of the word, and that is out of bounds of the loop conditional, so the loop will essentially stop, to prevent words from duplicating into the listview.
                    j = num8Arr[i].length();
                }
            }
        }
    }
    @FXML
    //ninth method.
    private void handleClick9(){
        //integers for the amount of lockers there are, inputted by the user, a counter, and a boolean array to represent the lockers, false meaning it is closed, and true meaning it is open.
        int lockernum = Integer.parseInt(txtInput9.getText());
        int counter = 1;
        boolean[] lockers = new boolean[lockernum];
        //loop that runs for the amount of times there are lockers.
        for (int i = 0; i<lockernum; i++){
            //loop that runs from 1 to the locker numbers+1, since counter needs to be added everytime, and cannot start with 0, and j is added to counter everytime to correspond to the multiples of each number (when counter is 2, j will be 2, 4, 6, etc. and not 2,3,4, etc.).
            for (int j = counter; j<lockernum+1; j+=counter) {
                //these if statements are basically seeing if the position is true or false, and changing the state of that position.
                if (lockers[j-1]) {
                    lockers[j-1] = false;
                } else {
                    lockers[j-1] = true;
                }
            }
            //adds 1 to counter.
            counter++;
        }
        //loop that runs for the amount of times there are lockers.
        for (int i = 0; i<lockernum; i++){
            //if the locker at the "i" position is open, or true as a boolean, it will add that locker number to the total string.
            if (lockers[i]){
                total+=i+1 + ", ";
            }
        }
        //prints all the lockers that are open.
        lbl9.setText("The open lockers are lockers " + substringCalc(total, 2));
        //resets the string total.
        resetTotal();
    }
    //accessor that simplifies an array list, by returning a string with the array list as spaced out values.
    public String arrayListSimplifier(ArrayList a){
        //an empty string is made.
        String b = "";
        //loop that runs for the length of the array list.
        for (int i=0; i<a.size(); i++){
            //adds the value in the array list to the string with an empty space.
            b+= a.get(i) + " ";
        }
        //returns the simplified array list as a string.
        return b;
    }
    //accessor that shuffles the array list, specifically meant for problem 5.
    public void p5Shuffle(ArrayList temp){
        //loop that runs from 19 to 0, so that the random number range decreases overtime.
        for (int i = 19; i>=0; i--){
            //random number integer set to any number between 0 and i+1.
            int random = (int)(Math.random()*(i+1));
            //sets the problem 5 array to the value of the number in the random position selected in the temp array list.
            p5Arr[i] = (int)temp.get(random);
            //removes the same position from the temp array, so the same number is not moved twice.
            temp.remove(random);
        }
    }
    //accessor that resets the total string.
    public void resetTotal(){
        //makes total string empty.
        total = "";
    }
    //accessor that prints integer arrays.
    public String printIntArray(int[] a, String prefix){
        //array total string is made.
        String arrayTotal = "";
        //loop that runs for the length of the array.
        for (int i=0; i<a.length; i++){
            //adds the value in the specific position of the array along with a comma and space to the arrayTotal string.
            arrayTotal+=a[i] + ", ";
        }
        //runs array total through substringCalc, to remove the extra comma and space at the end of it.
        arrayTotal = substringCalc(arrayTotal, 2);
        //returns the array with the prefix, which is a parameter you can add to print before the array.
        return prefix + "[" + arrayTotal + "]";
    }
    //accessor that prints string arrays.
    public String printStringArray(String[] a, int length, String prefix){
        //array total 2 string is made.
        String arrayTotal2 = "";
        //loop that runs for the length inputted.
        for (int i=0; i<length; i++){
            //adds the value in the specific position of the array along with a comma and space to the arrayTotal2 string.
            arrayTotal2+=a[i] + ", ";
        }
        //runs array total 2 through substringCalc, to remove the extra comma and space at the end of it.
        arrayTotal2 = substringCalc(arrayTotal2, 2);
        //returns the array with the prefix, which is a parameter you can add to print before the array.
        return prefix + "[" + arrayTotal2 + "]";
    }
    //accessor that prints an array list
    public String printArrayList(ArrayList a, String prefix){
        //returns the array list with the prefix added to it.
        return prefix + a;
    }
    //accessor that randomizes an integer array.
    public int[] randomArray(int[]a, int loopRunTimes, int max, int min){
        //runs the amount of times given in one of the parameters.
        for (int i=0; i<loopRunTimes; i++){
            //sets the value in the position in the array to a random number between the minimum and maximum parameters given.
            a[i] = (int)(Math.random()*(max-min+1)) + min;
        }
        //returns the randomized array, a.
        return a;
    }
    //accessor that calculates the substring of a string.
    public String substringCalc(String total, int num){
        //sets total to the substring of total from 0, and the number of values needed to be removed from the end, or num.
        total = total.substring(0,total.length()-num);
        //returns the total string.
        return total;
    }
}