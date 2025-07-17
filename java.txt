// Java program to answer queries for 
// count of primes in given range.
import java.util.*;

class GFG {
    
static final int MAX = 10000;

// prefix[i] is going to store count 
// of primes till i (including i).
static int prefix[] = new int[MAX + 1];

static void buildPrefix() {
    
    // Create a boolean array "prime[0..n]". A
    // value in prime[i] will finally be false
    // if i is Not a prime, else true.
    boolean prime[] = new boolean[MAX + 1];
    Arrays.fill(prime, true);

    for (int p = 2; p * p <= MAX; p++) {

    // If prime[p] is not changed, then
    // it is a prime
    if (prime[p] == true) {

        // Update all multiples of p
        for (int i = p * 2; i <= MAX; i += p)
        prime[i] = false;
    }
    }

    // Build prefix array
    prefix[0] = prefix[1] = 0;
    for (int p = 2; p <= MAX; p++) {
    prefix[p] = prefix[p - 1];
    if (prime[p])
        prefix[p]++;
    }
}

// Returns count of primes in range 
// from L to R (both inclusive).
static int query(int L, int R)
{
    return prefix[R] - prefix[L - 1]; 
}

// Driver code
public static void main(String[] args) {
    
    buildPrefix();
    int L = 5, R = 10;
    System.out.println(query(L, R));

    L = 1; R = 10;
    System.out.println(query(L, R));
}
}

// This code is contributed by Anant Agarwal.
