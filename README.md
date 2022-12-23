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
Greed is a dice game played with five six-sided dice. Your mission, should you choose to accept it, is to score a throw according to these rules. You will always be given an array with five six-sided dice values.

 Three 1's => 1000 points
 Three 6's =>  600 points
 Three 5's =>  500 points
 Three 4's =>  400 points
 Three 3's =>  300 points
 Three 2's =>  200 points
 One   1   =>  100 points
 One   5   =>   50 point
A single die can only be counted once in each roll. For example, a given "5" can only count as part of a triplet (contributing to the 500 points) or as a single 50 points, but not both in the same roll.

Example scoring

 Throw       Score
 ---------   ------------------
 5 1 3 4 1   250:  50 (for the 5) + 2 * 100 (for the 1s)
 1 1 1 3 1   1100: 1000 (for three 1s) + 100 (for the other 1)
 2 4 4 5 4   450:  400 (for three 4s) + 50 (for the 5)
In some languages, it is possible to mutate the input to the function. This is something that you should never do. If you mutate the input, you will not be able to pass all the tests.


My solution
public class Greed{
  public static int greedy(int[] dice){
    int c1=0;
    int c2=0;
    int c3=0;
    int c4=0;
    int c5=0;
    int c6=0;
    for(int i=0; i<dice.length; i++){
      switch (dice[i]){
          case 1: c1++;
          break;
          case 2: c2++;
          break;
          case 3: c3++;
          break;
          case 4: c4++;
          break;
          case 5: c5++;
          break;
          case 6: c6++;
          break;
      }
      
    }
   int sum=count(c1, 1000, 100)+count(c2, 200, 0)+count(c3, 300, 0)+count(c4, 400, 0)+count(c5, 500, 50)
           +count(c6, 600, 0);
    
    return sum;
  }
  
  
  public static int count(int counter, int sumthree, int sumone){
  int sum=0;
	    if(counter>=3){
	      counter-=3;
	      sum+=sumthree;
	      }
	    if(sumone!=0){
	    	if(sum==0 && counter!=0 ) {
	    		
	    		sum=1;
	    		sum=counter*sumone;
	    	}else {
	    		
	    		sum+=counter*sumone;
	    	}
	    }
	  return sum;
  }
}

fav 
public class Greed {

  public static int greedy(int[] dice) {
    int n[] = new int[7];
    for (int d : dice) n[d]++;
    return n[1]/3*1000 + n[1]%3*100 + n[2]/3*200 + n[3]/3*300 + n[4]/3*400 + n[5]/3*500 + n[5]%3*50 + n[6]/3*600;
  }
  
}
