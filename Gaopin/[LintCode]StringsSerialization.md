```
Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Please implement encode and decode

Example
Given strs = ["lint","code","love","you"]
string encoded_string = encode(strs)

return `["lint","code","love","you"]｀ when you call decode(encoded_string)
```
```
Solution 1. Application of escape sequence 

A straightforward idea is to add ";" between two strings as the divide symbol. But the problem here is, 

what about if the input strings contain ";" already? How do we distinguish between the divide symbol ";"

and the ";" that are part of the input strings? 

 

Consider how escape sequence works. \ represents the start of an escape sequence, like \n is a newline 

character. Since \ is already reserved as the start of any escape sequence, \\ is used to represent the 

backslash literal. We can simply borrow this idea and use it in this problem.

 

Let's define : as the start of escape sequence, so :; is our divide symbol now. 

Encode:  Replace all : with :: in each string, so :: represents the original : literal;

　　　　   Connect each string with divide symbol :;

Decode: Scan from left to right until a : is met.

 　　　　 If the next character is ;, it means we have a :; divide symbol; 

　　　　  If not, since we've already replaced all : with :: in encoding, so

　　　　  we know that we just saw a : literal.
```
- Solution 1
```java
import java.io.*;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * Created by anliu on 10/22/16.
 */
public class SerializeListOfStrings {

    public static void main(String[] args) {
        List<String> writeList = new ArrayList<String>();
        writeList.add("This");
        writeList.add("");
        writeList.add("is");
        writeList.add("a");
        writeList.add("book!");
        serialize(writeList);

        List<String> readList = deserialize();

        Assert.assertTrue("Serialize/Deserialize", writeList.toString(), readList.toString());
/**
Serialize/Deserialize
   Output: [This, , is, a, book!]
 Expected: [This, , is, a, book!]
   Result: true
*/
    }

    public static void serialize(List<String> list) {
        if(list == null || list.size() == 0) return;;

        StringBuilder sb = new StringBuilder();
        for( int i=0; i< list.size() -1 ; i++) {
            sb.append(list.get(i)).append(" ");
        }
        sb.append(list.get(list.size() - 1));

        try {
            FileOutputStream fileOut = new FileOutputStream("./test.txt");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(sb.toString());
            out.close();
            fileOut.close();
            System.out.printf("Serialized data is saved in ./test.txt file");
        } catch (IOException i) {
            i.printStackTrace();
        }
    }

    public static List<String> deserialize() {
        String str = null;
        try {
            FileInputStream fileIn = new FileInputStream("./test.txt");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            str = (String) in.readObject();
            in.close();
            fileIn.close();
        } catch (IOException i) {
            i.printStackTrace();
        } catch (ClassNotFoundException c) {
            System.out.println("String class not found");
            c.printStackTrace();
        }

        List<String> list = new ArrayList<String>();

        if( str == null) {
            return list;
        }

        list = Arrays.asList( str.split(" "));
        return list;
    }
}
```
- Solution 2
```java
public class Solution {
    public String encode(List<String> strs) {
        if(strs == null){
            return null;
        }
        if(strs.size() == 0){
            return ":;";
        }
        StringBuffer sb = new StringBuffer();
        for(String s : strs){
            String newStr = s.replaceAll(":", "::");
            sb.append(newStr);
            sb.append(":;");
        }
        return sb.toString();
    }
    public List<String> decode(String str) {
        if(str == null){
            return null;
        }
        List<String> strs = new ArrayList<String>();
        int idx = 0;
        StringBuffer sb = new StringBuffer();        
        while(idx < str.length()){
            if(str.charAt(idx) != ':'){
                sb.append(str.charAt(idx));
                idx++;
            }
            else if(str.charAt(idx + 1) == ';'){
                strs.add(sb.toString());
                idx += 2;
                sb = new StringBuffer();
            }
            else{
                sb.append(":");
                idx += 2;
            }
        }
        return strs;
    }
}
```
