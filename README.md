import 'dart:io';

void main() {
  print('Ласкаво просимо до калькулятора. Введіть "вихід", щоб завершити.');

  while (true) {
    stdout.write('Введіть вираз (наприклад, 2 + 2): ');
    String? input = stdin.readLineSync();

    if (input!.toLowerCase() == 'вихід') {
      print('До побачення!');
      break;
    }

    try {
      var result = calculate(input);
      print('Результат: $result');
    } catch (e) {
      print('Помилка: $e');
    }
  }
}

double calculate(String expression) {
  // Видаляємо пробіли з виразу
  expression = expression.replaceAll(' ', '');

  // Шукаємо позицію оператора
  int operatorIndex = -1;
  for (int i = 0; i < expression.length; i++) {
    if (expression[i] == '+' || expression[i] == '-' || expression[i] == '*' || expression[i] == '/') {
      operatorIndex = i;
      break;
    }
  }

  // Отримуємо числа та оператор
  double num1 = double.parse(expression.substring(0, operatorIndex));
  double num2 = double.parse(expression.substring(operatorIndex + 1));
  String operator = expression[operatorIndex];

  // Виконуємо обчислення
  switch (operator) {
    case '+':
      return num1 + num2;
    case '-':
      return num1 - num2;
    case '*':
      return num1 * num2;
    case '/':
      if (num2 == 0) {
        throw 'Ділення на нуль неможливе';
      }
      return num1 / num2;
    default:
      throw 'Непідтримуваний оператор: $operator';
  }
}
