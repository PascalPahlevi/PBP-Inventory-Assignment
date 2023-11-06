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

Before starting work on the widgets, I initially started by craeting the class ShopItem as shown below:
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



