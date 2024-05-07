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

double calculate(String input) {
  var parts = input.split(' ');
  if (parts.length != 3) {
    throw 'Невірний формат виразу';
  }

  var num1 = double.tryParse(parts[0]);
  var operator = parts[1];
  var num2 = double.tryParse(parts[2]);

  if (num1 == null || num2 == null) {
    throw 'Невірні операнди';
  }

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
