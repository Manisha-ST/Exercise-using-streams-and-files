# Exercise-using-streams-and-files

package streamandfileexample;
import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.util.List;
import java.util.stream.Collectors;

public class StreamAndFileExample {

    public static void main(String[] args) {
      String inputFilePath ="input_numbers.txt";
      String outputFilePath = "output_squares.txt";  
      try{
          List<Integer>numbers = readNumbersFromFile(inputFilePath);
          List<Integer> squares = numbers.stream().map(num -> num * num).collect(Collectors.toList());
          writeSquaresToFile(outputFilePath,squares);
          System.out.println("Squares written to"+outputFilePath);
      }
      catch(IOException e)
      {
          e.printStackTrace();
      }
      }
     private static List<Integer>readNumbersFromFile (String filePath) throws
IOException {
          try (BufferedReader reader = new BufferedReader(new FileReader(filePath))) {
              return reader.lines().map(Integer::parseInt).collect(Collectors.toList());
          }
      }
      private static void writeSquaresToFile (String filePath, List<Integer>squares) throws
IOException {
          try (BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
              for (Integer square : squares) {
                  writer.write(square.toString());
                  writer.newLine();
              }
          }
      }
}

Output:
Squares written to output_squares.txt
1
4
9
16
25

