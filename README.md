# Stack-Heap Diagram

This repository shows a simple example of a Stack-Heap diagram creation based on a java program.

## Task
Follow the code below and build a step-by-step Stack-Heap Diagram.<br/>
Doing this exercise, it is okay to omit intermediate states (like the states in expressions evaluation, system methods calls, and so on); however, make sure to note changes when named variables are created or user-defined methods are called.

## Java Program Code

```java
public class Main {
    public static void main(String[] args) {
        String name = "Kevin";
        List<String> list = new ArrayList<>();
        int times = 10;
        System.out.println(times + fill(list, name + name, times));
    }
    public static int fill(Collection<String> collection, String str, int times){
        String shrunk = shrink(str);
        times = (times + shrunk.length()) / 2;
        for (int i = 0; i < times / 2; i++) {
            collection.add(shrunk);
        }
        return times;
    }
 
    public static String shrink(String str){
        int newLength = str.length() / 2 + str.length() % 2;
        char[] chars = new char[newLength];
        for (int i = 0; i < str.length(); i+=2) {
            chars[i / 2] = str.charAt(i);
        }
        return new String(chars);
    }
}
```

## Implementation

### Step 1

The program execution starts from the main(String[] args) method defined in the Main class. So the first stack-frame is put on the Stack. This method has some local variables like 'name', 'times', and 'list'. Let's put them in the corresponding stack frame, meanwhile we create objects in the Heap memory space.

Executing the main() method we have another function call of a 'fill()' method that produces another stack-frame with its local variables. Let's put it right on top of the main() stack-frame following the LIFO queue rules.

fill() method as well has another function call of 'shrink()' method which makes us do the same set of instructions once again. We don't forget to follow the rules of Java Memory Model.

Here is what we've got in the Step 1:  
We completed a full stack-frames sequence, defined local variables on stack and connected reference variables with their objects on the Stack.

![Stack-Heap Diagram Step1](./diagrams/stack-heap%20diagram.png)

### Step 2

As the 'shrink()' method finishes its work we free a corresponding stack-frame on stack and remove some unnecessary references and local variables. Unlinked objects on the Heap will be removed from the Heap memory space at some point of time by Java Garbage Collector which is done automatically. 

Here is what we' got for Step2:  
![Stack-Heap Diagram Step2](./diagrams/stack-heap%20diagram2.png)


### Step 3

When the 'fill()' method is finished we do the same work as in Step 2. The program is almost done and waits for 17 to be printed in the console. After the program termination the Heap will be completely cleared because the objects created by the program are no longer needed.

![Stack-Heap Diagram Step1](./diagrams/stack-heap%20diagram3.png)