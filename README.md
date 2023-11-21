# pbp_inventory

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

# Assignment 7

## What are the main differences between stateless and stateful widget in Flutter?
In Flutter, widgets can be categorized into two, those being stateless and stateful widgets. Some of the main differences between them are:
1. Stateful widgets allow users to change their internal state while on the other hand stateless widgets do not.
2. Stateful widgets require a separate 'state' class in order to manage their mutable state.
3. Stateless widgets are much simpler and lightweight compared to stateful widgets as they do not need to maintain state.
4. Stateless widgets do not depened on internal state changes when rendering hence making them more efficient.

## Explain all widgets that you used in this assignment.
1. Scaffold : Provides the basic structure of the app.
2. AppBar : Displays a bar on top of the screen that contains the app's title.
3. SingleChildScrollView: Provides a scrolling  functionality for other widgets, if in any case they do not fit on the screen.
4. Text: A widget used to display text on the screen that displays the app's title.
5. Padding: Adds padding to the column widget.
6. Column: Displays the contents in a vertical arrangement.
7. GridView.count: A grid with a fixed number of columns that displays the 'ShopCard' widgets in a grid.
8. Material: Provides a rectangular area with a material design background.
9. InkWell: A widget that provides a touch response.
10. Icon: Displays an icon.

##  Explain how you implemented the checklist above step-by-step (not just following the tutorial).
__Create 3 simple buttons with icon and text to: <br>
 View the list of items (View Items) <br>
 Add Item (Add Item) <br>
 Logout (Logout)__ <br>

Before starting work on the widgets, I initially started by creating the class ShopItem as shown below:

```py
class ShopItem {
  final String name;
  final IconData icon;
  final Color color;

  ShopItem(this.name, this.icon, this.color);
}
```

This class basically determines the variables that will be used when making the widget class alongside their specific attributes. After this was done, I was able to start working on the widget class as shown below:

```py
Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'PBP Inventory',
        ),
      ),
      body: SingleChildScrollView(
        // Scrolling wrapper widget
        child: Padding(
          padding: const EdgeInsets.all(10.0), // Set padding for the page
          child: Column(
            // Widget to display children vertically
            children: <Widget>[
              const Padding(
                padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                // Text widget to display text with center alignment and appropriate style
                child: Text(
                  'The Krusty Krab', // Text indicating the shop name
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
              // Grid layout
              GridView.count(
                // Container for our cards.
                primary: true,
                padding: const EdgeInsets.all(20),
                crossAxisSpacing: 10,
                mainAxisSpacing: 10,
                crossAxisCount: 3,
                shrinkWrap: true,
                children: items.map((ShopItem item) {
                  // Iteration for each item
                  return ShopCard(item);
                }).toList(),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
Essentially, this widget creates a navbar which would be placed on top of the app page that displays text as well as a separate text widget that places the name of the app in the center of the page. Besides that, to display the buttons, a grid layout was used to create cards in which the buttons will be placed, complete with their respective icons, names, and colors. However, to actually display the specified contents in the cards, another class was made that extended the widget which can be seen below:
```py
class MyHomePage extends StatelessWidget {
  MyHomePage({Key? key}) : super(key: key);

  final List<ShopItem> items = [
    ShopItem("View Items", Icons.checklist, Colors.red),
    ShopItem("Add Items", Icons.add_shopping_cart, Colors.green),
    ShopItem("Logout", Icons.logout, Colors.blue),
  ];
```
This class consists of a list that would eventually become the contents of the card consisting of the string, the icon, and the color.

__Create a Snackbar with the following texts: <br>
 "You clicked the View Items button" when the View Items button is clicked. <br>
 "You clicked the Add Item button" when the Add Item button is clicked. <br>
 "You clicked the Logout button" when the Logout button is clicked.__ <br>

 To implement this feature in the app, the class ShopCard was created which extended the stateless widget as seen below:
 ```py
class ShopCard extends StatelessWidget {
  final ShopItem item;

  const ShopCard(this.item, {Key? key}); // Constructor

  @override
  Widget build(BuildContext context) {
    return Material(
      color: item.color,
      child: InkWell(
        // Responsive touch area
        onTap: () {
          // Show a SnackBar when clicked
          ScaffoldMessenger.of(context)
            ..hideCurrentSnackBar()
            ..showSnackBar(SnackBar(
                content: Text("You clicked the ${item.name} button!")));
        },
        child: Container(
          // Container to hold Icon and Text
          padding: const EdgeInsets.all(8),
          child: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Icon(
                  item.icon,
                  color: Colors.white,
                  size: 30.0,
                ),
                const Padding(padding: EdgeInsets.all(3)),
                Text(
                  item.name,
                  textAlign: TextAlign.center,
                  style: const TextStyle(color: Colors.white),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}
```

This class was created so to ensure that the buttons itself actually worked as seen by the use of 'onTap: () {...}' which makes it so that when the buttons are clicked, a message will pop up saying that the button was clicked. This message was also made so that it is placed inside a container.

# Assignment 8

## Explain the difference between Navigator.push() and Navigator.pushReplacement(), accompanied by examples of the correct usage of both methods!
Navigator.push() is used to navigate from one screen to another by pushing the new screen on top of the stack. This allows us to still go back to previous screens. Navigator.pushReplacement() on the other hand is also used to navigate from one screen to another, however, it replaces the current screen in the stack with a new one.

## Explain each layout widget in Flutter and their respective usage contexts!
1. Container
Usage: A versatile widget used for layout, decoration, alignment, and constraints.
Context: It's the most basic and flexible widget used to contain other widgets, providing control over their appearance and layout properties.
2. Row
Usage: Arranges its children widgets horizontally in a single line.
Context: Useful for creating horizontal layouts, such as button rows, navigation bars, or any elements that need to be placed side by side.
3. Column
Usage: Arranges its children widgets vertically in a single line.
Context: Perfect for creating vertical layouts, like forms, lists, or any stacked elements.
4. Stack
Usage: Stacks its children widgets on top of each other.
Context: Ideal for overlaying widgets, creating complex UIs where widgets need to overlap or be positioned at specific coordinates within the screen.
5. ListView
Usage: Displays a scrollable list of children widgets.
Context: Great for long lists of data or dynamic content that exceeds the screen size, providing scrolling functionality.
6. GridView
Usage: Displays a scrollable grid of children widgets in rows and columns.
Context: Perfect for arranging items in a grid layout, such as image galleries, product displays, or any structured content.
7. Wrap
Usage: Arranges its children widgets in multiple lines if needed.
Context: Useful when you have a dynamic number of elements and want them to flow across lines automatically instead of overflowing the available space.
8. Expanded
Usage: Expands a child widget to fill the available space along the main axis in a Row, Column, or Flex.
Context: Helps in controlling how much space a child widget takes within a layout.
9. SizedBox
Usage: Creates a box with a specific size or enforces specific constraints on its child widget.
Context: Useful for adding fixed sizes or constraints to widgets, like adding spacing between elements or enforcing a certain size.
10. ConstrainedBox
Usage: Applies additional constraints to its child widget.
Context: Helpful for imposing specific constraints, such as minimum and maximum sizes, on its child widget.

## List the form input elements you used in this assignment and explain why you used these input elements!
There are three form input elements that were used in the assignment:
1. Product Name Field: This input element collects the name of the product and it is needed to allow users to input the name of the product they wish to add.

2. Amount Field: This input element collects the quantity of the product and is needed to ensure that users are able to determine the amount of the product available in the inventory.

3. Description Field: This input element collects the description of the product and is needed to allow users to describe the product they wish to add into the inventory.

## How is clean architecture implemented in a Flutter application?
Clean architecture in a Flutter application involves restructuring the app's code, separating them into different layers/folders based on which they are categorized in. This makes it easier to maintain the code as well as test it.

## Explain how you implemented the checklist above step-by-step! (not just following the tutorial)

__Use at least three input elements: name, amount, description. Add input elements according to the model in your Django assignment.__

To do this, I had to create new variables as shown below:
```py
class _ShopFormPageState extends State<ShopFormPage> {
  final _formKey = GlobalKey<FormState>();
  String _name = "";
  int _amount = 0;
  String _description = "";
```

__Have a Save button. <br>
 Validate each input element in the form with the following requirements: <br>
 Each input element must not be empty. <br>
 Each input element must contain data of the same data type as its model attribute.__

All of the tasks above can be seen in the code below:

```py
@override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Center(
            child: Text(
              'Add Item Form',
            ),
          ),
          backgroundColor: Colors.indigo,
          foregroundColor: Colors.white,
        ),
        body: Form(
            key: _formKey,
            child: SingleChildScrollView(
                child: Column(
                    crossAxisAlignment: CrossAxisAlignment.start,
                    children: [
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Product Name",
                        labelText: "Product Name",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _name = value!;
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Name cannot be empty!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Amount",
                        labelText: "Amount",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _amount = int.parse(value!);
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Amount cannot be empty!";
                        }
                        if (int.tryParse(value) == null) {
                          return "Amount must be a number!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                      decoration: InputDecoration(
                        hintText: "Description",
                        labelText: "Description",
                        border: OutlineInputBorder(
                          borderRadius: BorderRadius.circular(5.0),
                        ),
                      ),
                      onChanged: (String? value) {
                        setState(() {
                          _description = value!;
                        });
                      },
                      validator: (String? value) {
                        if (value == null || value.isEmpty) {
                          return "Description cannot be empty!";
                        }
                        return null;
                      },
                    ),
                  ),
                  Align(
                    alignment: Alignment.bottomCenter,
                    child: Padding(
                      padding: const EdgeInsets.all(8.0),
                      child: ElevatedButton(
                        style: ButtonStyle(
                          backgroundColor:
                              MaterialStateProperty.all(Colors.indigo),
                        ),
                        onPressed: () {
                          if (_formKey.currentState!.validate()) {
                            showDialog(
                              context: context,
                              builder: (context) {
                                return AlertDialog(
                                  title:
                                      const Text('Product Succesfully saved'),
                                  content: SingleChildScrollView(
                                    child: Column(
                                      crossAxisAlignment:
                                          CrossAxisAlignment.start,
                                      children: [
                                        Text('Name: $_name'),
                                        Text('Amount: $_amount'),
                                        Text('Description: $_description')
                                      ],
                                    ),
                                  ),
                                  actions: [
                                    TextButton(
                                      child: const Text('OK'),
                                      onPressed: () {
                                        Navigator.pop(context);
                                      },
                                    ),
                                  ],
                                );
                              },
                            );
                            _formKey.currentState!.reset();
                          }
                        },
                        child: const Text(
                          "Save",
                          style: TextStyle(color: Colors.white),
                        ),
                      ),
                    ),
                  ),
                ]))));
  }
```
 
__Direct users to the new item addition form page when clicking the Add Item button on the main page. <br>
 Display data as entered in the form in a pop-up after clicking the Save button on the new item addition page.__

In order to direct users to the new item addition the code below was added in the ShopCard Class in menu.dart:
```py
if (item.name == "Add Items") {
            Navigator.push(context,
                MaterialPageRoute(builder: (context) => const ShopFormPage()));
          }
```

With this code, when the Add Items button is clicked, it will redirect to the ShopFormPage. In the case of the popup the code below was added in shoplist_form.dart:
```py
onPressed: () {
                          if (_formKey.currentState!.validate()) {
                            showDialog(
                              context: context,
                              builder: (context) {
                                return AlertDialog(
                                  title:
                                      const Text('Product Succesfully saved'),
                                  content: SingleChildScrollView(
                                    child: Column(
                                      crossAxisAlignment:
                                          CrossAxisAlignment.start,
                                      children: [
                                        Text('Name: $_name'),
                                        Text('Amount: $_amount'),
                                        Text('Description: $_description')
                                      ],
                                    ),
                                  ),
                                  actions: [
                                    TextButton(
                                      child: const Text('OK'),
                                      onPressed: () {
                                        Navigator.pop(context);
                                      },
                                    ),
                                  ],
                                );
                              },
                            );
                            _formKey.currentState!.reset();
                          }
                        },
```
With this code, if the save button is clicked, a popup containing information on the product, amount, and description will appear.

__Create a drawer in the application with the following requirements: <br>
 The drawer must have at least two options: Home and Add Item. <br>
 When choosing the Home option, the application will direct the user to the main page. <br>
 When choosing the Add Item option, the application will direct the user to the new item addition form page.__

To implement the left drawer the code belows was implemented in a new file with the name left_drawer.dart:
```py
import 'package:flutter/material.dart';
import 'package:pbp_inventory/screens/menu.dart';
import 'package:pbp_inventory/screens/shoplist_form.dart';

class LeftDrawer extends StatelessWidget {
  const LeftDrawer({super.key});

  @override
  Widget build(BuildContext context) {
    return Drawer(
      child: ListView(
        children: [
          const DrawerHeader(
            decoration: BoxDecoration(
              color: Colors.indigo,
            ),
            child: Column(
              children: [
                Text(
                  'The Krusty Krab',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 30,
                    fontWeight: FontWeight.bold,
                    color: Colors.white,
                  ),
                ),
                Padding(padding: EdgeInsets.all(10)),
                Text(
                  'Write all your shopping needs here!',
                  textAlign: TextAlign.center,
                  style: TextStyle(
                    fontSize: 15,
                    fontWeight: FontWeight.normal,
                    color: Colors.white,
                  ),
                ),
              ],
            ),
          ),
          ListTile(
            leading: const Icon(Icons.home_outlined),
            title: const Text('Home Page'),
            // redirect to MyHomePage
            onTap: () {
              Navigator.pushReplacement(
                context,
                MaterialPageRoute(
                  builder: (context) => MyHomePage(),
                ),
              );
            },
          ),
          ListTile(
            leading: const Icon(Icons.add_shopping_cart),
            title: const Text('Add Items'),
            // redirect to ShopFormPage
            onTap: () {
              Navigator.pushReplacement(
                context,
                MaterialPageRoute(
                  builder: (context) => const ShopFormPage(),
                ),
              );
            },
          ),
        ],
      ),
    );
  }
}
```


