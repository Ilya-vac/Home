import java.util.Scanner;

public class SimpleIterationMethod {

    public static double f(double x) {
        return Math.pow(x, 3) - x - 2;
    }

    public static double phi(double x) {
        return Math.cbrt(x + 2);
    }

    public static double solveByIteration(double x0, double epsilon, int maxIterations) {
        double xOld = x0;
        double xNew;
        int iteration = 0;

        System.out.println("\n--- Процесс итераций ---");
        System.out.printf("%-10s | %-12s | %-12s%n", "Итерация", "x_n", "Разность");

        do {
            xNew = phi(xOld);
            iteration++;
            
            double difference = Math.abs(xNew - xOld);
            System.out.printf("%-10d | %-12.6f | %-12.6f%n", iteration, xNew, difference);

            if (difference < epsilon) {
                System.out.println("Достигнута заданная точность.");
                return xNew;
            }

            xOld = xNew;
        } while (iteration < maxIterations);

        System.out.println("Достигнуто максимальное количество итераций.");
        return xNew;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Введите левую границу отрезка a: ");
        double a = scanner.nextDouble();

        System.out.print("Введите правую границу отрезка b: ");
        double b = scanner.nextDouble();

        System.out.print("Введите точность e (например, 0,0001): ");
        double epsilon = scanner.nextDouble();

        System.out.print("Введите максимальное количество итераций n: ");
        int maxIterations = scanner.nextInt();

        double x0 = (a + b) / 2.0;
        System.out.printf("Начальное приближение x0: %.4f%n", x0);

        double root = solveByIteration(x0, epsilon, maxIterations);

        System.out.println("\n--- Результат ---");
        System.out.printf("Приближенный корень уравнения: %.6f%n", root);
        System.out.printf("Значение f(root): %.6f%n", f(root));
        
        scanner.close();
    }
}
