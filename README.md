# StylumiaCode
public class MatrixMultiplication {
    public static int matrixMult(int[] arr) {
        int n = arr.length - 1;  // Number of matrices
        int[][] dp = new int[n][n];

        for (int i = 0; i < n; i++) {
            dp[i][i] = 0;
        }

        for (int length = 2; length <= n; length++) {
            for (int i = 0; i < n - length + 1; i++) {
                int j = i + length - 1;
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = i; k < j; k++) {
                    dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k + 1][j] + arr[i] * arr[k + 1] * arr[j + 1]);
                }
            }
        }

        return dp[0][n - 1];
    }

    public static void main(String[] args) {
        int[] arr1 = {2,3, 4};
        int[] arr2 = {1,4,5,6,8};
        System.out.println(matrixMult(arr1));  // Output: 24
        System.out.println(matrixMult(arr2));  // Output: 98
    }
}





//
package drcode;

public class Main {

    public static void main(String[] args) {
        int[] arr = {4,3,2,1};
        int steps = ArrayChallenge(arr);
        System.out.println("Least number of steps to sort the array: " + steps);
    }

    public static int ArrayChallenge(int[] arr) {
        int n = arr.length;
        int swapsNeeded = 0;

        for (int i = 0; i < n; i++) {
            while (arr[i] != i + 1) {
                int temp = arr[i];
                arr[i] = arr[temp - 1];
                arr[temp - 1] = temp;
                swapsNeeded++;
            }
        }

        return swapsNeeded;
    }
}


//
import java.util.ArrayList;

public class Main2 {

    public static void main(String[] args) {
        String[] A = {"FOOF", "OCOO", "OOOH", "FOOO"};
       // String[] B = {"OOOO", "OOFF", "OCHO", "OFOO"};
       // String[] C = {"FOOO", "OCOH", "OFOF", "OFOO"};
        //String[] D = {"COFO", "OOFH", "OOFO", "OOFO"};
        //String[] E = {"FOFF", "FOOO", "OCOH", "FOFO"};

        System.out.println(CharlietheDog(A)); // 11
//        System.out.println(CharlietheDog(B)); // 7
//        System.out.println(CharlietheDog(C)); // 10
//        System.out.println(CharlietheDog(D)); // 8
//        System.out.println(CharlietheDog(E)); // 12
    }

    public static int CharlietheDog(String[] strArr) {
        ArrayList<int[]> result = new ArrayList<>();
        int totalDistance = 0;
        int currentX = 0;
        int currentY = 0;
        int dogX = 0;
        int dogY = 0;

        // Traversing the matrix to collect the important locations
        for (int row = 0; row < strArr.length; row++) {
            for (int col = 0; col < strArr[row].length(); col++) {
                char c = strArr[row].charAt(col);

                if (c == 'H') {
                    currentX = row;
                    currentY = col;
                } else if (c == 'C') {
                    dogX = row;
                    dogY = col;
                } else if (c == 'F') {
                    result.add(new int[]{row, col});
                }
            }
        }

        while (!result.isEmpty()) {
            int lowest = Integer.MAX_VALUE;
            int lowestIndex = 0;
            int lowestX = 0;
            int lowestY = 0;

            for (int x = 0; x < result.size(); x++) {
                int[] food = result.get(x);
                int getDistance = calculateDistance(currentX, currentY, food[0], food[1]);

                if (getDistance < lowest) {
                    lowest = getDistance;
                    lowestIndex = x;
                    lowestX = food[0];
                    lowestY = food[1];
                } else if (getDistance == lowest && calculateDistance(dogX, dogY, lowestX, lowestY) < calculateDistance(dogX, dogY, food[0], food[1])) {
                    lowest = getDistance;
                    lowestIndex = x;
                    lowestX = food[0];
                    lowestY = food[1];
                }
            }

            totalDistance += lowest;
            currentX = lowestX;
            currentY = lowestY;
            result.remove(lowestIndex);
        }

        totalDistance += calculateDistance(currentX, currentY, dogX, dogY);
        return totalDistance;
    }

    public static int calculateDistance(int x1, int y1, int x2, int y2) {
        if (x1 == x2 || y1 == y2) {
            return (int) Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2));
        }

        int xDistance = Math.abs(y2 - y1);
        int yDistance = Math.abs(x2 - x1);
        return xDistance + yDistance;
    }
}


//
import java.util.Scanner;

public class Main {
    public static int ArrayChallenge(int[] arr) {
       
        int n = arr.length - 1;
        int[][] dp = new int[n][n];

        for (int i = 0; i < n; i++) {
            dp[i][i] = 0;
        }

        for (int length = 2; length <= n; length++) {
            for (int i = 0; i < n - length + 1; i++) {
                int j = i + length - 1;
                dp[i][j] = Integer.MAX_VALUE;
                for (int k = i; k < j; k++) {
                    dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k + 1][j] + arr[i] * arr[k + 1] * arr[j + 1]);
                }
            }
        }

        return dp[0][n - 1];
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

       
        System.out.print("Enter the matrix dimensions (separated by spaces): ");
        String[] input = scanner.nextLine().split(" ");
        int[] arr = new int[input.length];
        for (int i = 0; i < input.length; i++) {
            arr[i] = Integer.parseInt(input[i]);
        }

        
        System.out.println("Minimum number of multiplications: " + ArrayChallenge(arr));
    }
}


//
public class MatrixChallenge {
    public static int findLargestSubmatrixArea(String[] matrix) {
        if (matrix.length == 0 || matrix[0].length() == 0)
            return 0;

        int rows = matrix.length;
        int cols = matrix[0].length();
        int[][] dp = new int[rows][cols];
        int maxArea = 0;

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (i == 0 || matrix[i].charAt(j) == '0') {
                    dp[i][j] = matrix[i].charAt(j) - '0';
                } else {
                    dp[i][j] = dp[i - 1][j] + 1;
                }

                int minWidth = dp[i][j];
                for (int k = j; k >= 0; k--) {
                    minWidth = Math.min(minWidth, dp[i][k]);
                    maxArea = Math.max(maxArea, minWidth * (j - k + 1));
                }
            }
        }

        return maxArea;
    }

    public static void main(String[] args) {
        String[] matrix1 = {"1011", "0011", "0111","1111"};
        String[] matrix2 = {"101", "111", "001"};

        System.out.println("Output for matrix1: " + findLargestSubmatrixArea(matrix1)); 
        System.out.println("Output for matrix2: " + findLargestSubmatrixArea(matrix2)); 
    }
}



//
package Stylumia;

public class BandGandN {
    public static void main(String[] args) {
        int[] arr = {10,5,4};
        System.out.println(findPairs(arr));
    }

    private static int findPairs(int[] arr) {
        int bcount = arr[2]/2;
        int gcount = arr[2]-bcount;

        int boyComb = combination(arr[0],bcount);
        int girlComb = combination(arr[1],gcount);
        int permut = findPermut(bcount);

        return boyComb*girlComb*permut;

    }

    private static int findPermut(int bcount) {
        int n = 1;
        for(int i = 1; i<= bcount; i++){
            n = n*i;
        }
        return n;
    }

    private static int combination(int n, int r) {
        int c = 1;
        for(int i = 0; i<r; i++){
            c = c*(n-i);
            c = c/(i+1);
        }
        return c;
    }
}
