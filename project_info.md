import 'package:flutter/material.dart'; 
import 'package:file_picker/file_picker.dart'; 

void main() { 
runApp(const CareerLensApp()); 
} 

const Color purple = Color(0xFF7554E8); 
const Color pink = Color(0xFFFF83B5); 
const Color ink = Color(0xFF29243D); 
const Color pale = Color(0xFFF8F6FF); 
const Color muted = Color(0xFF858096); 

class CareerLensApp extends StatelessWidget { 
const CareerLensApp({super.key}); 

@override 
Widget build(BuildContext context) { 
return MaterialApp( 
title: 'Career Lens', 
debugShowCheckedModeBanner: false, 
theme: ThemeData( 
useMaterial3: true, 
scaffoldBackgroundColor: pale, 
colorScheme: ColorScheme.fromSeed(seedColor: purple), 
fontFamily: 'Roboto', 
), 
home: const AuthScreen(), 
); 
} 
} 

// ---------------- AUTH SCREEN ---------------- 

class AuthScreen extends StatefulWidget { 
const AuthScreen({super.key}); 

@override 
State<AuthScreen> createState() => _AuthScreenState(); 
} 

class _AuthScreenState extends State<AuthScreen> { 
final emailController = TextEditingController(); 
final passwordController = TextEditingController(); 
final nameController = TextEditingController(); 

bool isLogin = true; 
bool obscurePassword = true; 

@override 
void dispose() { 
emailController.dispose(); 
passwordController.dispose(); 
nameController.dispose(); 
super.dispose(); 
} 

void continueToApp() { 
if (emailController.text.trim().isEmpty || 
passwordController.text.trim().isEmpty) { 
ScaffoldMessenger.of(context).showSnackBar( 
const SnackBar( 
content: Text('Please enter your email and password'), 
), 
); 
return; 
} 

if (!isLogin && nameController.text.trim().isEmpty) { 
ScaffoldMessenger.of(context).showSnackBar( 
const SnackBar(content: Text('Please enter your name')), 
); 
return; 
} 

Navigator.pushReplacement( 
context, 
MaterialPageRoute( 
builder: (_) => const WelcomeScreen(), 
), 
); 
} 

@override 
Widget build(BuildContext context) { 
return Scaffold( 
body: SafeArea( 
child: Center( 
child: SingleChildScrollView( 
padding: const EdgeInsets.all(24), 
child: ConstrainedBox( 
constraints: const BoxConstraints(maxWidth: 430), 
child: Column( 
crossAxisAlignment: CrossAxisAlignment.start, 
children: [ 
Center( 
child: Container( 
height: 82, 
width: 82, 
decoration: BoxDecoration( 
gradient: const LinearGradient( 
colors: [purple, pink], 
), 
borderRadius: BorderRadius.circular(25), 
), 
child: const Icon( 
Icons.auto_awesome, 
color: Colors.white, 
size: 42, 
), 
), 
), 
const SizedBox(height: 22), 
const Center( 
child: Text( 
'Career Lens', 
style: TextStyle( 
fontSize: 31, 
fontWeight: FontWeight.bold, 
color: ink, 
), 
), 
), 
const SizedBox(height: 8), 
const Center( 
child: Text( 
'Discover your potential. Shape your future.', 
textAlign: TextAlign.center, 
style: TextStyle(color: muted), 
), 
), 
const SizedBox(height: 36), 
Text( 
isLogin ? 'Welcome back!' : 'Create your account', 
style: const TextStyle( 
fontSize: 25, 
fontWeight: FontWeight.bold, 
color: ink, 
), 
),
