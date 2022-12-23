# class-23-12
### Task 5 kyu
Complete the function scramble(str1, str2) that returns true if a portion of str1 characters can be rearranged to match str2, otherwise returns false.
Notes:
Only lower case letters will be used (a-z). No punctuation or digits will be included.
Performance needs to be considered.
Examples
scramble('rkqodlw', 'world') ==> True
scramble('cedewaraaossoqqyt', 'codewars') ==> True
scramble('katas', 'steak') ==> False

### My solution
```Java
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
```
### Fav solution
```Java
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
```
### Task 5kyu
At a job interview, you are challenged to write an algorithm to check if a given string, s, can be formed from two other strings, part1 and part2.
The restriction is that the characters in part1 and part2 should be in the same order as in s.
The interviewer gives you the following example and tells you to figure out the rest from the given test cases.

### My solution
```Java
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
```
### Fav solution
```Java
public class StringMerger {
  public static boolean isMerge(String s, String part1, String part2) {
    if(s.length() != part1.length() + part2.length()) return false;
    if(s.length() == 0) return true;
    return (part1.length() > 0 && part1.charAt(0) == s.charAt(0) && isMerge(s.substring(1), part1.substring(1), part2)) ||
            (part2.length() > 0 && part2.charAt(0) == s.charAt(0) && isMerge(s.substring(1), part1, part2.substring(1)));
  }
}
```
### Task 5 kyu
If you reverse the word "emirp" you will have the word "prime". That idea is related with the purpose of this kata: we should select all the primes that when reversed are a different prime (so palindromic primes should be discarded).
For example: 13, 17 are prime numbers and the reversed respectively are 31, 71 which are also primes, so 13 and 17 are "emirps". But primes 757, 787, 797 are palindromic primes, meaning that the reversed number is the same as the original, so they are not considered as "emirps" and should be discarded.
The emirps sequence is registered in OEIS as A006567
Your task
Create a function that receives one argument n, as an upper limit, and the return the following array:
[number_of_emirps_below_n, largest_emirp_below_n, sum_of_emirps_below_n]

### My solution
```Java
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
```Java

### Fav solution 
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
```

### Task 5 kyu
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

### My solution
```Java
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
``` 
Fav solution
```Java
public class Greed {

  public static int greedy(int[] dice) {
    int n[] = new int[7];
    for (int d : dice) n[d]++;
    return n[1]/3*1000 + n[1]%3*100 + n[2]/3*200 + n[3]/3*300 + n[4]/3*400 + n[5]/3*500 + n[5]%3*50 + n[6]/3*600;
  }
  
}
```
Its incredible short and logical 

### Task 4 kyu
https://www.codewars.com/kata/5d7bb3eda58b36000fcc0bbb/java

### My solution 
```Java
import java.math.BigInteger;

public class GeneralizedFibonacci {
  public static BigInteger[][] Multiply(BigInteger[][] a, BigInteger[][] b, byte n){
    BigInteger[][] c = new BigInteger[n][n];
    for (int i=0;i<n;i++){
      for (int j=0;j<n;j++){
        c[i][j] = BigInteger.ZERO;
        for (int k=0;k<n;k++){
          c[i][j] = c[i][j].add(a[i][k].multiply(b[k][j]));
        }
      }
    }
    return c;
  }

  public static BigInteger Get (byte[] a, byte[] b, long power)
  {
    byte l = (byte) a.length;
    BigInteger z = BigInteger.ZERO;
    BigInteger o = BigInteger.ONE;
    BigInteger[][] curr = new BigInteger[l][l];
    BigInteger[][] mult = new BigInteger[l][l];
    BigInteger result = BigInteger.ZERO;
    
    for (int i=0;i<l;i++){
      for (int j=0;j<l;j++){
        curr[i][j] = z;
        mult[i][j] = z;
      }
    }
    
    curr[0][0] = o;
    mult[l-1][l-1] = BigInteger.valueOf(b[0]);
    for (int i=0;i<l-1;i++){
      curr[i+1][i+1] = o;
      mult[i][i+1] = o;
      mult[l-1][i] = BigInteger.valueOf(b[l-1-i]);
    }
    
    long t = power - l + 1;
    
    while (t > 0){
      if ((t % 2) == 1){
        curr = Multiply(curr, mult, l);
      }
      t = t >> 1;
      mult = Multiply(mult, mult, l);
    }
    
    for (int u=0;u<l;u++){
      result = result.add( BigInteger.valueOf(a[u]).multiply(curr[l-1][u]) );
    }
    
    return result;
  }
}
```
### Fav solution
```Java
import java.math.BigInteger;
import java.util.Arrays;

public class GeneralizedFibonacci {
    private static BigInteger[][] squareMatrix(final BigInteger[][] mat) {
        final BigInteger[][] ret = new BigInteger[mat.length][mat.length];
        for (int i = 0; i < mat.length; i++) {
            for (int k = 0; k < mat.length; k++) {
                ret[i][k] = BigInteger.ZERO;
                for (int j = 0; j < mat.length; j++) {
                    ret[i][k] = mat[i][j].multiply(mat[j][k]).add(ret[i][k]);
                }
            }
        }
        return ret;
    }

    private static BigInteger[] vectorMul(final BigInteger[][] mat, final BigInteger[] vector) {
        final BigInteger[] ret = new BigInteger[mat.length];
        for (int i = 0; i < mat.length; i++) {
            ret[i] = BigInteger.ZERO;
            for (int j = 0; j < vector.length; j++) {
                ret[i] = mat[i][j].multiply(vector[j]).add(ret[i]);
            }
        }
        return ret;
    }

    public static BigInteger Get(final byte[] a, final byte[] b, long power) {
        BigInteger[][] baseMatrix = new BigInteger[b.length][b.length];
        for(BigInteger[] row:baseMatrix) Arrays.fill(row, BigInteger.ZERO);
        for (int i = 0; i < b.length; i++) {
            baseMatrix[b.length-1][i] = BigInteger.valueOf(b[b.length-1-i]);
        }
        for(int i=1; i<b.length;i++) {
            baseMatrix[i-1][i] = BigInteger.ONE;
        }
        BigInteger[] baseVector = new BigInteger[a.length];
        Arrays.setAll(baseVector, i -> BigInteger.valueOf(a[i]));
        while(power > 0) {
            if((power & 1) == 1) {
                baseVector = vectorMul(baseMatrix, baseVector);
                if(power == 1) break;
            }
            baseMatrix = squareMatrix(baseMatrix);
            power >>= 1;
        }
        return baseVector[0];
    }
}
```

### Task 4 kyu 
https://www.codewars.com/kata/5286a298f8fc1b7667000c1c/javascript
### My sol:
```Java
function DocumentParser(Reader)
{
  this.reader = Reader;
  this.reset();
}

DocumentParser.prototype.reset = function()
{
  this.wordCount = 0;
  this.charCount = 0;
  this.lineCount = 0;
};

DocumentParser.prototype.parse = function()
{
  var text = '';
  
  do {
    frag = this.reader.getChunk();
    text += frag;
    
    if( text.indexOf( '\n' ) != -1 || frag == '' ) {
      var parts = text.split( '\n' );

      text = (parts.length > 1) ? parts.splice( -1, 1 ) : '';
        
      var self = this;
      
      parts.forEach( function( p ) {
        self.charCount += p.length
        self.lineCount += self.charCount ? 1 : 0;
        p = p.trim();
        i = 0;
        while( i < p.length-1 ) {
          if( p.charAt( i ) == ' ' && p.charAt( i+1 ) == ' ' )
            p = p.slice( 0, i ) + p.slice( i+2 );
          else
            ++i;
        }
        
        self.wordCount += (self.charCount && p != '') ? p.split( ' ' ).length : 0;
      });
    }
  }
  while( frag != '' );
};
```

### Fav solution
```Java
function DocumentParser(Reader)
{
  this.reader = Reader;
  this.reset();
}

DocumentParser.prototype.reset = function()
{
  this.wordCount = 0;
  this.charCount = 0;
  this.lineCount = 0;
};

DocumentParser.prototype.parse = function()
{
  this.reset();
  var prevChar = ' ';
  var chunk = this.reader.getChunk();

  while (chunk !== '') {

    for (var i = 0; i < chunk.length; i++) {
      if (chunk[i] === '\n') {
        this.lineCount++;
        prevChar = ' ';
      } else {
        this.charCount++;
        if (this.lineCount === 0) this.lineCount = 1;
        if (chunk[i] !== ' ' && prevChar === ' ') {
          this.wordCount++;
        }
        prevChar = chunk[i];
      }
    }
    chunk = this.reader.getChunk();
  }
};
```

### Task 4 kyu
https://www.codewars.com/kata/55b7bb74a0256d4467000070/java
### My solution
```Java
public class ProperFractions {
  public static long properFractions(long n) {
       double res = n;
    
    if(n == 1){
      return 0;
    }
    
    for(long e=2; e*e<= n; e++) {
      if(n%e == 0) {
        while(n%e == 0){
          n /= e;
        }
        
        res *= (1.0 - (1.0 / (e*1.0) ));
      }
    }
  
    if(n > 1){
      res *= (1.0 - (1.0 / (n*1.0) ));
    }
    
    return (long)res;
  }
}
```
### Fav solution
```Java
public class ProperFractions {
  public static long properFractions(long n) {
    if (n==1) return 0;
    long r=n;
    for(long d=2;d*d<=n;d++)
      if(n%d<1){
        while(n%d<1)
          n/=d;
        r-=r/d;
      }
    if(n>1) r-=r/n;
    return r;
  }
}
```
### Task 5 kyu 
https://www.codewars.com/kata/52685f7382004e774f0001f7/java
### My solution
```Java
public class HumanReadableTime {
  public static String makeReadable(int seconds) {
    int hours = (seconds/60)/60;
    int mins = (seconds/60)%60;
    int secs = (seconds%60)%60;
    StringBuffer time = new StringBuffer( hours +":" + mins+":" + secs);
    if(hours <10)
      time.insert(0,'0');
      if (mins<10)
      time.insert(3,'0');
      if (secs<10)
      time.insert(6,'0');
    return time.toString();
  }
}
```
### Fav solution
```Java
public class HumanReadableTime {
  public static String makeReadable(int seconds) {
    return String.format("%02d:%02d:%02d", seconds / 3600, (seconds / 60) % 60, seconds % 60);
  }
}
```

### Task 5 kyu
https://www.codewars.com/kata/54521e9ec8e60bc4de000d6c
### My solution
```Java
public class Max {
  public static int sequence(int[] arr) {
   int m = 0, a = 0, s = 0;
    for(int f : arr) {
      s += f;
      m = Math.min(s, m);
      a = Math.max(a, s - m);
    }
    return a;
  }
}
```
### Fav solution
```Java
public class Max {
  public static int sequence(int[] arr) {

    int sum = 0;
    int max = 0;

    for(int a : arr) {
      sum += a;
      max = Math.max(max, sum);
      sum = Math.max(sum, 0);
    }

    return max;
  }
}
```
### Task 5 kyu 
https://www.codewars.com/kata/5c230f017f74a2e1c300004f
### My solution
```Java
public class Dinglemouse {

    private final static char wall = '#';
    private final static char POTUS = 'X';
    private final static char elve = 'o';
    private final static char checked = '*';
    private static char[][] white_house;
    private static boolean is_all_alone;

    public static boolean allAlone(char[][] house) {
        white_house = house;
        is_all_alone = true;
        loops:
        for (int h = 0; h < house.length; ++h)
            for (int w = 0; w < house[0].length; ++w)
                if (house[h][w] == 'X') {
                    check(h, w);
                    break loops;
                }
        return is_all_alone;
    }
    private static void check(int h, int w) {
        char current = white_house[h][w];
        if (current == wall || current == checked)
            return;
        if (current == elve) {
            is_all_alone = false;
            return;
        }
        white_house[h][w] = checked;
        check(h - 1, w);
        check(h + 1, w);
        check(h, w - 1);
        check(h, w + 1);
    }
}
```
### Fav solution
```Java
public class Dinglemouse {

  public static boolean allAlone(char[][] house) {
    for(int y = 0; y < house.length; y++)
      for(int x = 0; x < house[0].length; x++)
        if(house[y][x] == 'X')
          if(find(house, x, y))
            return false;
    
    return true;
  }
  
  public static boolean find(char[][] house, int x, int y) {
    if(y < 0 || y >= house.length)
      return false;//Out of bounds
    
    if(x < 0 || x >= house[0].length)
      return false;//Out of bounds
    
    if(house[y][x] == 'o')
      return true;//We found an elf!
    
    if(house[y][x] == '#' || house[y][x] == '-')
      return false;//We don't want to search walls or places we have already seen
    
    house[y][x] = '-';//Change so we won't visit again
    if(find(house, x + 1, y) || find(house, x - 1, y))
      return true;//We found an elf left/right of us
    
    return find(house, x, y + 1) || find(house, x, y - 1);//We found al elf above/below us
  }

}
```
