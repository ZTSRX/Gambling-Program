//This is a quick gambling project of mine


import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.*;

public class Totolotek {

    public static void main(String[] args) throws IOException {
        final int NUMBER_OF_DRAWS = 1000;
        final int NUMBERS_PER_DRAW = 7;
        final int MAX_NUMBER = 43;

        Random random = new Random();
        int[] frequency = new int[MAX_NUMBER + 1];
        List<Set<Integer>> draws = new ArrayList<>();

        for (int i = 0; i < NUMBER_OF_DRAWS; i++) {
            Set<Integer> draw = new HashSet<>();
            while (draw.size() < NUMBERS_PER_DRAW) {
                draw.add(random.nextInt(MAX_NUMBER) + 1);
            }
            draws.add(draw);
            for (int number : draw) {
                frequency[number]++;
            }
        }

        StringBuilder result = new StringBuilder();
        result.append("Number Frequency (%):\n");
        for (int i = 1; i <= MAX_NUMBER; i++) {
            result.append(String.format("%d: %.2f%%\n", i, frequency[i] * 100.0 / (NUMBER_OF_DRAWS * NUMBERS_PER_DRAW)));
        }
        result.append("\nDraws:\n");
        for (int i = 0; i < draws.size(); i++) {
            result.append(String.format("Draw %d: %s\n", i + 1, draws.get(i)));
        }

        writeFile("totolotek_results.txt", result.toString());
        System.out.println("Results saved to totolotek_results.txt");
    }

    private static void writeFile(String file, String text) throws IOException {
        Files.write(Paths.get(file), text.getBytes());
    }
}
