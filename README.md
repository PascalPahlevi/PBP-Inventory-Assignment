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

# Assignment 9

## Can we retrieve JSON data without creating a model first? If yes, is it better than creating a model before retrieving JSON data?
Yes it is possible to retrieve JSON without creating a model first. However, whether it is bettere than creating a model beforehand depends on various factors. Ultimately however, for simpler and smaller tasks, it may be better to immediately parse the JSON but on the other hand, for more complex and larger JSON structures, it may be best to create a model beforehand.

## Explain the function of CookieRequest and explain why a CookieRequest instance needs to be shared with all components in a Flutter application.
A CookieRequest is used when making HTTP requests that involve coookies. Such requests could be adding and/or managing cookies before being sent to servers. Sharing it with all components may be useful because of multiple reasons:
1. Consistency in Cookie Handling: By using the same CookieRequest instance across components, you ensure that all HTTP requests are made uniformly with the same cookie-related configurations.
2. Avoiding Redundancy: Sharing a single CookieRequest instance avoids redundant setup or configurations in multiple places within the app.
3. Simplifying Maintenance: When modifications or updates are needed in how the app handles cookies in requests, having a shared CookieRequest instance simplifies maintenance.

## Explain the mechanism of fetching data from JSON until it can be displayed on Flutter.
Fetching data from JSON and displaying it in a Flutter application involves several steps:
1. We would first fetch teh JSON data by making an HTTP request then receive the JSON data as a response.
2. Using the 'dart:convert" library, we will able to parse the JSON data into Dart objects.
3. We can then, optionally, create a model to represent the data structure of the JSON data.
4. Finally, we can use flutter widgets to represent the parsed data.

## Explain the authentication mechanism from entering account data on Flutter to Django authentication completion and the display of menus on Flutter.

1. Build a Flutter UI that allows users to input their account credentials (e.g., username/email and password).
2. Retrieve user-entered data from form fields.
3. Use HTTP requests (commonly with packages like http or dio) to send the user's credentials securely to the Django backend.
4. Implement authentication mechanisms on the Django server using Django's authentication system (such as 'django.contrib.auth').
5. Validate the received credentials and authenticate the user against the stored credentials in the Django database.
6. After successful authentication, retrieve necessary data from Django.
7. Finally, based on the received data, dynamically build menus or UI components in Flutter to display functionalities accessible to the authenticated user.

## List all the widgets you used in this assignment and explain their respective functions.
Widgets Used:
1. ShopItem: Represents an item in the shop with properties like name, icon, and color.
2. ShopCard: Represents a card widget displaying a shop item and displays an icon, item name, and triggers actions when tapped based on the item's name.
3. LeftDrawer: Represents a drawer widget displayed on the left side of the app and contains a header with shop information and various list items for navigation.
4. ShopFormPage: Represents a form page for adding items to the shop, contains text fields for product name, price, description, save button and, sends a request to add a new product to the Django backend.
5. MyHomePage: Represents the main page of the app displaying a list of shop items, uses GridView.count to display a grid of ShopCard widgets and each ShopCard represents an action like viewing items, adding items, or logging out.
6. LoginPage: Represents the login page where users enter their credentials, uses TextField for username and password input and sends login request to Django backend using CookieRequest.
7. ProductPage: Represents a page displaying a list of products fetched from the Django backend.
8. MaterialApp: Root widget defining the MaterialApp for the entire app and initializes the app theme, providers, and sets the initial route.

## Explain how you implement the checklist above step by step! (not just following the tutorial).

__Create a login page in the Flutter project.__ <br>
```py
import 'package:pbp_inventory/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
  const LoginApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Login',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const LoginPage(),
    );
  }
}

class LoginPage extends StatefulWidget {
  const LoginPage({super.key});

  @override
  _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final TextEditingController _usernameController = TextEditingController();
  final TextEditingController _passwordController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    final request = context.watch<CookieRequest>();
    return Scaffold(
      appBar: AppBar(
        title: const Text('Login'),
      ),
      body: Container(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextField(
              controller: _usernameController,
              decoration: const InputDecoration(
                labelText: 'Username',
              ),
            ),
            const SizedBox(height: 12.0),
            TextField(
              controller: _passwordController,
              decoration: const InputDecoration(
                labelText: 'Password',
              ),
              obscureText: true,
            ),
            const SizedBox(height: 24.0),
            ElevatedButton(
              onPressed: () async {
                String username = _usernameController.text;
                String password = _passwordController.text;

                // Check credentials
                // TODO: Change the URL and don't forget to add a trailing slash (/) at the end of the URL!
                // To connect the Android emulator to Django on localhost,
                // use the URL http://10.0.2.2/
                final response =
                    await request.login("http://127.0.0.1:8000/auth/login/", {
                  'username': username,
                  'password': password,
                });

                if (request.loggedIn) {
                  String message = response['message'];
                  String uname = response['username'];
                  Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(builder: (context) => MyHomePage()),
                  );
                  ScaffoldMessenger.of(context)
                    ..hideCurrentSnackBar()
                    ..showSnackBar(
                        SnackBar(content: Text("$message Welcome, $uname.")));
                } else {
                  showDialog(
                    context: context,
                    builder: (context) => AlertDialog(
                      title: const Text('Login Failed'),
                      content: Text(response['message']),
                      actions: [
                        TextButton(
                          child: const Text('OK'),
                          onPressed: () {
                            Navigator.pop(context);
                          },
                        ),
                      ],
                    ),
                  );
                }
              },
              child: const Text('Login'),
            ),
          ],
        ),
      ),
    );
  }
}
```

As seen above, the code simply creats a functional login page, allowing users to access the app. In order to do so, the login page was made to connect to a previously created Django website, where data on registered users already exist, Hence, using 'import package:pbp_django_auth/pbp_django_auth.dart' and 'import package:provider/provider.dart', users would be able to login to the app with an account that was created on the Django website.

__Integrate the Django authentication system with the Flutter project__ <br>
In order to do this, a few additions had to be made in the code for the Django application. For instance, a new app going by authentication was created where in this line of code was added to 'authentication/views.py':
```py
from django.shortcuts import render
from django.contrib.auth import authenticate, login as auth_login
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Successful login status.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login successful!"
                # Add other data if you want to send data to Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login failed, account disabled."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login failed, check email or password again."
        }, status=401)
```

On top of that another 'urls.py' file had to be created where in URL routing was done as seen below:
```py
from django.urls import path
from authentication.views import login

app_name = 'authentication'

urlpatterns = [
    path('login/', login, name='login'),
]
```
This was done in the previously created Django application, only as a setup, so that integrating Django into the Flutter app will run smoothly. To actually integrate it, a few packages needed to be added before hand, those being 'provider' and 'pbp_django_auth'. Once this was done, the root widget had to be slightly modified as seen below:
```py
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return Provider(
        create: (_) {
          CookieRequest request = CookieRequest();
          return request;
        },
        child: MaterialApp(
          title: 'Flutter Demo',
          theme: ThemeData(
            colorScheme: ColorScheme.fromSeed(seedColor: Colors.indigo),
            useMaterial3: true,
          ),
          home: LoginPage(),
        ));
  }
}
```
__Create a custom model according to your Django application project.__ <br>
In creating the custom model, the JSON data created from the Django application was required through the JSON endpoint. Afterords, the data was pasted into the 'Quicktype' website, converting the JSON into the Dart language. The model can be seen below:
```py
// To parse this JSON data, do
//
//     final product = productFromJson(jsonString);

import 'dart:convert';

List<Product> productFromJson(String str) =>
    List<Product>.from(json.decode(str).map((x) => Product.fromJson(x)));

String productToJson(List<Product> data) =>
    json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class Product {
  String model;
  int pk;
  Fields fields;

  Product({
    required this.model,
    required this.pk,
    required this.fields,
  });

  factory Product.fromJson(Map<String, dynamic> json) => Product(
        model: json["model"],
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
      );

  Map<String, dynamic> toJson() => {
        "model": model,
        "pk": pk,
        "fields": fields.toJson(),
      };
}

class Fields {
  String name;
  DateTime dateAdded;
  int price;
  String description;
  int user;

  Fields({
    required this.name,
    required this.dateAdded,
    required this.price,
    required this.description,
    required this.user,
  });

  factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        name: json["name"],
        dateAdded: DateTime.parse(json["date_added"]),
        price: json["price"],
        description: json["description"],
        user: json["user"],
      );

  Map<String, dynamic> toJson() => {
        "name": name,
        "date_added":
            "${dateAdded.year.toString().padLeft(4, '0')}-${dateAdded.month.toString().padLeft(2, '0')}-${dateAdded.day.toString().padLeft(2, '0')}",
        "price": price,
        "description": description,
        "user": user,
      };
}
```
__Create a page containing a list of all items available at the JSON endpoint in Django that you have deployed.__
__Display the name, amount, and description of each item on this page.__ <br>
To create this page, a new dart file was created by the name of 'list_product.dart' which is used to display all the items added. This page will also display the name, amount, and description of each item on the page which can be seen in the code below:
```py
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';
import 'package:pbp_inventory/models/product.dart';
import 'package:pbp_inventory/widgets/left_drawer.dart';

class ProductPage extends StatefulWidget {
  const ProductPage({Key? key}) : super(key: key);

  @override
  _ProductPageState createState() => _ProductPageState();
}

class _ProductPageState extends State<ProductPage> {
  Future<List<Product>> fetchProduct() async {
    // TODO: Change the URL to your Django app's URL. Don't forget to add the trailing slash (/) if needed.
    var url = Uri.parse('http://127.0.0.1:8000/json/');
    var response = await http.get(
      url,
      headers: {"Content-Type": "application/json"},
    );

    // decode the response to JSON
    var data = jsonDecode(utf8.decode(response.bodyBytes));

    // convert the JSON to Product object
    List<Product> list_product = [];
    for (var d in data) {
      if (d != null) {
        list_product.add(Product.fromJson(d));
      }
    }
    return list_product;
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: const Text('Product'),
        ),
        drawer: const LeftDrawer(),
        body: FutureBuilder(
            future: fetchProduct(),
            builder: (context, AsyncSnapshot snapshot) {
              if (snapshot.data == null) {
                return const Center(child: CircularProgressIndicator());
              } else {
                if (!snapshot.hasData) {
                  return const Column(
                    children: [
                      Text(
                        "No product data available.",
                        style:
                            TextStyle(color: Color(0xff59A5D8), fontSize: 20),
                      ),
                      SizedBox(height: 8),
                    ],
                  );
                } else {
                  return ListView.builder(
                      itemCount: snapshot.data!.length,
                      itemBuilder: (_, index) => Container(
                            margin: const EdgeInsets.symmetric(
                                horizontal: 16, vertical: 12),
                            padding: const EdgeInsets.all(20.0),
                            child: Column(
                              mainAxisAlignment: MainAxisAlignment.start,
                              crossAxisAlignment: CrossAxisAlignment.start,
                              children: [
                                Text(
                                  "${snapshot.data![index].fields.name}",
                                  style: const TextStyle(
                                    fontSize: 18.0,
                                    fontWeight: FontWeight.bold,
                                  ),
                                ),
                                const SizedBox(height: 10),
                                Text("${snapshot.data![index].fields.price}"),
                                const SizedBox(height: 10),
                                Text(
                                    "${snapshot.data![index].fields.description}")
                              ],
                            ),
                          ));
                }
              }
            }));
  }
}
```







