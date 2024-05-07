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
      var result = evaluateExpression(input);
      print('Результат: $result');
    } catch (e) {
      print('Помилка: $e');
    }
  }
}

double evaluateExpression(String expression) {
  // Розділити вираз на операнди та оператор
  List<String> elements = expression.split(' ');
  if (elements.length != 3) {
    throw 'Невірний формат виразу';
  }

  // Перетворити операнди на числа
  double operand1 = double.parse(elements[0]);
  double operand2 = double.parse(elements[2]);

  // Виконати арифметичну операцію
  switch (elements[1]) {
    case '+':
      return operand1 + operand2;
    case '-':
      return operand1 - operand2;
    case '*':
      return operand1 * operand2;
    case '/':
      if (operand2 == 0) {
        throw 'Ділення на нуль';
      }
      return operand1 / operand2;
    default:
      throw 'Непідтримуваний оператор';
  }
}

