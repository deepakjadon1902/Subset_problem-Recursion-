import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        int[] arr = new int[N];
        for (int i = 0; i < N; i++) {
            arr[i] = scanner.nextInt();
        }
        int target = scanner.nextInt();
        List<List<Integer>> subsets = new ArrayList<>();
        findSubsets(arr, 0, target, new ArrayList<>(), subsets);
        for (List<Integer> subset : subsets) {
            for (int num : subset) {
                System.out.print(num + " ");
            }
            System.out.print("  "); 
        }
        System.out.println();
        int count = countSubsets(arr, 0, target);
        System.out.println(count);
    }
    public static void findSubsets(int[] arr, int index, int target, List<Integer> current, List<List<Integer>> subsets) {
        if (target == 0) {
            subsets.add(new ArrayList<>(current));
            return;
        }
        if (index >= arr.length || target < 0) {
            return;
		}
        current.add(arr[index]);
        findSubsets(arr, index + 1, target - arr[index], current, subsets);
        current.remove(current.size() - 1);
        findSubsets(arr, index + 1, target, current, subsets);
    }
    public static int countSubsets(int[] arr, int index, int target) {
        if (target == 0) {
            return 1;
        }
        if (index >= arr.length || target < 0) {
            return 0;
        }
        int include = countSubsets(arr, index + 1, target - arr[index]);
        int exclude = countSubsets(arr, index + 1, target);
        return include + exclude;
    }
}
