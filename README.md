import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class FireDetectionProcessor {
	
	static int processedCount = 0;
	
    public static void main(String[] args) {
        String filePath = "grid.txt"; // Adjust path as necessary
        processFile(filePath);
    }

    private static void processFile(String filePath) {
        try {
            File file = new File(filePath);
            Scanner scanner = new Scanner(file);
            // Read grid dimensions
            int rows = scanner.nextInt();
            int cols = scanner.nextInt();
    
            // Read grid data
            int[][] grid = new int[rows][cols];
            for(int i = 0; i < rows; i++) {
            	for(int j = 0; j < cols; j++) {
            		grid[i][j] = scanner.nextInt();
            	}
            }
            // Read starting point
            
            int startRow = scanner.nextInt();
            int startCol = scanner.nextInt();
            // You may need to add additional methods or logic here
            scanner.close();
            
            System.out.println("Original Grid:");
            printGrid(grid);
            
            processFire(grid, startRow, startCol);
            
            System.out.println("\nProcessed Grid:");
            printGrid(grid);
            
            System.out.println("\nTotal fire-affected cells processed: " + processedCount);
            
            
        } catch (FileNotFoundException e) {
            System.err.println("File not found: " + filePath);
        }
    }

    public  static void printGrid(int[][] grid) {
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[i].length; j++) {
            	System.out.print(grid[i][j] + " ");
            }
            System.out.println();
        }
    }
    
    
    public  static void processFire(int[][] grid, int r, int c) {
    	
        if (r < 0 || r >= grid.length || c < 0 || c >= grid[0].length) {
            return;
        }
        
        if (grid[r][c] != 1) {
            return;
        }

        grid[r][c] = 2;
        processedCount++;

        processFire(grid, r - 1, c); //top
        processFire(grid, r + 1, c); //bottom
        processFire(grid, r, c - 1); //left
        processFire(grid, r, c + 1); //right
        
        processFire(grid, r - 1, c - 1); //top-left
        processFire(grid, r - 1, c + 1); //top-right
        processFire(grid, r + 1, c - 1); //bottom-left
        processFire(grid, r + 1, c + 1); //bottom-righthhhhhhhhhh
    }
}
