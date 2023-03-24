import java.util.InputMismatchException;
import java.util.Scanner;

class Main {
    static int one, two;
    static char operator;
    static int result;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Введите выражение чисел в диапозоне от 1 до 10 или римские числа в диапозоне от I до X");
        String inPut = scanner.nextLine();
        String in = calc(inPut);
        in = in.replaceAll("\\s+", "");
        char[] chars = new char[10];
        for (int i = 0; i < in.length(); i++) {
            chars[i] = in.charAt(i);
            if (chars[i] == '+') {
                operator = '+';
            }
            if (chars[i] == '-') {
                operator = '-';
            }
            if (chars[i] == '*') {
                operator = '*';
            }
            if (chars[i] == '/') {
                operator = '/';
            }
        }
        String nums = String.valueOf(chars);
        String[] symbols = nums.split("[+\\-/*]");
        if (symbols.length != 2) {
            throw new ArrayIndexOutOfBoundsException("Недопустимый оператор или введено недопустимое кол-во значений");
        }
        String symbol1 = symbols[0];
        String symbol2 = symbols[1];
        String string3 = symbol2.trim();
        one = toNum(symbol1);
        two = toNum(string3);
        if (((((ifNum(symbol1)) && (ifNum(string3)))) || (symbol1.equals(ifRoms(one))))) {
            if (one < 0 && two < 0) {
                result = 0;
            } else if (symbol1.equals(ifRoms(one)) && string3.equals(ifRoms(two))) {
                result = calculated(one, two, operator);
                try {
                    String resultRom = convertToRoman(result);
                    System.out.println(resultRom);
                } catch (ArrayIndexOutOfBoundsException e) {
                    throw new ArrayIndexOutOfBoundsException("Ошибка. Ответ не может быть отрицательным.");
                }
            }
            else {
                throw new ArrayIndexOutOfBoundsException("Введены неверные значения");
            }
            if (symbol1.matches("^[0-9]+$") && string3.matches("^[0-9]+$")) {
                one = Integer.parseInt(symbol1);
                two = Integer.parseInt(string3);
                if (one <= 10 && one > 0 && two <= 10 && two > 0) {
                    result = calculated(one, two, operator);
                    System.out.println(result);
                }
                else {
                    throw new ArrayIndexOutOfBoundsException("Введены неверные значения");
                }
            }
        }
        else {
            throw new IllegalArgumentException("Введены неверные значения");
        }
    }


    public static int calculated(int num1, int num2, char operator) {
        int result = 0;
        switch (operator) {
            case '+':
                result = num1 + num2;
                break;
            case '-':
                result = num1 - num2;
                break;
            case '*':
                result = num1 * num2;
                break;
            case '/':
                try {
                    result = num1 / num2;
                } catch (ArithmeticException | InputMismatchException e) {
                    System.out.println("Exception : " + e);
                    System.out.println("Only integer non-zero parameters allowed");

                    break;
                }
                break;
            default:
                throw new IllegalArgumentException("Не верный знак операции");
        }
        return result;
    }

    private static String convertToRoman(int res) {
        String[] rom = {"O", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X", "XI", "XII", "XIII", "XIV", "XV", "XVI", "XVII", "XVIII", "XIX", "XX",
                "XXI", "XXII", "XXIII", "XXIV", "XXV", "XXVI", "XXVII", "XXVIII", "XXIX", "XXX", "XXXI", "XXXII", "XXXIII", "XXXIV", "XXXV", "XXXVI", "XXXVII", "XXXVIII", "XXXIX", "XL",
                "XLI", "XLII", "XLIII", "XLIV", "XLV", "XLVI", "XLVII", "XLVIII", "XLIX", "L", "LI", "LII", "LIII", "LIV", "LV", "LVI", "LVII", "LVIII", "LIX", "LX",
                "LXI", "LXII", "LXIII", "LXIV", "LXV", "LXVI", "LXVII", "LXVIII", "LXIX", "LXX",
                "LXXI", "LXXII", "LXXIII", "LXXIV", "LXXV", "LXXVI", "LXXVII", "LXXVIII", "LXXIX", "LXXX",
                "LXXXI", "LXXXII", "LXXXIII", "LXXXIV", "LXXXV", "LXXXVI", "LXXXVII", "LXXXVIII", "LXXXIX", "XC",
                "XCI", "XCII", "XCIII", "XCIV", "XCV", "XCVI", "XCVII", "XCVIII", "XCIX", "C"};
        return rom[res];
    }

    private static int toNum(String rom) {
        try {
            switch (rom) {
                case "I":
                    return 1;
                case "II":
                    return 2;
                case "III":
                    return 3;
                case "IV":
                    return 4;
                case "V":
                    return 5;
                case "VI":
                    return 6;
                case "VII":
                    return 7;
                case "VIII":
                    return 8;
                case "IX":
                    return 9;
                case "X":
                    return 10;
            }
        } catch (InputMismatchException e) {
            throw new InputMismatchException("недопустимый формат");
        }
        return -1;
    }

    public static String ifRoms(int res) {
        try {
            String[] rom = {"O", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX", "X"};
            return rom[res];
        } catch (ArrayIndexOutOfBoundsException e) {
            return null;
        }
    }
    public static String calc(String inputString) {
        return inputString;
    }
    public static boolean ifNum(String in) {
        try {
            Integer.parseInt(in);
            return true;
        } catch(NumberFormatException e){
            return false;
        }
    }
}
