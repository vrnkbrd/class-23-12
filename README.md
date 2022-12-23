# class-23-12
### Task 5 kyu
DESCRIPTION:

Complete the function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise returns false.

Notes:

Only lower case letters will be used (a-z). No punctuation or digits will be included.
Performance needs to be considered.
Examples

scramble('rkqodlw', 'world') ==> True
scramble('cedewaraaossoqqyt', 'codewars') ==> True
scramble('katas', 'steak') ==> False

### My solution
public class Scramblies {

    public static boolean scramble(String str1, String str2) {
        int[] arr = new int[26];
        for(int i=0; i<26; i++){
            arr[i] = 0;
        }
        for(int i=0; i < str1.length(); i++) {
            arr[(int)str1.charAt(i) - (int)'a']++;
        }
        for(int i=0; i < str2.length(); i++) {
            arr[(int)str2.charAt(i) - (int)'a']--;
        }
        for(int i=0; i<26; i++){
            if(arr[i] < 0)
                return false;
        }
        return true;
    }
}
### Fav solution
import java.util.HashMap;
import java.util.Map;

public class Scramblies {

    public static boolean scramble(String str1, String str2) {
        Map<Character, Integer> word1 = countLetters(str1);
        Map<Character, Integer> word2 = countLetters(str2);

        for (Character c : word2.keySet()) {
            Integer n = word1.get(c);
            if (n == null || n < word2.get(c)) {
                return false;
            }
        }

        return true;
    }

    private static Map<Character, Integer> countLetters(String s) {
        Map<Character, Integer> map = new HashMap<Character, Integer>();
        for (char c : s.toCharArray()) {
            Integer n = map.get(c);
            if (n == null) {
                map.put(c, 1);
            } else {
                map.put(c, n + 1);
            }
        }
        return map;
    }
}
### Task 5kyu
public class StringMerger {
  public static boolean isMerge(String s, String part1, String part2) {
    if(s.length() != part1.length() + part2.length()) return false;
    if(s.length() == 0) return true;
    return (part1.length() > 0 && part1.charAt(0) == s.charAt(0) && isMerge(s.substring(1), part1.substring(1), part2)) ||
            (part2.length() > 0 && part2.charAt(0) == s.charAt(0) && isMerge(s.substring(1), part1, part2.substring(1)));
  }
}
My solution
public class StringMerger {

    public static boolean isMerge(String s, String part1, String part2) {
        if(part1 == "" && s.equals(part2) || part2 == "" && s.equals(part1))
            return true;
        else if(part1 == ""|| part2 == "" || s == "")
            return false;

        if(part1.charAt(0) == s.charAt(0) && part2.charAt(0) == s.charAt(0)) {
            return isMerge(s.substring(1, s.length()), part1.substring(1, part1.length()), part2)
                    || isMerge(s.substring(1, s.length()), part1, part2.substring(1, part2.length()));
        }
        else if(part1.charAt(0) == s.charAt(0)) {
            return isMerge(s.substring(1, s.length()), part1.substring(1, part1.length()), part2);
        }
        else if(part2.charAt(0) == s.charAt(0)) {
            return isMerge(s.substring(1, s.length()), part1, part2.substring(1, part2.length()));
        }
        return false;
    }

}
Fav solution
public class StringMerger {
  public static boolean isMerge(String s, String part1, String part2) {
    if(s.length() != part1.length() + part2.length()) return false;
    if(s.length() == 0) return true;
    return (part1.length() > 0 && part1.charAt(0) == s.charAt(0) && isMerge(s.substring(1), part1.substring(1), part2)) ||
            (part2.length() > 0 && part2.charAt(0) == s.charAt(0) && isMerge(s.substring(1), part1, part2.substring(1)));
  }
}

Task 5 kyu
If you reverse the word "emirp" you will have the word "prime". That idea is related with the purpose of this kata: we should select all the primes that when reversed are a different prime (so palindromic primes should be discarded).

For example: 13, 17 are prime numbers and the reversed respectively are 31, 71 which are also primes, so 13 and 17 are "emirps". But primes 757, 787, 797 are palindromic primes, meaning that the reversed number is the same as the original, so they are not considered as "emirps" and should be discarded.

The emirps sequence is registered in OEIS as A006567

Your task

Create a function that receives one argument n, as an upper limit, and the return the following array:

[number_of_emirps_below_n, largest_emirp_below_n, sum_of_emirps_below_n]

My solution
mport java.util.Arrays;

class Emirps {
    
    public static long[] findEmirp(long n){
        long l1 = 0 ; long l2= 0 ; long l3= 0 ; 
        for (long i =13 ; i <=n; i ++)  {   
          long x = Long.parseLong(new StringBuilder(""+i).reverse().toString()); 
          if (b(i)==true && b(x)==true && i!=x)
           {
             l1++; l2=i ; l3=l3+i; 
        } 
}
          return new long[]{l1 , l2 ,l3};
    }
  public static boolean b (long n ) {    
     for (long i =2 ; i<=Math.sqrt(n); i++) {  
        if (n%i==0) return false; 
     } 
    return true; 
  }
}



Fav solution 
import java.util.Arrays;

class Emirps {

    public static long[] findEmirp(long n){
        long number_of_emirps_below_n = 0;
        long largest_emirp_below_n = 0;
        long sum_of_emirps_below_n = 0;

        for(long i = 13; i <= n; i ++){
            long reverseNumber = Long.parseLong(new StringBuilder(""+i).reverse().toString());
            if(isPrime(i)==true && isPrime(reverseNumber)==true && i!=reverseNumber){
                number_of_emirps_below_n++;
                largest_emirp_below_n = i;
                sum_of_emirps_below_n += i;
            }

        }
        return new long[]{number_of_emirps_below_n,largest_emirp_below_n,sum_of_emirps_below_n};
        
    }
    
    public static boolean isPrime(long n){
        for(int i = 2 ; i <= Math.sqrt(n); i++){
            if(n%i == 0) return false;
        }
        return true;
    }
}
Task 5 kyu


My solution
