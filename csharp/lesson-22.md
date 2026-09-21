# C# · Урок 22. Windows Forms: основы

## Цели урока
- Создать оконное приложение
- Обрабатывать события элементов управления

## Создание проекта
Windows Forms работает на Windows. Через командную строку:
```bash
dotnet new winforms -n MyApp
cd MyApp
dotnet run
```
Или в Visual Studio: **Создать проект → Приложение Windows Forms**. Дизайнер позволяет перетаскивать элементы из панели инструментов.

## Основные элементы
`Form` (окно), `Label`, `Button`, `TextBox`, `CheckBox`, `RadioButton`, `ComboBox`, `ListBox`, `DataGridView`, `NumericUpDown`, `DateTimePicker`, `MenuStrip`, `Timer`.

## Пример без дизайнера
```csharp
public class MainForm : Form
{
    private readonly TextBox nameBox = new() { Left = 20, Top = 20, Width = 200 };
    private readonly Button greetBtn = new() { Text = "Поздороваться", Left = 20, Top = 60, Width = 200 };
    private readonly Label result = new() { Left = 20, Top = 100, AutoSize = true };

    public MainForm()
    {
        Text = "Приветствие";
        Width = 260;
        Height = 200;

        greetBtn.Click += OnGreetClick;
        Controls.AddRange(new Control[] { nameBox, greetBtn, result });
    }

    private void OnGreetClick(object? sender, EventArgs e)
    {
        string name = nameBox.Text.Trim();
        if (name == "")
        {
            MessageBox.Show("Введите имя", "Ошибка", MessageBoxButtons.OK, MessageBoxIcon.Warning);
            return;
        }
        result.Text = $"Привет, {name}!";
    }
}

static class Program
{
    [STAThread]
    static void Main()
    {
        ApplicationConfiguration.Initialize();
        Application.Run(new MainForm());
    }
}
```

## Приложение «Список дел»
```csharp
private void AddButton_Click(object sender, EventArgs e)
{
    if (string.IsNullOrWhiteSpace(taskBox.Text)) return;
    taskList.Items.Add(taskBox.Text.Trim());
    taskBox.Clear();
    taskBox.Focus();
}

private void DeleteButton_Click(object sender, EventArgs e)
{
    if (taskList.SelectedIndex >= 0)
        taskList.Items.RemoveAt(taskList.SelectedIndex);
}
```

## Диалоги
```csharp
var result = MessageBox.Show("Удалить запись?", "Подтверждение",
    MessageBoxButtons.YesNo, MessageBoxIcon.Question);
if (result == DialogResult.Yes) { /* ... */ }

using var dlg = new OpenFileDialog { Filter = "Текст|*.txt" };
if (dlg.ShowDialog() == DialogResult.OK) text = File.ReadAllText(dlg.FileName);
```

## Расположение элементов
- `Anchor` — привязка к краям окна
- `Dock` — прижатие к стороне
- `TableLayoutPanel`, `FlowLayoutPanel` — адаптивная раскладка

## Отзывчивость окна
Долгие операции выполняйте через `async/await` (урок 21), иначе окно «замёрзнет».

## Типичные ошибки
- Долгая работа в обработчике события блокирует интерфейс
- Обращение к элементам управления из другого потока (нужно `Invoke`)
- Логика приложения смешана с кодом формы — выносите в отдельные классы

## Практика
1. Калькулятор с двумя полями и кнопками «+ − × ÷».
2. Приложение «Список дел» с сохранением в файл.
3. Простой блокнот: открыть, сохранить, редактировать текст.

## Проверь себя
1. Что делает `Application.Run`?
2. Как подписаться на нажатие кнопки?
3. Почему нельзя блокировать UI-поток?

---
[← Урок 21](lesson-21.md) · [Программа курса](README.md) · [Урок 23 →](lesson-23.md)
