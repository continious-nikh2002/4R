# 4R
main.dart

import 'package:firebase_core/firebase_core.dart';
import 'package:flutter/material.dart' ;
import 'package:my_app/Screens/login_screen.dart';
import 'package:my_app/screens/authentication/phoneauth_screen.dart';
import 'package:my_app/screens/splash%20screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MyApp());
}
class MyApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    return FutureBuilder(
      // Replace the 3 second delay with your initialization code:
      future: Future.delayed(Duration(seconds: 3)), //after three
      builder: (context, AsyncSnapshot snapshot) {
        // Show splash screen while waiting for app resources to l
        if (snapshot.connectionState == ConnectionState.waiting) {
          return MaterialApp(
              debugShowCheckedModeBanner: false,
              home: SplashScreen());
        } else {
          // Loading is done, return the app:
          return MaterialApp(
            debugShowCheckedModeBanner: false,
            theme: ThemeData(
                primaryColor: Colors.cyan.shade900,
                fontFamily: 'Lato'
          ),
            home: LoginScreen(),
            routes: {

              LoginScreen.id: (context) =>  LoginScreen(),
             PhoneAuthScreen.id: (context) => PhoneAuthScreen(),

           },
          );
        }
      },
    );
  }
}
