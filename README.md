## Hive

flutter packages pub run build_runner build

Hive is a NoSQL database solution for Flutter applications. It's a fast, efficient, and lightweight alternative to traditional databases like SQLite. Hive stores data in files on disk, making it ideal for small and medium-sized projects.

# To use Hive in your Flutter app, you need to follow these steps:

# 1.Add the Hive dependency to your pubspec.yaml file:

dependencies:

hive: ^2.2.3
hive_flutter: ^1.1.0
build_runner: ^2.3.3
hive_generator: ^2.0.0
path_provider: ^2.0.14

This will include the Hive core library and the Hive Flutter adapter, which you need to use Hive with Flutter.


# 2.Initialize Hive in your app's main() function:

await Hive.initFlutter();
This initializes Hive with the default settings. You can also provide a path to the directory where you want to store your Hive data files:

final appDocumentDirectory = await getApplicationDocumentsDirectory();
await Hive.initFlutter(appDocumentDirectory.path);


# 3.Generate a model class: 
Define a model class that will be used to store data in Hive. The class should extend HiveObject and have annotations from the hive package. 
For example:

import 'package:hive/hive.dart';

part 'person.g.dart';

@HiveType(typeId: 0)
class Person extends HiveObject {
@HiveField(0)
String name;

@HiveField(1)
String fatherName;

@HiveField(2)
String motherName;

Person({required this.name, required this.fatherName, required this.motherName});
}

Note: the part 'person.g.dart'; line is used to generate a .g.dart file that contains the implementation for the HiveObject and TypeAdapter classes for this model.


# 4.Generate a TypeAdapter: 
A TypeAdapter is used to tell Hive how to convert an instance of the model class to and from bytes that can be stored in the database. To generate a TypeAdapter for the Person model, run the following command in the terminal:

flutter packages pub run build_runner build

This will generate the person.g.dart file that contains the implementation for the PersonAdapter class.

# 5.Register your data model classes with Hive:

Hive.registerAdapter(MyDataModelAdapter());
You need to create a HiveAdapter for each data model class that you want to store in Hive. This adapter maps the fields in your data model to Hive boxes and makes it possible to store and retrieve instances of your data model.


# 6.Open a Hive box:

final myBox = await Hive.openBox('myBox');
Hive stores data in boxes. A box is a collection of key-value pairs, where the keys are strings and the values can be any data type that Hive supports. When you open a box, Hive loads the data from the box's data file on disk (if it exists) and makes it available to your app.

# 7.Save data to a Hive box:

myBox.put('myKey', myData);
This saves myData to the box under the key 'myKey'. You can save any data type that Hive supports.

# 8.Retrieve data from a Hive box:

final myData = myBox.get('myKey');
This retrieves the data from the box that is stored under the key 'myKey'. If the key doesn't exist, null is returned.

# 9.Listen for changes in a Hive box:

myBox.listenable().addListener(() {
// Handle box changes here
});
This sets up a listener that is called whenever the data in the box changes. You can use this to update your UI when the data changes.

# 10.Close a Hive box:

await myBox.close();
This closes the box and saves its data to the data file on disk. You should always close a box when you're done using it.

# 11.Close Hive when your app exits:

await Hive.close();
This closes all open boxes and releases any resources that Hive is using. You should always close Hive when your app exits.


# Sure, here is the documentation for how to view stored data in Hive:

To view stored data in Hive, you can either use the Hive Visualizer or access the files directly in your app's data directory.

 # 1.Hive Visualizer:

1.Install the Hive Visualizer package by running the command "flutter pub global activate hive_visualizer" in your terminal.

2.Once the package is installed, run the command "flutter pub global run hive_visualizer" to start the visualizer.

3.In the visualizer, click on "Open Box" and select the box that you want to view data for.

4.You will now see all the data stored in the selected box.

  # 2.Directly accessing the files:

1.Get the app's data directory using the getApplicationDocumentsDirectory() function from the path_provider package.

2.In the data directory, you will find a folder named app_flutter. This is where Hive stores its files.

3.Inside the app_flutter folder, you will find a file for each box that you have created. The file name will be the name of the box with a .hive extension.

4.To view the contents of a file, you can use any text editor or SQLite browser that supports the Hive format.

5.Open the file using the text editor or SQLite browser to view the data stored in it.

Note: Directly accessing the files should be done with caution and only for debugging purposes. Editing the files directly can corrupt the data and cause unexpected behavior. It is recommended to use the Hive Visualizer to view and manage the data stored in Hive.

 # 3.Android Studio's Device File Explorer:

1.Open Android Studio and select the "View" menu from the toolbar.

2.Choose "Tool Windows" and then "Device File Explorer."

3.Make sure your emulator or device is connected to Android Studio and visible in the "Device File Explorer" window.

4.In the Device File Explorer, navigate to the path you got (/data/user/0/com.example.hive_demo/app_flutter).

5.You should now see your data file(s) there.

Note: If you can't find the "Device File Explorer" option in the "Tool Windows" menu, it might not be enabled. In that case, go to the "Settings/Preferences" menu, select "Plugins," search for "Android Support," and make sure the "Android Support" plugin is installed and enabled.