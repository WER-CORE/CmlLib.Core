# CmlLib.Core

## Бібліотека для лаунчера Minecraft

CmlLib.Core — це бібліотека для створення лаунчерів Minecraft на .NET

Підтримує всі ванільні та модифіковані версії (включаючи Forge, Fabric тощо...)

[Документація корейською мовою](https://www.google.com/search?q=https://cmllib.github.io/CmlLib.Core-wiki/ko/)

[Реклама: Створимо лаунчер для вас!](https://www.google.com/search?q=https://cmllib.github.io/CmlLib.Core-wiki/ko/ad/)

## Можливості

* Авторизація через обліковий запис Microsoft Xbox
* Отримання списку ванільних та встановлених версій
* Встановлення ванільних версій
* Запуск будь-якої ванільної версії (протестовано до 1.21)
* Запуск Forge, Optifine, FabricMC, LiteLoader або будь-якої іншої кастомної версії
* Встановлення середовища виконання Java (JRE)
* Встановлення LiteLoader, FabricMC
* Запуск із додатковими параметрами (пряме підключення до сервера, роздільна здатність екрана, аргументи JVM)
* Кросплатформеність (Windows, Linux, macOS)

[Перейти до Wiki для перегляду всіх можливостей](https://cmllib.github.io/CmlLib.Core-wiki/en/)

## Встановлення

Встановіть [NuGet-пакет CmlLib.Core](https://www.nuget.org/packages/CmlLib.Core)

## Швидкий старт

### Отримання всіх версій

```csharp
using CmlLib.Core;

var launcher = new MinecraftLauncher();
var versions = await launcher.GetAllVersionsAsync();
foreach (var version in versions)
{
    Console.WriteLine($"{version.Type} {version.Name}");
}

```

### Запуск гри

```csharp
using CmlLib.Core;
using CmlLib.Core.ProcessBuilder;

var launcher = new MinecraftLauncher();
var process = await launcher.InstallAndBuildProcessAsync("1.21", new MLaunchOption());
process.Start();

```

### Запуск гри з додатковими параметрами

```csharp
using CmlLib.Core;
using CmlLib.Core.Auth;
using CmlLib.Core.ProcessBuilder;

var path = new MinecraftPath("./my_game_dir");
var launcher = new MinecraftLauncher(path);
launcher.FileProgressChanged += (sender, args) =>
{
    Console.WriteLine($"Назва: {args.Name}");
    Console.WriteLine($"Тип: {args.EventType}");
    Console.WriteLine($"Всього: {args.TotalTasks}");
    Console.WriteLine($"Виконано: {args.ProgressedTasks}");
};
launcher.ByteProgressChanged += (sender, args) =>
{
    Console.WriteLine($"{args.ProgressedBytes} байт / {args.TotalBytes} байт");
};

await launcher.InstallAsync("1.20.4");
var process = await launcher.BuildProcessAsync("1.20.4", new MLaunchOption
{
    Session = MSession.CreateOfflineSession("Gamer123"),
    MaximumRamMb = 4096
});
process.Start();

```

## Документація

**[Офіційна документація](https://cmllib.github.io/CmlLib.Core-wiki/en/)**

**[Документація корейською мовою](https://www.google.com/search?q=https://cmllib.github.io/CmlLib.Core-wiki/ko/)**

## Приклад

[Приклад лаунчера](https://github.com/CmlLib/CmlLib-Minecraft-Launcher)

## Співрозробники

Створено за допомогою [contrib.rocks](https://contrib.rocks).
