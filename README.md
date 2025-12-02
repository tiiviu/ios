# Homework Submission Instructions

1. **Fork** the repository.  
2. Create a folder using this path:  
   ```
   homework -> lesson (lesson number) -> your_name -> your_homework
   ```
   Example:  
   ```
   homework/lesson2/john_doe/todo_app/
   ```
3. Put your homework project into your folder.  
4. Create a **Pull Request** to the main repository.  
5. I will review your PR and leave comments.

---

# Table of Contents

- [Lesson 1 — Intro to Swift & SwiftUI](#lesson-1--intro-to-swift--swiftui)
- [Lesson 2 — SwiftUI Views, Layout & State](#lesson-2--swiftui-views-layout--state)
- [Lesson 3 — Lists & Navigation](#lesson-3--lists--navigation)
- [Lesson 4 — Forms, Images & Alerts](#lesson-4--forms-images--alerts)
- [Lesson 5 — Data Models & Persistence](#lesson-5--data-models--persistence)

---

# Lesson 1 — Intro to Swift & SwiftUI

<a id="goal-of-the-lesson-1"></a>
## Goal of the lesson

After this lesson the student should be able to:

* understand basic Swift syntax
* use `var` / `let`
* work with simple data types (String, Int, Double, Bool)
* write simple functions
* understand the concept of state in SwiftUI
* build a very simple UI using `@State`, `Text`, `Button`, `VStack`

---

## 1. Introduction to Swift & Xcode

### Key points:

* Swift is a modern safe language used for iOS development.
* Xcode is the main tool for writing, testing, and running apps.
* SwiftUI is a declarative UI framework where UI updates automatically when data changes.

### Steps:

1. Open Xcode → File → New → Project
2. Select **iOS App**
3. Interface: **SwiftUI**
4. Language: **Swift**

### Default SwiftUI code:

```swift
struct ContentView: View {
    var body: some View {
        Text("Hello")
            .padding()
    }
}
```

Run the app in the simulator to confirm everything works.

---

## 2. Swift Basics

This block should be shown in a **Playground**.

### Key points:

* Use `var` for variables, `let` for constants.
* Basic types: `String`, `Int`, `Double`, `Bool`.
* Functions use `func` keyword.

### Examples:

```swift
var name = "Alex"
let age = 21
var temperature: Double = 36.5

func greet(_ name: String) -> String {
    "Hello, \(name)"
}

func mood(for value: Int) -> String {
    if value < 0 { return "Negative" }
    if value == 0 { return "Neutral" }
    return "Positive"
}
```

---

## 3. First SwiftUI Screen

### Concept:

> SwiftUI = UI as a function of **state**.
> When state changes, UI updates automatically.

### Example:

```swift
struct ContentView: View {
    @State private var count = 0

    var body: some View {
        VStack(spacing: 20) {
            Text("Count: \(count)")
                .font(.largeTitle)

            Button("Increase") {
                count += 1
            }
        }
        .padding()
    }
}
```

---

## 4. Homework — Mood Counter v1 (due via Pull Request)

Create a simple SwiftUI app with:

### Requirements:

1. `@State var count = 0`
2. Three buttons:

   * **+1** → increases count by 1
   * **–1** → decreases count by 1
   * **Reset** → sets count back to 0
3. A text showing the current count value:

   ```
   Value: X
   ```
   (where X is the current count number)
4. A function:

   ```swift
   func mood() -> String
   ```

   that returns:
   * "Negative" if count < 0
   * "Neutral" if count == 0
   * "Positive" if count > 0
5. Display the mood result in a separate `Text` view:

   ```
   Mood: [result of mood() function]
   ```
   
   The mood text color should change based on count:
   * red if count < 0
   * gray if count == 0
   * green if count > 0

---

## 5. Resources

* Apple Docs: Swift Basics
* SwiftUI Tutorials
* Xcode documentation

---

# Lesson 2 — SwiftUI Views, Layout & State  

<a id="goal-of-the-lesson-2"></a>
## Goal of the lesson

By the end of this lesson, the student should be able to:

* Understand declarative UI in SwiftUI
* Use `VStack`, `HStack`, `ZStack`
* Apply SwiftUI modifiers
* Use SF Symbols with `Image(systemName:)`
* Work with `@State`
* Use `ForEach` to iterate over collections
* Build simple interactive components  

---

## 1. Declarative UI

### Concept:

> UI = function of state, UI automatically updates when state changes.

### Example:

```swift
struct ExampleView: View {
    @State private var isOn = false
    
    var body: some View {
        VStack {
            Toggle("Switch", isOn: $isOn)
            Text(isOn ? "Enabled" : "Disabled")
                .font(.title)
        }
        .padding()
    }
}
```

---

## 2. Layout Containers

### Key points:

* `VStack` arranges views vertically.
* `HStack` arranges views horizontally.
* `ZStack` layers views on top of each other.

### Examples:

```swift
VStack(spacing: 16) {
    Text("Hello")
    Text("World")
}

HStack {
    Text("Left")
    Spacer()
    Text("Right")
}

ZStack {
    Color.blue
    Text("On top")
        .foregroundColor(.white)
}
```

---

## 3. Modifiers

### Key points:

* Order matters; modifiers return new views.

### Example:

```swift
Text("Hello")
    .font(.title)
    .padding()
    .background(Color.yellow)
    .cornerRadius(12)
```

---

## 4. SF Symbols

### Concept:

> SF Symbols is Apple's icon library with thousands of built-in symbols. Use `Image(systemName:)` to display them.

### Key points:

* SF Symbols are vector icons that scale perfectly.
* Use `Image(systemName: "symbol-name")` to display a symbol.
* You can customize size, color, and weight with modifiers.
* Browse symbols in Xcode: Editor → Add SF Symbol, or visit [developer.apple.com/sf-symbols](https://developer.apple.com/sf-symbols)

### Example:

```swift
HStack {
    Image(systemName: "star.fill")
        .foregroundColor(.yellow)
    Image(systemName: "heart")
        .foregroundColor(.red)
    Image(systemName: "circle")
        .foregroundColor(.blue)
}
```

Common symbols: `"circle"`, `"checkmark"`, `"star.fill"`, `"heart"`, `"plus"`, `"minus"`, `"trash"`

---

## 5. @State

### Concept:

> `@State` stores view-local state and triggers UI updates.

### Example:

```swift
struct NameView: View {
    @State private var name = ""
    @State private var isVisible = false
    
    var body: some View {
        VStack(spacing: 20) {
            TextField("Enter your name", text: $name)
                .textFieldStyle(.roundedBorder)
                .padding()
            
            Button("Show Greeting") {
                isVisible = true
            }
            .buttonStyle(.borderedProminent)
            
            if isVisible {
                Text("Hello, \(name.isEmpty ? "Guest" : name)!")
                    .font(.title)
                    .foregroundColor(.blue)
            }
        }
        .padding()
    }
}
```

---

## 6. ForEach

### Concept:

> `ForEach` iterates over collections and creates views for each element. It's used to display dynamic lists.

### Key points:

* `ForEach` requires each element to have a unique identifier (`id`).
* Use `id: \.self` for simple types like `String`.
* Works inside containers like `VStack`, `HStack`, or `List`.

### Example:

```swift
struct ContentView: View {
    @State private var items = ["Task 1", "Task 2", "Task 3"]
    
    var body: some View {
        VStack {
            ForEach(items, id: \.self) { item in
                HStack {
                    Image(systemName: "circle")
                    Text(item)
                }
                .padding()
            }
        }
    }
}
```

---

## 7. Homework — Mini To-Do List App

Create a simple SwiftUI app with:

### Requirements:

#### 1. State Management

* Use `@State private var items: [String] = []` to store the list of tasks
* Use `@State private var newTask: String = ""` to store the current input text

#### 2. Layout Structure

* **VStack**: Use as the main container for the entire screen (contains input section and tasks list)
* **HStack**: 
  * Use one `HStack` for the input section (TextField + "Add" button)
  * Use `HStack` inside `ForEach` for each task row (SF Symbol + task text)
* **ZStack**: Use to add a background color or decorative element (optional but encouraged)

#### 3. Input Section

* **TextField**: For entering new tasks, bound to `newTask` state
* **Button**: "Add" button that:
  * Adds `newTask` to `items` array
  * Clears the `newTask` field after adding
  * Only adds if `newTask` is not empty

#### 4. Tasks List

* **ForEach**: Use `ForEach(items, id: \.self)` to iterate over tasks
* Each task row must contain:
  * **HStack** with:
    * **SF Symbol**: Use `Image(systemName:)` (e.g., "circle", "checkmark.circle", "list.bullet")
    * **Text**: Display the task string

#### 5. Styling (Modifiers)

Apply modifiers to create a clean layout:

* Use `.padding()` on containers
* Use `.cornerRadius()` on task rows or background
* Use `.background()` with colors (e.g., `Color.gray.opacity(0.1)`)
* Use `.foregroundColor()` on SF Symbols
* Use `.textFieldStyle(.roundedBorder)` on TextField
* Use `.buttonStyle()` on Button (e.g., `.borderedProminent`)

#### 6. Structure Example

```
ContentView
 └─ VStack (main container)
     ├─ HStack (input section)
     │   ├─ TextField
     │   └─ Button("Add")
     └─ VStack or ForEach (tasks list)
         └─ ForEach(items)
             └─ HStack (each task row)
                 ├─ Image(systemName: "...")
                 └─ Text(task)
```

---

## 8. Resources

* Apple Docs: SwiftUI Essentials
* SwiftUI cheat sheets
* SwiftUI basics videos on YouTube
* [SF Symbols Browser](https://developer.apple.com/sf-symbols)

---

# Lesson 3 — Lists & Navigation

<a id="goal-of-the-lesson-3"></a>
## Goal of the lesson

By the end of this lesson, the student should be able to:

* Use `List` to display collections of data
* Implement navigation using `NavigationView` and `NavigationLink`
* Create detail views and pass data between screens
* Organize lists using `Section` with headers and footers
* Use `@Binding` to edit data in detail views
* Handle user interactions in lists (swipe-to-delete)
* Apply list modifiers for styling

---

## 1. Lists in SwiftUI

### Concept:

> `List` is a container that displays rows of data. It's optimized for scrolling and automatically handles cell reuse.

### Example:

```swift
struct ContentView: View {
    let items = ["Apple", "Banana", "Orange"]
    
    var body: some View {
        List {
            ForEach(items, id: \.self) { item in
                Text(item)
            }
        }
    }
}
```

---

## 2. Navigation

### Concept:

> `NavigationView` provides a navigation container, and `NavigationLink` creates tappable rows that navigate to detail views. You can pass data to detail views through their initializers.

### Key points:

* `NavigationView` wraps your content and provides navigation capabilities.
* `NavigationLink` creates tappable rows that navigate to another view.
* Pass data to detail views by including it as a parameter in the view's initializer.
* Use `.navigationTitle()` to set the title of the current screen.
* The detail view receives data as a `let` constant.

### Example:

```swift
struct ContentView: View {
    let fruits = ["Apple", "Banana", "Orange"]
    
    var body: some View {
        NavigationView {
            List {
                ForEach(fruits, id: \.self) { fruit in
                    NavigationLink(destination: DetailView(fruit: fruit)) {
                        Text(fruit)
                    }
                }
            }
            .navigationTitle("Fruits")
        }
    }
}

struct DetailView: View {
    let fruit: String
    
    var body: some View {
        VStack(spacing: 20) {
            Text(fruit)
                .font(.largeTitle)
            Text("You selected: \(fruit)")
                .foregroundColor(.secondary)
        }
        .navigationTitle(fruit)
        .padding()
    }
}
```

---

## 3. List Sections

### Concept:

> `Section` groups related rows in a list and can have headers and footers.

### Key points:

* Use `Section` to organize list items into groups.
* Add headers with `header:` parameter.
* Add footers with `footer:` parameter.

### Example:

```swift
struct ContentView: View {
    var body: some View {
        NavigationView {
            List {
                Section(header: Text("Fruits")) {
                    Text("Apple")
                    Text("Banana")
                    Text("Orange")
                }
                
                Section(header: Text("Vegetables")) {
                    Text("Carrot")
                    Text("Broccoli")
                }
            }
            .navigationTitle("Shopping List")
        }
    }
}
```

---

## 4. List Modifiers

### Key points:

* Lists can be styled with various modifiers.
* `.listStyle()` changes the appearance.
* `.onDelete()` enables swipe-to-delete.

### Example:

```swift
struct ContentView: View {
    @State private var items = ["Item 1", "Item 2", "Item 3"]
    
    var body: some View {
        NavigationView {
            List {
                ForEach(items, id: \.self) { item in
                    Text(item)
                }
                .onDelete(perform: deleteItems)
            }
            .navigationTitle("My List")
            .listStyle(.insetGrouped)
        }
    }
    
    func deleteItems(at offsets: IndexSet) {
        items.remove(atOffsets: offsets)
    }
}
```

---

## 5. Binding in Navigation

### Concept:

> `@Binding` allows a child view to modify data owned by a parent view. Use it when you need to edit data in a detail view.

### Key points:

* `@Binding` creates a two-way connection between views.
* Parent view uses `@State`, child view uses `@Binding`.
* Pass binding with `$` prefix: `$variableName`.

### Example:

```swift
struct ContentView: View {
    @State private var items = ["Item 1", "Item 2", "Item 3"]
    
    var body: some View {
        NavigationView {
            List {
                ForEach(items.indices, id: \.self) { index in
                    NavigationLink(destination: EditView(item: $items[index])) {
                        Text(items[index])
                    }
                }
            }
            .navigationTitle("My List")
        }
    }
}

struct EditView: View {
    @Binding var item: String
    
    var body: some View {
        VStack {
            TextField("Edit item", text: $item)
                .textFieldStyle(.roundedBorder)
                .padding()
            Text("Current value: \(item)")
        }
        .navigationTitle("Edit")
    }
}
```

---

## 6. Homework — Shopping List App

Create a simple SwiftUI app with:

### Requirements:

1. Use: `NavigationView`, `List`, `Section`, `ForEach`, `NavigationLink`, `@State`, `@Binding`, `TextField`, `Button`
2. Features:

   * TextField for item input
   * "Add" button to add items to the list
   * Store items in `@State var items = [String]()`
   * Display items in a `List` organized with `Section`:
     * Use at least one `Section` with a header (e.g., "My Items" or "Shopping List")
     * Items should be inside the section
   * Use `ForEach` to iterate over items
   * Each item should be a `NavigationLink` to a detail/edit view
   * Detail/Edit view:
     * Use `@Binding` to allow editing the item name
     * Shows a `TextField` bound to the item (using `@Binding`)
     * Displays the current item value
     * Changes made in detail view should update the main list automatically
     * Has a navigation title (e.g., "Edit Item")
   * Swipe-to-delete functionality (use `.onDelete()` modifier on `ForEach`)
   * Navigation title "Shopping List" on the main list screen
   * Clean layout with proper spacing and padding

---

## 7. Resources

* Apple Docs: Lists and Navigation
* SwiftUI List tutorial
* NavigationView documentation

---

# Lesson 4 — Forms, Images & Alerts

<a id="goal-of-the-lesson-4"></a>
## Goal of the lesson

By the end of this lesson, the student should be able to:

* Create forms using `Form` container
* Work with different input controls (`Toggle`, `Picker`, `Stepper`)
* Display images from assets and system symbols
* Show alerts and action sheets for user feedback
* Handle user input validation
* Build complete forms with multiple input types

---

## 1. Forms

### Concept:

> `Form` is a container that groups input controls together. It automatically adapts to different platforms and provides a native look.

### Key points:

* `Form` groups related input controls.
* Automatically styles controls for the platform.
* Use `Section` inside forms to organize inputs.

### Example:

```swift
struct ContentView: View {
    @State private var name = ""
    @State private var email = ""
    
    var body: some View {
        NavigationView {
            Form {
                Section(header: Text("Personal Information")) {
                    TextField("Name", text: $name)
                    TextField("Email", text: $email)
                }
            }
            .navigationTitle("Settings")
        }
    }
}
```

---

## 2. Input Controls

### Toggle

```swift
struct ContentView: View {
    @State private var isEnabled = false
    
    var body: some View {
        Form {
            Toggle("Enable notifications", isOn: $isEnabled)
        }
    }
}
```

### Picker

```swift
struct ContentView: View {
    @State private var selectedColor = "Red"
    let colors = ["Red", "Green", "Blue"]
    
    var body: some View {
        Form {
            Picker("Favorite Color", selection: $selectedColor) {
                ForEach(colors, id: \.self) { color in
                    Text(color).tag(color)
                }
            }
        }
    }
}
```

### Stepper

```swift
struct ContentView: View {
    @State private var quantity = 1
    
    var body: some View {
        Form {
            Stepper("Quantity: \(quantity)", value: $quantity, in: 1...10)
        }
    }
}
```

---

## 3. Images

### Concept:

> `Image` displays images from assets, system symbols, or remote URLs. Use it to add visual content to your app.

### Key points:

* Use `Image("asset-name")` for images.
* Use `Image(systemName:)` for SF Symbols.
* Apply modifiers like `.resizable()`, `.scaledToFit()`, `.frame()`.

### Example:

```swift
struct ContentView: View {
    var body: some View {
        VStack(spacing: 20) {
            // System symbol
            Image(systemName: "star.fill")
                .font(.system(size: 50))
                .foregroundColor(.yellow)
            
            // Asset image (if you have "logo" in Assets)
            Image("logo")
                .resizable()
                .scaledToFit()
                .frame(width: 200, height: 200)
        }
        .padding()
    }
}
```

### Image Modifiers:

```swift
Image("photo")
    .resizable()
    .scaledToFill()
    .frame(width: 300, height: 200)
    .clipped()
    .cornerRadius(12)
```

---

## 4. Alerts

### Concept:

> `Alert` displays a modal dialog with a message and buttons. Use it to confirm actions or show important information.

### Key points:

* Use `.alert()` modifier with `@State` boolean to control visibility.
* Define title, message, and buttons.
* Buttons can be dismissive or have custom actions.

### Example:

```swift
struct ContentView: View {
    @State private var showAlert = false
    
    var body: some View {
        VStack {
            Button("Show Alert") {
                showAlert = true
            }
        }
        .alert("Important", isPresented: $showAlert) {
            Button("OK") { }
            Button("Cancel", role: .cancel) { }
        } message: {
            Text("This is an important message.")
        }
    }
}
```

---

## 5. Action Sheets

### Concept:

> `ActionSheet` (now `.confirmationDialog`) presents options from the bottom of the screen. Use it for multiple choices.

### Key points:

* Similar to alerts but appears from the bottom.
* Good for presenting multiple action options.
* Use `.confirmationDialog()` modifier.

### Example:

```swift
struct ContentView: View {
    @State private var showActionSheet = false
    
    var body: some View {
        VStack {
            Button("Show Options") {
                showActionSheet = true
            }
        }
        .confirmationDialog("Choose an option", isPresented: $showActionSheet, titleVisibility: .visible) {
            Button("Option 1") { }
            Button("Option 2") { }
            Button("Cancel", role: .cancel) { }
        }
    }
}
```

---

## 6. Complete Form Example

### Example:

```swift
struct ProfileView: View {
    @State private var name = ""
    @State private var age = 18
    @State private var notificationsEnabled = true
    @State private var selectedTheme = "Light"
    @State private var showAlert = false
    
    let themes = ["Light", "Dark", "Auto"]
    
    var body: some View {
        NavigationView {
            Form {
                Section(header: Text("Personal Info")) {
                    TextField("Name", text: $name)
                    Stepper("Age: \(age)", value: $age, in: 13...120)
                }
                
                Section(header: Text("Preferences")) {
                    Toggle("Notifications", isOn: $notificationsEnabled)
                    Picker("Theme", selection: $selectedTheme) {
                        ForEach(themes, id: \.self) { theme in
                            Text(theme).tag(theme)
                        }
                    }
                }
                
                Section {
                    Button("Save Profile") {
                        showAlert = true
                    }
                }
            }
            .navigationTitle("Profile")
            .alert("Profile Saved", isPresented: $showAlert) {
                Button("OK") { }
            } message: {
                Text("Your profile has been saved successfully.")
            }
        }
    }
}
```

---

## 7. Homework — Event Registration App

Create a multi-screen SwiftUI app for event registration:

### Requirements:

1. Use: `NavigationView`, `List`, `Form`, `Section`, `TextField`, `Toggle`, `Picker`, `Stepper`, `Button`, `Alert`, `Image`, `@State`, `@Binding`, `ForEach`, `NavigationLink`

2. **Screen 1: Event List** (Main Screen):
   * Display a list of events using `List` and `ForEach`
   * Each event should show:
     * Event name (use SF Symbol as icon)
     * Event date
     * Number of registered attendees
   * Use `Section` to group events (e.g., "Upcoming Events", "Past Events")
   * Each event row should be a `NavigationLink` to registration screen
   * Navigation title: "Events"

3. **Screen 2: Registration Form** (Detail Screen):
   * Use `Form` with multiple `Section`s:
     * **Personal Information Section**:
       * TextField for full name (required)
       * TextField for email (required)
       * Stepper for number of tickets (range 1-10)
     * **Preferences Section**:
       * Toggle for "Receive event updates"
       * Picker for meal preference (at least 3 options: "Vegetarian", "Vegan", "Regular")
     * **Additional Info Section**:
       * TextField for special requests (optional)
   * **Validation Logic**:
     * "Register" button should be disabled if name or email is empty
     * Show different button style when disabled (use conditional modifier)
   * When "Register" is tapped:
     * Show Alert confirming registration
     * Alert should show number of tickets registered
     * After confirming alert, navigate back to event list
   * Navigation title should show event name

4. **Screen 3: Registration Summary** (Optional Bonus):
   * Create a summary view that shows:
     * Event name with large SF Symbol
     * All registration details in a formatted list
     * Use `Section` to organize information
     * "Done" button that navigates back

5. **Data Management**:
   * Store events in `@State var events: [String]` in main view
   * Use `@Binding` to pass event name to registration form
   * Track registration count (increment when registration is confirmed)
   * Registration form should use `@State` for all input fields

6. **Visual Requirements**:
   * Use SF Symbols throughout (at least 3 different symbols)
   * Style images with appropriate colors and sizes
   * Apply consistent padding and spacing
   * Use `.listStyle()` modifier on List

7. **Bonus Challenges**:
   * Add swipe-to-delete on event list
   * Show confirmation dialog before deleting
   * Add validation for email format (basic check for "@" symbol)
   * Display registration count badge on event list items

---

## 8. Resources

* Apple Docs: Forms and Controls
* SwiftUI Image documentation
* Alert and ActionSheet guide
* Human Interface Guidelines for Forms

---

# Lesson 5 — Data Models & Persistence

<a id="goal-of-the-lesson-5"></a>
## Goal of the lesson

By the end of this lesson, the student should be able to:

* Create data models using `struct` with `Identifiable`
* Use `UserDefaults` to persist simple data
* Create reusable custom views
* Work with arrays of custom objects
* Implement data persistence across app launches
* Build apps with structured data

---

## 1. Data Models

### Concept:

> Data models represent structured information in your app. Use `struct` to create models that conform to `Identifiable` for use in lists.

### Key points:

* Use `struct` to define data models.
* Conform to `Identifiable` protocol for use with `ForEach`.
* Properties can have default values.
* Models can contain computed properties.

### Example:

```swift
struct Task: Identifiable {
    let id = UUID()
    var title: String
    var isCompleted: Bool
    var priority: Int
    
    init(title: String, isCompleted: Bool = false, priority: Int = 1) {
        self.title = title
        self.isCompleted = isCompleted
        self.priority = priority
    }
}

struct ContentView: View {
    @State private var tasks = [
        Task(title: "Buy groceries", priority: 2),
        Task(title: "Finish homework", isCompleted: true, priority: 1)
    ]
    
    var body: some View {
        List {
            ForEach(tasks) { task in
                HStack {
                    Text(task.title)
                    Spacer()
                    if task.isCompleted {
                        Image(systemName: "checkmark.circle.fill")
                            .foregroundColor(.green)
                    }
                }
            }
        }
    }
}
```

---

## 2. Working with Arrays of Models

### Concept:

> Arrays of models allow you to manage collections of structured data. You can add, remove, and modify items.

### Key points:

* Use arrays to store multiple model instances.
* Modify arrays using methods like `append()`, `remove()`, `removeAll()`.
* Use indices when you need to modify specific items.

### Example:

```swift
struct ContentView: View {
    @State private var tasks: [Task] = []
    @State private var newTaskTitle = ""
    
    var body: some View {
        VStack {
            HStack {
                TextField("New task", text: $newTaskTitle)
                Button("Add") {
                    let task = Task(title: newTaskTitle)
                    tasks.append(task)
                    newTaskTitle = ""
                }
            }
            .padding()
            
            List {
                ForEach(tasks) { task in
                    Text(task.title)
                }
                .onDelete(perform: deleteTasks)
            }
        }
    }
    
    func deleteTasks(at offsets: IndexSet) {
        tasks.remove(atOffsets: offsets)
    }
}
```

---

## 3. UserDefaults

### Concept:

> `UserDefaults` is a simple way to persist small amounts of data. It's perfect for user preferences and settings.

### Key points:

* `UserDefaults.standard` is the main storage.
* Use `set()` to save values.
* Use methods like `string()`, `bool()`, `integer()` to retrieve values.
* Data persists across app launches.

### Example:

```swift
struct ContentView: View {
    @State private var username: String = ""
    
    var body: some View {
        VStack {
            TextField("Username", text: $username)
                .textFieldStyle(.roundedBorder)
                .padding()
            
            Button("Save") {
                UserDefaults.standard.set(username, forKey: "username")
            }
            
            Button("Load") {
                username = UserDefaults.standard.string(forKey: "username") ?? ""
            }
        }
        .onAppear {
            username = UserDefaults.standard.string(forKey: "username") ?? ""
        }
    }
}
```

---

## 4. Saving Arrays to UserDefaults

### Concept:

> You can save arrays to UserDefaults by encoding them to Data using `JSONEncoder`, or by saving simple types directly.

### Key points:

* Simple arrays (String, Int, Bool) can be saved directly.
* Complex objects need encoding with `Codable` protocol.
* Use `JSONEncoder` and `JSONDecoder` for encoding/decoding.

### Example:

```swift
struct Task: Identifiable, Codable {
    let id = UUID()
    var title: String
    var isCompleted: Bool
}

struct ContentView: View {
    @State private var tasks: [Task] = []
    
    var body: some View {
        VStack {
            // ... UI code ...
        }
        .onAppear {
            loadTasks()
        }
    }
    
    func saveTasks() {
        if let encoded = try? JSONEncoder().encode(tasks) {
            UserDefaults.standard.set(encoded, forKey: "tasks")
        }
    }
    
    func loadTasks() {
        if let data = UserDefaults.standard.data(forKey: "tasks"),
           let decoded = try? JSONDecoder().decode([Task].self, from: data) {
            tasks = decoded
        }
    }
}
```

---

## 5. Custom Views

### Concept:

> Custom views are reusable components you create. They help organize code and make it more maintainable.

### Key points:

* Create separate `struct` views for reusable components.
* Pass data using initializer parameters.
* Use `@Binding` when the view needs to modify parent data.

### Example:

```swift
struct TaskRowView: View {
    let task: Task
    
    var body: some View {
        HStack {
            Image(systemName: task.isCompleted ? "checkmark.circle.fill" : "circle")
                .foregroundColor(task.isCompleted ? .green : .gray)
            Text(task.title)
            Spacer()
        }
        .padding(.vertical, 4)
    }
}

struct ContentView: View {
    @State private var tasks: [Task] = []
    
    var body: some View {
        List {
            ForEach(tasks) { task in
                TaskRowView(task: task)
            }
        }
    }
}
```

### Custom View with Binding:

```swift
struct TaskToggleView: View {
    @Binding var task: Task
    
    var body: some View {
        HStack {
            Toggle("", isOn: $task.isCompleted)
            Text(task.title)
                .strikethrough(task.isCompleted)
        }
    }
}
```

---

## 6. Complete Example: Todo App with Persistence

### Example:

```swift
struct Task: Identifiable, Codable {
    let id = UUID()
    var title: String
    var isCompleted: Bool = false
}

struct TaskRowView: View {
    @Binding var task: Task
    
    var body: some View {
        HStack {
            Image(systemName: task.isCompleted ? "checkmark.circle.fill" : "circle")
                .foregroundColor(task.isCompleted ? .green : .gray)
                .onTapGesture {
                    task.isCompleted.toggle()
                }
            Text(task.title)
                .strikethrough(task.isCompleted)
            Spacer()
        }
        .padding(.vertical, 4)
    }
}

struct ContentView: View {
    @State private var tasks: [Task] = []
    @State private var newTaskTitle = ""
    
    var body: some View {
        NavigationView {
            VStack {
                HStack {
                    TextField("New task", text: $newTaskTitle)
                        .textFieldStyle(.roundedBorder)
                    Button("Add") {
                        let task = Task(title: newTaskTitle)
                        tasks.append(task)
                        newTaskTitle = ""
                        saveTasks()
                    }
                    .disabled(newTaskTitle.isEmpty)
                }
                .padding()
                
                List {
                    ForEach($tasks) { $task in
                        TaskRowView(task: $task)
                    }
                    .onDelete { indexSet in
                        tasks.remove(atOffsets: indexSet)
                        saveTasks()
                    }
                }
            }
            .navigationTitle("Tasks")
            .onAppear {
                loadTasks()
            }
        }
    }
    
    func saveTasks() {
        if let encoded = try? JSONEncoder().encode(tasks) {
            UserDefaults.standard.set(encoded, forKey: "tasks")
        }
    }
    
    func loadTasks() {
        if let data = UserDefaults.standard.data(forKey: "tasks"),
           let decoded = try? JSONDecoder().decode([Task].self, from: data) {
            tasks = decoded
        }
    }
}
```

---

## 7. Homework — Notes App with Categories

Create a SwiftUI app for managing notes with categories:

### Requirements:

1. Use: `NavigationView`, `List`, `Form`, `Section`, `TextField`, `Picker`, `Button`, `@State`, `@Binding`, `ForEach`, `UserDefaults`, Custom Views

2. **Data Model**:
   * Create a `Note` struct that conforms to `Identifiable` and `Codable`
   * Properties: `id`, `title`, `content`, `category`, `createdDate`
   * Create a `Category` enum or use String with predefined categories
   * Categories: "Personal", "Work", "Shopping", "Ideas"

3. **Screen 1: Notes List**:
   * Display notes in a `List` organized by `Section` (group by category)
   * Each section header should show category name with SF Symbol
   * Each note row should show:
     * Note title
     * Category badge/icon
     * Preview of content (first 50 characters)
   * Use custom view `NoteRowView` for note rows
   * Navigation title: "My Notes"
   * Swipe-to-delete functionality

4. **Screen 2: Add/Edit Note**:
   * Use `Form` with sections:
     * **Note Details**:
       * TextField for title (required)
       * TextField for content (multiline, optional)
     * **Category**:
       * Picker to select category
   * "Save" button that:
     * Validates title is not empty
     * Shows Alert if validation fails
     * Saves note and navigates back if successful
   * Use `@Binding` to allow editing existing notes
   * Navigation title: "New Note" or "Edit Note"

5. **Screen 3: Note Detail** (Optional):
   * Show full note content
   * Display category and date
   * "Edit" button that navigates to edit screen

6. **Persistence**:
   * Save notes array to `UserDefaults` using `JSONEncoder`
   * Load notes on app launch using `JSONDecoder`
   * Save automatically when notes are added, edited, or deleted

7. **Custom Views**:
   * Create `NoteRowView` for displaying notes in list
   * Create `CategoryBadgeView` for displaying category with color
   * Use SF Symbols for categories

8. **Bonus Challenges**:
   * Add search functionality to filter notes
   * Show note count per category
   * Add date formatting for createdDate
   * Implement note editing with `@Binding`

---

