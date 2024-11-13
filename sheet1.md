# Übungsblatt 1


## (1) Variablen: Typen und Namen

* Eine Variable, welche den Namen des Spielers speichert: `string name` (ein Name ist eine Zeichenkette).
* Eine Variable für die aktuellen Lebenspunkte des Spielercharakters: `double healthPoints` (könnte auch `int` o.ä. sein, ist in vielen Spielen aber als `double` gespeichert).
* Eine Variable, welche angibt, ob der Spielercharakter zur Zeit unverwundbar ist: `bool isInvincible` (es gibt hier nur zwei mögliche Zustände, unverwundbar und nicht unverwundbar).
* Eine Variable, welche die (möglichst exakte) Distanz zwischen zwei Objekten in unserer Spielewelt speichert: `double distance` (`double`, da der Wert _möglichst exakt_ sein soll).
* Eine Variable, welche angibt, wie viele Objekte sich in unserer Spielwelt befinden: `int numberOfObjects` (Anzahl ist eine ganze Zahl; wir könnten natürlich auch `uint` etc. verwenden.)
* Eine Variable, welche speichert, wie viel Zeit seit dem Start unseres Programmes vergangen ist: `int millisecondsSinceStart` (wir können die Zeit als Anzahl der verstrichenen Millisekunden speichern).
* Eine Variable für den aktuell anzuzeigenden Dialogtext: `string currentDialog` (Text).
* Eine Variable, die angibt, wie groß die Fläche eines bestimmten Rechtecks ist: `double area`.

## (2) Ein-/Ausgabe und Operatoren

```csharp
internal class Program {
    static void Main(string[] args) {
        // Remark: This solution uses a feature called string interpolation to
        // easily construct strings containing the values of variables. See:
        // https://learn.microsoft.com/en-us/dotnet/csharp/tutorials/string-interpolation

        // (1)
        Console.Write("Bitte geben Sie Ihren Namen ein: ");
        string name = Console.ReadLine();

        Console.WriteLine($"Ihr Name: {name}");
        Console.WriteLine($"Ihr Name in Kleinbuchstaben: {name.ToLower()}");
        Console.WriteLine($"Ihr Name in Großbuchstaben: {name.ToUpper()}");
        Console.WriteLine($"Ihr Name enthält den Buchstaben x: {name.Contains("x")}");

        // (2)
        Console.Write("Bitte geben Sie eine Ganze Zahl ein: ");
        int firstInt = int.Parse(Console.ReadLine());
        Console.Write("Bitte geben Sie eine weitere Ganze Zahl ein: ");
        int secondInt = int.Parse(Console.ReadLine());

        Console.WriteLine($"firstInt + secondInt == {firstInt + secondInt}");
        Console.WriteLine($"firstInt - secondInt == {firstInt - secondInt}");
        Console.WriteLine($"firstInt * secondInt == {firstInt * secondInt}");
        Console.WriteLine($"firstInt / secondInt == {firstInt / secondInt}");
        Console.WriteLine($"firstInt % secondInt == {firstInt % secondInt}");
        Console.WriteLine($"firstInt == secondInt == {firstInt == secondInt}");
        Console.WriteLine($"firstInt != secondInt == {firstInt != secondInt}");
        Console.WriteLine($"firstInt < secondInt == {firstInt < secondInt}");
        Console.WriteLine($"firstInt <= secondInt == {firstInt <= secondInt}");
        Console.WriteLine($"firstInt > secondInt == {firstInt > secondInt}");
        Console.WriteLine($"firstInt >= secondInt == {firstInt >= secondInt}");

        // (3)
        Console.Write("Bitte geben Sie eine Dezimalzahl ein: ");
        double firstDouble = double.Parse(Console.ReadLine());
        Console.Write("Bitte geben Sie eine weitere Dezimalzahl ein: ");
        double secondDouble = double.Parse(Console.ReadLine());

        Console.WriteLine($"firstDouble + secondDouble == {firstDouble + secondDouble}");
        Console.WriteLine($"firstDouble - secondDouble == {firstDouble - secondDouble}");
        Console.WriteLine($"firstDouble * secondDouble == {firstDouble * secondDouble}");
        Console.WriteLine($"firstDouble / secondDouble == {firstDouble / secondDouble}");
        Console.WriteLine($"firstDouble % secondDouble == {firstDouble % secondDouble}");
        Console.WriteLine($"firstDouble == secondDouble == {firstDouble == secondDouble}");
        Console.WriteLine($"firstDouble != secondDouble == {firstDouble != secondDouble}");
        Console.WriteLine($"firstDouble < secondDouble == {firstDouble < secondDouble}");
        Console.WriteLine($"firstDouble <= secondDouble == {firstDouble <= secondDouble}");
        Console.WriteLine($"firstDouble > secondDouble == {firstDouble > secondDouble}");
        Console.WriteLine($"firstDouble >= secondDouble == {firstDouble >= secondDouble}");

        // (4)
        bool boolTrue = true;
        bool boolFalse = false;

        Console.WriteLine($"!true == {!boolTrue}");
        Console.WriteLine($"!false == {!boolFalse}");

        Console.WriteLine($"true && true == {boolTrue && boolTrue}");
        Console.WriteLine($"true && false == {boolTrue && boolFalse}");
        Console.WriteLine($"false && true == {boolFalse && boolTrue}");
        Console.WriteLine($"false && false == {boolFalse && boolFalse}");

        Console.WriteLine($"true || true == {boolTrue || boolTrue}");
        Console.WriteLine($"true || false == {boolTrue || boolFalse}");
        Console.WriteLine($"false || true == {boolFalse || boolTrue}");
        Console.WriteLine($"false || false == {boolFalse || boolFalse}");
    }
}
```

## (3): FizzBuzz

```csharp
internal class Program {
    static void Main(string[] args) {
        // Ask the user for a positive integer.
        Console.Write("Please enter a positive integer: ");
        int max = int.Parse(Console.ReadLine());

        // Iterate all numbers from 1 to max.
        for (int i  = 1; i <= max; i++) {
            // Print depending on divisibility.
            if (i % 5 == 0 && i % 3 == 0) {
                Console.WriteLine("FizzBuzz");
            }
            else if (i % 3 == 0) {
                Console.WriteLine("Fizz");
            }
            else if (i % 5 == 0) {
                Console.WriteLine("Buzz");
            }
            else {
                Console.WriteLine(i);
            }
        }
    }
}
```

## (4) Codeknacker

```csharp
internal class Program {
    static void Main(string[] args) {
        // Generate the secret.
        int secretNumber = Random.Shared.Next(1, 100);
        Console.WriteLine("Die Zufallszahl wurde generiert. Viel Glück!");

        // Let the player guess until they find the secret number.
        while (true) {
            // Get next guess from the player.
            Console.Write("Ihr Versuch: ");
            int guess = int.Parse(Console.ReadLine());

            // Check if the player has won.
            if (guess == secretNumber) {
                Console.WriteLine($"Gratulation, Sie haben gewonnen! Die gesuchte Zahl war {secretNumber}.");
                break;
            }
            
            // Otherwise, give the player a tip.
            if (secretNumber < guess) {
                Console.WriteLine("Die gesuchte Zahl ist kleiner.");
            }
            else {
                Console.WriteLine("Die gesuchte Zahl ist größer.");
            }
        }
    }
}
```

## (5) Abwechselnd Hoch- und Runterzählen

```csharp
internal class Program {
    static void Main(string[] args) {
        int n = 16;

        for (int i = 1; i <= n / 2; i++) {
            Console.Write(i);
            Console.Write(" ");
            Console.Write(n - i + 1);
            Console.Write(" ");
        }
    }
}
```
