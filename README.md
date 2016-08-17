# CheckString1
Q.Given three strings A, B and C.Write a function that checks whether C is an interleaving of A and B. 
 C is said to be interleaving A and B, if it contains all characters of A and B and order of all characters in individual strings is preserved.
 The simple solution doesn’t work if strings A and B have some common characters. For example A = “XXY”, string B = “XXZ” and string C = “XXZXXXY”.
 To handle all cases, two possibilities need to be considered. 

 a) If first character of C matches with first character of A, we move one character ahead in A and C and recursively check. 

 b) If first character of C matches with first character of B, we move one character ahead in B and C and recursively check.

 If any of the above two cases is true, we return true, else false. 
 Following is simple recursive implementation of this approach......



sol.

import java.util.*;
import java.lang.*;
import java.io.*;
 

class Check
{
	private static boolean checkOverlap(String a, String b, String c) {
		Boolean[][][] memoize = new Boolean[a.length()+1][b.length()+1][c.length()+1];
		return checkOverlap(a, b, c, 0, 0, 0, memoize);
	}
	private static boolean checkOverlap(
		String a
	,   String b
	,   String c
	,   int pa
	,   int pb
	,   int pc
	,   Boolean[][][] memoize
	) {
		Boolean res = memoize[pa][pb][pc];
		if (res != null) {
			return (boolean)res;
		}
        if (pa == a.length() && pb == b.length() && pc == c.length()) {
        	res = true;
        } else if (pc == c.length()) {
        	res = false;
        } else {
            res = false;
            if (pa != a.length() && c.charAt(pc) == a.charAt(pa) && checkOverlap(a, b, c, pa+1, pb, pc+1, memoize)) {
            	res = true;
            } else if (pb != b.length() && c.charAt(pc) == b.charAt(pb) && checkOverlap(a, b, c, pa, pb+1, pc+1, memoize)) {
            	res = true;
            }
        }
        return (memoize[pa][pb][pc] = res);
	}
	public static void main (String[] args) throws java.lang.Exception
	{
		boolean r1 = checkOverlap("xxy", "xxz", "xxzxxy");
		System.out.println(r1);
		boolean r2 = checkOverlap("xxyxxy", "xxzxxz", "xxzxxyxxyxxz");
		System.out.println(r2);
		boolean r3 = checkOverlap("xxy", "xxy", "xxzxxyxxyxxz");
		System.out.println(r3);
	}
}

